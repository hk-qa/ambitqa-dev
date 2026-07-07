# AmbitQA 🎯

> **A RAG-powered QA assistant grounded in ISTQB Foundation Level, IEEE 829, and the Software Testing Life Cycle (STLC) — plus a companion artifact evaluator that scores any QA deliverable against weighted rubrics.**

🏆 **Winner — Codecademy Agentic AI Applications Bootcamp Contest #1** (2026)

🔗 **Live demo:** [ambitqa.com](https://ambitqa.com/)
🤖 **Chatbot:** [ambitqa.com/chatbot.html](https://ambitqa.com/chatbot.html)
🔬 **Evaluator:** [ambitqa.com/evaluator.html](https://ambitqa.com/evaluator.html)

Currently at **v1.2.0** — see [Changelog](#-changelog).

---

## 🤝 Hire Me

**Need QA work done faster, with documentation that passes any audit?**

I use **AmbitQA** as my personal force-multiplier to deliver senior-grade QA artifacts in a fraction of the typical time — grounded in ISTQB Foundation Level, IEEE 829, and modern STLC practices. Available for short engagements and ongoing retainers.

### What I can do for your team

| Engagement | Typical Outcome | Investment |
|---|---|---|
| **IEEE 829 Compliance Refresh** | Audit your existing QA documentation, generate compliant test plans, RTMs, and exit criteria | Fixed-fee, ~2 weeks |
| **Test Automation Framework Setup** | Scaffold Playwright, Cypress, or Selenium with Page Object Model and CI workflow, using your real HTML for working selectors | Fixed-fee, ~3-4 weeks |
| **QA Process Maturity Assessment** | Score your current QA artifacts against rubric-based standards, deliver a prioritized improvement roadmap | Fixed-fee, ~1 week |
| **Bug Triage & Severity Scoring** | Ongoing defect analysis with IEEE 829 bug reports and reproducibility validation | Monthly retainer |
| **API / Security / Performance Test Design** | Generate full test suites and execution plans across REST, GraphQL, OWASP Top 10, k6/JMeter | Per-project |
| **Custom QA Tooling** | Build internal QA tools tailored to your stack and workflow | Quoted on scope |

### Why work with me

- ✅ **Real QA practitioner**, not a generalist consultant
- ✅ **Tool-augmented delivery** — what would take a junior QA 2 weeks, I deliver in 3 days with higher quality
- ✅ **Methodology-grounded output** — every artifact references ISTQB / IEEE 829 sources, audit-ready by default
- ✅ **Transparent scoping** — fixed fees on defined deliverables, no surprises
- ✅ **Code stays yours** — all artifacts and frameworks are delivered as your property

### Get in touch

- 💼 **LinkedIn:** [linkedin.com/in/hkapur](https://linkedin.com/in/hkapur)
- 📧 **Email:** hitesh@ambitqa.com
- 📅 **Book a 20-minute intro call:** [Calendly link]

> _Currently accepting up to 2 new engagements per month. Best fit: startups and mid-size teams needing senior QA capacity without a full-time hire._

---

## 🌟 What it does

AmbitQA is a structured, retrieval-augmented chat agent that produces production-grade QA deliverables in seconds — not generic AI chat output. Every response is grounded in a curated methodology knowledge base and cites the exact sources used.

A separate **evaluator** scores any QA artifact (whether produced by AmbitQA or copy-pasted from anywhere) against weighted rubrics, returning a **PASS / WARN / FAIL** verdict with dimension scores, top issues, and an auto-generated improvement prompt.

### 14+ deliverable types
- **Test plans** (IEEE 829 format)
- **Test cases** — tabular and BDD/Gherkin
- **Bug reports** — full IEEE 829 defect structure
- **Requirements Traceability Matrices (RTM)**
- **Test execution summary reports**
- **Exit criteria checklists**
- **Lessons-learned documents**
- **Automation framework code** — Playwright (TypeScript), Cypress (JavaScript), Selenium WebDriver (Python + pytest), and BDD/Cucumber + Gherkin
- Plus risk-based strategies, accessibility checklists, exploratory test charters, API contracts, security test suites, performance test scenarios, and more

---

## ✨ Key features

### 🧠 Real RAG, not just a wrapper
- Curated knowledge base with methodology chunks (ISTQB, IEEE 829, STLC, automation patterns, OWASP, k6/JMeter, REST/GraphQL)
- Semantic keyword scoring + mode-aware retrieval boost
- Top-K relevant chunks injected into every prompt
- **Source citations on every response** — auditable, not hallucinated

### 🔬 Companion evaluator
A standalone artifact scoring engine (`evaluator.html`) that:
- Evaluates any QA artifact against 9 weighted rubrics (test plan, test cases, BDD, bug report, automation code, RTM, execution report, exit criteria, lessons learned)
- Returns **PASS / WARN / FAIL** verdict with dimension-level bar charts
- Lists the top issues found
- Generates an improvement prompt you can paste back into the chatbot
- Pre-scans for red flags before scoring
- Integrates with the chatbot via the 🔬 Evaluate button on every response

### 🔌 Multi-provider support
Works with multiple LLM providers — switch on the fly:
- **Anthropic** (Claude Sonnet 4.6 and other models)
- **OpenAI** (GPT-4, GPT-4o, GPT-4 Turbo)
- **Google** (Gemini Pro / Flash)
- **xAI** (Grok)
- **OpenRouter** (any model on their platform)
- **Custom endpoint** — bring your own OpenAI-compatible API

Per-provider API keys stored separately in localStorage. Custom model field for any provider.

### 🧭 11 STLC modes
Each mode has phase-specific quick actions and RAG retrieval boost:
- All Phases
- Requirements Review
- Test Planning
- Test Design
- Test Execution
- Defect Management
- Test Closure
- Test Automation (Playwright / Cypress / Selenium / BDD)
- **API Testing** (REST, GraphQL, Postman, JWT/OAuth)
- **Security Testing** (OWASP Top 10, XSS/injection/IDOR, Burp/ZAP)
- **Performance Testing** (k6, JMeter, load/stress/spike/soak)

### 🎯 Target real applications
- Set a target URL → agent fetches the page via CORS proxy
- Extracts forms, buttons, navigation, and structure from the HTML
- Generates **site-specific deliverables** referencing actual UI elements

### 📎 Multi-modal attachments
Three attachment paths to give the agent maximum context:
- **Screenshots** (PNG/JPG/WEBP/GIF) — vision capability sees the UI directly
- **PDFs** — native PDF understanding
- **HTML files** — DOM structure extracted and injected for **real, working selectors in automation code**

Attach via 📎 button, drag-and-drop, or paste from clipboard.

### 🤖 Test Automation mode
A dedicated STLC phase that generates production-ready code:
- Playwright POM + tests + `playwright.config.ts` + README
- Cypress POM + spec files
- Selenium WebDriver framework (Python + pytest)
- BDD Gherkin features + Cucumber.js step definitions
- GitHub Actions CI workflow
- **Honest about selector sources** — comments tell you whether selectors came from real HTML or were inferred from screenshots

### 📤 Five export formats
- **TXT** — clean plain text (markdown stripped, tables formatted as records)
- **MD** — raw markdown (great for GitHub, Notion, Obsidian)
- **HTML** — standalone styled document (one click away from PDF via browser print)
- **Jira CSV** — direct-importable for test cases and bug reports
- **Auto-form fill** — when the agent asks for structured input, a modal opens with proper input fields

### ⏸ Stop generation
Cancel in-flight responses via the Stop button (AbortController). Useful when an output is going in the wrong direction.

### 🎨 Polished UI
- Three-column resizable layout with drag handles
- Both side panels can collapse for full-screen chat
- Light & dark mode (defaults to system preference)
- Indigo/violet brand palette
- WCAG AAA-compliant text contrast
- Mode-aware autosuggestions in the chat box (↑↓ navigation, Enter to pick)
- Version badge driven by a single constant for clean release management
- Keyboard-friendly throughout

---

## 🏗 Architecture

**Pure browser-based** — no backend, no database, no server-side code.

- Static HTML + vanilla JS + CSS (~2,000 lines)
- Hosted on GitHub Pages
- Calls Anthropic / OpenAI / Google / xAI / OpenRouter APIs directly via Messages API
- API keys entered in-browser and never stored or transmitted to any third party
- Multi-modal request format (images, PDFs as binary; HTML as extracted text context)
- 48K token output ceiling with truncation detection + continue button

```
+--------------------------------------------------------------+
|  Browser (the entire app)                                    |
|                                                              |
|  +------------------+    +-----------------+                 |
|  | Knowledge base   |    | STLC mode       |                 |
|  | (curated chunks) |    | (11 modes)      |                 |
|  +--------+---------+    +--------+--------+                 |
|           |                       |                          |
|           v                       v                          |
|  +-----------------------------------------+                 |
|  | Semantic retrieval (top-K by mode boost)|                 |
|  +--------------------+--------------------+                 |
|                       |                                      |
|                       v                                      |
|  +-----------------------------------------+                 |
|  | Prompt builder + multi-modal content    |                 |
|  | (text + images + PDFs + HTML context)   |                 |
|  +--------------------+--------------------+                 |
|                       |                                      |
|                       v                                      |
|         api.anthropic.com / api.openai.com / etc.            |
|              (selected provider + model)                     |
|                       |                                      |
|                       v                                      |
|  +-----------------------------------------+                 |
|  | Markdown renderer + export pipeline     |                 |
|  | (TXT . MD . HTML . Jira CSV)            |                 |
|  +--------------------+--------------------+                 |
|                       |                                      |
|                       v                                      |
|  +-----------------------------------------+                 |
|  | Evaluator (rubric-based scoring)        |                 |
|  | PASS / WARN / FAIL + improvement prompt |                 |
|  +-----------------------------------------+                 |
+--------------------------------------------------------------+
```

---

## 🚀 How to use

### Chatbot

1. Visit the **[chatbot](https://ambitqa.com/chatbot.html)**
2. Pick a **provider** (Anthropic, OpenAI, Google, xAI, OpenRouter, or Custom)
3. Paste your **API key** for that provider (used only in this browser session)
4. **Pick an STLC mode** from the left panel
5. **(Optional)** Set a target URL in the right panel for site-specific deliverables
6. **(Optional)** Attach screenshots or HTML files for visual/structural context
7. Use a **quick action** or type your prompt — start typing to see autosuggestions
8. **Export** the result as TXT, MD, HTML, or Jira CSV
9. Click **🔬 Evaluate** on any response to score it

### Evaluator

1. Visit the **[evaluator](https://ambitqa.com/evaluator.html)** (or click the 🔬 button in chatbot)
2. Paste any QA artifact (test plan, test cases, bug report, etc.)
3. Select the artifact type
4. Get instant verdict, scores, issues, and improvement prompt

---

## 🔐 Privacy & security

- Your API key is **only used in the browser session** — never sent to any server other than your selected provider's API
- No analytics, no tracking, no cookies
- Code is fully open-source — audit it yourself
- All requests use explicit browser-access opt-ins required by each provider

**Recommendation:** Set per-key spending caps in your provider's console for any keys used in browser-based tools.

---

## 📚 Knowledge base coverage

| Source | Topics |
|---|---|
| **ISTQB Foundation Level** | Test design techniques (EP, BVA, decision tables, state transition), severity/priority guide |
| **IEEE 829** | Test plan, test case, defect report, RTM templates |
| **STLC** | All 5 phases (Requirements Review → Test Closure) |
| **BDD** | Gherkin syntax, scenario writing |
| **Agile QA** | Shift-left testing, Definition of Done |
| **Automation** | Playwright, Cypress, Selenium WebDriver, BDD/Cucumber, Page Object Model |
| **API Testing** | REST, GraphQL, Postman, JWT, OAuth |
| **Security Testing** | OWASP Top 10, XSS, injection, IDOR, Burp Suite, ZAP |
| **Performance Testing** | k6, JMeter, load/stress/spike/soak patterns |

---

## 🛠 Tech stack

- **AI:** Anthropic, OpenAI, Google, xAI, OpenRouter (any model, switchable)
- **Frontend:** Vanilla HTML / CSS / JavaScript (no framework, no build step)
- **Hosting:** GitHub Pages
- **No backend, no database, no dependencies**

---

## 📋 Changelog

### v1.2.0 (current)
- Stop generation button (AbortController)
- Version badge driven by `QA_NEXUS_VERSION` constant
- Custom model field with persistence
- Custom provider flow with URL validation gating
- Multiple UX fixes for evaluator and chatbot

### v1.1.0
- Multi-provider support (Anthropic, OpenAI, Google, xAI, OpenRouter, Custom)
- Three new STLC modes: API Testing, Security Testing, Performance Testing
- Companion evaluator with 9 weighted rubrics
- Evaluate button (🔬) on every response toolbar
- Nav restructured

### v1.0.0
- Initial release as Codecademy bootcamp capstone
- 8 STLC modes, RAG knowledge base, multi-modal input, 5 export formats

---

## 🐞 Known limitations

- **CORS-blocked sites** — page fetch falls back to URL + description mode (workaround: attach HTML file or screenshot)
- **Token limits** — very large outputs (~48K tokens) may be truncated; a Continue button resumes the response
- **No conversation persistence** — refreshing the page clears history (intentional for privacy)
- **Browser API key** — anyone with access to your browser session can see the key entered in that session (not stored persistently, but visible in JS memory during use)

---

## 📄 License

**Copyright © 2026 Hitesh Khaneja. All rights reserved.**

This code is published for **portfolio demonstration and educational reference**.

**You may:**
- ✅ View, read, and study the source code
- ✅ Reference patterns or approaches in your own original work
- ✅ Use the live demo with your own API key
- ✅ Share links to this repository and the live site

**You may NOT:**
- ❌ Copy, redistribute, or republish this code or any substantial portion
- ❌ Deploy this code (in whole or in part) to any public or commercial service
- ❌ Use this code in any commercial product or paid offering
- ❌ Remove attribution or claim authorship

See [LICENSE](./LICENSE) for full terms.

For commercial licensing inquiries, please contact via LinkedIn (linked above).

> The methodology knowledge base references (ISTQB Foundation Level concepts, IEEE 829 templates, STLC definitions, OWASP Top 10, k6/JMeter patterns) are based on publicly available industry standards and are not claimed as original works.

---

## 🙏 Acknowledgments

- **[Codecademy](https://www.codecademy.com)** for the Agentic AI Applications Bootcamp — and for awarding AmbitQA the Contest #1 winner spot
- **[Anthropic](https://www.anthropic.com)** for Claude and the multi-modal Messages API
- **OpenAI, Google, xAI** for their respective LLM APIs
- The ISTQB, IEEE, and OWASP communities for the methodology foundations this is built on

---

## 📱 Connect

Built by **Hitesh Kapur** — find me on [LinkedIn](https://www.linkedin.com/) · #CodecademyAgenticAIBootcamp
