# VMware {Code} Hackathon 2021 - Team DaftPyPosh - vSphereSCG

![Logo](images/logo_1_500x126.png)
## Team Members
- Barry Browne
- Bill Kindle
- Carl Capozza
- David Prows
- Jon Husen
- Justin Brant
- Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)

## The Idea
An Ansible based toolkit to apply the [VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7) to an exisitng infrastructure.
### Examples around the idea
[VMware vSphere Security Configuration Guide](https://core.vmware.com/vmware-vsphere-security-configuration-guide-7)
 - ESXi Security Configuration
 - VM Security Configuration
 - DVS Security Configuration

Some examples how this configurations are possible:
- https://mycloudrevolution.com/en/2020/06/15/esxi-ntp-security-configuration/
- https://mycloudrevolution.com/en/2019/05/27/vsphere-vm-security-configuration-with-ansible/
- https://mycloudrevolution.com/en/2019/04/09/vmware-esxi-security-configuration-with-ansible/
  
80% of the configurations might be done pretty quick, the other 20% are the problem.

## Goals
- 100% of recommendations should be possible (as long as it's not a permanent task like "ESXi is up to date." )
- Configurable which Recommendations should be applied 
- Deliverable as Ansible Collection via Ansible Galaxy