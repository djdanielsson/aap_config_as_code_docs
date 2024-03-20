---

---

# Ansible Automation Platform Configuration as Code Collections

## Introduction

Several collections have been created by the Red Hat Communities of Practice to assist with configuring aspects of the Ansible Automation Platform (AAP) using configuration as code practices. This site will guide you through these collections, the use cases, how to use and strategies for scaling appropriately.

### Where to get and maintain this document

This document is published to https://redhat-cop.github.io/aap_config_as_code_docs/, it is open source and its source code is maintained at https://github.com/redhat-cop/aap_config_as_code_docs/.

## Getting Help

We are on the Ansible Forums and Matrix, if you want to discuss something, ask for help, or participate in the community, please use the #infra-config-as-code tag on the forum, or post to the chat in Matrix.

[Ansible Forums](https://forum.ansible.com/tag/infra-config-as-code)

[Matrix Chat Room](https://matrix.to/#/#aap_config_as_code:ansible.com)

## AAP Config as Code Collections
NOTE: Further documentation for these collections will be stored here.

.Links to Ansible Automation Platform Collections

|Collection Name|Purpose|
|---------|---------|
|[awx.awx/Ansible.controller repo](https://github.com/ansible/awx/tree/devel/awx_collection)|Automation controller modules
|[Ansible Hub Configuration](https://github.com/ansible/automation_hub_collection)|Automation hub configuration

.Links to other Validated Configuration Collections for Ansible Automation Platform

|Collection Name|Purpose|
|---------|---------|
|[Controller Configuration](https://github.com/redhat-cop/controller_configuration)|Automation controller configuration
|[EE Utilities](https://github.com/redhat-cop/ee_utilities)|Execution Environment creation utilities
|[AAP installation Utilities](https://github.com/redhat-cop/aap_utilities)|Ansible Automation Platform Utilities
|[AAP Configuration Template](https://github.com/redhat-cop/aap_configuration_template)|Configuration Template for this suite

* [ad_hoc_command.md](collections/controller_configuration/ad_hoc_command.md)
* [ad_hoc_command_cancel.md](collections/controller_configuration/ad_hoc_command_cancel.md)
* [applications.md](collections/controller_configuration/applications.md)
* [bulk_host_create.md](collections/controller_configuration/bulk_host_create.md)
* [bulk_job_launch.md](collections/controller_configuration/bulk_job_launch.md)
* [credential_input_sources.md](collections/controller_configuration/credential_input_sources.md)
* [credential_types.md](collections/controller_configuration/credential_types.md)
* [credentials.md](collections/controller_configuration/credentials.md)
* [dispatch.md](collections/controller_configuration/dispatch.md)
* [execution_environments.md](collections/controller_configuration/execution_environments.md)
* [filetree_create.md](collections/controller_configuration/filetree_create.md)
* [filetree_read.md](collections/controller_configuration/filetree_read.md)
* [global_vars.md](collections/controller_configuration/global_vars.md)
* [groups.md](collections/controller_configuration/groups.md)
* [hosts.md](collections/controller_configuration/hosts.md)
* [instance_groups.md](collections/controller_configuration/instance_groups.md)
* [instances.md](collections/controller_configuration/instances.md)
* [inventories.md](collections/controller_configuration/inventories.md)
* [inventory_source_update.md](collections/controller_configuration/inventory_source_update.md)
* [inventory_sources.md](collections/controller_configuration/inventory_sources.md)
* [job_launch.md](collections/controller_configuration/job_launch.md)
* [job_templates.md](collections/controller_configuration/job_templates.md)
* [jobs_cancel.md](collections/controller_configuration/jobs_cancel.md)
* [labels.md](collections/controller_configuration/labels.md)
* [license.md](collections/controller_configuration/license.md)
* [notification_templates.md](collections/controller_configuration/notification_templates.md)
* [object_diff.md](collections/controller_configuration/object_diff.md)
* [organizations.md](collections/controller_configuration/organizations.md)
* [project_update.md](collections/controller_configuration/project_update.md)
* [projects.md](collections/controller_configuration/projects.md)
* [roles.md](collections/controller_configuration/roles.md)
* [schedules.md](collections/controller_configuration/schedules.md)
* [settings.md](collections/controller_configuration/settings.md)
* [teams.md](collections/controller_configuration/teams.md)
* [users.md](collections/controller_configuration/users.md)
* [workflow_job_templates.md](collections/controller_configuration/workflow_job_templates.md)
* [workflow_launch.md](collections/controller_configuration/workflow_launch.md)



* [aap_backup.md](collections/aap_utilities/aap_backup.md)
* [aap_certs.md](collections/aap_utilities/aap_certs.md)
* [aap_ocp_install.md](collections/aap_utilities/aap_ocp_install.md)
* [aap_remove.md](collections/aap_utilities/aap_remove.md)
* [aap_restore.md](collections/aap_utilities/aap_restore.md)
* [aap_setup_download.md](collections/aap_utilities/aap_setup_download.md)
* [aap_setup_install.md](collections/aap_utilities/aap_setup_install.md)
* [aap_setup_prepare.md](collections/aap_utilities/aap_setup_prepare.md)
* [git_ssh_setup.md](collections/aap_utilities/git_ssh_setup.md)
* [kerberos.md](collections/aap_utilities/kerberos.md)


[appendix]
## Contributing to this Documentation
We welcome community contributions to this documentation, or any of the mentioned collections. If you find problems, please open an issue and consider creating a PR against this, or any relevant, repository. More information about contributing can be found in our link:CONTRIBUTE.adoc[Contribution Guidelines].

We have a community meeting every 4 weeks. Find the agenda in the issues and the calendar invitation below:

[![Calendar](https://www.google.com/calendar/images/ext/gc_button1_en-GB.gif)(https://raw.githubusercontent.com/redhat-cop/controller_configuration/devel/docs/aap_config_as_code_public_meeting.ics)]

## Code of Conduct

This repository follows the Ansible project's
https://docs.ansible.com/ansible/latest/community/code_of_conduct.html[Code of Conduct].
Please read and familiarize yourself with this document.

[appendix]
## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.