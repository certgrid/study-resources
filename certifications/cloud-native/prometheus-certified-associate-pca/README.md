# Prometheus Certified Associate (PCA) - Study Cheatsheet

The Prometheus Certified Associate (PCA) is a vendor-neutral CNCF exam that validates foundational observability and Prometheus skills, including metrics fundamentals, PromQL, exporters, instrumentation, alerting, and dashboards. It is a 90-minute, multiple-choice exam aimed at developers, SREs, and platform engineers who deploy or query Prometheus and want to prove practical, hands-on monitoring knowledge.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Prometheus Certified Associate (PCA) |
| Credential | Prometheus Certified Associate (PCA) |
| Level | Associate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Observability Concepts | ~12% |
| 2 | Prometheus Fundamentals | ~24% |
| 3 | PromQL | ~22% |
| 4 | Instrumentation and Exporters | ~22% |
| 5 | Alerting and Dashboards | ~19% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Observability Concepts

- Observability is built on three pillars: metrics (numeric time-series), logs (discrete timestamped event records carrying rich context), and traces (following one request across services to locate latency or errors).
- Prometheus is a metrics-based, time-series monitoring and alerting system that pulls (scrapes) metrics over HTTP from target endpoints, conventionally /metrics.
- A time series is uniquely identified by its metric name plus its full set of label key/value pairs; changing any label value creates a new, distinct series.
- Cardinality is the number of distinct time series a metric produces across all its label-value combinations; high-cardinality labels (user IDs, request IDs, raw URLs) explode memory and TSDB series counts.
- An SLI (Service Level Indicator) is a measured metric such as availability or latency; an SLO is the target you commit to for that SLI; the error budget is the allowed unreliability (e.g., 0.5% of requests) that can be spent before the SLO is breached.
- The USE method inspects Utilization, Saturation, and Errors for each resource; it is best suited to resources like CPU, memory, disk, and network.

### Domain 2 - Prometheus Fundamentals

- Prometheus uses a pull model: it scrapes HTTP /metrics endpoints exposed by instrumented apps or exporters, so targets do not need to know any collector address.
- The built-in up metric is 1 if the last scrape of a target succeeded and 0 if it failed, making it the primary target-health signal.
- Key startup flags: --config.file=/etc/prometheus/prometheus.yml sets the config, --storage.tsdb.retention.time=15d sets local retention (15d is the default), and --web.enable-lifecycle enables the /-/reload and /-/quit HTTP endpoints.
- With --web.enable-lifecycle on, reload config without restarting via curl -X POST http://localhost:9090/-/reload; validate config first with promtool check config prometheus.yml.
- global.scrape_interval (commonly 15s) sets the default scrape frequency; shorter intervals improve resolution and detection speed but increase storage, CPU, and network cost.
- Dynamic targets come from service discovery (kubernetes_sd_config, consul, ec2, etc.) combined with relabel_configs in the scrape job to filter, rename, and set labels.

### Domain 3 - PromQL

- Filter a series with label matchers: = (exact), != (not equal), =~ (regex match), and !~ (regex not match), e.g., http_requests_total{job="api",status=~"5.."}.
- rate() computes the per-second average rate of a counter over a range, is counter-reset aware, and extrapolates to the window edges; it is the standard choice for smoothed dashboards and alert thresholds.
- irate() computes the instantaneous per-second rate from only the last two samples in a range and is best for fast-moving, volatile graphs, not alerting.
- Choose a rate() range window at least about 4x the scrape_interval so it always contains multiple samples; with fewer than two samples in the window rate() returns no result.
- increase() gives the total rise of a counter over a range (rate multiplied by the window) and is convenient for human-readable counts.
- Aggregation operators (sum, avg, min, max, count, stddev, topk, bottomk, quantile, count_values, group) collapse an instant vector, optionally grouped with by(...) or without(...).

### Domain 4 - Instrumentation and Exporters

- Direct instrumentation uses a Prometheus client library (Go, Java, Python, etc.) to define and expose metrics on a /metrics endpoint that Prometheus scrapes.
- The four core metric types are Counter (monotonically increasing, e.g., requests_total), Gauge (goes up and down, e.g., temperature), Histogram (bucketed observations with _bucket/_sum/_count), and Summary (client-side quantiles).
- Prefer histograms over summaries when you need to aggregate across instances, because histogram bucket counts are additive and percentiles are computed at query time with histogram_quantile.
- Follow naming conventions: use base units (seconds, bytes), append the _total suffix to counters, and keep a consistent label set, since a metric name must always carry the same label names or collection errors occur.
- Avoid high-cardinality labels such as user IDs, request IDs, or raw URLs; normalize URLs into a bounded route/handler label like /users/:id to prevent a cardinality explosion and possible OOM.
- node_exporter exposes host/OS metrics (CPU, memory, disk, filesystem, network) and listens on :9100 by default.

### Domain 5 - Alerting and Dashboards

- Alerting rules live in Prometheus rule files and are evaluated by Prometheus itself; when an expression matches, Prometheus sends alerts to Alertmanager.
- Alertmanager handles routing to receivers (email, Slack, PagerDuty, webhook), plus grouping, deduplication, silences, and inhibition; Prometheus only generates the alerts.
- The for clause requires the alert condition to stay true continuously for a sustained duration before the alert transitions from pending to firing, which reduces flapping.
- While an alert is pending, any single evaluation that returns no matching sample resets it to inactive and restarts the for timer.
- Recording rules precompute frequently used or expensive PromQL expressions into new time series, e.g., a success-ratio series, making dashboards and alerts faster and consistent.
- evaluation_interval controls how often both recording and alerting rules are evaluated, and is configured globally (independent of scrape_interval).

## Study tips

- Master the difference between rate() (smoothed, counter-reset aware, for alerts and dashboards) and irate() (last two samples, for volatile graphs), and remember a range window should be at least ~4x the scrape_interval so it always holds multiple samples.
- Be fluent in histogram_quantile with sum by (le) for percentiles, and know why histograms aggregate across instances while summary quantiles do not - this distinction is heavily tested.
- Memorize Alertmanager timing semantics: group_wait vs group_interval vs repeat_interval, plus what inhibition, silences, and grouping each do.
- Know the standard exporters and their default ports/roles (node_exporter :9100, blackbox_exporter probe model with ?target=, cAdvisor, kube-state-metrics, snmp_exporter) and the relabeling that wires probe exporters together.
- Practice reading prometheus.yml: scrape_configs, relabel_configs, service discovery, sample_limit, honor_labels, and the lifecycle flags (--web.enable-lifecycle, /-/reload), since config interpretation questions are common.

---

Want the full breakdown? See the complete **[Prometheus Certified Associate (PCA) study guide](https://certgrid.app/study-guide/prometheus-certified-associate-pca)** and **[free practice questions](https://certgrid.app/practice/prometheus-certified-associate-pca)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

