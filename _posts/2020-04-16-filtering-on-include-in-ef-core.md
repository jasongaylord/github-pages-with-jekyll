---
title: "Filtering on Include in EF Core"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "dd4d0a8b-148b-43f1-95f0-a56b036a90b2"
cloudscribe_path: "/Blog/filtering-on-include-in-ef-core"
permalink: /Blog/filtering-on-include-in-ef-core
date: 2020-04-16
categories: Development
tags: 
---

For years ([quite literally 3 years](https://jasong.us/34I5FSg)) I’ve been waiting for filtering to be available on includes within Entity Framework, or more specifically, EF Core. Finally, the next preview should [have this included](https://jasong.us/34NUSWL). From the pull request, the additional operations to be specified inside Include/ThenInclude are:

*   `Where`

*   `OrderBy(Descending)/ThenBy(Descending)`

*   `Skip`

*   `Take`

The [original request](https://jasong.us/3euxIJh) has been updated to show a few of the supported examples and restrictions. From the original request, note that only one filter allowed per navigation, so for cases where the same navigation needs to be included multiple times (e.g. multiple ThenInclude on the same navigation) apply the filter only once, or apply exactly the same filter for that navigation.

Example:

        customers 
            .Include(c => c.Orders.Where(o => o.Name != "Foo")).ThenInclude(o => o.OrderDetails) 
            .Include(c => c.Orders).ThenInclude(o => o.Customer)

or

        customers
            .Include(c => c.Orders.Where(o => o.Name != "Foo")).ThenInclude(o => o.OrderDetails)
            .Include(c => c.Orders.Where(o => o.Name != "Foo")).ThenInclude(o => o.Customer)

Special thanks to [Maurycy Markowski](https://jasong.us/2VhXFo9) for updating us all and [Gert Arnold](https://stackoverflow.com/users/861716/gert-arnold) for updating my original Stack Overflow request.<p>For years (<a href="https://jasong.us/34I5FSg" target="_blank">quite literally 3 years</a>) I’ve been waiting for filtering to be available on includes within Entity Framework, or more specifically, EF Core. Finally, the next preview should <a href="https://jasong.us/34NUSWL" target="_blank">have this included</a>. From the pull request, the additional operations to be specified inside Include/ThenInclude are:</p>

<ul>
	<li><code>Where</code></li>
	<li><code>OrderBy(Descending)/ThenBy(Descending)</code></li>
	<li><code>Skip</code></li>
	<li><code>Take</code></li>
</ul>

<p>The <a href="https://jasong.us/3euxIJh" target="_blank">original request</a> has been updated to show a few of the supported examples and restrictions. From the original request, note that only one filter allowed per navigation, so for cases where the same navigation needs to be included multiple times (e.g. multiple ThenInclude on the same navigation) apply the filter only once, or apply exactly the same filter for that navigation.</p>

<p>Example:</p>

<pre>
<code>customers 
    .Include(c =&gt; c.Orders.Where(o =&gt; o.Name != "Foo")).ThenInclude(o =&gt; o.OrderDetails) 
    .Include(c =&gt; c.Orders).ThenInclude(o =&gt; o.Customer)</code></pre>

<p>or</p>

<pre>
<code>customers
    .Include(c =&gt; c.Orders.Where(o =&gt; o.Name != "Foo")).ThenInclude(o =&gt; o.OrderDetails)
    .Include(c =&gt; c.Orders.Where(o =&gt; o.Name != "Foo")).ThenInclude(o =&gt; o.Customer)</code></pre>

<p>Special thanks to <a href="https://jasong.us/2VhXFo9" target="_blank">Maurycy Markowski</a> for updating us all and <a href="https://stackoverflow.com/users/861716/gert-arnold" target="_blank">Gert Arnold</a> for updating my original Stack Overflow request.</p>
