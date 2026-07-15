# Lab 10 - Extract Information with Content Understanding

Azure Content Understanding is the exam's answer to every "extract structured data from unstructured content" scenario. See it return fields, not just text.

## Time Needed

20 minutes.

## What You Will Learn

- What Content Understanding extracts from a document
- Why structured fields beat raw OCR text
- How the same tool covers images, audio, and video

## AI-901 Concepts Covered

| Concept                     | Where you see it in the lab                  |
| --------------------------- | -------------------------------------------- |
| Azure Content Understanding | You process a document and get fields back   |
| Information extraction      | Unstructured input becomes structured output |
| Multimodal extraction       | You see the audio/video input options        |

## Steps

### 1. Open Content Understanding

In the Foundry portal, find Azure Content Understanding in Foundry Tools and open its tryout experience.

### 2. Process a document

1. Use a sample invoice or receipt (the tryout usually offers samples; otherwise use any non-sensitive PDF).
2. Run the extraction.
3. Look at the output: key-value fields (vendor, date, total), tables, and confidence scores, not just a wall of text. That difference from plain OCR is the exam point.

### 3. Check the other modalities

Browse the options for image, audio, and video input. Note what each returns:

| Input    | Output                                  |
| -------- | --------------------------------------- |
| Document | Fields, tables, key-value pairs         |
| Image    | Text and structured information         |
| Audio    | Transcript plus structured insights     |
| Video    | Transcript, scenes, structured insights |

### 4. Say the rule

"Structured data out of unstructured content, any modality: Content Understanding." That single sentence answers several exam questions.

## Clean Up

Delete any uploaded sample files. Lab 11 covers the rest.

## Success Criteria

You are done when you can explain:

- The difference between OCR text and extracted fields
- One extraction scenario each for documents, audio, and video
- Which Foundry Tool this all lives in
