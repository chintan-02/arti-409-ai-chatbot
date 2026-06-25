# 🤖 ARTI 409 AI Chatbot

A tiny, friendly chatbot that talks to **Claude** (Anthropic's AI) right from your
terminal. It's about 60 lines of Python.

> **Why does this repo exist?** We're using it to learn **GitHub Desktop** — how to
> commit, push, branch, and open a pull request. The chatbot is kept deliberately
> simple so the focus stays on Git and GitHub. New to GitHub Desktop? Start with
> **[TEACHING_GUIDE.md](TEACHING_GUIDE.md)**.

---

## What it does

You type a message, Claude types back — and it remembers the conversation as you go:

```
============================================================
  ARTI 409 AI Chatbot   (type 'quit' to exit)
============================================================

You: Explain what an API is, like I'm five.
Claude: An API is like a waiter at a restaurant...

You: quit
Goodbye! 👋
```

---

## Setup (do this once)

You'll need **Python 3.9+** installed.

1. **Install the required packages**
   ```bash
   pip install -r requirements.txt
   ```

2. **Add your API key**
   - Get a key from <https://console.anthropic.com/>
   - Copy `.env.example` to a new file named `.env`
   - Paste your key into `.env`:
     ```
     ANTHROPIC_API_KEY=sk-ant-...your-real-key...
     ```
   - 🔒 Your `.env` file is listed in [`.gitignore`](.gitignore), so your key will
     **never** be uploaded to GitHub. Keeping secrets out of Git is an important habit!

3. **Run the chatbot**
   ```bash
   python chatbot.py
   ```

---

## ✏️ Your turn (a quick GitHub Desktop exercise)

Add a line below with your name and the date you cloned this repo, then **commit and
push** the change using GitHub Desktop. This is the easiest way to see your first commit
show up on GitHub.

**Students who completed the setup:**

- _Add your name here!_

---

## How it works

| File                  | What it's for                                              |
| --------------------- | ---------------------------------------------------------- |
| `chatbot.py`          | The whole app — reads your input, calls Claude, streams the reply |
| `requirements.txt`    | The Python packages to install                             |
| `.env.example`        | A template for your API key (you copy it to `.env`)        |
| `.gitignore`          | Tells Git which files to ignore (like your secret `.env`)  |
| `TEACHING_GUIDE.md`   | Step-by-step GitHub Desktop walkthrough                    |

The chatbot uses the **`claude-opus-4-8`** model. Want faster, cheaper replies while
testing? Open `chatbot.py` and change the `MODEL` line to `"claude-haiku-4-5"`.

---

## License

[MIT](LICENSE) — free to use, change, and share.


---

# GitHub Actions, CI, and Rollback Lab

This repository was also used to practice a real-world Git and GitHub maintenance workflow. The main goal of this activity was to understand how developers keep a project healthy after changes are made.

In this lab, I practiced:

* Creating a separate Git branch
* Adding automated tests
* Creating a GitHub Actions workflow
* Opening and merging a pull request
* Reading CI status checks
* Intentionally breaking the code
* Watching GitHub Actions catch the failure
* Safely rolling back using `git revert`

---

## Why This Activity Matters

GitHub is not only used to store code. It is also used to protect code quality.

In real software and AI projects, a small change can break the system. Continuous Integration helps catch problems early by automatically running tests every time code is pushed or a pull request is created.

This activity helped me understand the professional workflow of:

```text
Build → Test → Push → Review → Merge → Break → Detect → Revert → Recover
```

---

## Workflow Practiced

The full workflow followed in this lab was:

```text
Create own GitHub repository
        ↓
Create a new branch: add-ci
        ↓
Add automated tests
        ↓
Add GitHub Actions workflow
        ↓
Push branch to GitHub
        ↓
Open pull request: add-ci → main
        ↓
GitHub Actions runs automatically
        ↓
CI check passes
        ↓
Merge pull request into main
        ↓
Pull latest main locally
        ↓
Break the code intentionally
        ↓
Push broken change to main
        ↓
GitHub Actions fails
        ↓
Use git revert to undo the bad commit
        ↓
Push revert commit
        ↓
GitHub Actions passes again
```

---

## Files Added for CI

### `test_chatbot.py`

This file contains small smoke tests for the chatbot.

The tests check that:

* The chatbot is using an expected Claude model name
* The system prompt still mentions `ARTI 409`

These tests are simple on purpose. The focus of the lab was to understand GitHub Actions, pull requests, and rollback behavior.

---

### `.github/workflows/ci.yml`

This file defines the GitHub Actions workflow.

The workflow runs automatically on:

* Every push
* Every pull request

The workflow performs these steps:

1. Checks out the repository code
2. Sets up Python 3.11
3. Installs project dependencies
4. Installs `pytest`
5. Runs the test suite

This creates an automatic safety check for the project.

---

## Intentional Failure

After the CI workflow was working, I intentionally changed the chatbot system prompt from:

```text
ARTI 409
```

to:

```text
your course
```

This caused the automated test to fail because the test expected the system prompt to still contain `ARTI 409`.

GitHub Actions detected the issue and showed a red failed check.

This demonstrated how CI can catch a regression automatically.

---

## Safe Rollback with Git Revert

To fix the broken commit, I used:

```bash
git revert HEAD
```

This created a new commit that reversed the bad change.

The important point is that `git revert` does not delete history. Instead, it records the fix as a new commit.

This is the safer approach for team projects because:

* The original mistake remains visible
* The rollback is clearly documented
* Other team members stay in sync
* The main branch returns to a working state

---

## Important Git Commands Used

```bash
git checkout -b add-ci
```

Creates a new branch for the CI work.

```bash
git add test_chatbot.py .github/workflows/ci.yml
```

Stages the test file and workflow file.

```bash
git commit -m "Add CI workflow and chatbot tests"
```

Creates a saved version of the CI changes.

```bash
git push -u origin add-ci
```

Pushes the branch to GitHub.

```bash
git switch main
git pull origin main
```

Switches back to the main branch and downloads the latest merged changes.

```bash
git revert HEAD
```

Safely undoes the latest bad commit by creating a new revert commit.

```bash
git push origin main
```

Pushes the rollback commit to GitHub.

---

## Skills Demonstrated

This lab demonstrates practical experience with:

* Git
* GitHub
* GitHub CLI
* GitHub Actions
* Continuous Integration
* Pull requests
* Branching
* Commits
* Remote repositories
* Automated testing with `pytest`
* Debugging failed CI runs
* Safe rollback using `git revert`
* Version control best practices

---

## Key Learning

The biggest learning from this activity is that professional development is not only about writing code. It is also about protecting the codebase, catching mistakes early, and recovering safely when something goes wrong.

CI gives developers an automatic safety net. Rollback gives developers a recovery plan.

Together, they help keep software and AI systems healthy over time.

