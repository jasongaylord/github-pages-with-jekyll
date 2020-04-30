---
title: "Force Email to be Confirmed with Identity"
author: Jason Gaylord
email: jason@jasongaylord.com
cloudscribe_id: "fa5e5f9d-5be7-4fd8-9490-5ea2e6e63514"
cloudscribe_path: "/Blog/force-email-to-be-confirmed-with-identity"
permalink: /Blog/force-email-to-be-confirmed-with-identity
date: 2016-01-28
categories: [Archive]
tags: 
---

Microsoft Identity is an extremely flexible solution for authentication in modern web applications. The default table structure created with Identity contains properties for EmailConfirmed and PhoneConfirmed. Out of the box, these fields simply indicate whether or not the related fields have been confirmed.

In some circumstances, you may want to force the email address to be confirmed before allowing sign-in. If so, you will want to update the ApplicationSignInManager accordingly. The code snippet below demonstrates this:
