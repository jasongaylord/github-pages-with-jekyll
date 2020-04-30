---
title: "Resolving an SmtpException stating 'Too many messages for this session'"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "cb418641-7e6f-45a7-83ae-fed7241fc0de"
cloudscribe_path: "/Blog/resolving-smtpexception-too-many-messages-for-this-session"
permalink: /Blog/resolving-smtpexception-too-many-messages-for-this-session
date: 2012-02-21
categories: Archive
tags: 
---

Have you ever noticed an exception being thrown by your application stating something like the following:

    System.Net.Mail.SmtpException: Service not available, closing transmission channel. 
    The server response was: #4.x.2 Too many messages for this session

This has been an issue since early versions of the <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">System.Net.Mail</span> namespace. The <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">SmtpServer</span> object never included a <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">Dispose()</span> method that properly shutdown the connection to the server. So, even if you are creating new objects, the GC never disposed of the original thus causing this exception.

There are two workarounds for this exception as document on the [Connect website](http://jasong.us/wXDVAH):

1.  Upgrade to the .NET Framework 4.0 or later. This version of the framework now includes a <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">Dispose() </span>method that properly closes the connection to the server. Anytime you are connecting to the server to send a message, you should dispose the object afterwards.  

2.  If you are using older versions of the framework (.NET Framework 3.5 or earlier), you can set the <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">MaxIdleTime</span> property to 0 and the <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">ConnectionLimit</span> to 1 on the <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">SmtpClient</span>’s <span face="Consolas" size="2" style="font-family: consolas; font-size: x-small;">ServicePoint</span> object. For example, your code may look like the following:

> var client = new SmtpClient("hostname");
>     client.ServicePoint.MaxIdleTime = 0;
>     client.ServicePoint.ConnectionLimit = 1;
>     ...
>     client.Send(new MailMessage(...));
> 
>     // at this point, the connection will get closed
>     // since the ServicePoint idle time is now 0.

Hope this helps to solve any issues you’ve had with this.

[CodeProject](http://www.codeproject.com)
