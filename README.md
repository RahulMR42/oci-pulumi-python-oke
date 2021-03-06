OCI Pulmi OKE - With Python.
------

These is a OCI Pulumi python code  that deploys [Container Engine for Kubernetes (OKE)](https://docs.oracle.com/en-us/iaas/Content/ContEng/home.htm) on [Oracle Cloud Infrastructure (OCI)](https://cloud.oracle.com/en_US/cloud-infrastructure).

## About
Oracle Cloud Infrastructure Container Engine for Kubernetes is a fully-managed, scalable, and highly available service that you can use to deploy your containerized applications to the cloud. Use Container Engine for Kubernetes (sometimes abbreviated to just OKE) when your development team wants to reliably build, deploy, and manage cloud-native applications.

## Prerequisites 
1. Download and install Pulumi CLI - https://www.pulumi.com/docs/get-started/install/
2. You may use OCI cloud shell to install the Pulumi software as well.
```markdown : 
user@cloudshell$ curl -fsSL https://get.pulumi.com | sh
user@cloudshell$ bash
user@cloudshell$ pulumi version 
```
3. If not installed ,download and install Python3 (3.7 or later) - https://www.python.org/downloads/ 
4. Oracle credentilas for Pulumi - https://www.pulumi.com/registry/packages/oci/installation-configuration/ 

## Optional Prerequisites 

- You can manage pulumi stack with stage-managed by pulumi itself ,to do so create an account on Pulumi via - https://app.pulumi.com/ 
- In the below procedure we will be explaining with steps where state is manged by Pulumi or with a local file .

## How to deploy

- Validate the execution Pulumi CLI - `pulumi version`
- Validate the python3 execution - `python -V`
- Create a folder for the code and switch in to it.
```markdown
$ mkdir oci-pulumi-oke
$ cd oci-pulumi-oke
```
- Login to pulumi 
  - If you wish to have the infra states  managed by Pulumi use `pulumi login` and follow the instruction.
  - If you are using OCI Cloud shell ,create a user access token via app.pulumi.com and use it when prompted

![](images/personal_access_token.png)
```markdown
user@cloudshell$pulumi login
user@cloudshell$ Enter your access token from https://app.pulumi.com/account/tokens : XXXXX
```

  - If you wish to manage the states locally follow below 
```markdown

$ mkdir pulumi-state-local
$ pulumi login file://pulumi-state-local
```

![](images/pulumi_local.png)

- Create a new pulumi stack - `pulumi new https://github.com/RahulMR42/oci-pulumi-python-oke ` --force 
- Do not need to use `--force ` for login with Pulumi managed infra state mode.

![](images/pulumi_new_with_url.png)

- When prompted user `pulumi-oci-python-oke` as project name and use the default description.
- Provide the stack name as `pulumi-oci-python-oke`
- You may enter or keep an empty passphrase when asked for the config.
![](images/pulumi_new_final.png)

- You may also refer the files using `ls -ltr` commands.

![](images/pulumi_files.png)

- Let preview the stack using `pulumi preview`.
- It will list all the components to create but with  debug errors ,as expected.
![](images/pulumi_create_progress.png)

- Debug errors are due to the fact the OCI credentials are not yet setup.
- Set below   the environment variables Or with Secret configs - https://www.pulumi.com/registry/packages/oci/installation-configuration/ 

- As ENV values .
- 
```markdown
export TF_VAR_tenancy_ocid="ocid1.tenancy.oc1..<unique_ID>"
export TF_VAR_user_ocid="ocid1.user.oc1..<unique_ID>"
export TF_VAR_fingerprint="<key_fingerprint>"
export TF_VAR_region="us-ashburn-1"
export TF_VAR_private_key_file="/path/to/oci_api_key.pem"
```

- As an encrypted secrets (With in pumi config control/Not with OCI Vault)

```markdown
pulumi config set oci:tenancyOcid "ocid1.tenancy.oc1..<unique_ID>" --secret
pulumi config set oci:userOcid "ocid1.user.oc1..<unique_ID>" --secret
pulumi config set oci:fingerprint "<key_fingerprint>" --secret
pulumi config set oci:region "us-ashburn-1"
# Set the private key from standard input to retain the format
cat "PATH TO PEMFILE " | pulumi config set oci:privateKey --secret
```

- Set compartment_ocid as a config values.
```markdown
pulumi config set compartment_ocid "OCID of your compartment"
```
- You may verify the values of your stack using file `Pulumi.pulumi-oci-python-oke.yaml`
![](images/pulumi_config_yaml.png)
- Re run preview and validate the configuration `pulumi preview`

![](images/pulumi_preview.png)

- Create the infra using `pulumi up` ,use the arrow key and provide the confirmation.

![](images/pulumi_up_confirmation.png)

- You may see the infra is getting created.

![](images/pulumi_confirmation_yes.png)

- The OKE Cluster creation will take some minutes to complete .

![](images/pulumi_completed.png)

- Once completed ,validate the resources /access the OKE Cluster resource via OCI console

- Delete the stack using `pulumi destroy `

![](images/pulumi_destroy.png)

- Delete stack files - `pulumi stack rm pulumi-oci-python-oke`

![](images/pulumi_stack_rm.png)

- Logout from pulumi `pulumi logout`

## Read more 

- https://www.pulumi.com/registry/packages/oci/installation-configuration/ 

## Contributors
Author : Rahul M R.
Collaborators : NA
Last release : May 2022








