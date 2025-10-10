---
title: Best practices for building agent in Teams user experience
description: Learn about the user experience for agents in Teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.date: 09/27/2024
---

# Agents user experience

[!INCLUDE [teams-ai-lib-v2-rec](../../../includes/teams-ai-lib-v2-rec.md)]

An agent transforms system interactions. For developers, creating an exceptional user experience is crucial. This article details the steps, principles, and considerations for designing intuitive, user-centered interfaces that seamlessly integrate AI capabilities. The main goals are to simplify complex tasks, enhance productivity, and offer personalized experiences through adaptive learning. An agent includes features that enhance its functionality and integration within the Teams environment:
<!--the Microsoft ecosystem-->

- **Generative AI integration**: Uses advanced AI models for natural language processing and interaction.
<!--
- **Bots**: Allows building or extending bots with LLM and generative AI for high-quality chat experiences.-->
- **Customizable orchestration**: Provides extensive customization options for tailoring the agent's behavior and responses to specific use cases.

To achieve this, you must follow mandatory requirements and best practices. For more information, see [validation guidelines for agents](../../../concepts/deploy-and-publish/appsource/prepare/review-copilot-validation-guidelines.md).

## Ensure mandatory requirements for an agent in Teams

The following requirements are mandatory for building the agent UX:

