# What is Dialogflow ?


> Dialogflow (formerly known as api.ai) is a Google-owned developer of human-computer interaction technologies based on natural language conversations. The company is best known for creating the Assistant, a virtual assistant for Android. Dialogflow has many built-in integrations. Users can simply integrate their chatbot with website, messenger, slack and more with just a few clicks.

## Overview

Dialogflow lets you build conversational interfaces on top of your products and services by providing a powerful natural language understanding (NLU) engine to process and understand natural language input. This document goes over how Dialogflow works and how it can help you create conversational user interfaces that delight users.

Traditional computer interfaces require structured and predictable input to function properly, which makes the use of these interfaces unnatural and sometimes difficult. If users can't easily figure out this structured input, they'll have a hard time figuring out what to do.

For example, consider an easy user request like "What's the forecast like today?". Other users might also ask:

- "What's the weather like right now?"
- "What's the temperature like in San Francisco tomorrow?"
- "What will the weather be like on the 21st?"

Even with this simple question, you can see that conversational experiences are hard to implement. Interpreting and processing natural language requires a very robust language parser that's capable of understanding the nuances of language.

Your code would have to handle all these different types of requests (and potentially many more) to carry out the same logic: looking up some forecast information for a time and location. For this reason, a traditional computer interface would tend to force users to input a well-known, standard request at the detriment of the user experience, because it's just easier.

However, Dialogflow lets you easily achieve a conversational user experience by handling the natural language understanding (NLU) for you. When you use Dialogflow, you create ***agents*** that can understand the vast and varied nuances of human language and translate that to standard and structured meaning that your apps and services can understand. Let's take a look at how Dialogflow might handle the previous examples for weather forecast requests.

