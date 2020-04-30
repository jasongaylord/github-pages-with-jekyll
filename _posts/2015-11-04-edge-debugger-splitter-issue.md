---
title: "Edge Debugger Splitter Issue"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "e386790f-cbb8-4390-b7c2-d1f6a595b89f"
cloudscribe_path: "/Blog/edge-debugger-splitter-issue"
permalink: /Blog/edge-debugger-splitter-issue
date: 2015-11-04
categories: Archive
tags: 
---

The other day I hit F12 and started to debug some code. Microsoft Edge stopped showing the left side of the splitter that shows file content and the file browser for scripts and such. The issue breaks down that the right window was set at 100%. After talking with some people on the Microsoft Edge team, the solution, for now, was to tweak a registry key. The key to update is below, if you are using the Windows 10 RTM version (meaning you’re not on the Slow or Fast ring for updating):
 <div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; border-image: none; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: " courier="" new",="" courier,="" monospace;="" font-size:="" 8pt;="" cursor:="" text;="" direction:="" ltr;="" max-height:="" 200px;="" background-color:="" rgb(244,="" 244,="" 244);"=""> <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: " courier="" new",="" courier,="" monospace;="" font-size:="" 8pt;="" direction:="" ltr;="" background-color:="" rgb(244,="" 244,="" 244);"="">

HKEY_CURRENT_USER\SOFTWARE\Classes\Local 

Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Storage\microsoft.microsoftedge_8wekyb3d8bbwe\MicrosoftEdge\F12
</div></div>


Change the value of DebuggerVEditorSplitterPosition to 0.2 or something greater than 0 and less than 1. Your splitter bar will now appear.


The initial screen looked like this below:


[![20151104_1242_EdgeDevToolsSplitterIssue](/media/images/20151104_1242_edgedevtoolssplitterissue-wlw.png "20151104_1242_EdgeDevToolsSplitterIssue")](/media/images/20151104_1242_edgedevtoolssplitterissue.png)

Special thanks to [Andy Sterland](https://twitter.com/AndySterland) for the help on this.<p>The other day I hit F12 and started to debug some code. Microsoft Edge stopped showing the left side of the splitter that shows file content and the file browser for scripts and such. The issue breaks down that the right window was set at 100%. After talking with some people on the Microsoft Edge team, the solution, for now, was to tweak a registry key. The key to update is below, if you are using the Windows 10 RTM version (meaning you’re not on the Slow or Fast ring for updating):</p> <div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; border-image: none; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: &quot;Courier New&quot;, courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 200px; background-color: rgb(244, 244, 244);"> <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: &quot;Courier New&quot;, courier, monospace; font-size: 8pt; direction: ltr; background-color: rgb(244, 244, 244);"><pre style="margin: 0em; padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: &quot;Courier New&quot;, courier, monospace; font-size: 8pt; direction: ltr; background-color: white;">HKEY_CURRENT_USER\SOFTWARE\Classes\Local </pre><!--CRLF--><pre style="margin: 0em; padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: &quot;Courier New&quot;, courier, monospace; font-size: 8pt; direction: ltr; background-color: rgb(244, 244, 244);">Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Storage\microsoft.microsoftedge_8wekyb3d8bbwe\MicrosoftEdge\F12</pre><!--CRLF--></div></div>
<p>Change the value of DebuggerVEditorSplitterPosition to 0.2 or something greater than 0 and less than 1. Your splitter bar will now appear.
<p>The initial screen looked like this below:
<p><a href="/media/images/20151104_1242_edgedevtoolssplitterissue.png"><img title="20151104_1242_EdgeDevToolsSplitterIssue" alt="20151104_1242_EdgeDevToolsSplitterIssue" src="/media/images/20151104_1242_edgedevtoolssplitterissue-wlw.png" border="0"></a><p>Special thanks to <a href="https://twitter.com/AndySterland" target="_blank">Andy Sterland</a> for the help on this.</p>