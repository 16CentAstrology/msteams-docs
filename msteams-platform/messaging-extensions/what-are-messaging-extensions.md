---
title: Message extensions
author: surbhigupta
description: Learn how to build message extensions and the scenarios where they are used. Explore samples on action and search based message extensions.
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.owner: slamba
ms.date: 01/23/2025
---
# Build message extensions

Message extensions enable users to engage with your web service through buttons and forms within the Microsoft Teams client. Users can search or initiate actions in an external system from the compose message area, the command box, or directly from a message. The results of these interactions can be returned to the Teams client as a richly formatted card.

> [!IMPORTANT]
> Message extensions are available in [Government Community Cloud (GCC), GCC High, Department of Defense (DoD)](../concepts/cloud-overview.md#teams-app-capabilities), and [Teams operated by 21Vianet](../concepts/sovereign-cloud.md) environments.

The article provides an overview of message extensions, use cases, functionality, action and search commands, and link unfurling.

The following image displays the locations from where message extensions can be invoked:

> [!NOTE]
>
> * @mentioning message extensions in the compose box isn't supported.
> * Message extension options aren't supported for group chats with external users.

# [Desktop](#tab/desktop)

:::image type="content" source="../assets/images/messaging-extension-invoke-locations.png" alt-text="Screenshot shows the message extensions invoke location on Teams desktop.":::

# [Mobile](#tab/mobile)

:::image type="content" source="../assets/images/messaging-extension-invoke-location-mobile.png" alt-text="Screenshot shows the message extensions invoke location on Teams mobile.":::

---

## Scenarios where message extensions are used

| Scenario | Example |
|:-----------------|:-----------------|
|You need an external system to perform an action and return the result to your conversation.|Reserve a resource and allow the channel to know the reserved time slot.|
|You need to search for something in an external system and share the results with the conversation.|Search for a work item in Azure DevOps and share it with the group as an Adaptive Card.|
|You want to complete a complex task involving multiple steps or large amounts of information in an external system and share the results with a conversation.|Create a bug in your tracking system based on a Teams message, assign that bug, and send a card to the conversation thread with the bug's details.|

## Understand how message extensions work

A message extension is composed of a web service hosted by you and an app manifest that defines the location where your web service is invoked within the Teams client. The web service utilizes the Bot Framework's messaging schema and secure communication protocol, so you must register your web service as a bot in the Bot Framework.

> [!NOTE]
> Though it's possible to manually create the web service, we recommend to use [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) to work with the protocol.

In the app manifest (previously called as Teams app manifest), a single message extension is defined with up to 10 different commands. Each command defines a type, such as action or search and the locations in the client from where the message extension is invoked. The invoke locations include the compose message area, command bar, and message. On invoke, the web service receives an HTTPS message with a JSON payload with all the relevant information. Respond with a JSON payload to inform the Teams client of the next interaction to enable.

## Message extension commands types

There are two types of message extension commands, action command and search command. The message extension command type defines the UI elements and interaction flows available to your web service. Certain interactions, such as authentication and configuration, are available for both commands types.

### Action commands

Action commands are used to present the users with a modal pop-up to collect or display information. When the user submits the form, your web service responds by inserting a message into the conversation directly or into the compose message area. Later, the user can submit the message. For more complex workflows, you can link multiple forms together.

Action commands are triggered from the compose message area, the command box, or a message. When the command is invoked from a message, the initial JSON payload sent to your bot includes the entire message from which it was invoked. The following image displays the message extension action command dialog (referred as task module in TeamsJS v1.x):

:::image type="content" source="../assets/images/task-module.png" alt-text="Message extension action command dialog":::

### Search commands

Search commands allow the users to search an external system for information. To use search commands, enter a query manually into the search box or insert a link to a monitored domain in the compose message area, then embed the search results into a message. In a simple search command flow, the initial invoke message includes the search string submitted by the user. You respond with a list of cards and card previews. The Teams client renders a list of card previews for the user. When the user selects a card from the list, the full-size card is inserted into the compose message area.

The cards are triggered from the compose message area or the command box, but not from a message. They can't be triggered from a message.
The following image displays the message extension search command dialog:

:::image type="content" source="../assets/images/search-extension.png" alt-text="Message extension search command":::

> [!NOTE]
> For more information on cards, see [what are cards](../task-modules-and-cards/what-are-cards.md).

## Link unfurling

> [!NOTE]
> Link unfurling is supported only for bot-based message extensions.

When a URL is pasted in the compose message area, a web service is invoked. This functionality is known as link unfurling. You can subscribe to receive an invoke message when URLs containing a specific domain are pasted into the compose message area. Your web service can **unfurl** the URL into a detailed card, providing more information than the standard website preview card. You can add buttons to allow the users to immediately take action without leaving the Teams client.
The following images display link unfurling feature when a link is pasted in a message extension:

:::image type="content" source="../assets/images/messaging-extension/unfurl-link.png" alt-text="unfurl link":::

![link unfurling](../assets/images/messaging-extension/link-unfurl.gif)

## Build message extensions

To build a message extension, if you don't already have one, there are two ways:

* **Build message extensions using API (API-based)**: You can easily create a message extension from an existing API. An OpenAPI Description (OAD) document is required for this method.

* **Build message extensions using Bot Framework (Bot-based)**: If you want a one-on-one conversational experience, you can create a new message extension from a bot.

The following table helps you select a message extension type to get started:

:::row:::
    :::column:::
**API-based message extension**</br>

* Simpler and faster to create and maintain.
* Message extension uses an API.
* No extra code or resource is required for bot logic.
* Ideal for scenarios where the message extension only needs to communicate with a web service and doesn't need any complex logic or state management.
* Traffic is privatized as they don’t depend on Azure bot infrastructure.
* Supports search commands.

    :::column-end:::
    :::column:::

**Bot-based message extension**</br>

* More flexible.
* Message extension uses a Bot Framework.
* Can use the full capabilities of a bot.
* Ideal for scenarios where the message extension needs to communicate with multiple services, manage complex logic or user interactions, or maintain state across sessions.
* Supports action commands, search commands, and link unfurling.

    :::column-end:::
:::row-end:::

</br>

:::image type="content" source="../assets/images/Copilot/api-bot-based-message-extension-decision-tree.png" alt-text="Screenshot shows the decision tree, which helps the user to choose between API based and bot based message extension.":::

**Select an option to start building a message extension:**

:::row:::
    :::column span="4":::
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; :::image type="content" source="../assets/images/Copilot/build-message-extension-api-tile.png" alt-text="Screenshot shows the OpenAPI icon tile." link="api-based-overview.md" border="false":::
    :::column-end:::
    :::column span="4":::
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:::image type="content" source="../assets/images/Copilot/build-message-extension-bot-tile.png" alt-text="Screenshot shows the Bot Framework tile." link="build-bot-based-message-extension.md" border="false":::
    :::column-end:::
:::row-end:::

## Code sample

| **Sample name** | **Description** | **.NET** | **Node.js** | **Python** | **Manifest**|
|------------|-------------|----------------|------------|------------|------------|
| Message extension with action-based commands | This sample demonstrates how to create Action-Based Message Extensions for Microsoft Teams, enabling users to interactively generate content. It features bots, message extensions, and seamless integration with user inputs for enhanced functionality. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action/nodejs) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action/python) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action/csharp/demo-manifest/msgext-action.zip)
| Message extension with search-based commands | This sample demonstrates how to create a Message Extension in Microsoft Teams that allows users to perform searches and retrieve results. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-search/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-search/nodejs) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-search/python) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-search/csharp/demo-manifest/msgext-search.zip)
|Message extension action preview| This sample app illustrates how to utilize action previews in Teams Message Extensions, allowing users to create cards from input in a Task Module. It showcases bot interactions that enhance user engagement by attributing messages to users. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action-preview/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action-preview/nodejs) |NA|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-action-preview/csharp/demo-manifest/msgext-action-preview.zip) |
|Message extension action for task scheduling|This sample demonstrates a Message Extension that allows users to schedule tasks and receive reminder cards in Microsoft Teams.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)| NA |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp/demo-manifest/msgext-message-reminder.zip)|
| Northwind inventory message extension| This sample implements a Teams message extension that can be used as a plugin for Microsoft 365 Copilot. The message extension allows users to query the Northwind Database. | NA |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-copilot-handoff/ts) |NA |NA
