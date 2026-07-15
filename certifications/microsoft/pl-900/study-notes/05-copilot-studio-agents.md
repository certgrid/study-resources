# 05 - Describe Features and Capabilities of Agents in Microsoft Copilot Studio

This domain is worth 20-25% of the exam and is the newest part of PL-900. It covers how agents are built in Microsoft Copilot Studio (use cases, topics, knowledge sources, tools including MCP servers and agent flows, publishing to channels) and how they are managed (Microsoft Agent 365, monitoring usage and adoption, and agent evaluations).

## Mental model

An agent is a new team member you configure instead of hire. Knowledge sources are the documents you hand it to read. Topics are the scripts it follows for specific conversations. Tools are the systems you give it access to so it can actually do things (create tickets, look up orders). Channels are the desks where users can find it (Teams, a website, Microsoft 365 Copilot). Agent 365 is HR for agents: registering, securing, and overseeing them across the organization. Evaluations are its performance reviews.

| Scenario keyword                                       | Likely concept                           |
| ------------------------------------------------------ | ---------------------------------------- |
| Guided, scripted conversation path with specific steps | Topic                                    |
| Answer questions from a website or SharePoint docs     | Knowledge source                         |
| Agent performs an action in another system             | Tool (agent flow, MCP server, connector) |
| Make the agent available in Teams or on a website      | Publish to a channel                     |
| Manage and secure many agents across the org           | Microsoft Agent 365                      |
| Is the agent being used? By whom? How often?           | Monitoring usage and adoption            |
| Test answer quality against expected results           | Agent evaluations                        |

## What agents are for

Microsoft Copilot Studio is the low-code product for building agents: AI-powered assistants that converse with users, answer from approved knowledge, and take actions.

| Use case category     | Example                                                                          |
| --------------------- | -------------------------------------------------------------------------------- |
| Employee self-service | HR agent answers leave-policy questions from official documents                  |
| Customer support      | Website agent answers product questions and creates support cases                |
| IT help desk          | Agent troubleshoots common issues and raises tickets                             |
| Process front-end     | Agent collects details conversationally, then hands to a flow                    |
| Autonomous work       | Agents can also act on events without a user chatting (agent flows and triggers) |

Choose an agent when people need conversational answers or actions; choose a plain Power Automate flow when a process should run in the background with no conversation.

## Building agents

### Topics: conversation paths

A topic is a designed conversation path for a specific subject.

| Topic element   | Meaning                                                             |
| --------------- | ------------------------------------------------------------------- |
| Trigger phrases | Example utterances that tell the agent when this topic applies      |
| Nodes           | Steps in the conversation: messages, questions, conditions, actions |
| Questions       | Collect input from the user and store it in variables               |
| Conditions      | Branch the conversation based on answers                            |

Use topics when the conversation must be predictable and controlled, such as collecting the exact fields needed to open a case. Generative answers from knowledge handle open-ended questions; topics handle structured ones. Copilot can generate topics from a natural-language description.

### Knowledge sources

Knowledge sources let an agent answer questions with generative AI grounded in approved content, without a maker scripting every answer.

| Knowledge source type     | Example                                    |
| ------------------------- | ------------------------------------------ |
| Public websites           | Your company's public documentation site   |
| SharePoint content        | HR policy library                          |
| Uploaded files            | PDF manuals and guides                     |
| Dataverse                 | Business records the agent can answer from |
| Connected enterprise data | Other systems connected as knowledge       |

Key idea: knowledge makes the agent informative. Grounding in approved sources keeps answers based on your content rather than the open model alone.

### Tools: letting agents act

Tools give agents the ability to do things, not just answer.

| Tool type                | What it provides                                                                                           |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Agent flows              | Flows (Power Automate style) the agent runs to perform multi-step actions                                  |
| MCP servers              | Model Context Protocol servers that expose external systems' tools and data to the agent in a standard way |
| Connectors               | Direct actions against services through Power Platform connectors                                          |
| Prompts / custom actions | Task-specific AI or API actions the agent can call                                                         |

| If the agent must...                            | Give it...                         |
| ----------------------------------------------- | ---------------------------------- |
| Create a ticket, send an email, update a record | An agent flow or connector action  |
| Use an external system that publishes MCP tools | An MCP server                      |
| Only answer questions from documents            | Knowledge sources (no tool needed) |

### Publishing to channels

Publishing makes the agent available to users. One agent can be published to multiple channels.

| Channel                                         | Audience                          |
| ----------------------------------------------- | --------------------------------- |
| Microsoft Teams and Microsoft 365 Copilot       | Employees inside the organization |
| Custom website                                  | Customers and visitors            |
| Other channels (such as messaging integrations) | Users where they already chat     |

Flow to remember: build, test in the built-in test pane, then publish to channels.

## Managing agents

### Microsoft Agent 365

Microsoft Agent 365 is how organizations manage agents at scale, treating them like a workforce that needs identity, security, and oversight.

