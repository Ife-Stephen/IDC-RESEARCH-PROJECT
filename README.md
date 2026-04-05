# IDC-RESEARCH-PROJECT

---
# INVADUCTAR-GPT

Multimodal AI Assistant for Medical Image Understanding & Chat
*By Ife Stephen*

---

## 🧬 Project Overview

INVADUCTAR-GPT is a prototype AI system that combines image-analysis and natural language understanding to support medical image (mammogram / IDC) interpretation and patient-friendly dialogue.
It features:

* A REST backend (Flask) that loads a pretrained CLIP model for image classification and a “DeepSeek” style LLM for explanation.
* A “zero-code” user flow: Upload image → Analyze → Get structured result + plain-language explanation; or ask general questions.
* Scoped for research prototype / demonstration; **not for clinical use**.

---

## 🧩 How it Works (Architecture)

```
[Browser UI] ←→ [Streamlit Frontend] ←→ [Flask API Backend]
                                               ├─ CLIP (vision model) → predicts label & confidence
                                               ├─ DeepSeek (LLM) → produces human-friendly explanation / chat
                                               └─ LangGraph orchestration (optional) managing tool-calls
```

### Key components

* **tools.py**: defines two core operations

  * `analyze_image(image_path)`: accepts uploaded image path, returns dict `{prediction, confidence, scores}`
  * `explain_result(result)`: accepts result dict, calls LLM, returns `{ result: explanation }`
* **agent.py**: decision-making node, interprets user commands (e.g. `ANALYZE_IMAGE: path`)

  * If image command: runs analysis → explanation
  * Else: routes to general chat via LLM
* **app.py**: Streamlit/Next.js module (depending on your choice) that handles UI, uploads, conversation rendering, and chat input.
* **frontend/**: (chat / image upload)
* **backend/**: Flask server exposing endpoints to upload image, trigger analysis, and serve chat responses.

---

## 🚀 Setup & Local Run

### Backend

1. Clone the repository:

   ```bash
   git clone https://github.com/Ife-Stephen/IDC-RESEARCH-PROJECT.git
   cd IDC-RESEARCH-PROJECT/backend
   ```
2. Create and activate a Python virtual environment:

   ```bash
   python -m venv venv
   .\venv\Scripts\activate    # Windows  
   source venv/bin/activate    # macOS/Linux  
   ```
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```
4. Set your environment variables (e.g., in `.env`):

   ```bash
   TOKEN=hf_xxxYOUR_HUGGINGFACE_TOKENxxx
   ```
5. Start the Flask server:

   ```bash
   python api_server.py
   ```

   The server should listen on `http://127.0.0.1:5000` (default).

### Frontend

1. In the project root:

   ```bash
   cd frontend
   npm install
   ```
2. Set API URL in `.env.local`:

   ```bash
   NEXT_PUBLIC_API_URL=http://localhost:5000
   ```
3. Run development server:

   ```bash
   npm run dev
   ```
4. Open browser: `http://localhost:3000`
   Upload image or chat to interact with the system.

---

## ✅ Usage Examples

* **Image upload flow**

  1. Upload a mammogram image (.jpg/.png)
  2. Click **Analyze**
  3. View structured output (prediction, confidence)
  4. Read AI’s explanation, including patient-friendly language and next-step suggestions.
* **General chat flow**

  1. Enter question (e.g., “What does ‘malignant tumor’ mean?”)
  2. Receive answer from LLM (without image upload).

---

## ⚠️ Important Notes

* **This project is for demonstration and research only. It is *not* a clinical diagnostic tool.**
* The models used are **pretrained** and not clinically validated.
* Users must consult qualified clinicians for any medical decision.
* Model performance depends on dataset quality and may not generalize.

---

---

## 🧠 Tech Stack

* Python 3.10+
* Flask & flask-cors (backend)
* PyTorch / Transformers (for CLIP + LLM)
* LangGraph / LangChain-Core for orchestration
* Streamlit used if alternative UI chosen.

---

## 🔮 Future Work

* Fine-tune the CLIP model and LLM on dedicated medical imaging + pathology data.
* Add bounding box / heatmap segmentation (explainable AI) for lesions.
* Web deployment (Docker + Kubernetes) with GPU acceleration.
* Logging & monitoring for model predictions, accuracy tracking, and user feedback.
* Secure authentication and HIPAA-compliant data handling.

---

---

## 🤝 Contributing

1. Fork the repo
2. Create a new branch `feature/your-feature`
3. Commit your changes & push
4. Submit a Pull Request
5. Ensure all CI tests pass (if configured).

---

### 👏 Acknowledgments

Thanks to the Hugging Face open models community for enabling this development.

---
