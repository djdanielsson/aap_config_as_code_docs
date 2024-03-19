# controller_configuration.ad_hoc_command_cancel

## Description

An Ansible Role to cancel a list of ad hoc commands on Ansible Controller.

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
The role defaults to False as normally the add ad hoc commands cancel task does not include sensitive information.
controller_configuration_ad_hoc_command_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



## Data Structure

### Ad Hoc Command Cancel Variables



### Standard Ad Hoc Command Cancel Data Structure

#### Yaml Example

```yaml
---
controller_ad_hoc_commands_cancel:
  - id: 10
    fail_if_not_running: false
    interval: 1
    timeout: 10
  - id: 12
    fail_if_not_running: false
    interval: 1
    timeout: 10

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
      ansible.builtin.include_vars:
        dir: ./yaml
        ignore_files: [controller_config.yml.template]
        extensions: ["yml"]
  roles:
    - {role: infra.controller_configuration.ad_hoc_command_cancel, when: controller_ad_hoc_commands is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
