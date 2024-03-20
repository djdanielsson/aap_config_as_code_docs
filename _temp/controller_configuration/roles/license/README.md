

# controller_configuration.license

## Description

An Ansible Role to deploy a license on Ansible Controller.

This will either accept a manifest file, or use redhat subscription account credentials to lookup available subscriptions and use them.

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
The role defaults to False as normally the add license task does not include sensitive information.
controller_configuration_license_secure_logging defaults to the value of controller_configuration_secure_logging if it is not explicitly called. This allows for secure logging to be toggled for the entire suite of controller configuration roles with a single variable, or for the user to selectively use it.


## Data Structure

### Manifest vs Subscription

The module and this role can use either a manifest file, or lookup the subscription on your account. Only one method is needed, provide the appropriate variables to use the either method.

### License Variables for using mainfest


### License Variables for using Red Hat Subscription


### Standard License Data Structure

#### Json Example

```json
{
    "controller_license": {
        "manifest_file": "/tmp/my_controller.license",
        "force": true
      }
}
```

#### Yaml Example

```yaml
---
controller_license:
  manifest_url: "https://fileserver.internal/controller_license.zip"
  manifest_username: admin
  manifest_password: password
  force: false
```

## Playbook Examples

### Standard Manifest Role Usage

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
    - {role: infra.controller_configuration.license, when: controller_license is defined}
```

### Standard Subscription lookup Role Usage

```yaml
---
- name: Playbook to configure ansible controller post installation
  hosts: localhost
  connection: local
  vars:
    controller_validate_certs: false
    controller_hostname: controller.example.com
    controller_username: admin
    controller_password: changeme
    redhat_subscription_username: changeme
    redhat_subscription_password: changeme
    controller_license:
      filters:
        product_name: "Red Hat Ansible Automation Platform"
        support_level: "Self-Support"
  roles:
    - {role: infra.controller_configuration.license}
```

## License

[MIT](https://github.com/redhat-cop/controller_configuration#licensing)

## Author

[Tom Page](https://github.com/Tompage1994)
