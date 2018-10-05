# Ansible : Playbook GlusterFS

The aim of this project is to deploy a simple Gluster cluster on Vagrant with some default value.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to run this Ansible playbook :

*   [Vagrant](https://www.vagrantup.com/docs/installation/) must be installed on your computer
*   Update the Vagrant file based on your computer (CPU, memory), if needed
*   You must have download the ubuntu Xenial64 vagrant box :

```bash
$ vagrant box add https://app.vagrantup.com/ubuntu/boxes/xenial64
```

### Usage

A good point with Vagrant is that you can create, update and destroy all architecture easily with some commands.

Be aware that you need to be in the Vagrant directory to be able to run the commands.

#### Build Environment

Vagrant needs to init the project to run and build it :

```bash
$ vagrant up
```

After build, you can check which virtual machine Vagrant has created :

```bash
$ vagrant status
```

If all run like it is expected, you should see something like this :

```bash
$ vagrant status

Current machine states:

gfsserver01                  running (virtualbox)
gfsserver02                  running (virtualbox)
gfsclient01                  running (virtualbox)
```

#### Deployment

To deploy the Gluster cluster, you just have to run the Ansible playbook glusterfs.yml with this command :

```bash
$ ansible-playbook glusterfs.yml
```

If everything run as expected, you should connect on any server node and get the shared volume informations with this command :

```bash
$ sudo gluster volume info

Volume Name: data1
Type: Replicate
Volume ID: 090406b3-b684-4cf8-aa3b-f488ee0d7510
Status: Started
Number of Bricks: 1 x 2 = 2
Transport-type: tcp
Bricks:
Brick1: 10.0.3.61:/opt/glusterfs/data1
Brick2: 10.0.3.62:/opt/glusterfs/data1
Options Reconfigured:
performance.readdir-ahead: on

Volume Name: data2
Type: Replicate
Volume ID: 89515bf4-6f0d-4c87-a500-198cfca445ea
Status: Started
Number of Bricks: 1 x 2 = 2
Transport-type: tcp
Bricks:
Brick1: 10.0.3.61:/opt/glusterfs/data2
Brick2: 10.0.3.62:/opt/glusterfs/data2
Options Reconfigured:
performance.readdir-ahead: on

```

On the client node, you can create any file or directory in any mount volume (/mnt/dataX) by gluster and see the replication on the two server nodes.

#### Destroy

To destroy the Vagrant resources created, just run this command :

```bash
$ vagrant destroy
```

## Author

Member of Wikitops : https://www.wikitops.io/

## Licence

This project is licensed under the Apache License, Version 2.0. For the full text of the license, see the LICENSE file.
