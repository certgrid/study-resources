# AZ-204: Azure Developer Associate - Study Cheatsheet

AZ-204 validates your ability to design, build, test, deploy, and maintain cloud applications and services on Microsoft Azure across compute, storage, security, monitoring, and service integration. It targets developers with one-to-two years of professional development experience and hands-on Azure SDK, CLI, and portal experience. You should be comfortable with at least one Azure-supported language (C#, Java, JavaScript/Node, Python) and with REST APIs, JSON, and authentication concepts.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-204 |
| Credential | AZ-204: Azure Developer Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Develop Azure Compute Solutions | ~21% |
| 2 | Develop for Azure Storage | ~20% |
| 3 | Implement Azure Security | ~18% |
| 4 | Monitor, Troubleshoot, and Optimize | ~19% |
| 5 | Connect to and Consume Azure Services | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Develop Azure Compute Solutions

- Azure App Service WebJobs of type Continuous start automatically with the app and run indefinitely (ideal for queue-processing loops); Triggered WebJobs run on demand or on a CRON schedule. Continuous WebJobs need 'Always On' enabled (not available on the Free/Shared tiers).
- Deployment slots let you deploy to a non-production slot (e.g., staging), warm it up and validate, then swap into production with no downtime; swap with preview applies production app settings first so you can verify before completing. Slots are a Standard tier or higher feature.
- App settings and connection strings can be marked as deployment-slot settings (sticky), so they stay with the slot and do not move during a swap.
- Azure Functions Consumption plan scales from zero and bills per execution, execution time (GB-seconds), and memory; it has a default 5-minute timeout (max 10). Premium plan adds pre-warmed (always-ready) instances to eliminate cold starts, VNet integration, and longer/unbounded timeouts.
- A Functions Timer trigger uses NCRONTAB with six fields {second} {minute} {hour} {day} {month} {day-of-week}; for example '0 0 3 * * *' runs daily at 03:00.
- Blob trigger default polling can lag several minutes detecting new/changed blobs; configuring Event Grid as the source gives near-real-time, low-latency triggering and scales better for high blob volumes.

### Domain 2 - Develop for Azure Storage

- Block blobs store unstructured data (files, images, video) up to roughly 190.7 TiB with current service versions; upload large content with Put Block to stage blocks then Put Block List to commit them in order.
- Blob access tiers are Hot (frequent access), Cool (infrequent, 30-day min), Cold (90-day min), and Archive (offline, 180-day min, rehydration required to read).
- Blob lifecycle management policies are rule-based JSON actions on the storage account that automatically move blobs between tiers (e.g., Hot to Cool after N days) or delete blobs/versions based on days since last modification or creation.
- Authorize blob data access with Microsoft Entra ID plus RBAC role assignments (preferred), Shared Access Signatures (SAS) with an expiry, or account/Shared Key; a user delegation SAS is signed with Entra ID credentials rather than the account key and is more secure.
- Copy a blob asynchronously server-side with BlobClient.StartCopyFromUri; the source can be in another account if accessible (anonymous or via SAS).
- Blob leases provide exclusive write/delete access; a finite lease must be 15 to 60 seconds, or you can request an infinite lease and release it explicitly.

### Domain 3 - Implement Azure Security

- App registration supported account types control sign-in scope; to allow work/school accounts from any tenant plus personal Microsoft accounts choose the multitenant + personal accounts option.
- Single-page browser apps must use the OAuth 2.0 authorization code flow with PKCE (the implicit flow is deprecated); PKCE protects against authorization-code interception.
- The OAuth 2.0 client credentials flow is for daemons/background services with no signed-in user; a confidential client authenticates as itself with a client secret or, more securely, a certificate.
- Delegated permissions act on behalf of a signed-in user; application permissions are used by apps running without a user and require admin consent. The token's aud (audience) claim identifies the intended recipient API.
- System-assigned managed identities are tied to a single resource's lifecycle (created/deleted with it); user-assigned managed identities are standalone resources that can be shared across multiple resources. Both eliminate stored credentials.
- Grant an App Service or Function a managed identity, then assign it Key Vault access so it can read secrets at runtime without credentials in code or config.

### Domain 4 - Monitor, Troubleshoot, and Optimize Azure Solutions

- Application Insights auto-collects request telemetry (incoming HTTP), dependency telemetry (outgoing calls to SQL/HTTP/storage), and exception telemetry (unhandled exceptions); use the Failures blade and Application Map to diagnose latency and errors.
- Track custom business events with TrackEvent (with properties and measurements), custom metrics with TrackMetric, and use the distributed Application Map to visualize dependency call durations.
- Query telemetry with Kusto Query Language (KQL); e.g., 'requests | where timestamp > ago(24h) | where duration > 5000' finds requests slower than 5 seconds, and '... | top 10 by duration desc' returns the slowest ten.
- Set up availability tests in Application Insights: a URL ping test for a simple endpoint check and a Standard test that supports HTTP verbs, custom headers, and SSL validation.
- Create metric alerts with static thresholds (or dynamic thresholds) on signals like response time, failures, or CPU to trigger action groups (email, SMS, webhook, Logic App).
- Build resiliency for transient faults (throttling, brief outages) with the Polly library: configure retry policies with exponential backoff, and use the CircuitBreaker policy to stop hammering a failing dependency.

### Domain 5 - Connect to and Consume Azure Services

- Azure Service Bus is an enterprise message broker (queues for point-to-point, topics/subscriptions for publish-subscribe) supporting AMQP 1.0 and HTTP/HTTPS, transactions, and dead-lettering.
- Enable Service Bus sessions to get guaranteed FIFO ordering for a group of related messages sharing a session ID; the EventProcessor/receiver locks a session so messages process in order.
- Service Bus subscription filters route messages: correlation filters match on system/user properties (e.g., Priority = High) efficiently, while SQL filters allow richer boolean expressions on message properties.
- Service Bus duplicate detection discards messages with a repeated MessageId within a configured time window; set maxDeliveryCount (e.g., 5) so messages exceeding the delivery attempts move to the dead-letter queue.
- Azure Event Grid is a discrete-event routing service for reactive, event-driven apps with advanced filtering (event type, subject prefix/suffix, numeric/string operators) and supports the CloudEvents v1.0 schema for interoperability.
- Event Grid delivers with exponential-backoff retries and supports dead-lettering to a storage account for events that cannot be delivered within the retry/TTL window; use one custom topic and differentiate consumers via event types and subject filtering.

## Study tips

- Watch for the 'right service' decision questions in domain 5: Service Bus = ordered/transactional enterprise messaging, Event Grid = discrete event routing with filtering, Event Hubs = high-volume telemetry streaming. Pick by the verbs in the scenario (ordering, FIFO, dead-letter vs. react-to-event vs. millions/second).
- Default to managed identities and Key Vault references for any 'no credentials in code/config' scenario; if asked which identity to use, system-assigned ties to one resource's lifecycle and user-assigned is shareable across resources.
- Memorize Functions plan trade-offs and the NCRONTAB six-field format. Remember Blob triggers can lag minutes on default polling but are near-real-time with Event Grid, a common 'reduce latency' answer.
- For Cosmos DB, the partition-key answer is almost always high cardinality, even distribution, and used in WHERE clauses; cross-partition queries cost more RUs, so single-partition queries that filter on the partition key are the optimization.
- Expect KQL snippets in monitoring questions; know that requests/dependencies/exceptions are separate tables, duration is in milliseconds, and ago() defines the time window. Pair Polly retry/circuit-breaker with transient-fault scenarios.

---

Want the full breakdown? See the complete **[AZ-204 study guide](https://certgrid.app/study-guide/az-204-azure-developer-associate)** and **[free practice questions](https://certgrid.app/practice/az-204-azure-developer-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

