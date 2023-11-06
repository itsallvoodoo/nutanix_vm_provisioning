provision_vm_role
=========

A role to provision a vm in nutanix

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

### Variables
|Variable Name|Default Value|Required|Type|Description|
|:---:|:---:|:---:|:---:|:---:|
|`ntx_host`||yes|str|Nutanix VM hostname.|
|`ntx_port`|9440|no|int|Nutanix port.|
|`ntx_user`||yes|str|Nutanix username. Ex: <username>@<domain>|
|`ntx_password`||yes|str|Nutanix password.|
|`ntx_validate_certs`|False|no|bool|Whether to validate the certificate of the Nutanix host|
|`ntx_cluster_name`||yes|str||
|`provision_vm_role_provision_vms`|{}|yes|dict|Dictionary of hostnames to provision and an initialization script for guest customization|
|`provision_vm_role_image_name`||yes|str|Name of image used to create a new VM. Ex: windows_2019|  
|`provision_vm_role_cores_per_vcpu`||yes|int|Number of cores per vcpu|
|`provision_vm_role_memory_gb`||yes|int|Memory amount in GB|
|`provision_vm_role_nutanix_network_name`||yes|str|Name of the subnet to attach the VM|
|`provision_vm_role_vcpus`||yes|int|Number of vCPU's|


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
Example of how to reference this role in a playbook.

```yaml
---
- name: Provision in Nutanix
  hosts: all
  gather_facts: no
  tasks:
    - name: provision a vm in nutanix
      ansible.builtin.import_role:
        name: provision_vm_role
      vars:
        ntx_host: "ntx host"
        ntx_port: 9224
        ntx_user: "ntx username"
        ntx_password: "ntx password"
        ntx_validate_certs: False
        provision_vm_role_image_name: "rhel9latest"
        provision_vm_role_vcpus: 2
        provision_vm_role_cores_per_vcpu: 2
        provision_vm_role_memory_gb: 8
        provision_vm_role_nutanix_network_name: "provisioning-network"
        provision_vm_role_provision_vms:
          - hostname: 'server01'
            init_script: '/path/to/script/server01_init'
          - hostname: 'server02'
            init_script: '/path/to/script/server02_init'
...
```

Behaviors
---------
- Success: Role will create a new VM in Nutanix cluster
- Error: Failure to pass required variables
- Error: Nutanix credentials are incorrect
- Error: Nutanix host is unavailable

License
-------

MIT

Author Information
------------------
Tony Reveal
