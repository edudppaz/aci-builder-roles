net-migration
=========

The following role accomplish a network migration from a legacy network (VLANS/Subnets) to an ACI fabric, based on a "Network Centric Deployment"

Two Application Profiles are created, one for L2 VLANS and one for L3 VLANS, with names "L2-LEGACY" and "L3-LEGACY". This names can be modified directly on the tasks.
The naming convention used for the migrated EPGs is: VLANID-VLANNAME Where "VLANNAME" cannot be longer than 15 characters for ease of readability on ACI.

If needed, the VLAN names should be modified before running the tasks on the .csv file.

As from previous experience, some network administrators can relate more to VLAN IDs than to the vlan name. For both L2 and L3 Vlans, the mapping is 1 BD and one EPG per vlan, in order to mirror the Broadcast scope of a "normal" legacy VLAN.

Both L2 and L3 BDs are configured in "floooding" mode, in order to extend the L2 out to the legacy environment and perform the migration

Requirements
------------

The VRF name MUST be defined on the l3-vlans.csv, the "default" vrf name is taken as the default VRF. Following some experience and best practices, the "default" vrf is renamed to TENANT-DEFAULT so is easier to find and does not conflict with the default VRF in common and other tenants

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------
The playbook reads the L2 and L3 vlan information from two files defined on the /files/ subfolder.

Example l2-vlans:
```yaml
vlanid,vlanname
id1,vlan1
id2,vlan2
id3,vlan3
```
Example l3-vlans:
```yaml
vlanid,vlanname,dg,mask,vrf
id10,vlan10,192.168.10.1,24,default
id20,vlan20,192.168.20.1,24,vrf123
id30,vlan30,192.186.30.1,24,default
```
The playbook needs a TENANT name and a PHYSICAL DOMAIN, read from the main playbooks as variables, this should already be in place as this role does NOT create the Tenant or the physical domain on the APIC.

Example:
tenant_name : TENANT
tenant_phydom_name: TENANT-PHYDOM

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

- name: ACI Playbook 
  hosts: apic
  connection: local
  gather_facts: no
  vars_files:
    - vars/tenant-info.yml
  roles:
    - net-migration

Author Information
------------------

Eduardo Pozo