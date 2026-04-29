# AutoTest — Agentic Developer Assistant

Takes a natural language programming request, generates the code, and commits it directly to a GitHub repository. Runs as a Streamlit app.

## Architecture

```
User prompt (Streamlit UI)
    └── OpenAI GPT (code generation)
            └── File writer (creates/updates files in repo)
                    └── GitHub API (commits via PyGithub)
                            └── Target repository
```

**Pipeline:**
1. User describes what they want built in the Streamlit input field.
2. The request goes to OpenAI for code generation with full repo context injected as system context.
3. Generated files are written locally.
4. PyGithub commits the changes directly to the configured repository.
5. A research agent supplements requests that need external knowledge (library docs, API specs).

## Usage

### Prerequisites

- Python 3.7+
- Git
- GitHub personal access token with `repo` scope
- OpenAI API key

### Install

```bash
git clone https://github.com/quinnhasse-test/AutoTest.git
cd AutoTest
pip install -r requirements.txt
```

### Configure

Create a `.env` file:

```env
OPENAI_API_KEY=your_openai_key
GITHUB_TOKEN=your_github_token
GITHUB_REPO=owner/repo-name
```

### Run

```bash
streamlit run app.py
```

Open [http://localhost:8501](http://localhost:8501), enter a programming request, and the assistant generates and commits the code.

## Features

- Natural language to code via GPT
- Direct GitHub commit via PyGithub — no manual copy-paste
- Research agent for library lookups
- Multi-language support
- Maintains project context across prompts in a session

## Dependencies

```
openai>=1.0.0
gitpython>=3.1.0
PyGithub>=2.0.0
streamlit>=1.28.0
requests>=2.31.0
python-dotenv>=1.0.0
```

Install with `pip install -r requirements.txt`.
