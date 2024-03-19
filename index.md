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

[roles.md](_collection/controller_configurationroles.md)
[workflow_job_templates.md](_collection/controller_configurationworkflow_job_templates.md)
[groups.md](_collection/controller_configurationgroups.md)
[license.md](_collection/controller_configurationlicense.md)
[workflow_launch.md](_collection/controller_configurationworkflow_launch.md)
[settings.md](_collection/controller_configurationsettings.md)
[users.md](_collection/controller_configurationusers.md)
[object_diff.md](_collection/controller_configurationobject_diff.md)
[applications.md](_collection/controller_configurationapplications.md)
[credential_input_sources.md](_collection/controller_configurationcredential_input_sources.md)
[inventory_source_update.md](_collection/controller_configurationinventory_source_update.md)
[labels.md](_collection/controller_configurationlabels.md)
[instance_groups.md](_collection/controller_configurationinstance_groups.md)
[credentials.md](_collection/controller_configurationcredentials.md)
[credential_types.md](_collection/controller_configurationcredential_types.md)
[project_update.md](_collection/controller_configurationproject_update.md)
[job_launch.md](_collection/controller_configurationjob_launch.md)
[bulk_host_create.md](_collection/controller_configurationbulk_host_create.md)
[ad_hoc_command_cancel.md](_collection/controller_configurationad_hoc_command_cancel.md)
[schedules.md](_collection/controller_configurationschedules.md)
[inventory_sources.md](_collection/controller_configurationinventory_sources.md)
[jobs_cancel.md](_collection/controller_configurationjobs_cancel.md)
[notification_templates.md](_collection/controller_configurationnotification_templates.md)
[filetree_create.md](_collection/controller_configurationfiletree_create.md)
[organizations.md](_collection/controller_configurationorganizations.md)
[filetree_read.md](_collection/controller_configurationfiletree_read.md)
[projects.md](_collection/controller_configurationprojects.md)
[hosts.md](_collection/controller_configurationhosts.md)
[execution_environments.md](_collection/controller_configurationexecution_environments.md)
[bulk_job_launch.md](_collection/controller_configurationbulk_job_launch.md)
[global_vars.md](_collection/controller_configurationglobal_vars.md)
[teams.md](_collection/controller_configurationteams.md)
[ad_hoc_command.md](_collection/controller_configurationad_hoc_command.md)
[dispatch.md](_collection/controller_configurationdispatch.md)
[instances.md](_collection/controller_configurationinstances.md)
[job_templates.md](_collection/controller_configurationjob_templates.md)
[inventories.md](_collection/controller_configurationinventories.md)

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