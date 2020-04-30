---
title: "Using PowerShell to Obtain CD/DVD Disk Information"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "31845b4a-1f3d-4a33-b01c-956f3a9d338f"
cloudscribe_path: "/Blog/using-powershell-to-obtain-cd-dvd-disk-information"
permalink: /Blog/using-powershell-to-obtain-cd-dvd-disk-information
date: 2013-05-29
categories: Archive
tags: 
---

As the years go by, more and more research, information, and documents can be found online. However, several business verticals still use CDs and DVDs to access research content, backup documents, and share files. In every position that I’ve ever held, I have been asked by someone to locate a disk. I had an old WMI script that would grab the information, place it in a text file on a machine, and notify me via a net message that the file was ready. This was great and did the job, but I wanted to see how I can do the same using PowerShell (and WMI).

When you install PowerShell, it’s capabilities can be expanded through modules. One of the modules that is found in the base installation of PowerShell is the Microsoft.PowerShell.Management module. This module contains a method called <font face="Courier New" size="2">Get-WmiObject</font>. This method will use WMI to gain access to certain machine information. In this case, we can obtain the drive information by using the class <font face="Courier New" size="2">Win32_LogicalDisk</font> and filtering the drive type to <font face="Courier New" size="2">2</font> and <font face="Courier New" size="2">5</font>. We’ll choose 2 and 5 as this will return only the Removable Disc and Compact Disc drives. The [<a href="http://jasong.us/146i3n5" target="_blank">other drive types</a> are shown below:

> <table width="238" border="0" cellspacing="0" cellpadding="2"> <tbody> <tr> <td width="57" valign="top"><font face="Segoe UI Semibold">Value</font></td> <td width="179" valign="top"><font face="Segoe UI Semibold">Meaning</font></td></tr> <tr> <td width="57" valign="top">0</td> <td width="179" valign="top">Unknown</td></tr> <tr> <td width="57" valign="top">1</td> <td width="179" valign="top">No Root Directory</td></tr> <tr> <td width="57" valign="top">2</td> <td width="179" valign="top">Removable Disk</td></tr> <tr> <td width="57" valign="top">3</td> <td width="179" valign="top">Local Disk</td></tr> <tr> <td width="57" valign="top">4</td> <td width="179" valign="top">Network Drive</td></tr> <tr> <td width="57" valign="top">5</td> <td width="179" valign="top">Compact Disk</td></tr> <tr> <td width="57" valign="top">6</td> <td width="179" valign="top">RAM Disk</td></tr></tbody></table>

From each of these drives, we’ll be able to obtain the <font face="Courier New" size="2">DriveID</font> (drive letter) and <font face="Courier New" size="2">VolumeName</font> (CD/DVD label or name of the removable device). Finally, we’ll pass this information into a custom <font face="Courier New" size="2">psobject</font> to display a result table such as below:

<a href="/media/images/20120529_1628_powershelloutput.png">![20120529_1628_PowershellOutput](/media/images/20120529_1628_powershelloutput-wlw.png "20120529_1628_PowershellOutput")</a>

The final script appears as below:

For this script to work, remote RPC needs to be enabled, it should be executed from an administrator account, and it should either be signed or executed by allowing (temporarily) unsigned scripts to be executed. This script has been tested to work with PowerShell v1 so that it will work with legacy versions of PowerShell. With later versions of PowerShell (and potentially with this version), this may be able to be refactored.

Feel free to submit revisions to this <a href="http://jasong.us/11zC7lO" target="_blank">Gist</a>.
](http://msdn.microsoft.com/en-us/library/windows/desktop/aa394173(v=vs.85).aspx)
