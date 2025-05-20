---
title: "Openstack - Deploying a Virtual Machine with a spark data platform"
date: 2025-04-30
---

Our objective here is to deploy an instance (virtual machine) and to be able to ssh into this machine. Spoiler: deploying an instance is straight forward. Being able to ssh into this instance and giving this instance the ability to connect to external networks is a little more challenging. You will still be able to explore the functionality of Openstack without this, so if you can't achieve this don't worry. I will be writing future blog posts with a full throated Openstack installation where we will be addressing the specifics of setting up all required networking.

# Use the demo project
For your first deployment of a Virtual Machine and to test the functionality of Openstack, make use of the demo project as it already has preconfigured networks and routing.

## Set up the networking to allow ssh, ping and http access 

First you will need to generate an ssh key for the account you will be using to ssh into the instance.
``` bash
ssh-keygen
```
press return when asked when questions about the filename and password for the public/private rsa keypair.

You can do all the below from within the horizon web dashboard, however to do it from the command line, which is more exact, replicable and faster, you need to ensure you have authenhticated.
- Download the Openstack RC file (menu in the top left corner of the horizon dashboard), and then run (assume you are working in the demo project.
``` bash
source demo-openrc.sh
```

Open up required ports in the security group

``` bash
openstack security group rule create --proto icmp --dst-port 0 default
openstack security group rule create --proto tcp --dst-port 22 default
```

You may need to change the name of the default security group to use its id. Find this by running openstack security group list

Create a keypair in your Openstack project

``` bash
openstack keypair create --public-key ~/.ssh/id_rsa.pub test-keypair
```

Create an instance, to validate our Openstack is working and our networking is set up correctly we will use the minimal VM image that comes with Devstack

``` bash
openstack server create --network private --key-name test-keypair --image cirros-0.6.3-x86_64-disk --security-group default --flavor cirros256 test-server
```

You will likely have to replace the name default of the security group with the id owing to the fact that there will be more than one security group called default across different projects. To get this information:

``` bash
openstack project list # to get the id of the demo project to determine which default security group we should take the id for
openstack security group list # to get the id of the group to use in place of the name default
```

Validate the image names and flavor that will use in the "openstack server create" command 
``` bash
openstack image list
openstack flavor list
```

Check that your instance has been created and that it's status is RUNNING, you may have to wait a few minutes for it to build, as you are probably running this inside a VM inside a laptop (for maximum abstraction!). 

``` bash
openstack server list
```

Once your server is built create a floating IP, associate it with the instance we have created in the public network

``` bash
fip_id=$(openstack floating ip create public -f value -c id)
openstack server add floating ip test-server ${fip_id}
```

Now attempt to ssh into your instance

``` shell
openstack server ssh test-server -- -l cirros
```

Userful reference documents.
https://docs.openstack.org/devstack/latest/networking.html
https://static.opendev.org/docs/devstack/ocata/guides/single-machine.html


