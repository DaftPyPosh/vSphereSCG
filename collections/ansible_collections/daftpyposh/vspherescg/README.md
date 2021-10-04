# Ansible Collection - daftpyposh.vspherescg

Ansible based toolkit to apply the [VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7) to an existing ESXi deployment.

## Requirements

---

### vSphere

- The code can only be run against vSphere Clusters.  It is not supported on a single host.
- VMware vSphere 7.0+

### Ansible

- Ansible 2.10.3+
- community.vmware Collection 1.14.0+

## Collection Variables

---

``` Ansible
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
esxi_scg_logslevel: true

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

## Dependencies

---

### Colections

- communnity.vmware

## Example Playbook

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
    esxi_scg_logslevel: true

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
    - name: import ESXi role from a collection
      import_role:
        name: daftpyposh.vspherescg.esxi_scg
    - name: import VM role from a collection
      import_role:
        name: daftpyposh.vspherescg.vm_scg

```

## License

---

 GNU GPLv3

## Author Information

---

- Barry Browne [@barrybrowne](https://twitter.com/barrybrowne)
- Bill Kindle [@billkindle](https://www.linkedin.com/in/billkindle/)
- David Prows [@Commputethis](https://twitter.com/commputethis)
- Jon Husen [@JonHusen](https://twitter.com/JonHusen)
- Justin Brant [@JustinBrant93](https://twitter.com/JustinBrant93)
- Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)
