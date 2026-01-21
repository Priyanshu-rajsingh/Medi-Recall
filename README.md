# Medi-Recall: A Multimodal Healthcare Memory Assistant

**Built for Convolve 4.0 - A Pan-IIT AI/ML Hackathon**  
**Societal Challenge:** Healthcare & Memory Support for Chronic Patients

---

## 01. Motivation & Societal Impact

Patients with chronic conditions, elderly individuals, or those with cognitive decline often struggle to manage fragmented medical data. Their **"medical memory"** is scattered across doctor’s notes (text), prescriptions (structured data), and medical scans/photos (images).

Medi-Recall uses **Qdrant** to build a high-performance, multimodal long-term memory system. It allows patients to:

- Search across different data types  
  *(e.g., "Find the photo of my rash" or "Why did I feel dizzy last week?")*
- Receive evidence-based answers grounded in their actual medical history
- Bridge the gap between raw data and actionable healthcare reasoning

---

## 02. System Architecture

Medi-Recall follows a **Retrieval-Augmented Generation (RAG)** architecture optimized for multimodal data:

- **Data Ingestion:**  
  Text logs and images are processed using the CLIP (ViT-B-32) model.

- **Vector Storage:**  
  Embeddings (512-dim) are stored in a Qdrant Cloud collection.

- **Multimodal Retrieval:**  
  Qdrant's `query_points` API performs semantic search across both text and visual signals.

- **Reasoning Engine:**  
  Google Gemini 1.5 Flash synthesizes the retrieved evidence into a compassionate, human-readable response.

---

## 03. Technical Stack

- **Vector Database:** Qdrant (Cloud Tier)
- **Embedding Model:** CLIP (Contrastive Language-Image Pre-training) via sentence-transformers
- **LLM:** Google Gemini 1.5 Flash
- **Language:** Python 3.10+
- **Environment:** Google Colab / Local Python

---

## 04. Setup Instructions (End-to-End)

Follow these steps to get the system running in under **5 minutes**.

### 1. Prerequisites

You will need API keys for:

- **Qdrant Cloud:** Get a free cluster here
- **Google Gemini API:** Get a free key here

---

### 2. Environment Setup

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME

## 3. Data Preparation

The system expects data in the following structure (automatically created by the notebook):

```text
data/
├── text_logs/   # Place .txt medical records here
└── images/      # Place .jpg or .png medical scans/photos here

05. Usage
Running the Notebook

Open the Medi_Recall_Final.ipynb in Google Colab.

Enter your QDRANT_URL, QDRANT_API_KEY, and GEMINI_API_KEY in the Configuration cell.

Run all cells (Runtime > Run all).

06. Multimodal Strategy

We utilize a Joint Embedding Space approach. By using the CLIP model, we encode both medical images and text descriptions into the same 512-dimensional vector space. This allows Qdrant to find relevant images even when the user queries in natural language text, fulfilling the requirement for Effective Multimodal Retrieval.

07. Evidence-Based Outputs & Reliability

To prevent AI hallucinations (Requirement 04.4), Medi-Recall ensures:

Strict Prompting:
The LLM is instructed to answer only using the context retrieved from Qdrant.

Traceability:
Every response includes a list of "Evidence Sources" (filenames) used to generate the answer.

Safety:
If no relevant data is found in Qdrant, the system defaults to:
"I don't have a specific memory of that, please consult your doctor."

08. Limitations & Ethics

Privacy:
In a production environment, data would be encrypted at rest and HIPAA-compliant.

Accuracy:
CLIP is a general-purpose multimodal model; fine-tuning on specific medical imagery (X-rays/MRI) would improve performance.

Responsibility:
This is an assistive memory tool, not a diagnostic device.

09. Deliverables

Reproducible Code (Colab/Python)

Multimodal Search Capability

Traceable Reasoning Path

Societal Impact Documentation

Team Members

Priyanshu Raj Singh

Grandhi Mohith Gopi Krishna

Convolve 4.0 Hackathon Submission

# Install dependencies
pip install qdrant-client sentence-transformers torch pillow google-genai
