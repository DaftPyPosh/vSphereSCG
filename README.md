# VMware {code} Connect Hackathon 2021 - Team DaftPyPosh - vSphereSCG

![Logo](images/logo_1_500x126.png)

## Team Members

- Barry Browne [@barrybrowne](https://twitter.com/barrybrowne)
- Bill Kindle [@billkindle](https://www.linkedin.com/in/billkindle/)
- Carl Capozza [@Carlcapozza](https://twitter.com/Carlcapozza)
- David Prows [@Commputethis](https://twitter.com/commputethis)
- Jon Husen [@JonHusen](https://twitter.com/JonHusen)
- Justin Brant [@JustinBrant93](https://twitter.com/JustinBrant93)
- Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)

## The Idea

An Ansible based toolkit to apply the [VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7) to an existing infrastructure.

### Examples around the idea

[VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7)

- ESXi Security Configuration
- VM Security Configuration
- DVS Security Configuration

Some examples how this configurations are possible:

- <https://mycloudrevolution.com/en/2020/06/15/esxi-ntp-security-configuration/>
- <https://mycloudrevolution.com/en/2019/05/27/vsphere-vm-security-configuration-with-ansible/>
- <https://mycloudrevolution.com/en/2019/04/09/vmware-esxi-security-configuration-with-ansible/>
  
80% of the configurations might be done pretty quick, the other 20% are the problem.

## Goals

- 100% of recommendations should be possible (as long as it's not a permanent task like "ESXi is up to date." )
- Configurable which Recommendations should be applied
- Deliverable as Ansible Collection via Ansible Galaxy

## Code Structure

The Project is shipped as an Ansible Collection with Roles. The Roles do contain the Hardening Tasks for the infrastructure objects.

```
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

- Only vSphere Clusters can be managed, no single Hosts
- VMware vSphere 7.0+

### Ansible

- Ansible 2.10.3+
- community.vmware Collection 1.14.0+
## Usage

### Install Ansible

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

### esxi-7.lockdown-mode

Enabling lockdown mode disables direct access to an ESXi host and requires that the host managed remotely from vCenter Server.  This is done to ensure the roles and access controls implemented in vCenter are always enforced and users cannot bypass them by logging into a host directly.   By forcing all interaction to occur through vCenter Server, the risk of someone inadvertently attaining elevated privileges or performing tasks that are not properly audited is greatly reduced.  Note:  Lockdown mode does not apply to  users who log in using authorized keys. When you use an authorized key file for root user authentication, root users are not prevented from accessing a host with SSH even when the host is in lockdown mode. 

Note that users listed in the DCUI.Access list for each host are allowed to override lockdown mode and login to the DCUI.  

By default the "root" user is the only user listed in the DCUI.Access list.

There are three settings for lockdown mode: disabled, normal, and strict. The choice of strict means that if the ESXi host loses contact with vCenter Server it cannot be managed in any way until that connection is restored. If that connection cannot be restored the host will need to be rebuilt. This is beyond the needs of most deployments. As such, we recommend normal lockdown mode.Enabling lockdown mode disables direct access to an ESXi host and requires that the host managed remotely from vCenter Server.  This is done to ensure the roles and access controls implemented in vCenter are always enforced and users cannot bypass them by logging into a host directly.   By forcing all interaction to occur through vCenter Server, the risk of someone inadvertently attaining elevated privileges or performing tasks that are not properly audited is greatly reduced.  Note:  Lockdown mode does not apply to  users who log in using authorized keys. When you use an authorized key file for root user authentication, root users are not prevented from accessing a host with SSH even when the host is in lockdown mode. 

Note that users listed in the DCUI.Access list for each host are allowed to override lockdown mode and login to the DCUI.  

By default the "root" user is the only user listed in the DCUI.Access list.

There are three settings for lockdown mode: disabled, normal, and strict. The choice of strict means that if the ESXi host loses contact with vCenter Server it cannot be managed in any way until that connection is restored. If that connection cannot be restored the host will need to be rebuilt. This is beyond the needs of most deployments. As such, we recommend normal lockdown mode.

### VM

### vm-7.disable-console-copy

Copy and paste operations are disabled by default. However, if you explicitly disable this feature audit controls can check that this setting is correct.

As the default is the desired state you can audit by verifying that the parameter is either unset, or if it is set it is set to TRUE.
