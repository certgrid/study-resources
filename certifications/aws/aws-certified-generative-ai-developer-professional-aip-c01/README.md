# AWS Certified Generative AI Developer - Professional (AIP-C01) - Study Cheatsheet

The AWS Certified Generative AI Developer - Professional (AIP-C01) validates professional-level skills in building generative AI applications on AWS, primarily with Amazon Bedrock. It targets developers who integrate foundation models, implement RAG and agents, enforce guardrails and responsible AI, and optimize cost, performance, and reliability. The exam covers model selection and prompt engineering, retrieval and vector search, agent orchestration and tool use, AI safety and governance, operational efficiency, and testing and troubleshooting.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS Certified Generative AI Developer - Professional (AIP-C01) |
| Credential | AWS Certified Generative AI Developer - Professional (AIP-C01) |
| Level | Advanced |
| Practice mock length | ~65 questions |
| Duration | ~170 minutes |
| Passing score | 750 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Foundation Model Integration, Data Management, and Compliance | ~31% |
| 2 | Implementation and Integration | ~26% |
| 3 | AI Safety, Security, and Governance | ~20% |
| 4 | Operational Efficiency and Optimization for GenAI Applications | ~12% |
| 5 | Testing, Validation, and Troubleshooting | ~11% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Foundation Model Integration, Data Management, and Compliance

- The Converse API gives one consistent request and response format across supported Bedrock providers, so switching models usually means only changing the modelId; InvokeModel instead requires a provider-specific JSON schema per model family.
- Converse does not support every Bedrock model; embeddings-only models return vectors rather than conversational completions and must be called through InvokeModel.
- Choosing a model with a large enough context window is the key requirement for summarizing a very long document in a single request without splitting it, since the window caps combined input plus output length.
- Temperature, top-p, and top-k all shape randomness and diversity in generated text, while max tokens caps only the generated output length, not the input prompt length.
- RAG is favored when information changes often, when teams want to avoid building a labeled dataset, and when answers must be traceable to specific source documents; a fixed permanent style is better instilled through fine-tuning.
- In a RetrieveAndGenerate response, the citations array pairs each answer segment with its retrievedReferences, including the supporting chunk content and source location, so users can trace and verify each part of the answer.

### Domain 2 - Implementation and Integration

- The pgvector extension adds a native vector column type and similarity search to Aurora PostgreSQL, so embeddings can be joined with existing relational data via SQL without a separate vector service.
- Amazon OpenSearch Serverless offers a vector search collection type purpose-built for dense embeddings; on a knn_vector field the engine parameter selects the ANN library (Faiss, NMSLIB, or Lucene) and space_type sets the distance metric.
- Cosine similarity scores vectors purely by the angle between them, ideal for normalized embeddings, while dot product preserves magnitude so encoded signals like popularity can influence ranking.
- A stopReason of tool_use means the app must read the toolUse block (tool name, arguments, toolUseId), execute the tool, and append a toolResult message referencing that toolUseId, then call Converse again.
- Forcing a tool call eliminates stray commentary because the model must populate defined arguments in a structured toolUse block, leaving no free-text channel; a plain 'reply only in JSON' instruction can still be violated.
- Multi-step tool chains work by looping the conversation, returning each toolResult so the model can decide the next tool call; a supervisor agent delegating subtasks to specialized workers is the multi-agent collaboration pattern.

### Domain 3 - AI Safety, Security, and Governance

- Bedrock Guardrails apply to both prompt and response because different risks surface at different stages: injected instructions arrive in input while data leakage or a leaked system prompt appears in output.
- Guardrails content filter strength levels are None, Low, Medium, and High (Firm is not valid); the Misconduct category targets requests for help with criminal or unethical activity.
- Word filters match the literal configured words or phrases, whereas denied topics use a natural-language definition so the guardrail recognizes semantically related requests rather than keywords.
- The Guardrails sensitive information filter includes managed PII entity types such as email address and phone number that are recognized automatically.
- Malicious instructions embedded in a document that is later retrieved and fed to the model is a classic indirect prompt injection; grounding output in retrieved official API docs reduces fabricated method names.
- Tenant isolation for a shared retrieval Lambda means deriving the knowledge base ID from the authenticated session server-side, never trusting a model-supplied or user-supplied ID, so one tenant cannot reach another's data.

### Domain 4 - Operational Efficiency and Optimization for GenAI Applications

- Because API Gateway enforces a fixed maximum integration timeout, long-running generation should be handled asynchronously by returning a job reference immediately and letting the client poll or await notification; keep Lambda's timeout shorter than the gateway's and the client at least as patient.
- Provisioned throughput can beat on-demand pricing when a workload sustains high, predictable volume around the clock, since reserved capacity's effective per-request cost can fall below accumulated on-demand token charges.
- Providers price generated output tokens above input tokens because generation is autoregressive and sequential, consuming more compute per token, so long summaries cost more; stop sequences and length guidance cut trailing output tokens.
- Right-size to a smaller model when evaluation shows its accuracy is within an acceptable margin of the larger one at lower cost, driven by measured results rather than an assumed quality delta.
- Estimated cost per request built from expected token volumes gives a directly comparable financial measure, and passing only the relevant sections of a source document cuts input tokens per question.
- Prompt caching saves only when the cached segment is an exact, unchanged prefix reused across calls before it expires; a daily-changing value in the prefix breaks the exact-match requirement.

### Domain 5 - Testing, Validation, and Troubleshooting

- Reading an agent trace in its natural chronological order (preprocessing, orchestration reasoning, tool or knowledge base calls, post-processing) mirrors the order the agent executed and shows where its understanding diverged.
- Comparing segment durations in a trace localizes latency to model invocation, orchestration, or a tool call, and instrumenting a Lambda's own external calls narrows a slow tool call to the specific dependency.
- Temperature 0 favors the highest-probability token and makes output far more consistent but not guaranteed identical, because floating-point differences or backend routing can still add nondeterminism.
- Deterministic sampling, semantic similarity assertions, and JSON schema validation together reduce flaky LLM tests by tolerating valid rewording and checking structure instead of exact text.
- Faithfully reflecting irrelevant retrieved chunks points to a retrieval-stage problem (embedding mismatch, poor chunking, or missing documents), not a generation failure; feeding a known-correct passage directly isolates the generation step.
- Lowering temperature and instructing the model to rely only on supplied context both reduce fabricated content, since high temperature raises run-to-run variation and invented specifics even with grounded context.

## Study tips

- Learn the Converse versus InvokeModel split cold: Converse gives a unified format for conversational text and multimodal models, while embeddings-only models require InvokeModel. Many questions hinge on this distinction.
- For any RAG scenario, trace the failure to the right stage. Irrelevant-but-faithful answers mean retrieval is broken; fabricated content on good context means generation or temperature; use citations and precision/recall to reason about it.
- Memorize the exact Guardrails vocabulary: filter strengths are None, Low, Medium, High; word filters are literal; denied topics use natural-language definitions; and guardrails screen both prompt and response.
- When a question involves API Gateway plus long generation, default to an asynchronous job-and-poll pattern, and remember prompt caching only pays off with an unchanged exact prefix reused before expiry.
- Watch for security answers that trust model or user input. The correct choice almost always resolves tenant identity and sensitive parameters server-side from the authenticated session, not from the model.

---

Want the full breakdown? See the complete **[AWS Certified Generative AI Developer - Professional (AIP-C01) study guide](https://certgrid.app/study-guide/aws-certified-generative-ai-developer-professional-aip-c01)** and **[free practice questions](https://certgrid.app/practice/aws-certified-generative-ai-developer-professional-aip-c01)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

