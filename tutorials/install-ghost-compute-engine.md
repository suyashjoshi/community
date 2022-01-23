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

1.  Review Google Cloud [Free Tier resources](https://cloud.google.com/free/docs/gcp-free-tier/#compute
2.  Login to [Google Cloud Console](https://console.cloud.google.com/).
3.  Select the approprite Google Cloud project where you wish to create the compute instance for the hosting your website using Ghost


### Provision Compute Instance

1. Navigate to [Google Cloud Compute Engine webpage](https://console.cloud.google.com/compute/instances)
2. Click 'Create Instance'
3. Give it a meaningful name like 'my-website-ghost-ubuntu"
4. Select one of the Free Tier Region (Oregon: us-west1, Iowa: us-central1, South Carolina: us-east1) and default zone for the same.
5. Machine Configuration : Series must be *E2* and Machine Type must be *e2-micro(2 vCPU, 1 GB memory). Change Boot Disk Settings to *Ubuntu* Version *Ubuntu 20.04 LTS* for Operating System with *Balance persistent disk* Boot Disk type at *30 GB* storage which is part of free tier.
6. Firewall : Check to allow both *HTTP Traffic* and *HTTPS Traffic*
7. Network Interface : Create a Network Interface for this VM and the leave all settings as default.
8. Finally click 'Create' button and in few moments your Compute Instance should be available.

### Configure Nework

1. Click on the Hamburger looking menu on the left side to open the navigation window.
2. Navigate to Networking > VPC network > External IP addresses -> Click on "Reserver a Static Address" button
3. Enter a name for your static IP adddress setting, Change *Networking service tier* to 'Standard', *Region* to 'us-west1(Oregon) and *Attached to* your compute instance that you created in previous step. Click 'Reserve' to confirm. 
4. After confirmation, you should see new static IP assed to your compute instance, here take note of the *External IP Address*, we will use it later to open the Ghost website.

## Configuring Ubuntu and Ghost

Finally it's time to login to the virtual machine and set it up so we can install and run Ghost. Follow the steps below and in no time you will have Ghost running securely. During install, the CLI will ask a number of questions to configure, just follow the steps in the wizards and prompts accordindly.

1. Navigate to your project in the Compute Instance Portal
2. Click the 'drop down' icon next to *SSH* and chose 'Open in browser window', this is the easier and quickest way to SSH inside the VM.
3. Verify Ubuntu Version by typing `lsb_release -a` and you should see Ubuntu 20.04.3 LTS in the 'Description' as the OS version
4. It's always good to create an admin user with super user privilage so let's do that and switch to this new user. Follow the commands and wizard to do the same:

```
sudo adduser <username>
sudo usermod -aG sudo <username>
su - <username>
```

4. Let us also update Ubuntu packages by runing `sudo apt-get update` followed by `sudo apt-get upgrade`
5. Now we will install the key packages we need for Ghost so do the same by running the following commands:

```
# Ghost uses an NGINX server so let's install that and open firewall for the same to allow web traffic over HTTP & HTTPS
sudo apt-get install nginx
sudo ufw allow 'Nginx Full'

# Install MySQL as Database for Ghost & Set password for MySQL 'Root' User. Leave the quotes, just change the password to a something else
sudo apt-get install mysql-server
# Now update your user with this command. Replace 'password' with your password, but keep the quote marks!
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
# Then exit MySQL
quit

# Add the NodeSource APT repository for Node 14
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash
# Install Node.js
sudo apt-get install -y nodejs

# Install & Verfiy Ghost CLI
sudo npm install ghost-cli@latest -g
ghost help



# Ghost must be installed in a directory so let's create one. Change `sitename` to whatever you like such as your website name
sudo mkdir -p /var/www/sitename
# Set directory owner: Replace <user> with the name of your user
sudo chown <username>:<username> /var/www/sitename
# Set the correct permissions
sudo chmod 775 /var/www/sitename
# Then navigate into it
cd /var/www/sitename

## Install Ghost via the Ghost CLI
ghost install
```

### Ghost Install Steps and other important information

**Blog URL**
Enter the exact URL your publication will be available at and include the protocol for HTTP or HTTPS. For example, https://example.com. If you use HTTPS, Ghost-CLI will offer to set up SSL for you. Using IP addresses will cause errors.

**MySQL hostname**
This determines where your MySQL database can be accessed from. When MySQL is installed on the same server, use localhost (press Enter to use the default value). If MySQL is installed on another server, enter the name manually.

**MySQL username / password**
If you already have an existing MySQL database, enter the the username. Otherwise, enter root. Then supply the password for your user.

**Ghost database name**
Enter the name of your database. It will be automatically set up for you, unless you’re using a non-root MySQL user/pass. In that case the database must already exist and have the correct permissions.

**Set up a ghost MySQL user? (Recommended)**
If you provided your root MySQL user, Ghost-CLI can create a custom MySQL user that can only access/edit your new Ghost database and nothing else.

**Set up NGINX? (Recommended)**
Sets NGINX up automatically enabling your site to be viewed by the outside world. Setting up NGINX manually is possible, but why would you choose a hard life?

**Set up SSL? (Recommended)**
If you used an https Blog URL and have already pointed your domain to the right place, Ghost-CLI can automatically set up SSL for you using Let’s Encrypt. Alternatively you do this later by running ghost setup ssl at any time.

**Enter your email**
SSL certification setup requires an email address so that you can be kept informed if there is any issue with your certificate, including during renewal.

**Set up systemd? (Recommended)**
systemd is the recommended process manager tool to keep Ghost running smoothly. We recommend choosing yes but it’s possible to set up your own process management.

**Start Ghost?**
Choosing yes runs Ghost, and makes your site work.

**Ghost maintenance**
Once Ghost is properly set up it’s important to keep it properly maintained and up to date. Fortunately, this is relatively easy to do using Ghost-CLI. Run ghost help for a list of available commands, or explore the full Ghost-CLI documentation.

**What to do if the install fails**
If an install goes horribly wrong, use ghost uninstall to remove it and try again. This is preferable to deleting the folder to ensure no artifacts are left behind.
If an install is interrupted or the connection lost, use ghost setup to restart the configuration process.
For troubleshooting and errors, use the site search and FAQ section to find information about common error messages.

### Hello World blog powered by Ghost!

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
