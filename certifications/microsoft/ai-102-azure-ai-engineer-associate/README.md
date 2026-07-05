# AI-102: Azure AI Engineer Associate - Study Cheatsheet

AI-102: Azure AI Engineer Associate validates your ability to build, manage, deploy, and secure AI solutions on Azure using services for natural language processing, computer vision, document intelligence, knowledge mining, and generative AI. It targets software developers and AI engineers who integrate Azure AI services into applications and is a 120-minute exam with a passing score of 700 (scaled 1-1000). Expect scenario-based questions covering provisioning, security, monitoring, responsible AI, and the correct service selection for a given business need.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AI-102 |
| Credential | AI-102: Azure AI Engineer Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Plan and Manage an Azure AI Solution | ~17% |
| 2 | Implement Content Moderation Solutions | ~14% |
| 3 | Implement Computer Vision Solutions | ~15% |
| 4 | Implement NLP Solutions | ~17% |
| 5 | Implement Knowledge Mining and Document Intelligence | ~16% |
| 6 | Implement Generative AI Solutions | ~15% |
| 7 | Implement Agentic Solutions | ~5% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Plan and Manage an Azure AI Solution

- An Azure AI Services multi-service resource exposes one endpoint and one key (one pair) for many services (Vision, Language, Speech, etc.), simplifying management and consolidating billing versus separate single-service resources.
- Microsoft Entra ID (formerly Azure AD) token authentication is the recommended secure method over subscription keys; it supports RBAC, centralized identity, and audit trails. The Cognitive Services User role grants data-plane access.
- To lock down network access, configure a private endpoint (a NIC inside your VNet) for the Azure AI Services resource and disable public network access so traffic never traverses the public internet.
- Store subscription keys in Azure Key Vault and reference them at runtime; regenerate keys periodically (each resource has two keys so you can rotate one while the other stays active).
- Customer-managed keys (CMK) for encryption at rest are configured using keys stored in Azure Key Vault, giving you control over the encryption key lifecycle (Microsoft-managed keys are the default).
- Azure AI containers (for disconnected/on-premises use) require the ApiKey and Billing (endpoint URI) parameters plus EULA acceptance; they periodically send metering/usage data to Azure for billing and stop functioning after a billing grace period if connectivity is lost.

### Domain 2 - Implement Content Moderation Solutions

- Azure AI Content Safety returns discrete severity scores of 0 (Safe), 2 (Low), 4 (Medium), and 6 (High) on a 0-6 even-number scale for each harm category.
- The four harm categories analyzed by Content Safety are Hate (and fairness), Sexual, Violence, and Self-Harm; each is scored independently.
- Setting a filter threshold to 0 blocks content flagged at any severity (strictest); higher thresholds allow lower-severity content through.
- Prompt Shields detect and mitigate prompt-injection and jailbreak attacks, including attempts to override system instructions (direct attacks) and indirect attacks embedded in documents.
- Groundedness detection checks whether a model's response is factually grounded in the provided source documents, helping catch hallucinations in RAG scenarios.
- Protected material detection identifies known copyrighted text (and code) in model output to reduce IP risk.

### Domain 3 - Implement Computer Vision Solutions

- Azure AI Vision Image Analysis 4.0 provides built-in visual features: Caption, Dense Captions, Tags, Objects (with bounding boxes), People (with bounding boxes), Smart Crops, and Read (OCR) in a single API.
- The Read API (OCR) extracts both printed and handwritten text from images and documents and returns text with location coordinates.
- Dense captions generate natural-language descriptions for multiple regions of an image (vs. a single caption for the whole image).
- Smart cropping with aspect-ratio support generates thumbnails focused on the most relevant region of an image.
- Multimodal embeddings (vectorize image / vectorize text) let you perform image similarity and image-to-text search by comparing vectors in the same embedding space.
- An object's bounding box is the rectangular region, expressed in pixels, that encloses a detected object within the image.

### Domain 4 - Implement NLP Solutions

- Conversational Language Understanding (CLU) is the modern Azure AI Language feature for building language models that recognize user intents and extract entities from utterances; both intents and entities are required components.
- An Orchestration workflow project in CLU routes an incoming utterance to the right downstream project: a CLU app, a custom question answering knowledge base, or a LUIS app.
- Custom text classification supports two project types: single-label (each document belongs to exactly one mutually exclusive category) and multi-label (a document can have multiple categories).
- Custom Named Entity Recognition (Custom NER) trains on labeled examples to extract domain-specific entities (e.g., policy numbers, claim IDs) not covered by prebuilt NER.
- Prebuilt NER recognizes categories such as Person, Location, Organization, DateTime, Quantity, and more without training.
- Sentiment analysis returns positive/negative/neutral with confidence scores; enabling opinion mining (aspect-based) links sentiments to specific opinion targets (e.g., 'the food' vs. 'the service').

