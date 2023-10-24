---
title: "RE Tutorial"
chapter: true
weight: 100
---

![vFunction Logo](/images/vFunction.png)

# Refactoring Engine (RE) Tutorial

{{% notice note %}}
Please complete the [Setup Environment](/10_setup.html) section before starting the tutorial
and don't forget to [Cleanup](/300_cleanup.html) when you're done with the workshop
{{% /notice %}}

This is a hands-on tutorial for the vFunction Refacotring Engine (RE) module.

We will use the Order Management System (OMS) demo application with the measurement done in the AO Tutorial to show how to create services from domain specifications defined in the AO module.

**We assume this tutorial is done after completing the AO Tutorial**

If you have not completed the AO Tutorial Import the completed measurment first.

### Learning Objectives

- How to use vFunction RE to create services corresponding to the domains identified in vFunction AO
- What manual efforts are involved in the service process
- Understand some of the best practices


### Workshop Flow

The following flowchart describes the tutorial steps and artifacts of this tutorial. 

The rounded rectangles represent steps you'll perform (with time estimation), the parallelograms represent artifatcs / results (some can be downloaded) and the trapezoid represent an event.

{{<mermaid align="center">}}
graph TD;
    BaseLineMeasurement[/" Baseline Measurement"/]-->ServiceCreation(["Service Creation: Create the independently deployable services (100 min.)"])
    ServiceCreation --> Services[/"Services (click to see in Git)"/]
    Services --> Deployment(["Deployment: Deploy the services to EKS (20 min.)"])
    Deployment --> KubeServices("Services Deployed in EKS")

    click Setup "./10_setup/_index.aws.html"
    click Learning "./20_learning.html"
    click Analysis "./30_analysis.html"
    click ServiceCreation "./40_servicecreation.html"
    click Deployment "./50_deployment/_index.aws.html"
    click Cleanup "./60_cleanup/_index.aws.html"

    click OMSApp "https://bitbucket.org/vfunction/oms-tutorial/src/mysql/oms-webmvc/" _blank
    click Measurement "https://portal.vfunction.com/file/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1dWlkIjoiNWNhYmNjYTMtNTc5MC00MmY1LWE0ODgtM2RhODZmOGVjYzlmIn0.C--1C7PmFRGUxWxDe-hOtaA9PvmV8NiLLbHrmXmYEr0/5cabcca3-5790-42f5-a488-3da86f8ecc9f/Analysis-Tutorial-Start.zip"
    click ServiceSpecs "https://bitbucket.org/vfunction/oms-tutorial/src/mysql/oms-services/service-specs/" _blank
    click Services "https://bitbucket.org/vfunction/oms-tutorial/src/mysql/oms-services/" _blank
{{< /mermaid >}}

![vFunction Logo](/images/vFunction.png)


