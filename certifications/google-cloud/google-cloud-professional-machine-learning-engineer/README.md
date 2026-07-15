# Google Cloud Professional Machine Learning Engineer - Study Cheatsheet

The Google Cloud Professional Machine Learning Engineer certification validates the ability to design, build, deploy, and operate ML solutions on Google Cloud, centered on Vertex AI. It targets engineers and data scientists who take models from prototype to production. The exam spans low-code AI (BigQuery ML, pretrained APIs, AutoML, Model Garden), data and model management, scaling custom training, serving and rollouts, pipeline automation, and monitoring.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Machine Learning Engineer |
| Credential | Google Cloud Professional Machine Learning Engineer |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Architecting Low-Code AI Solutions | ~13% |
| 2 | Collaborating to Manage Data and Models | ~14% |
| 3 | Scaling Prototypes into ML Models | ~18% |
| 4 | Serving and Scaling Models | ~20% |
| 5 | Automating and Orchestrating ML Pipelines | ~22% |
| 6 | Monitoring AI Solutions | ~13% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Architecting Low-Code AI Solutions

- In BigQuery ML, ML.ROC_CURVE returns recall, false positive rate, and the corresponding threshold across a full sweep of thresholds, unlike ML.CONFUSION_MATRIX which reports counts at one fixed threshold.
- Choose the BigQuery ML model type by task: LOGISTIC_REG for binary or multiclass labels (for example churn), LINEAR_REG for continuous targets, KMEANS for unsupervised clustering with no label, ARIMA_PLUS for single time-series forecasting, and DNN_CLASSIFIER for deep non-linear patterns over large labeled data.
- ML.EVALUATE reports quality metrics for the model type, including mean absolute error, mean squared error, and r2_score for a linear regression model.
- BigQuery ML preprocessing functions include ML.STANDARD_SCALER to standardize numeric columns, ML.BUCKETIZE for fixed ranges, and ML.QUANTILE_BUCKETIZE for quantile-based buckets.
- Model Garden provides a catalog of open-source and Google foundation models that can be browsed and deployed to a Vertex AI endpoint with minimal, guided setup.
- Supervised fine-tuning adapts a foundation model's behavior using a curated dataset of input and desired-output pairs.

### Domain 2 - Collaborating to Manage Data and Models

- In Vertex Explainable AI, sampled Shapley works for any model whether differentiable or not, integrated gradients suits differentiable models, and pixel-level integrated gradients is preferred over XRAI for low-contrast images such as X-rays where region segmentation performs poorly.
- A negative feature attribution value means that feature pulled the prediction opposite to the observed outcome, not that the value is missing or an error.
- Feature Store batch ingestion imports a full table or partition of precomputed feature values in bulk on a schedule, matching a nightly ETL job rather than a continuous stream.
- A feature view links a BigQuery table or view source to the online store and re-syncs on a configured recurring schedule; an entity is the object (such as a customer) whose feature values are tracked and served.
- Registered feature groups, cross-project IAM roles, and a synced feature view together let other teams safely discover and consume shared features.
- Dataset versions freeze an immutable snapshot of a non-tabular managed dataset's items and annotations so training pins to it for reproducibility; only text, image, and video (non-tabular) datasets support versions.

### Domain 3 - Scaling Prototypes into ML Models

- scikit-learn's Pipeline API is a lightweight choice for quickly prototyping preprocessing plus a simple classifier on a modest dataset before moving to heavier frameworks.
- Fault-tolerant Spot VM training combines regular checkpointing, catching the preemption notice to save state before shutdown, and configuring automatic resumption from the latest checkpoint.
- Distributed TensorFlow strategies: MirroredStrategy is synchronous all-reduce on one machine, MultiWorkerMirroredStrategy is the same across machines, and ParameterServerStrategy needs dedicated chief, worker, and parameter-server pools.
- Vertex AI automatically injects the TF_CONFIG environment variable into each worker so distributed TensorFlow strategies coordinate without manual cluster configuration.
- As worker count grows, communication overhead can outweigh added compute, causing diminishing or negative returns, so scaling must be validated rather than assumed linear.
- Accelerator selection: NVIDIA H100 gives the highest throughput and interconnect for the largest pretraining jobs, and A100 offers NVLink high-bandwidth GPU-to-GPU communication with greater memory for demanding distributed training.

