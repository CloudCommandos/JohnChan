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
string_var3: '"12345"'

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

# Dictionary             
dict_var:
    a:
        - 1
        - 2
        - 3
    b:
        - 4
        - 5
        - 6
```

## Referencing Variables
Sample role:
```yaml
- name: string_var1
  debug:
    msg: "Variable `string_var1` is : {{ string_var1 }}"

- name: string_var2
  debug:
    msg: "Variable `string_var2` is : {{ string_var2 }}"

- name: string_var3
  debug:
    msg: "Variable `string_var3` is : {{ string_var3 }}"

- name: integer_var1
  debug:
    msg: "Variable `integer_var1` is : {{ integer_var1 }}"

- name: object_var array prop
  debug:
    msg: "Variable `object_var` has array property with value: {{ item }}"
  loop: "{{ object_var.property3 }}"

- name: dict_var with_dict
  debug:
    msg: "{{ item.key }} -- {{ item.value }}"
  with_dict:
    - "{{ dict_var }}"

- name: flatten dict_var array
  set_fact:
      flattened_dict_var: |
          {% set res = [] -%}
          {% for key in dict_var.keys() -%}
              {% for value in dict_var[key] -%}
                  {% set ignored = res.extend([{'key': key, 'value':value}]) -%}
              {%- endfor %}
          {%- endfor %}
          {{ res }}

- name: flattened dict_var array
  debug:
      msg: "{{ item.key }} {{ item.value }}"
  with_items: "{{ flattened_dict_var }}"
```

Output:
```yaml
TASK [test-variables : string_var1] ***************************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => {
    "msg": "Variable `string_var1` is : this is string without quotes"
}

TASK [test-variables : string_var2] ***************************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => {
    "msg": "Variable `string_var2` is : 12345"
}

TASK [test-variables : string_var3] ***************************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => {
    "msg": "Variable `string_var3` is : \"12345\""
}

TASK [test-variables : integer_var1] **************************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => {
    "msg": "Variable `integer_var1` is : 12345"
}

TASK [test-variables : object_var array prop] *****************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => (item=I) => {
    "msg": "Variable `object_var` has array property with value: I"
}
ok: [127.0.0.1] => (item=am) => {
    "msg": "Variable `object_var` has array property with value: am"
}
ok: [127.0.0.1] => (item=array) => {
    "msg": "Variable `object_var` has array property with value: array"
}

TASK [test-variables : dict_var with_dict] ********************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => (item={u'key': u'a', u'value': [1, 2, 3]}) => {
    "msg": "a -- [1, 2, 3]"
}
ok: [127.0.0.1] => (item={u'key': u'b', u'value': [4, 5, 6]}) => {
    "msg": "b -- [4, 5, 6]"
}

TASK [test-variables : flatten dict_var array] ****************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => {"ansible_facts": {"flattened_dict_var": [{"key": "a", "value": 1}, {"key": "a", "value": 2}, {"key": "a", "value": 3}, {"key": "b", "value": 4}, {"key": "b", "value": 5}, {"key": "b", "value": 6}]}, "changed": false}

TASK [test-variables : flattened dict_var array] **************************************************************************************************************************************************************************************************************************************************************************
ok: [127.0.0.1] => (item={u'value': 1, u'key': u'a'}) => {
    "msg": "a 1"
}
ok: [127.0.0.1] => (item={u'value': 2, u'key': u'a'}) => {
    "msg": "a 2"
}
ok: [127.0.0.1] => (item={u'value': 3, u'key': u'a'}) => {
    "msg": "a 3"
}
ok: [127.0.0.1] => (item={u'value': 4, u'key': u'b'}) => {
    "msg": "b 4"
}
ok: [127.0.0.1] => (item={u'value': 5, u'key': u'b'}) => {
    "msg": "b 5"
}
ok: [127.0.0.1] => (item={u'value': 6, u'key': u'b'}) => {
    "msg": "b 6"
}
```
