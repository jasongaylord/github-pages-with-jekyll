---
title: "T-SQL Count of Tables, Views, Stored Procedures and Functions"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "317bb8c7-0cab-4830-b596-a3b3bec5513d"
cloudscribe_path: "/Blog/tsql-count-tables-views-sprocs-functions"
permalink: /Blog/tsql-count-tables-views-sprocs-functions
date: 2013-10-29
categories: Archive
tags: 
---

Have you ever needed to obtain a list or count of all tables, views, stored procedures, and functions in a database? It’s quite easy. Simply copy the T-SQL from below to a query window, set the desired database and execute.
 <div id="codeSnippetWrapper"> <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: " courier="" new",="" courier,="" monospace;="" font-size:="" 8pt;="" direction:="" ltr;="" background-color:="" rgb(244,="" 244,="" 244);"="">

<span style="color: rgb(0, 0, 255);">SELECT</span> * <span style="color: rgb(0, 0, 255);">FROM</span> INFORMATION_SCHEMA.TABLES <span style="color: rgb(0, 0, 255);">WHERE</span> TABLE_TYPE=<span style="color: rgb(0, 96, 128);">'BASE TABLE'</span>

<span style="color: rgb(0, 0, 255);">SELECT</span> * <span style="color: rgb(0, 0, 255);">FROM</span> INFORMATION_SCHEMA.VIEWS

<span style="color: rgb(0, 0, 255);">SELECT</span> * <span style="color: rgb(0, 0, 255);">FROM</span> INFORMATION_SCHEMA.ROUTINES <span style="color: rgb(0, 0, 255);">WHERE</span> ROUTINE_TYPE = <span style="color: rgb(0, 96, 128);">'PROCEDURE'</span>

<span style="color: rgb(0, 0, 255);">SELECT</span> * <span style="color: rgb(0, 0, 255);">FROM</span> INFORMATION_SCHEMA.ROUTINES <span style="color: rgb(0, 0, 255);">WHERE</span> ROUTINE_TYPE = <span style="color: rgb(0, 96, 128);">'FUNCTION'</span>
</div></div>


This will produce four result sets that will list the tables, views, stored procedures and functions. You can simply update the select statements with the keyword count to grab the count of each object if that’s all you are looking for.
