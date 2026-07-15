# AI-901 Exam-Day Review

Use this page in the final 30-45 minutes before the exam. It is intentionally short and focused on high-frequency decisions.

## The Exam Mindset

AI-901 is a fundamentals exam. Most questions ask you to recognize the right concept, capability, or Foundry building block from the wording, plus a few light code-recognition items. Domain 2 (Microsoft Foundry) carries 55-60% of the marks.

When stuck, ask:

1. Is this about responsible AI principles?
2. Is this about how generative models work or their parameters?
3. Is this about which AI workload fits?
4. Is this about the Foundry pipeline: catalog, deployment, endpoint, playground, SDK?
5. Is this about agents, or about a Foundry Tool (Speech, Content Understanding)?

## Must-Know Pairs

| Pair                               | Difference                                      |
| ---------------------------------- | ----------------------------------------------- |
| Fairness vs inclusiveness          | Unbiased outcomes vs usable by everyone         |
| Transparency vs accountability     | Explainable decisions vs humans responsible     |
| Token vs embedding                 | Unit of text vs vector of meaning               |
| Temperature vs max tokens          | Randomness vs response length                   |
| Grounding/RAG vs fine-tuning       | Your data at request time vs retraining weights |
| Serverless API vs managed compute  | Per token, no infra vs provisioned capacity     |
| Model name vs deployment name      | Catalog identity vs what your code calls        |
| Playground vs SDK                  | No-code portal testing vs application code      |
| Prompt vs agent                    | One response vs steps, tools, autonomy          |
| Tools vs knowledge                 | Agent actions vs agent data                     |
| Thread vs run                      | Conversation session vs one execution           |
| Speech recognition vs synthesis    | Speech to text vs text to speech                |
| Image interpretation vs generation | Understand an image vs create one               |
| OCR vs Content Understanding       | Raw text vs structured fields                   |

## Responsible AI in Ten Seconds

| Scenario says...                  | Principle              |
| --------------------------------- | ---------------------- |
| Biased against a group            | Fairness               |
| Must not cause harm when it fails | Reliability and safety |
| Customer data must be protected   | Privacy and security   |
| Works for users with disabilities | Inclusiveness          |
| Explain how it decided            | Transparency           |
| Someone must own the outcome      | Accountability         |

## The Foundry Pipeline

```text
Model catalog -> Deployment -> Endpoint + key -> Playground test -> App via Foundry SDK
```

- Serverless API: pay per token, zero infrastructure, the default way to start.
- Managed compute: dedicated capacity, you provision, for steady volume or custom models.
- Code calls the **deployment name** with the endpoint and a key or Microsoft Entra ID.

## Final Capability Picker

| Keyword                                | Answer                      |
| -------------------------------------- | --------------------------- |
| Draft, write, generate text            | Language model              |
| Questions about an uploaded image      | Multimodal model            |
| Create a new image                     | Image-generation model      |
| Transcribe audio                       | Speech to text              |
| Speak responses                        | Text to speech              |
| Sentiment, entities, topics, summary   | Text analysis               |
| Fields from forms/images/audio/video   | Azure Content Understanding |
| Multiple steps + API calls + decisions | Agent with tools            |
| Answer only from company docs          | Grounding / knowledge (RAG) |
| Similar-content search                 | Embeddings                  |

## Parameter Fixes

| Symptom           | Fix               |
| ----------------- | ----------------- |
| Too random        | Lower temperature |
| Cut off           | Raise max tokens  |
| Repetitive        | Frequency penalty |
| Wrong tone/format | System prompt     |
| Wrong facts       | Ground with data  |

## Last Five Reminders

1. Weight your time like the exam: Foundry questions are more than half the marks.
2. Read the verb on image questions: describe/answer = multimodal input, create/design = generation.
3. Any "extract fields from unstructured content" is Content Understanding, whatever the modality.
4. An agent needs a reason to exist: steps, tools, or autonomy. Otherwise it is a grounded prompt.
5. Do not overthink code snippets: identify the endpoint, credential, deployment name, and message roles.
