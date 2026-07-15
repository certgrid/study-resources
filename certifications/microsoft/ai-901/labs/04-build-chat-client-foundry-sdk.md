# Lab 04 - Build a Chat Client with the Foundry SDK

The exam includes light code recognition. Writing one tiny client yourself makes those questions easy.

## Time Needed

25-30 minutes.

## What You Will Learn

- How a Python app authenticates to a Foundry project
- How the deployment name, system prompt, and user prompt appear in code
- What comes back in a chat completion response

## AI-901 Concepts Covered

| Concept          | Where you see it in the lab                     |
| ---------------- | ----------------------------------------------- |
| Foundry SDK      | You install and use the Python client libraries |
| Endpoint and key | Your code connects using project credentials    |
| Deployment name  | Your code targets `chat-ai901-lab`              |
| Message roles    | You send system and user messages               |

## Before You Start

You need Python 3.10 or later and the deployment from Lab 02. Install the SDK packages:

```bash
pip install azure-ai-projects azure-identity
```

Sign in with the Azure CLI so `DefaultAzureCredential` works without keys in code:

```bash
az login
```

## Steps

### 1. Get your project endpoint

In the Foundry portal, open your project settings and copy the project endpoint URL. Set it as an environment variable:

```bash
set FOUNDRY_PROJECT_ENDPOINT=<your-project-endpoint>
```

### 2. Write the client

Save this as `chat.py`:

```python
import os
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

project = AIProjectClient(
    endpoint=os.environ["FOUNDRY_PROJECT_ENDPOINT"],
    credential=DefaultAzureCredential(),
)

chat = project.get_openai_client()
response = chat.chat.completions.create(
    model="chat-ai901-lab",
    messages=[
        {"role": "system", "content": "You are a concise study coach."},
        {"role": "user", "content": "Give me one tip for the AI-901 exam."},
    ],
)
print(response.choices[0].message.content)
```

### 3. Run and experiment

1. Run `python chat.py` and read the response.
2. Change the system prompt and rerun; the behavior changes without touching the user message.
3. Add a second user turn to the messages list and observe the model using the conversation context.

### 4. Map code to concepts

Say out loud (really) what each part is: endpoint, credential, deployment name, system role, user role. That mapping is exactly what the exam checks.

## Clean Up

Nothing new in Azure was created. Keep the deployment for labs 05-09.

## Success Criteria

You are done when you can explain:

- The four things the code needed to talk to the model
- Why the code says `chat-ai901-lab` and not the catalog model name
- Where you would change tone/behavior vs the actual question
