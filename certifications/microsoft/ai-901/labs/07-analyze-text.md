# Lab 07 - Analyze Text

Text analysis scenarios are frequent in both domains: recognize the technique, then see it work.

## Time Needed

15-20 minutes.

## What You Will Learn

- Sentiment, entities, key phrases, and summarization on real text
- How the same needs map to a deployed language model with good prompts

## AI-901 Concepts Covered

| Concept               | Where you see it in the lab                 |
| --------------------- | ------------------------------------------- |
| Sentiment analysis    | You score sample reviews                    |
| Entity detection      | You pull names, dates, and places from text |
| Key phrase extraction | You list the main topics                    |
| Summarization         | You shorten a long passage                  |

## Steps

### 1. Prepare sample text

Use three short fake customer reviews (write your own, one clearly positive, one negative, one mixed) and one long paragraph from any public documentation page.

### 2. Run the four techniques

In the chat playground with your `chat-ai901-lab` deployment, run each task with a clear prompt:

| Task        | Prompt pattern                                                       |
| ----------- | -------------------------------------------------------------------- |
| Sentiment   | "Classify each review as positive, negative, or mixed: ..."          |
| Entities    | "List every person, organization, place, and date in this text: ..." |
| Key phrases | "List the five main topics of this text: ..."                        |
| Summary     | "Summarize this text in two sentences: ..."                          |

### 3. Note the exam mapping

The technique names are what the exam tests. Sentiment = feeling, entities = named things, key phrases = topics, summarization = shorter version. In production these also exist as ready-made language capabilities; the concepts are identical.

## Clean Up

Nothing new was created.

## Success Criteria

You are done when you can explain:

- Which technique answers "how do customers feel"
- Which technique answers "what is mentioned"
- The difference between key phrases and a summary
