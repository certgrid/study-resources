# AWS Certified AI Practitioner (AIF-C01) - Study Cheatsheet

The AWS Certified AI Practitioner (AIF-C01) validates foundational understanding of artificial intelligence, machine learning, and generative AI on AWS, along with responsible AI, security, and governance. It is aimed at people who use AI/ML solutions and understand the underlying concepts rather than those who build and train models. Expect conceptual questions on choosing the right approach or AWS service, not hands-on coding or math.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS Certified AI Practitioner (AIF-C01) |
| Credential | AWS Certified AI Practitioner (AIF-C01) |
| Level | Intermediate |
| Practice mock length | ~65 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Fundamentals of AI and ML | ~20% |
| 2 | Fundamentals of generative AI | ~24% |
| 3 | Applications of foundation models | ~28% |
| 4 | Guidelines for responsible AI | ~14% |
| 5 | Security, compliance, and governance for AI solutions | ~14% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Fundamentals of AI and ML

- Supervised learning trains on labeled data where the outcome is already known, and it powers both classification (predicting a category) and regression (predicting a numeric value). If historical records already contain the answer, such as loans marked repaid or defaulted, it is a supervised problem.
- Unsupervised learning finds structure in unlabeled data. Clustering algorithms like k-means discover natural groupings, such as customer segments, without any predefined labels or categories.
- Inference is the act of using an already-trained model to score new, unseen data, for example scoring a single new transaction for fraud risk.
- Hyperparameters are settings chosen before training begins, such as the number of layers or the learning rate. They are configured by the practitioner, unlike model parameters (weights), which are learned during training.
- Overfitting is when a model performs well on training data but poorly on new data, shown by a large gap between training and validation accuracy or by validation loss rising while training loss keeps falling. Underfitting is the opposite: the model is too simple to capture the pattern.
- The bias-variance tradeoff describes how model complexity shifts error between underfitting (high bias) and overfitting (high variance); tuning complexity balances the two.

### Domain 2 - Fundamentals of generative AI

- Foundation models are large models pre-trained on broad data that can be adapted to many tasks. Pre-training gives broad general ability but not task-optimized behavior, which is why further customization is often needed.
- Tokens are the units of text a model processes, and each model uses its own tokenizer and vocabulary. The same text can split into different numbers of tokens across models, so token counts are model-specific, not universal.
- Prompt engineering (prompt design) is how a prompt is worded, structured, and detailed; it strongly influences output quality and is the lowest-effort way to steer a model without changing its weights.
- The typical customization effort ranking from least to most is: prompt engineering, then Retrieval Augmented Generation (RAG), then fine-tuning.
- In-context learning, including few-shot prompting (supplying a handful of example input-output pairs in the prompt), guides the model at inference time and leaves the model's weights unchanged.
- Fine-tuning updates the model's weights to bake a behavior or format directly into the model, reducing per-request prompt length and cost. Its drawbacks are that baked-in knowledge can become stale and it requires the most effort of the customization approaches.

### Domain 3 - Applications of foundation models

- A RAG pipeline typically chunks documents into smaller pieces, uses an embedding model to convert each chunk and the user query into numeric vectors, stores those vectors, then retrieves the most similar chunks to ground the model's response in current, verified source content.
- Cosine similarity is the standard measure for comparing embedding vectors, ranking retrieved chunks by how close they are in vector space to the query.
- Vector storage options on AWS include the pgvector extension on Aurora PostgreSQL, and Amazon Kendra can act as a managed retriever with prebuilt enterprise connectors and ML relevance ranking, so a team need not pick an embedding model, build chunking, or run a separate vector database.
- Temperature reshapes the token probability distribution to control randomness; a temperature near 0 approximates deterministic, greedy selection. Combined with a restrictive top-k (for example top-k of 1), it drives near-deterministic, repeatable output.
- Maximum tokens only caps the length of the output; it does not affect creativity or randomness.
- Prompt structure matters for safety: separating trusted, developer-authored system instructions from untrusted user input (via message roles or clear delimiters) makes prompt injection harder, though not impossible.

### Domain 4 - Guidelines for responsible AI

- The core dimensions of responsible AI include fairness, robustness, privacy and security, transparency, explainability, governance, and sustainability.
- Robustness is a system's ability to keep performing reliably under noisy, degraded, unexpected, or adversarial inputs, such as an image classifier that still works despite blur, poor lighting, or deliberate perturbations.
- Hallucination is when a model generates plausible-sounding but fabricated or incorrect content. Grounding responses in retrieved verified sources with RAG is a key mitigation.
- SageMaker Clarify targets bias detection and prediction explainability (feature attribution). It computes pre-training bias metrics on the raw dataset before any model exists, such as Class Imbalance (CI) and Difference in Proportions of Labels (DPL), and separate post-training bias metrics computed on model predictions.
- SageMaker Model Monitor detects drift in production, including bias drift and feature attribution drift, addressing shifting fairness disparities and changing feature importance over time.
- Amazon Bedrock Guardrails enforce runtime safety policies on generative AI applications; a single guardrail configuration can be reused across multiple models and applications. Clarify focuses on bias and explainability, while Guardrails focus on real-time content safety.

### Domain 5 - Security, compliance, and governance for AI solutions

- The AWS shared responsibility model applies to managed services like Bedrock: AWS secures the underlying infrastructure, while the customer remains responsible for access control, data protection, and guardrail configuration.
- Private connectivity keeps AI traffic off the public internet: an interface VPC endpoint (AWS PrivateLink) keeps Bedrock API calls on the AWS network, and running a training job inside a VPC with network isolation enabled contains its network access.
- IAM should scope permissions tightly; for example, restricting the Bedrock InvokeModel action to specific model ARNs enforces exactly which models a principal is allowed to call.
- Server-side encryption with KMS using a customer managed key (SSE-KMS with CMK) gives the data owner control over key policy, rotation, and grants, so access can be revoked immediately if the key is suspected of compromise.
- Secrets such as API keys should be stored in AWS Secrets Manager and retrieved at build or run time, keeping credentials out of source control and container images.
- Amazon Inspector performs automated vulnerability scanning and factors network reachability into its risk scores, reflecting whether a vulnerable resource is actually exposed. Adding a scan as a CI/CD gate that fails the build on critical findings blocks vulnerable images from reaching production.

## Study tips

- Focus on choosing the right approach or AWS service for a scenario rather than math or coding; the exam tests conceptual judgment for people who use AI/ML, not build it.
- Memorize the customization effort ladder (prompt engineering, then RAG, then fine-tuning) and know which fits: RAG for frequently changing data, fine-tuning to bake in format or domain style, prompting for quick low-effort steering.
- Learn what each AWS AI tool is for: Bedrock and Bedrock Guardrails for generative AI and runtime safety, SageMaker Clarify for bias and explainability, Model Monitor for drift, and managed services (Polly, Transcribe, Textract, Rekognition) for ready-made tasks.
- Understand evaluation metrics and when accuracy misleads: use precision, recall, and F1 on imbalanced data, and know that inference parameters like temperature and top-k control randomness while max tokens only caps length.
- For security questions, apply the shared responsibility model, least-privilege IAM scoping, private connectivity via VPC endpoints, encryption with customer managed KMS keys, and Secrets Manager for credentials.

---

Want the full breakdown? See the complete **[AWS Certified AI Practitioner (AIF-C01) study guide](https://certgrid.app/study-guide/aws-certified-ai-practitioner-aif-c01)** and **[free practice questions](https://certgrid.app/practice/aws-certified-ai-practitioner-aif-c01)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

