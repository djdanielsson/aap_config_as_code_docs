---
# controller_configuration.workflow_job_templates

## Description

An Ansible Role to create/update/remove Workflow Job Templates on Ansible Controller.

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

'controller_configuration_workflows_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.


### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add Workflow Job Templates task does not include sensitive information.
workflow_job_templates_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of genie roles with a single variable, or for the user to selectively use it.


### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Data Structure

### Variables For Workflow Job Template



### Variables For Workflow Job Template Node


### Approval node dictionary


### Surveys

Refer to the [Controller Api Guide](https://docs.ansible.com/ansible-tower/latest/html/towerapi/api_ref.html#/Job_Templates/Job_Templates_job_templates_survey_spec_create) for more information about forming surveys


### Workflow Data Structures

This role accepts two data models.

#### Simplified Workflow nodes

A simple straightforward easy to maintain model using the var simplified_workflow_nodes.
However this is, not compatible with the schema option on the controller_workflow_job_template module and will result in errors.
Uses the variable 'simplified_workflow_nodes' to describe nodes as shown below.

#### Simplified Workflow Node Data structure model

##### Yaml Example

```yaml
---
controller_workflows:
  - name: Simple workflow schema
    description: a basic workflow
    extra_vars: ''
    survey_enabled: false
    allow_simultaneous: false
    ask_variables_on_launch: false
    inventory:
    limit:
    scm_branch:
    ask_inventory_on_launch: false
    ask_scm_branch_on_launch: false
    ask_limit_on_launch: false
    webhook_service: ''
    webhook_credential:
    organization: Default
    schedules: []
    simplified_workflow_nodes:
      - all_parents_must_converge: false
        identifier: node101
        unified_job_template: RHVM-01
        credentials: []
        success_nodes:
          - node201
        failure_nodes: []
        always_nodes: []
      - identifier: node201
        approval_node:
          name: Simple approval node name
          description: Approve this to proceed in workflow
          timeout: 900 # 15 minutes
      - all_parents_must_converge: false
        identifier: node301
        unified_job_template: test-template-1
        credentials: []
        success_nodes: []
        failure_nodes: []
        always_nodes: []
    notification_templates_started: []
    notification_templates_success: []
    notification_templates_error: []
    notification_templates_approvals: []
    survey_spec: {}

```

#### Controller Export Model

This model is based off of the output from awx.awx.export, that is based on the API.
This is more complicated, However it allows the user to use the schema input on the role which runs much faster compared to the simplified model.
This can be under the subvariable 'workflow_nodes' or under the subvariable 'related.workflow_nodes' which is the output of controller_export.

#### Controller Export Data structure model

##### Yaml Export Example

```yaml
---
controller_workflows:
  - name: Simple workflow schema
    description: a basic workflow
    extra_vars: ''
    survey_enabled: false
    allow_simultaneous: false
    ask_variables_on_launch: false
    inventory:
    limit:
    scm_branch:
    ask_inventory_on_launch: false
    ask_scm_branch_on_launch: false
    ask_limit_on_launch: false
    webhook_service: ''
    webhook_credential:
    organization:
      name: Default
    workflow_nodes:
      - all_parents_must_converge: false
        identifier: node101
        unified_job_template:
          name: RHVM-01
          type: job_template
          organization:
            name: Default
        related:
          success_nodes:
            - workflow_job_template:
                name: Simple workflow schema
              identifier: node201
      - all_parents_must_converge: false
        identifier: node201
        unified_job_template:
          name: test-template-1
          type: job_template
          organization:
            name: Default
      notification_templates_started: []
      notification_templates_success: []
      notification_templates_error: []
      notification_templates_approvals: []
      survey_spec:
        name: ''
        description: ''
        spec:
          - question_name: Basic Name
            question_description: Name
            required: true
            type: text
            variable: basic_name
            min: 0
            max: 1024
            default: ''
            choices: ''
            new_question: true

```

#### Json Export Example

```json
{
  "controller_workflows": [
    {
      "name": "Simple workflow schema",
      "description": "a basic workflow",
      "extra_vars": "",
      "survey_enabled": false,
      "allow_simultaneous": false,
      "ask_variables_on_launch": false,
      "inventory": null,
      "limit": null,
      "scm_branch": null,
      "ask_inventory_on_launch": false,
      "ask_scm_branch_on_launch": false,
      "ask_limit_on_launch": false,
      "webhook_service": "",
      "webhook_credential": null,
      "organization": {
        "name": "Default"
      },
      "related": {
        "schedules": [

        ],
        "workflow_nodes": [
          {
            "all_parents_must_converge": false,
            "identifier": "node101",
            "unified_job_template": {
              "name": "RHVM-01",
              "type": "job_template",
              "organization": { "name": "Default" }
            },
            "related": {
              "credentials": [

              ],
              "success_nodes": [
                {
                  "workflow_job_template": {
                    "name": "Simple workflow schema"
                  },
                  "identifier": "node201"
                }
              ],
              "failure_nodes": [

              ],
              "always_nodes": [

              ]
            }
          },
          {
            "all_parents_must_converge": false,
            "identifier": "node201",
            "unified_job_template": {
              "name": "test-template-1",
              "type": "job_template",
              "organization": { "name": "Default" }
            },
            "related": {
              "credentials": [

              ],
              "success_nodes": [

              ],
              "failure_nodes": [

              ],
              "always_nodes": [

              ]
            }
          }
        ],
        "notification_templates_started": [

        ],
        "notification_templates_success": [

        ],
        "notification_templates_error": [

        ],
        "notification_templates_approvals": [

        ],
        "survey_spec": {
        }
      }
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
    - {role: infra.controller_configuration.workflow_job_templates, when: controller_workflows is defined}

```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
