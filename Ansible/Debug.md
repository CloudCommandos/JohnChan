To verify the variables of your host group
```bash
ansible -m debug -a 'var=hostvars[inventory_hostname]' YOUR_GROUP_NAME -i inventory.yaml --ask-vault-pass -k
```
