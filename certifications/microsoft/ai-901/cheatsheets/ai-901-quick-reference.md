# AI-901 Quick Reference

One-page revision for the final day. If a line surprises you, go back to the matching study note.

## Responsible AI principles

| Principle              | One-line trigger                           |
| ---------------------- | ------------------------------------------ |
| Fairness               | Biased outcomes between groups             |
| Reliability and safety | Must work correctly and fail safely        |
| Privacy and security   | Protect personal data, resist attacks      |
| Inclusiveness          | Works for everyone, including disabilities |
| Transparency           | People understand how it decides           |
| Accountability         | Humans answer for AI outcomes              |

## Generative AI vocabulary

| Term           | Meaning                                           |
| -------------- | ------------------------------------------------- |
| Token          | Unit of text the model reads/writes               |
| Embedding      | Numeric vector of meaning                         |
| Prompt         | Input to the model                                |
| Completion     | The model's response                              |
| Context window | Max tokens the model considers at once            |
| Hallucination  | Confident but wrong output                        |
| Grounding/RAG  | Give the model your data at request time          |
| Fine-tuning    | Retrain weights with your examples                |
| Multimodal     | Accepts images/audio in the prompt, not just text |

## Configuration parameters

| Symptom                    | Fix                            |
| -------------------------- | ------------------------------ |
| Output too random          | Lower temperature              |
| Output too repetitive/dull | Raise temperature              |
| Response cut off           | Raise max tokens               |
| Repeats itself             | Frequency penalty              |
| Wrong tone or format       | Better system prompt           |
| Wrong facts                | Grounding/RAG, not temperature |

## Microsoft Foundry pipeline

```text
Model catalog -> Deploy (serverless API or managed compute)
             -> Endpoint + key (or Microsoft Entra ID)
             -> Test in playground -> Call from app (Foundry SDK)
```

| Compare        | Serverless API    | Managed compute              |
| -------------- | ----------------- | ---------------------------- |
| Billing        | Per token         | Provisioned capacity         |
| Infrastructure | None              | You provision                |
| Best for       | Start, spiky load | Steady volume, custom models |

## Agents

Agent = model + instructions + tools + knowledge.

| Part         | Role                                 |
| ------------ | ------------------------------------ |
| Instructions | The agent's standing system prompt   |
| Tools        | Functions/APIs it can call (actions) |
| Knowledge    | Data it is grounded in               |
| Thread       | Conversation session                 |
| Run          | One execution on a thread            |

Use an agent when the task needs multiple steps, external actions, or decisions. Otherwise a grounded prompt is enough.

## Capability picker

| Need                                        | Use                                 |
| ------------------------------------------- | ----------------------------------- |
| Chat, drafting, Q&A                         | Deployed language model             |
| Answer questions about an image             | Multimodal model (image in prompt)  |
| Create new images                           | Image-generation model              |
| Transcribe speech                           | Speech to text (Azure Speech)       |
| Read text aloud                             | Text to speech (Azure Speech)       |
| Spoken conversation with the model          | Multimodal model with audio prompts |
| Sentiment, entities, key phrases, summary   | Text analysis                       |
| Fields from documents, images, audio, video | Azure Content Understanding         |
| Semantic search over your content           | Embeddings + index (RAG)            |

## Text analysis quick table

| Question asks for          | Technique             |
| -------------------------- | --------------------- |
| Feeling/opinion            | Sentiment analysis    |
| Names, places, dates       | Entity detection      |
| Main topics                | Key phrase extraction |
| Shorter version            | Summarization         |
| Personal data found/masked | PII detection         |

## SDK, REST, and CLI anatomy

| Element                                         | Meaning                                                       |
| ----------------------------------------------- | ------------------------------------------------------------- |
| Endpoint + credential                           | Project location + authentication                             |
| `model="deployment-name"`                       | Call your deployment, not the model                           |
| `role: system`                                  | Standing behavior                                             |
| `role: user`                                    | The actual request                                            |
| `POST .../deployments/<name>/chat/completions`  | REST call to a deployment; deployment name is in the URL path |
| `api-key` header vs `Authorization: Bearer`     | Key auth vs a Microsoft Entra ID token                        |
| `az cognitiveservices account create/keys list` | CLI creates the resource / retrieves its keys (automation)    |

## Last-minute reminders

- Domain 2 (Foundry) is 55-60% of the exam; prompts, deployments, agents, and Foundry Tools decide the pass.
- Scenario says "multiple steps / call an API / decide": agent. Says "answer from our docs": grounding/RAG.
- Interpret an image = multimodal input. Create an image = image generation.
- Structured fields from unstructured content = Content Understanding, whatever the modality.
- Match disability wording to inclusiveness, explanation wording to transparency, responsibility wording to accountability.
