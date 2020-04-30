---
title: "Detecting Browser Features and Internet Explorer Compatibility Mode"
author: Jason Gaylord
email: jason@jasongaylord.com
cloudscribe_id: "05fa947f-4afb-45cf-9af0-5d6b54b8827c"
cloudscribe_path: "/Blog/detecting-browser-features-and-ie-compatibility-mode"
permalink: /Blog/detecting-browser-features-and-ie-compatibility-mode
date: 2013-06-08
categories: [Archive]
tags: 
---

First of all, before I begin, please know that in every case, you should detect browser features and not browser versions. However, there are still times that you may need to know the browser version (such as providing screenshots of various browser alerts – ie: ActiveX installation).

**Detecting IE Compatibility Mode**

There are several JavaScript files that are available to detect browsers and their versions. However, I have never come across something that can properly detect IE compatibility mode. This is important as IE10, when run in compatibility mode, runs IE7 quirks mode. 

You can obtain the desired values by capturing the <font face="Courier New" size="2">userAgent</font> string and parsing it. I’ve created a quick JavaScript function to capture three different properties: <font face="Courier New" size="2">compatibilityMode</font> (true/false), <font face="Courier New" size="2">version</font> (float), and <font face="Courier New" size="2">renderVersion</font> (float). If <font face="Courier New" size="2">compatibilityMode</font> is true, the <font face="Courier New" size="2">renderVersion</font> is set to a different value than <font face="Courier New" size="2">version</font>. This is the version of IE that is emulated within the browser.

A complete example is shown below:

The output for this looks like the following:
<iframe src="http://jasongaylord.com/Media/Default/Post-Downloads/IECompatMode/ieCompatModeTest.html" style="border: 1px solid navy; border-image: none; width: 100%; height: 60px;"></iframe> 

If you change over to compatibility mode in IE, you’ll notice that the output changes.

*<font size="2">NOTE: The above demonstrates how to read the User Agent string to check to see if IE compatibility mode is enabled. This does not check all browser types and, if used, this should be expanded for your specific purpose.</font>*

**Why is this Bad?**

When you review the JavaScript, you’ll notice that we’re checking for IE versions 7 through 10. However, there are hundreds of user agent strings. As an example, look at the following link to see the user agents that have been documented for Internet Explorer: [http://useragentstring.com/pages/Internet%20Explorer/](http://jasong.us/18e0VUd)

What do we do when Chrome 74 is released? What about Internet Explorer 11? Keeping up with user agent strings is a nightmare which is why there are so many commercial products that attempt to detect browser versions.

**The Solution: Detecting Browser Features**

In the past, it may have been difficult to detect browser features as there were so many potential implementations of a feature. In nearly all modern browsers, features have all been standardized around HTML 5. [<a href="http://jasong.us/18e1FIW" target="_blank">Internet Explorer 10</a> standardizes in HTML 5. Google <a href="http://jasong.us/13MvMkq" target="_blank">recently announced that their abandoning WebKit</a> to standardize more.

It’s not that difficult to check for features. It’s as simple as checking to see if the feature is undefined and then acting upon it. You can see an example below:

In this case, since WebKit has its own implementation of the getUserMedia() method, we must include the webkit preface to some of the properties.

You can see this in live action by <a href="http://jasong.us/13MwxtO" target="_blank">clicking here</a>. If you are using Chrome or another WebKit browser, you’ll be prompted to allow the browser to have access to your webcam. If not, you should get an error message.

Feel free to <a href="https://gist.github.com/jasongaylord/5734097" target="_blank"><a href="https://gist.github.com/jasongaylord/5734097" target="_blank">fork the Gist</a> above and begin adding your own features to detect to the BrowserFeatures object.

</a>](http://www.modern.ie/en-us)
