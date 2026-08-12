# AI-Powered Legal Risk & Contract Analyzer (RAG)

An intelligent legal risk evaluation and contract analysis assistant built using **LangChain**, **Chroma DB**, and **Google Gemini**. Designed to streamline legal review workflows, this system ingests complex real-world agreements (such as the official *Nasdaq Master Services Agreement*), indexes contractual clauses into a persistent vector database, and generates structured legal risk reports with redline recommendations[cite: 22].

**Legal Tech & AI Engineering | Production RAG Implementation**
Data PDF Link: https://listingcenter.nasdaq.com/assets/Master%20Services%20Agreement%20Form.pdf

> This project demonstrates an enterprise-grade Retrieval-Augmented Generation (RAG) architecture tailored for automated document extraction, clause verification, risk scoring, and anti-hallucination contract auditing[cite: 22].

## Overview
Reviewing long, complex legal agreements manually is time-consuming and prone to human oversight. This project implements a domain-specific RAG framework to automate contract analysis:
- **PDF Document Ingestion:** Downloads and parses official PDF service agreements using `PyPDFLoader`[cite: 22].
- **NLTK Text Chunking:** Splits dense legal texts into 1,000-character windows with 100-character overlaps using `NLTKTextSplitter` to maintain clause boundaries and semantic coherence[cite: 22].
- **Batch Vector Storage & Rate Limiting:** Generates embeddings using Google's `gemini-embedding-001` and indexes them into a local Chroma vector database using controlled batch processing to handle API quotas smoothly[cite: 22].
- **Legal Analysis & Redline Generation:** Queries `gemini-flash-latest` using LangChain Expression Language (LCEL) and custom prompt templates to output structured legal reports containing risk levels (HIGH, MEDIUM, LOW), liability breakdowns, and exact redline draft recommendations[cite: 22].

## Key Features
- **Real-World Contract Processing:** Ingests official PDF agreements directly via URL or local upload[cite: 22].
- **Batch Ingestion with Quota Cooldowns:** Manages API rate limits by processing embeddings in small batches (e.g., 15 chunks) with automated cooldown timers[cite: 22].
- **Structured Legal Risk Reports:** Evaluates retrieved clauses and returns standardized reports including:
  1. Direct Answers & Clause Quotes[cite: 22]
  2. Risk Level Assessment (HIGH / MEDIUM / LOW)[cite: 22]
  3. Liabilities, Limitations, and Restrictions[cite: 22]
  4. Redline / Renegotiation Recommendations[cite: 22]
- **Strict Anti-Hallucination Guardrails:** Forces the LLM to return `'NO MATCHING CLAUSE FOUND IN CONTRACT'` if the requested information is absent from the document[cite: 22].

## How It Works
- **Package Installation:** Installs `langchain`, `langchain-chroma`, `pypdf`, `nltk`, and `langchain-google-genai`[cite: 22].
- **Environment Setup:** Loads system environment variables and Google GenAI API credentials[cite: 22].
- **Document Loading & Processing:** Fetches the target PDF agreement, parses the page contents, and splits them into structured chunks[cite: 22].
- **Vector Database Persistence:** Converts chunks into vector embeddings and saves them locally at `/content/legal_chroma_db`[cite: 22].
- **Interactive Query & Report Execution:** Accepts legal queries (e.g., *Confidential Information definitions*, *License restrictions*, *Data protection rules*), performs top-$k$ similarity searches, and generates the final redline analysis[cite: 22].

## Repository Layout
```text
├── legal_chroma_db/                      # Persistent Chroma vector database storing contract embeddings[cite: 22]
├── nasdaq_master_services_agreement.pdf  # Sample input legal contract PDF[cite: 22]
├── Legal_Contract_Analyzer_RAG.ipynb     # Primary execution notebook[cite: 22]
└── README.md                             # Comprehensive system documentation
