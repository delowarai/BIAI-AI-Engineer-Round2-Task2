# 🏦 Multilingual Banking FAQ Support System with Local LLM & Semantic Search

This project implements an offline-first, highly secure, and extremely accurate banking customer support agent. It combines **multilingual semantic retrieval (LaBSE)** with a fast, high-performance **local LLM (Qwen-2.5-3B-Instruct)** to answer customer queries in English, Bangla, and Banglish while strictly adhering to data privacy and custom fallback instructions.

---

## 🚀 How to Run the Project

### 1. Prerequisites & Environment Setup
Ensure your Google Colab instance is connected to a GPU runtime (T4 GPU or better is highly recommended for running the 3B parameter local LLM efficiently).

### 2. Execution Steps
Follow the notebook cells sequentially from top to bottom:

1. **Step 1: Install & Import Libraries**  
   Run the first code block to install critical dependencies including `torch`, `transformers`, `sentence-transformers`, and `accelerate` directly from PyPI.
   
2. **Step 2: Upload Datasets**  
   Ensure you have the following CSV files uploaded to your active workspace root directory:
   - `bank-faq.csv`: Your reference database containing banking topics, questions, and standard answers.
   - `test-questions.csv`: A list of customer queries used to test and evaluate the pipeline.

3. **Step 3: Load the Local LLM & Embedding Models**  
   - The pipeline downloads and initializes `Qwen/Qwen2.5-3B-Instruct` into GPU memory with FP16 precision.
   - It initializes `LaBSE`, a high-performance multilingual model, to compute semantic embeddings of your FAQ database and user queries.

4. **Step 4: Run the Benchmark Pipeline**  
   Execute the evaluation loop. For each of the test questions, the system:
   - Runs a semantic search using cosine similarity.
   - Flags queries below a similarity threshold ($0.55$) for immediate fallback.
   - Builds a strict system prompt and generates a response in the user's input language (English, Bangla, or Banglish).

5. **Step 5: View Performance & Analytics**  
   Verify latency, fallback triggers, accuracy metrics, and review the detailed prediction breakdown compared against standard online benchmarks.

---

## 🛠️ Configuration & Customization
- **Similarity Threshold**: You can adjust the sensitivity of the semantic matcher in the `get_relevant_faq()` function by modifying the `threshold` parameter (default: `0.55`).
- **Fallback Message**: System prompt rules can be tailored in `generate_bilingual_response()` to change how the bot reacts to out-of-domain questions.
