# ChatFusion

**ChatFusion** is an AI-powered conversational system designed to provide more human-like and context-aware interactions. The application combines natural language processing, emotion detection, speech recognition, and voice synthesis to create an interactive chatbot capable of responding to users in a more personalized way.

The system is developed using the **Flask framework** and integrates multiple AI models for speech processing, emotion analysis, and conversational response generation.

---

## Key Features

### Emotion-Aware Conversation

ChatFusion monitors the user’s facial expressions through a webcam using **OpenCV** and **DeepFace**.
The detected emotional state (such as happy, neutral, or sad) is stored and used as contextual information when generating chatbot responses. This allows the system to modify its replies based on the user's emotional state and provide more empathetic interactions.

### Speech Interaction

The application supports full audio interaction through speech recognition and voice generation.

**Speech-to-Text**
User audio input is converted into text using the **faster-whisper** model. The transcribed text becomes the chatbot query.

**Text-to-Speech**
After generating a response, the chatbot converts the text into audio using either:

* **gTTS** for basic speech generation
* **XTTSv2** for more advanced voice synthesis

This allows users to interact with the chatbot entirely through voice.

### Voice Personalization

A unique feature of ChatFusion is the ability to generate responses using a voice that resembles the user's own voice.

Users can upload a few voice samples, which are stored and registered in a database. These samples act as reference inputs for the **XTTSv2 voice synthesis model**.

When the chatbot generates a reply, the model uses the stored audio reference to produce speech in a voice similar to the user’s sample.

---

## System Workflow

### User Interaction

Users access the application through a web interface. Once logged in, they can interact with the chatbot through text or voice.

At the same time, the system continuously analyzes webcam frames to detect the user’s emotional state. This information is periodically stored and updated.

### Audio Processing

When a user submits voice input:

1. The audio file is uploaded to the server.
2. The system converts the audio into WAV format.
3. The **faster-whisper model** transcribes the audio into text.

### Response Generation

The chatbot response is created using a large language model accessed through **OpenRouter APIs**.

The prompt sent to the model includes:

* The user’s query
* A selected conversation role (assistant, friend, tutor)
* The latest detected emotional context

This helps generate responses that are more contextually appropriate.

### Voice Generation

Once the response text is generated:

1. The system retrieves a stored reference audio sample.
2. The **XTTSv2 model** extracts voice characteristics from the sample.
3. The chatbot response is synthesized in that voice.
4. The final audio response is returned to the user.

---

## Voice Cloning Approach

ChatFusion uses a **zero-shot voice cloning approach** through the XTTSv2 model.

This means the model can generate speech in a new voice using only a small reference audio sample instead of requiring long training sessions.

The process works as follows:

1. Users upload a small set of voice samples.
2. These samples are converted to WAV format and stored.
3. The system extracts voice characteristics from the sample.
4. When generating speech, the model uses these characteristics to synthesize the chatbot response in a similar voice.

---

## Technology Stack

The project combines multiple technologies and frameworks:

* **Python**
* **Flask**
* **OpenCV**
* **DeepFace**
* **faster-whisper**
* **XTTSv2**
* **SQLite Database**
* **OpenRouter API (LLM Integration)**

---

## Future Improvements

Planned improvements for ChatFusion include adding **vector database memory** using **ChromaDB**. This will allow the chatbot to store conversation history as embeddings and retrieve relevant past interactions.

With this enhancement, the chatbot will be able to maintain better context across conversations and produce more consistent responses.

---

## Project Goal

The goal of ChatFusion is to explore how different AI components such as emotion recognition, speech processing, and large language models can be combined to create more natural and adaptive conversational systems.


