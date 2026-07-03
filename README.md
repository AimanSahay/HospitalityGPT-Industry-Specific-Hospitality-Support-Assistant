# 🏨 HospitalityGPT – Industry-Specific Hospitality Support Assistant

HospitalityGPT is a domain-specific AI chatbot designed to assist customers with hotel and hospitality-related queries. The project combines **Large Language Models (LLMs)** with **Retrieval-Augmented Generation (RAG)** to deliver accurate, context-aware, and conversational responses for common hospitality support tasks such as reservations, billing, check-in/check-out, cancellations, amenities, and customer services.

The chatbot was built by fine-tuning **TinyLlama-1.1B-Chat** using **LoRA (Low-Rank Adaptation)** and enhancing its responses using a semantic retrieval pipeline powered by **Sentence Transformers** and **FAISS**.

<img width="2186" height="1140" alt="image" src="https://github.com/user-attachments/assets/30785568-2c8c-469d-bf8b-a38bbae0ffda" />


---

# 🚀 Project Highlights

- Fine-tuned TinyLlama using LoRA
- Hospitality-specific instruction dataset from Hugging Face
- Retrieval-Augmented Generation (RAG)
- Semantic search using Sentence Transformers
- FAISS Vector Database
- 4-bit Quantization using BitsAndBytes
- Interactive chatbot built with Gradio
- Automatic evaluation using BLEU and ROUGE metrics
- Cached embeddings and FAISS index for faster inference

---

# 🛠 Tech Stack

| Category | Technologies |
|-----------|--------------|
| Language | Python |
| Framework | Hugging Face Transformers |
| Base Model | TinyLlama-1.1B-Chat-v1.0 |
| Fine-Tuning | PEFT (LoRA) |
| Quantization | BitsAndBytes (4-bit) |
| Embeddings | all-MiniLM-L6-v2 |
| Vector Store | FAISS |
| Interface | Gradio |
| Evaluation | BLEU, ROUGE |
| Environment | Google Colab (T4 GPU) |

---

# 🏗 Project Architecture

```
                    User Query
                         │
                         ▼
              Sentence Transformer
                         │
                         ▼
                FAISS Similarity Search
                         │
               Top Relevant Documents
                         │
                         ▼
                 Prompt Construction
                         │
                         ▼
        Fine-Tuned TinyLlama (HospitalityGPT)
                         │
                         ▼
                Context-Aware Response
```

---

# 📂 Project Structure

```
HospitalityGPT/
│
├── data/
│   ├── bitext-hospitality-llm-chatbot-training-dataset.csv
│   ├── train_data.csv
│   └── test_data.csv
│
├── models/
│   └── hospitalitygpt/
│
├── rag/
│   ├── documents.csv
│   ├── embeddings.npy
│   ├── hospitality.index
│   └── evaluation_results.csv
│
├── 01_Data_Preprocessing.ipynb
├── 02_Model_FineTuning.ipynb
├── 03_RAG_Deployment.ipynb
│
└── README.md
```

---

# 📊 Dataset

**Source:** Bitext Hospitality LLM Chatbot Training Dataset (Hugging Face)

The dataset contains hospitality-specific customer support conversations covering a variety of hotel-related services including:

- Reservations
- Billing & Invoices
- Check-in & Check-out
- Room Services
- Hotel Amenities
- Cancellation Policies
- Airport Transfers
- Loyalty Programs
- Customer Support

The dataset was cleaned, validated, and converted into instruction-response pairs suitable for supervised fine-tuning.

---

# 🤖 Model Fine-Tuning

The chatbot is built on **TinyLlama-1.1B-Chat-v1.0**.

Parameter-efficient fine-tuning was performed using **LoRA**, allowing only a small subset of trainable parameters to be updated while keeping the base model frozen. This significantly reduces GPU memory usage and training time while maintaining strong performance.

Training was performed on **Google Colab T4 GPU**.

---

# 🔎 Retrieval-Augmented Generation (RAG)

Instead of relying solely on the language model, HospitalityGPT retrieves semantically relevant hospitality documents before generating a response.

The RAG pipeline consists of:

1. User query embedding using Sentence Transformers
2. Semantic similarity search using FAISS
3. Retrieval of the most relevant hospitality documents
4. Prompt augmentation with retrieved context
5. Response generation using the fine-tuned TinyLlama model

To improve inference speed, generated embeddings and the FAISS index are cached and reused in subsequent sessions.

---

# 📈 Evaluation

The chatbot was evaluated using a representative sample from the held-out test dataset.

| Metric | Score |
|---------|--------|
| BLEU | **0.0928** |
| ROUGE-1 | **0.2904** |
| ROUGE-2 | **0.1384** |
| ROUGE-L | **0.2297** |

Although BLEU is relatively low, this is expected for conversational AI because multiple valid responses may differ in wording while conveying the same meaning. The ROUGE scores indicate that the chatbot preserves important keywords and sentence structure while generating contextually relevant responses.

---

# 💬 Example Questions

The chatbot can answer questions such as:

- Can I check in early?
- Is breakfast included?
- How can I view my invoices?
- Can I cancel my reservation?
- Do you allow pets?
- Can I arrange airport transportation?

---

# ▶️ Running the Project

1. Clone the repository.

```
git clone <repository-url>
```

2. Install the required libraries.

```
pip install -r requirements.txt
```

3. Run the notebooks in order:

- 01_Data_Preprocessing.ipynb
- 02_Model_FineTuning.ipynb
- 03_RAG_Deployment.ipynb

4. Launch the Gradio chatbot.

---

# 🔮 Future Improvements

- Replace TinyLlama with larger instruction-tuned models (e.g., Mistral or Llama 3).
- Integrate a production-grade vector database such as ChromaDB or Pinecone.
- Add multilingual support.
- Deploy the chatbot using Hugging Face Spaces or Streamlit Cloud.
- Integrate live hotel booking APIs for real-time information.

---

# 🙏 Acknowledgements

- Hugging Face Transformers
- Hugging Face Datasets
- Bitext Hospitality Dataset
- Sentence Transformers
- FAISS
- PEFT (LoRA)
- Gradio
