---
title: "Deployment"
chapter: true
weight: 220
---
![vFunction Logo](/images/vFunction.png)


# Deployment using vFunction Deployment Tool

This section is an optional/advanced section intended for people with DevOps experience. 

Also, you should skip ths section if you haven't set **use_refactoring** to true in [Setup Environment](/10_setup.html) section.

After having working services, you can optionally deploy them to a micro-services environment such as a Kubernetes cluster or cloud service.

vFunction has an experimental tool to automate such a deployment.

### Steps

1. Connect to the *workshop-linux* VM (via PuTTY)

2. cd to deployment tool folder 

    ```bash
    cd /opt/vfunction-packages/vfunction-refactoring-for-kubernetes
    ```

3. Review the configuration file

    ```bash 
    less config/installation.yaml
    ```

    During the environment setup, the terraform has already configured the necessary settings such as the repo URL, username, password, nginx.

    The services and the properties are also already configured under services:springBoot:services

4. Exit the configuration file (installation.yaml) and create the following folders (the names must match the names of the services in installation.yaml and in general, they must be all small letters with hyphens)

    ``` bash
        cd services
        mkdir product-controller
        mkdir inventory-controller
        mkdir order-controller
    ```

5. Open Git Bash window

6. Go to the services folder

    ```bash 
    cd /c/vFunctionLab/oms-services
    ```

7. Set an environment variable for the IP address of the *workshop-linux* machine

    ``` bash
    LINUXVMIP=[the IP address of workshop Linux VM]
    ```

8. Copy order-controller

    ```bash
    scp ./order-controller/target/OrderController-1.0-SNAPSHOT.jar workshop@$LINUXVMIP:/opt/vfunction-packages/vfunction-refactoring-for-kubernetes/services/order-controller
    ```

    Enter the password (vFunction2021!) when prompted

    Note: If scp fails because the remote certification has changed, then delete c:\Users\workshop\.ssh (the entire folder) and try again

8. Similarly copy inventory controller

    ```bash
    scp ./inventory-controller/target/InventoryController-1.0-SNAPSHOT.jar workshop@$LINUXVMIP:/opt/vfunction-packages/vfunction-refactoring-for-kubernetes/services/inventory-controller
    ```

    And product controller:
    ```bash
    scp ./product-controller/target/ProductController-1.0-SNAPSHOT.jar workshop@$LINUXVMIP:/opt/vfunction-packages/vfunction-refactoring-for-kubernetes/services/product-controller 
    ```

9. Go back to the *workshop-linux* VM (PuTTY) and do ```cd /opt/vfunction-packages/vfunction-refactoring-for-kubernetes```

10. Since the ECR password is valid only for 24 hours, refresh it in the configuration by running:

    ```bash
    bash ./aws-refresh-ecr-token.sh

    ```

11. Run the installer 

   ```bash
   sudo bash install.sh -n vfunction -b
   ```

    The last output messages of the script should look *similar* to:

    ```text
    Wait for all service pods to run in namespace vfunction and then access the services with the following FQDNs:
        product-controller -> a2ac33ccf24a245bd9891679063fd3a5-840504988.us-west-2.elb.amazonaws.com/product-controller/
        inventory-controller -> a2ac33ccf24a245bd9891679063fd3a5-840504988.us-west-2.elb.amazonaws.com/inventory-controller/
        order-controller -> a2ac33ccf24a245bd9891679063fd3a5-840504988.us-west-2.elb.amazonaws.com/order-controller/
    ```

    Copy the FQDN somewhere for later use (e.g., copy them to a notepad)

12. Go to the AWS console and open the EKS service (in the same region as the EC2 instances) with the name starting with workshop_eks and review the workloads. You should see three workloads corresponding to the three services with namespace vfunction and they should be in the Ready state.

    ![EKS Deployed Services](/images/EKS-Deployed-Services.png)
You can also review the ECR and see three repositories corresponding to the three services.

13. Open postman and test the calls to the various services by replacing the hostname from localhost:8080 with the corresponding FQDNs above. Below is an example screenshot (note the URL):

    ![Postman Deployed](/images/Postman-KubDeployed-AWS.png)

    *Note: Some API calls of the product controller return internal server error (500). Can you think why and how to fix it? (hint: service to service dependency)*

14. Now that we have three services deployed to EKS, we can use [AWS Migration Hub Refactor Spaces](https://aws.amazon.com/migration-hub/features/#Incremental_app_refactoring) to redirect calls from the OMS original application to the services. If you are interested in trying this out, do <a href="/70_awsrefactorspaces/_index.aws.html">this Appendix</a> before proceeding to Cleanup.

![vFunction Logo](/images/vFunction.png)
