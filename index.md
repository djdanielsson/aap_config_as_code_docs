---
= Ansible Automation Platform Configuration as Code Collections
include::_style/render.adoc[]

== Introduction

Several collections have been created by the Red Hat Communities of Practice to assist with configuring aspects of the Ansible Automation Platform (AAP) using configuration as code practices. This site will guide you through these collections, the use cases, how to use and strategies for scaling appropriately.

=== Where to get and maintain this document

This document is published to https://redhat-cop.github.io/aap_config_as_code_docs/, it is open source and its source code is maintained at https://github.com/redhat-cop/aap_config_as_code_docs/.

== Getting Help

We are on the Ansible Forums and Matrix, if you want to discuss something, ask for help, or participate in the community, please use the #infra-config-as-code tag on the forum, or post to the chat in Matrix.

https://forum.ansible.com/tag/infra-config-as-code[Ansible Forums]

https://matrix.to/#/#aap_config_as_code:ansible.com[Matrix Chat Room]

== AAP Config as Code Collections
NOTE: Further documentation for these collections will be stored here.

.Links to Ansible Automation Platform Collections
[options="header"]
|================
|Collection Name|Purpose
|[awx.awx/Ansible.controller repo](https://github.com/ansible/awx/tree/devel/awx_collection)|Automation controller modules
|[Ansible Hub Configuration](https://github.com/ansible/automation_hub_collection)|Automation hub configuration
|================

.Links to other Validated Configuration Collections for Ansible Automation Platform
[options="header"]
|================
|Collection Name|Purpose
|[Controller Configuration](https://github.com/redhat-cop/controller_configuration)|Automation controller configuration
|[EE Utilities](https://github.com/redhat-cop/ee_utilities)|Execution Environment creation utilities
|[AAP installation Utilities](https://github.com/redhat-cop/aap_utilities)|Ansible Automation Platform Utilities
|[AAP Configuration Template](https://github.com/redhat-cop/aap_configuration_template)|Configuration Template for this suite
|================

* [roles.md](collections/controller_configuration/roles.md)
* [workflow_job_templates.md](collections/controller_configuration/workflow_job_templates.md)
* [groups.md](collections/controller_configuration/groups.md)
* [license.md](collections/controller_configuration/license.md)
* [workflow_launch.md](collections/controller_configuration/workflow_launch.md)
* [settings.md](collections/controller_configuration/settings.md)
* [users.md](collections/controller_configuration/users.md)
* [object_diff.md](collections/controller_configuration/object_diff.md)
* [applications.md](collections/controller_configuration/applications.md)
* [credential_input_sources.md](collections/controller_configuration/credential_input_sources.md)
* [inventory_source_update.md](collections/controller_configuration/inventory_source_update.md)
* [labels.md](collections/controller_configuration/labels.md)
* [instance_groups.md](collections/controller_configuration/instance_groups.md)
* [credentials.md](collections/controller_configuration/credentials.md)
* [credential_types.md](collections/controller_configuration/credential_types.md)
* [project_update.md](collections/controller_configuration/project_update.md)
* [job_launch.md](collections/controller_configuration/job_launch.md)
* [bulk_host_create.md](collections/controller_configuration/bulk_host_create.md)
* [ad_hoc_command_cancel.md](collections/controller_configuration/ad_hoc_command_cancel.md)
* [schedules.md](collections/controller_configuration/schedules.md)
* [inventory_sources.md](collections/controller_configuration/inventory_sources.md)
* [jobs_cancel.md](collections/controller_configuration/jobs_cancel.md)
* [notification_templates.md](collections/controller_configuration/notification_templates.md)
* [filetree_create.md](collections/controller_configuration/filetree_create.md)
* [organizations.md](collections/controller_configuration/organizations.md)
* [filetree_read.md](collections/controller_configuration/filetree_read.md)
* [projects.md](collections/controller_configuration/projects.md)
* [hosts.md](collections/controller_configuration/hosts.md)
* [execution_environments.md](collections/controller_configuration/execution_environments.md)
* [bulk_job_launch.md](collections/controller_configuration/bulk_job_launch.md)
* [global_vars.md](collections/controller_configuration/global_vars.md)
* [teams.md](collections/controller_configuration/teams.md)
* [ad_hoc_command.md](collections/controller_configuration/ad_hoc_command.md)
* [dispatch.md](collections/controller_configuration/dispatch.md)
* [instances.md](collections/controller_configuration/instances.md)
* [job_templates.md](collections/controller_configuration/job_templates.md)
* [inventories.md](collections/controller_configuration/inventories.md)

[appendix]
== Contributing to this Documentation
We welcome community contributions to this documentation, or any of the mentioned collections. If you find problems, please open an issue and consider creating a PR against this, or any relevant, repository. More information about contributing can be found in our link:CONTRIBUTE.adoc[Contribution Guidelines].

We have a community meeting every 4 weeks. Find the agenda in the issues and the calendar invitation below:

[link=https://raw.githubusercontent.com/redhat-cop/controller_configuration/devel/docs/aap_config_as_code_public_meeting.ics]
image::https://www.google.com/calendar/images/ext/gc_button1_en-GB.gif[Google Calendar Invite,80,20]

[appendix]
== Code of Conduct

This repository follows the Ansible project's
https://docs.ansible.com/ansible/latest/community/code_of_conduct.html[Code of Conduct].
Please read and familiarize yourself with this document.

[appendix]
== Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.