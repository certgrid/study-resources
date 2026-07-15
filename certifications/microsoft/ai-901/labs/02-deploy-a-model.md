# Lab 02 - Deploy a Model

Deployment is the exam's most important Foundry concept: it turns a catalog entry into something applications can call.

## Time Needed

15 minutes.

## What You Will Learn

- How to deploy a model with the serverless API option
- What a deployment name is and why code calls it
- Where the endpoint and keys live

## AI-901 Concepts Covered

| Concept          | Where you see it in the lab                       |
| ---------------- | ------------------------------------------------- |
| Deployment       | You create one from a catalog model               |
| Serverless API   | You choose pay-per-token deployment               |
| Deployment name  | You set the name applications will call           |
| Endpoint and key | You locate the URL and credential for client apps |

## Cost Note

Serverless API deployments bill per token used. Running this lab's handful of test prompts costs a few cents at most. Do not deploy managed compute for these labs; that bills while provisioned.

## Steps

### 1. Deploy from the catalog

1. In the model catalog, open a small general chat model.
2. Select **Deploy** and choose the serverless API option.
3. Set the deployment name:

```text
chat-ai901-lab
```

4. Confirm and wait for the deployment to finish.

### 2. Inspect the deployment

1. Open **Deployments** in your project and select `chat-ai901-lab`.
2. Find the endpoint URL and keys. This pair is exactly what a client application needs.
3. Note that the deployment name is yours; the underlying model name stays in the catalog.

### 3. Send a first test

Use the built-in test option on the deployment page (or continue to Lab 03 for the playground) and send one short prompt to confirm the deployment responds.

## Clean Up

Keep the deployment; labs 03-09 use it. If you stop here, delete the deployment so nothing is left callable.

## Success Criteria

You are done when you can explain:

- Why applications call the deployment name and not the catalog model name
- What serverless API means for billing
- The two things (plus the name) a client app needs to call this deployment
