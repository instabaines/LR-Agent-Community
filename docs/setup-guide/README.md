<div align="center">

<img src="assets/icon-hero.svg" width="84" alt="A laptop running a local AI model" />

# Zero to App in 30 Minutes

### Pre-workshop setup &middot; LLM &amp; AI Agent Community

**📅 Saturday, June 6** &nbsp;·&nbsp; **📍 5520 Woodlawn Drive, Little Rock**

</div>

---

In the workshop we'll build a tiny web app that talks to an AI model running **entirely on your own laptop**. No cloud, no API keys, no accounts.

To keep the 30 minutes moving, please get set up **before you arrive**: watch the walkthrough video first, then complete the steps and run the 2-minute check at the end. You don't need to write any code beforehand — we'll do that together.

> [!WARNING]
> **Download the model at home, on good wifi.** The model is a few GB. Venue wifi will **not** handle 50 people downloading models at once — so get it done before Saturday.

---

## <img src="assets/icon-resources.svg" height="30" alt=""> Watch this first

> [!IMPORTANT]
> **Start here — this video is required, not optional.** It's the most complete walkthrough of everything you need: it covers **installing Git**, creating the **accounts** you'll use, and the extra **configuration** the quick steps below don't spell out. **Watch it all the way through first**, then come back and run through Steps 1–4 and the pre-flight check.

<div align="center">

[![Every Account and Tool You Need to Start Building with AI](https://img.youtube.com/vi/izi-qO9m_LE/maxresdefault.jpg)](https://youtu.be/izi-qO9m_LE)

**▶ [Every Account and Tool You Need to Start Building with AI](https://youtu.be/izi-qO9m_LE)**

</div>

### What you'll set up

| | Before Saturday | Why it matters |
|:---:|---|---|
| **▶** | [Watch the walkthrough](#watch-this-first) — **required, first** | Full setup: Git, accounts & configuration |
| **1** | [Install Ollama](#step-1-install-ollama) | Runs the AI model |
| **2** | [Download a model](#step-2-download-a-model) | The brain — *do this at home* |
| **3** | [Install Node.js](#step-3-install-nodejs) | Runs the web app |
| **4** | [Install a code editor](#step-4-install-a-code-editor) | Where we write the app |
| **✅** | [Pre-flight check](#pre-flight-check) | Confirm it all works |

---

## <img src="assets/icon-ollama.svg" height="30" alt=""> Step 1: Install Ollama

This is what runs the AI model on your machine.

- **Mac:** download from [ollama.com/download](https://ollama.com/download) and open it
- **Windows:** download the installer from [ollama.com/download](https://ollama.com/download) and run it
- **Linux:** open a terminal and run:

  ```bash
  curl -fsSL https://ollama.com/install.sh | sh
  ```

> [!TIP]
> **Check it worked.** Open a terminal and run the command below. If you see a version number, you're good.

```bash
ollama --version
```

---

## <img src="assets/icon-model.svg" height="30" alt=""> Step 2: Download a model

> 🏠 **Do this at home, on good wifi** — not at the venue.

Pick **one** of these small models and pull it in a terminal. Any of them works for the workshop, so just choose one.

**⭐ Recommended — Qwen 3.5 · 4B** &nbsp;(about 3.4 GB)

```bash
ollama pull qwen3.5:4b
```

**Lighter — Qwen 3.5 · 2B** &nbsp;(about 2.7 GB, for older or low-memory laptops)

```bash
ollama pull qwen3.5:2b
```

**Prefer Google's Gemma? — Gemma 4 · e2b** &nbsp;(about 7.2 GB)

```bash
ollama pull gemma4:e2b
```

> [!TIP]
> **Check it worked.** Run the model you pulled, type `hello` and press enter. If it replies, you're set. Type `/bye` to exit.

```bash
ollama run qwen3.5:4b
```

*(Swap `qwen3.5:4b` for whichever model you pulled.)*

---

## <img src="assets/icon-node.svg" height="30" alt=""> Step 3: Install Node.js

This is what runs the web app we'll build.

- Go to [nodejs.org](https://nodejs.org) and download the **LTS** version (the one on the left, marked *"Recommended"*)
- Install it with the default options

> [!TIP]
> **Check it worked.** In a terminal, run the command below. A version number of **v20 or higher** means you're set.

```bash
node --version
```

---

## <img src="assets/icon-editor.svg" height="30" alt=""> Step 4: Install a code editor

If you don't already have one, install **VS Code** from [code.visualstudio.com](https://code.visualstudio.com). Any editor you like is fine.

---

## <img src="assets/icon-preflight.svg" height="30" alt=""> Pre-flight check

Run this the **night before**. Each command should return something, not an error:

```bash
git --version
ollama --version
node --version
ollama run qwen3.5:4b "say hi"
```

*(Swap `qwen3.5:4b` for whichever model you pulled. The walkthrough video shows how to install Git if `git --version` errors.)*

Then open your web browser and go to **<http://localhost:11434>** — it should say **"Ollama is running."** That confirms the app will be able to reach the model.

**Tick these off before Saturday:**

- [ ] I watched the [walkthrough video](#watch-this-first) all the way through
- [ ] `git --version` returns a version number
- [ ] `ollama --version` returns a version number
- [ ] `node --version` returns **v20 or higher**
- [ ] `ollama run <your-model> "say hi"` gets a reply
- [ ] [http://localhost:11434](http://localhost:11434) says *"Ollama is running."*

---

## <img src="assets/icon-read.svg" height="30" alt=""> Further reading (optional)

Want a head start before the video? This short article walks through the same first steps in writing.

<div align="center">

<a href="https://open.substack.com/pub/theoyinbooke/p/run-it"><img src="https://substackcdn.com/image/fetch/$s_!6nBO!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcfc50749-a8e5-4716-8e71-de61b548117e_2468x1424.png" width="560" alt="Run it — article cover" /></a>

</div>

**[Run it](https://open.substack.com/pub/theoyinbooke/p/run-it)** — *Your first local AI model is 5 minutes away. Here's the exact setup.*
Olanrewaju Oyinbooke · *Your Local LLM* on Substack

---

## <img src="assets/icon-help.svg" height="30" alt=""> Need help?

If any of the above didn't work, or you're not sure, **come 30 minutes early** — we'll have people on hand to get you set up. It's much faster to fix before we start than during the workshop.

<div align="center">

### See you Saturday. 👋

*LLM &amp; AI Agent Community · Little Rock · Zero to App in 30 Minutes*

</div>
