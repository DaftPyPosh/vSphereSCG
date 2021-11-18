# VMware {code} Connect Hackathon 2021 - Team DaftPyPosh - vSphereSCG - Took 2nd Place

![Logo](images/Logo_2_500x126.png)

- [VMware {code} Connect Hackathon 2021 - Team DaftPyPosh - vSphereSCG - Took 2nd Place](#vmware-code-connect-hackathon-2021---team-daftpyposh---vspherescg---took-2nd-place)
  - [CI/CD:](#cicd)
  - [Team Members](#team-members)
  - [The Idea](#the-idea)
    - [Examples around the idea](#examples-around-the-idea)
  - [The Project](#the-project)
    - [Goals](#goals)
    - [Code Structure](#code-structure)
  - [Requirements](#requirements)
    - [vSphere](#vsphere)
    - [Ansible](#ansible)
  - [Usage](#usage)
    - [Install Ansible](#install-ansible)
    - [Install VMware Automation SDK and Tools](#install-vmware-automation-sdk-and-tools)
    - [Install VMware Community Collection](#install-vmware-community-collection)
    - [Run Playbook](#run-playbook)
  - [Features](#features)
    - [ESXi](#esxi)
      - [esxi-7.timekeeping](#esxi-7timekeeping)
      - [esxi-7.lockdown-mode](#esxi-7lockdown-mode)
      - [esxi-7.disable-ssh](#esxi-7disable-ssh)
      - [esxi-7.account-auto-unlock-time](#esxi-7account-auto-unlock-time)
      - [esxi-7.account-lockout](#esxi-7account-lockout)
      - [esxi-7.account-password-history](#esxi-7account-password-history)
      - [esxi-7.account-password-policies](#esxi-7account-password-policies)
      - [esxi.dcui-timeout](#esxidcui-timeout)
      - [esxi-7.disable-mob](#esxi-7disable-mob)
      - [esxi-7.network-bpdu](#esxi-7network-bpdu)
      - [esxi-7.shell-interactive-timeout](#esxi-7shell-interactive-timeout)
      - [esxi-7.shell-timeout](#esxi-7shell-timeout)
      - [esxi-7.shell-warning](#esxi-7shell-warning)
      - [esxi-7.tls-protocols](#esxi-7tls-protocols)
      - [esxi-7.transparent-page-sharing](#esxi-7transparent-page-sharing)
      - [esxi-7.vib-trusted-binaries](#esxi-7vib-trusted-binaries)
      - [esxi-7.logs-level](#esxi-7logs-level)
      - [esxi-7.logs-persistent](#esxi-7logs-persistent)
    - [VM](#vm)
      - [vm-7.disable-console-copy](#vm-7disable-console-copy)
      - [vm-7.disable-console-paste](#vm-7disable-console-paste)
      - [vm-7.disable-disk-shrinking-shrink](#vm-7disable-disk-shrinking-shrink)
      - [vm-7.disable-disk-shrinking-wiper](#vm-7disable-disk-shrinking-wiper)
      - [vm-7.disable-non-essential-3d-features](#vm-7disable-non-essential-3d-features)
      - [vm-7.limit-console-connections](#vm-7limit-console-connections)
      - [vm-7.limit-setinfo-size](#vm-7limit-setinfo-size)
      - [vm-7.log-retention](#vm-7log-retention)
      - [vm-7.log-rotation-size](#vm-7log-rotation-size)
      - [vm-7.restrict-host-info](#vm-7restrict-host-info)
      - [vm-7.vmrc-lock](#vm-7vmrc-lock)
    - [vCenter](#vcenter)
      - [vcenter-7.vami-time](#vcenter-7vami-time)
      - [vcenter-7.vami-syslog](#vcenter-7vami-syslog)
      - [vcenter-7.vami-access-ssh](#vcenter-7vami-access-ssh)
      - [vcenter-7.vami-access-dcli](#vcenter-7vami-access-dcli)

## CI/CD:

| Main Branch     | Any Branch |
| ----------- | ----------- |
| ![Ansible-Lint](https://github.com/DaftPyPosh/vSphereSCG/actions/workflows/main.yml/badge.svg?branch=main)      | ![Ansible-Lint](https://github.com/DaftPyPosh/vSphereSCG/actions/workflows/main.yml/badge.svg)       |
| ![Ansible-Galaxy](https://github.com/DaftPyPosh/vSphereSCG/actions/workflows/publish.yml/badge.svg?branch=main)      | ![Ansible-Galaxy](https://github.com/DaftPyPosh/vSphereSCG/actions/workflows/publish.yml/badge.svg)       |

## Team Members

- Barry Browne [@barrybrowne](https://twitter.com/barrybrowne)
- Bill Kindle [@billkindle](https://www.linkedin.com/in/billkindle/)
- David Prows [@Commputethis](https://twitter.com/commputethis)
- Jon Husen [@JonHusen](https://twitter.com/JonHusen)
- Justin Brant [@JustinBrant93](https://twitter.com/JustinBrant93)
- Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)

## The Idea

We have decided to write an Ansible based toolkit to apply the [VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7) to an existing ESXi deployment.

### Examples around the idea

[VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7)

- ESXi Security Configuration
- VM Security Configuration
- DVS Security Configuration

Some examples how this configurations are possible:

- <https://mycloudrevolution.com/en/2020/06/15/esxi-ntp-security-configuration/>
- <https://mycloudrevolution.com/en/2019/05/27/vsphere-vm-security-configuration-with-ansible/>
- <https://mycloudrevolution.com/en/2019/04/09/vmware-esxi-security-configuration-with-ansible/>
  
As with all projects, 80% of the configuratio can be done pretty quickly, it is the the other 20% that is the problem.

## The Project

### Goals

- 100% of recommendations should be possible (as long as it's not a permanent task like "ESXi is up to date." )
- Configurable which Recommendations should be applied
- Deliverable as Ansible Collection via Ansible Galaxy

### Code Structure

The Project is shipped as an Ansible Collection with Roles. The Roles contain the Hardening Tasks for the infrastructure objects.

``` Markdown
.
└── daftpyposh
    └── vspherescg
        ├── docs
        ├── galaxy.yml
        ├── LICENSE
        ├── plugins
        │   └── README.md
        ├── README.md
        └── roles
            ├── esxi_scg
            │   ├── defaults
            │   │   └── main.yml
            │   ├── files
            │   ├── handlers
            │   │   └── main.yml
            │   ├── meta
            │   │   └── main.yml
            │   ├── README.md
            │   ├── tasks
            │   │   ├── esxi_scg_accountlockfailures.yml
            │   │   ├── esxi_scg_accountunlocktime.yml
            │   │   ├── esxi_scg_dcuitimeout.yml
            │   │   ├── esxi_scg_disableslp.yml
            │   │   ├── esxi_scg_lockdown.yml
            │   │   ├── esxi_scg_logslevel.yml
            │   │   ├── esxi_scg_logspersistent.yml
            │   │   ├── esxi_scg_mob.yml
            │   │   ├── esxi_scg_networkbpdu.yml
            │   │   ├── esxi_scg_ntp.yml
            │   │   ├── esxi_scg_passwordhistory.yml
            │   │   ├── esxi_scg_passwordpolicies.yml
            │   │   ├── esxi_scg_shelldisable.yml
            │   │   ├── esxi_scg_shellinteractivetimeout.yml
            │   │   ├── esxi_scg_shelltimeout.yml
            │   │   ├── esxi_scg_shellwarning.yml
            │   │   ├── esxi_scg_ssh.yml
            │   │   ├── esxi_scg_tlsprotocols.yml
            │   │   ├── esxi_scg_transparentpagesharing.yml
            │   │   ├── esxi_scg_vibtrustedbinaries.yml
            │   │   └── main.yml
            │   ├── templates
            │   ├── tests
            │   │   ├── inventory
            │   │   └── test.yml
            │   └── vars
            │       └── main.yml
            ├── vcenter_scg
            │   ├── defaults
            │   │   └── main.yml
            │   ├── files
            │   ├── handlers
            │   │   └── main.yml
            │   ├── meta
            │   │   └── main.yml
            │   ├── README.md
            │   ├── tasks
            │   │   ├── main.yml
            │   │   ├── vcenter_scg_vami_dcui.yml
            │   │   ├── vcenter_scg_vami_ntp.yml
            │   │   ├── vcenter_scg_vami_ssh.yml
            │   │   └── vcenter_scg_vami_syslog.yml
            │   ├── templates
            │   ├── tests
            │   │   ├── inventory
            │   │   └── test.yml
            │   └── vars
            │       └── main.yml
            └── vm_scg
                ├── defaults
                │   └── main.yml
                ├── files
                ├── handlers
                │   └── main.yml
                ├── meta
                │   └── main.yml
                ├── README.md
                ├── tasks
                │   ├── main.yml
                │   ├── vm_scg_disable_3d.yml
                │   ├── vm_scg_disable_copy.yml
                │   ├── vm_scg_disable_disk_shrink.yml
                │   ├── vm_scg_disable_disk_wiper.yml
                │   ├── vm_scg_disable_paste.yml
                │   ├── vm_scg_limit_setinfo.yml
                │   ├── vm_scg_limit_vmrc.yml
                │   ├── vm_scg_log_retention.yml
                │   ├── vm_scg_log_rotation.yml
                │   ├── vm_scg_restrict_host_info.yml
                │   └── vm_scg_vmrc_lock.yml
                ├── templates
                ├── tests
                │   ├── inventory
                │   └── test.yml
                └── vars
                    └── main.yml
```

## Requirements

### vSphere

- The code can only be run against vSphere Clusters.  It is not supported on a single host.
- VMware vSphere 7.0+

### Ansible

- Ansible 2.10.3+
- community.vmware Collection 1.14.0+

## Usage

### Install Ansible

```pip3 install --user ansible```

### Install VMware Automation SDK and Tools

``` Ansible
- name: Prepare Ansible Box for my Projects
  hosts: localhost
  gather_facts: false
  tasks:
  - name: Ansible-Lint
    pip:
        name: ansible-lint
        extra_args: "--upgrade --user"
  - name: PIP setuptools
    pip:
        name: setuptools
        extra_args: "--upgrade --user"
  - name: PIP pyVmomi
    pip:
        name: pyVmomi
        extra_args: "--upgrade --user" 
  - name: PIP VMware vSphere Automation SDK for Python
    pip:
        name: git+https://github.com/vmware/vsphere-automation-sdk-python.git
        extra_args: "--upgrade --user"

```

### Install VMware Community Collection

```ansible-galaxy collection install community.vmware```

### Run Playbook

```ansible-playbook vSphereSCG.yml```

## Features

### ESXi

#### esxi-7.timekeeping

Cryptography, audit logging, cluster operations, and incident response/forensics depend deeply on synchronized time. The recommendation for NTP is to have at least four sources. Do not have two sources (one source is preferable to two).

- Manage NTP Firewall Rules
- Set NTP servers
- Set NTP Service

#### esxi-7.lockdown-mode

Enabling lockdown mode disables direct access to an ESXi host and requires that the host managed remotely from vCenter Server.  This is done to ensure the roles and access controls implemented in vCenter are always enforced and users cannot bypass them by logging into a host directly.   By forcing all interaction to occur through vCenter Server, the risk of someone inadvertently attaining elevated privileges or performing tasks that are not properly audited is greatly reduced.  Note:  Lockdown mode does not apply to  users who log in using authorized keys. When you use an authorized key file for root user authentication, root users are not prevented from accessing a host with SSH even when the host is in lockdown mode.

Note that users listed in the DCUI.Access list for each host are allowed to override lockdown mode and login to the DCUI.  

By default the "root" user is the only user listed in the DCUI.Access list.

There are three settings for lockdown mode: disabled, normal, and strict. The choice of strict means that if the ESXi host loses contact with vCenter Server it cannot be managed in any way until that connection is restored. If that connection cannot be restored the host will need to be rebuilt. This is beyond the needs of most deployments. As such, we recommend normal lockdown mode.Enabling lockdown mode disables direct access to an ESXi host and requires that the host managed remotely from vCenter Server.  This is done to ensure the roles and access controls implemented in vCenter are always enforced and users cannot bypass them by logging into a host directly.   By forcing all interaction to occur through vCenter Server, the risk of someone inadvertently attaining elevated privileges or performing tasks that are not properly audited is greatly reduced.  Note:  Lockdown mode does not apply to  users who log in using authorized keys. When you use an authorized key file for root user authentication, root users are not prevented from accessing a host with SSH even when the host is in lockdown mode.

Note that users listed in the DCUI.Access list for each host are allowed to override lockdown mode and login to the DCUI.  

By default the "root" user is the only user listed in the DCUI.Access list.

There are three settings for lockdown mode: disabled, normal, and strict. The choice of strict means that if the ESXi host loses contact with vCenter Server it cannot be managed in any way until that connection is restored. If that connection cannot be restored the host will need to be rebuilt. This is beyond the needs of most deployments. As such, we recommend normal lockdown mode.

#### esxi-7.disable-ssh

ESXi is not a UNIX-like multiuser OS -- it is a purpose-built hypervisor intended to be managed via the Host Client, vSphere Client, and/or APIs. On ESXi, SSH is a troubleshooting and support interface, and is intentionally stopped and disabled by default. Enablement of the interface brings risk.

#### esxi-7.account-auto-unlock-time

Multiple account login failures for the same account can indicate a security problem. Such attempts to brute force the system should be limited by locking out the account after reaching a threshold. However, as this can be used to deny service an unlock period is often specified.

#### esxi-7.account-lockout

Multiple account login failures for the same account can indicate a security problem. Such attempts to brute force the system should be limited by locking out the account after reaching a threshold.

#### esxi-7.account-password-history

Because of password complexity guidelines users will sometimes attempt to reuse older passwords. This setting prevents that.

#### esxi-7.account-password-policies

It is important to use passwords that are not easily guessed and that are difficult for password generators to determine. Password strength and complexity rules apply to all ESXi users, including root. They do not apply to Active Directory users when the ESX host is joined to a domain, as those password policies are enforced by AD.

More information can be found at <https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-DC96FFDB-F5F2-43EC-8C73-05ACDAE6BE43.html>

#### esxi.dcui-timeout

DCUI is used for directly logging into ESXi host and carrying out host management tasks. The idle connections to DCUI must be terminated to avoid any unintended usage of the DCUI originating from a left over login session.

#### esxi-7.disable-mob

The managed object browser (MOB) provides a way to explore the object model used by the VMkernel to manage the host; it enables configurations to be changed as well. This interface is meant to be used primarily for debugging the vSphere SDK. Please audit your ESXi servers to ensure someone hasn't turned on the MOB.

#### esxi-7.network-bpdu

BPDU Guard and Portfast are commonly enabled on the physical switch to which the ESXi host is directly connected to reduce the spanning tree convergence delay.

If a BPDU packet is sent from a virtual machine on the ESXi host to the physical switch so configured, a cascading lockout of all the uplink interfaces from the ESXi host can occur.

To prevent this type of lockout, BPDU Filter can be enabled on the ESXi host to drop any BPDU packets being sent to the physical switch.

Some network-oriented workloads can legitimately generate BPDU packets. The administrator should verify that there are no legitimate BPDU packets generated by virtual machines on the ESXi host prior to enabling BPDU Filter.

If BPDU Filter is enabled in this situation, enabling Reject Forged Transmits on the virtual switch port group adds protection against Spanning Tree loops.

#### esxi-7.shell-interactive-timeout

If a user forgets to log out of their SSH session, the idle connection will remains open indefinitely, increasing the potential for someone to gain privileged access to the host.  The ESXiShellInteractiveTimeOut allows you to automatically terminate idle shell sessions.

#### esxi-7.shell-timeout

When the ESXi Shell or SSH services are enabled on a host they will run indefinitely.  To avoid having these services left running set the ESXiShellTimeOut.  The ESXiShellTimeOut defines a window of time after which the ESXi Shell and SSH services will automatically be terminated.

#### esxi-7.shell-warning

SSH and the ESXi Shell are troubleshooting and support interfaces, and are intentionally stopped and disabled by default. Enablement of those interfaces brings risk. Dismissal of the warning masks potential risk present.

#### esxi-7.tls-protocols

ESXi 7 ships with TLS 1.2 enabled.

#### esxi-7.transparent-page-sharing

Transparent Page Sharing (TPS) is a method to reduce the memory footprint of virtual machines. Under highly controlled conditions it can be used to gain unauthorized access to data on neighboring virtual machines.

VMs that do not have the sched.mem.pshare.salt option set cannot share memory with any other VMs.

Large page sizes, a performance optimization in the hypervisor on many modern CPUs, is incompatible with TPS.

#### esxi-7.vib-trusted-binaries

ESXi conducts integrity checks of "vSphere Installable Bundles" or VIBs, governed by the Acceptance Level (see below). Instructing ESXi to only execute binaries that originated from a valid VIB installed on the host makes it harder for attackers to use prebuilt toolkits during a compromise, and increases chances of detection.

#### esxi-7.logs-level

It is important to ensure that enough information is present in audit logs for diagnostics and forensics.

#### esxi-7.logs-persistent

ESXi can be configured to store log files on an in-memory file system.  This occurs when the host's "/scratch" directory is linked to "/tmp/scratch". When this is done only a single day's worth of logs are stored at any time. In addition log files will be reinitialized upon each reboot.  This presents a security risk as user activity logged on the host is only stored temporarily and will not persistent across reboots.  This can also complicate auditing and make it harder to monitor events and diagnose issues.  ESXi host logging should always be configured to a persistent datastore.

### VM

#### vm-7.disable-console-copy

Copy and paste operations are disabled by default. However, if you explicitly disable this feature audit controls can check that this setting is correct.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to TRUE.

#### vm-7.disable-console-paste

Copy and paste operations are disabled by default, however, if you explicitly disable this feature, audit controls can check that this setting is correct.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to TRUE.

#### vm-7.disable-disk-shrinking-shrink

Repeated disk shrinking can make a virtual disk unavailable. Limited capability is available to non-administrative users in the guest.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to TRUE.

#### vm-7.disable-disk-shrinking-wiper

Repeated disk shrinking can make a virtual disk unavailable. Limited capability is available to non-administrative users in the guest.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to TRUE.

#### vm-7.disable-non-essential-3d-features

It is suggested that 3D be disabled on virtual machines that do not require 3D functionality, (e.g. server or desktops not using 3D applications).

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to FALSE.

#### vm-7.limit-console-connections

Multiple users can connect to a single VM console and observe activity. Limiting this to 1 prevents this behavior.

#### vm-7.limit-setinfo-size

The configuration file containing these name-value pairs is limited to a size of 1 MB by default. This limit is applied even when the sizeLimit parameter is not listed in the .vmx file. Uncontrolled size for the VMX file can lead to denial of service if the datastore is filled.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to 1048576.

#### vm-7.log-retention

By default there is a limit of 6 old diagnostic logs. The VMware documentation recommends setting this to 10 to conserve datastore space but also enable troubleshooting should it need to occur.

#### vm-7.log-rotation-size

By default there is no limit on VM diagnostic log sizes, and they are rotated when the VM changes power state or live-migrates using vMotion. On long-running VMs this may consume considerable space. The VMware documentation recommends setting this no lower than 2 MB (measured in KB).

#### vm-7.restrict-host-info

"By enabling a VM to get detailed information about the physical host, an adversary could potentially use this information to inform further attacks on the host.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to FALSE."

#### vm-7.vmrc-lock

An attacker can take advantage of console sessions left logged in.

### vCenter

#### vcenter-7.vami-time

Cryptography, audit logging, cluster operations, and incident response/forensics depend deeply on synchronized time. The recommendation for NTP is to have at least four sources. Do not have two sources (one source is preferable to two).

This was configured during install so it should be audited for correctness.

#### vcenter-7.vami-syslog

Remote logging to a central log host provides a secure, centralized store for vCenter Server logs. By gathering host log files onto a central host you can more easily monitor all hosts with a single tool. You can also do aggregate analysis and searching to look for such things as coordinated attacks on multiple hosts. Logging to a secure, centralized log server helps prevent log tampering and also provides a long-term audit record.

#### vcenter-7.vami-access-ssh

vCenter Server is delivered as an appliance, and intended to be managed through the VAMI, vSphere Client, and APIs. SSH is a troubleshooting and support tool and should only be enabled when necessary.

vCenter Server High Availability uses SSH to coordinate the replication and failover between the nodes. Use of this feature requires SSH to remain enabled.vCenter Server is delivered as an appliance, and intended to be managed through the VAMI, vSphere Client, and APIs. SSH is a troubleshooting and support tool and should only be enabled when necessary.

vCenter Server High Availability uses SSH to coordinate the replication and failover between the nodes. Use of this feature requires SSH to remain enabled.

#### vcenter-7.vami-access-dcli

The Datacenter CLI is a CLI/API designed to speed management operations on vCenter Server appliance itself. If you are not using it we suggest disabling it to reduce attack surface.
