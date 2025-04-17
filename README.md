🧠 Luna System – Private AI Cognition Engine
Luna is a Swift + Python native macOS platform designed as a private, project-centric AI cognition engine. It powers auto-generating multi-agent reasoning scenarios, self-iterating agents that dynamically tune their parameters, and swarm self-cloning workers for continuous background analysis. The system integrates NLP, web intelligence, geolocation, chat analysis, and code management, with support for Mistral, OpenAI, and Google Gemini LLMs (via 10 Mistral API keys and other provider APIs). All data is stored locally (except LLM inference) in specialized databases, with a CoreML-powered Swift frontend and a robust Python backend.
This is a private repository for internal development and experimentation.

🌟 Core Features



Feature
Description



Multi-Agent Reasoning Scenarios
Auto-generates dynamic scenarios with per-agent parameters (e.g., temperature, role).


Self-Iterating Agents
Agents self-modify parameters to optimize responses iteratively.


Swarm Self-Cloning Workers
6-worker threads clone themselves for parallel analysis of chats, code, and data.


Chat Intelligence
Real-time chat analysis with cosine similarity, sentiment, bias, ABSA, and topic modeling.


Web Intelligence
Multi-engine querying with 5-score ranked results (articles, images), NER, entity linking, geotagging.


NLP & Data Analysis
ABSA, topic modeling (BERTopic, LDA), keyword extraction, entity linking, geolocation.


Geolocation & Geotagging
Extracts and maps geolocation data with AI-augmented insights.


Code Management
Extracts, auto-titles, and stores code with keyword associations.


TTS/STT
Text-to-speech and speech-to-text for interactive workflows.


Persistent Memory
Local storage in SQLite/JSON for chats, web scrapes, and scenario analysis.


Multi-LLM Support
Integrates Mistral (10 API keys), OpenAI, and Google Gemini for flexible model selection.



🛠️ Tech Stack
⚙️ Backend (Python)

Standard Libraries: os, json, logging, re, uuid, datetime, urllib.parse, threading, subprocess, random, socket, gc, tempfile, time, collections.deque, io.
Third-Party Libraries:
Web & Scraping: requests, aiohttp, httpx, bs4 (BeautifulSoup), playwright, selenium, newspaper, readability, yarl, tenacity, cachetools, markdown2, fitz (PyMuPDF), pdfplumber, PIL, pytesseract.
Data & Analysis: numpy, pandas, sklearn, matplotlib, seaborn, spacy, nltk, umap, collections.Counter, sklearn.feature_extraction.text (TfidfVectorizer, CountVectorizer), sklearn.decomposition (LDA).
AI & NLP: torch, transformers, sentence_transformers, bertopic, keybert, openai, google.generativeai, mistralai, T5, BERT, spacy.matcher.
Database: sqlite3, sqlalchemy, aiosqlite.
Web Framework: fastapi, starlette, slowapi.
Async & Concurrency: asyncio, concurrent.futures, aiofiles, anyio, websockets.
Geolocation: geopy (Nominatim, RateLimiter).
Utilities: tracemalloc, mimetypes, docx, base64.


Custom Modules: scraper, uniscrape, database, scraper_controller, data_analysis, advanced_data_analysis, utils, startterminalserver, terminal.

📱 Frontend (Swift)

CoreML: On-device ML for chat analysis, scenario orchestration, and UI interactions.
Native macOS: Swift-based interface for managing projects, chats, and analysis.
Planned: Tauri/React for cross-platform support.


📁 Database Architecture



DB Name
Type
Stores



backend.db
SQLite
Web scrape results (articles, images), ranked results, analysis (ABSA, topic modeling, NER, entity linking, geolocation, geotagging), chat analysis (cosine similarity, sentiment, bias).


frontend_chat.db
SQLite
Projects, chats, messages, summaries, web scrapes, web searches, and associated analysis.


cognition_scenario.db
Custom SQL Parallel
Multi-agent reasoning scenarios, agent parameters, iteration logs, and scenario analysis.


context.json
JSON
Indexed chats, embeddings, metadata, and scraped data.


backlog/
Folder
Imported logs (CSV, JSON).



🔍 Key Workflows
🧠 Cognition Scenario Engine

Auto-Generation: Creates multi-agent reasoning scenarios with dynamic parameters.
Self-Iteration: Agents tune parameters (e.g., temperature, top-k) using Mistral, OpenAI, or Gemini models.
Parallel Analysis: Swarm workers analyze scenarios in cognition_scenario.db for novelty, conflict, and coherence.
Endpoints: FastAPI endpoints for scenario creation, agent management, and analysis retrieval.

💬 Chat Intelligence

Inputs: Live chats, CSV/JSON imports, URLs (stored in frontend_chat.db).
Analysis (shared Python stack):
Cosine similarity (sentence_transformers) for prompt/response matching.
Sentiment, bias, ABSA (transformers, spacy).
Topic modeling (bertopic, sklearn.LDA), keyword extraction (keybert).


Endpoints: FastAPI endpoints for chat analysis, keyword search, and TTS/STT queue management.
Outputs: Summaries, tagged metadata, embeddings in backend.db and frontend_chat.db.

🌐 Web Intelligence

Querying: Multi-engine searches (Google, OpenAI, DuckDuckGo) with unified aggregation.
Scraping: Extracts articles, images, and metadata using playwright, selenium, bs4, newspaper.
Ranking: 5-score system (relevance, authority, recency, depth, trust).
Analysis (stored in backend.db):
NER, entity linking (spacy, transformers).
Geolocation, geotagging (geopy.Nominatim).
ABSA, topic modeling (bertopic, sklearn.LDA), keyword extraction (keybert).


Endpoints: FastAPI endpoints for search, scrape, and analysis retrieval.

📍 Geolocation & Geotagging

Extraction: Identifies geolocation data using geopy.Nominatim.
Geotagging: Tags data with location metadata.
Mapping: Maps locations with AI-augmented insights, stored in backend.db.

📦 Code Management

Extracts code from chats, auto-titles, and stores in backend.db with keyword tags.
Links code to scenarios and projects in frontend_chat.db.


🚀 Quickstart
# Clone the private repo
git clone <private-repo-url>
cd luna-system

# Install dependencies
pip install -r requirements.txt

# Configure API keys (Mistral, OpenAI, Google Gemini)
# Add keys to environment variables or config file

# Start backend
uvicorn app.main:app --reload

# (Optional) Run terminal and scraper services
python startterminalserver.py
python scraper_controller.py


📈 Roadmap

[ ] Contextual memory for multi-conversation linking (in progress).
[ ] Vector search across chats, code, and scraped data.
[ ] Offline LLM support (Mistral, TinyLlama via ollama).
[ ] Bias and emergent behavior detection (in progress).
[ ] Agent collaboration graphs for reasoning.
[ ] Native macOS app with enhanced CoreML integration.
[ ] Separate public repo for stripped-down demo.


🧠 Philosophy
Luna is a private AI research lab—an autonomous cognition engine for experimenting with multi-agent reasoning, NLP, and web intelligence. It’s designed for deep, project-centric workflows with minimal external dependencies, leveraging Mistral, OpenAI, and Gemini LLMs under your control.

📝 Notes

Private Repository: For internal use only. Public demos will use a separate repo with limited features.
Mistral Integration: 10 API keys configured for flexible LLM access.
Future App: A stripped-down macOS app is planned but not public.
Contact: Reach out via internal project channels for collaboration.

