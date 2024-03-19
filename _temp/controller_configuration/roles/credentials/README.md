---
---
---
# controller_configuration.credentials

## Description

An Ansible Role to create/update/remove Credentials on Ansible Controller.

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

'controller_configuration_credentials_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add credentials task does not include sensitive information.
controller_configuration_credentials_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.



### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Data Structure

### Credential Variables



### Credential types



### Standard Credential Data Structure

#### Json Example

```json

{
    "controller_credentials": [
      {
        "name": "gitlab",
        "description": "Credentials for GitLab",
        "organization": "Default",
        "credential_type": "Source Control",
        "inputs": {
          "username": "person",
          "password": "password"
        }
      }
    ]
}
```

#### Yaml Example

```yaml
---
controller_credentials:
- name: gitlab
  description: Credentials for GitLab
  organization: Default
  credential_type: Source Control
  inputs:
    username: person
    password: password
- name: localuser
  description: Machine Credential example with become_method input
  credential_type: Machine
  inputs:
    username: localuser
    password: password
    become_method: sudo
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
    - {role: infra.controller_configuration.credentials, when: controller_credentials is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Andrew J. Huffman](https://github.com/ahuffman)
[Sean Sullivan](https://github.com/sean-m-sullivan)
