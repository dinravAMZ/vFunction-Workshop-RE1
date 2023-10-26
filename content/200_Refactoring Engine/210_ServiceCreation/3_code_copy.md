---
title: "Code extraction"
chapter: true
weight: 3
---

![vFunction Logo](/images/vFunction.png)

### Compile the original OMS application

The code-copy application relies on the local maven repo to generate the required maven / gradle dependencies. To ensure the local repo is updated, compile the original application so the necessary used libraries will be downloaded from maven central.

1. Open a command prompt and cd to ```c:\vFunctionLab\oms-tutorial```

2. Checkout the mysql branch

```
git checkout mysql
```

Note: If the git is not connected, rename the oms-tutorial folder and clone the public repository ```git clone https://ws@bitbucket.org/vfunction/oms-tutorial.git``` and then checkout mysql branch

3. Pull the latest version from the public git repository:

```
git pull
```

4. Go to the application folder

```
cd oms-webmvc
```

5. Compile using maven: 
```
mvn clean install
```

### Extracting baseline code using code-copy

You will now use the code-copy application, downloaded with the specification files, to create the baseline code for the extracted services. 

1. Open a command prompt and cd to c:\vFunctionLab\service-specs

2. Optionally run code-copy -help to see the various arguments and their meaning

3. Run the following commands:

    ``` text
    code-copy -spec CommonLibrary.json -source ..\oms-tutorial\oms-webmvc -dest ..\oms-services\common
    ```

    ``` text
    code-copy -spec OrderController.json -source ..\oms-tutorial\oms-webmvc -dest ..\oms-services\order-controller
    ```

    ``` text
    code-copy -spec InventoryController.json -source ..\oms-tutorial\oms-webmvc -dest ..\oms-services\inventory-controller
    ```

    ``` text
    code-copy -spec ProductController.json -source ..\oms-tutorial\oms-webmvc -dest ..\oms-services\product-controller
    ```

### Run Spotless to cleanup the code

vFunction v2.8 and above includes the [spotless plugin](https://github.com/diffplug/spotless) in the build files by default. This plugin removes redundant imports as well as formats the source code.

Run the following command in each of the services folders (i.e., subfolders of c:\vFunctionLab\oms-services)

```cmd
mvn spotless:apply
```

Note: if you don't want to use spotless, you can remove the spotless plugin from the build files (pom.xml and build.gradle) or add ```-DskipSpotless``` when compiling the services

### Import the services to Eclipse

1. Validate your Eclipse settings:

    a. Run Eclipse and select C:\vFunctionLab\workspace as the workspace

    ![Select-Workspace](/images/Selecting-Workspace.png)

    b. Open the Eclipse Preferences dialog (Windows -> Preferences)

    c. Select Java->Compiler and set the Compiler compliance level to 1.8

    ![Eclipse-Compiler](/images/Eclipse-Compiler.png)

    d. Add OpenJDK to the Java-Installed JREs (path as in the image below or under C:\Program Files\Eclipse Adoptium\ e.g., C:\Program Files\Eclipse Adoptium\jdk-8.0.362.9-hotspot)

    ![Eclipse Installed JREs0](/images/Eclipse-Installed-JRE.png)

    e. Set the Java->Installed JREs->Execution Environment for JavaSE-1.8 to point at the installed JDK

    ![Eclipse-Exec-Env](/images/Eclipse-Exec-Env.png)



2. Delete the existing projects in the Eclipse Workspace 

3. Import the code in the folder containing the extracted code into your Java IDE as Maven projects

    a. Do File->Import... (Eclipse menu bar)

    b. Select Existing Maven Projects and hit Next >

    ![Import-Existing-Maven](/images/Import-Existing-Maven.png)

    c. Set the root directory as C:\vFunctionLab\oms-services and select all Project

    ![Import-Dialog](/images/Import-Dialog.png)   

    d. Click Finish and wait for the load/build to complete

    ![Post-Import](/images/Post-Import.png)   

![vFunction Logo](/images/vFunction.png)
