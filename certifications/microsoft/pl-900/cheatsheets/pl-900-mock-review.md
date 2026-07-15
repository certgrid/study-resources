# PL-900 Mock Review

27 original scenario drills in shuffled order, weighted roughly like the real exam: a couple from business value (5-10%) and six or seven from each of the four big domains (20-25% each). Read each scenario, commit to an answer out loud, then check the answer guide. These are original practice drills, not real exam questions.

How to use: first pass, answer all 27 without notes. Score yourself, then re-read the matching study note for every miss. Second pass a day later, only the ones you missed.

## Drills

1. An accounting team retypes data every night from a legacy desktop invoicing program with no API into a web system. The job must run after hours with nobody signed in to the machine. What should they build?

2. A warehouse team needs a phone app with barcode scanning, a camera control, and a fully custom screen layout designed around gloves-on use. Which Power Apps experience fits?

3. HR wants employees to ask questions like "how many vacation days can I carry over" inside Microsoft Teams and get answers drawn from the official policy library in SharePoint. What should HR build, and what makes the answers come from the policies?

4. Makers in the default environment keep building flows that copy Dataverse rows into a personal file-sharing service. The admin must stop business and personal connectors being combined. Which control?

5. A city council wants residents, who have no company accounts, to report potholes through a public website that saves reports into Dataverse. Which product?

6. Every Friday at 4 PM, a summary email of the week's open cases must go to the support team, whether or not anything changed that week. Which flow type?

7. Sales reps must see and edit their own opportunity rows but never see rows owned by reps in other regions. Which feature enforces this?

8. A help desk agent in Copilot Studio collects the caller's issue details, and must then actually create a ticket in the service desk system. What does the agent need?

9. A support department needs a case management app over many related Dataverse tables, with consistent forms, views, and a staged business process. Speed matters more than custom screen design. Which app type?

10. An admin wants to see which apps and flows are most used across the whole tenant and where capacity is going. Where does that answer live on the current exam?

11. A flow is described as: "When a Microsoft Forms response arrives, start an approval, then post the outcome to Teams." Which part is the trigger?

12. A team lead describes an employee onboarding problem in natural language and wants AI to propose the user roles, Dataverse tables, apps, and agents for the whole solution before anything is built. Which capability?

13. Leadership wants a central inventory of every agent in the organization, each with its own identity, access controls, and security oversight. Which product answers this?

14. A solution has passed testing and must now be promoted from the test environment to production in guided, repeatable steps. What is the right mechanism?

15. A cloud flow must read rows from a SQL Server that runs in the company's own server room. The maker added the SQL Server connector but the flow cannot reach the database. What is missing?

16. An internal development team wants to build a complex app in real code with web technologies, but the IT department insists it must keep Power Platform sign-in, connectors, and governance. What should the developers use?

17. An agent must walk every user through the same five fixed questions, in order, to log a facilities request, storing each answer along the way. Which agent building block?

18. A maker with no development background types a plain-language description of an inspection-tracking app and expects a working draft app connected to data. Which Power Platform capability delivers this?

19. Everyone in the company can open employee records, but the salary column must be visible only to the HR leadership team. Which security feature?

20. Supplier name, invoice date, and total must be extracted automatically from incoming PDF invoices and written to Dataverse without manual retyping. Which Power Automate capability?

21. A maker who published an agent wants to review how many sessions it handled this month, how many conversations were resolved versus abandoned, and which topics fired most. Where should the maker look?

22. After Copilot generates a draft app, the maker keeps chatting: "add a screen for managers," "make status a choice column," "highlight overdue items." Each prompt updates the working app. What is this way of building called?

23. New testers joining a project must be able to experiment freely without any chance of touching production apps or data. What should the admin create?

24. An agent built for employees in Teams turns out to be useful for customers too, and should also appear on the public website. What is the correct approach?

25. Copilot builds a cloud flow from the description "when a Dataverse row is added, post a message to Teams." Before the flow can run, what must the maker still do?

26. A maker describes a solution to Copilot, reviews the Dataverse tables and relationships it proposes, confirms them, and receives a generated app with forms and views built from those tables. Which app type was created?

27. Before relaunching an updated agent, the team runs a fixed battery of realistic sample questions against it and grades every response against expected answers. What is this practice called?

## Answer guide

1. Unattended desktop flow. No API means UI automation (RPA), and "nobody signed in" makes it unattended. A cloud flow is the tempting wrong answer, but cloud flows need a connector or API, which this legacy program does not have.

2. Canvas app. Custom pixel-level layout, camera control, and mobile use are the canvas signature. Model-driven is the trap: its UI is generated from the data model, so you cannot design the screens around gloves-on use.

3. A Copilot Studio agent with a SharePoint knowledge source, published to the Teams channel. Knowledge sources let the agent generate grounded answers from approved content. Topics are the tempting wrong choice, but topics script fixed conversation paths; they cannot answer open-ended policy questions from a document library.

