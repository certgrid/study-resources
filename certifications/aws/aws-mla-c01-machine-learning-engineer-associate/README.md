# AWS MLA-C01: Machine Learning Engineer Associate - Study Cheatsheet

The AWS Certified Machine Learning Engineer - Associate (MLA-C01) validates your ability to build, deploy, and operationalize ML solutions on AWS, spanning data preparation, model development, deployment/orchestration, and monitoring/security. It is aimed at engineers with at least one year of hands-on experience using Amazon SageMaker and related AWS services. The exam is 130 minutes, contains scored and unscored questions, and requires a scaled score of 720 out of 1000 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS MLA-C01 |
| Credential | AWS MLA-C01: Machine Learning Engineer Associate |
| Level | Associate |
| Practice mock length | ~65 questions |
| Duration | ~130 minutes |
| Passing score | 720 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Data Preparation for ML | ~29% |
| 2 | ML Model Development | ~23% |
| 3 | Deployment and Orchestration | ~27% |
| 4 | Monitoring and Security | ~21% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Data Preparation for ML

- Amazon S3 is the primary, most cost-effective store for large-scale raw ML training data in a data lake; it provides 11 nines of durability and integrates directly with SageMaker, Athena, and Glue.
- SageMaker Data Wrangler is a visual, low-code tool for data preparation and feature engineering; it offers 300+ built-in transforms and can export generated code as a SageMaker Pipelines step, Python script, or Feature Store job.
- SageMaker Feature Store has an online store for low-latency real-time inference lookups and an offline store (backed by S3, in Parquet) for batch training, ensuring the same feature definitions serve both training and inference.
- When creating a SageMaker Feature Group, --record-identifier-feature-name names the unique record column and an event-time feature is required to track record versions over time.
- Fit scalers and encoders on the training split only, then apply the fitted transform to validation and test sets; fitting on the full dataset causes data leakage and inflated metrics.
- Split data into training (teaches the model), validation (guides hyperparameter tuning and early stopping), and test (unbiased final generalization estimate) sets to avoid overfitting to evaluation data.

### Domain 2 - ML Model Development

- Amazon SageMaker is AWS's end-to-end managed ML platform covering data labeling, feature engineering, notebooks, distributed training, tuning, evaluation, model registry, and scalable inference; built-in algorithms train and deploy without managing servers.
- SageMaker Automatic Model Tuning (AMT) runs parallel/sequential training jobs using Bayesian optimization or random search over a defined hyperparameter space to maximize or minimize a target metric.
- In AMT, set HyperParameterTuningJobObjective Type to Minimize for losses/error metrics and Maximize for accuracy/F1; define search spaces with ContinuousParameter(0.001, 0.2), IntegerParameter, and CategoricalParameter(['relu','tanh']).
- Use precision (fraction of positive predictions correct), recall (fraction of actual positives captured), and F1 (their harmonic mean) for binary classification; AUC-ROC summarizes discrimination across thresholds.
- For imbalanced binary classification prefer F1 or AUC-PR (precision-recall) over plain accuracy, which is misleading when one class dominates.
- For regression use RMSE or MAE (error in the target's units) or R-squared (proportion of variance explained); RMSE penalizes large errors more heavily than MAE.

### Domain 3 - Deployment and Orchestration

- SageMaker real-time endpoints serve synchronous, low-latency predictions over a persistent HTTPS endpoint via the InvokeEndpoint API; suited to interactive applications needing millisecond responses.
- SageMaker Batch Transform scores large datasets in S3 offline, writes results back to S3, and terminates compute when done, avoiding the cost of a persistent endpoint; start it with aws sagemaker create-transform-job.
- SageMaker Asynchronous Inference queues requests, supports large payloads (up to 1 GB) and long processing times, writes results to S3, and can scale to zero when idle.
- SageMaker Serverless Inference provisions compute per request and scales to zero between requests, making it cost-effective for intermittent or bursty traffic with no charges when idle.
- SageMaker Multi-Model Endpoints host many models behind one endpoint, loading them on demand to share infrastructure and reduce cost when individual models receive sparse traffic.
- Before serving traffic you must create-model (container + artifacts + role) and then create-endpoint-config; the endpoint is then created/updated from that config.

### Domain 4 - Monitoring and Security

- SageMaker Model Monitor captures inference requests/responses (Data Capture), compares live distributions against a training baseline, and emits CloudWatch metrics and violation reports for data-quality, model-quality, bias, and feature-attribution drift.
- Data drift occurs when production input feature distributions diverge from the training distribution due to seasonality or upstream changes, degrading accuracy and signaling the need to retrain.
- Create a monitoring schedule with aws sagemaker create-monitoring-schedule, referencing a config that points to the computed baseline statistics and constraints.
- Attach a least-privilege IAM execution role to training jobs and endpoints granting only the needed S3 actions and bucket prefixes; AWS rotates temporary role credentials so no static keys live in code.
- Attach managed policies with aws iam attach-role-policy --role-name SageMakerExecRole --policy-arn arn:aws:iam::aws:policy/AmazonSageMakerFullAccess, but prefer scoped custom policies for production least privilege.
- SageMaker writes inference container stdout/stderr to CloudWatch Logs under /aws/sagemaker/Endpoints and training logs under /aws/sagemaker/TrainingJobs; retrieve them with aws logs get-log-events.

## Study tips

- Match the inference modality to the workload: real-time for low-latency interactive calls, Batch Transform for bulk offline scoring, Asynchronous for large payloads/long jobs, Serverless for intermittent traffic, and Multi-Model Endpoints to consolidate many sparsely used models.
- Watch for data leakage in data-prep questions: scalers, encoders, and imputers must be fit on training data only, then applied to validation and test.
- Default to least privilege and managed credentials: scoped IAM execution roles, KMS CMKs for encryption, VPC + network isolation, and CloudTrail for audit are the recurring 'most secure' answers.
- Pick metrics by problem type and balance: F1/AUC-PR for imbalanced classification, AUC-ROC for general discrimination, and RMSE/MAE/R-squared for regression - never plain accuracy on imbalanced data.
- Know the CLI specifics: create-model and create-endpoint-config precede create-endpoint; invoke-endpoint needs --endpoint-name/--content-type/--body; and EventBridge plus SageMaker Pipelines is the canonical drift-triggered retraining pattern.

---

Want the full breakdown? See the complete **[AWS MLA-C01 study guide](https://certgrid.app/study-guide/aws-mla-c01-machine-learning-engineer-associate)** and **[free practice questions](https://certgrid.app/practice/aws-mla-c01-machine-learning-engineer-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

