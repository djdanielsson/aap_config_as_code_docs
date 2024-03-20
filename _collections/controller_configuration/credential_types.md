

# controller_configuration.credential_types

## Description

An Ansible Role to create/update/remove Credential Types on Ansible Controller.

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

'controller_configuration_credential_types_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.


### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add credential type task does not include sensitive information.
controller_configuration_credential_types_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.


### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Data Structure

### Credential Type Variables


### Formating Injectors

Injectors use a standard Jinja templating format to describe the resource.

Example:

```json
{{ variable }}
```

Because of this it is difficult to provide controller with the required format for these fields.

The workaround is easier to do in yaml with unsafe syntax, to read more about this check out the [documentation](https://docs.ansible.com/ansible/latest/user_guide/playbooks_advanced_syntax.html):

```yaml
!unsafe '{{ variable }}'
```

If you want to use json you will have to use the following format:

```json
{  { variable }}
```

The role will strip the double space between the curly bracket in order to provide controller with the correct format for the Injectors.

### Input and Injector Schema

The following details the data format to use for inputs and injectors. These can be in either YAML or JSON For the most up to date information and more details see [Custom Credential Types - Ansible Controller Documentation](https://docs.ansible.com/automation-controller/latest/html/userguide/credential_plugins.html)

#### Input Schema

```yaml
fields:
  - type: string
    id: username
    label: Username
  - type: string
    id: password
    label: Password
    secret: true
required:
  - username
  - password
```

#### Injector Schema

```json
{
  "file": {
      "template": "[mycloud]\ntoken={{ api_token }}"
  },
  "env": {
      "THIRD_PARTY_CLOUD_API_TOKEN": "{{ api_token }}"
  },
  "extra_vars": {
      "some_extra_var": "{{ username }}:{{ password }}"
  }
}
```

### Standard Credential Type Data Structure

#### Json Example

```json
{
    "controller_credential_types": [
      {
        "name": "REST API Credential",
        "description": "REST API Credential",
        "kind": "cloud",
        "inputs": {
          "fields": [
            {
              "type": "string",
              "id": "rest_username",
              "label": "REST Username"
            },
            {
              "secret": true,
              "type": "string",
              "id": "rest_password",
              "label": "REST Password"
            }
          ],
          "required": [
            "rest_username",
            "rest_password"
          ]
        },
        "injectors": {
          "extra_vars": {
            "rest_password": "{  { rest_password }}",
            "rest_username": "{  { rest_username }}"
          },
          "env": {
            "rest_username_env": "{  { rest_username }}",
            "rest_password_env": "{  { rest_password }}"
          }
        }
      }
    ]
}
```

#### Yaml Example

```yaml
---
controller_credential_types:
- name: REST API Credential
  description: REST API Credential
  inputs:
    fields:
    - type: string
      id: rest_username
      label: REST Username
    - secret: true
      type: string
      id: rest_password
      label: REST Password
    required:
    - rest_username
    - rest_password
  injectors:
    extra_vars:
      rest_password: !unsafe "{{ rest_password }}"
      rest_username: !unsafe "{{ rest_username }}"
    env:
      rest_username_env: !unsafe "{{ rest_username }}"
      rest_password_env: !unsafe "{{ rest_password }}"
```

## Playbook Examples

### Standard Role Usage

```yaml
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
    - {role: infra.controller_configuration.credential_types, when: controller_credential_types is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
