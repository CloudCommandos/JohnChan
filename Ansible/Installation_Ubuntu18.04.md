Use Root User
```bash
sudo su -
```
## Ansible Python3
```bash
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```


## Ansible Python3 (Alternative)
Install Ansible through pip3
```bash
apt update
apt install -y python3-pip
pip3 --timeout=1000 install ansible
```


## Ansible AWX
Install Ansible through pip
```bash
apt update
apt install -y python3-pip
pip3 install ansible
```

Install pip docker-py
```bash
pip3 install docker-py
```

Install Docker-Compose
```bash
apt install docker-compose
```

Install Node and NPM
```bash
apt install -y nodejs npm
npm install npm --global
```

Install git and pwgen
```bash
apt install -y git pwgen
```

Install Docker-Compose Python Module that matches your Docker-Compose Version
```bash
pip3 install docker-compose==1.17.1
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
pwgen -N 1 -s 30
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
