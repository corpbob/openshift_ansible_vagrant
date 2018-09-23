# Install an OpenShift cluster using Vagrant and ansible

## Prerequisites
- Install Vagrant
- Install Ansible
- Your computer has internet access

## The Setup

- 1 master node
  - IP address: 10.1.3.2 
- 1 app node
  - IP address: 10.1.3.3

## How to Run the Installation

- Clone this repository
  
```
git clone https://github.com/corpbob/openshift_ansible_vagrant.git
```

- Change directory to openshift_ansible_vagrant/vagrant directory and run vagrant:

```
cd openshift_ansible_vagrant/vagrant
vagrant up
vagrant provision
```
The username/password for the virtual machines is:

  - username: vagrant
  - password: vagrant

- Run the ansible script to prepare the hosts.

Assuming you are in the directory openshift_ansible_vagrant/vagrant
```
cd ..
ansible-playbook -i hosts openshift.yaml
```

- Clone the openshift-ansible project

```
git clone https://github.com/openshift/openshift-ansible
cd openshift-ansible
git checkout release-3.9
```
- Run the prerequisites playbook

```
ansible-playbook -i hosts openshift-ansible/playbooks/prerequisites.yml
```

- Run the deploy_cluster playbook

```
ansible-playbook -i hosts openshift-ansible/playbooks/deploy_cluster.yml
```

- After the installation, if all goes well, navigate to the Openshift console:

https://master.10.1.3.2.nip.io:8443

