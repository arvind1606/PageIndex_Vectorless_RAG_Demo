# 📄 PageIndex — Vectorless RAG Demo

A ready-to-run Jupyter notebook demonstrating **Vectorless RAG** using [PageIndex](https://pageindex.ai) and Google Gemini. Instead of chunking documents into embeddings, PageIndex builds a hierarchical tree of your PDF's structure and lets an LLM navigate directly to the relevant section — no vector database needed.

---

## 🧠 How It Works

```
PDF → PageIndex Tree Index → chat_completions() → Grounded Answer
```

1. **Submit** your PDF to PageIndex — it parses the document and builds a structured "Table of Contents" tree
2. **Poll** `get_tree()` until the index is ready
3. **Query** using `chat_completions()` — PageIndex navigates the tree, extracts the exact section, and returns a cited answer
4. **Render** the answer as Markdown inside the notebook

Traditional RAG retrieves by *similarity*. PageIndex retrieves by *reasoning*.

---

## 🚀 Quickstart

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
```

### 2. Install dependencies

```bash
pip install pageindex google-genai
```

Or run the first cell in the notebook:

```python
%pip install pageindex google-genai
```

### 3. Add your API keys

Open the notebook and fill in Cell 2:

```python
PAGEINDEX_API_KEY = "YOUR_PAGEINDEX_API_KEY"
GEMINI_API_KEY    = "YOUR_GEMINI_API_KEY"
```

| Key | Where to get it |
|-----|----------------|
| PageIndex | [dash.pageindex.ai](https://dash.pageindex.ai) |
| Gemini | [aistudio.google.com](https://aistudio.google.com) |

### 4. Set your PDF path and run

```python
PDF_PATH = "your_document.pdf"
```

Then run all cells top to bottom. The indexing cell only needs to be run **once per document** — a guard flag prevents re-indexing in the same session.

---

## 📓 Notebook Structure

| Cell | What it does |
|------|-------------|
| **Cell 1** | Install dependencies |
| **Cell 2** | Import libraries and initialise API clients |
| **Cell 3** | Set PDF path and initialise `doc_id = None` |
| **Cell 4** | Submit PDF to PageIndex and poll until tree is ready ⚠️ *run once* |
| **Cell 5** | Inspect the submission response |
| **Cell 6** | Define `run_rag()` query helper using `chat_completions()` |
| **Cell 7** | Run a single query and print the answer |
| **Cell 8** | Render the answer as formatted Markdown |

---

## 💡 Example Output

```
============================================================
QUERY  : What is the architecture of DeepSeek-V3?
============================================================
DeepSeek-V3 is a 671B parameter Mixture-of-Experts (MoE) model
built on the Transformer framework with three key innovations:

1. Multi-Head Latent Attention (MLA) — efficient KV cache compression
2. DeepSeekMoE — auxiliary-loss-free load balancing with shared + routed experts
3. Multi-Token Prediction (MTP) — predicts multiple future tokens per step
...
```

---

## ⚠️ Notes

- **Index once** — `doc_id` is stored in memory. Re-running Cell 4 will skip submission if `doc_id` is already set. If you restart the kernel, you can reuse an existing `doc_id` by setting it manually in Cell 3.
- **Gemini free tier** has rate limits. If you hit a `429` error, wait a few minutes or enable billing at [aistudio.google.com](https://aistudio.google.com). Alternatively, switch to `gemini-2.5-flash-lite` for higher free-tier throughput.
- Only **PDF files** are currently supported by PageIndex.

---

## 📚 Resources

- [PageIndex Documentation](https://docs.pageindex.ai)
- [PageIndex Python SDK](https://docs.pageindex.ai/sdk)
- [Vectorless RAG Cookbook](https://docs.pageindex.ai/cookbook/vectorless-rag-pageindex)
- [Google Gemini API](https://ai.google.dev)

---

## 📝 License

MIT
