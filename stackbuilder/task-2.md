---
title: Task 2
sidebar_position: 2 
---


## Overview

StackSync AI Connector is a new feature in a StackGen platform that keeps your infrastructure architecture and code definitions in sync automatically. When you make changes to your infrastructure in the appStack section, StackSync AI Connector automatically pushes those changes to your code files, keeping everything up to date.

### How Does StackSync AI Connector Work?

StackSync AI Connector keeps your appStack and IaC (Infrastructure as Code) state in sync by automating configuration synchronization:

1. **Automatic Synchronization**: When you modify your appStack configuration, StackSync detects changes and attempts to sync them to IaC state  
2. **Conditional Syncing**: Certain conditions must be met for synchronization to occur.  
3. **Asynchronous Webhook Trigger**: In the background, it  processes the synchronization without blocking your work.  
4. **Consistency Across Tools**: It keeps your infrastructure design (appStack) and your IaC state files (.tfstate) aligned.  
5. **Error Visibility**: Error message pop-up, stating clear messages when validation fails, and indicate what needs to be fixed.

## Set Up and Usage

Let’s see in detail how you can enable the **StackSync AI Connector** to synchronize any configuration changes.

###  Prerequisites

Before you start make sure:

1. You have access to StackGen platform to manage appStacks. You can also refer to [this section](https://docs.stackgen.com/docs/quickstart/appstacks).  
2. You have an [appStack](https://docs.stackgen.com/docs/concepts/appstacks/) created in StackGen (from any creation method: [scratch](https://docs.stackgen.com/docs/concepts/appstacks/createappstacks/fromscratch), [migrating IaC](https://docs.stackgen.com/docs/concepts/appstacks/createappstacks/migrateiac), [deployment files](https://docs.stackgen.com/docs/concepts/appstacks/createappstacks/fromdeploymentfiles), or [Cloud2Code](https://docs.stackgen.com/docs/cli-guide/cloud2code/) import)  
3. Your appStack is accessible in [StackBuilder](https://docs.stackgen.com/docs/stackbuilder/)  
4. Your metadata.json file includes both required fields: ai\_index and clusters

### Enabling **StackSync AI Connector**

To enable the StackSync AI Connector follow these steps:

1. Log in to StackGen, go to the **appStack** section on the homepage, and search for the appStack you [created using Cloud Discovery](https://docs.stackgen.com/docs/concepts/appstacks/createappstacks/fromdiscovery) from the search bar. Alternatively, click on [Assist me](https://docs.stackgen.com/docs/stackbuilder/#navigating-to-the-stackbuilder) and locate your appStack using StackBuilder.  
   ![](./images/image1.png)
2. Now, open your appStack to view the Topology Canvas. The [Topology Canvas](https://docs.stackgen.com/docs/concepts/topology/) in StackGen is a visual design tool for creating, managing, and validating cloud infrastructure.   
3. You'll see all the resources discovered from your .tfstate file visualized in the Topology Canvas  
   ![](./images/image2.png)
4. At the top-right  corner, you will see the **Run AI** **Sync** toggle button. It appears disabled by default,  It becomes active once configuration is initiated. Toggle it **ON** to enable synchronization.  
5. Now, you can add, edit, or remove resources, configure properties, and define dependencies to align with application requirements.

:::note
You cannot remove resources that were added during the base appStack creation, but you can modify their configurations.
:::  
	  ![](./images/image3.png)

6. StackSync requires metadata validation before syncing. Before syncing, make sure your configuration file (metadata.json) has these two pieces of information:  
   ```  
   {  
     ai_index: true,  
     clusters: ["production"],  
     version: "1.0"  
   }  
   ```  
7. After you've made your changes, click the "Run AI Sync" button (it might have been called "Sync Now" in older versions)  
8. StackSync automatically detects configuration changes, validates the metadata.json file, triggers an async webhook to sync with the IaC state, updates the definitions if all conditions are met, and reports the sync status.

