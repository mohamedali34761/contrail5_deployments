## Steps to deploy Contrail 5.0.3 on single server or VM

1. Bring up 1 Centos 7.5 (1804) Servers or Virtual Machines with recommended specifications 
   for Contrail deployments, 1 contrail Controller+OpenStack+Compute 
2. Install required packages on server or VM
```
yum install -y epel-release
yum install -y git python-pip net-tools sshpass
pip install ansible==2.4.2.0
```
3. Download  [Contrail 5.0.3 GA code](https://www.juniper.net/support/downloads/?p=contrail#sw),
```
tar -zxvf contrail-ansible-deployer-5.0.3-0.493.tgz
cd contrail-ansible-deployer
```
4. Copy [instances.yaml](https://github.com/urao/contrail5_deployments/blob/master/5_0_3_deployments/openstack_queens/instances.yaml) 
   into $HOME/contrail-ansible-deployer/config/ folder
5. Add docker registry credentials and make IP address changes as per your topology
6. Execute the below commands from deployer VM.
```
cd contrail-ansible-deployer
ansible-playbook -i inventory/ -e orchestrator=openstack playbooks/configure_instances.yml
```
7. Deploy Openstack 
```
ansible-playbook -i inventory/ playbooks/install_openstack.yml
```
8. Deploy Contrail 
```
ansible-playbook -i inventory/ -e orchestrator=openstack playbooks/install_contrail.yml
```
