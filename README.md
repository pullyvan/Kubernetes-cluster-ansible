# Ansible role for Kubernetes master and node

Ansible playbooks to setup a kubernetes cluster

## Inventory
```
git clone https://github.com/pullyvan/kubernetes-master-ansible.git
cd kubernetes-master-ansible
```
Edit master_prod in inventory folder, add your master server
Edit node_prod in inventory folder, add your node server

## Master
To setup a master server
```
ansible-playbook -u root -i inventory/master_prod playbooks/main.yml
```
## Node
To setup a node server you will need to perform few changes to main playbooks files.
From the kubernetes-master-ansible folder, edit the main playbooks
```
- name: This is the main playbook
  hosts: all
  tasks:

    - name: Update and upgrade all packages
      include_role:
        name: roles/update-system

    - name: Install Docker
      include_role:
        name: roles/ansible_docker

    - name: Install Kubernetes packages and setup the cluster
      include_role:
        name: roles/ansible_role_node_kubernetes
```
From the terminal run these command

```
ansible-playbook -u root -i inventory/node_prod playbooks/main.yml
```
