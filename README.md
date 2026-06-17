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
