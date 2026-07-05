# AI-901: Azure AI Fundamentals - Study Cheatsheet

A concise, exam-focused study guide for **AI-901**, the refreshed Azure AI Fundamentals exam that replaced **AI-900** (retired 30 June 2026). Same credential, but the focus moved to generative AI, AI agents, and Microsoft Foundry. Always confirm the current objectives on Microsoft Learn before you book.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AI-901 (replaces AI-900) |
| Credential | Microsoft Certified: Azure AI Fundamentals |
| Level | Beginner - no coding or data-science background required |
| Format | ~40-45 multiple-choice / multi-response questions |
| Duration | ~45 minutes |
| Passing score | 700 out of 1000 |
| Focus shift | Generative AI, AI agents, Microsoft Foundry (away from classical ML) |

## Domain 1 - Fundamentals of AI and responsible AI

- **AI workload types:** machine learning, computer vision, natural language processing, document intelligence and knowledge mining, generative AI, and agents.
- **ML task types:** regression (predict a number), classification (predict a category), clustering (group unlabeled data), anomaly detection (flag outliers), forecasting (predict future values over time).
- **Core concepts:** features (inputs) vs labels (the answer), training vs inference, model, dataset, and the train / validate / test split. Overfitting = memorizing training data instead of generalizing.
- **Responsible AI - the 6 Microsoft principles:**

| Principle | What it means |
|---|---|
| Fairness | Treat all groups equitably; avoid bias |
| Reliability & safety | Perform consistently and safely, even in unexpected conditions |
| Privacy & security | Protect data and respect user privacy |
| Inclusiveness | Work for people of all abilities and backgrounds |
| Transparency | Be understandable; users know how and why it decides |
| Accountability | People remain responsible for the system's outcomes |

## Domain 2 - Fundamentals of generative AI and language models

- **LLM basics:** transformers, tokens (text broken into chunks), embeddings (numeric meaning vectors), prompts and completions, context window (how much the model can "see"), and temperature (higher = more creative, lower = more focused).
- **Prompt engineering:** zero-shot vs few-shot prompting, system messages, chain-of-thought. **Grounding** and **RAG** (retrieval-augmented generation) feed the model your own trusted data so answers are relevant and current.
- **Azure OpenAI:** access to GPT chat models, embedding models, and image models through the model catalog. Choose a model by capability, cost, and context size.
- **Responsible generative AI:** Azure AI Content Safety filters harmful content; hallucinations (confident wrong answers) are reduced with grounding/RAG; Prompt Shields defend against prompt injection and jailbreaks; evaluate outputs on groundedness, relevance, and coherence.

## Domain 3 - Build and manage AI solutions with Microsoft Foundry

- **Microsoft Foundry** (formerly Azure AI Foundry) is the unified platform to build, deploy, and manage AI solutions - organized into **projects**, **hubs**, and connected resources.
- **Model catalog:** browse and compare foundation models from multiple providers.
- **Deployment options:** serverless API (pay per token, no infrastructure) vs managed compute (dedicated capacity). You get an endpoint URL + key to consume the model.
- **Also covered:** fine-tuning, model evaluation and benchmarks, prompt flow, grounding data/indexes, monitoring, and quota/cost management.

## Domain 4 - AI agents and agentic solutions

- **What an agent is:** an AI that can use **tools / function calling**, follow **orchestration** steps, and act with some **autonomy** to complete a goal, grounded in your data.
- **When to use an agent** vs a single prompt: when the task needs multiple steps, external actions, or decision-making.
- **Azure AI Agent Service** (in Microsoft Foundry): build agents with threads, tools, and knowledge sources.
- **Multi-agent solutions** coordinate several agents; responsible agent design adds guardrails, human-in-the-loop, and safety checks.

## Domain 5 - Vision, language, speech, and document intelligence on Azure

| Service | Use it for |
|---|---|
| **Azure AI Vision** | Image analysis (captions, tags, objects), OCR / Read (text in images), Face, Custom Vision (train your own image model) |
| **Azure AI Language** | Entity recognition, sentiment analysis, key phrase extraction, PII detection, summarization, translation |
| **Azure AI Speech** | Speech-to-text, text-to-speech, speech translation |
| **Azure AI Document Intelligence** | Extract fields/tables from forms and documents (prebuilt + custom models) |
| **Azure AI Search** | Index your content for retrieval-augmented generation (RAG) |

## Study tips

- Focus on **what each Azure AI service does** and **which workload fits a scenario** - that is most of the exam.
- Know the **6 responsible AI principles** by name and definition; expect scenario questions.
- Understand **generative AI vocabulary** (tokens, embeddings, grounding, RAG, prompt injection) and **what Microsoft Foundry is for**.
- You do **not** need to write code or build models.

---

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_
