# 02 - Implement AI Solutions by Using Microsoft Foundry

This domain is worth 55-60% of AI-901, the largest share. It tests whether you know how to deploy and use models in Microsoft Foundry, build simple generative AI apps and agents, and use Foundry capabilities for text, speech, vision, and information extraction. Expect light code recognition: you should be able to read a short Python snippet that calls the Foundry SDK and say what it does.

## Mental model

Everything in this domain follows one pipeline: pick a model from the catalog, deploy it in a Foundry project, get an endpoint and key, then call it from the portal playground or a small client app. Agents add instructions, tools, and knowledge on top of a deployed model. Foundry Tools add ready-made capabilities (speech, content understanding) you call the same way.

| Scenario keyword                                | Likely concept                               |
| ----------------------------------------------- | -------------------------------------------- |
| Browse and compare available models             | Model catalog                                |
| Make a model callable by apps                   | Deployment (endpoint + key)                  |
| Pay only per token                              | Serverless API deployment                    |
| Dedicated capacity you provision                | Managed compute deployment                   |
| Try prompts without writing code                | Foundry portal playground                    |
| Small Python app that chats with a model        | Foundry SDK chat client                      |
| Set standing behavior for the model             | System prompt                                |
| Assistant that calls functions and APIs         | Agent with tools (function calling)          |
| Agent answers from your documents               | Knowledge / grounding                        |
| Transcribe or speak with users                  | Azure Speech in Foundry Tools                |
| Answer questions about an uploaded image        | Multimodal model, visual input in the prompt |
| Generate a new image from a description         | Image-generation model                       |
| Extract fields from forms, images, audio, video | Azure Content Understanding in Foundry Tools |

## Microsoft Foundry building blocks

Microsoft Foundry (formerly Azure AI Foundry) is the unified platform for building, deploying, and managing AI solutions on Azure.

| Building block   | What it is                                                                 |
| ---------------- | -------------------------------------------------------------------------- |
| Foundry portal   | The web experience where you create projects, deploy models, and test them |
| Project          | The workspace that holds your deployments, agents, data, and settings      |
| Model catalog    | Browse and compare foundation models from Microsoft, OpenAI, and others    |
| Deployment       | A model instance made callable, with a name you reference from code        |
| Endpoint and key | The URL and credential an application uses to call a deployment            |
| Playground       | Portal chat interface for testing prompts and parameters without code      |
| Foundry SDK      | Client libraries (Python and others) for calling models and agents         |
| Foundry Tools    | Ready-made AI capabilities such as Azure Speech and Content Understanding  |

### Deploying a model

1. Open the model catalog in the Foundry portal and pick a model by capability, cost, and context window.
2. Deploy it: choose serverless API (pay per token) or managed compute (dedicated capacity).
3. The deployment gets a name, an endpoint URL, and keys (or Microsoft Entra ID authentication).
4. Test it in the playground, then call it from an application.

| Compare        | Serverless API              | Managed compute                        |
| -------------- | --------------------------- | -------------------------------------- |
| Billing        | Per token used              | For provisioned capacity while it runs |
| Infrastructure | None to manage              | You choose and pay for compute         |
| Best for       | Starting out, spiky traffic | Steady volume, open or custom models   |

## Prompts: system vs user

| Prompt type   | Purpose                                                 | Example                                                   |
| ------------- | ------------------------------------------------------- | --------------------------------------------------------- |
| System prompt | Standing instructions: role, tone, rules, output format | "You are a support assistant. Answer in three sentences." |
| User prompt   | The actual question or task for this turn               | "How do I reset my password?"                             |

Effective prompts state the role, the task, the constraints, and the output format. Few-shot examples in the prompt improve consistency. The exam tests whether you know which instruction belongs in the system prompt (behavior) vs the user prompt (the request).

## A minimal chat client with the Foundry SDK

You do not need to write this from scratch in the exam, but you should recognize the moving parts:

```python
import os
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

project = AIProjectClient(
    endpoint=os.environ["FOUNDRY_PROJECT_ENDPOINT"],
    credential=DefaultAzureCredential(),
)

chat = project.get_openai_client()
response = chat.chat.completions.create(
    model="my-deployment-name",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Explain tokens in one sentence."},
    ],
)
print(response.choices[0].message.content)
```

What the exam wants you to recognize:

| Code element                  | Meaning                                              |
| ----------------------------- | ---------------------------------------------------- |
| Endpoint + credential         | Where the project lives and how you authenticate     |
| `model="my-deployment-name"`  | You call the deployment name, not the raw model name |
| `role: system` / `role: user` | System prompt vs user prompt                         |
| The messages list             | Conversation history gives the model context         |

