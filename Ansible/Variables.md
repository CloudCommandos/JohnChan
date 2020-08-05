## `group_vars` directory structure
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

## Vault protected variables
Create an ansible-vault protected file
```bash
ansible-vault create any_vault_file1.yaml
```
You will be prompted for the file's vault password, then declare your variables in the file
```yaml
my_secret_password1: 1234567890
my_secret_password2: 0987654321
```
You can edit the vault file
```bash
ansible-vault edit any_vault_file1.yaml
```
Or view the vault file
```bash
ansible-vault view any_vault_file1.yaml
```


## Debug
To verify the variables of your host group
```bash
ansible -m debug -a 'var=hostvars[inventory_hostname]' YOUR_GROUP_NAME -i inventory.yaml --ask-vault-pass -k

#e.g.
ansible -m debug -a 'var=hostvars[inventory_hostname]' hostgroup1 -i inventory.yaml --ask-vault-pass -k
```