---
---
---

# controller_configuration.bulk_host_create

## Description

An Ansible Role to create bulk hosts on Ansible Controller.

## Requirements

ansible-galaxy collection install -r tests/collections/requirements.yml to be installed
Currently:
  awx.awx
  or
  ansible.controller

## Variables



### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add ******* task does not include sensitive information.
controller_configuration_*******_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.



## Data Structure

### Bulk Host Variables


### Bulk Host Sub Options



### Standard Bulk Host Data Structure

#### Json Example

```json
{
  "controller_bulk_hosts": [
    {
      "inventory": "localhost",
      "hosts": [
        {
          "name": "localhost"
        },
        {
          "name": "127.0.0.1",
          "variables": {
            "some_var": "some_val",
            "ansible_connection": "local"
          }
        }
      ]
    }
  ]
}
```

#### Yaml Example

```yaml
---
controller_bulk_hosts:
  - inventory: localhost
    hosts:
      - name: localhost
      - name: 127.0.0.1
        variables:
          some_var: some_val
          ansible_connection: local
```

## Playbook Examples

### Standard Role Usage

```yaml
---
- name: Playbook to configure ansible controller post installation
  hosts: localhost
  connection: local
  # Define following vars here, or in controller_configs/controller_auth.yml
  # controller_hostname: ansible-controller-web-svc-test-project.example.com
  # controller_username: admin
  # controller_password: changeme
  pre_tasks:
    - name: Include vars from controller_configs directory
      include_vars:
        dir: ./yaml
        ignore_files: [controller_config.yml.template]
        extensions: ["yml"]
  roles:
    - {role: redhat_cop.controller_configuration.bulk_host_create, when: controller_bulk_hosts is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
