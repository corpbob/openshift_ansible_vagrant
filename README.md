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
- Openshift 3.9

## How to Run the Installation

*Note: All commands are run in the local machine.*

0. If you don't have an ssh key pair, execute the following:

```
ssh-keygen
```

Accept the defaults and don't enter a password.

1. Clone this repository
  
```
git clone https://github.com/corpbob/openshift_ansible_vagrant.git
```

2. Change directory to openshift_ansible_vagrant/vagrant directory and run vagrant:

```
cd openshift_ansible_vagrant/vagrant
vagrant up
vagrant provision
```
The username/password for the virtual machines is:

  - username: vagrant
  - password: vagrant

Make sure that you can ssh to the machines without a password. Execute the following commands:

```
ssh vagrant@10.1.3.2
ssh vagrant@10.1.3.3
```

3. Run the ansible script to prepare the hosts.

Assuming you are in the directory openshift_ansible_vagrant/vagrant
```
cd ..
ansible-playbook -i hosts openshift.yaml
```

4. Clone the openshift-ansible project

```
git clone https://github.com/openshift/openshift-ansible
( cd openshift-ansible &&  git checkout release-3.9)
```
5. Run the prerequisites playbook

```
ansible-playbook -i hosts openshift-ansible/playbooks/prerequisites.yml
```

6. Run the deploy_cluster playbook

```
ansible-playbook -i hosts openshift-ansible/playbooks/deploy_cluster.yml
```

7. After the installation, if all goes well, navigate to the Openshift console:

https://master.10.1.3.2.nip.io:8443

Login credentials:
- username: admin
- password: admin

8. Give admin the role cluster-admin:

```
oc adm policy add-cluster-role-to-user cluster-admin admin
```


