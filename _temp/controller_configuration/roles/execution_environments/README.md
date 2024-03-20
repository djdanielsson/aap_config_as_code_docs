---
---

# controller_configuration.execution_environments

## Description

An Ansible Role to create/update/remove execution_environments on Ansible Controller.

## Requirements

ansible-galaxy collection install -r tests/collections/requirements.yml to be installed
Currently:
  awx.awx
  or
  ansible.controller

## Variables



### Enforcing defaults

The following Variables compliment each other.
If Both variables are not set, enforcing default values is not done.
Enabling these variables enforce default values on options that are optional in the controller API.
This should be enabled to enforce configuration and prevent configuration drift. It is recomended to be enabled, however it is not enforced by default.

Enabling this will enforce configurtion without specifying every option in the configuration files.

'controller_configuration_execution_environments_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add execution_environments task does not include sensitive information.
controller_configuration_execution_environments_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.



## Data Structure

### Execution Environment Variables



### Standard Execution Environment Data Structure

#### Json Example

```json
{
  "controller_execution_environments": [
    {
      "name": "My EE",
      "image": "quay.io/ansible/awx-ee"
    }
  ]
}
```

#### Yaml Example

```yaml
---
controller_execution_environments:
  - name: "My EE"
    image: quay.io/ansible/awx-ee
```

## Playbook Examples

### Standard Role Usage

```yaml
---
- name: Add Execution Environments to controller
  hosts: localhost
  connection: local
  gather_facts: false
  vars:
    controller_execution_environments:
      name: "My EE"
      image: quay.io/ansible/awx-ee

  tasks:
    - name: Add Execution Environments
      include_role:
        name: infra.controller_configuration.execution_environments
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Tom Page](https://github.com/Tompage1994)
