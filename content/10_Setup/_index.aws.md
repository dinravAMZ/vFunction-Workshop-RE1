---
title: "Setup Environment"
chapter: true
weight: 10
---

![vFunction Logo](/images/vFunction.png)

# Setup AWS workshop environment

In this section, you will create and deploy the necessary AWS services required for this workshop by running a Terraform
package.

The below diagram depicts the AWS services provisioned the workshop installation package and their usage (the xxx in the names represent a variable string):
vFunction-Workshop-RE1
![Workshop Environment](/images/Workshop-Environment-AWS-TF.png)


### Run the installation package to deploy the Workshop resources

1. Log in to your AWS Account

2. Open the AWS CloudShell (icon is on top right toolbar)

3. Download the workshop installation package from the vFunction portal using the command:

```bash
curl -o vfunction-workshop-aws-installation.tgz https://portal.vfunction.com/file/2265236af5b0e6563c813dd3756e4ce8/02a4ee02-c7cf-4b21-a560-48f428b1a521/vfunction-workshop-aws-installation.tgz
```

4. Unpack the installation package

```bash
tar zxvf vfunction-workshop-aws-installation.tgz
```

{{% notice tip %}}
<p style='text-align: left;'>

If deploying the workshop into a corporate account with security policies restricting ingress access, you can remove the auto created ingress rules from the terraform template. Remember to add your own rules to RDP to the Windows EC2 instance.
</p>
{{% /notice %}}

Optional remove ingress secuirty groups:
``` 
vi vfunction-workshop/terraform/aws/module.tf
```

Optional remove:

``` XML
ingress_with_cidr_blocks = [
    {
        from_port   = 8080
        to_port     = 8080
        protocol    = "tcp"
        cidr_blocks = "0.0.0.0/0"
    },
    {
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = "0.0.0.0/0"
    }
]

ingress_with_cidr_blocks = [
    {
        from_port   = 3389
        to_port     = 3389
        protocol    = "tcp"
        cidr_blocks = "0.0.0.0/0"
    },
    {
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = "0.0.0.0/0"
    }
]
```




5. Edit the file ./config/installation.yaml file:

```bash
vim ~/vfunction-workshop/config/installation.yaml
```

   1. Set the region to which the resources will be deployed- you can use any US region, however, if you want to do the [Appendix for using AWS Migration Hub Refactor Spaces](/500_awsrefactorspaces.html), make sure that this service is available in the region you choose by searching Refactor Spaces in this region.
   
   2. Fill in your org_name (must be shorter than 50 chars) and email (e.g., "my company" as org_name and "myname@company.net" as email)

   3. If you intend to deploy services to EKS, Set use_refactoring to true, otherwise set it to false


1. Run the installation and wait for the script to complete


   ```bash
   bash ~/vfunction-workshop/install.sh
   ```

### Setup Remote Desktop to Workshop Windows VM

1. Switch to the EC2 Instances page in the region you set to deploy the workshop

2. Open the EC2 instance with the name starting with workshop-windows (should be in running state) and copy its public IPv4 Address

3. Open your Remote Desktop Protocol (RDP) client and paste the IP as the Host Name or Address

4. Start the RDP session. The user name is ```workshop``` the password is ```vFunction2021!```

5. If prompted, approve the certificate to access the remote machine

6. You should now see the Windows Desktop running on the Dev VM.

### Access the Workshop Linux VM

1. Copy the private IP address of the Workshop-Linux VM from the AWS console

2. In the Windows VM (Remote Desktop), run PuTTY (icon is on the desktop)

3. In the PuTTY dialog, enter the *private* IP address of the Linux VM and click Open

4. Login using the same credentials (login: ```workshop``` password:```vFunction2021!```)

### Login to the vFunction server

The vFunction platform installation was automated by the Workshop Installation package.

To login to the platform:

1. Open Chrome in the Windows VM (Remote Desktop)

2. Type the IP Address of the Linux VM

3. Login with the e-mail you entered in the installation.yaml file. The password is ```vFunction2021!```
   
   You should see a screen similar to:

   ![vFunction Server](/images/vFunctionServer.png)

You are now ready to proceed to the workshop.

![vFunction Logo](/images/vFunction.png)
