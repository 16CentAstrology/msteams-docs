---
title: Build Interactive Notification Bot
description: Learn to build an interactive notification bot with the help of GitHub codespaces which sends messages in Teams channel, group chat, or personal chat.
ms.localizationpriority: medium
ms.date: 02/06/2025
ms.topic: reference
---

# Build an interactive notification bot app

For an interactive notification, a bot sends messages in a Teams channel, group chat, or personal chat. You can trigger an interactive notification bot with an HTTP request, such as cards or texts. For proactive notifications from tab apps, use [activity feed notifications](/graph/teams-send-activityfeednotifications).

:::image type="content" border="false" source="../assets/images/get-started/get-started-bot.png" alt-text="Screenshot shows you the conceptual notification bot in Teams client":::

In this tutorial, learn about an interactive notification bot app in one of the following ways.

* **GitHub Codespaces**: The codespace instance allows you to experience a Teams app instantaneously. It opens Visual Studio Code (VS Code) where the Microsoft 365 Agents Toolkit (previously known as Teams Toolkit) extension, the app source code, and all the dependencies are pre-packaged for you.
* **Step-by-step guide**: Allows you to set up your development environment and build a Teams app from the start.

# [GitHub Codespaces](#tab/agentstoolkitcodespaces)

Before you create your codespace, ensure that you have the following prerequisites:

* A GitHub account to create your codespace instance
* A [Microsoft 365 account](https://developer.microsoft.com/microsoft-365/dev-program) with custom app upload permission
* A [Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md)

> [!TIP]
>
> [GitHub Codespaces](https://github.com/features/codespaces) offers a free plan with a fixed amount of usage per month. If you need to free up more space, go to [github.com/codespaces](https://github.com/codespaces) and delete the codespace that you no longer need.

To create an interactive Teams notification bot with GitHub Codespaces, follow these steps:

1. Select the following button to open GitHub Codespaces.

   <a href="https://github.com/codespaces/new?hide_repo_select=true&ref=v3&repo=348288141&machine=basicLinux32gb&location=WestUs2&devcontainer_path=.devcontainer%2Fnotification-codespaces%2Fdevcontainer.json&resume=1" target="_blank"><img src="https://github.com/codespaces/badge.svg" alt="Open hello-world tab in GitHub Codespaces"></a>

   You might be asked to sign in to GitHub account if you haven't already.

1. Select **Create new codespace**.

   :::image type="content" source="../assets/images/get-started/codespace.png" alt-text="Screenshot shows you the GitHub page to create a codespace for bot.":::

   The **Setting up your codespace** page appears.

   :::image type="content" source="../assets/images/get-started/building-codespace.png" alt-text="Screenshot shows you the codespace building your notification bot.":::

   Agents Toolkit prepares an interactive notification bot project for you and opens it in VS Code in the browser. The Microsoft 365 Agents Toolkit icon appears in the activity bar of VS Code.

1. Select **Sign in to your Microsoft 365** and **Sign in to Azure** to sign in with your Microsoft 365 account.

   :::image type="content" source="../assets/images/get-started/toolkit-in-browser-sign-in.png" alt-text="Screenshot shows you the Agents Toolkit window in browser to sign in."lightbox="../assets/images/get-started/add-tab-in-teams.png":::

    > [!NOTE]
    >
    > When you build your app, GitHub Codespaces loads it to the Teams client in a new tab. If your browser blocks pop-up tabs or windows, you need to allow pop-ups for your app to open.

1. Select **Preview your Teams App (F5)**.

      :::image type="content" source="../assets/images/get-started/toolkit-in-browser.png" alt-text="Screenshot shows you the Agents Toolkit window in browser with your notification bot."lightbox="../assets/images/get-started/toolkit-in-browser.png":::

   GitHub Codespaces builds your interactive notification bot app, loads it to Teams client, and opens it in a separate browser tab.

1. Select **Add** to install your interactive notification bot in Teams.

   :::image type="content" source="../assets/images/get-started/codespace/bot-teams.png" alt-text="Screenshot of the app details dialog to install the notification bot app in Teams.":::

   When the app is added, a dialog appears where you can select the scope to use your app.

1. Select **Open** to open the app in personal scope. 

   Alternatively, you can either search and select the required scope or select a channel, chat, or meeting from the list, and move through the dialog to select **Go**.

   :::image type="content" source="../assets/images/get-started/codespace/bot-teams-scope.png" alt-text="Screenshot of the scope selection dialog with the options to select from shared scopes.":::

1. Open a new terminal in your codespace and run the following command to trigger an event for sending an interactive notification to your bot:

   ```bash
   curl -X POST http://localhost:3978/api/notification
   ```

   > [!TIP]
   >
   > In real time, events are triggered by an external source, such as a third-party API that cause the notification bot to send the user an interactive notification. To emulate an event trigger, you can send an event manually through curl commands on terminal.

   The notification bot app sends an interactive notification as an Adaptive Card to your Teams client:

   :::image type="content" source="../assets/images/get-started/codespace/notification-bot.png" alt-text="Screenshot shows your notification bot loaded in the Teams client.":::

   You've now successfully created an interactive notification bot and loaded it in the Teams client.

 > [!div class="nextstepaction"]
 > [I ran into an issue](https://github.com/MicrosoftDocs/msteams-docs/issues/new?template=Doc-Feedback.yaml&title=%5BI+ran+into+an+issue%5D+Build+an+interactive+notification+bot+app+using+GitHub+Codespaces&&author=%40surbhigupta&pageUrl=https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fmicrosoftteams%2Fplatform%2Fget-started%2Fbuild-interactive-notification-bot%3Ftabs%3Dagentstoolkitcodespaces&contentSourceUrl=https%3A%2F%2Fgithub.com%2FMicrosoftDocs%2Fmsteams-docs%2Fblob%2Fmain%2Fmsteams-platform%2Fget-started%2Fbuild-interactive-notification-bot.md&documentVersionIndependentId=e5653869-a83d-3558-0896-b88c45816a22&platformId=eee097dd-e3f6-d51e-48d6-fc448f59cf0d&metadata=*%2BID%253A%2Be473e1f3-69f5-bcfa-bcab-54b098b59c80%2B%250A*%2BService%253A%2B%2A%2Amsteams%2A%2A)

# [Step-by-step guide](#tab/step-by-step-guide)

If you want to learn how to start a project with Agents Toolkit from the beginning, you need to set up your development environment. Select the following button to start building your interactive notification bot.

> [!div class="nextstepaction"]
> [Start building an interactive notification bot](../sbs-gs-notificationbot.yml)

---

If you want to build a message extension, go to:

> [!div class="nextstepaction"]
> [Build message extension](build-message-extension.md)

If you want to build basic tab app, go to:

> [!div class="nextstepaction"]
> [Build your basic tab app](build-basic-tab-app.md)
