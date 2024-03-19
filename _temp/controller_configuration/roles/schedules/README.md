# controller_configuration.schedules

## Description

An Ansible Role to create/update/remove Schedules on Ansible Controller.

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

'controller_configuration_schedules_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.


### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add schedules task does not include sensitive information.
controller_configuration_schedules_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.


### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Data Structure

### Schedule Variables


### Standard Schedule Data Structure

#### Json Example

```json
"controller_schedules": [
    {
      "name": "Demo Schedule",
      "description": "A demonstration",
      "unified_job_template": "Demo Job Template",
      "rrule": "DTSTART:20191219T130551Z RRULE:FREQ=DAILY;INTERVAL=1;COUNT=1",
      "extra_data": {
        "scheduled": true
      },
      "verbosity": 1
    }
  ]

```

#### Yaml Example

```yaml
---
controller_schedules:
  - name: Demo Schedule
    description: A demonstration
    unified_job_template: Demo Job Template
    rrule: "DTSTART:20191219T130551Z RRULE:FREQ=DAILY;INTERVAL=1;COUNT=1"
    extra_data:
      scheduled: true
    verbosity: 1
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
    - {role: infra.controller_configuration.schedules, when: controller_schedules is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Tom Page](https://github.com/Tompage1994)