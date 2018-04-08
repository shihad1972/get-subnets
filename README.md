get-subnets
=========

Get EC2 VPC subnet facts based on tags. Use this role to return a list
of subnet ID's in a variable subnet_ids that you can then use in other
roles.
If you are using the Availability Zone tag key, then you can define
subnet_has_az_tags to get a the availability zones the subnets are in
from the subnet_azs variable. The index in this list will correspond to
the index in the subnet_ids variable
Requirements
------------

Ansible 2.3 and boto module are required for this role

Role Variables
--------------

Required variables for this role are as follows:

  - region: AWS region
 One of:
    - vpc_name: Name of the vpc
    - vpc_id: AWS VPC identifier.

You can then choose how to get the subnets based on the following variables:

  - subnet_name: A list of subnet names; returns the corresponding subnet ID's
  - subnet_tier: if defined, the value of {{ subnet_layer }} will be used to match
    the Tier tag of the subnet. Values could be: application, presentation, data
  - subnet_env_tier: If defined, the role will take the variable values for
    environment and tier to get the list of subnets. You will need to pass in
    the full name for the Environment as {{ environ }} variable and also the
    {{ subnet_layer }} variable will be used for the Tier tag.
  - environ: 
  - subnet_has_az_tags: define if you are using Availability zone: tags in
    your subnets.

  
Dependencies
------------

No depenencies on other ansible roles

Example Playbook
----------------

    - hosts: localhost
      vars:
        subnet_tier: true
        subnet_layer: application
        region: us-east-1
        vpc_name: PFE VPC
      roles:
         - role: get-subnets

License
-------

GPL

Author Information
------------------

Iain M Conochie <iain@shihad.org>


Bugs
----

Playbook fails in role at set_fact task with error:
    the field 'args' has an invalid value, which appears to include a variable that is undefined.

Check your seubnet names; if the role is unable to locate your subnets, there will be no results and the role will fail