4. A data loss prevention (DLP) policy. DLP classifies connectors into business, non-business, and blocked groups and prevents mixing them in one app or flow. A security role is the trap: roles control what users can do with Dataverse data, not which connectors can be combined.

5. Power Pages. External users without organizational accounts and a public website on Dataverse are the Power Pages pattern. Power Apps is the trap: it targets internal users, not anonymous or external website visitors.

6. Scheduled cloud flow. A timetable starts it, regardless of events. Automated flow is the trap: automated flows start when an event happens, and "whether or not anything changed" tells you there is no event to wait for.

7. A Dataverse security role with row-level (user-owned) scope, based on row ownership and business units. DLP is the trap here: DLP governs connector combinations, and column security hides columns, not other people's rows.

8. A tool: an agent flow, a connector action, or an MCP server if the service desk exposes one. Tools let agents act. A knowledge source is the trap: knowledge only lets the agent answer questions, it cannot create a ticket.

9. Model-driven app. Data-first, generated consistent UI, business process flows for stages, built on Dataverse. Canvas is the trap: it would mean hand-building every form and view the platform can generate for free.

10. Power Platform admin center analytics. Tenant-wide usage and capacity live in the admin center. Power BI is the tempting wrong answer, but Power BI was removed from the PL-900 outline; on the current exam it is not the correct answer to anything.

11. The Microsoft Forms response arriving ("when a response is submitted"). Whatever starts the flow is the trigger, and each cloud flow has exactly one. The approval is the trap: starting an approval is an action, one of the steps that runs after the trigger fires.

12. Plan designer. It turns a business problem description into a proposed solution plan: roles, requirements, tables, apps, agents, and automations. Copilot canvas app generation is the trap: it drafts one app, not a coordinated multi-asset solution.

13. Microsoft Agent 365. Registry, identity, access, security, and observability for agents across the organization. Copilot Studio is the trap: it builds and publishes individual agents; org-wide inventory and identity management is Agent 365.

14. Solutions deployed with Power Platform pipelines, arriving in production as a managed solution. Manual export and re-creation is the trap: the exam wants controlled ALM, and pipelines are the built-in guided mechanism.

15. The on-premises data gateway. Cloud flows need the gateway as a secure bridge to reach data hosted inside the company network. "Just fix the connector" is the trap: the SQL Server connector alone cannot cross into an on-premises network.

16. Code apps. Real code hosted and run through Power Apps, keeping platform sign-in, connectors, and governance. A custom connector is the trap: that wraps an API for low-code makers to call; it is not a way to build a whole coded app.

17. A topic with question nodes. Fixed questions in a fixed order are a scripted conversation path. Knowledge sources are the trap: they generate free-form answers and cannot guarantee the same five questions run in order.

18. Generative AI (Copilot) in Power Apps: describe the app and get a working draft to refine. "Hand it to developers" is the trap: PL-900 rewards the low-code, AI-assisted route for maker scenarios like this.

19. Column-level security (a column security profile) on the salary column. DLP is the classic trap: DLP has nothing to do with hiding data from users; it governs connector combinations.

20. Document automation. AI-powered document processing extracts fields from documents like invoices and pushes them into systems. A desktop flow is the trap: RPA retypes what a human sees, while document automation reads the documents themselves; and AI Builder as a named answer belongs to the older outline.

21. Copilot Studio usage and adoption analytics (sessions, outcomes, top topics). Power BI is the tempting answer for anything that sounds like "reports and dashboards," but Power BI is no longer in PL-900 scope; agent analytics are built into Copilot Studio.

22. The vibe experience: conversational, iterative building of AI-powered apps. Power Fx is the trap: Power Fx is the formula language a maker can still edit; the chat-to-refine loop itself is the vibe experience.

23. A sandbox environment (or another non-production environment). Environments are the isolation boundary for apps, flows, and data. A security role is the trap: roles limit actions inside an environment, but true separation from production means a separate environment.

24. Publish the same agent to an additional channel (the website). One agent can be published to multiple channels. Building a second agent is the trap: it doubles maintenance for no benefit; channels exist exactly for this.

25. Review the draft and sign in to (authenticate) the connections each connector needs, then test. "Nothing, Copilot did it all" is the trap: Copilot drafts the flow, but connections always run under an authenticated account the maker must provide.

26. A model-driven app, created with AI. Copilot proposed the data model first and generated the app from tables, forms, and views, which is the model-driven pattern. Canvas is the trap: canvas generation starts from the app experience, not from a confirmed data model.

27. Agent evaluations. Structured testing of answer quality against expected results, repeated before and after changes. Monitoring is the trap: monitoring shows live usage and adoption in production; evaluations grade answer quality in a controlled test.
