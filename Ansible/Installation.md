Use Root User
```bash
sudo su -
```

## Ansible
Install Ansible through pip
```bash
apt update
apt install -y python3-pip
pip3 install ansible
```


## Ansible AWX
Install Ansible through pip
```bash
apt update
apt install -y python3-pip
pip3 install ansible
```

Install Docker-Compose
```bash
curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose version
```

Install Node and NPM
```bash
apt install -y nodejs npm
npm install npm --global
```

Install git, pwgen, and vim
```bash
apt install -y git pwgen vim
pip3 install requests==2.14.2
```

Install Docker-Compose Python Module that matches your Docker-Compose Version
```bash
pip3 install docker-compose==1.26.2
```

Make a directory for Ansible AWX git repository, then clone it
```bash
mkdir -p /opt/awx
cd /opt/awx
git clone --depth 50 https://github.com/ansible/awx.git
```
