---
---
---

# infra.aap_utilities.aap_ocp_install

A role to install Ansible Automation Platform (AAP) 2.x on OpenShift using the operator.

## Requirements

This role requires the `kubernetes` (version 12.0.0 or later) Python module.
In addition the kubernetes.core and redhat.openshift Ansible collections are required.

## Role Variables

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

* Variable and required keys must be defined when the type of tag is specified (e.g. `--tags controller` requires the aap_ocp_install_controller variable be defined).
If the variable is omitted the corresponding component will not be installed (e.g. if only aap_ocp_install_hub variable is defined then the operator and controller installation will be skipped)

### aap_ocp_install_connection keys


### aap_ocp_install_operator keys


> ℹ️ **NOTE**
>
> When `approval` is set to `Manual` the operator will be installed with `Automatic` approval and then after installation the approval will be updated to Manual.

### aap_ocp_install_controller keys


## Dependencies

This role depends on the redhat.openshift and kubernetes.core collections.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yml
---
- name: Install AAP on OCP playbook
  hosts: localhost
  gather_facts: false

  vars:
    aap_ocp_install_connection:
      host: "https://api.crc.testing:6443"
      username: kubeadmin
      password: <PASSWORD>
      validate_certs: false
    aap_ocp_install_namespace: aap-test
    aap_ocp_install_operator:
      channel: "stable-2.2"
    aap_ocp_install_controller:
      instance_name: automationcontroller
    aap_ocp_install_hub:
      instance_name: automationhub

  roles:
    - infra.aap_utilities.aap_ocp_install
...
```

## License

[GPLv3+0](https://github.com/redhat-cop/aap_utilities#licensing)

## Author Information

Brant Evans