## REST and CLI recognition

The official study guide says you should be familiar with REST APIs, SDKs, and CLIs. The SDK does most of the work in this pack, but the exam can show you a raw HTTP call or an Azure CLI command and ask what it does. Recognition is enough; you will not write these from memory.

### A REST call to a deployment

The SDK snippet above is a wrapper around an HTTP request like this:

```http
POST https://contoso-ai.openai.azure.com/openai/deployments/my-deployment-name/chat/completions?api-version=2024-10-21
Content-Type: application/json
api-key: <YOUR-RESOURCE-KEY>

{
  "messages": [
    { "role": "system", "content": "You are a helpful assistant." },
    { "role": "user", "content": "Explain tokens in one sentence." }
  ]
}
```

| Part of the request                   | What it tells you                                                                                                  |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `https://contoso-ai.openai.azure.com` | The endpoint URL of the Foundry resource the deployment lives in                                                   |
| `/deployments/my-deployment-name/`    | The deployment name in the path; you call your deployment, never the catalog model name                            |
| `/chat/completions`                   | The operation: send messages, get a completion back                                                                |
| `api-key` header                      | Key-based authentication; the alternative is an `Authorization: Bearer` header carrying a Microsoft Entra ID token |
| JSON `messages` body                  | The same system and user roles as the SDK: standing behavior vs the actual request                                 |

### Azure CLI recognition

Azure CLI commands manage the resources themselves, not the conversation. Recognize the shape and the purpose:

| Command shape                                                         | What it accomplishes                                            |
| --------------------------------------------------------------------- | --------------------------------------------------------------- |
| `az cognitiveservices account create --name ... --kind ... --sku ...` | Creates the Azure AI services resource that backs Foundry Tools |
| `az cognitiveservices account keys list --name ...`                   | Retrieves the keys an application uses to authenticate          |
| `az cognitiveservices account show --name ...`                        | Shows resource details, including the endpoint URL              |

### REST vs SDK vs CLI

- REST: any language or tool that can send HTTP can call a deployment; nothing to install.
- SDK: the convenient choice inside application code; it handles authentication, request shaping, and responses for you.
- CLI: scripting and automation of the resources themselves, such as creating an account or listing keys, not chatting with a model.

## Agents

An agent is a model plus instructions, tools, and knowledge, able to take steps toward a goal with some autonomy. Use an agent instead of a single prompt when the task needs multiple steps, external actions, or decisions.

| Agent part   | What it does                                                    |
| ------------ | --------------------------------------------------------------- |
| Model        | The deployed model that powers reasoning and language           |
| Instructions | The agent's system prompt: role, rules, goal                    |
| Tools        | Functions and APIs the agent can call to act or fetch live data |
| Knowledge    | Your data sources (files, indexes) the agent is grounded in     |
| Thread       | A conversation session with an agent                            |
| Run          | One execution of the agent working on a thread                  |

In the Foundry portal you can create a single-agent solution without code: pick the model, write instructions, attach tools and knowledge, then test it in the portal. A lightweight client application then talks to the agent by creating threads and runs through the SDK.

| Compare          | Single prompt              | Agent                                 |
| ---------------- | -------------------------- | ------------------------------------- |
| Steps            | One response               | Plans and executes multiple steps     |
| External actions | None                       | Calls tools and APIs                  |
| Data             | Only what is in the prompt | Grounded in attached knowledge        |
| Autonomy         | None                       | Decides which tool or step comes next |

Multi-agent solutions coordinate several specialized agents on a complex task. Responsible agent design adds guardrails and human-in-the-loop checkpoints for consequential actions.

## Text and speech solutions

### Text analysis

Build lightweight apps that analyze text: sentiment, entities, key phrases, PII detection, language detection, summarization. In Foundry you can do this with a deployed language model or with the language capabilities in Foundry Tools; the exam cares that you match the technique to the scenario.

| Need                                    | Technique             |
| --------------------------------------- | --------------------- |
| How do customers feel                   | Sentiment analysis    |
| Which products and places are mentioned | Entity detection      |
| The main topics of each ticket          | Key phrase extraction |
| A short version of a long report        | Summarization         |
| Find and mask personal data             | PII detection         |

### Speech

Azure Speech in Foundry Tools provides speech to text (recognition), text to speech (synthesis), and speech translation. A deployed multimodal model can also respond directly to spoken prompts: the audio goes into the prompt, the model answers.

| Scenario                                   | Answer                                        |
| ------------------------------------------ | --------------------------------------------- |
| Transcribe support calls                   | Speech to text (Azure Speech)                 |
| App reads answers aloud                    | Text to speech (Azure Speech)                 |
| Users talk to the assistant and it answers | Spoken prompts to a deployed multimodal model |

