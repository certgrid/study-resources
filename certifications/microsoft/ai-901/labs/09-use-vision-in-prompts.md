# Lab 09 - Use Vision in Prompts

Interpret vs generate is a guaranteed exam distinction. This lab does both so the difference sticks.

## Time Needed

15-20 minutes.

## What You Will Learn

- Sending an image to a multimodal model and asking about it
- Generating a new image from a text description
- Why these are different capabilities and often different models

## AI-901 Concepts Covered

| Concept              | Where you see it in the lab                |
| -------------------- | ------------------------------------------ |
| Multimodal input     | You attach an image to a prompt            |
| Image interpretation | The model describes and answers about it   |
| Image generation     | A model creates a new image from your text |

## Steps

### 1. Interpret an image

1. In the chat playground, pick a deployment with vision (multimodal) capability. Deploy one from the catalog if needed (serverless API).
2. Attach any photo (for example, a desk or a street scene).
3. Ask: "Describe this image." Then: "How many chairs are visible?"
4. This is visual input in a prompt: interpretation.

### 2. Generate an image

1. Open the images playground (or deploy an image-generation model from the catalog).
2. Prompt: "A minimalist illustration of a cloud with a graduation cap, flat design."
3. This is generation: text in, new image out.

### 3. Lock in the verbs

| Scenario verb           | Capability       |
| ----------------------- | ---------------- |
| Describe, answer, check | Multimodal input |
| Create, design, draw    | Image generation |

## Clean Up

If you deployed extra models for this lab, delete those deployments now unless you want them for review. Lab 11 covers full cleanup.

## Success Criteria

You are done when you can explain:

- What made the interpretation model "multimodal"
- Why "describe this photo" never means image generation
- One business scenario for each capability
