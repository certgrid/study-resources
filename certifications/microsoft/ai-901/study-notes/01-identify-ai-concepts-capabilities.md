# 01 - Identify AI Concepts and Capabilities

This domain is worth 40-45% of AI-901. It tests whether you can recognize responsible AI principles in scenarios, explain how generative AI models work at a conceptual level, choose an appropriate model, and match business scenarios to the right AI workload.

## Mental model

Think of this domain as three questions the exam keeps asking in different clothes: Is this AI being used responsibly? How does a generative model actually produce an answer? And which kind of AI capability does this scenario need? If you can name the principle, describe the prompt-to-completion flow, and pick the workload, you have most of this domain.

| Scenario keyword                         | Likely concept                        |
| ---------------------------------------- | ------------------------------------- |
| Model treats one group unfairly          | Fairness                              |
| AI must work for users with disabilities | Inclusiveness                         |
| Users should know how the AI decided     | Transparency                          |
| A human must answer for AI outcomes      | Accountability                        |
| Chatbot that writes original text        | Generative AI                         |
| System that plans steps and calls tools  | Agentic AI                            |
| Detect sentiment in reviews              | Text analysis                         |
| Convert a meeting recording to text      | Speech recognition                    |
| Describe the content of a photo          | Computer vision                       |
| Pull fields out of invoices or videos    | Information extraction                |
| Model invents facts                      | Hallucination, fix with grounding/RAG |

## What you must know

AI-901 does not ask you to build models. It asks you to recognize concepts. The three skill groups in this domain are:

1. Describe the principles of responsible AI.
2. Identify AI model components and configurations.
3. Identify AI workloads.

## Responsible AI principles

Microsoft defines six responsible AI principles. Learn them by name and be able to match each to a one-line scenario. The exam almost always tests these as scenario-to-principle matching.

| Principle              | Core idea                                                      | Typical scenario wording                                       |
| ---------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| Fairness               | AI should treat all groups without bias                        | "The model approves loans for one demographic more often"      |
| Reliability and safety | AI should work correctly and fail safely                       | "The self-driving feature must handle unexpected conditions"   |
| Privacy and security   | AI should protect personal data and resist attacks             | "Training data contains customer records that must be secured" |
| Inclusiveness          | AI should empower everyone, including people with disabilities | "The app must work for users with low vision"                  |
| Transparency           | People should understand how the AI makes decisions            | "Users should know why their application was rejected"         |
| Accountability         | People, not systems, are answerable for AI outcomes            | "Who is responsible when the AI gives harmful advice"          |

### The pairs people mix up

| Pair                           | Difference                                                                        |
| ------------------------------ | --------------------------------------------------------------------------------- |
| Fairness vs inclusiveness      | Avoiding biased outcomes vs deliberately designing so everyone can use the system |
| Transparency vs accountability | Making decisions understandable vs keeping humans responsible for outcomes        |
| Privacy vs reliability         | Protecting data vs the system behaving correctly and safely                       |

## How generative AI models work

You need a working vocabulary, not the math.

| Term            | Meaning                                                                      |
| --------------- | ---------------------------------------------------------------------------- |
| Token           | The unit of text a model reads and writes. Words are split into tokens.      |
| Embedding       | A numeric vector that represents meaning, used for similarity and search.    |
| Transformer     | The architecture behind large language models.                               |
| Prompt          | The input you send to the model.                                             |
| Completion      | The model's response.                                                        |
| Context window  | The maximum amount of text (tokens) the model can consider at once.          |
| Hallucination   | Confident output that is factually wrong.                                    |
| Grounding / RAG | Supplying your own trusted data with the request so answers stay accurate.   |
| Fine-tuning     | Additional training that adjusts model weights using your examples.          |
| Multimodal      | A model that accepts more than text, such as images or audio, in the prompt. |

A large language model predicts the next token repeatedly. It does not look facts up unless you ground it with data. That is why hallucinations happen and why retrieval-augmented generation (RAG) reduces them: the relevant documents are retrieved first and passed to the model as context.

### Prompting techniques

| Technique             | Meaning                                                        |
| --------------------- | -------------------------------------------------------------- |
| System prompt/message | Standing instructions that set behavior, tone, and constraints |
| Zero-shot             | Ask directly with no examples                                  |
| Few-shot              | Include a few worked examples in the prompt                    |
| Chain-of-thought      | Ask the model to reason step by step                           |

## Choosing an appropriate model

The exam gives a scenario and asks which model fits. Think in capabilities:

| Scenario needs...                     | Pick a model with...                |
| ------------------------------------- | ----------------------------------- |
| Chat or text generation               | A general language model            |
| Answers about images, or spoken input | Multimodal capabilities             |
| Generating new images                 | An image-generation model           |
| Semantic search or similarity         | An embedding model                  |
| Long documents in one request         | A large context window              |
| Low cost and low latency at scale     | A smaller model                     |
| Hard multi-step problems              | A larger or reasoning-focused model |

## Deployment options and configuration parameters

Models in Microsoft Foundry are deployed before applications can call them. Two options matter:

| Deployment option | How it works                                               | When it fits                              |
| ----------------- | ---------------------------------------------------------- | ----------------------------------------- |
| Serverless API    | Pay per token, no infrastructure to manage                 | Getting started, variable or low traffic  |
| Managed compute   | Dedicated capacity you provision and pay for while it runs | Steady high volume, custom or open models |

Configuration parameters shape the output of a deployed model:

