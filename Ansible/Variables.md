## `group_vars` Directory Structure
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

## Vault Protected Variables
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

### SSH Variables
You can place SSH credentials inside vault files as well
```bash
ansible-vault create ssh_vault.file
```
```yaml
ansible_ssh_user: john
ansible_ssh_pass: 12345
ansible_sudo_pass: 12345
```
With this, you do not need to supply SSH credentials when running the playbook

## Debug
To verify the variables of your host group
```bash
ansible -m debug -a 'var=hostvars[inventory_hostname]' YOUR_GROUP_NAME -i inventory.yaml --ask-vault-pass -k

#e.g.
ansible -m debug -a 'var=hostvars[inventory_hostname]' hostgroup1 -i inventory.yaml --ask-vault-pass -k
```

## Variable Types
```yaml
# Take value from another variable
ssh_password: "{{ vault_ssh_password }}"

# String 
string_var1: this is string without quotes
string_var2: "12345"
string_var3: \"12345\"

# Integer
integer_var1: 12345

# Object and Array 
object_var:
    property1: I am string
    property2:
        property2A: I am property A
        property2B: I am property B
    property3:
        - I
        - am
        - array
```
