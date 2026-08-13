# Azure Resource Manager 
Single layer to deploy resources 

System that helps you organize, manage and create resources in the cloud. 

ARM is a central organizer for your Azure resources 

![[Pasted image 20251121184807.png]]

Azure portal makes a call to azure resource manager to create a resource, for example a VM with a specific OS and version. 

The resource manager passes the information to the VM and the VM service does the deployment

Every call goes through the Resource Manager

*What if you pass an older version of the VM through the CLI or PowerShell?*
When you specify the version 

# ARM Templates
Doing things manually will most probably cause issues. That's why we use templates. 

From the resource group, you can view every resource you have deployed. From this 'trash can of resources' you can create a template. Select any of the deployments and then you click 'view template' you will get a json structure that represents the deployment. 

Also, inside the template section where you see the json, you can click on `edit template/custom template`, here you can modify some of the values within the json and create a custom new template 

Inside each resource there is also a button to export template 

**How do you make a template of several resources**

**PROMPT**: In 1,000 words or less, please address each of the following items in your statement:  
  
**Areas of Interest**: Discuss the areas of interest that you wish to study in the MSIS program as well as identify any significant issues or problems within those areas that you would like to explore or address during your studies.  
  
**Background & Experience**: Describe how your academic background and work experiences have prepared you for graduate studies in the field of information and why you wish to study specifically at the UT Austin iSchool.  
  
**Career Objective(s)**: Discuss your long-term career goals and how you anticipate the completion of your MSIS degree advancing your career.