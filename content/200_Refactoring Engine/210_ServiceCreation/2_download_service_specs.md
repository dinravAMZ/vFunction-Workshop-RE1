---
title: "Download service specs"
chapter: true
weight: 2
---

![vFunction Logo](/images/vFunction.png)

### Download the service specification files

1. Open the Chrome web browser and go to the vFunction WebUI Analysis page. Select **"Baseline 1"** measurement (specified in the AO Tutorial)

2. Mark InventoryController, OrderController and ProductController for extraction in the ANALYSIS page by going through each one, clicking the menu near the number next to the name (3 dots) and selecting SAVE. A tick-mark on the sphere indicates it is marked for extraction. Note that the common library is marked for extraction too.

    | ![Marking a service for extraction](/images/Marking-for-extraction.png) |
    | :--: |
    | Marking a service for extraction |


    | ![Marked for extraction](/images/Marked4Extraction.png) |
    | :--: |
    | Services marked for extraction |


3. Switch to the SERVICE CREATION page, press CONFIGURE and set it up as shown here:

    | ![Service Config](/images/Service-Config1.png) |
    | :--: |
    | Service Config Dialog for Service Creation |

    The Group ID is the group ID that will be set for the services. The Target Platform is what platform should the services be configured for and the Dependency Repository type is the **current** repository type **used for building the application**


4. Close the Service Configuration dialog and download all service specifications to *C:\vFunctionLab\service-specs* files by clicking DOWNLOAD. Then, download the code-copy tool to the same folder as the specification files (click on the link in the *Extract your first service* dialog)

5. Download the legacy code-copy utility (as we are using an old java version) from '''http://[vfunctionserver]/downloads/vfunction-tools/windows/code-copy.exe''' (replace with vFunction server IP) and download to the same folder as the specification files.

{{% notice note %}}
The browser might be configured not to prompt for a folder when downloading files. In that case, locate the destination folder by doing "Show in Folder" on one of the downloaded files and then copy the files to *C:\vFunctionLab\service-specs*. Note that code-copy.exe should also be in the same folder as the .json files.
</p>
{{% /notice %}}

![vFunction Logo](/images/vFunction.png)
