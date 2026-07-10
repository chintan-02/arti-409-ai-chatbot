# ARTI 409 AI Chatbot — API Integration & CI/CD Engineering Lab

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic-API-191919?style=flat-square)
![Pytest](https://img.shields.io/badge/Testing-pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI-GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

**A focused engineering lab demonstrating LLM API integration, automated testing, continuous integration, pull requests, regression detection, and safe rollback.**

</div>

---

> [!NOTE]
> **Project level:** Completed course engineering lab.
>
> This repository is intentionally small. Its value is not application complexity; it demonstrates disciplined Git workflows, API-key handling, automated testing, GitHub Actions, pull-request practices, failure detection, and safe recovery.
>
> My current flagship work focuses on production-minded AI/ML systems, NLP, RAG, FastAPI, model evaluation, responsible AI, and full-stack AI product engineering.

---

## Project Overview

This project began as a lightweight command-line chatbot that connects to the Anthropic API and maintains conversation context during a terminal session.

It was later extended into a practical software-engineering lab covering:

- LLM API integration
- Environment-variable configuration
- Secret-management fundamentals
- Git branches and structured commits
- Pull-request workflows
- Automated testing with `pytest`
- Continuous integration with GitHub Actions
- Intentional regression testing
- CI failure investigation
- Safe rollback using `git revert`

The repository demonstrates an important AI engineering principle:

> Building an AI feature is only one part of the job. The code also needs testing, version control, failure detection, and a safe recovery process.

---

## Engineering Snapshot

| Area | Implementation |
|---|---|
| Application | Python command-line chatbot |
| AI provider | Anthropic API |
| Conversation behavior | In-session message history |
| Configuration | Environment variables with `.env` |
| Testing | `pytest` smoke tests |
| Continuous integration | GitHub Actions |
| Collaboration workflow | Feature branch and pull request |
| Failure exercise | Intentional regression |
| Recovery method | `git revert` |
| Primary purpose | Git, CI/CD, testing, and API integration practice |

---

## What the Chatbot Does

The user enters a message in the terminal, the application sends the conversation to the configured Anthropic model, and the response is streamed back to the command line.

Example interaction:

```text
============================================================
  ARTI 409 AI Chatbot   (type 'quit' to exit)
============================================================

You: Explain what an API is in simple language.

Claude: An API is a structured way for two software systems
to communicate with each other...

You: quit

Goodbye!
```

The chatbot keeps conversation history during the active session so follow-up questions can use earlier context.

---

## High-Level Architecture

```text
User enters terminal message
            ↓
Python validates the input
            ↓
Conversation history is updated
            ↓
Anthropic API request is created
            ↓
Model response is streamed
            ↓
Response is displayed in the terminal
```

---

## Repository Structure

```text
arti-409-ai-chatbot/
│
├── chatbot.py
├── test_chatbot.py
├── requirements.txt
├── .env.example
├── .gitignore
├── TEACHING_GUIDE.md
├── LICENSE
├── README.md
│
└── .github/
    └── workflows/
        └── ci.yml
```

### File responsibilities

| File | Purpose |
|---|---|
| `chatbot.py` | Runs the command-line chatbot and Anthropic API interaction |
| `test_chatbot.py` | Contains smoke tests used by CI |
| `requirements.txt` | Lists Python dependencies |
| `.env.example` | Documents the required environment-variable structure |
| `.gitignore` | Prevents common local and secret files from being tracked |
| `TEACHING_GUIDE.md` | Provides the original GitHub Desktop learning walkthrough |
| `.github/workflows/ci.yml` | Defines the automated GitHub Actions test workflow |
| `LICENSE` | MIT license |

---

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/chintan-02/arti-409-ai-chatbot.git
cd arti-409-ai-chatbot
```

### 2. Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure the API key

Copy the example environment file:

```bash
cp .env.example .env
```

Add your Anthropic API key:

```text
ANTHROPIC_API_KEY=your-api-key
```

> [!WARNING]
> Never commit a real API key.
>
> The `.gitignore` file is configured to exclude `.env`, but developers should still verify staged files before every commit.

### 5. Run the chatbot

```bash
python chatbot.py
```

### 6. Run the tests

```bash
pytest
```

---

## GitHub Actions Continuous Integration

The repository includes a GitHub Actions workflow that automatically runs the test suite when code is pushed or a pull request is opened.

### CI workflow

```text
Push or pull request
        ↓
GitHub Actions starts
        ↓
Repository code is checked out
        ↓
Python environment is created
        ↓
Dependencies are installed
        ↓
pytest executes
        ↓
Workflow passes or fails
```

The workflow performs these core steps:

1. Checks out the repository
2. Configures Python
3. Installs dependencies
4. Installs or invokes `pytest`
5. Runs the automated tests
6. Reports the result in GitHub

This provides an automated safety check before code changes are merged.

---

## Branch and Pull-Request Workflow

The lab used a feature-branch workflow rather than making every change directly on `main`.

```text
Create feature branch
        ↓
Implement tests and CI workflow
        ↓
Commit changes
        ↓
Push branch
        ↓
Open pull request
        ↓
GitHub Actions runs
        ↓
Review CI result
        ↓
Merge into main
```

Example commands:

```bash
git checkout -b add-ci
git add test_chatbot.py .github/workflows/ci.yml
git commit -m "Add CI workflow and chatbot tests"
git push -u origin add-ci
```

After the pull request was reviewed and CI passed, the branch was merged into `main`.

---

## Intentional Regression Exercise

To understand how CI protects a codebase, the chatbot was intentionally changed in a way that violated an existing test expectation.

The automated test expected the system configuration to contain the course identifier:

```text
ARTI 409
```

The value was temporarily changed, causing the test to fail.

GitHub Actions detected the regression and displayed a failed workflow result.

This exercise demonstrated that CI can catch unintended behavior before additional changes are built on top of a broken state.

---

## Safe Recovery with `git revert`

The regression was corrected using:

```bash
git revert HEAD
```

Unlike deleting or rewriting Git history, `git revert` creates a new commit that reverses an earlier change.

This is safer in collaborative repositories because:

- The original change remains visible
- The corrective action is documented
- Team members do not need to repair rewritten history
- The repository returns to a known working state
- CI can verify that the correction succeeded

Recovery workflow:

```text
Broken commit reaches main
        ↓
GitHub Actions fails
        ↓
Failure is investigated
        ↓
git revert creates corrective commit
        ↓
Corrective commit is pushed
        ↓
GitHub Actions runs again
        ↓
Tests pass
```

---

## Testing Scope

The repository uses lightweight smoke tests because the primary objective was learning CI and Git workflow fundamentals.

The tests verify selected application assumptions such as:

- Expected model configuration format
- Presence of the course context in the system prompt
- Importable application configuration
- Basic regression protection

The test suite is intentionally limited and should not be interpreted as production-level LLM application coverage.

A larger AI application would also test:

- API failure handling
- Timeouts and retries
- Invalid or empty input
- Structured response validation
- Rate-limit behavior
- Provider fallback
- Prompt injection controls
- Output safety checks
- Token and cost limits
- Observability and logging

---

## Skills Demonstrated

### AI and API Integration

- Anthropic API usage
- Conversation-history handling
- Streaming model responses
- Environment-based configuration
- Separation of secrets from source code

### Software Engineering

- Modular Python application structure
- Dependency management
- Basic automated testing
- Regression protection
- Error-aware development practices

### Git and Collaboration

- Feature branches
- Structured commits
- Pull requests
- Merge workflow
- Remote repositories
- Transparent history
- Safe rollback

### DevOps Foundations

- GitHub Actions
- Continuous integration
- Automated test execution
- Failed-workflow investigation
- Recovery verification

---

## Limitations

- Small command-line learning application
- No web or mobile interface
- No database or persistent conversation storage
- No authentication or user management
- Minimal test coverage
- No structured logging or monitoring
- No retry or fallback provider architecture
- No prompt-evaluation framework
- No token, latency, or cost dashboard
- No production security review
- Not intended as a production chatbot

---

## Key Learning

This project reinforced that professional AI engineering requires more than calling a model API.

A reliable workflow also requires:

```text
Build
  → Test
  → Commit
  → Review
  → Integrate
  → Detect failures
  → Recover safely
  → Verify stability
```

The most important outcome was learning how automated tests, continuous integration, pull requests, and transparent rollback practices work together to protect a codebase.

---

## Current Applied AI/ML Work

My current flagship projects include:

- [TriageAI — ESI Clinical Intake & Care Routing Assistant](https://github.com/chintan-02/triageai-esi-care-routing)
- [PolicyGPT Enterprise — Evidence-First RAG for Policy and Compliance](https://github.com/chintan-02/policygpt-enterprise)
- [ResumeIQ — AI Resume Intelligence Platform](https://github.com/chintan-02/smart-resume-classifier)
- [Applied AI/ML Engineering Portfolio](https://chintan-patel-ai.netlify.app/)

---

## Author

**Chintan Patel**

- [GitHub](https://github.com/chintan-02)
- [LinkedIn](https://www.linkedin.com/in/chintan-patel-987765129/)
- [Portfolio](https://chintan-patel-ai.netlify.app/)

---

## License

This project is available under the [MIT License](LICENSE).

---

## Repository Note

This repository remains public as evidence of API integration, Git, testing, CI/CD, pull-request, and rollback fundamentals. It is not one of my current flagship AI engineering projects.
