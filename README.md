# Install an OpenShift cluster using Vagrant and ansible

## Prerequisites

Install the following in your local machine:

   - VirtualBox
   - Vagrant
   - Ansible
   - Git

- Your computer has internet access

## The Setup

- 1 master node
  - IP address: 10.1.3.2 
- 1 app node
  - IP address: 10.1.3.3
- 1 bastion node:
  - IP address: 10.1.3.4
- Openshift 3.9

## How to Run the Installation

*Note: All commands are run in the bastion host.*

1. Clone this repository
  
```
git clone https://github.com/corpbob/openshift_ansible_vagrant.git
```

2. Change directory to openshift_ansible_vagrant/vagrant directory and run vagrant:

```
cd openshift_ansible_vagrant/vagrant
vagrant up
```
The username/password for the virtual machines is:

  - username: vagrant
  - password: vagrant

3. Go to the VirtualBox window of the bastion host and login as vagrant/vagrant. Run the ansible script to prepare the hosts.

In the /home/vagrant directory enter the commands:

```
ansible-playbook -i hosts openshift.yaml
```

4. Run the prerequisites playbook

```
ansible-playbook -i hosts openshift-ansible/playbooks/prerequisites.yml
```

5. Run the deploy_cluster playbook

```
ansible-playbook -i hosts openshift-ansible/playbooks/deploy_cluster.yml
```
6. Run the fix.yml playbook:

```
ansible-playbook -i hosts fix.yml
```
7. Give admin the role cluster-admin:

```
oc adm policy add-cluster-role-to-user cluster-admin admin
```

8. If all goes well, navigate to the Openshift console:

https://master.10.1.3.2.nip.io:8443

Login credentials:
- username: admin
- password: admin


