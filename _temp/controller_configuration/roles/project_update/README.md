---
---
---

# controller_configuration.project_update

## Description

An Ansible Role to update a list of projects on Ansible Controller.

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
The role defaults to False as normally the project update task does not include sensitive information.
controller_configuration_project_update_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.

### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Data Structure

### Project Update Variables


### Standard Project Update Data Structure

#### Yaml Example

```yaml
---
controller_projects:
  - name: Test Project
    scm_type: git
    scm_url: https://github.com/ansible/tower-example.git
    scm_branch: master
    scm_clean: true
    description: Test Project 1
    organization: Satellite
    wait: true
  - name: Test Project 2
    scm_type: git
    scm_url: https://github.com/ansible/tower-example.git
    description: Test Project 2
    organization: Satellite
    wait: true
  - name: Test Inventory source project
    scm_type: git
    scm_url: https://github.com/ansible/ansible-examples.git
    description: ansible-examples
    organization: Satellite
    wait: true

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
    - {role: infra.controller_configuration.project_update, when: controller_projects is defined}

```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Sean Sullivan](https://github.com/sean-m-sullivan)
