# controller_configuration.groups

## Description

An Ansible Role to create/update/remove Groups on Ansible Controller.

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

'controller_configuration_groups_enforce_defaults' defaults to the value of 'controller_configuration_enforce_defaults' if it is not explicitly called. This allows for enforced defaults to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.



### Secure Logging Variables

The following Variables compliment each other.
If Both variables are not set, secure logging defaults to false.
The role defaults to False as normally the add groups task does not include sensitive information.
controller_configuration_groups_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.



### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.



### Formating Variables

Variables can use a standard Jinja templating format to describe the resource.

Example:

```json
{{ variable }}
```

Because of this it is difficult to provide controller with the required format for these fields.

The workaround is to use the following format:

```json
{  { variable }}
```

The role will strip the double space between the curly bracket in order to provide controller with the correct format for the Variables.

## Data Structure

### Group Variables

|Variable Name|Default Value|Required|Type|Description|
|:---:|:---:|:---:|:---:|:---:|
|`name`|""|yes|str|Name of Group|
|`new_name`|""|yes|str|Name of Group, used in updating a Group.|
|`description`|`False`|no|str|Description of the Group.|
|`inventory`|""|yes|str|Name of inventory the group should be made a member of.|
|`variables`|{}|no|dict|variables applicable to group.|
|`hosts`|""|no|list|hosts (list) in group|
|`children`|""|no|list|List of groups that should be nested inside in this group|
|`preserve_existing_hosts`|`False`|no|bool|Whether to preserve existing hosts in an existing group|
|`preserve_existing_children`|`False`|no|bool|Whether to preserve existing children in an existing group|
|`state`|`present`|no|str|Desired state of the resource.|

### Standard Group Data Structure

#### Json Example

```json
{
    "controller_groups": [
      {
        "name": "PSQL_Servers",
        "description": "Default",
        "inventory": "Source Control",
        "variables": {
        "my_var": true
        }
      }
    ]
}
```

#### Yaml Example

```yaml
---
controller_groups:
- name: PSQL_Servers
  description: Group for Postgres SQL Servers
  inventory: Default
  variables:
    myvars: example1
  hosts:
   - PSQL1
   - PSQL2
   - PSQL3
  children:
   - group1
   - group2
   - group3
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
    - {role: infra.controller_configuration.groups, when: controller_groups is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Wei-Yen Tan](https://github.com/weiyentan)
[Andrew J. Huffman](https://github.com/ahuffman)
[Sean Sullivan](https://github.com/sean-m-sullivan)