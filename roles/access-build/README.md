Role Name
=========

This role builds the Fabric/Access configuration on an APIC controller based on some "best practices" or experience-based configuration as:

1 Switch Selector per leaf and per VPC pair
1 Switch profile selector per Switch selector

Requirements
------------

The role uses a pre-defined "topology.yml" file that is read by the main ansible playbook. The topology.yml file includes the LEAFs, and VPC pairs to build the infra.
It also reads information from "tenant-info.yml" to build the AEP and Physical domain. These two are not used in this role itself, but i added it as part of the "access-build" general tasks.

Role Variables
--------------

No variables on the role itself, it uses variables inherited from the main playbook

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

---
- name: ACI Playbook 
  hosts: apic
  connection: local
  gather_facts: no
  vars_files:
    - vars/topology.yml
    - vars/tenant-info.yml
  roles:
    - access-build

Author Information
------------------

Eduardo Pozo