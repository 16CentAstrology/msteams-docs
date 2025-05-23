---
title: Explore Agents Toolkit UI & Features
author: zyxiaoyuer
description: Learn about Microsoft 365 Agents Toolkit UI in VS, and functions such as app dependencies, manifest update, and authentication code to build and develop your app.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
---
# Explore Microsoft 365 Agents Toolkit in Visual Studio

In this article, explore Microsoft 365 Agents Toolkit (previously known as Teams Toolkit) and its features in Microsoft Visual Studio. Agents Toolkit appears as a workload in the app you've created in Visual Studio. For more information, see [How to create a Microsoft Teams app](create-new-project-vs.md).

You can view Agents Toolkit in Visual studio in the following ways:

* Project
* Solution Explorer

# [Project](#tab/prj)

To view Agents Toolkit from the **Project** menu, follow these steps:

1. Select **Project**.
1. Select **Microsoft 365 Agents Toolkit**.

   :::image type="content" source="../../assets/images/toolkit-v2/toolkit-vs/toolkit-installed.png" alt-text="Screenshot shows the Agents toolkit project menu.":::

# [Solution Explorer](#tab/solutionexplorer)

   To view Agents Toolkit under **Solution Explorer**, follow these steps:

1. Select **View** > **Solution Explorer** to view **Solution Explorer** panel.
1. Right-click on your app project name.
1. Select **Microsoft 365 Agents Toolkit**.

   > [!NOTE]
   > In this scenario the project name is **MyTeamsApp14**.

   :::image type="content" source="../../assets/images/toolkit-v2/toolkit-vs/toolkit-solution explorer.png" alt-text="Screenshots the Agents toolkit operations from Project":::
  
---

After you've created your Teams app project, you can use the following options to develop and build your app:

:::image type="content" source="../../assets/images/toolkit-v2/toolkit-vs/toolkit-solution explorer-options.png" alt-text="Agents toolkit operations from Project menu":::

|Function  |Description  |
|---------|---------|
|**Select Microsoft 365 Account** |Before you debug locally, ensure that you prepare your app for dependencies. This option helps you to set up the local debug dependencies and register Teams app in the Teams platform. You must have a Microsoft 365 account. For more information, see [how to debug your Teams app locally using Visual Studio](debug-local-vs.md).         |
|**Update Manifest in Teams Developer Portal** | Helps you to update the app manifest (previously called Teams app manifest) file. When you update the app manifest file, only then you can redeploy the app manifest file to Azure without deploying the whole project again. Use this command to update your changes to remote. For more information, see [how to edit app manifest using Visual Studio](TeamsFx-preview-and-customize-app-manifest-vs.md).       |
|**Add Authentication Code** | Helps you obtain signed-in Teams user token to access Microsoft Graph and other APIs. Agents Toolkit facilitates the interaction by abstracting from the Microsoft Entra ID, which flows and integrates with simple APIs. For more information, see [how to add single sign-on to Teams app](add-single-sign-on-vs.md).        |
|**Provision in the Cloud** | Helps you to create Azure resources that host your Teams app. For more information, see [how to provision cloud resources using Visual Studio](provision-vs.md).        |
|**Deploy to the Cloud** | Helps you to copy your code to the cloud resources that you provisioned in Microsoft Entra ID. For more information, see [how to deploy Teams app to the cloud using Visual Studio](deploy-vs.md).        |
|**Preview in** | Launches the Teams web client, Outlook and the Microsoft 365 app lets you preview the Teams app in your browser.         |
|**Zip App Package** | Generates a Teams app package in the **Build** folder under the project. You can upload the app package to the Teams client and run the Teams app.         |
|**Microsoft 365 Agents Toolkit Documentation** | Launches a web page to view Agents Toolkit documentation.         |

## See also

* [Microsoft 365 Agents Toolkit Overview](agents-toolkit-fundamentals-vs.md)
* [Create a new Teams app using Agents Toolkit](create-new-project-vs.md)
* [App manifest schema](~/resources/schema/manifest-schema.md)
* [Prepare to build apps using Agents Toolkit](build-environments-vs.md)
