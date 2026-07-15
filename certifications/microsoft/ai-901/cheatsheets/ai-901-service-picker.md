# AI-901 Service Picker

AI-901 questions often reduce to "which model, tool, or capability fits this scenario?" Use the keyword in the question to pick fast, then sanity-check with the notes column.

## By scenario keyword

| Keyword in the question                          | Pick                                | Why                                           |
| ------------------------------------------------ | ----------------------------------- | --------------------------------------------- |
| "Draft, write, generate text"                    | Deployed language model             | Generative text is the base case              |
| "Compare available models"                       | Model catalog                       | Browsing and comparing happens in the catalog |
| "Make the model callable from an app"            | Deployment                          | Deployment creates the endpoint and key       |
| "Pay only for what we use, no infrastructure"    | Serverless API deployment           | Per-token billing, nothing to manage          |
| "Dedicated capacity, steady high volume"         | Managed compute deployment          | Provisioned compute you control               |
| "Test prompts without code"                      | Foundry portal playground           | No-code prompt testing                        |
| "Small Python app that chats"                    | Foundry SDK                         | Client libraries for calling deployments      |
| "Set the assistant's role, tone, and rules"      | System prompt                       | Standing behavior lives in the system prompt  |
| "Answers must come from our documents"           | Grounding / RAG (knowledge)         | Supply trusted data at request time           |
| "Teach the model our style with examples"        | Fine-tuning                         | Adjusts weights using your examples           |
| "Multiple steps, calls APIs, decides what to do" | Agent                               | Tools + orchestration + autonomy              |
| "Several specialists working together"           | Multi-agent solution                | Coordinated specialized agents                |
| "Transcribe calls, meetings, voicemails"         | Speech to text (Azure Speech)       | Recognition: audio in, text out               |
| "Read content aloud, voice responses"            | Text to speech (Azure Speech)       | Synthesis: text in, audio out                 |
| "Talk to the assistant, it answers by voice"     | Multimodal model with audio prompts | Spoken prompts to a deployed model            |
| "Describe / answer questions about an image"     | Multimodal model (visual input)     | Image interpretation                          |
| "Create images from a description"               | Image-generation model              | Visual output, not interpretation             |
| "Sentiment of reviews or tickets"                | Text analysis: sentiment            | Feeling of the text                           |
| "Find names, dates, organizations"               | Text analysis: entity detection     | Things named in the text                      |
| "Main topics per document"                       | Text analysis: key phrases          | Main terms, not a rewrite                     |
| "Shorten long reports"                           | Text analysis: summarization        | Shorter version, meaning kept                 |
| "Find and mask personal data"                    | Text analysis: PII detection        | Personal data handling                        |
| "Extract fields from invoices, forms, receipts"  | Azure Content Understanding         | Structured fields from documents              |
| "Extract info from images, audio, video"         | Azure Content Understanding         | Same tool, any modality                       |
| "Semantic search / find similar content"         | Embedding model + index             | Vectors power similarity and RAG retrieval    |

## Model choice by requirement

| Requirement                  | Choose                            |
| ---------------------------- | --------------------------------- |
| Text chat only               | General language model            |
| Image or audio in the prompt | Multimodal model                  |
| New images out               | Image-generation model            |
| Similarity and search        | Embedding model                   |
| Whole book in one request    | Large context window              |
| Cheap and fast at scale      | Smaller model                     |
| Hard multi-step reasoning    | Larger or reasoning-focused model |

## Parameter picker

| Symptom in the scenario  | Change            |
| ------------------------ | ----------------- |
| Too random, inconsistent | Lower temperature |
| Too bland, wants variety | Raise temperature |
| Cut off mid-answer       | Raise max tokens  |
| Repeats phrases          | Frequency penalty |
| Ends in the wrong place  | Stop sequences    |
| Wrong persona or format  | System prompt     |
| Wrong or stale facts     | Grounding/RAG     |

## Decision flow

```text
Is the scenario about creating content or answering questions?
  Text out           -> language model
  Image out          -> image-generation model
  Image/audio in     -> multimodal model
Is it about meaning in existing text?
  Feeling            -> sentiment
  Names/dates        -> entities
  Topics             -> key phrases
  Shorter version    -> summarization
Is it structured data out of unstructured content?
  Any modality       -> Azure Content Understanding
Is it speech conversion?
  Audio to text      -> speech to text
  Text to audio      -> text to speech
Does it need steps, tools, or decisions?
  Yes                -> agent (tools = actions, knowledge = data)
```
