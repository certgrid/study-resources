# PL-400: Power Platform Developer - Study Cheatsheet

The PL-400: Microsoft Power Platform Developer exam validates your ability to extend Power Platform with pro-code: Dataverse plug-ins, client scripting and PCF controls, custom connectors, and external integrations. It targets developers who design and build solutions on Dataverse, Power Apps, and Power Automate, and who manage application lifecycle. Expect 40-60 questions in 120 minutes, with a scaled passing score of 700.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | PL-400 |
| Credential | PL-400: Power Platform Developer |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Application Lifecycle Management | ~23% |
| 2 | Extend the User Experience | ~19% |
| 3 | Extend the Platform | ~22% |
| 4 | Develop Integrations | ~18% |
| 5 | Extend the User Experience and Platform | ~17% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Application Lifecycle Management

- Prefer low-code (business rules, calculated/rollup columns, flows) over pro-code; only write plug-ins when requirements exceed declarative capabilities (complex server logic, integrations, strict performance needs).
- Solutions are the unit of packaging: develop in unmanaged solutions, deploy managed solutions downstream. Managed solutions are read-only in target environments and support clean uninstall.
- Never hardcode secrets in code or solutions; store them as environment variables backed by Azure Key Vault references, never embedding the raw secret value.
- Use the Power Platform CLI (pac) for ALM: pac auth create --url, pac solution export/import, pac solution unpack/pack with --packagetype Both|Managed|Unmanaged.
- pac solution import --path MySolution.zip --async --max-async-wait-time 60 imports asynchronously; pac solution unpack --packagetype Both produces source you can commit to version control.
- Automate deployments with Power Platform Build Tools for Azure DevOps or the Power Platform GitHub Actions; these wrap pac CLI tasks like who-am-i, export, import, and pack/unpack.

### Domain 2 - Extend the User Experience

- JavaScript is the only supported language for client-side logic in model-driven forms; it runs in the browser on events like OnLoad, OnChange, and OnSave via the Client API.
- Retrieve the form context with executionContext.getFormContext(); pass executionContext as the first parameter to handlers and avoid the deprecated global Xrm.Page.
- Common Client API calls: formContext.getAttribute("telephone1").setRequiredLevel("required"); formContext.getControl("creditlimit").setVisible(false); formContext.data.entity.getId() returns the record GUID.
- Power Apps Component Framework (PCF) builds reusable code components in TypeScript/React for both canvas and model-driven apps; the framework calls init, updateView, getOutputs, and destroy in the control lifecycle.
- In a PCF dataset component, request only needed columns and use delegable queries with filters/Top so paging happens server-side; minimize work inside updateView since it is called frequently.
- Calculated columns automatically compute and store a value when a record is created or updated, with no code; they are the lowest-maintenance choice when the formula fits supported functions.

### Domain 3 - Extend the Platform

- Dataverse plug-ins are .NET assemblies that run server-side on the event pipeline in response to messages (Create, Update, Delete, Retrieve, RetrieveMultiple, custom messages).
- The pipeline has stages: pre-validation (stage 10, outside the database transaction), pre-operation (stage 20, inside the transaction before commit), and post-operation (stage 40, after commit).
- The platform passes IPluginExecutionContext carrying InputParameters (including the Target entity), OutputParameters, pre/post entity images, MessageName, Depth, and the initiating/user IDs.
- Throw InvalidPluginExecutionException in pre-validation or pre-operation to cancel an operation and surface a validation error to the user.
- Plug-ins run in a sandbox with a hard 2-minute execution limit and restricted resources; offload long-running or heavy integration work to async flows, async plug-ins, or Azure Functions.
- Register plug-in steps and images with the Plug-in Registration Tool (or pac plugin), specifying message, primary entity, stage, execution mode (sync/async), and filtering attributes.

### Domain 4 - Develop Integrations

- Use asynchronous processing (async plug-ins, async flows) for long-running or non-blocking work so it does not delay the user's transaction; use synchronous logic when results must be enforced before save.
- Power Automate cloud flows (automated, instant, scheduled) orchestrate processes across hundreds of connectors with low-code conditional logic, approvals, and event triggers.
- Server-side validation that must apply regardless of client (web, mobile, API, integrations) belongs in a synchronous pre-operation or pre-validation plug-in, because client-side JavaScript can be bypassed.
- Register an asynchronous service endpoint to Azure Service Bus or Event Hub via the event pipeline for durable, decoupled messaging with built-in retry and dead-lettering.
- Use Dataverse webhooks to POST event data to an external HTTPS endpoint synchronously or asynchronously; Service Bus is preferred for high-volume, guaranteed delivery.
- Honor HTTP 429 (Too Many Requests) by reading the Retry-After header and applying exponential backoff with jitter before retrying.

### Domain 5 - Extend the User Experience and Platform

- Custom connectors wrap a REST API so Power Apps and Power Automate can consume it; you can define them from an OpenAPI (Swagger) 2.0 JSON definition, a Postman collection, or from scratch.
- Custom connector definitions include actions/triggers, authentication, and policies; configure pagination and define the environment scope in which the connector is available.
- Define connector authentication (e.g., OAuth 2.0) in the connector itself rather than embedding API keys in flows; supported types include No auth, API key, Basic, and OAuth 2.0.
- The Dataverse Web API is OData v4 over REST and is the standard interface for external apps to query and manipulate data using OAuth 2.0 bearer tokens.
- Send the OAuth token in the Authorization header as 'Bearer <token>'; never embed user credentials in requests.
- Application users are non-interactive identities (service principals) for app/integration access; assign them scoped security roles so access is not tied to a person's credentials or license.

## Study tips

- Master the plug-in event pipeline cold: memorize the stages (pre-validation 10, pre-operation 20, post-operation 40), sync vs async, and when each is appropriate. This single topic spans multiple domains.
- Know the pac CLI verbs and key flags by heart (auth create, solution export/import/pack/unpack, --packagetype, --async); the exam tests exact command syntax.
- When a question asks for the lowest-effort solution, follow the ladder: business rule or calculated/rollup column first, then flow, then JavaScript/PCF, then plug-in, then Azure Function - choose the least code that meets the requirement.
- For integration questions, decide async vs sync by whether work is long-running and whether it must block the save; pick Service Bus/webhooks for external messaging and always handle 429 with Retry-After and backoff.
- For security questions, default to OAuth 2.0 with a Microsoft Entra app registration mapped to a least-privilege Dataverse application user, and store secrets in Key Vault via environment variables - never hardcode credentials.

---

Want the full breakdown? See the complete **[PL-400 study guide](https://certgrid.app/study-guide/pl-400-power-platform-developer)** and **[free practice questions](https://certgrid.app/practice/pl-400-power-platform-developer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

