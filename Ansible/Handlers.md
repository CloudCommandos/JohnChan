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

* Handlers can be defined in the main playbook's `tasks` section as well.
* Handlers of Roles will be executed before handlers that are defined in the main playbook.
* Handlers are triggered by the `notify` property of tasks.
* Handlers can only be invoked once per playbook execution no matter how many times the same handler has been notified.
* Handlers can be notified through their `name` or `listen` properties. It is recommended to use the `listen` property.

## Sample Handler
./roles/role1/handlers/handler1.yaml
```yaml
- name: handler1
  debug:
    msg: "Handler1 has been invoked"

- name: handler2
  debug:
    msg: "Handler2 has been invoked"
```

./main-playbook.yaml
