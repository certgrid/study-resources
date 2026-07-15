# Lab 08 - Create an Agent in Copilot Studio

Agents are 20-25% of PL-900. In this lab you create one in Microsoft Copilot Studio, give it a knowledge source and a topic, test it, and see where tools and channels fit.

## Time Needed

30-40 minutes.

## What You Will Learn

- How to create an agent with a description
- How knowledge sources answer open questions
- How a topic scripts a specific conversation
- Where tools (agent flows, MCP servers) and channels appear
- What the analytics area tracks

## PL-900 Concepts Covered

| Concept          | Where you see it in the lab                            |
| ---------------- | ------------------------------------------------------ |
| Agent            | You create one in Copilot Studio                       |
| Knowledge source | You add a public website the agent answers from        |
| Topic            | You build a scripted conversation path                 |
| Tools            | You locate where agent flows and MCP servers are added |
| Channels         | You see the publish options (Teams, website, and more) |
| Analytics        | You find usage and adoption reporting                  |

## Licensing and Cost Notes

Copilot Studio offers a free trial. Sign in at `copilotstudio.microsoft.com` with the same account as your other labs and start the trial if prompted. Trials expire; nothing in this lab creates paid charges.

## Steps

### 1. Create the agent

1. Go to `copilotstudio.microsoft.com` and check the environment picker.
2. Select **Create** and describe the agent, for example:

```text
An IT help agent that answers questions about Microsoft Power
Platform and helps employees log equipment issues.
```

3. Review the generated name, description, and instructions, then create it.

### 2. Add a knowledge source

1. Open the **Knowledge** section of your agent.
2. Add a public website as knowledge, for example the Microsoft Power Platform documentation site.
3. In the test pane, ask: "What is a canvas app?" The agent should answer from the knowledge with generative AI, citing the source.

### 3. Build a topic

1. Open **Topics** > add a new topic (describe it to Copilot or build manually).
2. Trigger phrases: "report an equipment issue", "my laptop is broken".
3. Add nodes: a question asking which device, a question asking for a description, then a message confirming "Your issue has been recorded."
4. Test in the test pane: type "report an equipment issue" and walk the scripted path. Notice how different this controlled path feels from the generative knowledge answer.

### 4. Look at tools (no build required)

1. Open the **Tools** (actions) area of the agent.
2. Note what could be added: agent flows (to create a Dataverse row for the issue), connector actions, prompts, and MCP servers. This is how the agent would act instead of only chat.

### 5. Look at channels and analytics

1. Open **Channels**: see Teams, Microsoft 365 Copilot, custom website, and other options. Publishing pushes the agent to the selected channels.
2. Open **Analytics**: this is where sessions, engagement, and outcomes appear once the agent has real users. Evaluations complement this by testing answer quality with prepared question sets.

### 6. Publish (optional)

If your trial allows, publish the agent and try it on the demo website channel.

## Clean Up

Delete the agent if you are finished with it, or keep it until Lab 09. Let the trial lapse; it does not convert to paid automatically.

## Success Criteria

You are done when you can explain:

- The difference you saw between a knowledge answer and a topic path
- What tools would let this agent do that knowledge cannot
- What publishing to a channel means
- Where usage analytics live, and what evaluations add on top
