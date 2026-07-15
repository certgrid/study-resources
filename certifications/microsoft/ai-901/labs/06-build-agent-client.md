# Lab 06 - Build a Lightweight Agent Client

The exam expects you to recognize how an application talks to an agent: create a thread, add a message, run the agent, read the reply.

## Time Needed

20-25 minutes.

## What You Will Learn

- The thread / message / run pattern for agents
- How a client references an existing agent
- How this differs from the plain chat completion call in Lab 04

## AI-901 Concepts Covered

| Concept  | Where you see it in the lab                   |
| -------- | --------------------------------------------- |
| Agent ID | Your code references the portal-built agent   |
| Thread   | You create a conversation session             |
| Run      | You execute the agent on the thread           |
| Messages | You add user input and read the agent's reply |

## Steps

### 1. Find the agent ID

In the Foundry portal, open your `study-buddy` agent and copy its ID.

### 2. Write the client

Save this as `agent_chat.py` (same environment as Lab 04):

```python
import os
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

project = AIProjectClient(
    endpoint=os.environ["FOUNDRY_PROJECT_ENDPOINT"],
    credential=DefaultAzureCredential(),
)

agents = project.agents
thread = agents.threads.create()
agents.messages.create(
    thread_id=thread.id,
    role="user",
    content="Name two responsible AI principles from my notes.",
)
run = agents.runs.create_and_process(
    thread_id=thread.id,
    agent_id="<your-agent-id>",
)
for message in agents.messages.list(thread_id=thread.id):
    print(message.role, ":", message.content)
```

### 3. Run and observe

1. Run the script and read the agent's answer.
2. Add a follow-up message to the same thread and run again: the agent remembers the thread context.

### 4. Compare with Lab 04

| Lab 04 chat completion          | Lab 06 agent client                         |
| ------------------------------- | ------------------------------------------- |
| You send the whole message list | The thread stores the conversation          |
| No tools or knowledge           | Agent brings instructions, tools, knowledge |
| One request, one response       | A run may take multiple steps               |

## Clean Up

Nothing new in Azure was created beyond threads, which are lightweight. Full cleanup happens in Lab 11.

## Success Criteria

You are done when you can explain:

- The order: thread, message, run, read messages
- Why the agent remembered your follow-up question
- Two things the agent client gets that the plain chat client does not
