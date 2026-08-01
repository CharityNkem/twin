# Charity Umoren — Digital Twin

An AI-powered chat app that acts as my digital twin. Visitors can ask it about my
career, background, skills, and experience, and it answers in character — drawing on
my LinkedIn profile and a personal summary. If it doesn't know an answer, or a visitor
wants to get in touch, it records the details for follow-up.

**Live demo:** https://twin-txjc.onrender.com/

## What it does

- Conversational digital twin built on the OpenAI Chat Completions API
- Grounds its answers in my LinkedIn profile (`linkedin.pdf`) and a short bio (`summary.txt`)
- **Tool calling** — records a visitor's email for follow-up, and logs any question it
  couldn't answer, both delivered as push notifications via Pushover
- Custom-themed [Gradio](https://www.gradio.app/) chat interface

## Tech stack

Python · Gradio · OpenAI API · pypdf · Pushover (notifications) · deployed on [Render](https://render.com/)

## Project structure

| File | Purpose |
| --- | --- |
| `app.py` | Gradio chat app and the OpenAI tool-calling loop |
| `context.py` | Builds the system prompt from `linkedin.pdf` + `summary.txt` |
| `tools.py` | Tool definitions and handlers (record email / unknown question) |
| `styles.py` | Custom CSS/JS theming and example prompts |
| `summary.txt` | Short personal bio used for context |
| `linkedin.pdf` | LinkedIn profile export used for context |
| `requirements.txt` | Python dependencies |

## Running locally

1. Clone the repo and install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

2. Set the required environment variables (or put them in a local `.env` file):

   ```
   OPENAI_API_KEY=your_openai_key
   PUSHOVER_USER=your_pushover_user_key
   PUSHOVER_TOKEN=your_pushover_app_token
   ```

3. Run it:

   ```bash
   python app.py
   ```

   The app starts on `http://127.0.0.1:7860`.

## Deployment (Render)

Deployed as a Render **Web Service**:

- **Build command:** `pip install -r requirements.txt`
- **Start command:** `python app.py`
- **Environment variables:** `OPENAI_API_KEY`, `PUSHOVER_USER`, `PUSHOVER_TOKEN` are set
  in the Render dashboard (never committed to the repo).

Each push to `main` triggers an automatic redeploy.

## Notes

- Secrets are kept out of version control via `.gitignore` and set as environment
  variables in the deployment platform.
- The twin only answers questions related to my career, background, skills, and
  experience, and always identifies itself as an AI.
