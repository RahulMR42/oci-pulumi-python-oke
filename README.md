OCI Pulmi OKE - With Python.
------

These is a OCI Pulumi python code  that deploys [Container Engine for Kubernetes (OKE)](https://docs.oracle.com/en-us/iaas/Content/ContEng/home.htm) on [Oracle Cloud Infrastructure (OCI)](https://cloud.oracle.com/en_US/cloud-infrastructure).

## About
Oracle Cloud Infrastructure Container Engine for Kubernetes is a fully-managed, scalable, and highly available service that you can use to deploy your containerized applications to the cloud. Use Container Engine for Kubernetes (sometimes abbreviated to just OKE) when your development team wants to reliably build, deploy, and manage cloud-native applications.

## Prerequisites 
1. Download and install Pulumi CLI - https://www.pulumi.com/docs/get-started/install/
2. Download and install Python3 (3.6 or later) - https://www.python.org/downloads/ 
3. Oracle credentilas for Pulumi - https://www.pulumi.com/registry/packages/oci/installation-configuration/ 

## Optional Prerequisites 

- You can manage pulumi stack with stage managed by pulumi itself ,to do so create an account on Pulumi via - https://app.pulumi.com/ 
- In the below procedure we will be explaining with steps where state is manged by Pulumi or with a local file .

## How to deploy 

Validate installed softwares

---

- Validate the execution Pulumi CLI - `pulumi version`
- Validate the python3 execution - `python -V`
- Create a new pulumi stack - `pulumi new `

![](images/pul)


