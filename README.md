# 📑 Planning Document Text Extraction & Embedding Pipeline 

![generated-image (2) copy](https://github.com/user-attachments/assets/4ef6f28c-c38c-4ec4-b3d0-05a9e4f44aa1)

## 🎯 Problem Statement  

The UK holds 12 million+ planning applications in diverse formats (PDF, TIF, DOCX, RTF, TXT)—plus noisy files (.msg, .html, .mp4, .jpeg, .gif). I needed to extract all text, generate sentence- and paragraph-level embeddings, and power land chatbot (LandGPT) with precise citations linked back to source docs.

## ⚙️ Technical Approach  

* S3 bucket ingestion with MIME-type filtering to weed out noise    
* Text extraction via pure-Python libs (pymupdf, docx, pypdandoc) to keep LLM extraction costs to a minimum  
* OCR of scanned PDFs/TIFs using Google Gemini Flash 2.0 (1M token context, multimodal, fast, incredibly cheap)    
* Embedding with open source nomic-embed-text model (768­-dimensional vectors) via ollama for cost-effective search   
* Storage in client’s Postgres DB, leveraging pgvector, pgvectorScale & pgai extensions    
* Scheduler-worker pattern with Docker \+ AWS SQS, horizontally scalable on Kubernetes spot instances    
* Environment management via Pydantic BaseSettings, modular clean code with idempotent upsert logic


## 🛠 Skills  

Python · AWS S3 · Google Gemini Flash 2.0 · ollama · nomic-embed-text · Postgres · pgvector · pgvectorscale · pgai · Docker · AWS SQS · Kubernetes · Pydantic · OCR · Embeddings · Clean Architecture · Cost Optimisation

## 🔧 Challenges & Solutions  

• High noise ratio in S3 → rigorous MIME-type & extension filtering    
• Scanned PDF/TIF files → Gemini Flash Flash 2.0 OCR for reliable multimodal extraction    
• Massive scale & cost constraints → open-source embeddings \+ spot-instance K8s scaling    
• Avoiding redundant work → SQL-backed dedupe checks before extract/embed    
• Client DB consistency → integrated with existing Postgres stack (deliberately didn’t use a vector DB such as Qdrant to keep tech stack simple and maintainable)

## 📊 Quantifiable Business Impact  

• Processed 12 million docs (avg. 10 pages) in under 48 hours (≈ 250k pages/hr)    
• Reduced extraction & embedding cost by 65% vs. GPT-4 baseline    
• Enables daily ingestion of 1k+ new planning apps, keeping LandGPT data fresh    
• LandGPT platform engagement up 22%

## ⭐ Client Review

<img width="933" alt="Screenshot 2025-05-09 at 13 14 02" src="https://github.com/user-attachments/assets/9b0c4c3a-8882-42e9-be76-6e4b9f340ffe" />

*Note: this was one project of many from a long-term contract with the above client*
