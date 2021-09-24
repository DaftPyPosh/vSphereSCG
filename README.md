# VMware {code} Connect Hackathon 2021 - Team DaftPyPosh - vSphereSCG

![Logo](images/logo_1_500x126.png)

- [VMware {code} Connect Hackathon 2021 - Team DaftPyPosh - vSphereSCG](#vmware-code-connect-hackathon-2021---team-daftpyposh---vspherescg)
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
    - [vCenter](#vcenter)
      - [vcenter-7.vami-time](#vcenter-7vami-time)

## Team Members

- Barry Browne [@barrybrowne](https://twitter.com/barrybrowne)
- Bill Kindle [@billkindle](https://www.linkedin.com/in/billkindle/)
- Carl Capozza [@Carlcapozza](https://twitter.com/Carlcapozza)
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

The Project is shipped as an Ansible Collection with Roles. The Roles do contain the Hardening Tasks for the infrastructure objects.

``` Markdown
daftpyposh
└── vspherescg
 ├── docs
 ├── galaxy.yml
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
     │   │   ├── esxi_scg_ntp.yml
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
     │   │   └── main.yml
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
         │   └── main.yml
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

```
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

### vCenter

#### vcenter-7.vami-time

Cryptography, audit logging, cluster operations, and incident response/forensics depend deeply on synchronized time. The recommendation for NTP is to have at least four sources. Do not have two sources (one source is preferable to two).

This was configured during install so it should be audited for correctness.
