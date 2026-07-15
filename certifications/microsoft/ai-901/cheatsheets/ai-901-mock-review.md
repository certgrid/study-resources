# AI-901 Mock Review

28 original scenario drills in shuffled order, weighted roughly like the exam: about 40% Domain 1 (Identify AI concepts and capabilities) and 60% Domain 2 (Implement AI solutions by using Microsoft Foundry). These are practice drills written for this pack, not real exam questions. Answer each one in your head or on paper, then check the answer guide at the bottom and read the rationale even when you were right.

## How to use this file

| Step | Action                                                                     |
| ---- | -------------------------------------------------------------------------- |
| 1    | Answer all 28 drills without looking at the answer guide                   |
| 2    | Score yourself; anything below 22 correct means another study-note pass    |
| 3    | For every miss, read the rationale and note which wrong choice tempted you |
| 4    | Re-read only the matching study-note section, then retry the missed drills |

## Drills

1. A retail team wants an assistant that checks warehouse stock through an internal API, compares supplier prices, and places a restock order once it finds the best option. What should they build?
2. A Python script calls `chat.chat.completions.create(model="gpt-support-bot", ...)` and fails with a model-not-found error, even though the catalog model was deployed successfully under a different name. What is wrong?
3. A bank customer asks why the AI declined her credit application, and the team cannot explain the decision. Which responsible AI principle is not being met?
4. A startup wants to try a new language model this afternoon with no infrastructure to manage and costs that scale with usage. Which deployment option fits?
5. A developer sends `POST https://contoso-ai.openai.azure.com/openai/deployments/chat-prod/chat/completions` with an `api-key` header and a JSON `messages` array. What is this request doing, at a recognition level?
6. Support-ticket summaries keep stopping mid-sentence. Which configuration parameter should be changed, and in which direction?
7. A legal firm needs contract dates, party names, and renewal clauses pulled out of thousands of scanned PDFs as structured fields. Which capability fits?
8. A voice kiosk should let visitors ask questions out loud and have a single deployed model understand the audio directly, without a separate transcription step. What does this require?
9. A hiring model shortlists candidates from one university far more often than equally qualified candidates from others. Which responsible AI principle does this violate?
10. A marketing analyst with no coding background wants to experiment with prompt wording and temperature against a deployed model. Where should she work?
11. An agent built in the Foundry portal must answer questions using only the company's HR policy documents. Which agent component handles this?
12. An operations engineer wants a script that spins up an Azure AI services resource for a new environment and then prints its keys, without opening the portal. Which kind of command sequence is this, and roughly what does it look like?
13. A chatbot confidently describes a product feature that does not exist. What is this behavior called, and what is the standard first fix?
14. A team needs a model that can answer questions about photos users upload and also handle typed follow-up questions in the same conversation. Which model capability matters most when choosing from the catalog?
15. In a Foundry SDK snippet, one message has `"role": "system"` and another has `"role": "user"`. A reviewer asks why the tone-of-voice rules are in the user message. What should change?
16. An insurer runs a claims model that must keep working correctly during storms and fail safely when it hits inputs it cannot handle. Which responsible AI principle is this?
17. A developer must add sentiment scoring and key phrase extraction to a feedback form with a small amount of Python. Which approach fits AI-901's scope?
18. A company wants weekly podcast episodes turned into transcripts plus a structured list of topics and speakers. Which Foundry capability handles audio like this?
19. A product owner asks whether their single-question FAQ bot, which answers from a grounded prompt, should be rebuilt as an agent. What is the right call?
20. Which is the better reason to call a deployed model through raw REST instead of the Foundry SDK: the client app is written in a language with no SDK available, or REST responses are faster?
21. A generative model gives excellent answers but wildly different ones each time, and the team wants consistency for compliance reasons. What should they adjust?
22. A team deployed a model with managed compute for a demo, finished the demo a week ago, and is surprised by the bill. Why is it still costing money?
23. A news app must read articles aloud in a natural voice for commuters. Which capability is this, and which Foundry Tool provides it?
24. A single agent conversation session contains several separate executions where the agent worked on a task. In Foundry agent vocabulary, what are the session and each execution called?
25. An accessibility review finds a voice assistant unusable for customers who cannot speak clearly. Which responsible AI principle should drive the redesign?
26. A designer needs twenty fresh concept images of a product that does not exist yet, generated from short text descriptions. Which kind of model does this need?
27. A REST request to a deployment fails with 401 Unauthorized. The URL and deployment name are correct. Name the two authentication approaches the request could be using, one of which is misconfigured.
28. A team wants semantic search so that "cheap flights" also matches documents saying "low-cost airfare". Which model type and technique should they use?

## Answer guide

