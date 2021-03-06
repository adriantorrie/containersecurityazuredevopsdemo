# ContainerSecurityAzureDevOpsDemo
An Azure DevOps Pipeline Demo to showcase scanning of images during build pipeline using Qualys Container Security (CS) before being pushed to the registry for deployment in Azure Web Apps and Scanning of Web Apps in QA slot using Qualys Web Application Scanning (WAS) before swapping it to production

## License
_**THIS SCRIPT IS PROVIDED TO YOU "AS IS."  TO THE EXTENT PERMITTED BY LAW, QUALYS HEREBY DISCLAIMS ALL WARRANTIES AND LIABILITY FOR THE PROVISION OR USE OF THIS SCRIPT.  IN NO EVENT SHALL THESE SCRIPTS BE DEEMED TO BE CLOUD SERVICES AS PROVIDED BY QUALYS**_

## Description
The aim of this repository is to build a solution which will help you understand how Qualys CS and WAS can be used to detect vulnerabilities in the Container Image and Web applications built from it.

## **Prerequisites:**
  1. [**An Azure Container Registry**](/prerequisite/azurecontainerregistry.md)
  2. [**An Azure APP service with Containers**](/prerequisite/azureappservice.md)
  3. [**A Qualys Subscription**](https://www.qualys.com/free-trial/)
 
## Usage
**Task 1:** Use the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/) to provision the project to your Azure DevOps Org. Use the below GitHub link as source template
_https://raw.githubusercontent.com/mkhanal1/containersecurityazuredevopsdemo/master/containersecuritydemo.zip_

  ![Image1](/images/1.png?raw=true)
  ![Image2](/images/2.png?raw=true)

**Task 2:** Import this repository to Azure GIT

![Image3](/images/3.png?raw=true)


**Task 3:** Edit your pipeline variables in Variable Groups
The template file has these 9 variables.

  * **QUALYS_API_SERVER:** "Qualys baseurl for CS API"
  * **QUALYS_PASSWORD:** "Qualys password to call CS API"
  * **QUALYS_USERNAME:** "Qualys username to call CS API"
  * **QUALYS_WAS_PROFILEID:** "Option Profile Id"
  * **SENSOR_ACTIVATION_ID:** " Activation Id for the container sensor"
  * **SENSOR_CUSTOMER_ID:** "Qualys subscription’s customerId"
  * **WEBAPP_PASSWORD:** "Password for the Webapp"
  * **WEBAPP_USERNAME:** "username for the Webapp"
  * **SENSOR_LOCATION:** "Path to download the sensor"
  
  Eg: _https://{storage-account}.blob.core.windows.net/{container-name}/QualysContainerSensor.tar_
  
  
**Task 4:** Edit the Build Pipeline

  * Select the Task **Build an image** and edit the parameters
  
    Parameter|Value|Notes|
    ---------|-----|-----|
    Container Registry Type | Azure Container Registry | Azure Container Registry to connect to it by using an Azure Service Connection |
    Azure subscription | Name of service connection | select the Azure subscription from the list and click 'Authorize'. |
    Azure Container Registry | Name of the registry | The container image will be built and pushed to this container registry in the selected Azure Subscription |
  
    ![Image4](/images/4.png?raw=true)
  
  * Select the Task **Push an image**
  
    Use the same parameters as described in Task "Build an image"
    

**Task 5:** Edit the release Pipeline

  * Select the stage "Stage 1"
  
    Parameter|Value|Notes|
    ---------|-----|-----|
    Azure subscription | Name of service connection | select the Azure subscription from the list and click 'Authorize'. |
    App type | Web App for Containers (Linux) | type of app service to host the application |
    App service name | Name of the app | an existing Azure App Service |
    Registry or Namespace | Name of registry | A globally unique top-level domain name for your specific registry | 
    Repository | Name of repository | repository where the container images are stored | 
    Resource group | Name of Resource Group| the Azure Resource group that contains the Azure App Service specified |
    Slot | Name of slot | an existing Slot other than the Production slot |
  
    ![Image5](/images/5.png?raw=true)
  
  * Select the Task **Deploy Azure App Service to Slot**
  
    Use the same parameter named **Azure subscription** as described in stage.
  
  * Select the Task **Deploy Azure App Service to Slot**
  
    Use the same parameter named **Azure subscription** as described in stage.
