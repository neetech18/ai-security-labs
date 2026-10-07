# AI Security Testing Labs

**A hands-on, browser-based range for practising AI security testing — LLM apps, RAG pipelines and agentic / MCP systems.** Read the concept, then break a live (deliberately vulnerable) build of that layer yourself, flip a switch to the hardened build, and watch the control stop your payload.

No install, no server, no API keys, no external model. Everything runs client-side in a single HTML file.

![AI Security Testing Labs](docs/hero.png)

---

## ▶ Live demo

Once you enable GitHub Pages (see **Hosting** below), your copy is live at:

```
https://<your-username>.github.io/ai-security-labs/
```

---

## What's inside

- **23 playable exercises** across three layers, each a mini attack range:
  - **Lab 1 — LLM apps (8):** prompt injection, jailbreak, system-prompt leakage, sensitive-info disclosure, insecure output handling (XSS), unbounded consumption / DoS, hallucination, model/plugin supply chain.
  - **Lab 2 — RAG (7):** indirect injection, knowledge-base poisoning, tenant isolation, PII in the index, embedding inversion, re-ranking / citation abuse, vector-store security.
  - **Lab 3 — Agentic + MCP (8):** goal hijack, tool misuse via injection, excessive privilege, unsafe tool chaining / SSRF, memory poisoning, inter-agent trust abuse, human-in-the-loop bypass, MCP tool poisoning.
- **Vulnerable ⇆ Hardened toggle** on every console — run the *same* payload against the secure build and see the control (instruction-hierarchy boundary, output encoding, tenant pre-filter, PII redaction, approval gate, egress allow-list, trust-weighted re-ranking) block it.
- **Graduated hints**, a per-level **solution** button, and a collapsed **answer key** at the bottom.
- **Framework explainers** mapped to every exercise: **OWASP** LLM / ML / Agentic Top 10, **MITRE ATLAS**, **NIST AI RMF**.
- A little **confetti + "flag captured"** celebration when you solve one.

![A practice console](docs/console.png)

## How to use it

1. Open the page (your Pages URL, or `index.html` locally).
2. Scroll to any lab. Read the exercise cards, then drop to the **▶ Practice** console at the end of the section.
3. Pick a level chip, read the **target + objective**, type your payload, and hit **▶ Run attack**. You get **✓ SOLVED** only when you actually break it.
4. Flip the console to **Hardened** and run the same payload — watch it get **BLOCKED**, with the control named.
5. Stuck? Use **hint** (graduated) or **solution**. The full answer key is collapsed at the bottom of the page.

## How it works (and why it's safe)

The "LLM" is a small, deterministic, injection-susceptible component written in plain JavaScript — not a real model. That's deliberate: these labs teach the **controls and architecture**, which is where AI security actually lives. The only difference between the vulnerable and hardened builds is the engineering around the model.

Everything is synthetic. Agent "tools" in Lab 3 are **logging stubs** — they record the attempted call and return a mock result; nothing is moved, fetched, deleted or sent. All console output is HTML-escaped before it touches the page, so even the XSS exercise can't execute against the page itself.

## Hosting on GitHub Pages

**Option A — web upload (no command line)**
1. Create a new repository on GitHub named `ai-security-labs` (public).
2. Click **Add file → Upload files**, drag in everything from this folder (`index.html`, `README.md`, `LICENSE`, `.nojekyll`, the `docs/` folder), and commit.
3. Go to **Settings → Pages**. Under **Build and deployment → Source**, choose **Deploy from a branch**, pick branch **`main`** and folder **`/ (root)`**, and **Save**.
4. Wait ~1 minute. Your site is at `https://<your-username>.github.io/ai-security-labs/`.

**Option B — command line**
```bash
git init
git add .
git commit -m "AI Security Testing Labs"
git branch -M main
git remote add origin https://github.com/<your-username>/ai-security-labs.git
git push -u origin main
# then enable Pages in Settings → Pages (Deploy from a branch → main → /root)
```

> `.nojekyll` is included so GitHub Pages serves the files as-is. The whole app is one self-contained `index.html`, so nothing else needs to build.

## Run it locally

Just open `index.html` in any modern browser (Chrome, Edge, Firefox). No server needed. Offline, fonts fall back to system fonts; online, it loads IBM Plex from Google Fonts.

## Standards mapped

Each exercise references the frameworks a client report would use:

- **OWASP Top 10 for LLM Applications (2025)**, **OWASP ML Security Top 10**, **OWASP Agentic Security (ASI) Top 10 (2026)** — <https://genai.owasp.org>
- **MITRE ATLAS** — adversary tactics & techniques for AI — <https://atlas.mitre.org>
- **NIST AI RMF (AI 100-1)** and the **Generative AI Profile (AI 600-1)** — <https://www.nist.gov/itl/ai-risk-management-framework>

## ⚠️ Rules of engagement

This is a **training tool**. The techniques are for learning to **test and defend** AI systems. Run adaptations only against systems you **own or are explicitly authorised to test**. Never point these methods at production systems, real data, or third-party services without written permission. The authors accept no liability for misuse.

## License

MIT — see [LICENSE](LICENSE). Free to use, fork, and adapt for training. Attribution appreciated.

---

*Built as a companion to an AI Security Testing capability deck (LLM apps · RAG · Agentic AI + MCP). Contributions and new levels welcome — open an issue or PR.*
