daftpyposh.vspherescg.esxi_scg
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

``` Ansible
esxi_scg_ntp: false
esxi_scg_lockdown: false
esxi_scg_ssh: false
esxi_scg_accountlockfailures: false
esxi_scg_accountunlocktime: false
esxi_scg_passwordhistory: false
esxi_scg_passwordpolicies: false
esxi_scg_dcuitimeout: false
esxi_scg_mob: false
esxi_scg_networkbpdu: false
esxi_scg_shellinteractivetimeout: false
esxi_scg_shelltimeout: false
esxi_scg_shellwarning: false
esxi_scg_tlsprotocols: false
esxi_scg_transparentpagesharing: false
esxi_scg_vibtrustedbinaries: false
esxi_scg_logslevel: false

vcenter_hostname: 'vcenter.lab.local'
vcenter_username: 'Administrator@vsphere.local'
vcenter_password: 'C0mpl3x!'
cluster_name: 'lab'

ntp1: '192.168.2.100'
ntp2: '192.168.2.101'
ntp3: '192.168.2.102'
ntp4: '192.168.2.103'
```

Dependencies
------------

Colections:

- communnity.vmware

Example Playbook
----------------

``` Ansible
- name: Execute Ansible based toolkit to apply the vSphere Security Configuration Guide
  hosts: localhost
  gather_facts: false
  vars:
    vcenter_hostname: 'vcenter.lab.local'
    vcenter_username: 'Administrator@vsphere.local'
    vcenter_password: 'C0mpl3x!'
    cluster_name: 'lab'

    esxi_scg_ntp: true
    ntp1: '192.168.2.100'
    ntp2: '192.168.2.101'
    ntp3: '192.168.2.102'
    ntp4: '192.168.2.103'

    esxi_scg_lockdown: true
    esxi_scg_ssh: true
    esxi_scg_accountlockfailures: true
    esxi_scg_accountunlocktime: true
    esxi_scg_passwordhistory: true
    esxi_scg_passwrodpolicies: true
    esxi_scg_dcuitimeout: true
    esxi_scg_networkbpdu: true
    esxi_scg_shellinteractivetimeout: true
    esxi_scg_shelltimeout: true
    esxi_scg_shellwarning: true
    esxi_scg_tlsprotocols: true
    esxi_scg_transparentpagesharing: true
    esxi_scg_vibtrustedbinaries: true

  collections:
    - daftpyposh.vspherescg
  tasks:
    - name: import ESXi role from a collection
      import_role:
        name: daftpyposh.vspherescg.esxi_scg

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
