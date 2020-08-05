```yaml
...
group_vars/
    all/
        any_name1.yaml
        any_name2.yaml
        any_vault_file1.yaml
        any_vault_file2.yaml
    hostgroup1/
        any_name1.yaml
        any_name2.yaml
        any_vault_file1.yaml
        any_vault_file2.yaml
    hostgroup2/
        any_name1.yaml
        any_name2.yaml
        any_vault_file1.yaml
        any_vault_file2.yaml
```

To verify the variables of your host group
```bash
ansible -m debug -a 'var=hostvars[inventory_hostname]' YOUR_GROUP_NAME -i inventory.yaml --ask-vault-pass -k

#e.g.
ansible -m debug -a 'var=hostvars[inventory_hostname]' hostgroup1 -i inventory.yaml --ask-vault-pass -k
```
