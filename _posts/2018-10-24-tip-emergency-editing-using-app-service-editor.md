---
title: "Tip: Emergency Editing using App Service Editor"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "4ff4e6fc-9f8e-44a6-a7b1-4b2d3f0d291b"
cloudscribe_path: "/Blog/tip-emergency-editing-using-app-service-editor"
permalink: /Blog/tip-emergency-editing-using-app-service-editor
date: 2018-10-24
categories: Development,Tip
tags: 
---

Imagine that you’ve published a web app to an app service in Azure. You’ve tested the app and then head out to dinner with family and friends. You decide to showcase your website over dinner and see an error. Now what?

You may not be aware, but Azure App Services have an option under the Development Tools menu called the App Service Editor.  It’s currently in Preview mode but I would anticipate this graduating in the next few months. 

![](https://cdn.jasongaylord.com/images/2018/10/23/Azure_App_Service_Editor.png)

This tool allows real time code updates to your application. Not only does it provide upload and download functionality, but you’ll have an online editor for text based files such as razor files or JavaScript. Simply open a file, make the change, and your change will automatically save. With this great power comes great responsibility. Whichever application you edit will be changed live. If you do edit production, whatever change (even partial change) you make will be live.
<div class="alert alert-danger">**Caution: It is not recommended to update a production application unless you understand the full ramifications of what you are changing.**</div>

In addition to the notice above, if your application uses a CI/CD process, the next time your application is automatically deployed, your changes will be destroyed. So, I’d highly recommend using this only in an emergency situation and to copy any changes back to your real source code.
<div class="alert alert-primary">**Bonus Tip**: Azure App Services can also have an application or virtual directory defined within the app service. Today, there’s no obvious way to use the App Service Editor on the application. However, you can do so by using the URL structure similar to this: [https://{AppServiceName}.scm.azurewebsites.net/dev/{AppName}/wwwroot/](https://{AppServiceName}.scm.azurewebsites.net/dev/{AppName}/wwwroot/ "https://bhportalspa.scm.azurewebsites.net/dev/quote/wwwroot/"). Be sure to replace {AppServiceName} with the application name and {AppName} with the application or virtual directory name.</div>
