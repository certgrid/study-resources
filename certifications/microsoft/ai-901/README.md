# AI-901: Microsoft Azure AI Fundamentals

AI-901 is the refreshed Azure AI Fundamentals exam. It replaced AI-900, which retired on June 30, 2026, and both grant the same Azure AI Fundamentals credential. Compared with AI-900, the focus has moved toward generative AI, AI agents, and Microsoft Foundry, and away from classical machine learning framing.

AI-901 is still a beginner exam, but it is more hands-on than AI-900 was. You should be able to recognize basic Python and Foundry SDK patterns, know your way around the Foundry portal, and understand what each Foundry Tool does. You are not expected to design or debug production AI systems.

These notes are built for fast revision and real understanding. Read the two domain notes, do the labs in the Foundry portal, then use the cheatsheets to remove confusion before taking practice tests.

## Start Here

Pick the path that matches your timeline:

| If you have...      | Use this path                                                                                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 day               | Read [Exam-Day Review](cheatsheets/ai-901-exam-day-review.md), then [Common Confusions](cheatsheets/ai-901-common-confusions.md)                                 |
| 3 days              | Read the two study notes, review [Service Picker](cheatsheets/ai-901-service-picker.md), then do practice questions                                              |
| 5 days              | Follow the recommended plan below and complete the Foundry project, model deployment, playground, agent, and cleanup labs                                        |
| No Azure experience | Start with [00 - Create a Microsoft Foundry Project](labs/00-create-foundry-project.md), then [01 - Explore the Model Catalog](labs/01-explore-model-catalog.md) |

## What to Memorize vs Understand

| Memorize                                                                   | Understand                                                         |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| The six responsible AI principles by name                                  | Which principle a given scenario is testing                        |
| AI workload types: generative, agentic, text, speech, vision, extraction   | Which workload fits a short business scenario                      |
| Generative AI vocabulary: token, embedding, prompt, context window         | How an LLM turns a prompt into a completion                        |
| Deployment options and configuration parameters (temperature, max tokens)  | When to change each parameter and what changes in the output       |
| Foundry building blocks: project, model catalog, deployment, endpoint, key | How an application actually calls a deployed model                 |
| Foundry Tools: Azure Speech, Azure Content Understanding                   | Which tool handles text, speech, vision, or information extraction |
| Prompt vs agent                                                            | When a task needs tools, steps, and autonomy instead of one prompt |

## Exam Snapshot

| Item           | Detail                                                     |
| -------------- | ---------------------------------------------------------- |
| Exam code      | AI-901                                                     |
| Certification  | Microsoft Certified: Azure AI Fundamentals                 |
| Level          | Beginner                                                   |
| Passing score  | 700 out of 1000                                            |
| Question count | Roughly 40-50 questions in about 45 minutes                |
| Question style | Conceptual and scenario-based, with light code recognition |
| Prerequisites  | Basic Azure familiarity and Python reading ability help    |
| Replaces       | AI-900 (retired June 30, 2026, same credential)            |

## Official Skill Areas

Aligned to the official study guide, skills measured as of April 15, 2026:

| Domain | Skill area                                        | Weight |
| ------ | ------------------------------------------------- | ------ |
| 1      | Identify AI concepts and capabilities             | 40-45% |
| 2      | Implement AI solutions by using Microsoft Foundry | 55-60% |

Source: [Official AI-901 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-901). Always confirm the active outline on the official study guide before booking.

Last verified: July 10, 2026.

For a bullet-by-bullet mapping of the official outline to these files, see the [Objective Coverage Matrix](coverage-matrix.md).

## How to Use This Folder

1. Read the two study notes in order. Domain 2 carries more weight, so give it more time.
2. Open the common-confusions file and check every pair you mix up.
3. Complete the labs so Foundry stops being a diagram and becomes a portal you have used.
4. Review the architecture diagram before practice tests.
5. Use the quick reference on the final day.

## Contents

### Study Notes

| File                                                                                                             | Use it for                                                       |
| ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [01 - Identify AI Concepts and Capabilities](study-notes/01-identify-ai-concepts-capabilities.md)                | Responsible AI, how generative models work, AI workload types    |
| [02 - Implement AI Solutions with Microsoft Foundry](study-notes/02-implement-ai-solutions-microsoft-foundry.md) | Foundry portal and SDK, agents, text, speech, vision, extraction |

### Cheatsheets

| File                                                                | Use it for                                 |
| ------------------------------------------------------------------- | ------------------------------------------ |
| [AI-901 Quick Reference](cheatsheets/ai-901-quick-reference.md)     | Last-day revision                          |
| [AI-901 Common Confusions](cheatsheets/ai-901-common-confusions.md) | Fixing the traps that cause wrong answers  |
| [AI-901 Service Picker](cheatsheets/ai-901-service-picker.md)       | Choosing the right model, tool, or service |
| [AI-901 Exam-Day Review](cheatsheets/ai-901-exam-day-review.md)     | Final 30-minute review before the exam     |
| [AI-901 Mock Review](cheatsheets/ai-901-mock-review.md)             | Original scenario drills with answer guide |
| [Azure CLI Cheatsheet](../azure-cli-cheatsheet.md)                  | Recognizing resource, key, endpoint, and CLI automation commands |

### Hands-On Labs

