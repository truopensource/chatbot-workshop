# Agents 

## Agents Overview

Agents are best described as Natural Language Understanding (NLU) modules. These modules can be included in your app, website, product, or service and translate text or spoken user requests into actionable data. This translation occurs when a user's utterance matches an intent within your agent.

![figure1](https://dialogflow.com/docs/images/intro/overview-diagram.png)

**Figure 1.** Example of how Dialogflow's fulfillment calls an external API to construct the response to a user.

The matched intent then delivers a response back to the user. This response can be a simple text or spoken acknowledgment or a webhook response that includes information obtained from another system. In Figure 1, Dialogflow sends a webhook request with the location and date parameters to a third-party weather service. This weather service returns a webhook response in JSON format. The agent's custom fulfillment parses the JSON data and delivers a response to the user with the relevant information.