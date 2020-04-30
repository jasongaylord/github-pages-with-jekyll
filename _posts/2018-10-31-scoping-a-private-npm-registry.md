---
title: "Scoping a Private NPM Registry"
author: Jason Gaylord
email: jason@jasongaylord.com
cloudscribe_id: "fbecda99-60d8-4822-ad30-a1d0dfbb5a37"
cloudscribe_path: "/Blog/scoping-a-private-npm-registry"
permalink: /Blog/scoping-a-private-npm-registry
date: 2018-10-31
categories: [Development]
tags: 
---

If you’re using a custom package manage, such as JFrog, Verdaccio, or Azure Artifacts, you’ll notice that each includes an upstream feed allowing you to cache publicly available npmjs.org packages. However, you may prefer to use the public feed for public packages assuring that you have the latest versions. In this case, you’ll want to scope your NPM repository. In a lot of cases, you’ll have a username and password accompanying the custom NPM feed. So, I recommend referencing the repository in an .npmrc within the project and storing your credentials in an .npmrc file in your default user bin (in Windows, this is usually <font face="Courier New" size="2">%userprofile%</font>) 

The .npmrc file in the project, may look like this:

<span style="color: rgb(128, 128, 48);">@</span>foo<span style="color: rgb(128, 128, 48);">:</span>registry<span style="color: rgb(128, 128, 48);">=</span>https<span style="color: rgb(128, 128, 48);">:</span><span style="color: rgb(105, 105, 105);">//foo.pkgs.visualstudio.com/_packaging/bar/npm/registry/</span>
<span style="color: rgb(128, 128, 48);">@</span>foo<span style="color: rgb(128, 128, 48);">:</span>always<span style="color: rgb(128, 128, 48);">-</span>auth<span style="color: rgb(128, 128, 48);">=</span><span style="color: rgb(128, 0, 0); font-weight: bold;">true</span>



<div class="alert alert-primary">**Tip**: If you do not scope that you are always authenticating, you will receive an error that 'This request requires auth credentials. Run `npm login` and repeat the request.' This is due to the login being globally set instead of set to the appropriate repository.</div>

The .npmrc file in your user profile, may look like this:

<span style="color: rgb(105, 105, 105);">//foo.pkgs.visualstudio.com/_packaging/bar/npm/registry/:_authToken={AUTH_TOKEN}</span>
<span style="color: rgb(105, 105, 105);">//foo.pkgs.visualstudio.com/_packaging/bar/npm/:_authToken={AUTH_TOKEN}</span>

