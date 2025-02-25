---
title: Boost conversations (preview)
description: Provide answers and information for your bot users, even if you haven't created a topic for their issue.
keywords: "PVA"
ms.date: 3/16/2023
ms.topic: how-to
author: iaanw
ms.author: iawilt
ms.reviewer: 
manager: leeclontz
ms.collection: virtual-agent
ms.service: power-virtual-agents
ms.search.region: USA
searchScope:
  - "Power Virtual Agents"
---



# Boost conversations (preview)

[!INCLUDE [AI tech disclosure with Bing Search](includes/disclosure-ai-preview-bing-addendum.md)]

When designing and creating a chatbot, you'll likely encounter situations where your bot users ask questions that your bot doesn't have an answer for. However, by utilizing the boosted conversations in Power Virtual Agents, your bot can find and present information from an external source - even if you haven't created a topic for it.

In the past, when a bot couldn't determine a user's intent, it asked the user to rephrase their question. If, after two prompts, the bot still couldn't determine the user's intent, the bot escalated to a live agent by using the [system **Escalate** topic](authoring-system-fallback-topic.md).

Now, before involving a live agent, the bot uses natural language processing (NLP) to:
- Parse what a user types to determine what they're asking
- Find, collate, and parse relevant information from a specified URL (for example, your company's website) with Bing Search
- Create a plain language response and then deliver that to the bot user

This means you can quickly create and deploy a functional bot, without having to first manually author multiple topics that may or may not cover all the questions your customers might end up asking.

Your workflow might be like this:

1. You create a bot and enable this capability. You test it thoroughly.

1. After testing it, you publish your bot so you can instantly provide answers, help, and guidance to your customers or bot users.

1. You create individual topics for the most important or most often-asked questions from your customers (which you might have developed based on [analytics from previous bots](analytics-overview.md) or existing support issues). This could take a while and some specialized knowledge - but with **Boost conversations** enabled you're up and running from day one.

## Prerequisites

> [!CAUTION] 
>  
> Your bot must be created in the US region. 
>  
> Other regions, and languages other than English, aren't supported during the preview.

- You'll need an account for Power Virtual Agents.

    > [!NOTE]
    >
    > If you don't have a Power Virtual Agents account, or you haven't created chatbots with Power Virtual Agents before, see the [Quickstart guide for building bots with GPT (preview)](nlu-gpt-quickstart.md).

- You must be using the [preview version of Power Virtual Agents](preview/overview.md), and the bot type must be **Preview**. Preview chatbots have **(preview)** added to their name. When you create a new bot, select **Try the unified canvas (preview)**.

    :::image type="content" source="media/nlu-gpt/nlu-boost-preview-bots.png" alt-text="Screenshot of the list of chatbots showing bots with preview added to their names.":::

- You must enable the **Boost conversations** option for each bot.

- [Review AI response generation training, model, and usage notes](#ai-response-generation-training-model-and-usage-notes) and [Learn more about Azure OpenAI](/legal/cognitive-services/openai/transparency-note).

- Your bot must be created in the US region. Other regions, and languages other than English, aren't supported during the preview.

- This capability may be subject to usage limits or capacity throttling.

## Boost your bot's reach

1. Go to the [Power Virtual Agents home page](https://web.powerva.microsoft.com/). 

1. In the side navigation menu, select **Create**. You can also select **Create a bot** on the **Home** page or **New chatbot** from the **Chatbots** page.

1. Select **Try the unified canvas (preview)**. Preview chatbots have **(preview)** added to their name in the list of bots.
    
1. Enter a name for the bot.

3. Provide a website you'd like the bot to use for generating answers, and click **Create**. See the [URL considerations](#url-considerations) section for what types of URLs you can use. 

    :::image type="content" source="media/nlu-gpt/responses-create-preview-bot.png" alt-text="Screenshot of the bot creation screen with the preview option highlighted.":::

After your bot is created and ready for you to use, it'll open to the bot's **Overview** page. From here, you can confirm that **Boost conversations** is enabled, or choose to change the URL you want to use.

You can also change the URL, disable **Boost conversations**, or change the level of content moderation in the settings for the bot:

1. With a bot open, expand **Settings** on the side navigation pane, and select **AI Capabilities**.

    1. Under **Boost conversational coverage (preview)**, use the checkbox for **Boost conversations** to enable or disable the capability.

    1. In the field under the checkbox, add or change the URL. The [same requirements apply for the URL](#url-considerations) as when enabling the capability when you create a bot.

    1. Under **Bot content moderation**, select the level you want for your bot. A higher level of moderation means that the bot’s answers will be more relevant. A lower level of moderation means that the bot will generate more answers, but the answers may be irrelevant or undesirable.

    :::image type="content" source="media/nlu-gpt/responses-enable.png" alt-text="Screenshot of the Power Virtual Agents AI capabilities page with Boost conversations enabled and highlighted.":::

1. Select **Save** at the top of the **AI capabilities** page.

You can now test your bot to see how well it responds to questions related to the content on the URL you specified.

> [!NOTE]
>  
> During the Preview of this feature you'll need to contact Microsoft Support if you want to publish a bot that has **Boost conversations** enabled.

### URL considerations

The URL you provide represents the scope of content that will be used for generating responses. 

There are some requirements on the type and structure of the URL you use:

The URL can have up to two levels of depth (or "sub-paths", indicated by forward slashes (/)). Your URL can have a trailing forward slash, and this won't be included in the limit of two slashes: 
- The URLs *<span>www</span>.contoso.com*, *<span>www</span>.fabrikam.com/engines/rotary*, or *<span>www</span>.fabrikam.com/engines/rotary/* would be valid. 
    The URL *<span>www</span>.fabrikam.com/engines/rotary/dual-shaft* would not.

If the URL you specify redirects to another top-level site, that content won't be included in results:
- If, when visited in a browser, *<span>www</span>.fabrikam.com* redirected to *<span>www</span>.contoso.fabrikam.com*, then the bot wouldn't generate responses from content on either of those URLs.  
  

The capability won't generate responses from a URL that points to a website that requires authentication or that isn't indexed by Bing:
- Wikis, SharePoint sites, and other types of websites that require authentication, for example *<span>fabrikam</span>.visualstudio.com/project/_wiki* or *<span>fabrikam</span>.sharepoint.com*, can't be used.  
  

You should also be aware of the following characteristics of the capability:
  
The bot will generate responses from any publicly viewable content under the URL you specify. This includes subdomains under a top-level domain:
- If you were to use the URL *<span>www</span>.fabrikam.com/engines/rotary*, the content on *<span>www</span>.fabrikam.com/engines/rotary/dual-shaft* would also be used by the bot to generate responses.  
Content from *<span>www</span>.fabrikam.com/tools* would not be used.  

- If you were to use *<span>www</span>.fabrikam.com*, the bot wouldn't generate responses from content on *<span>news</spam>.fabrikam.com*, as *news.* is a subdomain under the top-level domain *<span>fabrikam</span>.com*.  
 
- If you were to use *<span>fabrikam</span>.com*, then content from *<span>www</span>.fabrikam.com* and *<span>news</span>.fabrikam.com* would be used, as they sit "under" the top-level domain *<span>fabrikam</span>.com*.  

The bot may generate nonsensical, irrelevant, or inappropriate answers if you use a forum or social network site as your URL:  
- Community content on social networks can often increase the risk of more answers being rejected due to inappropriate, offensive, and malicious content that is more common on those sites.  
See the [AI response generation training, model, and usage notes](#ai-response-generation-training-model-and-usage-notes) for more information on how the AI is trained to avoid generating malicious and offensive responses.

The URL you specify should host the content you want the bot to generate answers from; it should not be the URL for a search engine:
-  Using *<span>bing</span>.com* or other search engines in the URL won't provide useful responses.  



## Test your bot's boosted conversational reach 

1. Click on **Test your bot** at the bottom of the side navigation pane. 

1. In the **Test bot** panel, ask the bot questions that take advantage of **Boost conversations** capability.

The boost conversation preview works well with a large variety of question types. However, there are certain types of questions that may produce less-helpful responses, including:

- personal questions 
- questions that require authenticated access to content
- questions for each there is no related content at the specified URL
 
You should also be aware of some of the characteristics of the AI, and how to get the most out of the questions you ask:

- The bot can have difficulty answering questions that require calculations, comparisons, or form submissions to provide answers. 
    This includes questions that use comparative and superlative terms such as better or best, latest, or cheapest. 

- The boost conversation capability doesn't remember context across multiple questions in the conversation (also known as "multi-turn questions"). 
    You should treat each question you ask the bot as part of testing this capability in isolation.

- If the bot can't generate an answer to a question, it will ask you to rephrase the question. After two of these prompts, the bot will initiate the [system **Escalate** topic](authoring-system-fallback-topic.md).

- To learn more about how the question is being interpreted by Bing against the URL you specify, add "site: \<your URL here>" to the end of your question to see the top Bing results for the question.  

- You may need to disable the [sample topics that are created automatically](authoring-template-topics.md) when you create a bot. 

> [!TIP]
>  
> You can provide feedback on how well the AI does by selecting the "thumbs up" or "thumbs down" icon underneath the generated response.
>  
> If you encounter irrelevant or inappropriate generated response, select the thumbs down icon to let us know. You can also include more verbose feedback. 
>  
> We'll use this feedback to improve the quality of the AI.



## What's supported

### Publishing

During this preview, you won't be able to publish bots that have **Boost conversations** enabled. 

If you'd like to publish a bot that has **Boost conversations** enabled, you'll need to ask your admin to enable it for your tenant in the **Power Platform admin center**. 


:::image type="content" source="media/nlu-gpt/nlu-boost-conversation.jpg" alt-text="Screenshot of the Power Virtual Agents boost conversation.":::


If your admin wants to enable it only for some environments instead of your tenant, they can start a support request. We'll review your request and get in touch with your admin.

### Quotas

Quotas are default constraints applied to chatbots that limit how often messages can be sent to the chatbot. The purpose of quotas is to throttle the client's service load, which protects a service from being overloaded and the client from unexpected resource usage. During preview, bots with "Boost conversations" enabled will have a limit on the amount of queries they can make that reach out to the URL you specified.

During the preview, bots with **Boost conversations** enabled will have a limit on the amount of queries they can make that reach out to the URL you specified. Normal conversations that use bot topics follow the [usual quotas and limitations](requirements-quotas.md#quotas)

### Pricing

During the preview, the use of the boosted conversations capability is not billable and will follow the [usual quotas and limitations](requirements-quotas.md#quotas).

## Application for the internal document search preview

The internal document search capability will allow your chatbot to return answers generated from your internal knowledge sources.

This capability is in gated preview, and you'll need to apply for consideration to the trial. You should only apply if you are willing to sign a marketing and PR agreement and if you have a use case for how you'd use this capability in a future production scenario.

To be considered for early access to trial this capability, you can apply [here](https://aka.ms/PVAGPTInterest). You can also apply by following the link on the **AI Capabilities** page.

## AI response generation training, model, and usage notes

This FAQ answers common questions about the AI that is used by the **Boost conversations** capability in Power Virtual Agents.


### Does the capability produce perfect responses?   

Responses generated by the **Boost conversations** capability are not always perfect and can contain mistakes. 

The system is designed to query knowledge from the website of your choosing and to package relevant findings into an easily consumable response. However, it's important to keep in mind some characteristics of the AI that may lead to unexpected responses:

- The corpus upon which the model has been trained doesn't include data created after 2021.  
  We have implemented mitigations to prevent the model from using its training corpus as a source for answers, however it is possible for answers to include content from websites other than the one you selected. 

- The system does not perform an accuracy check, so if the selected website contains inaccurate information this could be shown to your chatbot users. We have implemented mitigations to filter out irrelevant and offensive responses, and the feature is designed not to respond when offensive language is detected. These filters and mitigations are not foolproof.  

> [!NOTE]
> You should always test and review your bots before publishing them. During the preview, your admin will need to contact Microsoft support to enable publication.


### How was the capability evaluated? What metrics are used to measure performance?   

The capability was evaluated on a collection of manually curated question-and-answer datasets, covering multiple industries. 

Additional evaluation was performed over custom datasets for offensive and malicious prompts and responses.

## Fairness and broader impact

### Will the capability work as well using languages other than  English?

The system only supports English. Inaccurate responses may be returned when users converse with the system in languages other than English.

## Privacy

### What data does the capability collect? How is the data used?
The capability collects user prompts, the responses returned by the system, and any feedback you provide. 

We use this data to evaluate and improve the quality of the capability. More information on what data is collected is available in the [preview terms](https://go.microsoft.com/fwlink/?linkid=2189520). 

[!INCLUDE[footer-include](includes/footer-banner.md)]
