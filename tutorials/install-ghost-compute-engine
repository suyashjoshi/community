---
title: How to install Ghost CMS on Google Compute Engine (free tier)
description: In this tutorial, we will learn how to setup popular Ghost blog/website engine on Google Compute Engine e2-micro VM instance on Ubuntu.
author: suyashjoshi
tags: ghost, compute engine, open source, free tier
date_published: 2022-01-23
---

Suyash Joshi | Community Developer

<p style="background-color:#D9EFFC;"><i>Contributed by the Google Cloud community. Not official Google documentation.</i></p>

To begin creating a tutorial, copy the Markdown source for this tutorial template into your blank Markdown file. Replace the explanatory text and examples with 
your own tutorial content. Not all documents will use all of the sections described in this template. For example, a conceptual document or code walkthrough
might not include the "Costs" or "Cleaning up" sections. For more information, see the 
[style guide](https://cloud.google.com/community/tutorials/styleguide) and [contribution guide](https://cloud.google.com/community/tutorials/write).

Replace the placeholders in the metadata at the top of the Markdown file with your own values. Follow the guidance provided by the placeholder values for spacing
and punctuation.

The first line after the metadata should be your name and an optional job description and organization affiliation.

After that is one of two banners that indicates whether the document was contributed by a Google employee. Just leave one banner and delete the other one.

The first paragraph or two of the tutorial should tell the reader the following:

  * Who the tutorial is for
  * What they will learn from the tutorial
  * What prerequisite knowledge they need for the tutorial

Don't use a heading like **Overview** or **Introduction**. Just get right to it.

## Objectives

* Provision Google Compute Engine instance using Free Tier so it won't cost anything as long as you don't go over the limit
* Setup OS - Ubuntu 
* Install Ghost (open source) engine and it's depdencies including MySQL Database
* Setup DNS
* Open website to test installation and access over public internet

## Before you begin

Give a numbered sequence of procedural steps that the reader must take to set up their environment before getting into the main tutorial.

Don't assume anything about the reader's environment. You can include simple installation instructions of only a few steps, but provide links to installation
instructions for anything more complex.

### Example: Before you begin

This tutorial assumes that you're using the Microsoft Windows operating system.

1.  Login to [Google Cloud Console](https://console.cloud.google.com/).
2.  Select the approprite Google Cloud project where you wish to create the compute instance for the hosting your website using Ghost
3.  Review Google Cloud [Free Tier resources](https://cloud.google.com/free/docs/gcp-free-tier/#compute

## Setup Google Compute Instance (Free Tier)

Break the tutorial body into as many sections and subsections as needed, with concise headings.

### Use short numbered lists for procedures

Use numbered lists of steps for procedures. Each action that the reader must take should be its own step. Start each step with the action, such as *Click*, 
*Run*, or *Enter*.

Keep procedures to 7 steps or less, if possible. If a procedure is longer than 7 steps, consider how it might be separated into sub-procedures, each in its
own subsection.

### Provide context, but don't overdo the screenshots

Provide context and explain what's going on.

Use screenshots only when they help the reader. Don't provide a screenshot for every step.

Help the reader to recognize what success looks like along the way. For example, describing the result of a step helps the reader to feel like they're doing
it right and helps them know things are working so far.

## Cleaning up

Tell the reader how to shut down what they built to avoid incurring further costs.

### Example: Cleaning up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, you can delete the project.

Deleting a project has the following consequences:

- If you used an existing project, you'll also delete any other work that you've done in the project.
- You can't reuse the project ID of a deleted project. If you created a custom project ID that you plan to use in the
  future, delete the resources inside the project instead. This ensures that URLs that use the project ID, such as
  an `appspot.com` URL, remain available.

To delete a project, do the following:

1.  In the Cloud Console, go to the [Projects page](https://console.cloud.google.com/iam-admin/projects).
1.  In the project list, select the project you want to delete and click **Delete**.
1.  In the dialog, type the project ID, and then click **Shut down** to delete the project.

## What's next

Tell the reader what they should read or watch next if they're interested in learning more.

### Example: What's next

- Watch this tutorial's [Google Cloud Level Up episode on YouTube](https://youtu.be/uBzp5xGSZ6o).
- Learn more about [AI on Google Cloud](https://cloud.google.com/solutions/ai/).
- Learn more about [Cloud developer tools](https://cloud.google.com/products/tools).
- Try out other Google Cloud features for yourself. Have a look at our [tutorials](https://cloud.google.com/docs/tutorials).
