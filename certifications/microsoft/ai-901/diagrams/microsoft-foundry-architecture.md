# Microsoft Foundry Architecture

This page gives a simple visual overview of how AI-901's main building blocks fit together.

Use these diagrams as memory anchors before practice tests. AI-901 rarely asks you to draw architecture, but it often asks which building block a scenario needs or where something fits in the pipeline.

## From catalog to application

```mermaid
flowchart LR
    CAT[Model Catalog]
    DEP[Deployment<br/>serverless API or managed compute]
    EP[Endpoint + Key]
    PG[Playground<br/>no-code testing]
    APP[Your App<br/>Foundry SDK]

    CAT --> DEP --> EP
    EP --> PG
    EP --> APP
```

Key idea: the catalog is for browsing; only a deployment is callable, and both the playground and your application call the same deployment.

Exam memory hook:

```text
Catalog    = browse and compare
Deployment = callable instance (your name for it)
Endpoint   = where to call
Key/Entra  = how to authenticate
```

## Inside a Foundry project

```mermaid
flowchart TD
    PROJ[Foundry Project]
    DEPS[Deployments]
    AGENTS[Agents]
    TOOLS[Foundry Tools<br/>Azure Speech, Content Understanding]
    DATA[Knowledge / Data]

    PROJ --> DEPS
    PROJ --> AGENTS
    PROJ --> TOOLS
    PROJ --> DATA
```

Key idea: the project is the workspace; deployments, agents, tools, and data all live inside it.

## Anatomy of an agent

```mermaid
flowchart TD
    AGENT[Agent]
    MODEL[Model<br/>a deployment]
    INST[Instructions<br/>standing system prompt]
    TOOLS2[Tools<br/>functions and APIs = actions]
    KNOW[Knowledge<br/>your data = grounding]

    MODEL --> AGENT
    INST --> AGENT
    TOOLS2 --> AGENT
    KNOW --> AGENT

    AGENT --> THREAD[Thread<br/>conversation session]
    THREAD --> RUN[Run<br/>one execution]
```

Exam memory hook:

```text
Tools     = what the agent can DO
Knowledge = what the agent can READ
Thread    = the conversation
Run       = one execution on the thread
```

## Grounding / RAG flow

```mermaid
flowchart LR
    Q[User question]
    IDX[Index of your content<br/>embeddings]
    CTX[Relevant passages]
    LLM[Deployed model]
    A[Grounded answer]

    Q --> IDX --> CTX --> LLM --> A
    Q --> LLM
```

Key idea: the question first retrieves relevant passages from your indexed content; the model answers from those passages. That is why grounding fixes hallucinations and fine-tuning does not.
