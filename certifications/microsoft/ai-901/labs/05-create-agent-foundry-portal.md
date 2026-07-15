# Lab 05 - Create an Agent in the Foundry Portal

Agents are the headline addition in AI-901 vs the old AI-900. This lab builds a single-agent solution with no code.

## Time Needed

25 minutes.

## What You Will Learn

- What instructions, tools, and knowledge each add to an agent
- How to create and test a single agent in the portal
- When an agent is the right choice over a plain prompt

## AI-901 Concepts Covered

| Concept      | Where you see it in the lab                        |
| ------------ | -------------------------------------------------- |
| Agent        | You create a goal-driven assistant                 |
| Instructions | You write the agent's standing behavior            |
| Knowledge    | You ground the agent in a file you upload          |
| Tools        | You see where actions like function calling attach |
| Thread       | Your test conversation is a thread                 |

## Steps

### 1. Create the agent

1. In your project, open the **Agents** area and create a new agent.
2. Pick your `chat-ai901-lab` deployment as the model.
3. Name it `study-buddy`.

### 2. Write the instructions

```text
You are a study assistant for the AI-901 exam. Answer only questions
about AI and Azure AI topics. Keep answers under 100 words. If the
answer is in the attached notes, prefer them over general knowledge.
```

Instructions are the agent's system prompt; behavior rules live here.

### 3. Attach knowledge

1. Create a small text file with a few facts (for example, your own notes on the six responsible AI principles).
2. Upload it as a knowledge source for the agent.
3. This grounds the agent: it can now answer from your data.

### 4. Look at the tools options

Browse the available tool types (function calling, and any built-in tools listed). You do not need to wire one up; recognize that tools are how an agent takes actions, while knowledge is what it reads.

### 5. Test in the portal

1. Open the agent playground and ask something covered by your uploaded file. The answer should use it.
2. Ask an off-topic question. The instructions should keep the agent on topic.
3. Notice your conversation is a thread; each response generation is a run.

## Clean Up

Keep the agent for Lab 06. Delete the uploaded file and agent in Lab 11.

## Success Criteria

You are done when you can explain:

- The difference between instructions, tools, and knowledge
- Why this task needed an agent only if steps/tools/grounding matter
- What thread and run mean in the agent playground