- [Update the app manifest an agent](#update-the-app-manifest-an-agent)
- [Stream the agent response to the user](#stream-the-agent-response-to-the-user)
- [Ensure the agent response contains citations](#ensure-the-agent-response-contains-citations)
- [Ensure the agent response contains an AI label](#ensure-the-agent-response-contains-an-ai-label)
- [Ensure that the agent maintains intelligent conversation](#ensure-that-the-agent-maintains-intelligent-conversation)
- [Ensure that the agent offers prompt starters or a welcome card](#ensure-that-the-agent-offers-prompt-starters-or-a-welcome-card)

<!--
> [!NOTE]
>
> - AI label, citation, feedback buttons, and sensitivity label are available for bots in personal chats, group chats, and channels.
-->

### Update the app manifest an agent

You must update the app manifest for the agent to define specific properties and configurations that characterize its capabilities and behavior.

Here's an example for updating the app manifest. You must add the `botID` property to the `copilotAgents` node in the app manifest.

<details>
<summary>App manifest update example:</summary>

```json
    "bots": [
        { 
          "botId": "00001111-aaaa-2222-bbbb-3333cccc4444", 
          // ... existing bot node fields
        } 
      ],
      "copilotAgents": {
        "customEngineAgents": [{ // New 
          "type": "bot", // Only option 
          "id": "00001111-aaaa-2222-bbbb-3333cccc4444"  // Validated against bots node 
        }] 
      },

```

</details>

### Stream the agent response to the user

An agent uses LLM for complex user requests, which may delay responses. To prevent noticeable delays, the agent streams its responses, making them appear fast.

:::image type="content" source="../../../assets/images/bots/ai-streaming-ux.gif" alt-text="Graphical representation shows streaming agent messages" border="false":::

Use the following types of updates while streaming responses:

- Informative updates: Send information on the sub-steps as the agent generates the response before it sends the final response.
- Response streaming: Send the intermediate states of the final response while the LLM creates its full response.

<!--
You can use one of the following to stream the response:

- Use Teams AI library to add streaming to the agent.
- Call the Bot Framework APIs directly for streaming.
-->

Use [Teams AI library](/microsoftteams/platform/teams-ai-library/) to add streaming to the agent.

>[!NOTE]
>
> Streaming bot messages is available only for one-on-one chats and in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md).

### Ensure the agent response contains citations

Users must know the sources an agent uses to generate its final response. Identifying these resources allows users to validate and trust the agent's responses.

:::image type="content" source="../../../assets/images/bots/ai-citation.png" alt-text="Image shows an example of citations in agents." border="false":::

<!--
You can use one of the following to include citations for the resources used by the agent:

- Use Teams AI library citations module.
- Incorporate citations into the Bot Framework API calls.
-->

Use [Teams AI library](/microsoftteams/platform/teams-ai-library/) to add streaming to the agent.

> [!NOTE]
>
> - Citations with Adaptive Cards are available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md).

### Ensure the agent response contains an AI label

An agent must identify that it uses AI. Informing users that a response is AI-generated helps build trust in the agent's capabilities. To ensure this, an agent must include a flag in each AI-generated response to indicate it was generated by AI. This flag automatically adds an AI label next to the response.

Examples of AI label:

- Example of AI-generated label:

    :::image type="content" source="../../../assets/images/bots/ai-labels-1.png" alt-text="Image shows an example of AI label for AI-generated message." border="false":::

- Example of sensitivity label:

    :::image type="content" source="../../../assets/images/bots/ai-labels-2.png" alt-text="Image shows an example of AI label for a confidential message." border="false":::

<!--
You can use one of the following to include AI label in the agent's response:

- Use Teams AI library to add the AI label to all AI-generated messages automatically.
- Set the flag in the Bot Framework API for message activities.
-->

Use [Teams AI library](/microsoftteams/platform/teams-ai-library/) to add streaming to the agent.

### Ensure that the agent maintains intelligent conversation

An agent must track a conversation's context and history to provide an intelligent interaction. The agent must meet the user's expectation by being aware of the conversation's context and allowing them to refer to previous messages and responses.

Use Teams AI library to ensure intelligent context-based conversation and to manage and pass conversational history and context to the LLM. Teams AI library enables you to:

<!--
- Use Bot Framework SDK to:
-->
- **Manage context and conversation history**: Ensure that the agent can track the context and conversation history.
- **Identify conversation location**: Ensure the agent is aware of the platform on which the conversation is ongoing, such as on Teams, copilot.com, in a meeting side panel, or a group chat.
- **Store and pass conversation history**: Determine the means of storage and pass some of the conversation history to the agent.
- **Understand user references**: Ensure that when a user sends a message, the agent must understand what the user is referring to. You can build this understanding in the agent using LLM and the recent conversation history. The agent mustn't need the user to reestablish context with every message.

### Ensure that the agent offers prompt starters or a welcome card

An agent must assist users by offering prompt suggestions on how to best utilize the agent. This helps users overcome challenges during both initial and subsequent interactions with the agent.

:::image type="content" source="../../../assets/images/bots/ai-zero-prompts.png" alt-text="Image shows an example of prompt starters." border="false":::

- **Prompt starters**: Prompt starters are the initial prompts users see when an agent is added to a new conversation, whether it's a one-on-one chat, a new session, or a group chat. These prompts must be tailored to the user's context and the specific conversation thread.
- **Contextual prompts**: Contextual prompts are dynamic recommendations from an agent during user interactions. These prompts appear via contextual flyouts, such as **View Prompts** in one-on-one chats and @mention flyouts in group chats. These suggestions are updated to stay relevant to the ongoing conversation.
- **Suggested action**: Suggested actions are prompts that appear as pills above the compose box in one-on-one chats and as action buttons in group chats. They are suggestions for actions a user might take in response to the agent's message and must be customized to match the response.

<!--
## Compound utterance guidelines for agents

Agents must support at least three unique compound utterances by handling three or more parameters. Guidelines for agents provide detailed information on [parameter description](../../../messaging-extensions/dev-guidelines-agents.md#parameter-description) and ways to [enhance message extension to retrieve information through compound utterances](../../../messaging-extensions/dev-guidelines-agents.md#enhance-message-extension-to-retrieve-information-through-compound-utterances).

:::image type="content" source="../../../assets/images/Copilot/high-quaity-me-pass-multi-parameters.png" alt-text="Screenshot shows an example of a pass scenario where the Northwind app returns a response for a seafood and in stock parameters.":::
-->

## Best practices for agents in Teams

The following best practices can help enhance the overall effectiveness of an agent:

- [Ensure that agent's response contains feedback button](#ensure-that-agents-response-contains-feedback-button).
- [Enable Teams Azure AD single sign-on](#enable-teams-azure-ad-single-sign-on).
- [Enable the agent to understand conversational history and context](#enable-the-agent-to-understand-conversational-history-and-context)
- [Offer dynamic and contextual suggestion prompts](#offer-dynamic-and-contextual-suggestion-prompts).

### Ensure that agent's response contains feedback button

Develop the capability in the agent to receive user feedback. This could enable the collection of valuable insights from users, which can be analyzed to identify areas for improvement. By incorporating this feedback, the bot's responses can be continuously refined and enhanced, leading to a more effective and user-friendly interaction experience.

:::image type="content" source="../../../assets/images/bots/ai-feedback-loop.png" alt-text="Image shows an example of feedback loop." border="false":::

To collect the user feedback, you must:

- Provide feedback buttons with every response.
- Provide the feedback received from the user to the agent.
- Use the feedback to improve the quality of agent's responses.

<!--
You can use one of the following to enable feedback collection and usage:

- Use Teams AI library to add the feedback button property to the AI module. This property adds a feedback button to each AI-generated message automatically.
- Use the feedback flag in the Bot Framework API to add the feedback button for each message.
-->

Use Teams AI library to add the feedback button property to the AI module. This property adds a feedback button to each AI-generated message automatically.

> [!NOTE]
> Customizable feedback forms are available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md).

### Enable Teams Azure AD single sign-on

You can add single sign-on (SSO) authentication to your agent. For more information, see [enable SSO for your app](../authentication/bot-sso-overview.md).

### Enable the agent to understand conversational history and context

You can design your agent to understand and refer to conversational history and context. It helps to ensure that every interaction is relevant and tailored to the user's specific needs. The agent can refer to the context and offer responses that are accurate and contextually appropriate.

<!--For more information, see [messages in bot conversations](../conversations/conversation-messages.md).-->

### Offer dynamic and contextual suggestion prompts

Enhance your agent's user experience with intelligent and context-aware prompts. The agent can offer context-relevant prompts dynamically.

:::image type="content" source="../../../assets/images/bots/ai-suggested-prompts.png" alt-text="Image shows an example of suggested prompts." border="false":::

To achieve this, the agent must leverage the conversation context and history, and prompt suggestions can be timely and fit for the query.

## See also

- [Teams AI library](teams-conversation-ai-overview.md)
- [Stream bot messages](../../streaming-ux.md)
- [Enhance AI-generated bot messages](../bot-messages-ai-generated-content.md)
