---
title: "Creating a Twitter ViewComponent in ASP.NET Core – Part 2"
author: 
email: 
cloudscribe_id: "97689e0c-737e-4e9b-8232-218aa4933630"
cloudscribe_path: "/Blog/creating-a-twitter-viewcomponent-in-aspnet-core-–-part-2"
permalink: /Blog/creating-a-twitter-viewcomponent-in-aspnet-core-–-part-2
date: 2018-11-07
categories: [Development]
tags: 
---

Yesterday, I started heading down the path to create a Twitter ViewComponent. As I mentioned, when redesigning my website I wanted to show a list of recent tweets that I’ve made on the homepage. 

There will be 2 parts in this series:

*   [Part 1: Create an Interface and a Class to connect to Twitter](https://jasong.us/2Os34lz)
*   [Part 2: Create a View Component to handle pre-packaged UI](https://jasong.us/2PbDOpg)

If you are looking for a feature complete, ready to use example, feel free to visit [https://github.com/jasongaylord/gaylordsolutions.TwitterWidget](https://github.com/jasongaylord/gaylordsolutions.TwitterWidget). 

#### Setting up the Twitter Service in Middleware

Since we’ll start to add MVC features to our Class Library project, we’ll want to add the <font face="Courier New" size="2">Microsoft.AspNetCore.Mvc</font>, <font face="Courier New" size="2">Microsoft.AspNetCore.Mvc.ViewFeatures</font> and <font face="Courier New" size="2">Microsoft.Extensions.Options.ConfigurationExtensions</font> NuGet packages.

![](https://cdn.jasongaylord.com/images/2018/11/07/Nuget_Packages.png)

Next, we’ll create a static class called <font face="Courier New" size="2">ServiceCollectionExtensions</font>. In the class, we’ll create a new method called <font face="Courier New" size="2">AddTwitter</font> that’s an extension method of <font face="Courier New" size="2">IServiceCollection</font>. We’ll then add in our Twitter options we created in Part 1 as a singleton service and our Twitter service as a scoped service. An example is shown below:

#### Adding the ViewComponent

Up to this point, we’ve spent a decent amount of time setting up the foundation for our <font face="Courier New" size="2">ViewComponent</font> to work. Of course, if we had a different purpose, we may be reaching this point sooner. We’ll create a new class and name it <font face="Courier New" size="2">RetrieveTweetsViewComponent</font>. This will allow us to use RetrieveTweets in our Razor files or Razor pages.

As you can see, there’s not much to it. We’ll create a local protected property to hold our Twitter options that are passed in through the constructor. Then, we have a single async method called <font face="Courier New" size="2">InvokeAsync()</font> that creates the service and waits for the tweets to come back. Finally, you’ll see we are returning a default view. However, we haven’t created the view yet. So, let’s go do that now.

To do that, we’ll create a folder called Views\Shared\Components\RetrieveTweets and place a new Razor file called Default.cshtml in there. 

![](https://cdn.jasongaylord.com/images/2018/11/07/ViewComponentFolderStructure.png)

The Razor file won’t have much in it either. Within the file, we’ll loop through the tweets listing the message and showing the friendly date.

#### Adding Razor Support to the Library

This is one of the most important steps in this process. If you do not follow this step, you will not have the compiled views library included as an artifact in your build. Edit your .csproj file and change the project type from <font face="Courier New" size="2">Microsoft.NET.Sdk</font> to <font face="Courier New" size="2">Microsoft.NET.Sdk.Razor</font>. Your .csproj file should look similar to this:

#### Creating the Demo Application

If you are using Visual Studio, it’s probably easiest to create a new Web Project within the same solution as your library. If you are using VSCode, be sure to compile the class library and reference both DLLs that are generated. The files generated will look like this:

![](https://cdn.jasongaylord.com/images/2018/11/07/LibrariesGenerated.png)

In your appsettings.json, you’ll want to add in the TwitterOptions section as we defined yesterday. For example:

Then, in your startup file, you’ll want to add the Twitter middleware by using:

<font face="Courier New" size="2">services.AddTwitter(Configuration.GetSection("TwitterOptions"));</font>

Finally, create a Razor page or edit an existing one so that the component is invoked. For example, you may end up with something like this:

#### Conclusion

Between the two days, we were able to put together a <font face="Courier New" size="2">ViewComponent</font> that should render our recent tweets. After compiling our demo application, we should get a result like this:

![](https://cdn.jasongaylord.com/images/2018/11/07/RecentTweets.png)

Of course we can take next steps to expand this by changing the formatting or including more options. I’ll be interested in seeing what you come up with. Be sure to post back or submit a pull request to the project at [https://github.com/jasongaylord/gaylordsolutions.TwitterWidget](https://github.com/jasongaylord/gaylordsolutions.TwitterWidget).
