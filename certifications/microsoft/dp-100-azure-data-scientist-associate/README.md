# DP-100: Azure Data Scientist Associate - Study Cheatsheet

DP-100 (Azure Data Scientist Associate) validates your ability to design machine learning solutions, prepare data, train and evaluate models, and operationalize them with Azure Machine Learning. It targets data scientists and ML engineers who use the Azure ML SDK v2, CLI v2, and studio to run experiments and deploy models. Expect heavy emphasis on the Azure ML workspace, compute, jobs, MLflow tracking, endpoints, and MLOps retraining patterns.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | DP-100 |
| Credential | DP-100: Azure Data Scientist Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~100 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Design and Prepare a Machine Learning Solution | ~25% |
| 2 | Explore Data and Train Models | ~25% |
| 3 | Prepare a Model for Deployment | ~25% |
| 4 | Deploy and Retrain a Model | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Design and Prepare a Machine Learning Solution

- The Azure Machine Learning workspace is the top-level resource that centralizes data assets, models, compute, jobs, environments, and endpoints for a team's ML work.
- A workspace automatically provisions and references companion resources: Azure Storage (default datastore), Azure Key Vault (secrets), Azure Container Registry, and Application Insights.
- A compute instance is a managed single-user dev workstation (pre-configured Jupyter/VS Code) for interactive authoring; a compute cluster is multi-node managed compute for training and batch jobs that can autoscale.
- Set a compute cluster's minimum nodes to 0 so it scales down to zero when idle, eliminating idle cost; it scales up on demand when jobs are queued.
- Low-priority (Spot) VM nodes in a compute cluster cut cost substantially but can be pre-empted, so use them for fault-tolerant or interruptible training workloads.
- Datastores are connection configurations that reference an Azure storage account (Blob, ADLS Gen2, File); data assets are named, versioned references to specific data for reproducibility and lineage.

### Domain 2 - Explore Data and Train Models

- Hyperparameters (learning rate, tree depth, regularization strength, batch size, number of layers) are set before training and control how the algorithm learns; model parameters are learned during training.
- Split data into training (fit parameters), validation (tune hyperparameters and select models), and test (final unbiased generalization estimate) sets to avoid overfitting bias.
- Cross-validation (for example k-fold) trains and validates across multiple data folds to give a more robust performance estimate than a single train/validation split.
- Feature engineering transforms raw data into informative features (polynomial terms, binning, temporal components, encodings) to make patterns more learnable.
- Regression metrics include MSE, RMSE, MAE, and R-squared; classification metrics include accuracy, precision, recall, F1, and AUC (area under the ROC curve).
- For imbalanced classification (for example a 5% positive class), raw accuracy is misleading; optimize F1 or AUC, which reflect performance on the minority class.

### Domain 3 - Prepare a Model for Deployment

- Registering a model creates a named, versioned artifact with metadata linking it to the job, metrics, and data that produced it, enabling deployment, rollback, and audit.
- A managed online endpoint serves real-time, low-latency predictions over a REST API with the model kept in memory to avoid cold-start delays.
- A batch endpoint scores large volumes of data asynchronously (on a schedule or on demand) on a compute cluster, ideal when per-record latency is tolerable.
- A scoring/entry script (typically score.py) defines init() to load the model once and run() to process each inference request, including preprocessing and postprocessing.
- An inference environment (curated or custom Docker/conda) pins the runtime and dependencies so inference is reproducible and matches training.
- An online endpoint can front multiple deployments behind one scoring URI, with traffic allocation percentages set per deployment to enable blue/green and canary rollouts.

### Domain 4 - Deploy and Retrain a Model

- Managed online endpoints expose models over REST with low latency and automatic scaling for real-time prediction; batch endpoints handle scheduled, high-volume asynchronous scoring.
- MLOps operationalizes the ML lifecycle: Azure ML pipelines orchestrate multi-step workflows (data prep, train, evaluate, register) for reproducible, schedulable retraining.
- CI/CD integration with GitHub Actions or Azure DevOps invokes the Azure ML CLI/SDK to trigger pipeline runs on code or data changes, automating retraining and deployment.
- Data drift is a shift in the production data distribution relative to training data; it degrades accuracy over time and signals a need to retrain.
- Azure ML monitors deployed models by comparing recent inference data against a baseline to detect data drift and performance degradation.
- Common retraining triggers are arrival of fresh labeled data, a recurring schedule, and monitoring that detects drift or a drop in production performance.

## Study tips

- Master the v2 vocabulary: workspace, datastore, data asset, environment, compute instance vs compute cluster, command/sweep/pipeline jobs, and managed online vs batch endpoints; many questions hinge on choosing the right resource for a scenario.
- Know the online-vs-batch endpoint decision cold: real-time low-latency REST equals managed online endpoint; high-volume, latency-tolerant, scheduled scoring equals batch endpoint.
- Watch for cost-optimization questions: compute clusters scaling to zero (min nodes 0), Spot/low-priority VMs, autoscale min/max, reserved instances, and same-region co-location are recurring correct answers.
- On imbalanced data, never pick raw accuracy; choose F1 or AUC. Be ready to map metrics to problem types (RMSE/R-squared for regression, precision/recall/F1/AUC for classification).
- Expect yes/no "does this solution meet the goal" series and az ml CLI v2 syntax questions; read each scenario carefully and recognize valid command flags like --traffic, --set, and --request-file.

---

Want the full breakdown? See the complete **[DP-100 study guide](https://certgrid.app/study-guide/dp-100-azure-data-scientist-associate)** and **[free practice questions](https://certgrid.app/practice/dp-100-azure-data-scientist-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

