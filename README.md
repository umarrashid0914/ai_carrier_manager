# AI Career Co‑Pilot – Resume Analyzer

A full‑stack Flask application that leverages a local **Large Language Model** (LLM) to provide expert‑level resume analysis and career guidance. Upload your resume (PDF, DOCX, or TXT), specify a target role, and get an instant, personalised report covering your existing skills, missing competencies, a learning roadmap, and tailored interview questions – all processed **offline** for complete data privacy.

---

## ✨ Features

- 📄 **Resume Parsing** – Supports PDF, DOCX, and plain text uploads.
- 🧠 **AI Analysis** – Uses a local LLM (via Ollama) or OpenAI’s API to:
  - Extract skills from your resume.
  - Identify skills missing for your target role.
  - Generate a step‑by‑step learning roadmap.
  - Suggest 5 interview questions.
- 🔐 **User Authentication** – Sign up / login system with password protection.
- 📚 **History Dashboard** – View all past analyses and roadmaps.
- 💾 **Permanent Storage** – SQLite (or TiDB/MySQL) to keep your data safe.
- 🎨 **Modern UI** – Clean, responsive design with CSS styling.

---

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/ai-resume-analyzer.git
cd ai-resume-analyzer
```

### 2. Set up a virtual environment (recommended)
```bash
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install flask sqlalchemy openai pypdf2 python-docx
```
> If you use SQLite (default), you do not need `pymysql`. For MySQL/TiDB, also install `pymysql`.

### 4. Configure the AI provider

You can choose between **local LLM (Ollama)** or **OpenAI API**.

#### Option A: Use a local model with Ollama (recommended for privacy)
- Install [Ollama](https://ollama.com) and pull a model (e.g., Mistral, Gemma, Phi-3):
  ```bash
  ollama pull mistral
  ```
- Open `ai.py` and set:
  ```python
  client = openai.OpenAI(
      base_url="http://localhost:11434/v1",
      api_key="ollama",           # any string works
  )
  model_name = "mistral:latest"   # or "gemma2:2b", etc.
  ```
- Make sure Ollama is running (`ollama serve` in a separate terminal).

#### Option B: Use OpenAI’s cloud API
- Get an API key from [platform.openai.com](https://platform.openai.com/api-keys).
- In `ai.py`, set:
  ```python
  client = openai.OpenAI(api_key="sk-...your-key...")
  model_name = "gpt-4o-mini"      # or "gpt-4", etc.
  ```
- For security, use environment variables instead of hard‑coding the key.

### 5. Configure the database (optional)

By default, the app uses **SQLite** (no extra setup). To use **TiDB/MySQL**, edit `db.py` with your connection string.

### 6. Run the application
```bash
python app.py
```
Visit `http://127.0.0.1:5000` in your browser.

---

## 📁 Project Structure
```
ai-resume-analyzer/
├── app.py                 # Main Flask application
├── db.py                  # Database connection
├── models.py              # SQLAlchemy models (User, Report)
├── ai.py                  # AI client and analysis function
├── static/
│   └── style.css          # Custom CSS
└── templates/
    ├── base.html          # Layout template
    ├── signup.html
    ├── login.html
    ├── dashboard.html     # Upload & results
    └── history.html       # Past analyses
```

---

## 🔧 How It Works

1. A user signs up / logs in.
2. On the dashboard, they paste a resume (or upload a file).
3. They enter a target job role (e.g., "Python Developer").
4. The app sends the resume text + role to the AI provider.
5. The AI returns a structured JSON with skills, missing skills, roadmap, and interview questions.
6. The report is displayed and saved to the database for future reference.

---

## 📜 License

This project is licensed under the **GNU General Public License v3.0** – see the [LICENSE](LICENSE) file for details.  
You are free to use, modify, and distribute this software, provided that any derivative work also remains open source under the same license.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!  
Feel free to check the [issues page](https://github.com/yourusername/ai-resume-analyzer/issues) or submit a pull request.

---

## 🙏 Acknowledgements

- [Flask](https://flask.palletsprojects.com/) – web framework
- [SQLAlchemy](https://www.sqlalchemy.org/) – ORM
- [Ollama](https://ollama.com) – local LLM runner
- [OpenAI](https://openai.com) – cloud AI API
- [PyPDF2](https://pypi.org/project/PyPDF2/) and [python-docx](https://python-docx.readthedocs.io/) – document parsing

---

**Made with ❤️ for career development and lifelong learning.**