### Domain 4 - Serving and Scaling Models

- Shadow testing runs a candidate model on mirrored production traffic while hiding its predictions from users, ideal for sensitive cases like fraud scoring where an untested model must not reach a customer.
- Standard Vertex AI online prediction does not scale below its configured minimum replica count, so a minReplicaCount of 1 or higher keeps replicas running and billing even when idle.
- Setting minReplicaCount to zero lets an endpoint scale fully down to save cost, but the next request after idle triggers a cold start while a replica provisions and loads the model.
- Batch prediction fits latency-tolerant workloads that avoid idle infrastructure cost, reads inputs from Cloud Storage or BigQuery only, and accepts accelerator_type and accelerator_count directly in the job request.
- Vertex AI batch prediction jobs record errors for individual malformed instances and continue rather than failing the whole job.
- Vertex AI injects AIP_STORAGE_URI so a custom serving container knows the Cloud Storage location of the model artifacts to load, and rawPredict passes the request body directly without the standard instances/parameters wrapper.

### Domain 5 - Automating and Orchestrating ML Pipelines

- Vertex AI Pipelines components do not retry automatically; a retry policy with a retry count and backoff must be explicitly configured on a task.
- Pipeline caching is evaluated per component from its own inputs and definition, so changing one component's inputs re-executes only it and its downstream steps while unchanged upstream components reuse cached outputs.
- Point-in-time correctness matters: joining labels to present-day feature values instead of their historical state leaks future information and inflates offline metrics unrealistically.
- A Kubeflow exit handler wraps the pipeline's tasks so a designated component always runs once the pipeline finishes, whether it succeeded or failed, ideal for a single notification or cleanup step.
- Component authoring: a typing.NamedTuple return type exposes several named outputs, base_image selects the starting image, packages_to_install adds pip dependencies at runtime, and dsl.importer registers an existing external file as a typed artifact.
- Artifacts are written under pipeline_root nested by run identifier and then by producing task name, and publishing versioned components to a shared Artifact Registry repository lets other teams reuse them.

### Domain 6 - Monitoring AI Solutions

- Vertex AI Model Monitoring is built for structured tabular features, depends on request-response logging to capture serving data, and adds storage and compute costs that scale with usage.
- Model Monitoring compares numerical feature distributions using Jensen-Shannon divergence and categorical feature distributions using L-infinity distance.
- Batch prediction monitoring is tied to the specific job's input data at execution time rather than running as a continuous background schedule like online-endpoint monitoring.
- Audit log types differ: Admin Activity logs (always on, cannot be disabled) show who performed a deployment, while Data Access logs, once enabled, show who has been invoking predictions.
- Focus monitoring on the subset of business-critical features rather than every column at maximum sensitivity, which keeps signal meaningful and controls cost and alert noise.
- Under severe class imbalance, the precision-recall curve is far more sensitive to minority-class performance than a ROC curve.

## Study tips

- Learn the BigQuery ML model-type-to-task mapping cold (LOGISTIC_REG, LINEAR_REG, KMEANS, ARIMA_PLUS, DNN_CLASSIFIER, BOOSTED_TREE), since many low-code questions hinge on picking the one model that fits the stated label and data shape.
- For any low-code scenario, default to the highest level tool that satisfies the requirement: pretrained API first, then AutoML or BigQuery ML, then custom training, and reach for custom code only when nothing simpler fits.
- Memorize the online-versus-batch prediction tradeoffs, including that standard online endpoints never scale below their minimum replica count while batch jobs run to completion and avoid idle cost.
- Distinguish the monitoring distance metrics (Jensen-Shannon for numerical, L-infinity for categorical) and the drift-versus-skew-versus-corrupted-pipeline decision, since the correct fix differs for each.
- When two options seem valid, favor the managed, event-driven, or reproducible choice (Eventarc over polling, dataset versions for reproducibility, dedicated service accounts over broad credentials), which matches Google's recommended patterns.

---

Want the full breakdown? See the complete **[Google Cloud Professional Machine Learning Engineer study guide](https://certgrid.app/study-guide/google-cloud-professional-machine-learning-engineer)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-machine-learning-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

