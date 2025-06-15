# Grama_Voice_Qualcomm_Hackathon
Voice based assistant for rural population in India

Multilingual Speech-to-Text & RAG Question-Answering System
This is a Flask-based web application that supports speech-to-text transcription, language detection, machine translation, and contextual question-answering (QA) using Retrieval-Augmented Generation (RAG) pipelines. It supports both English and Hindi inputs (typed or spoken), using Faster-Whisper, Gemma-3-1b, and OpenAI-compatible LLM endpoints via LM Studio.

📌 Features
🔊 Speech-to-Text using Faster-Whisper (offline ASR)

🧠 Context-aware QA using RAG and custom vectorstores

🌍 Multilingual Support: Detects and translates Hindi ↔ English

🤖 LLM Integration: Works with google/gemma-3-1b hosted locally via LM Studio

📁 Document Retrieval from pre-built vectorstores

⚙️ Modular code via Flask blueprints (retrieve_services.py, llm_services.py)

🧪 API endpoints for testing and integration

🧰 Tech Stack
Component	Tool/Library
Backend	Flask (Python)
ASR	Faster-Whisper (large-v3)
Language Detection	langdetect
Translation/LLM	Gemma-3-1b (via OpenAI SDK + LM Studio)
Vector DB (RAG)	Custom vectorstores (db1, db2)
Environment	dotenv (.env) for config

🗂️ Directory Structure
bash
CopyEdit
project-root/
├── app.py                  # Main Flask app
├── retrieve_services.py    # Vectorstore loading + RAG blueprint
├── llm_services.py         # LLM + QA logic blueprint
├── static/                 # Frontend static files (e.g., audio)
│   └── audio/              # Pre-recorded audio prompts
├── frontend/               # UI (index.html, etc.)
├── .env                    # LM Studio config
└── voice.zip               # Audio files (uploaded)
🚀 Setup Instructions
1. Clone and Install
bash
CopyEdit
git clone <your-repo-url>
cd project-root
pip install -r requirements.txt
Make sure you have the following packages installed:

bash
CopyEdit
pip install flask faster-whisper langdetect openai python-dotenv
2. Configure .env
Create a .env file with:

ini
CopyEdit
LMSTUDIO_BASE_URL=http://127.0.0.1:1234/v1
LOCAL_LLM_MODEL_NAME=google/gemma-3-1b
Start LM Studio and load the Gemma model with the above name.

3. Pre-Build Vector Databases
Ensure these scripts exist and are executed:

bash
CopyEdit
python build_db1.py
python build_db2.py
These scripts must create and store vectorstores db1 and db2 for use in the RAG pipeline.

🧪 API Endpoints
/transcribe-audio (POST)
Converts audio (.webm) to text using Faster-Whisper.

FormData:

css
CopyEdit
audio: [audio file]
Returns:

json
CopyEdit
{
  "transcribed_text": "Hello world",
  "language": "en"
}
/process-text (POST)
Takes user text (Hindi or English), answers it using context (RAG), and returns a response in the same language.

JSON Body:

json
CopyEdit
{
  "text": "आपका नाम क्या है?",
  "pdf_context": "..." // optional
}
Returns:

json
CopyEdit
{
  "original_text": "आपका नाम क्या है?",
  "processed_text": "मेरा नाम चैटबॉट है।",
  "language": "hindi"
}
🖼️ Frontend Integration
Place your index.html and any static frontend files inside the frontend/ directory. Flask serves index.html at /.

Audio prompts for accessibility (stored in static/audio/wav1.mp3 to wav9.mp3) can be triggered via <audio> elements or JavaScript.

⚠️ Troubleshooting
Speech model not loading?

Ensure your system has 3GB+ RAM.

Try re-running pip install faster-whisper.

LLM not responding?

Ensure LM Studio is open and model name matches .env.

Vectorstore errors?

Re-run build_db1.py, build_db2.py.

Check correct file paths and format.

📸 Screenshots (Optional)
(Include UI/endpoint testing screenshots if applicable)

🙏 Credits
Faster-Whisper

LangDetect

LM Studio

OpenAI-compatible SDK

📄 License
This project is licensed under MIT License (or specify yours).
