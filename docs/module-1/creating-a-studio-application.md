---
title: Creating a Studio application
description: A course module where we will create a simple SPREAD Studio application.
comments: true
hide:
     - toc
---

To display data, we will be working in SPREAD Studio - which is a tool to create applications that build on your product knowledge. From the SPREAD Platform Launcher page, select the **Studio** tile. You can also use the [direct link](<<https://studio.{{> snippets.tenantURL }}) for your SPREAD instance.

{{ snippets.tile }}

## Navigating Studio

First, let's get familiar with the layout of the Studio application.

{{ studio.navigatingStudio }}

<figure markdown="span">
	![Navigating the SPREAD Studio canvas]({{ config.site_url }}platform-tools/using-studio/src/navigating-spread-studio-canvas.png)
	<figcaption>Navigating the SPREAD Studio canvas</figcaption>
</figure>
{{ studio.creatingApplications }}

## Create a user interface

{{ studio.buildUI }}

??? exercise "Task 1: Create a UI"

     Create a simple user interface with just an [input box](#) and a [submit button](#).

## Configure the settings

{{ studio.configureAppSettings }}

<figure markdown="span">
	![Styling your Studio application]({{ config.site_url }}platform-tools/using-studio/src/styling-studio-applications.png)
	<figcaption>Styling your Studio application</figcaption>
</figure>

{{ studio.configureAppTheme }}

??? exercise "Task 2: Configure your application"

     1. Set the name of your application to "Acme Inc widgerator"
     2. Set the app logo to this image
     3. Change the primary color to `#ff450e`.

## Publish the application

{{ studio.publishApp }}

??? exercise "Task 3: Publish your application"

     Publish the application that you have created and then open it.