1. An agent with tools (function calling). The task needs multiple steps, external API calls, and a decision, which is exactly when an agent beats a single prompt; a grounded prompt is tempting but cannot call the stock or ordering APIs.
2. The code is passing the catalog model name instead of the deployment name. Applications call the deployment name you chose at deployment time; the raw model name is the tempting wrong value because it appears throughout the catalog.
3. Transparency. People should be able to understand how the AI reached its decision; accountability is the tempting wrong answer, but that principle is about humans being answerable for outcomes, not about explaining them.
4. Serverless API. It bills per token with no infrastructure to manage, ideal for starting out; managed compute is wrong here because you would provision and pay for dedicated capacity before knowing if the model fits.
5. It is a chat completions call to a specific deployment (`chat-prod`) on a Foundry resource, authenticated with a key and sending the conversation as JSON messages. Recognizing the deployment name in the URL path is the key skill; the model name never appears in the path.
6. Raise max tokens. Max tokens caps completion length, so a low value truncates output; temperature is the tempting wrong knob, but it changes randomness, not length.
7. Azure Content Understanding in Foundry Tools. It returns structured fields from documents and forms; plain OCR is the tempting wrong answer because it returns raw text, not labeled fields like dates and clauses.
8. A deployed multimodal model that accepts audio input in the prompt. Azure Speech transcription plus a text model is the tempting alternative, but the scenario explicitly rules out a separate transcription step.
9. Fairness. The model produces biased outcomes between groups; inclusiveness is the tempting wrong answer, but that is about designing so everyone can use the system, not about biased results.
10. The Foundry portal playground. It is the no-code place to test prompts and parameters against a deployment; building an SDK client is the tempting overkill answer for a non-coder.
11. Knowledge (grounding). Knowledge is the data the agent answers from; tools are the tempting wrong choice, but tools are actions the agent takes, not sources it reads.
12. An Azure CLI script, shaped like `az cognitiveservices account create ...` followed by `az cognitiveservices account keys list ...`. The CLI is for resource management and automation; the SDK is the tempting wrong answer, but it is for calling models from app code, not provisioning resources.
13. Hallucination, fixed first by grounding the model with trusted data (RAG). Fine-tuning is the tempting wrong fix because it changes style and skills through retraining rather than supplying accurate facts at request time.
14. Multimodal capability, so the model accepts image input in the prompt alongside text. An image-generation model is the tempting wrong pick; it creates images and cannot answer questions about them.
15. Move the tone-of-voice rules into the system message. Standing behavior belongs in the system prompt; the user message should carry only the actual request for that turn.
16. Reliability and safety. The system must work correctly under unexpected conditions and fail safely; privacy and security is the tempting neighbor, but nothing here is about protecting data.
17. A lightweight text analysis application, using a deployed language model or the language capabilities in Foundry Tools. Training a custom ML model is the tempting wrong answer; AI-901 is about using existing capabilities, not building models.
18. Azure Content Understanding in Foundry Tools, which extracts transcripts and structured insights such as topics from audio. Azure Speech is the tempting wrong answer; it transcribes, but structured insights across content is Content Understanding's job.
19. Keep the grounded prompt; do not build an agent. Agents are for multiple steps, external actions, and autonomy; a one-question, one-answer bot gains nothing from the extra machinery.
20. The language has no SDK. REST works from anything that can send HTTP, which is its real advantage; the speed claim is the trap, since the SDK wraps the same REST endpoints.
21. Lower the temperature (or top P, but not both). Low temperature makes output focused and repeatable; raising max tokens is the tempting irrelevant change, since length is not the complaint.
22. Managed compute bills for provisioned capacity the whole time it exists, not per request. Serverless-style per-token billing is the tempting assumption; the fix is to delete the deployment when it is idle.
23. Speech synthesis (text to speech), provided by Azure Speech in Foundry Tools. Speech recognition is the classic reversal trap; recognition converts speech to text, the opposite direction.
24. The session is a thread and each execution is a run. Swapping them is the standard trap; remember a thread holds the conversation while runs happen on it.
25. Inclusiveness. The system should empower everyone, including people with speech differences or disabilities; fairness is the tempting wrong answer, but no group is receiving biased outcomes from a decision.
26. An image-generation model deployed in Foundry. A multimodal model is the tempting wrong answer; it interprets images you give it but does not create new ones.
27. Either an `api-key` header carrying a resource key, or an `Authorization: Bearer` header carrying a Microsoft Entra ID token. Knowing both exist is the point; assuming key-based auth is the only option is the trap.
28. An embedding model with a vector index (the retrieval side of RAG). Embeddings capture meaning so similar phrases land near each other; keyword extraction is the tempting wrong answer because it matches literal terms, not meaning.

## Domain mix

| Domain                                                | Drills                                                        | Share     |
| ----------------------------------------------------- | ------------------------------------------------------------- | --------- |
| 1 - Identify AI concepts and capabilities             | 3, 6, 9, 13, 14, 16, 21, 25, 26, 28 and part of 4             | About 40% |
| 2 - Implement AI solutions by using Microsoft Foundry | 1, 2, 5, 7, 8, 10, 11, 12, 15, 17, 18, 19, 20, 22, 23, 24, 27 | About 60% |
