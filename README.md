# OpenShift Vagrant

## Overview

The `OpenShift Vagrant` project aims to make it easy to bring up a real OpenShift Origin cluster by providing pre-configured `Vagrantfile` of several major versions of Origin.

## Prerequisite

- Oracle VirtualBox
- Vagrant (2.0 or above)

## OpenShift Origin Version Support

Currently this project pre-configured and support 3 major versions of the OpenShift Origin, which are

- [OpenShift Origin release v3.6.0](https://github.com/openshift/origin/releases/tag/v3.6.0)
- [OpenShift Origin release v3.6.1](https://github.com/openshift/origin/releases/tag/v3.6.1)
- [OpenShift Origin release v3.7.0](https://github.com/openshift/origin/releases/tag/v3.7.0)

But, it's very easy to customize the respected ansible hosts file in order to supprot other incoming major versions.

The `Vagrantfile` uses Origin `v3.6.1` and openshift-ansible `release-3.6` branch by default. Feel free to adjust your versions by updating the following 2 variables in Vagrantfile:

1. `OPENSHIFT_VERSION`
2. `OPENSHIFT_ANSIBLE_BRANCH`

The following table lists the corresponding version relationships between Origin and openshift-ansible:

| OpenShift Origin version | openshift-ansible version |
| --- | --- |
| v3.6.0 | release-3.6 |
| v3.6.1 | release-3.6 |
| v3.7.0 | release-3.7 |


## Getting Started

After adjusting your expected version information, now it's time to bring your cluster up and running. This Vagrantfile will create 3 VMs in VirtualBox listed below:

| VM Node | Private IP | Roles |
| --- | --- | --- |
| master | 192.168.101.101 | master, etcd |
| node01 | 192.168.101.102 | node, lb |
| node02 | 192.168.101.103 | node |

### Bring Vagrant Up

```bash
$ vagrant up
```

### Copy Private Keys

```bash
$ vagrant provision --provision-with master-key,node01-key,node02-key
```

### Install Origin Using Ansible

```bash
$ vagrant ssh master
$ # The following command will be executed within master VM
$ ansible-playbook /home/vagrant/openshift-ansible/playbooks/byo/config.yml
```

### Open Web Console

In browser of your host, open the following page: https://master.example.com:8443/ and you should see OpenShift Web Console login page.

*Have fun with OpenShift Origin and Vagrant :p*