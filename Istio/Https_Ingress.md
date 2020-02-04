## Prerequisite
Make sure that your Istio setup was initialized using the default profile with TLS flags.
Secret Discovery Service (SDS) allows Istio to retrieve certs from K8s secrets and inject them into your containers.
```bash
istioctl manifest apply \
  --set values.gateways.istio-ingressgateway.sds.enabled=true \
  --set values.global.k8sIngress.enabled=true \
  --set values.global.k8sIngress.enableHttps=true \
  --set values.global.k8sIngress.gatewayName=ingressgateway
```

## Side Car Injection
Option 1: Label namespace accordingly for the Istio sidecar injector to inject sidecar containers into the corresponding pods  
```bash
kubectl label namespace <namespace> istio-injection=enabled
```
or  
Option 2: Inject manually for each deployment
```bash
kubectl apply -f <(istioctl kube-inject -f your_deployment.yaml)
```

## Create Istio Gateway
```bash
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: jay-admin-gateway
  namespace: jay-admin
spec:
  selector:
    istio: ingressgateway # use Istio default gateway implementation
  servers:
  - port:
      number: 443
      name: https
      protocol: HTTPS
    hosts:
    - "confluence.sunnyburst.com"
EOF
```

## Create Virtual Service
```bash
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: confluence
  namespace: jay-admin
spec:
  hosts:
  - "confluence.sunnyburst.com"
  gateways:
  - jay-admin-gateway
  http:
  - match:
    - uri:
        prefix: /
    route:
    - destination:
        port:
          number: 8090
        host: confluence
EOF
```

## TLS Cert Creation
Create root cert
```bash
apt-get install -y openssl
openssl req -x509 -sha256 -nodes -days 99999 -newkey rsa:2048 -subj '/O=rootca Inc./CN=istio' -keyout istio_ca.key -out istio_ca.crt
```

Create self-signed certs for istio ingress gateway and your application (e.g. Confluence)
```bash
openssl req -out istio-ingressgateway.csr -newkey rsa:2048 -nodes -keyout istio-ingressgateway.key -subj "/CN=istio-ingressgateway/O=istio"
openssl x509 -req -days 99999 -CA istio_ca.crt -CAkey istio_ca.key -set_serial 0 -in istio-ingressgateway.csr -out istio-ingressgateway.crt

openssl req -out confluence.sunnyburst.com.csr -newkey rsa:2048 -nodes -keyout confluence.sunnyburst.com.key -subj "/CN=confluence.sunnyburst.com/O=confluence"
openssl x509 -req -days 99999 -CA istio_ca.crt -CAkey istio_ca.key -set_serial 0 -in confluence.sunnyburst.com.csr -out confluence.sunnyburst.com.crt
```

Create k8s secret with self-signed cert for Istio ingress gateway
```bash
kubectl create -n istio-system secret tls istio-ingressgateway-certs \
--key istio-ingressgateway.key \
--cert istio-ingressgateway.crt
```

Create k8s secret with self-signed cert for confluence (or any other app)
```bash
kubectl create -n istio-system secret tls confluence-gateway-cert \
--key confluence.sunnyburst.com.key \
--cert confluence.sunnyburst.com.crt
```

## Checks
Optional: Check missing ingress gateway listeners
```bash
istioctl proxy-config listeners -n istio-system <your_istio_ingressgateway_podname>
```
E.g. if port 443 is missing then there is an error in the istio-proxy container of your istio-ingressgateway pod. You can see the logs of the container for more info.  

Optional: Check ingress gateway listeners in detail
```bash
istioctl pc listeners -n istio-system -o json <your_istio_ingressgateway_podname>
```

For HTTPS workloads make sure that their K8s Service Objects have port name prefixed with `http`. E.g.:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: confluence
  namespace: jay-admin
  labels:
    app: confluence
spec:
  ports:
    - name: http-query
      protocol: TCP
      port: 8090
      targetPort: 8090
  selector:
    app: confluence
```
