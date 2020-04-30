---
title: "Git Tip: Link a Local Project to a Hosted Repository"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "4269bb21-10ed-4cfe-9f23-64fb19463a5e"
cloudscribe_path: "/Blog/git-tip-link-a-local-project-to-a-hosted-repository"
permalink: /Blog/git-tip-link-a-local-project-to-a-hosted-repository
date: 2018-11-16
categories: Development,Tip
tags: 
---

How many times have you started a project locally on your machine, initialized it as a git repository, then after doing some work, realized that you have a repository sitting on GitHub or Azure DevOps with a readme markdown file and a .gitignore file? If you’re like me, that probably happens more than you’d like to admit. There’s an easy solution for this. 

First, we need to add a remote. We can do this by using the following command:

<font face="Courier New">git remote add origin https://{path-to-repository} </font>

Next, we need to take our existing branch, presumably it’s the master branch, and create the link between the origin\master and the local master branch:

<font face="Courier New">git branch --set-upstream-to=origin/master master</font>

Finally, when we pull our changes, we may run into the following:

<font face="Courier New">>git pull  
 fatal: refusing to merge unrelated histories</font>

This can be solved by merging in the unrelated histories. We can do this by using:

<font face="Courier New">git pull --allow-unrelated-histories</font>

Just note, we may now have merge conflicts as there can be files with the same name in both locations. However, we can follow our normal diff processes to determine which file or portion of each we need to keep.
