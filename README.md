# Two-zone Virtual Private Cloud

With this template, you can use IBM Cloud Schematics to create two virtual private clouds (VPCs) in two separate zones of your IBM Cloud account. Schematics uses [Terraform](https://www.terraform.io/) as the infrastructure-as-code engine. With this template, you can create and manage infrastructure as a single unit as follows. For more information about how to use this template, see the [IBM Cloud Schematics documentation](https://cloud.ibm.com/docs/schematics).

**Included**:
* 2 [virtual private cloud](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-getting-started) instances, in separate zones.
* 1 [VPC virtual servers](https://cloud.ibm.com/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-getting-started) instances per zone. The virtual servers include an NGINX load balancer.

**Not included**:
* No VPC load balancers are created to expose workloads in the virtual servers on the public network.
* No global load balancer is provisioned to manage traffic across the 2 VPC instances.

## Costs

When you apply template, the infrastructure resources that you create incur charges as follows. To clean up the resources, you can [delete your Schematics workspace or your instance](https://cloud.ibm.com/docs/schematics?topic=schematics-manage-lifecycle#destroy-resources). Removing the workspace or the instance cannot be undone. Make sure that you back up any data that you must keep before you start the deletion process.

* **VPC**: VPC charges are incurred for the infrastructure resources within the VPC, as well as network traffic for internet data transfer. For more information, see [Pricing for VPC](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-pricing-for-vpc).
* **VPC virtual servers**: You specify how many virtual servers to provision in each VPC. The price for your virtual server instances depends on the flavor of the instances, how many you provision, and how long the instances are run. For more information, see [Pricing for Virtual Servers for VPC](https://cloud.ibm.com/docs/infrastructure/vpc-on-classic?topic=vpc-on-classic-pricing-for-vpc#pricing-for-virtual-servers-for-vpc).

## Dependencies

Before you can apply the template in IBM Cloud, complete the following steps.

1.  Make sure that you have the following permissions in IBM Cloud Identity and Access Management:
    * **Manager** service access role for IBM Cloud Schematics
    * **Operator** platform role for VPC Infrastructure
2.  Download the [`ibmcloud` command line interface (CLI) tool](https://cloud.ibm.com/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli).
3.  Install the `ibmcloud terraform` and `ibmcloud is` CLI plug-ins for Schematics and VPC infrastructure. **Tip**: To update your current plug-ins, run `ibmcloud plugin update`.
    *  `ibmcloud plugin install schematics`
    *  `ibmcloud plugin install vpc-infrastructure`
4.  [Create or use an existing SSH key for VPC virtual servers](https://cloud.ibm.com/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-ssh-keys).

## Terraform version requirements :  

Refer [versions.tf](versions.tf)

|  **Name**                  | **Version** |
|  --------------------------| -------------|
|  terraform                 | >= 1.0 |
|  terraform_provider_ibm    | = 1.38.0 |


## Configuring your deployment values

When you select the [`2-zone-vpc`template](https://cloud.ibm.com/catalog/content/2-zone-vpc) from the IBM Cloud catalog, you set up your deployment variables from the **Create** page. When you apply the template, IBM Cloud Schematics provisions the resources according to the values that you specify for these variables.

### Required values
Fill in the following values, based on the steps that you completed before you began.

|Variable Name|Description|
|-------------|-----------|
|`ssh_public_key`|Enter the [public SSH key](https://cloud.ibm.com/docs/vpc?topic=vpc-ssh-keys#locating-ssh-keys) that you use to access your VPC virtual servers. Use the public key from the `~/.ssh/id_rsa.pub` file generated by the latest version of ssh-keygen tool, with the recommended key-size 2048.|

### Optional values
Before you apply your template, you can customize the following default variable values.

|Variable Name|Description|Default Value|
|-------------|-----------|-------------|
|`region`|The region to create your two VPCs in, such as `us-south`. The VPCs are created in two separate zones within the same region. To get a list of all regions, run `ibmcloud is regions`.|`us-south`|
|`ssh_key_name`|The name of your public SSH key.|`vpc-ssh-key`|
|`image`|Enter the ID of the image that represents the operating system that you want to install on your VPC virtual server. To list available images, run `ibmcloud is images`. The default image is for an `ubuntu-20-04-amd64` OS.|`r006-396ef8b6-91a3-48ce-a83b-0c6f67105cad`|
|`profile`|Enter the profile of compute CPU and memory resources that you want your VPC virtual servers to have. To list available profiles, run `ibmcloud is instance-profiles`.|`bx2-2x8`|


## Outputs
After you apply the template your VPC resources are successfully provisioned in IBM Cloud, you can review information such as the virtual server IP addresses and VPC identifiers in the Schematics log files, in the `Terraform SHOW` section.