| Parameter         | Controls                                            | Symptom it fixes                                      |
| ----------------- | --------------------------------------------------- | ----------------------------------------------------- |
| Temperature       | Randomness. Low = focused, high = creative          | Output too random: lower it. Too repetitive: raise it |
| Top P             | Alternative randomness control via probability mass | Similar effect to temperature, adjust one not both    |
| Max tokens        | Maximum length of the completion                    | Responses cut off: raise it                           |
| Stop sequences    | Strings that end the completion                     | Output runs past where it should stop                 |
| Frequency penalty | Discourages repeating the same tokens               | Output repeats itself                                 |
| System prompt     | Standing behavior instructions                      | Wrong tone, wrong format, off-topic answers           |

## AI workloads

Match the scenario to the workload type. This is high frequency on the exam.

| Workload               | What it covers                                              | Example                                          |
| ---------------------- | ----------------------------------------------------------- | ------------------------------------------------ |
| Generative AI          | Creating original text, images, code, or audio              | Draft product descriptions                       |
| Agentic AI             | Goal-driven systems that plan steps and call tools          | Assistant that checks stock and places the order |
| Text analysis          | Extracting meaning from text                                | Sentiment of support tickets                     |
| Speech                 | Recognizing and synthesizing spoken language                | Transcribe calls, read answers aloud             |
| Computer vision        | Understanding or generating images and video                | Tag photos, describe scenes, generate images     |
| Information extraction | Pulling structured data from text, images, audio, and video | Invoice fields, contract dates, call topics      |

### Text analysis techniques

| Technique                     | What it does                                      |
| ----------------------------- | ------------------------------------------------- |
| Keyword/key phrase extraction | Finds the main terms in a text                    |
| Entity detection              | Finds people, places, organizations, dates        |
| Sentiment analysis            | Scores text as positive, negative, neutral, mixed |
| Summarization                 | Produces a shorter version that keeps the meaning |

### Speech capabilities

| Capability         | Direction      | Example                          |
| ------------------ | -------------- | -------------------------------- |
| Speech recognition | Speech to text | Transcribe a meeting recording   |
| Speech synthesis   | Text to speech | An app reads notifications aloud |

### Vision and image generation

| Capability       | What it does                                               |
| ---------------- | ---------------------------------------------------------- |
| Image analysis   | Captions, tags, objects, and text (OCR) from images        |
| Image generation | Creates new images from a text description                 |
| Multimodal input | A deployed model answers questions about an image you send |

### Information extraction

Information extraction turns unstructured content into structured data. On Azure, Azure Content Understanding (a Foundry Tool) extracts fields from documents and forms, text from images, and insights such as transcripts and topics from audio and video. If the scenario says "pull specific fields out of unstructured content," think information extraction.

## Common confusions

| Confused pair                          | How to keep them apart                                                      |
| -------------------------------------- | --------------------------------------------------------------------------- |
| Generative AI vs agentic AI            | Produces content vs pursues a goal with steps and tools                     |
| Grounding/RAG vs fine-tuning           | Adds your data at request time vs retrains model weights with your examples |
| Temperature vs top P                   | Both control randomness, adjust one, not both                               |
| Embedding vs token                     | Vector of meaning vs unit of text                                           |
| Sentiment analysis vs entity detection | Feeling of the text vs things named in the text                             |
| Speech recognition vs speech synthesis | Speech in, text out vs text in, speech out                                  |
| OCR vs information extraction          | Raw text from an image vs structured fields with meaning                    |

## Exam traps

| Trap                                                   | Correct thinking                                                                                 |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| Picking fine-tuning when answers must use company data | Grounding/RAG is the first choice; fine-tuning changes style and skills, not knowledge freshness |
| Raising temperature to fix wrong facts                 | Temperature changes randomness, not accuracy. Ground the model instead                           |
| Calling every chatbot an agent                         | An agent needs tools, orchestration, or autonomy, not just chat                                  |
| Choosing image generation for "describe this photo"    | Describing needs analysis or a multimodal model, not generation                                  |
| Matching "users with disabilities" to fairness         | That is inclusiveness                                                                            |
| Matching "explain the decision" to accountability      | That is transparency                                                                             |

## Mini scenarios

| Scenario                                                                    | Answer             |
| --------------------------------------------------------------------------- | ------------------ |
| A hiring model shortlists men more often than equally qualified women       | Fairness problem   |
| A bank must tell customers why the AI declined their application            | Transparency       |
| An assistant books travel by searching flights and paying with a saved card | Agentic AI         |
| Reviews must be scored positive or negative automatically                   | Sentiment analysis |
| A model must answer questions about uploaded floor-plan images              | Multimodal model   |
| Chatbot answers must come only from the company handbook                    | Grounding/RAG      |
| Completions stop mid-sentence                                               | Raise max tokens   |
| Marketing wants five very different slogan drafts                           | Raise temperature  |

## Check yourself

1. Name all six responsible AI principles.
2. A model keeps inventing product specs. What is this called, and what fixes it?
3. What is the difference between a token and an embedding?
4. When would you choose managed compute over serverless API?
5. Which parameter do you change when output is cut off early?
6. Speech to text is called what? Text to speech is called what?
7. A scenario needs invoice fields extracted from PDFs. Which workload is this?
8. What makes an agent different from a prompt-only chatbot?

## Answer guide

1. Fairness, reliability and safety, privacy and security, inclusiveness, transparency, accountability.
2. Hallucination. Ground the model with trusted data (RAG).
3. A token is a unit of text the model processes; an embedding is a numeric vector representing meaning.
4. Steady, high-volume workloads or when you need dedicated capacity for a custom or open model.
5. Max tokens.
6. Speech recognition; speech synthesis.
7. Information extraction (Azure Content Understanding).
8. An agent pursues a goal with orchestration steps, tools (function calling), and some autonomy.
