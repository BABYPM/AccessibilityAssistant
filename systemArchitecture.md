### System Architecture: Accessibility Assistant - Real-Time AI Guide

### Overview

Accessibility Assistant is a **multi-layered AI accessibility system** designed to provide real-time, voice-based guidance and control across any digital interface. It operates by seamlessly integrating **computer vision**, **natural language processing (NLP)**, and **voice control** at the operating system level.

This architecture is built for **low-latency performance** and deep integration to ensure smooth, intuitive, and device-wide user interaction.

### Architecture Layers and Components

| Layer | Components | Core Function | Technical Purpose |
| :--- | :--- | :--- | :--- |
| **1. Interface & OS Layer** | Accessibility API hooks (Android, Windows, macOS) | System-level UI access and event monitoring. | Allows the assistant to "see" and interpret the current display hierarchy and trigger actions. |
| **2. AI Interpreter Layer** | **TensorFlow.js**, **OpenCV**, **ML Kit** | Visual layout analysis, element detection, and content categorization. | Converts raw UI/screen data into structured, labeled information for machine understanding. |
| **3. NLP & Context Engine** | **Custom LLM**, **Whisper API**, **Dialogflow** | Interprets user voice commands and maintains conversational context. | Translates user intent into executable system commands and generates natural responses. |
| **4. Speech Processing Layer** | **Web Speech API (TTS)**, **Vosk (STT)** | Handles voice input (recognition) and output (synthesis). | Provides the critical two-way conversational bridge between user and system. |
| **5. Learning & Personalization** | **SQLite** (local), **Firestore** (cloud) | Stores user preferences, frequently used apps, and interaction patterns. | Enables adaptive learning, tailoring future responses, shortcuts, and custom workflows. |
| **6. Frontend / User Interface** | **Electron.js / React Native** | Visual dashboard, setup, configuration, and logs panel. | Provides a necessary configuration tool for partially sighted users or caregivers. |

### Data Flow: Executing a Voice Command

The execution of a voice command is a sequential process leveraging multiple layers:

1.  **User Input:** The user speaks a command (e.g., “Open WhatsApp”).
2.  **Speech Processing (STT):** The **Vosk Engine** converts the voice audio into text.
3.  **Intent Parsing (NLP):** The **NLP Engine** interprets the text to determine the user's **intent** (e.g., `ACTION_NAVIGATE`) and the **target** (`WhatsApp`).
4.  **UI Scan (AI Interpreter):** The Interpreter Layer requests the current screen state from the **OS API**. It uses **TensorFlow.js/OpenCV** to visually confirm the target element (the WhatsApp icon) and its coordinates.
5.  **Action Execution (Backend):** The system executes the navigation command using the **OS Accessibility APIs** (e.g., simulating a tap or finding the package name).
6.  **Confirmation (Response Generation):** The **LLM/Context Engine** generates a natural language confirmation ("Opening WhatsApp.").
7.  **Speech Output (TTS):** The **Web Speech API** synthesizes and speaks the confirmation back to the user.

### Communication Diagram
User Voice Input
       |
       v
[Speech-to-Text Engine (Vosk)]
       |
       v
[NLP Context Engine]
       |
       v
[AI Interpreter Layer (TensorFlow/OpenCV)]
       |
       v
[OS Accessibility APIs]
       |
       v
[Action Execution / App Control]
       |
       v
[Response Generator (LLM)]
       |
       v
[Text-to-Speech Output]

