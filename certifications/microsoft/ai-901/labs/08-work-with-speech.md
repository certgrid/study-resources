# Lab 08 - Work with Speech

Speech questions are quick marks if you keep recognition and synthesis straight. This lab makes the direction physical: you speak, it types; it types, you listen.

## Time Needed

15-20 minutes.

## What You Will Learn

- Speech to text (recognition) and text to speech (synthesis) in practice
- Where Azure Speech lives in Foundry Tools
- How a multimodal model can respond to spoken prompts directly

## AI-901 Concepts Covered

| Concept            | Where you see it in the lab                     |
| ------------------ | ----------------------------------------------- |
| Speech recognition | You transcribe your own voice                   |
| Speech synthesis   | You generate spoken audio from text             |
| Foundry Tools      | You find Azure Speech among the tools           |
| Multimodal audio   | You see how audio can go straight into a prompt |

## Steps

### 1. Find Azure Speech in Foundry Tools

In the Foundry portal, browse Foundry Tools and open the Azure Speech capabilities. Identify the two core directions before touching anything: speech to text, text to speech.

### 2. Try speech to text

1. Open the speech-to-text tryout experience.
2. Use your microphone to say two sentences.
3. Watch the transcription appear. That is recognition.

### 3. Try text to speech

1. Open the text-to-speech tryout experience.
2. Paste a sentence and pick a voice.
3. Play the audio. That is synthesis. Note the voice options; natural-sounding voices are the point of modern synthesis.

### 4. Connect to multimodal prompts

If your deployed model (or a catalog model you can try) accepts audio input, send a short spoken question. The difference from step 2 is important for the exam: Azure Speech converts audio; a multimodal model answers it.

## Clean Up

Nothing persistent was created.

## Success Criteria

You are done when you can explain:

- Which direction is recognition and which is synthesis
- When you need Azure Speech vs a multimodal model with audio prompts
- One scenario for each direction
