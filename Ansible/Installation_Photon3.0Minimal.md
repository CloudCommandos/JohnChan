Use Root User
```bash
sudo su -
```

## Ansible
Install Ansible through pip
```bash
tdnf update
tdnf install python3-pip
pip3 --timeout=1000 install ansible
```


## Ansible AWX
Install Ansible through pip
```bash
tdnf update
tdnf install python3-pip
pip3 --timeout=1000 install ansible
```

Install Docker-Compose
```bash
curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose version
```

Install Node and NPM
```bash
tdnf install nodejs
npm install npm --global
```

Install git
```bash
tdnf install git
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
cd awx/installer/
```

Generate a secret key
```bash
head /dev/urandom | tr -dc A-Za-z0-9 | head -c 30 ; echo ''
```

Edit `inventory` file
```bash
nano inventory
```

Assign the generated secret key to the `secret_key` variable. Configure other parameters where applicable.
```yaml
...
secret_key=gQ5FYKzMORpyRrPO2N7y7h0qODQHIU
...
```

Install with Ansible
```bash
ansible-playbook -i inventory install.yml
```