| Lab                                                                                                  | What it teaches                                                      |
| ---------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| [00 - Create a Microsoft Foundry Project](labs/00-create-foundry-project.md)                         | Foundry portal, projects, connected resources, cost awareness        |
| [01 - Explore the Model Catalog](labs/01-explore-model-catalog.md)                                   | Model catalog, comparing models by capability, cost, and context     |
| [02 - Deploy a Model](labs/02-deploy-a-model.md)                                                     | Deployment options, endpoints, keys                                  |
| [03 - Prompt in the Chat Playground](labs/03-chat-playground-prompts.md)                             | System prompts, few-shot prompting, temperature, max tokens          |
| [04 - Build a Chat Client with the Foundry SDK](labs/04-build-chat-client-foundry-sdk.md)            | Python client, endpoint and key, chat completions                    |
| [05 - Create an Agent in the Foundry Portal](labs/05-create-agent-foundry-portal.md)                 | Agent instructions, tools, knowledge, testing in the portal          |
| [06 - Build a Lightweight Agent Client](labs/06-build-agent-client.md)                               | Calling an agent from code, threads and runs                         |
| [07 - Analyze Text](labs/07-analyze-text.md)                                                         | Sentiment, entities, key phrases, summarization                      |
| [08 - Work with Speech](labs/08-work-with-speech.md)                                                 | Speech to text, text to speech, spoken prompts to a multimodal model |
| [09 - Use Vision in Prompts](labs/09-use-vision-in-prompts.md)                                       | Image input to a multimodal model, image analysis                    |
| [10 - Extract Information with Content Understanding](labs/10-extract-with-content-understanding.md) | Documents, forms, images, audio, and video extraction                |
| [11 - Clean Up Resources](labs/11-clean-up-resources.md)                                             | Deleting deployments and resources, avoiding surprise cost           |

### Diagrams

| Diagram                                                                      | What it teaches                                                |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------- |
| [Microsoft Foundry Architecture](diagrams/microsoft-foundry-architecture.md) | Foundry building blocks, app-to-model flow, agent anatomy, RAG |

### Coverage

| File                                            | Use it for                                                           |
| ----------------------------------------------- | -------------------------------------------------------------------- |
| [Objective Coverage Matrix](coverage-matrix.md) | Checking every official skill bullet against the file that covers it |

## What Usually Decides Pass or Fail

Most AI-901 mistakes come from confusing similar terms:

| If you confuse...                             | Review                                                      |
| --------------------------------------------- | ----------------------------------------------------------- |
| A prompt-only app and an agent                | One response vs tools, steps, and autonomy                  |
| Temperature and max tokens                    | Randomness of output vs length limit of output              |
| Serverless API and managed compute deployment | Pay per token vs dedicated capacity you provision           |
| Grounding/RAG and fine-tuning                 | Supplying data at question time vs retraining model weights |
| Speech recognition and speech synthesis       | Speech to text vs text to speech                            |
| Content Understanding and plain OCR           | Structured fields from any modality vs raw text from images |
| Fairness and inclusiveness                    | Avoiding biased outcomes vs designing for every user        |
| Transparency and accountability               | Explainable decisions vs humans answerable for outcomes     |

## High-Value Exam Traps

| Trap                                                 | Correct thinking                                                      |
| ---------------------------------------------------- | --------------------------------------------------------------------- |
| "The task needs multiple steps and external actions" | Build an agent, not a single prompt.                                  |
| "Answers must come from company documents"           | Ground the model with your data (RAG), do not just raise temperature. |
| "Output is too random and inconsistent"              | Lower the temperature.                                                |
| "Responses get cut off before finishing"             | Raise max tokens.                                                     |
| "Extract fields from invoices, calls, or videos"     | Azure Content Understanding in Foundry Tools.                         |
| "Read text aloud to users"                           | Speech synthesis (text to speech) with Azure Speech.                  |
| "Describe or answer questions about an image"        | Send the image to a deployed multimodal model.                        |
| "A loan model approves one group more often"         | Fairness principle.                                                   |
| "Users should know they are talking to AI"           | Transparency principle.                                               |
| "Who is responsible when the AI is wrong"            | Accountability principle.                                             |

## Recommended 5-Day Plan

| Day | Focus                                                                  |
| --- | ---------------------------------------------------------------------- |
| 1   | Responsible AI principles, AI workload types, generative AI vocabulary |
| 2   | Model selection, deployment options, configuration parameters          |
| 3   | Foundry portal and SDK, agents, labs 00-06                             |
| 4   | Text, speech, vision, Content Understanding, labs 07-11                |
| 5   | Quick reference, practice questions, wrong-answer review               |

## Readiness Checklist

Before booking, you should be able to explain these without notes:

- All six responsible AI principles with a one-line scenario for each
- How a generative model uses tokens, embeddings, and a context window
- What temperature, max tokens, and a system prompt each control
- Serverless API vs managed compute deployment
- Project, model catalog, deployment, endpoint, and key in Microsoft Foundry
- What makes an agent different from a single prompt, and what tools and knowledge add
- Which capability handles text analysis, speech, vision, and information extraction
- What Azure Content Understanding extracts from documents, images, audio, and video

## Score Booster Routine

Use this after each practice test:

1. Write down every wrong answer in one line.
2. Label the reason: vocabulary gap, workload confusion, Foundry confusion, or responsible AI confusion.
3. Re-read only the matching section in this folder.
4. Add the confused pair to your own notes.
5. Retake a small focused quiz before doing another full mock.

The goal is not to memorize answers. The goal is to stop repeating the same type of mistake.

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and hands-on tasks.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
