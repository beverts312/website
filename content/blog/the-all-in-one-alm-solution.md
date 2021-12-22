---
date: 2016-12-17
title: "The all-in-one ALM Solution"
author: Bailey Everts
---

##### The Problem 
Many large enterprises still insist on running their Application Lifecycle Management (ALM) tools in house, they pour a ton of resources into what often ends up being a large suite of a mismanaged tools that loosely integrate with each other. This becomes a pain point for developers and the usage of these tools turns almost ceremonial in nature and leads to things like high developer turnover. Furthermore the mismanagement of these tools can make them nearly unusable.  

In this world, even if developers are disciplined enough (and able) to use the tools properly, it is extremely difficult to sees a connection between a developer checkin, a build, a test case, a version, a deployment, approval(s), and/or whatever steps happen as part of your ALM process. Often many, if not all of these steps happen in different tools, not only does this make it difficult to get an end to end picture in the event of a problem or audit, but it requires developers to change context numerous times (which slows them down).    

##### What is Visual Studio Team Services (VSTS)?  
[VSTS](https://www.visualstudio.com/team-services/) is a SaaS ALM tool (ALMaaS if you will) from Microsoft. Team Foundation Service is the on-premise equivalent. It has modules for version control, build, release, package, test case, and project management. With all of these capabilities in one tool traceability is easy. We can look at a release and see exactly what feature(s) are being released, what build(s) produced those artifacts, and the commits that triggered those builds. VSTS has easy to configure dashboards that allow its users to see all of the information that is important to them relative to the project on one screen.    

![](/content/images/2016/12/Screenshot-from-2016-12-11-15-24-43.png)    

Here is a breakdown of the different tabs (from left to right in the image above):

* **Home** - This tab is made up of easily customized dashboards to view information about your project.
* **Code** - In this tab you can view browse your repositories and commit history. Supports Git and TFSVC.
* **Work** - In this tab you can manage your work items. Supports Agile, CMMI, and Scrum. The templates are extremely customizable.
* **Build & Release** - In this tab you can create/manage your builds, releases, artifacts, and packages. The build & release systems are heavily customizable. Currently the only package types supported are NuGet and NPM. 
* **Test** - In this tab you can create/manage Test Cases & Plans as well as Load Tests
* **Arcade Hub** - Microsoft has even added games to VSTS. *Note: You must install [Galactic Dodge](https://marketplace.visualstudio.com/items?itemName=ms-devlabs.galactic-dodge) for this tab to appear*
* **Settings** - From here we can manage project level settings. There is a different section for account management  

Each one of these tabs encapsulate capabilities that are often provided by at least one tool, with VSTS all of these capabilities are provided by one tool. The deep integration provided by this makes it possible to setup Continuous Integration and Delivery flows with just a few clicks. 

##### But I don''t use C#/Windows/Azure?  
Under Satya Nadella Microsoft has made monumental changes towards embracing Linux and Open Source. VSTS is no exception to that trend, it works with any language, on any platform, on any cloud. Out of the box you get access to free hosted build agents on  Linux and Windows (personally I use exclusively Linux agents). It supports Android, iOS, Ant, Gradle, Grunt, Gulp, Maven, NPM, Xamarin and more without installing any extensions.  

If you doubt the validity of this or simply want to see how a language/tech could be supported feel free to comment below.

##### Integrations & Extensibility  
VSTS has a plethora of integrations available out of the box and even more are available through the [marketplace](http://marketplace.visualstudio.com/vsts). Here are a few highlights:

* [Github](https://marketplace.visualstudio.com/items?itemName=ms-vsts.services-github)- You can use VSTS to trigger builds from Github repositories.  
* [Docker](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker) - Execute docker commands, secure docker host management, registry credential management.
* [Apple App Store](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.app-store) & [Google Play Store](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play) - Enabling CD to the app stores.
* [Teams](https://marketplace.visualstudio.com/items?itemName=ms-vsts.vss-services-teams), [Slack](https://marketplace.visualstudio.com/items?itemName=ms-vsts.vss-services-slack), & [HipChat](https://marketplace.visualstudio.com/items?itemName=ms-vsts.services-hipchat) - For *ChatOps*.
* [PowerBI](https://www.visualstudio.com/en-us/docs/report/powerbi/connect-vso-pbi-vs) - PowerBI is an extremely powerful, easy to use, free analytics tool from Microsoft. It can reveal a variety of information based off data collected from your Project.
* [Jenkins](https://marketplace.visualstudio.com/items?itemName=ms-vsts.services-jenkins) - While I am not a huge fan of Jenkins and I certainly wouldn''t recommend it over the VSTS build system, the fact is some people love Jenkins, and many people already have a lot of Jenkins jobs. You could use this integration as a stepping stone in your migration to full blown VSTS.

If you cant find an extension for what you need it isn''t all that difficult to build one yourself. Microsoft provides 2 SDK''s:  

* [VSTS Task Lib](https://github.com/Microsoft/vsts-task-lib) - This can be used for extending the build system. Very easy to use (see my samples [here](https://github.com/beverts312/vsts-build-tasks)). Available for Node.Js and Powershell. I will post a tutorial on this soon.
* [VSS Web Extension SDK](https://github.com/Microsoft/vss-web-extension-sdk) - This allows for more advanced extensions (i.e modifying the gui).  

Currently a friend and I are working on a yeoman generator to assist with creating these (and a variety of other typescript projects). Check it out on [github](https://github.com/swellaby/generator-swell). I will do a full write up on it when we make our first release.

Plugins are available for many popular IDE''s:  

* [Eclipse](https://java.visualstudio.com/Downloads/eclipseplugin/Index)
* [IntelliJ](https://java.visualstudio.com/Downloads/intellijplugin/Index)
* [Android Studio](https://java.visualstudio.com/Downloads/androidstudioplugin/Index)
* Visual Studio
* [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team)

You can also integrate with Visual Studio Team Services via its [RESTful API](https://www.visualstudio.com/en-us/docs/integrate/api/overview) or via Client Libraries for popular programming languages.   

##### Pricing  
VSTS is very competitively priced, see the details [here](https://www.visualstudio.com/team-services/pricing/). I use VSTS extensively for my personal projects and I don''t pay anything at all. At the time of writing this is what you get for free:  

* VSTS is free for projects of 5 or less people.  
* Unlimited Private Git Repos
* 1 Private Agent Slot (unlimited minutes)*
* 1 Hosted Agent Slot (with 240 minutes/month)*
* 20,000 virtual user minutes/month for load testing

*1 slot means 1 agent running a build/release at a time, not 1 agent running at a time  

##### Code  
Here is some of my VSTS related code on Github:  

* [Build Tasks](https://github.com/beverts312/vsts-build-tasks)  
* [Build Agent Dockerfiles](https://github.com/beverts312/vsts-agent)  

##### The Future  
To see what features are currently being developed (or what has been released) you can view the [VSTS Feature Timeline](https://www.visualstudio.com/en-us/articles/news/features-timeline), easily one of my favorite places on the Internet.  

I will post some tutorials and/or more in depth looks at pieces of VSTS sometime soon! If there is anything specific you would like to see please comment below.