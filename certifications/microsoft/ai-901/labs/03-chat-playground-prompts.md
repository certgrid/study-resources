# Lab 03 - Prompt in the Chat Playground

The playground is where prompt engineering stops being theory. This lab exercises the exact parameters the exam asks about.

## Time Needed

20 minutes.

## What You Will Learn

- How the system prompt changes behavior
- Zero-shot vs few-shot prompting
- What temperature and max tokens do to real output

## AI-901 Concepts Covered

| Concept       | Where you see it in the lab                    |
| ------------- | ---------------------------------------------- |
| Playground    | You test prompts without writing code          |
| System prompt | You set role, tone, and format rules           |
| Few-shot      | You add examples and watch consistency improve |
| Temperature   | You compare low vs high randomness             |
| Max tokens    | You cause and then fix a cut-off response      |

## Steps

### 1. Open the playground

1. In your project, open the chat playground.
2. Select your `chat-ai901-lab` deployment.

### 2. Test the system prompt

1. Ask: "Explain what a token is."
2. Now set the system prompt to:

```text
You are a strict examiner. Answer in exactly two sentences, no examples.
```

3. Ask the same question and compare the answers. The behavior change is the system prompt doing its job.

### 3. Try few-shot prompting

Ask the model to classify support tickets as Billing, Technical, or Other. First zero-shot, then add two worked examples to the prompt. Notice the format becomes more consistent with examples.

### 4. Play with temperature

1. Set temperature low (near 0) and ask for a product slogan three times. The answers stay similar.
2. Set temperature high and repeat. The answers vary much more.

### 5. Cause a cut-off

1. Set max tokens very low (for example 20) and ask for a paragraph. The response stops mid-thought.
2. Raise max tokens and confirm the full answer returns. This symptom-to-parameter link is exam gold.

## Clean Up

Nothing new was created. Keep the deployment for the next lab.

## Success Criteria

You are done when you can explain:

- Which instruction goes in the system prompt vs the user prompt
- What few-shot prompting improves
- Which parameter you change for "too random" vs "cut off" output
