<<<<<<< HEAD

=======
---
---
---
>>>>>>> 268fe1cce9a3aa964a29848a2eb041021df101a6

# controller_configuration.settings

An Ansible role to alter Settings on Ansible Controller.

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
The role defaults to False as normally the add settings task does not include sensitive information.
controller_configuration_settings_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of configuration roles with a single variable, or for the user to selectively use it.


### Asynchronous Retry Variables

The following Variables set asynchronous retries for the role.
If neither of the retries or delay or retries are set, they will default to their respective defaults.
This allows for all items to be created, then checked that the task finishes successfully.
This also speeds up the overall role.


## Data Structure

There are two choices for entering settings. Either provide as a single dict under `settings` or individually as `name` `value`. In the first case `controller_settings` will simply be an individual dict, but in the second case, it will be a list.

### Setting Variables


### Standard Setting Data Structure - as a dict

#### Json Dict Example

```json
{
  "controller_settings": {
    "settings": {
      "AUTH_LDAP_USER_DN_TEMPLATE": "uid=%(user)s,ou=Users,dc=example,dc=com",
      "AUTH_LDAP_BIND_PASSWORD": "password"
    }
  }
}

```

#### Yaml Dict Example

```yaml
---
controller_settings:
  settings:
    AUTH_LDAP_USER_DN_TEMPLATE: "uid=%(user)s,ou=Users,dc=example,dc=com"
    AUTH_LDAP_BIND_PASSWORD: "password"

```

### Standard Setting Data Structure - as a list

#### Json List Example

```json
{
  "controller_settings": [
    {
      "name": "AUTH_LDAP_USER_DN_TEMPLATE",
      "value": "uid=%(user)s,ou=Users,dc=example,dc=com"
    },
    {
      "name": "AUTH_LDAP_BIND_PASSWORD",
      "value": "password"
    }
  ]
}

```

#### Yaml List Example

```yaml
---
controller_settings:
  - name: AUTH_LDAP_USER_DN_TEMPLATE
    value: "uid=%(user)s,ou=Users,dc=example,dc=com"
  - name: AUTH_LDAP_BIND_PASSWORD
    value: "password"
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
    - {role: infra.controller_configuration.settings, when: controller_settings is defined}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Kedar Kulkarni](https://github.com/kedark3)
[Sean Sullivan](https://github.com/sean-m-sullivan)
