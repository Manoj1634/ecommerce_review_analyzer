# 💬 Product QA and Review Chatbot

This project implements an interactive chatbot that provides answers based on customer product reviews and uploaded PDF documentation. It leverages advanced AI techniques, including **Retrieval-Augmented Generation (RAG)** using **Mistral-7B-Instruct-v0.3**, embeddings with **SentenceTransformers**, and document storage with **ChromaDB**.

---

## 🚀 Features

- ✅ **Ask questions** about any product based on review data or uploaded PDF manuals
- 🧠 **Retrieval-Augmented Generation (RAG)** with accurate, context-grounded responses
- 📄 **PDF Ingestion:** Extract and use text chunks for QA
- 📁 **Switch Products:** Upload custom CSV & PDF to analyze new products
- ⚡ **Efficient 4-bit LLM inference** with `BitsAndBytes` + `Mistral-7B`
- 💬 **Conversation memory** and **source document tracing**
- 📦 Clean **ChromaDB** integration with automatic document indexing

---

## 🛠️ Tech Stack

| Layer            | Tool / Library                          |
|------------------|------------------------------------------|
| UI               | Streamlit                                |
| Embeddings       | SentenceTransformers (BAAI BGE)          |
| Reranker         | CrossEncoder (MS Marco MiniLM)           |
| Language Model   | Mistral-7B-Instruct (via HuggingFace)    |
| Quantization     | BitsAndBytes (4-bit inference)           |
| Retrieval        | ChromaDB                                 |
| PDF Parsing      | PyMuPDF (fitz)                           |


---


## ⚙️ Installation

### Step 1: Clone the repository
```bash
git clone <your_repository_url>
cd final_project_capstone
```
### Step 2: Create a virtual environment
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install dependencies
```bash
pip install streamlit sentence-transformers transformers bitsandbytes chromadb pymupdf torch torchvision torchaudio

```

### Step 4: Ensure CUDA is available (optional but recommended)

```bash
nvidia-smi
```

🚦 Quick Start

### Run the Streamlit chatbot app
```bash
streamlit run app.py --server.runOnSave false
```
Open your browser and go to [http://localhost:8501](http://localhost:8501).

---

## 📝 How to Use

- 💬 **Ask a Question:** Type your question in the chat input field and receive context-aware answers.
- 📄 **Upload Extra PDFs:** Append PDF manuals to the existing product context using the sidebar.
- 🔄 **Switch Product:** Upload a new CSV and optional PDF to reset and analyze a different product entirely.
- 🧹 **Clear Chat:** Click the clear button to reset the conversation history.
- 📎 **View Sources:** Toggle the checkbox to display the source documents used to generate the answer.

---

## 📂 Default Data

By default, the app loads the following product context:

- `sample.csv` — Amazon Tap product reviews  
- `Amazon_Tap_Quick_Start_Guide.pdf` — Official product manual

> 📌 To switch products, upload:
> - A new CSV containing only the columns: `reviews.title` and `reviews.text`
> - An optional new product PDF manual  
> All data will be re-embedded and replace the current context.

---

## 🖥️ GPU Requirements

This app is optimized for fast inference on GPU-equipped machines. Recommended specs:

- ✅ **GPU:** NVIDIA A10G or better
- ✅ **Memory:** ≥16GB VRAM

To **force CPU mode**, modify the following line in `app.py`:

```python
device_map="auto"  # Use device_map={"": "cpu"} to force CPU-only mode

```
---

## 🛡️ Handling Errors

### Common Issues:

- **GPU Memory Issues**
  - Reduce `max_new_tokens` in the `generator()` call.
  - Use CPU fallback mode by modifying your model loading in `app.py`:

    ```python
    device_map = {"": "cpu"}
    ```

- **Streamlit Watcher Errors** (safe to ignore):

    ```bash
    streamlit run app.py --server.runOnSave false
    ```

---

## 📚 References & Resources

- [Streamlit Documentation](https://docs.streamlit.io/)
- [ChromaDB GitHub](https://github.com/chroma-core/chroma)
- [Mistral-7B Model Card](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.3)
- [SentenceTransformers GitHub](https://github.com/UKPLab/sentence-transformers)

---

## 🤝 Contributing

Feel free to open issues, submit pull requests, or reach out with suggestions or feedback!
