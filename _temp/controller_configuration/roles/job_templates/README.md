---
---
---
# controller_configuration.job_templates

## Description

An Ansible Role to create/update/remove Job Templates on Ansible Controller.

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

'controller_configuration_job_templates_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add job_template task does not include sensitive information.
controller_configuration_job_templates_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.



### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.



## Data Structure

### Job Template Variables



### Surveys

Refer to the [controller Api Guide](https://docs.ansible.com/ansible-tower/latest/html/towerapi/api_ref.html#/Job_Templates/Job_Templates_job_templates_survey_spec_create) for more information about forming surveys



### Standard Job Template Data Structure

#### Json Example

```json
{
    "controller_templates": [
        {
            "name": "Survey Template with vars",
            "job_type": "run",
            "inventory": "Demo Inventory",
            "survey_enabled": true,
            "survey": "{{ lookup('template', 'template_surveys/basic_survey.json') | regex_replace('\\n', '') }}",
            "project": "controller Config",
            "playbook": "helloworld.yml",
            "credentials": [
                "Demo Credential"
              ],
            "extra_vars": "{{ survey_extra_vars }}",
            "notification_templates_error": [
                "Slack_for_testing"
              ]
        },
        {
            "name": "No Survey Template no vars",
            "job_type": "run",
            "inventory": "Demo Inventory",
            "project": "controller Config",
            "playbook": "helloworld.yml",
            "credentials": [
                "Demo Credential"
              ],
            "survey": {},
            "extra_vars": "{{ empty_master_vars }}",
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
controller_templates:
- name: Survey Template with vars
  job_type: run
  inventory: Demo Inventory
  execution_environment: my_exec_env
  survey_enabled: true
  survey: "{{ lookup('template', 'template_surveys/basic_survey.json') | regex_replace('\\n', '') }}"
  project: controller Config
  playbook: helloworld.yml
  credentials:
  - Demo Credential
  extra_vars: "{{ survey_extra_vars }}"
  notification_templates_error:
  - Slack_for_testing
- name: No Survey Template no vars
  job_type: run
  inventory: Demo Inventory
  project: controller Config
  playbook: helloworld.yml
  credentials:
  - Demo Credential
  survey: {}
  extra_vars: "{{ empty_master_vars }}"
  notification_templates_error:
  - Slack_for_testing
```

### Survey Data Structure

#### Survey Json Example

```json
{
    "name": "Basic Survey",
    "description": "Basic Survey",
    "spec": [
      {
        "question_description": "Name",
        "min": 0,
        "default": "",
        "max": 128,
        "required": true,
        "choices": "",
        "new_question": true,
        "variable": "basic_name",
        "question_name": "Basic Name",
        "type": "text"
      },
      {
        "question_description": "Choosing yes or no.",
        "min": 0,
        "default": "yes",
        "max": 0,
        "required": true,
        "choices": "yes\nno",
        "new_question": true,
        "variable": "option_true_false",
        "question_name": "Choose yes or no?",
        "type": "multiplechoice"
      },
      {
        "question_description": "",
        "min": 0,
        "default": "",
        "max": 0,
        "required": true,
        "choices": "group1\ngroup2\ngroup3",
        "new_question": true,
        "variable": "target_groups",
        "question_name": "Select Group:",
        "type": "multiselect"
      }
    ]
  }
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
    - {role: infra.controller_configuration.job_templates, when: controller_templates is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
