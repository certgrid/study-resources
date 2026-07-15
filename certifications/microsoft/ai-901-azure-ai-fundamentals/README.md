# AI-901: Azure AI Fundamentals - Study Cheatsheet

AI-901: Azure AI Fundamentals is the refreshed Azure AI Fundamentals exam that replaced AI-900 (retired 30 June 2026). It validates foundational knowledge of AI and responsible AI, generative AI and language models, building and managing AI solutions and agents with Microsoft Foundry, and the vision, language, speech, and document intelligence services on Azure. It is a beginner exam that requires no coding or data-science background, with roughly 40-45 questions, about 45 minutes of working time, and a passing score of 700 on a 1-1000 scale.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AI-901 |
| Credential | AI-901: Azure AI Fundamentals |
| Level | Beginner |
| Practice mock length | ~45 questions |
| Duration | ~45 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Fundamentals of AI and responsible AI | ~19% |
| 2 | Fundamentals of generative AI and language models | ~21% |
| 3 | Build and manage AI solutions with Microsoft Foundry | ~21% |
| 4 | AI agents and agentic solutions | ~19% |
| 5 | Computer vision, natural language, speech, and document intelligence on Azure | ~21% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Fundamentals of AI and responsible AI

- AI workload types include machine learning, computer vision, natural language processing, document intelligence and knowledge mining, generative AI, and AI agents.
- Common machine learning task types: regression predicts a numeric value, classification predicts a category, clustering groups unlabeled data, anomaly detection flags outliers, and forecasting predicts future values over time.
- Features are the input variables a model learns from; labels are the known answers used in supervised learning. Models are trained on data, then used for inference (predictions) on new data.
- Datasets are split into training, validation, and test sets; overfitting means a model memorizes training data and fails to generalize to new data.
- Microsoft's six Responsible AI principles are fairness, reliability and safety, privacy and security, inclusiveness, transparency, and accountability.
- Fairness avoids bias across groups, transparency makes decisions understandable, and accountability keeps people responsible for AI outcomes.

### Domain 2 - Fundamentals of generative AI and language models

- Large language models are built on the transformer architecture and process text as tokens; embeddings represent meaning as numeric vectors used for similarity and search.
- A prompt is the input and a completion is the model's response; the context window limits how much text the model can consider at once.
- Temperature controls randomness: lower values give focused, deterministic output while higher values give more creative, varied output.
- Prompt engineering techniques include zero-shot and few-shot prompting, system messages, and chain-of-thought prompting.
- Grounding and retrieval-augmented generation (RAG) supply the model with your own trusted data so answers stay relevant and current, which reduces hallucinations.
- Responsible generative AI uses Azure AI Content Safety to filter harmful content, Prompt Shields to defend against prompt injection and jailbreaks, and evaluation on groundedness, relevance, and coherence.

### Domain 3 - Build and manage AI solutions with Microsoft Foundry

- Microsoft Foundry (formerly Azure AI Foundry) is the unified platform to build, deploy, and manage AI solutions, organized into projects, hubs, and connected resources.
- The model catalog lets you browse and compare foundation models from Microsoft, OpenAI, and other providers.
- Deployment options include serverless API (pay per token, no infrastructure to manage) and managed compute (dedicated capacity you provision).
- Deployed models expose an endpoint URL and key that applications use to send prompts and receive completions.
- Foundry supports fine-tuning, model evaluation and benchmarks, prompt flow, and grounding with your own data and indexes.
- Monitoring, quota, and cost management help you operate AI solutions responsibly and within budget.

### Domain 4 - AI agents and agentic solutions

- An AI agent uses tools (function calling), follows orchestration steps, and acts with some autonomy to complete a goal, grounded in your data.
- Use an agent instead of a single prompt when a task needs multiple steps, external actions, or decision-making.
- The Azure AI Agent Service in Microsoft Foundry builds agents with threads, tools, and knowledge sources.
- Tool or function calling lets an agent call external functions and APIs to take real actions or fetch live data.
- Multi-agent solutions coordinate several specialized agents to solve complex tasks.
- Responsible agent design adds guardrails, human-in-the-loop checkpoints, and safety controls.

### Domain 5 - Computer vision, natural language, speech, and document intelligence on Azure

- Azure AI Vision provides image analysis (captions, tags, objects), OCR through the Read capability, and Face detection; Custom Vision trains your own image classification or object detection model.
- Azure AI Language provides entity recognition, sentiment analysis, key phrase extraction, PII detection, summarization, and language detection.
- Azure AI Translator provides text and document translation across many languages.
- Azure AI Speech provides speech-to-text, text-to-speech, and speech translation.
- Azure AI Document Intelligence extracts fields and tables from forms and documents using prebuilt and custom models.
- Azure AI Search indexes your content to power retrieval-augmented generation (RAG) over your own data.

## Study tips

- Focus on what each Azure AI service does and which workload fits a given scenario - that is most of the exam.
- Memorize the six Responsible AI principles by name and be able to match each to a scenario.
- Know the core generative AI vocabulary: tokens, embeddings, prompts, context window, temperature, grounding, RAG, and prompt injection.
- Understand what Microsoft Foundry is for and the difference between serverless API and managed compute deployments.
- No coding is required; the exam is conceptual.

---

Want the full breakdown? See the complete **[AI-901 study guide](https://certgrid.app/study-guide/ai-901-azure-ai-fundamentals)** and **[free practice questions](https://certgrid.app/practice/ai-901-azure-ai-fundamentals)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