![figure1](https://dialogflow.com/docs/images/intro/overview-diagram.png)

**Figure 1.** Example of how Dialogflow handles a user utterance.

To look up a weather forecast, you might need a few pieces of information, like the time users want the forecast for and their location. However, as we previously mentioned, different users might request a forecast in different ways. Dialogflow can understand these differences and translate them to a standard user intent to get the forecast. It can then parse the user's request for the pertinent data you need to fulfill the request. In this case, that's the user's desired time and location for the weather forecast. Finally, you can use this data to look up the weather with a public REST API and return the weather to the user in the form of a response.

## How do agents work?

As we mentioned previously, an agent helps you process user input into structured data that you can use to return an appropriate response. You define all of these things inside one or many ***intents***, which define how to map user input to a corresponding response.

Let's take a look at an intent to get a better idea of how it works. A basic intent is comprised of these components:

**Training phrases**: Defines example phrases of what users can say. Dialogflow uses these training phrases and naturally expands them to many more similar phrases to build a language model that accurately matches user input. Through further training and machine learning, Dialogflow builds a more robust and varied language model to better match user input.

**Action and Parameters**: To improve an intent's language model, you can also annotate your training phrases with entities, or categories of data that you want Dialogflow to match. This lets you tell Dialogflow that you want a particular type of input and to not just match the literal input of the user. Dialogflow extracts matched entities as parameters from the training phrases. You can then process these parameters in logic called fulfillment to further customize a response to the user. You'll learn about fulfillment later in this document.

**Responses**: Defines a text, speech, or visual response to the user, which usually prompts users in a way that lets them know what to say next or that the conversation is ending. To send responses, you can use Dialogflow's built-in response handler or call fulfillment to process the extracted data and return a response back to Dialogflow.

Now let's see how these three major parts of an intent work together.

![figure2](https://dialogflow.com/docs/images/intro/agent-diagram.png)

1. When users say something, referred to as an ***utterance***, your agent matches the utterance to an appropriate intent, otherwise known as ***intent classification***. An intent is matched if the language model for that intent can closely or exactly match the user utterance. You define the language model by specifying training phrases, or examples of things users might want to say. Dialogflow takes these training phrases and expands upon them to create the intent's language model.

2. Once your agent matches an intent, it extracts ***parameters*** that you need from the utterance. This can be a color, name, date, or a host of other data categories called ***entities***. Dialogflow defines a large set entities that categorize extracted parameters, or you can create your own. You define what to extract in your training phrases as well, annotating specific parts of the training phrases to specify what parameters you want to extract.

3. You then send a response that can either prompt users for more information to continue the conversation or to just end the conversation. If more information is required, this back and forth happens again. Your agent matches a user utterance with an intent, extracts parameters, and returns a response. Dialogflow includes an easy-to-use response handler to return simple, usually static responses. If you want to return more catered responses, you can use logic called ***fulfillment*** to process any extracted parameters and return a response that is more dynamic or useful.

## How does fulfillment work?

Every intent has a built-in response handler that can return responses after the intent is matched. However, this feature only allows you to construct responses that are static or have minimal logic. Most times, you'll want to use fulfillment to process the intent first, and then return a more intelligent or useful response. Fulfillment is custom logic that you implement as a webhook, which services requests, processes them, and returns responses.

> Note: Your agent typically uses a combination of the two response types, using Dialogflow's built-in response handler to return simple or static responses like welcome or goodbye messages, and then delegating to fulfillment to generate more catered, varied, or appropriate responses. Dialogflow's response handler also acts as a fallback if your webhook is unresponsive.

Let's see how this works with a simple agent:

![figure3](https://dialogflow.com/docs/images/intro/fulfillment-diagram.png)

1. Your agent matches a user utterance to an intent.
2. Your agent extracts parameters out of the user utterance and calls your fulfillment with a JSON payload that contains the parameters along with a host of other useful information about the intent. Here's what a typical JSON request might look like for a user wanting to know the weather:

```json
{
"responseId": "3e9a2ec3-d79c-4a90-92dd-2375cc687029",
"queryResult": {
  "queryText": "What's the weather in Mountain View tomorrow?",
  "action": "weather",
  "parameters": {
    "date-time": "2018-08-10T12:00:00-07:00",
    "address": {
      "city": "Mountain",
      "business-name": "View"
    },
    "unit": "",
    "date-period": ""
  },
  "allRequiredParamsPresent": true,
  "fulfillmentMessages": [
    {
      "text": {
        "text": [
          ""
        ]
      }
    }
  ],
  "outputContexts": [
    {
      "name": "projects/weatherv2-784f4/agent/sessions/9f57c69d-e4cd-5f01-8ed9-fb72ea043570/contexts/weather",
      "lifespanCount": 2,
      "parameters": {
        "date-time.original": "tomorrow?",
        "unit.original": "",
        "unit": "",
        "address": {
          "city": "Mountain",
          "city.original": "Mountain",
          "city.object": {},
          "business-name": "View",
          "business-name.original": "View",
          "business-name.object": {}
        },
        "date-time": "2018-08-10T12:00:00-07:00",
        "date-period.original": "",
        "date-period": "",
        "address.original": "Mountain View"
      }
    }
  ],
  "intent": {
    "name": "projects/weatherv2-784f4/agent/intents/f1b75ecb-a35f-4a26-88fb-5a8049b92b02",
    "displayName": "weather"
  },
  "intentDetectionConfidence": 0.91,
  "languageCode": "en"
},
"originalDetectIntentRequest": {
  "payload": {}
},
"session": "projects/weatherv2-784f4/agent/sessions/9f57c69d-e4cd-5f01-8ed9-fb72ea043570"
}
```

3. Your fulfillment processes any necessary information it needs to from the JSON, such as calling another REST API with the extracted parameters.

4. Your fulfillment constructs a response and returns it back to Dialogflow to render to the user. This response can be simple text or a rich response, such as a card with an image. A typical response might look like this:

```json
{
"fulfillmentText": "This is a text response",
"fulfillmentMessages": [
  {
    "card": {
      "title": "card title",
      "subtitle": "card text",
      "imageUri": "https://assistant.google.com/static/images/molecule/Molecule-Formation-stop.png",
      "buttons": [
        {
          "text": "button text",
          "postback": "https://assistant.google.com/"
        }
      ]
    }
  }
],
"source": "example.com",
"payload": {
  "google": {
    "expectUserResponse": true,
    "richResponse": {
      "items": [
        {
          "simpleResponse": {
            "textToSpeech": "this is a simple response"
          }
        }
      ]
    }
  },
  "facebook": {
    "text": "Hello, Facebook!"
  },
  "slack": {
    "text": "This is a text response for Slack."
  }
},
"outputContexts": [
  {
    "name": "projects/${PROJECT_ID}/agent/sessions/${SESSION_ID}/contexts/context name",
    "lifespanCount": 5,
    "parameters": {
      "param": "param value"
    }
  }
],
"followupEventInput": {
  "name": "event name",
  "languageCode": "en-US",
  "parameters": {
    "param": "param value"
  }
}
}
```

> Note: If your webhook is unresponsive, Dialogflow automatically returns a response using the intent's built-in response handler as a fallback. It's sometimes useful to define a response in your agent and in fulfillment to take advantage of this feature.