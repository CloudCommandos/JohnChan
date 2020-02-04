### Install Istio
Download the latest Istio release
```bash
cd $HOME
curl -L https://istio.io/downloadIstio | sh -
```

Option 1: Temporarily add istioctl client into your path  
```bash
cd istio-1.4.3
export PATH=$PWD/bin:$PATH
```
or  
Option 2: Add istioctl client into your account's path persistently
```bash
nano ~/.profile

   #...
   export PATH=$PATH:$HOME/istio-1.4.3/bin
```

Install the default profile of Istio into the k8s cluster with tls flags.  
SDS allows Istio to retrieve certs from K8s secrets and inject them into your containers.
```bash
istioctl manifest apply \
  --set values.gateways.istio-ingressgateway.sds.enabled=true \
  --set values.global.k8sIngress.enabled=true \
  --set values.global.k8sIngress.enableHttps=true \
  --set values.global.k8sIngress.gatewayName=ingressgateway
```
