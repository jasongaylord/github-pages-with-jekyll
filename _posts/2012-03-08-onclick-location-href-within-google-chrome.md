---
title: "JavaScript onClick Navigation Issues within Google Chrome are Solved"
author: Jason Gaylord
email: jason@jasongaylord.com
cloudscribe_id: "493938d7-6de9-45e2-b1f0-aabcf693c0a8"
cloudscribe_path: "/Blog/onclick-location-href-within-google-chrome"
permalink: /Blog/onclick-location-href-within-google-chrome
date: 2012-03-08
categories: [Archive]
tags: 
---

For the longest time, If I needed to use an <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">onclick</span> event for navigation (<span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">div</span> or some other page element), I’d use something similar to:

<div onClick="location.href('/admin');"><!-- Something here --></div>

However, Google Chrome interprets the <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">href</span> property as a method or an object initializer. Instead, to get the <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">onclick</span> navigation to work properly in Chrome, set the property to a value using a typical setter such as:

<div onClick="location.href='/admin';"><!-- Something here --></div>

This simple change will allow Google Chrome to properly navigate to the page.

Hope that helps!

[CodeProject](http://www.codeproject.com)
