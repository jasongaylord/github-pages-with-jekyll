---
title: "Converting Unix Epoch to Date in Excel"
author: Jason Gaylord
email: jason@jasongaylord.com
cloudscribe_id: "15799d92-45d0-42f7-b040-dc0618d7863d"
cloudscribe_path: "/Blog/converting-unix-epoch-to-date-in-excel"
permalink: /Blog/converting-unix-epoch-to-date-in-excel
date: 2013-08-28
categories: [Archive]
tags: 
---

 <div id="codeSnippetWrapper">I ran into an interesting problem earlier today. I was using a CDR dump from our Cisco system. However, all of the datetime fields were represented as seconds. I knew right away that it used an epoch value. What I didn’t know is what the originating date was. Apparently, I was correct at my first guess. I guessed that it was using the standard Unix epoch value of 1/1/1970. Many applications, such as Microsoft Excel, use 1/1/1900.</div> 

Since I wanted to represent the correct date and time in Excel, I began looking around for a formula. To my surprise, nothing exists out of the box (unless my eyes are failing me). So, I had two options. The first option I headed down had me save my spreadsheet as a macro-enabled workbook. From there, I added a formula to an empty module.
 <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: " courier="" new",="" courier,="" monospace;="" font-size:="" 8pt;="" direction:="" ltr;="" background-color:="" rgb(244,="" 244,="" 244);"="">

<span id="lnum1" style="color: rgb(96, 96, 96);">   1:</span> <span style="color: rgb(0, 0, 255);">Public</span> <span style="color: rgb(0, 0, 255);">Function</span> EpochConversion(timeZoneOffset <span style="color: rgb(0, 0, 255);">As</span> <span style="color: rgb(0, 0, 255);">Long</span>, myNumber <span style="color: rgb(0, 0, 255);">As</span> <span style="color: rgb(0, 0, 255);">Long</span>, myDate <span style="color: rgb(0, 0, 255);">As</span> <span style="color: rgb(0, 0, 255);">Date</span>) <span style="color: rgb(0, 0, 255);">As</span> <span style="color: rgb(0, 0, 255);">Date</span>

<span id="lnum2" style="color: rgb(96, 96, 96);">   2:</span>     EpochConversion = DateAdd(<span style="color: rgb(0, 96, 128);">"s"</span>, myNumber + (timeZoneOffset * 3600), myDate)

<span id="lnum3" style="color: rgb(96, 96, 96);">   3:</span> <span style="color: rgb(0, 0, 255);">End</span> <span style="color: rgb(0, 0, 255);">Function</span>
</div>


The function accepts 3 parameters: timeZoneOffset which is the offset from GMT (for example, New York City is in the Eastern Time Zone which is –5), the number of seconds, and the base date (in the event I need to use 1/1/1900 instead). So, an example use would look like this:

[![20130828_1723_EpochConversion](/media/images/20130828_1723_epochconversion-wlw.png "20130828_1723_EpochConversion")](/media/images/20130828_1723_epochconversion.png)

That works, but it requires that my spreadsheet is a macro-enabled workbook. I can accomplish something similar by using the following formula. This is my second option for handling the conversion.

<div id="codeSnippetWrapper">
<div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: " courier="" new",="" courier,="" monospace;="" font-size:="" 8pt;="" direction:="" ltr;="" background-color:="" rgb(244,="" 244,="" 244);"="">

=(((G2-(5*3600))/86400)+25569)
</div></div>


In this formula, the following values are used:

<table width="452" border="1" cellspacing="0" cellpadding="2">
<tbody>
<tr>
<td width="52" valign="top">G2</td>
<td width="398" valign="top">The cell containing the number of seconds from epoch.</td></tr>
<tr>
<td width="57" valign="top">-</td>
<td width="393" valign="top">If you are in the western hemisphere, this would be negative. Otherwise, change this to a plus sign. This handles the offset from GMT.</td></tr>
<tr>
<td width="62" valign="top">5</td>
<td width="389" valign="top">The is the value of the timezone from GMT. It’s combined with the minus sign above.</td></tr>
<tr>
<td width="66" valign="top">3600</td>
<td width="385" valign="top">The number of seconds in an hour used to assist with the timezone offset.</td></tr>
<tr>
<td width="70" valign="top">86400</td>
<td width="382" valign="top">The number of seconds in a day.</td></tr>
<tr>
<td width="73" valign="top">25569</td>
<td width="380" valign="top">The number of days since 1/1/1900 to assist Excel in the proper epoch conversion of 1/1/1970.</td></tr></tbody></table>


In either case, I’ll obtain the same result.

One thing is for sure, I’m hoping that I’m retired by January 19th, 2038 so that we don’t have another Y2K crisis when the 32-bit versions of epoch have overflows: [http://2038bug.com/](http://2038bug.com/).
