Role Name
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
vcenter_hostname: 'vcenter.lab.local'
vcenter_username: 'Administrator@vsphere.local'
vcenter_password: 'C0mpl3x!'
cluster_name: 'lab'

vcenter_scg_vami_ntp: true
vc_ntp1: '0.pool.ntp.org'
vc_ntp2: '1.pool.ntp.org'
vc_ntp3: '2.pool.ntp.org'
vc_ntp4: '3.pool.ntp.org'
vcenter_scg_vami_syslog: true
vc_syslog_hostname: 'syslog.lab.local'
vc_syslog_port: '514'
vc_syslog_protocol: 'UDP'
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

    vcenter_scg_vami_ntp: true
    vc_ntp1: '0.pool.ntp.org'
    vc_ntp2: '1.pool.ntp.org'
    vc_ntp3: '2.pool.ntp.org'
    vc_ntp4: '3.pool.ntp.org'
    vcenter_scg_vami_syslog: true
    vc_syslog_hostname: 'syslog.lab.local'
    vc_syslog_port: '514'
    vc_syslog_protocol: 'UDP'

  collections:
    - daftpyposh.vspherescg
  tasks:
    - name: import vCenter role from a collection
      import_role:
        name: daftpyposh.vspherescg.vcenter_scg

```

License
-------

BSD

Author Information
------------------

- Barry Browne [@barrybrowne](https://twitter.com/barrybrowne)
- Bill Kindle [@billkindle](https://www.linkedin.com/in/billkindle/)
- David Prows [@Commputethis](https://twitter.com/commputethis)
- Jon Husen [@JonHusen](https://twitter.com/JonHusen)
- Justin Brant [@JustinBrant93](https://twitter.com/JustinBrant93)
- Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)
- Carl Capozza [@Carlcapozza](https://twitter.com/Carlcapozza)
