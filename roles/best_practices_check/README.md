Best-practices-check
=========

This role contains tasks to verify different "best practices" that should be in place/configured in a Cisco ACI fabric as a starting point to migrate from a legacy-style environment (vlans/subnets) into ACI. This best practices are taken from different Cisco-documents and with the GREAT help of https://unofficialaciguide.com/ which saved me LOTS of time with their "ACI Best Practices for curling" article

Requirements
------------

The role makes use of inventory_hostname, username and password already defined on the hosts file.

Role Variables
--------------

None. Uses variables from hosts files
inventory_hostname
username
password

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

From requirements of the Ansible ACI modules, the connection must be set to LOCAL and gather_facts as NO

Example Playbook
----------------

Calls the role from the mail playbook

name: ACI Playbook 
  hosts: apic
  connection: local
  gather_facts: no
  roles:
    - best-practices-check

Author Information
------------------

Eduardo Pozo