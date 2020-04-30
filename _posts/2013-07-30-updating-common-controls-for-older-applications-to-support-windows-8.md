---
title: "Updating Common Controls for Older Applications to Support Windows 8"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "5b0b2357-1f98-4471-be8e-03da5dd3b129"
cloudscribe_path: "/Blog/updating-common-controls-for-older-applications-to-support-windows-8"
permalink: /Blog/updating-common-controls-for-older-applications-to-support-windows-8
date: 2013-07-30
categories: Archive
tags: 
---

There are times that you may need to install an older Windows application especially something developed using Visual Basic 6 or earlier. In these cases, you should always ensure that the installed application is using the most current common control library available from Microsoft. If not, you may receive strange error message that logs the following in the Event Viewer (abbreviated exception):

<div id="codeSnippetWrapper">
<div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: " courier="" new",="" courier,="" monospace;="" font-size:="" 8pt;="" direction:="" ltr;="" background-color:="" rgb(244,="" 244,="" 244);"="">


<span id="lnum1" style="color: rgb(96, 96, 96);">   1:</span> Log Name: Application

<span id="lnum2" style="color: rgb(96, 96, 96);">   2:</span> Source: Application Error

<span id="lnum3" style="color: rgb(96, 96, 96);">   3:</span> Date: 07/08/2013 11:10:57 AM

<span id="lnum4" style="color: rgb(96, 96, 96);">   4:</span> Event ID: 1000

<span id="lnum5" style="color: rgb(96, 96, 96);">   5:</span> Task Category: (100)

<span id="lnum6" style="color: rgb(96, 96, 96);">   6:</span> Level: Error

<span id="lnum7" style="color: rgb(96, 96, 96);">   7:</span> Keywords: Classic

<span id="lnum8" style="color: rgb(96, 96, 96);">   8:</span> User: N/A

<span id="lnum9" style="color: rgb(96, 96, 96);">   9:</span> Computer: my-msft-surface

<span id="lnum10" style="color: rgb(96, 96, 96);">  10:</span> Description:

<span id="lnum11" style="color: rgb(96, 96, 96);">  11:</span> Faulting application name: TestComControls.exe, version: 1.0.0.0, time stamp: 0x4cb60c27

<span id="lnum12" style="color: rgb(96, 96, 96);">  12:</span> Faulting module name: comctl32.ocx, version: 6.0.81.5, time stamp: 0x3802598b

<span id="lnum13" style="color: rgb(96, 96, 96);">  13:</span> Exception code: 0xc000041d

<span id="lnum14" style="color: rgb(96, 96, 96);">  14:</span> Fault offset: 0x00020f51

<span id="lnum15" style="color: rgb(96, 96, 96);">  15:</span> Faulting process id: 0x858

<span id="lnum16" style="color: rgb(96, 96, 96);">  16:</span> Faulting application start time: 0x01ce7bed4062ea40

<span id="lnum17" style="color: rgb(96, 96, 96);">  17:</span> Faulting application path: C:\Program Files (x86)\Test\TestComControls.exe

<span id="lnum18" style="color: rgb(96, 96, 96);">  18:</span> Faulting module path: C:\Windows\SYSTEM32\comctl32.ocx

<span id="lnum19" style="color: rgb(96, 96, 96);">  19:</span> Report Id: 96a08c71-e7e0-11e2-be6c-6045bd92f0bd

<span id="lnum20" style="color: rgb(96, 96, 96);">  20:</span> Faulting package full name:

<span id="lnum21" style="color: rgb(96, 96, 96);">  21:</span> Faulting package-relative application ID:

</div>
</div>


On most Windows 8 machines, the application worked correctly. However, in the case of a touch device such as our Microsoft Surface Pro, whenever we used touch or the pen for input, this error would occur. So, in this case, we needed to update to the latest COM controls. These were found at [http://www.microsoft.com/en-us/download/details.aspx?id=10019](http://jasong.us/1ckYsqp "http://www.microsoft.com/en-us/download/details.aspx?id=10019").