### Domain 5 - Implement Knowledge Mining and Document Intelligence

- Azure AI Search has four core components: a data source (connection to the data store, e.g., Blob Storage), a skillset (AI enrichment), an indexer (orchestrates the pipeline), and an index (queryable schema that stores results).
- The indexer pipeline runs in this order: document cracking, skillset enrichment, output field mappings, then index population (field mappings map source fields to index fields).
- A skillset contains built-in cognitive skills (language detection, key phrase extraction, entity recognition, OCR, image analysis) chained together, and can include custom skills.
- A custom skill (Web API skill) calls external logic such as an Azure Function with an HTTP trigger or an Azure ML endpoint, defined in the skillset with input/output mappings.
- A knowledge store persists enriched output to storage: table projections write structured rows to Azure Table Storage (good for Power BI), and object projections write JSON blobs to Azure Blob Storage.
- Vector search in an index requires a vector field of type Collection(Edm.Single) with an assigned vector search profile and a vector search algorithm configuration such as HNSW (or exhaustive KNN).

### Domain 6 - Implement Generative AI Solutions

- GPT models are deployed in an Azure OpenAI resource managed through Azure AI Foundry (formerly Azure AI Studio); a deployment specifies the model, version, and capacity (tokens per minute) and provides the endpoint.
- The system message defines the assistant's persona, role, output format, and global behavior constraints; instructions about tone and format belong here.
- Temperature controls randomness: lower values (near 0) give deterministic, grounded outputs; higher values increase creativity. top_p (nucleus sampling) is the alternative randomness control.
- Retrieval-Augmented Generation (RAG) combines a retrieval system (e.g., Azure AI Search) that fetches relevant documents with a generative model that produces grounded responses; it grounds answers without changing model weights.
- Azure OpenAI On Your Data is the built-in RAG feature that connects an Azure AI Search index to a deployment and instructs the model to answer from retrieved data, with no fine-tuning required.
- Embedding models such as text-embedding-ada-002, text-embedding-3-small, and text-embedding-3-large convert text into dense vectors for semantic similarity search.

### Domain 7 - Implement Agentic Solutions

- An AI agent autonomously plans, reasons, and takes actions using tools to accomplish goals with minimal human intervention, iterating based on observations (unlike a passive chatbot).
- A tool (function) is defined with a name, description, and a JSON schema describing its parameters; clear tool descriptions and system instructions are critical so the agent picks the right tool.
- The Microsoft Foundry Agent Service (Azure AI Agent Service) requires an Azure AI Foundry project with a connected Azure OpenAI deployment to power agent reasoning.
- Built-in agent tools include File Search (connected to a vector store of indexed documents for grounding), Code Interpreter, and Function calling for custom actions.
- The ReAct (Reasoning and Acting) pattern has the agent alternate between thinking, acting (calling a tool), and observing results until the goal is met.
- Agent memory persists conversation context and user information; create a separate conversation thread per user with isolated memory so contexts do not leak between users.

## Study tips

- Master service selection: many questions describe a business scenario and ask which Azure AI service fits. Build a mental decision table mapping needs (extract form fields, moderate images, recognize intent, ground answers in your data) to the exact service.
- Know the security and management story cold: private endpoints + disable public access, Entra ID over keys, Key Vault for secrets and CMK, Azure Monitor + Log Analytics for diagnostics, and the six Responsible AI principles.
- Memorize concrete numbers and defaults: Content Safety severity scale (0/2/4/6), the four harm categories, low temperature for deterministic output, embedding model names, HNSW for vector search, and the indexer pipeline order.
- Distinguish overlapping features: fine-tuning (style/format) vs. RAG (knowledge); single-label vs. multi-label classification; Custom NER vs. prebuilt NER; Custom Vision classification vs. object detection; extractive vs. abstractive summarization.
- Read scenario questions for the deciding constraint (cost, latency, data residency, on-premises/disconnected, network isolation, or no model training allowed) - that constraint usually eliminates all but one answer.

---

Want the full breakdown? See the complete **[AI-102 study guide](https://certgrid.app/study-guide/ai-102-azure-ai-engineer-associate)** and **[free practice questions](https://certgrid.app/practice/ai-102-azure-ai-engineer-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

