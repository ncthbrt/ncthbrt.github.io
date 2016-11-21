+++
date = "2016-11-21T21:38:49+02:00"
title = "Azure Worker Roles the Hard Way"
draft = true
+++

Microsoft seems to be making a lot of right moves lately, MSSQL is available on Linux, C# seems to be gaining platform support
left, right and centre, Kestrel seems to be fast becoming a speed demon and Azure Functions entered General Availability. 
But as happy as I am with the direction the new agile Microsoft is going, it seems as though some existing products are
 being left by the wayside in their fervour to support the new shiny (a.k.a docker).

Azure Cloud Services is particularly concerning. With the dreadful "classic" monniker, no firm commitment for 
future support or a suggested migration plan, and a host of services which could approximately fulfill the same 
role (with a host of caveats), the story of low friction long running .NET services is messy.

Our new project at work would have been an ideal fit for a worker role, but I didn't want to take the risk 
of an emergency migration. So we decided to create a simulcrum of worker roles - the hard way. This is mostly 
a reference for my future self, but hopefully it'll be useful for others. This tut will walk through provisioning 
a VM, setting up security, creating install and release scripts to allow smooth continuous deployment, and how to 
create an .NET app which can hook into the windows service framework. 

The example will use AspnetCore, Topshelf, Kestrel and Akka.net to create a toy service; a Web API which calculates factorial 
numbers with horizontal scaleout, though if your app can run as a console application, the specifics shouldn't really matter.
The example uses `net462` as many libraries are not yet compatible with `netcoreapp1.0`.

