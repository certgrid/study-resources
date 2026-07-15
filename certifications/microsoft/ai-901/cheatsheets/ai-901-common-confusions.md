# AI-901 Common Confusions

Most wrong answers on AI-901 come from mixing up one of these pairs. Check every pair; if you hesitate, read the line twice and find it in the study notes.

## Responsible AI pairs

| Pair                           | The difference                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------- |
| Fairness vs inclusiveness      | Unbiased outcomes between groups vs designed so everyone can use it              |
| Transparency vs accountability | Decisions are understandable vs humans are answerable for outcomes               |
| Privacy vs security            | Protecting personal data vs resisting attacks and misuse                         |
| Reliability vs safety          | Works correctly vs fails without causing harm (tested together as one principle) |

## Generative AI pairs

| Pair                           | The difference                                                 |
| ------------------------------ | -------------------------------------------------------------- |
| Token vs embedding             | Unit of text vs numeric vector of meaning                      |
| Prompt vs completion           | What you send vs what the model returns                        |
| Temperature vs max tokens      | Randomness of output vs length limit of output                 |
| Temperature vs top P           | Two randomness controls; adjust one, not both                  |
| Zero-shot vs few-shot          | No examples in the prompt vs a few worked examples             |
| Grounding/RAG vs fine-tuning   | Your data supplied at request time vs retraining model weights |
| Hallucination vs bias          | Invented facts vs systematically skewed outputs                |
| Multimodal vs image generation | Accepts images/audio as input vs creates images as output      |

## Foundry pairs

| Pair                              | The difference                                                    |
| --------------------------------- | ----------------------------------------------------------------- |
| Model catalog vs deployment       | Browsing/comparing models vs a callable instance with an endpoint |
| Model name vs deployment name     | Catalog identity vs the name your code calls                      |
| Serverless API vs managed compute | Pay per token, no infra vs dedicated capacity you provision       |
| Playground vs SDK                 | Test in the portal without code vs call from an application       |
| Endpoint vs key                   | Where to call vs how to authenticate                              |
| Project vs deployment             | The workspace vs one callable model inside it                     |

## Agent pairs

| Pair                         | The difference                                                  |
| ---------------------------- | --------------------------------------------------------------- |
| Prompt-only chatbot vs agent | One response vs steps, tools, and autonomy toward a goal        |
| Tools vs knowledge           | Actions the agent can take vs data the agent answers from       |
| Instructions vs user message | Standing behavior of the agent vs the current request           |
| Thread vs run                | Conversation session vs one execution of the agent              |
| Single agent vs multi-agent  | One agent with tools vs several specialized agents coordinating |

## Capability pairs

| Pair                                     | The difference                                                     |
| ---------------------------------------- | ------------------------------------------------------------------ |
| Speech recognition vs speech synthesis   | Speech to text vs text to speech                                   |
| Azure Speech vs multimodal audio prompts | Dedicated speech service vs a model that takes audio in the prompt |
| Image analysis vs image generation       | Understand an existing image vs create a new one                   |
| OCR vs Content Understanding             | Raw text from an image vs structured fields with meaning           |
| Text analysis vs Content Understanding   | Meaning from text vs structured extraction from any modality       |
| Sentiment vs entity detection            | How the text feels vs what the text names                          |
| Key phrases vs summarization             | List of main terms vs a shorter rewritten version                  |
| Embeddings vs chat completions           | Vectors for search/similarity vs generated text answers            |

## The five that cost the most points

1. **Grounding/RAG vs fine-tuning.** "Answers must use our documents / stay current" is grounding. Fine-tuning changes style and skill, not knowledge freshness.
2. **Agent vs prompt.** Count the verbs: if the scenario needs looking things up, calling systems, or deciding next steps, it is an agent.
3. **Interpret vs generate images.** Describe/answer/check = multimodal input. Create/design/draw = image generation.
4. **Deployment name in code.** Applications call the deployment you created, never the catalog model name.
5. **Content Understanding for any "extract fields" scenario.** Documents, forms, images, audio, video: if the output is structured data, this is the tool.
