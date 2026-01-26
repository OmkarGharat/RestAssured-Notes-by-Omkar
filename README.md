# RestAssured-Notes-by-Omkar

A comprehensive, phase-based educational repository for mastering API Automation using **Rest Assured** and **Java**. This project documents the transition from a junior tester to a **Senior SDET** by deep-diving into framework architecture, security protocols, and industry best practices.

## 🚀 Roadmap Overview

The repository is structured into progressive learning phases to ensure a "confusion-free" mastery of API testing:

* **Phase 4: Framework Thinking** – Focuses on centralizing logic, environment configurations (`config.properties`), and reusable request specifications.
* **Phase 5: Professional Expansion** – Advanced topics including OAuth 2.0 flows, the Token Lifecycle, and Senior-level interview preparation.

## 🌟 Key Features & Modules

### 🛡️ Advanced Authentication (Phase 5)

Detailed exploration of **OAuth 2.0**, distinguishing between different flows used in modern software:

* **Client Credentials Flow**: Machine-to-machine (M2M) communication without human intervention, most common in automation.
* **Authorization Code Flow**: User-based authentication involving consent screens and temporary authorization codes.
* **Token Lifecycle Management**: Understanding the "Birth, Life, and Death" of tokens, including Access vs. Refresh tokens to prevent CI/CD failures.

### 🏗️ Framework Architecture (Phase 4)

* **Static Initialization**: Utilizing `static {}` blocks for thread-safe, one-time loading of configuration files.
* **Request & Response Specs**: Implementing the **Builder Pattern** (`RequestSpecBuilder`) to maintain consistency across global test suites.
* **Environment Switching**: Logic for dynamically overriding environments (Dev/QA/Prod) via command-line arguments (`mvn test -Denv=dev`).

### 🛠️ Professional "Senior" Tricks

* **Utility Methods**: Writing reusable methods to automatically fetch fresh tokens when a `401 Unauthorized` is detected.
* **API Chaining**: Mastering the "Two-Step Dance"—hitting an Auth Server for a key followed by the Business API for data.
* **Error Investigation**: Dedicated notes on resolving common exceptions like `ConnectException` or `422 Unprocessable Entity` (Data Validation errors).

## 📂 Project Structure

```text
RestAssured-Notes-by-Omkar-main/
├── Phase 4/                   # Framework-level setup and Java logic
│   ├── Rest Assured - TRICKS.md
│   ├── Static Block.md
│   └── Environment Config.md
├── Phase 5/                   # Advanced security and professional flows
│   ├── OAuth 2.0 Basics.md
│   ├── Token Lifecycle.md
│   └── Access & Refresh Token.md
├── assets/                    # Flowcharts and architectural diagrams
└── README.md

```

## 🧠 Strategic Learning

The repository follows a **Strategic Teaching** methodology, where complex topics like path parameters and cookies are introduced only after the core framework foundation is solid. This ensures every concept can be immediately integrated and applied in a real-world project style.
