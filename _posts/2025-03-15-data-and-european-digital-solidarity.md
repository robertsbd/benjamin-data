---
title: "UK & European Digital solidarity - OpenStack and Data Platforms - Installing OpenStack "
date: 2025-03-15
---

Digital sovereignty is increasingly becoming a critical geopolitical imperative, especially for the UK and Europe. Ensuring control over our digital infrastructure is essential for maintaining autonomy and security. One way to achieve this is by leveraging open-source technologies. In the upcoming series of Blog posts I wish to explore the deployment of OpenStack to provide open source cloud computing, and the the use of free and open-sourced tooling with which to build a modern robust cloud data platform.

In the first blog post I will be providing a step-by-step guide to deploying a virtual machine and running OpenStack on this Virtual Machine.

OpenStack is an open-source cloud computing platform primarily used for creating and managing large groups of virtual private servers in a data center. It is designed to provide infrastructure as a service (IaaS) and is widely adopted by organizations seeking to build scalable and flexible cloud environments. OpenStack is a key piece of technology with which an organisation can build out and manage their own cloud services.

# Objective
My overall-goal is to build a data platform using open-source technologies on an open sourced cloud environment. The stack will include:

- **Apache Spark + Delta:** For data storage and processing
- **Apache Airflow:** For orchestration
- **Neo4j Graph Database:** For data modeling and data lineage visualisation
- **PostgreSQL:** For SQL storage
- **Locally Hosted Large Language Models (LLMs):** To integrate these components

# Digital Sovereignty in Practice
Digital sovereignty means having control over your data and the infrastructure that processes it. By using open-source tools, we can ensure that our data platform is transparent, secure, and free from vendor lock-in. Tools like Databricks and Fabric, while highly marketed, are essentially wrappers around existing open-source software. This series will demonstrate how to achieve similar capabilities with open-source alternatives.

## Deploying OpenStack
OpenStack is a powerful open-source cloud platform that allows you to manage large pools of compute, storage, and networking resources. I will be using DevStack, a script-based tool designed to quickly deploy OpenStack on a single machine, to set up my environment.

To find out instructions to use DevStack to install OpenStack visit the following page: [OpenStack](https://docs.openstack.org/devstack/latest/)

### System Specifications

- **CPU:** Ryzen 7 AMD
- **RAM:** 64 GB
- **GPU:** Integrated
- **OS:** Fedora (GNU/Linux distribution)

## Creating a Linux VM for OpenStack

The first step is to create a virtual machine (VM) to install DevStack. Here are the specifications for the VM:

- **CPU Cores:** 8
- **RAM:** 32 GB
- **Disk Storage:** 120 GB
- **OS:** Ubuntu Desktop 22.04 LTS (Jammy Jellyfish)

I used Boxes, a VM management tool that comes with Gnome in Fedora, to create the VM. The process was straightforward and followed the recommendations in the DevStack documentation.

## Deploying OpenStack on the VM

Initially, I attempted to deploy OpenStack directly on the VM, but the process failed midway due to issues with deploying Kubernetes controllers. I suspected that the VM was underpowered, so I repeated the process on a spare laptop with the required CPU cores but only 8 GB of RAM. This attempt also failed.

## Success with DevStack

DevStack provides a streamlined way to set up an OpenStack environment quickly. However, I encountered several issues related to network stability and the cloning of large Git repositories. To resolve these, I ran the following commands to configure Git for better stability:

```bash
git config --global http.postBuffer 104857600
git config --global http.version HTTP/1.1
git config --global core.compression 0
```

With these adjustments, I successfully installed OpenStack and accessed the Horizon dashboard, which is equivalent to the Azure portal or AWS Console.

Here is a picture of the Horizon dashboard.

![OpenStack Horizon dashboard](/benjamin-data/docs/assets/images/horizon.png)
 
# Next Steps
The next phase will involve deploying networking, virtual machines, and the data platform on OpenStack. Stay tuned for more updates as I continue this journey towards digital sovereignty.

