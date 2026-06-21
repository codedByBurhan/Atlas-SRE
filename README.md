<div align="center">

# 🌐 ATLAS SRE

**AI-Powered Engineering Incident Intelligence System**

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)]()
[![Platform](https://img.shields.io/badge/platform-Browser--based-success.svg)]()
[![AI Powered](https://img.shields.io/badge/AI-Google_Gemini-orange.svg)]()
[![License](https://img.shields.io/badge/license-MIT-green.svg)]()

*Your zero-backend, privacy-first copilot for incident response, root cause analysis, and architecture exploration.*

[Features](#-key-features) • [How it Works](#-how-it-works) • [Getting Started](#-getting-started) • [Architecture](#-architecture--design) • [Roadmap](#-roadmap)

</div>

---

## 🛑 The Problem

During a critical Sev-1 incident, Mean Time to Resolution (MTTR) is everything. Site Reliability Engineers (SREs) and DevOps teams often waste precious minutes frantically searching through fragmented PDFs, historical postmortems, and outdated runbooks. Existing AI solutions require uploading highly sensitive infrastructure documents to third-party vector databases, creating severe security and compliance bottlenecks.

## 💡 The Solution

**Atlas SRE** is a radically different approach to incident intelligence. It is a completely self-contained, single-file web application that runs a **Retrieval-Augmented Generation (RAG) pipeline entirely inside your browser**. 

By processing PDFs locally and utilizing the Google Gemini API solely for answer generation, Atlas allows teams to query their infrastructure documentation instantly, securely, and without deploying a single backend server.

---

## ✨ Key Features

* **Zero-Backend Local RAG:** Document chunking, keyword overlap scoring, and TF-IDF style retrieval happen entirely on the client side. Your documents never leave your browser until explicitly queried.
* **True PDF Rendering Engine:** Built on PDF.js, Atlas doesn't just extract text—it features a built-in, canvas-based PDF viewer. Click a citation, and instantly jump to the exact page of the original document.
* **Intelligent Citation System:** The AI doesn't just give answers; it provides transparent, clickable source chips. Every claim is mapped directly back to the ingested postmortems and runbooks.
* **Deterministic 3-Mode System:**
    * 🟢 **Live Mode:** Connects to Gemini (1.5 Flash/Pro) for deep, context-aware reasoning.
    * 🟡 **Demo Mode:** Operates fully offline using embedded datasets and local heuristics.
    * 🔴 **Fallback Mode:** Gracefully downgrades to local intelligence if the API experiences throttling or network failure.
* **Continuous Scroll & Highlight:** Navigate complex architectural PDFs seamlessly with multi-page continuous scrolling and automatic highlighting of relevant search terms.

---

## ⚙️ How it Works

Atlas SRE operates on a straightforward but powerful client-side workflow:

1.  **Ingestion:** Users drag-and-drop architecture diagrams, RCAs, or runbook PDFs into the app.
2.  **Processing:** PDF.js extracts the text, which is mathematically chunked and stored in the browser's memory alongside the raw binary PDF data for visual rendering.
3.  **Retrieval:** When an engineer asks a question (e.g., *"How do we mitigate a cache stampede based on the Stripe incident?"*), Atlas performs a local lexical search to surface the most relevant document chunks.
4.  **Generation:** These chunks are packaged securely into a prompt and sent to the Gemini API, which synthesizes a clean, markdown-formatted response complete with exact page citations.

---

## 🚀 Getting Started

Atlas SRE is designed for immediate deployment. There are no databases to spin up, no Node modules to install, and no Docker containers to build.

### Prerequisites

* A modern web browser (Chrome, Edge, Firefox, Safari).
* A free [Google Gemini API Key](https://aistudio.google.com/app/apikey).

### 1. Local Installation

You can run Atlas SRE locally in seconds. First, clone the repository or download the source code:

`git clone https://github.com/yourusername/atlas-sre.git`

**Option A: Quick Run**
Simply double-click the `index.html` file to open it directly in your browser.

**Option B: Local Server (Highly Recommended)**
*Crucial Note:* Because PDF.js utilizes Web Workers for parsing, strict modern browsers may block PDF rendering if run directly via the `file://` protocol due to CORS security policies. Serving the file through a lightweight local server prevents these errors.

* **Using Python:** Run `python -m http.server 8000` in the directory.
* **Using Node.js:** Run `npx serve` in the directory.
* **Using VS Code:** Right-click `index.html` and select "Open with Live Server".

### 2. Configuration

To unlock the full conversational power of the LLM, you must configure your API key inside the application:

1. Open Atlas SRE in your browser.
2. Click **Settings** (the slider icon) in the bottom-left sidebar.
3. Paste your Gemini API Key into the designated field.
4. Select your preferred model (e.g., `gemini-1.5-flash` is recommended for speed and efficiency).
5. Click **Save Configuration**. The engine status in the sidebar will update to "Live Mode Active".

### 3. Deployment to Production

Because Atlas SRE is a 100% client-side, single HTML file application, deploying it is incredibly fast and completely free. 

* **Vercel / Netlify:** Simply drag and drop the project folder into your dashboard, or link your GitHub repository. It will deploy instantly without any build commands.
* **GitHub Pages:** Push the file to a repository, go to Settings > Pages, and deploy straight from your `main` branch.

*(Note: Users will input their own Gemini API keys in the settings panel on the live deployed site; your personal key is not stored in the codebase).*

---

## 🏗 Architecture & Design

Atlas SRE proves that powerful AI tools can be built with vanilla web technologies, prioritizing speed and deployment simplicity.

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **UI / Styling** | HTML5, Tailwind CSS | Responsive, modern glassmorphism interface. |
| **Logic & State** | Vanilla JavaScript | Manages the 3-mode system, chat history, and retrieval logic without framework overhead. |
| **Document Engine**| PDF.js (Mozilla) | Handles binary parsing, text extraction, and high-fidelity canvas rendering of PDFs. |
| **LLM Integration**| Google Gemini API | Provides reasoning, summarization, and formatting based strictly on the local context window. |
| **Formatting** | Marked.js, DOMPurify | Safely renders AI-generated Markdown and syntax highlighting. |

---

## 🖥 User Interface

*(Placeholder for Screenshots)*

* **The Chat Interface:** An intuitive, split-pane view where you chat with the incident copilot on the left and view documents on the right.
* **The Knowledge Base:** A drag-and-drop zone to manage your internal incident documentation.
* **The PDF Engine:** A continuous-scroll PDF reader that automatically jumps to and highlights AI-cited evidence.

---

## ⚠️ Limitations & Known Issues

* **Memory Constraints:** Because documents are stored in local browser memory, ingesting hundreds of massive PDFs simultaneously may cause browser sluggishness or crash the tab. It is optimized for focused, highly-relevant runbook directories.
* **Lexical vs. Semantic Search:** The current retrieval engine uses advanced keyword/TF-IDF logic rather than heavy vector embeddings. While incredibly fast and entirely local, it may require slightly more specific search terms than a backend vector database.

---

## 🗺 Roadmap

* [ ] **IndexedDB Support:** Move document storage from volatile state to persistent browser storage (IndexedDB) so uploaded PDFs remain available between browser sessions.
* [ ] **Web-Worker Processing:** Offload the PDF chunking pipeline to background web workers to prevent UI blocking during large document uploads.
* [ ] **Export/Import Contexts:** Allow teams to download their processed knowledge base as a single JSON file to quickly share "incident workspaces" with other engineers.
* [ ] **Semantic WebGL Embeddings:** Explore lightweight, browser-based embedding models (like Transformers.js) to upgrade from lexical to semantic search without leaving the client.

---

## 🤝 Contributing

Contributions make the open-source community an incredible place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

