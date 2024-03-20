

# controller_configuration.organizations

## Description

An Ansible Role to create/update/remove Organizations on Ansible Controller.

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

'controller_configuration_organizations_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.


### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add organization task does not include sensitive information.
controller_configuration_organizations_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.


### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Organization Data Structure

This role accepts two data models. A simple straightforward easy to maintain model, and another based on the controller api. The 2nd one is more complicated and includes more detail, and is compatible with controller import/export.

### Organization Variables


### Standard Organization Data Structure model

#### Json Example

```json
{
    "controller_organizations": [
      {
        "name": "Default",
        "description": "This is the Default Group"
      },
      {
        "name": "Automation Group",
        "description": "This is the Automation Group",
        "custom_virtualenv": "/opt/cust/environment/",
        "max_hosts": 10,
        "galaxy_credentials": "Automation Hub",
        "notification_templates_error": [
          "Slack_for_testing"
        ]
      }
    ]
}
```

#### Yaml Example

```yaml
---
controller_organizations:
- name: Default
  description: This is the Default Group
- name: Automation Group
  description: This is the Automation Group
  custom_virtualenv: "/opt/cust/environment/"
  max_hosts: 10
```

#### Controller Export Data structure model

##### Export Yaml Example

```yaml
---
controller_organizations:
- name: Satellite
  description: Satellite
  max_hosts: 0
  custom_virtualenv:
  related:
    notification_templates_started: []
    notification_templates_success: []
    notification_templates_error:
    - name: irc-satqe-chat-notification
    notification_templates_approvals: []
- name: Default
  description: Default
  max_hosts: 0
  custom_virtualenv:
  galaxy_credentials:
    - Automation Hub
  related:
    notification_templates_started: []
    notification_templates_success: []
    notification_templates_error: []
    notification_templates_approvals: []
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
    - {role: infra.controller_configuration.organizations, when: controller_organizations is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
