# JBoss EAP with postgresql drivers

This repository contains a set of Ansible based roles and playbooks to demonstrate the deployment of a [JBoss EAP](https://wildfly.org/) cluster, postgresql database, postgresql drivers, and addressbook application configured to connect to postgresql.

These playbooks will install a single postgresql instance on a dedicated server, and will deploy multiple Wildfly instances on individual servers.  These Jboss EAP instances will be configured to connect to the postgresql instance.  
## Prerequisites
2 or more RHEL 8.4+ vms with 4096mb per vm.


## Set up

The following sections describe the steps necessary to prepare your machine for execution

### JCliff Integration

First of all, you'll need to install the [JCliff Ansible collection](https://github.com/middleware_automation/ansible_collections_jcliff):

    $ ansible-galaxy collection install -r molecule/default/requirements.yml

### Ansible Inventory

Ansible groups are used to define the Wildfly instances. Configure these groups in the [hosts](inventory/hosts) file similar to the following:

```
# Placeholder Group
[demo]

# Wildfly Group
[wildfly]
192.168.122.11
192.168.122.125

# postgresql database Group
[postgresql]
192.168.122.84

# jbbs Group
[jbcs]
192.168.122.85

[demo:children]
wildfly
postgresql
jbcs
```

## Execution
You will need a valid Red Hat login in order to download JBoss EAP.   
You can now run the playbook to set up the demo, inserting your RH login details to the command.


    $ ansible-playbook -i inventory/hosts demo.yml --extra-vars "rhn_username=<your_username> rhn_password=<your_password>"