## Vision and image generation

| Scenario                                         | Answer                                             |
| ------------------------------------------------ | -------------------------------------------------- |
| Answer questions about an image the user uploads | Send the image in the prompt to a multimodal model |
| Caption or tag photos in an app                  | Vision capabilities in a lightweight app           |
| Create marketing images from a text description  | Image-generation model deployed in Foundry         |

Interpreting visual input (analysis via a multimodal model) and creating visual output (generation) are different capabilities and often different models. Read the scenario verb: describe/answer/check means interpret; create/design/draw means generate.

## Information extraction with Azure Content Understanding

Azure Content Understanding in Foundry Tools extracts structured information from unstructured content across modalities:

| Input               | What it extracts                                                |
| ------------------- | --------------------------------------------------------------- |
| Documents and forms | Fields, tables, key-value pairs (invoices, receipts, contracts) |
| Images              | Text and structured information in the image                    |
| Audio               | Transcripts plus structured insights such as topics             |
| Video               | Transcripts, scenes, and structured insights                    |

A lightweight information-extraction app sends content to Content Understanding and receives structured output (fields and values) it can store or act on. If the scenario is "turn unstructured content into structured data," this is the answer, regardless of modality.

## Common confusions

| Confused pair                            | How to keep them apart                                               |
| ---------------------------------------- | -------------------------------------------------------------------- |
| Model catalog vs deployment              | Browsing models vs making one callable with an endpoint              |
| Deployment name vs model name            | Code calls your deployment name, not the catalog model name          |
| Playground vs SDK                        | No-code portal testing vs calling from an application                |
| System prompt vs agent instructions      | Same idea; instructions are the agent's standing system prompt       |
| Tools vs knowledge                       | Actions the agent can take vs data the agent is grounded in          |
| Thread vs run                            | The conversation session vs one execution of the agent               |
| Azure Speech vs multimodal audio prompts | Dedicated speech service vs a general model that accepts audio input |
| Content Understanding vs text analysis   | Structured fields from any modality vs meaning from text             |

## Exam traps

| Trap                                                      | Correct thinking                                                    |
| --------------------------------------------------------- | ------------------------------------------------------------------- |
| Calling the catalog model name in code                    | Applications call the deployment name                               |
| Choosing managed compute "to start quickly"               | Serverless API is the quick, no-infrastructure start                |
| Putting behavior rules in the user prompt                 | Standing behavior belongs in the system prompt                      |
| Building an agent for a single-question FAQ bot           | A grounded prompt is enough; agents are for steps, tools, autonomy  |
| Using image generation to answer questions about an image | That is visual interpretation with a multimodal model               |
| Using plain OCR for invoice fields                        | Content Understanding returns structured fields, not just text      |
| Ignoring cost when a deployment is idle                   | Managed compute bills while provisioned; serverless bills per token |

## Mini scenarios

| Scenario                                                             | Answer                                      |
| -------------------------------------------------------------------- | ------------------------------------------- |
| Compare two models' context windows before choosing                  | Model catalog                               |
| Marketing tests prompt wording without writing code                  | Foundry portal playground                   |
| A Python app sends a system and user message to a deployment         | Chat client using the Foundry SDK           |
| The assistant must check order status via an internal API            | Agent with a tool (function calling)        |
| The agent must answer only from the product manual                   | Attach the manual as knowledge (grounding)  |
| Users speak to the kiosk and it answers questions about a menu photo | Multimodal model with audio and image input |
| Extract totals and dates from thousands of scanned receipts          | Azure Content Understanding                 |
| Convert articles into natural-sounding audio                         | Text to speech with Azure Speech            |

## Check yourself

1. What four things does an application need to call a deployed model?
2. Serverless API or managed compute: which bills per token?
3. Where do standing behavior instructions belong, and what is that called for an agent?
4. Name the four parts that make an agent more than a prompt.
5. What is the difference between a thread and a run?
6. A user uploads a photo and asks "is this plug damaged?" Which capability answers?
7. Which Foundry Tool extracts structured data from audio and video?
8. In the SDK snippet, why is `model="my-deployment-name"` and not the catalog name?

## Answer guide

1. The endpoint URL, a credential (key or Microsoft Entra ID), the deployment name, and the messages/prompt.
2. Serverless API.
3. In the system prompt; for an agent they are called instructions.
4. Model, instructions, tools, knowledge.
5. A thread is the ongoing conversation session; a run is one execution of the agent on that thread.
6. Visual input to a deployed multimodal model (image interpretation, not generation).
7. Azure Content Understanding.
8. Applications call the named deployment you created; the deployment maps to the underlying model.
