---
title: "Azure DevOps “Run as Package” Change May Break Application"
author: Jason Gaylord
email: jason@jasongaylord.com
cloudscribe_id: "a5044911-0c9d-4b2e-8fc9-8492e6c642fc"
cloudscribe_path: "/Blog/azure-devops-change-may-break-application"
permalink: /Blog/azure-devops-change-may-break-application
date: 2019-02-25
categories: [Cloud, DevOps, Tip]
tags: 
---

Microsoft recently made a change to the deployment type in the release pipeline. This change offers some great benefits and is known as the “Run as Package” feature. The feature is explained at [https://github.com/Azure/app-service-announcements-discussions/issues/32](https://github.com/Azure/app-service-announcements-discussions/issues/32 "https://github.com/Azure/app-service-announcements-discussions/issues/32"). 

Run from package is a new way to allow an Azure Function, Azure WebApp, and other Azure web application types to run from within a zip file. The application settings for the application will have a new key named <font face="Courier New">WEBSITE_RUN_FROM_PACKAGE</font> set to a value of 1. Removing this key will stop your application from working. The benefit of this is to allow faster startup for deployments. However, there are limitations. One of the limitations is explained further below. However, for more details, visit [https://github.com/Azure/app-service-announcements/issues/84](https://jasong.us/2EoArTJ "https://jasong.us/2EoArTJ").

At some point in the past week, the default version in the release pipeline is now set to Version 4. This version has the “Select deployment method” checkbox disabled, which in turn, allows the “Run as Package” feature by default as well. To change this value, go into the “Deploy Azure App Service” task for each environment and expand Additional Deployment Options. You’ll probably want to change it most often to Web Deploy.

![](https://cdn.jasongaylord.com/images/2019/02/25/Additional_Deployment_Options.jpg)

Potentially, you’re Azure WebApp can experience issues with the change since during deployment, your application files and folders are locked for editing. So, if you plan on  folder structure so that you cannot add files or folders using the Azure tools or the application itself. So, if you are deploying a CMS, expect to use App Service Editor to create folders or files, or use a site extension (such as "Let's Encrypt") that creates folders in the app, it will not work as expected.

This is something to take note of in the event you choose this accidently and your application editing breaks.
