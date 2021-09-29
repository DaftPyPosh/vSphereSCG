daftpyposh.vspherescg.vm_scg
=========

Ansible based toolkit to apply the [VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7) to an existing ESXi deployment.

Requirements
------------

vSphere:

- The code can only be run against vSphere Clusters.  It is not supported on a single host.
- VMware vSphere 7.0+

Ansible:

- Ansible 2.10.3+
- community.vmware Collection 1.14.0+

Role Variables
--------------

```
vm_scg_disable_copy: false
vm_scg_disable_paste: false
vm_scg_disable_disk_shrink: false
vm_scg_disable_disk_wiper: false
vm_scg_disable_3d: false
vm_scg_limit_vmrc: false
vm_scg_limit_setinfo: false
vm_scg_log_retention: false
vm_scg_log_rotation: false
vm_scg_restrict_host_info: false
vm_scg_vmrc_lock: false

vcenter_hostname: 'vcenter.lab.local'
vcenter_username: 'Administrator@vsphere.local'
vcenter_password: 'C0mpl3x!'
cluster_name: 'lab'

```
Dependencies
------------

Colections:

- communnity.vmware

Example Playbook
----------------

```
- name: Execute Ansible based toolkit to apply the vSphere Security Configuration Guide
  hosts: localhost
  gather_facts: false
  vars:
    vcenter_hostname: 'vcenter.lab.local'
    vcenter_username: 'Administrator@vsphere.local'
    vcenter_password: 'C0mpl3x!'
    cluster_name: 'lab'

    vm_scg_disable_copy: true
    vm_scg_disable_paste: true
    vm_scg_disable_disk_shrink: true
    vm_scg_disable_disk_wiper: true
    vm_scg_disable_3d: true
    vm_scg_limit_vmrc: true
    vm_scg_limit_setinfo: true
    vm_scg_log_retention: true
    vm_scg_log_rotation: true
    vm_scg_restrict_host_info: true
    vm_scg_vmrc_lock: true

  collections:
    - daftpyposh.vspherescg
  tasks:
    - name: import VM role from a collection
      import_role:
        name: daftpyposh.vspherescg.vm_scg

```

License
-------

 GNU GPLv3

Author Information
------------------

- Barry Browne [@barrybrowne](https://twitter.com/barrybrowne)
- Bill Kindle [@billkindle](https://www.linkedin.com/in/billkindle/)
- David Prows [@Commputethis](https://twitter.com/commputethis)
- Jon Husen [@JonHusen](https://twitter.com/JonHusen)
- Justin Brant [@JustinBrant93](https://twitter.com/JustinBrant93)
- Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)
- Carl Capozza [@Carlcapozza](https://twitter.com/Carlcapozza)
