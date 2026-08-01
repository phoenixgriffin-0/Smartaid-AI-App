 # SmartAid: Edge-AI Emergency First Response System

![React](https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Capacitor](https://img.shields.io/badge/Capacitor-119EFF?style=for-the-badge&logo=capacitor&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Gemini_2.5_Flash-8E75B2?style=for-the-badge&logo=google&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)

> **Graded Class 1 Distinction – Midlands State University (BCom Hons, Information Systems)**

---

## 📱 The Interface: Designed for High-Stress Scenarios
<img width="942" height="486" alt="image" src="https://github.com/user-attachments/assets/14a0f4ce-e53d-44d2-a902-b704d4dd7ec9" />


**SmartAid** is a hybrid (PWA/Native Android) AI-powered mobile first aid coaching system designed specifically for low-connectivity environments. It monitors emergency scenes in real-time using on-device cameras, interacts via a Voice User Interface (VUI) for hands-free operation, and delivers dynamic, contextual guidance to untrained bystanders.

---

## 🏢 The Business Case: Solving "Action Paralysis"
In high-stress medical emergencies, survival outcomes depend heavily on the accuracy of initial bystander care. However, traditional mobile health (mHealth) applications present critical structural weaknesses:
1. **Cognitive Overload:** Users must read static text on a screen while managing a trauma victim, leading to misdiagnosis and procedural errors.
2. **Connectivity Dependency:** Advanced triage apps fail entirely in rural or congested network environments.
3. **Absence of Telemetry:** First responders receive no structured incident data regarding the bystander's interventions prior to ambulance arrival.

**The Solution:** SmartAid shifts the paradigm from *static instruction* to *interactive coaching*. By utilizing multimodal generative AI, the application acts as a virtual paramedic—seeing the injury, listening to symptoms, and guiding the user step-by-step, all while operating on a highly resilient offline-first architecture.

---

## 🧠 Under the Hood: Multimodal AI & Triage Logic
The core intelligence of SmartAid is powered by the **Google Gemini 2.5 Flash** model, integrated to handle complex spatial and auditory inputs under strict time constraints.

### 1. Real-Time Vision Framework (Camera Scan)
<img width="942" height="490" alt="image" src="https://github.com/user-attachments/assets/12ecd058-7a33-4ac5-9402-3186f66eb145" />


Instead of relying on cloud uploads, the application grabs a still frame from the active video canvas, transforms it to a Base64-encoded JPEG, and passes it to the AI for instant analysis. 
* A dynamic `RAPID_MODE` toggle shortens AI inference times, forcing the LLM to return only the top 3 critical life-saving steps rather than exhaustive text.

### 2. Voice User Interface (VUI)
<img width="942" height="489" alt="image" src="https://github.com/user-attachments/assets/a967b524-b8cf-4251-aad3-56c50437b25b" />


Implemented via a custom `useVoiceInterface` hook wrapping the browser's native `SpeechRecognition` and `SpeechSynthesis` APIs. 
* Bystanders confirm safety checks (e.g., "Continue") hands-free, preventing cross-contamination and allowing uninterrupted patient care.

### 3. Graceful Network Degradation
The application is engineered to eliminate reliance on active web connections for life-preserving functionalities. 
* **Online:** Full multimodal AI triage and dynamic GPS routing to nearby medical facilities.
* **Offline (Airplane Mode):** AI features gracefully degrade. The system seamlessly routes the user to a localized, pre-cached JSON knowledge base of decision trees and step-by-step guides bundled at build time.

---

## ⚙️ System Architecture & Edge Integration
<img width="942" height="444" alt="image" src="https://github.com/user-attachments/assets/e043b8c9-39fc-469a-a83c-b5d6a8fca6a7" />


To guarantee ultra-low latency responsiveness during a crisis, the system utilizes a modular, service-oriented architecture tailored for edge computing. 
* **Presentation Tier:** Built with **React 19** and **TypeScript**, packaged for native Android via **Capacitor**.
* **Edge Processing Engine:** Handles natural language queries and live camera frame extraction locally to prevent dangerous latency.
* **Hybrid Data Tier:** Employs device internal flash memory (SQLite/JSON document storage) for zero-latency retrieval of medical protocols, synchronized securely with **Supabase** via encrypted background workers when connectivity is restored.

---

## 📊 Security & Automated Incident Logging
During an emergency, bystanders cannot manually document their actions. SmartAid's `IncidentLogger` service acts as a background telemetry engine.
* Captures start times, voice confirmations, and severe procedural deviations.
* Data is encrypted at rest using native hardware encryption protocols.
* Generates an automated, structured clinical summary for immediate handover to arriving paramedics, fundamentally improving the continuum of care.
* 
