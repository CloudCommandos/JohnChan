## `handlers` Directory Structure
```yaml
...
roles/
    role1/
        handlers/
            handler1.yaml
            handler2.yaml
    role2/
        handlers/
            handler3.yaml
            handler4.yaml
```

* Handlers can be defined in the main playbook's `tasks` section as well
* Handlers of Roles will be executed before handlers that are defined in the main playbook.
