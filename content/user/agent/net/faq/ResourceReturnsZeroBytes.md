<!--
title: "A Particular Resource Returns 0 Bytes Under Contrast.NET"
description: "Troubleshooting guide for .NET agent issues"
tags: "zero bytes agent installation .Net"
-->


## Symptoms

* A particular resource (page, image, etc.) works normally when the Contrast.NET agent is not running and stops working once the agent is running
* When using browser developer tools or something similar to view network traffic, the resource returns **0 bytes** while the Contrast.NET agent is running

## How To Solve

Contrast.NET uses a filter within a ```System.Web.IHttpModule``` to gather HTTP response data. There is a known Microsoft bug in the .NET framework: ```HttpModules``` with filters can cause resources such as ***WebResource.axd*** to return **0 bytes** (which can result in 500 status responses for embedded resources such as images).

* *Configure Contrast.NET* using the ```ResponseUrlWhitelistRegex``` settings to prevent Contrast from applying the ```HttpModules``` filter to the resource.
* Or, disable collection and analysis of HTTP response bodies by disabling full-content-analysis  (```<full-content-analysis enabled="false">```) in ```%ProgramData%\Contrast.NET\customerPolicy.xml```.

## See Also

[Getting .NET Agent Logs](user_netinstall.html#logs)

[.NET Agent Configuration](user_netconfig.html#config)

[.NET Response-based Rules](user_netrules.html#response)