| Capability              | Meaning                                                                 |
| ----------------------- | ----------------------------------------------------------------------- |
| Agent registry          | Central inventory of the organization's agents                          |
| Identity and access     | Agents get identities and permissions, managed like users (Entra-based) |
| Security and governance | Apply organizational controls and protection to agents                  |
| Observability           | Understand what agents are doing across Microsoft 365 tools             |

Exam cue: "manage, secure, and inventory all the agents across the company" is Microsoft Agent 365; "build one agent" is Copilot Studio.

### Monitoring usage and adoption

Copilot Studio provides analytics so makers and admins can see whether agents work and are used.

| Question                                 | Where the answer comes from              |
| ---------------------------------------- | ---------------------------------------- |
| How many sessions and users?             | Agent usage analytics in Copilot Studio  |
| Are conversations resolved or abandoned? | Session outcome and engagement analytics |
| Which topics fire most?                  | Topic-level analytics                    |
| Tenant-wide oversight                    | Power Platform admin center              |

### Agent evaluations

Evaluations test agent quality in a structured way instead of relying on ad-hoc chats.

| Evaluation idea                 | Meaning                                                       |
| ------------------------------- | ------------------------------------------------------------- |
| Test with sample questions      | Run sets of realistic questions against the agent             |
| Compare to expected answers     | Judge whether responses meet expectations                     |
| Iterate                         | Fix knowledge, topics, or tools where the agent scored poorly |
| Repeat before and after changes | Catch regressions when the agent is updated                   |

Memory hook: monitoring tells you what is happening in production; evaluations tell you how good the answers are before and after changes.

## Common confusions

| Confusion                              | Correct idea                                                                                |
| -------------------------------------- | ------------------------------------------------------------------------------------------- |
| Topic vs knowledge source              | Topic is a scripted conversation path; knowledge lets AI answer open questions from content |
| Knowledge vs tools                     | Knowledge answers questions; tools take actions                                             |
| Agent flow vs regular cloud flow       | Agent flows are run by an agent as a tool; cloud flows run on triggers/schedules            |
| Copilot Studio vs Microsoft Agent 365  | Build and publish agents vs manage and secure agents across the organization                |
| Publish vs test                        | The test pane is for the maker; publishing puts the agent on channels for users             |
| Copilot Studio vs Power Virtual Agents | Same product line; the current name is Microsoft Copilot Studio                             |
| Monitoring vs evaluations              | Live usage and adoption data vs structured quality testing of responses                     |

## Exam traps

| Trap                                                             | Why people miss it                                                             |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| "Agent should answer from our docs" answered with topics         | Open-ended Q and A from content is knowledge sources                           |
| "Agent must actually reset the password" answered with knowledge | Actions need tools (agent flow, connector, MCP server)                         |
| Assuming one agent = one channel                                 | One agent can publish to multiple channels                                     |
| Using Power Automate alone for a conversational assistant        | Conversations are Copilot Studio; flows have no chat interface                 |
| Treating MCP servers as a knowledge source                       | MCP servers expose tools and data for the agent to act with                    |
| Ignoring governance because agents are "just bots"               | Agent 365 exists exactly because agents need identity, security, and oversight |

## Mini scenarios

| Scenario                                                                                        | Best answer                                                                      |
| ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Employees should ask an assistant in Teams about expense policy, answered from SharePoint.      | Agent with a SharePoint knowledge source, published to Teams                     |
| The agent must walk users through exactly four questions to log a facilities request.           | A topic with question nodes                                                      |
| After collecting details, the agent should create a ticket in the service desk system.          | A tool: agent flow or connector action (or MCP server if the system exposes one) |
| The company wants an inventory of all agents with identity and security controls.               | Microsoft Agent 365                                                              |
| The maker wants to know how many users chatted with the agent this month and what was resolved. | Usage and adoption analytics in Copilot Studio                                   |
| Before relaunch, the team runs a battery of sample questions and grades the responses.          | Agent evaluations                                                                |
| The same agent should also be available on the public website.                                  | Publish the agent to the website channel                                         |

## Check yourself

1. What is the difference between a topic and a knowledge source?
2. Name three types of knowledge sources an agent can use.
3. What are tools in an agent, and name two kinds.
4. What is an MCP server used for in Copilot Studio?
5. How does an agent become available to users in Microsoft Teams?
6. What is Microsoft Agent 365 for?
7. What is the difference between monitoring an agent and evaluating an agent?
8. When should you build a Copilot Studio agent instead of a Power Automate flow?

## Answer guide

1. A topic is a designed conversation path triggered by phrases; a knowledge source lets the agent generate answers from approved content without scripting.
2. Any three: public websites, SharePoint content, uploaded files, Dataverse, other connected enterprise data.
3. Tools let the agent take actions; kinds include agent flows, MCP servers, and connector actions.
4. It exposes an external system's tools and data to the agent through the Model Context Protocol standard so the agent can use them.
5. The maker publishes the agent to the Teams channel.
6. Managing agents at scale across the organization: registry/inventory, identity and access, security, governance, and observability.
7. Monitoring shows real usage and adoption in production; evaluations are structured tests of answer quality against expectations.
8. When users need a conversation (questions answered, details collected interactively); use a flow when the process runs in the background without dialogue.
