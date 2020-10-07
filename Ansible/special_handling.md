## Merging dictionaries with same name of different hosts
host_vars/host1.yaml
```yaml
my_dict:
  key1:
    value1a: SomeVal1a
    value1b: SomeVal1b
  key2:
    value2a: SomeVal2a
    value2b: SomeVal2b
```

host_vars/host2.yaml
```yaml
my_dict:
  key3:
    value3a: SomeVal3a
    value3b: SomeVal3b
  key4:
    value4a: SomeVal4a
    value4b: SomeVal4b
```

playbook.yaml
```yaml
- name: consolidate and display my result
  hosts: localhost

  tasks:
    - name: Consolidate result in a single hashmap
      set_fact:
        my_final_map: "{{ my_final_map | default({}) | combine(item) }}"
      loop: >-
        {{
          groups["all"]
          | map("extract", hostvars)
          | map(attribute="my_dict")
          | list
        }}

    - name: Display consolidated result
      debug:
        var: my_final_map
```

---
