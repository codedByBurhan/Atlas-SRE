<div align="center">

# 🌐 ATLAS SRE

**AI-Powered Engineering Incident Intelligence System**

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg?style=flat-square)]()
[![Platform](https://img.shields.io/badge/platform-Browser--based-success.svg?style=flat-square)]()
[![AI Powered](https://img.shields.io/badge/AI-Gemini_3.5_Flash%2FPro-orange.svg?style=flat-square)]()
[![License](https://img.shields.io/badge/license-MIT-green.svg?style=flat-square)]()

*Reduce Mean Time to Resolution (MTTR) with a zero-backend, privacy-first copilot for incident response, root cause analysis, and architecture exploration.*

<br />

![Atlas SRE Showcase](./screenshot.png)

</div>

---

## 📑 Table of Contents

- [🛑 The Problem](#-the-problem)
- [💡 The Solution](#-the-solution)
- [✨ Core Modules & Features](#-core-modules--features)
- [🏗️ Technical Architecture](#-technical-architecture)
- [🚀 Getting Started](#-getting-started)
- [🗺️ Blueprint Roadmap](#-blueprint-roadmap)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 🛑 The Problem

During a critical Sev-1 incident, **Mean Time to Resolution (MTTR)** is everything. Site Reliability Engineers (SREs) and DevOps teams waste precious minutes frantically searching through fragmented PDFs, historical postmortems, and outdated runbooks. 

While existing AI solutions attempt to solve this, they introduce a massive risk: they force you to upload highly sensitive infrastructure documents, security policies, and proprietary architecture diagrams to third-party centralized vector clouds. This creates severe security and compliance bottlenecks, effectively rendering them unusable for secure enterprise environments.

## 💡 The Solution

**Atlas SRE** introduces a radically different approach to incident intelligence. We engineered a completely self-contained web application that runs a **Retrieval-Augmented Generation (RAG)** pipeline entirely inside your browser. 

> **Architectural Philosophy:** Your sensitive infrastructure data should never leave your machine. 

Atlas SRE parses and processes PDFs locally in the client. We utilize the **Google Gemini 3.5 Flash/Pro API** solely for context-aware generation, effectively eliminating the need for backend vector databases. Keep your documents local, resolve queries instantly, and explore your infrastructure documentation securely without deploying a single backend server.

---

## ✨ Core Modules & Features

| Feature | Description |
| :--- | :--- |
| 🛡️ **Zero-Backend Local RAG** | Execute document chunking, **TF-IDF lexical indexing**, and local keyword overlap scoring completely in the browser. You eliminate the backend vector cloud, ensuring your sensitive data stays strictly local. |
| 🤖 **AI Investigator (Incident Copilot)** | Chat with an assistant powered by **Gemini 3.5 Flash/Pro** for context-aware synthesis. Trigger instant action macros (e.g., *"Draft RCA"*) and audit the system through a **RAG Transparency Log** that exposes retrieval scores, chunks used, and confidence estimates. |
| 📄 **Interactive PDF Citation Engine** | Render high-fidelity canvas elements and extract localized text using `PDF.js`. Click dynamically generated citation chips to anchor directly back to specific pages in the original documents. |
| 📚 **Knowledge Base Management** | Drag and drop sensitive PDFs securely for instant ingestion. View live metrics for chunks and documents, or load the preloaded 18-document **Demo Knowledge Base** (covering SLOs, Outages, etc.) for immediate testing and evaluation. |
| 🗺️ **Service Explorer** | Map operational dependencies automatically. The explorer parses uploaded architecture documents and visualizes relationships between services (e.g., Redis, PostgreSQL, Kafka) using an ASCII-style tree topology. |
| ⚙️ **System Settings Configuration** | Take fine-grained control over the live LLM parameters. Select your preferred model (**Gemini 3.5 Flash/Pro**) and adjust the Retrieval Top-K and LLM Temperature to suit your needs. |

---

## 🏗️ Technical Architecture

Atlas SRE proves that you can build powerful, secure AI tools with modern vanilla web technologies, prioritizing extreme speed, absolute privacy, and deployment simplicity.

### 🛠️ Tech Stack

- **UI & Styling:** Construct a responsive, modern glassmorphism interface using **Tailwind CSS** and **FontAwesome**.
- **Document Engine:** Handle binary parsing, text layer extraction, and high-fidelity canvas rendering natively with **PDF.js**.
- **Retrieval Logic:** Execute client-side **TF-IDF indexing**, chunking, and lexical search entirely in memory using **Vanilla JavaScript**.
- **LLM Integration:** Integrate the **Google Gemini API** to provide advanced reasoning, summarization, and formatting based strictly on the retrieved local context window.
- **Formatting & Security:** Render AI-generated Markdown safely with syntax highlighting using `marked.js`, `DOMPurify`, and `highlight.js`.

### 🔄 Data Flow

1. **Ingestion:** Extract text layers locally via `PDF.js` Web Workers.
2. **Indexing:** Chunk the text and mathematically index it in the browser's memory using **TF-IDF** style heuristics.
3. **Retrieval:** Score local keyword overlap to fetch the highest relevance document chunks based on user queries.
4. **Generation:** Dispatch the precise chunks to **Gemini 3.5 Flash/Pro** to synthesize a response with exact citation anchoring.

---

## 🚀 Getting Started

We designed Atlas SRE for immediate evaluation by project reviewers and engineers. You require no databases to spin up, no Node modules to install, and no Docker containers to build.

### Prerequisites

- A modern web browser (Chrome, Edge, Firefox, Safari).
- A free [Google Gemini API Key](https://aistudio.google.com/app/apikey).

### 1. Local Installation & Launch

First, clone the repository to your local machine:

```bash
git clone https://github.com/yourusername/atlas-sre.git
cd atlas-sre
```

Because `PDF.js` utilizes Web Workers for parsing, you must serve the files via a local web server to bypass CORS restrictions. Choose one of the following methods:

- **Python:** Run `python -m http.server 8000`
- **Node.js:** Run `npx serve`
- **VS Code:** Right-click `index.html` and select **Open with Live Server**.

Navigate to `http://localhost:8000` in your browser to launch the application.

### 2. Enter Workspace & Load Demo Data

1. On the landing page, click **Enter Workspace**.
2. Notice the global **Demo Mode** banner at the top of the screen.
3. Click **Load Demo Knowledge Base** to instantly ingest the pre-packaged dataset of 18 SRE documents (SLOs, past outages, runbooks).

### 3. Configure the AI Engine

1. Navigate to **Settings** in the bottom-left sidebar.
2. Paste your **Gemini API Key**.
3. Select **Gemini 3.5 Flash** or **Gemini 3.5 Pro**.
4. Adjust the Retrieval Top-K and Temperature if desired, then click **Save Configuration**.

### 4. Issue Queries

Open the **AI Investigator** chat interface. Try the built-in macros or ask complex queries:

- *"Based on the recent context, draft a structured SRE Blameless Postmortem for the cache stampede."*
- *"What is the dependency chain for the payment gateway according to the architecture docs?"*

Observe the **RAG Transparency Log** and click on the generated **Citation Chips** to instantly render the corresponding PDF page alongside the chat.

---

## 🗺️ Blueprint Roadmap

- [ ] **IndexedDB Support:** Migrate document storage from volatile memory to persistent browser storage to maintain PDFs between sessions.
- [ ] **Semantic WebGL Embeddings:** Upgrade from lexical search to semantic search using lightweight, browser-based embedding models (like Transformers.js) locally.
- [ ] **Automated Service Map Generation:** Enhance the Service Explorer to dynamically draw node-based architecture diagrams from text context using D3.js.
- [ ] **Exportable Workspaces:** Enable teams to download their processed knowledge base as a single encrypted JSON payload to share securely during live incidents.

---

## 🤝 Contributing

We welcome contributions from the community! Whether it's fixing a bug, improving documentation, or proposing new features, your help is appreciated. Please feel free to submit a Pull Request or open an Issue to discuss potential changes. Let's build the future of secure incident intelligence together.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---
<div align="center">
  <p>Built with 🩵 by <strong>codedByBurhan</strong></p>
</div>
