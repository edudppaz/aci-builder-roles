aci-fabric-playbook
=========

The following playbook uses a set of tasks defined in roles to deploy the tenant and access configurations on an APIC needed for a migration from a legacy style infrastructure to a network-centric ACI infrastructure
Refer to the README.md file on each role for more information

Roles and a quick description:

 - access-build
 Build the Fabric Access configuration (Switch selectors, switch profiles, etc) based on best practices and ease-of-use. 

 - tenant-build
 Simple role that creates the tenant and a default VRF reading from the tenant-info.yml variable file

 - net-migration
This role reads a l2 and l3 vlan list and configures them as EPGs on the ACI fabric

 - best-practices-check
 Misc best-practices check, based on cisco white papers and https://unofficialaciguide.com/ blog posts.

Requirements
------------

The playbook itself has no underlaying requirements beside ansible 2.9+ (csv module). 

Variables
--------------

In order for all roles to function properly, the tenant-info.yml and topology.yml file must be in place and with the necessary data.

Example tenant-info.yml
```yaml
tenant_name : EDPP
tenant_phydom_name: EDPP-PHYDOM
tenant_aep_name: EDPP-AEP
```

Example topology.yml
```yaml
leafs:
    - 101
    - 102
vpcs:
    - 101-102
```


Author Information
------------------

Eduardo Pozo
