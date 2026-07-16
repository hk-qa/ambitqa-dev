# AmbitQA — Defect Backlog

Defects found during development and testing, tracked in the same spirit
as the IEEE 829 defect structure AmbitQA's own Bug Report rubric scores
against. New defects go in **Open**; move to **Resolved** once fixed, with
root cause and resolution filled in.

---

## Summary

| ID | Title | Severity | Component | Status | Fixed In |
|---|---|---|---|---|---|
| DEF-001 | Multi-provider support completely non-functional | **Critical** | chatbot.html | Fixed | v1.4.0 |
| DEF-002 | Evaluator misclassifies Risk Assessments as Security Test Cases | High | evaluator.html | Fixed | evaluator v1.3.4 |
| DEF-003 | Target-page fetch unreliable on production domain | Medium | chatbot.html | Fixed | v1.3.8 |
| DEF-004 | Deprecated/stale model IDs cause 404s after routing fix | Medium | chatbot.html | Fixed | v1.4.1 |
| DEF-005 | "Change Key" button invisible due to CSS scoping bug | Medium | chatbot.html | Fixed | v1.4.0 |
| DEF-006 | Evaluator API key validation rejects valid non-Anthropic keys | Medium | evaluator.html | Fixed | evaluator v1.3.5 |
| DEF-007 | Scroll buttons never appear (DOM timing) | Medium | chatbot.html | Fixed | v1.3.7 |
| DEF-008 | Scroll buttons render over right sidebar | Low | chatbot.html | Fixed | v1.3.7 |
| DEF-009 | Scroll buttons collide with send/stop buttons | Low | chatbot.html | Fixed | v1.3.7 |
| DEF-010 | Scroll buttons stale/invisible after panel toggle | Low | chatbot.html | Fixed | v1.3.7 |
| DEF-011 | Standalone Evaluate launch shows stale artifact from prior session | Low | chatbot.html | Fixed | v1.3.9 |
| DEF-012 | README copyright name inconsistent with rest of document | Low | README.md | Fixed | — |
| DEF-013 | Auto-detect misclassifies Test Plan as Bug Report | High | evaluator.html | Fixed | evaluator v1.3.8 |
| DEF-014 | Evaluation fails with "Unterminated string in JSON" error | Medium | evaluator.html | Fixed | evaluator v1.3.8 |

**Open defects: 0** (as of this writing — add new entries above the line
when something breaks)

---

## Resolved — detail

### DEF-001 — Multi-provider support completely non-functional
**Severity:** Critical · **Component:** chatbot.html · **Fixed in:** v1.4.0

**Description:** Selecting any provider other than Anthropic (Google,
OpenAI, xAI, OpenRouter, Custom) and entering a valid key for that
provider always failed with an authentication error.

**Root cause:** The API-calling function was literally named
`callClaude()` and unconditionally sent every request to Anthropic's
hardcoded endpoint (`api.anthropic.com/v1/messages`) with a hardcoded
model (`claude-sonnet-4-6`), regardless of what was selected in the
provider/model dropdowns. The full provider-switching UI (labels, model
lists, console links, key modal) was correctly built and functional —
only the underlying network call was never actually wired to route
anywhere else. Likely went unnoticed because testing had mostly used
Anthropic keys.

**Resolution:** Renamed to `callLLM()` and rewrote with proper branching:
native format for Anthropic, Gemini's `generateContent` format for
Google, and standard OpenAI-compatible chat completions for
OpenAI/xAI/OpenRouter/Custom — including correct per-provider handling
of image/PDF attachments (Gemini supports inline PDF natively;
OpenAI-compatible format has no raw-PDF block, so a visible note is
substituted instead of silently dropping the attachment). Verified via
simulated requests (mocked `fetch`) confirming correct endpoint, headers,
and request/response shape for all 5 providers.

---

### DEF-002 — Evaluator misclassifies Risk Assessments as Security Test Cases
**Severity:** High · **Component:** evaluator.html · **Fixed in:** evaluator v1.3.4

**Description:** A legitimately well-structured risk assessment/register
document scored FAIL (22/100) when evaluated, graded against Security
Test Cases criteria (OWASP coverage, attack payload specificity) that
were never applicable to a risk register.

**Root cause:** No dedicated rubric existed for Risk Assessment/Register
as a document type among the (then) 12 rubrics. Auto-detect is a pure
keyword-frequency matcher with no structural awareness — a well-written
risk register naturally names its risk categories using security
vocabulary (auth bypass, XSS, session handling), which was enough
keyword overlap to force-match it into Security Test Cases over the much
weaker match against Test Plan (which only shares the single word "risk").

**Resolution:** Added a dedicated Risk Assessment / Risk Register rubric
with appropriate dimensions (risk category coverage, likelihood/impact
rating rigor, mitigation quality, completeness, IEEE 829 §9 format
compliance). Verified via keyword-overlap simulation against the actual
failing document: new rubric scores 7/10 keyword hits vs. 3/15 for
Security Test Cases — decisively correct classification going forward.

---

### DEF-003 — Target-page fetch unreliable on production domain
**Severity:** Medium · **Component:** chatbot.html · **Fixed in:** v1.3.8

**Description:** Fetching a target URL's HTML (for grounding generated
artifacts in real page structure) failed inconsistently — observed 403s,
429s, 500s, and CORS-header errors from the free public proxies in use
(allorigins.win, corsproxy.io), reproducible specifically and
consistently on `ambitqa.com` across multiple retries, while the same
requests succeeded on the `ambitqa-dev` staging domain.

**Root cause:** Free public CORS proxy services apply their own
rate-limiting/abuse protection, most likely per-referrer — heavy test
traffic from `ambitqa.com`'s origin during development plausibly tripped
a soft block on one or more proxies that `ambitqa-dev`'s lighter usage
hadn't triggered. Outside the app's control either way.

**Resolution:** Deployed a dedicated Cloudflare Worker
(`ambitqa-cors-proxy`) as the primary fetch method — fetches server-side
under the author's own account, with no third-party rate limits
involved. Free public proxies kept as fallback. Confirmed working via
DevTools Network tab (200 OK, request URL matching the Worker's
hostname) on both dev and production.

---

### DEF-004 — Deprecated/stale model IDs cause 404s after routing fix
**Severity:** Medium · **Component:** chatbot.html · **Fixed in:** v1.4.1

**Description:** After DEF-001 was fixed (requests correctly reaching
each provider's real endpoint), Google and xAI still failed — Google
with `models/gemini-1.5-pro is not found for API version v1beta`, xAI
with a 400 Bad Request against `grok-beta`.

**Root cause:** Default model IDs in `PROVIDER_MODELS` had gone stale.
Confirmed via each provider's current documentation: Google has fully
shut down all Gemini 1.0 and 1.5 models (all return 404), and xAI has
long deprecated `grok-beta` in favor of the `grok-4.x` family. OpenAI's
list (`gpt-4o` era) was also stale by the same elapsed time, though not
yet reported as broken.

**Resolution:** Updated to current model IDs verified directly from each
provider's docs: Google → `gemini-2.5-pro`/`gemini-2.5-flash`/
`gemini-3.5-flash`; xAI → `grok-4.3`/`grok-4.1-fast`; OpenAI →
`gpt-5.6-sol`/`gpt-5.6-terra`/`gpt-5.6-luna`. Left a code comment flagging
these as current-as-of-verification-date, since provider lineups reshuffle
every few months.

---

### DEF-005 — "Change Key" button invisible due to CSS scoping bug
**Severity:** Medium · **Component:** chatbot.html · **Fixed in:** v1.4.0

**Description:** No visible way existed to re-enter/fix an API key for
the currently active provider without switching providers away and back.

**Root cause:** The button and its handler (`openKeyModalForCurrentProvider()`)
already existed in code and were fully functional — but the shared
`.home-badge` CSS rule was scoped as `.nav-left .home-badge`, and this
particular button lived in `.nav-right`. It rendered as a bare, unstyled
default browser button among a nav bar full of properly-styled elements,
making it essentially invisible.

**Resolution:** Un-scoped the CSS rule so `.home-badge` styling applies
consistently regardless of which nav section it's used in.

---

### DEF-006 — Evaluator API key validation rejects valid non-Anthropic keys
**Severity:** Medium · **Component:** evaluator.html · **Fixed in:** evaluator v1.3.5

**Description:** Discovered while adding multi-provider support: the
Evaluator's key validation hard-required the key to start with `sk-`,
which would reject valid Google (`AIza...`) or xAI (`xai-...`) keys.

**Root cause:** Validation was written when the Evaluator was
Anthropic-only and never revisited.

**Resolution:** Relaxed to non-empty-only validation, matching the
chatbot's existing (permissive) pattern, with a provider-aware
placeholder hint shown instead of a hard format gate.

---

### DEF-007 — Scroll buttons never appear (DOM timing)
**Severity:** Medium · **Component:** chatbot.html · **Fixed in:** v1.3.7 (consolidated)

**Root cause:** `initScrollBtn()` executed synchronously as the `<script>`
block was parsed, but `#scrollUpBtn`/`#scrollDownBtn` are declared in the
HTML *after* that closing `</script>` tag — so `getElementById` returned
`null` for both and the guards silently no-op'd.

**Resolution:** Deferred init via `DOMContentLoaded` (falling back to
immediate execution if the document was already loaded).

---

### DEF-008 — Scroll buttons render over right sidebar
**Severity:** Low · **Component:** chatbot.html · **Fixed in:** v1.3.7 (consolidated)

**Root cause:** `position: fixed; right: 2rem` anchored to the raw
browser viewport, with no awareness of the resizable right sidebar —
landed on top of it whenever the panel was open.

**Resolution:** Computed the `right` offset dynamically from
`#chatMessages.getBoundingClientRect()` instead of a fixed value.

---

### DEF-009 — Scroll buttons collide with send/stop buttons
**Severity:** Low · **Component:** chatbot.html · **Fixed in:** v1.3.7 (consolidated)

**Root cause:** The vertical `bottom` offset was a hardcoded rem guess
that didn't account for the input bar's actual height.

**Resolution:** Derived the offset from the input bar's real
`getBoundingClientRect().top` instead.

---

### DEF-010 — Scroll buttons stale/invisible after panel toggle
**Severity:** Low · **Component:** chatbot.html · **Fixed in:** v1.3.7 (consolidated)

**Root cause:** `ResizeObserver` reliably caught direct resizes
(drag-resize, window resize) but didn't consistently fire when a sibling
panel flipped to/from `display:none` via a class toggle.

**Resolution:** Added an explicit reposition call from `togglePanel()`,
via `requestAnimationFrame`, as a reliable fallback alongside the
existing `ResizeObserver`.

---

### DEF-011 — Standalone Evaluate launch shows stale artifact from prior session
**Severity:** Low · **Component:** chatbot.html · **Fixed in:** v1.3.9 (hotfix)

**Root cause:** `window.open()` to a same-origin page carries over
`sessionStorage` from the opener tab. A prior per-response "Evaluate"
click had set `ambitqa_eval_artifact`; the standalone nav button never
set it, but also never cleared it, so the Evaluator picked up the
leftover value from earlier in the session.

**Resolution:** Standalone launch (no artifact to pass) now explicitly
`sessionStorage.removeItem('ambitqa_eval_artifact')` before opening.

---

### DEF-012 — README copyright name inconsistent with rest of document
**Severity:** Low · **Component:** README.md · **Fixed in:** —

**Description:** License section read "Copyright © 2026 Hitesh Khaneja,"
while every other reference in the document (Hire Me, Connect sections)
says "Hitesh Kapur."

**Root cause:** Likely a leftover typo from an earlier draft.

**Resolution:** Corrected to Hitesh Kapur for consistency. *(Flagged to
the author in case "Khaneja" was intentional for a legal-name reason —
not confirmed either way.)*

---

### DEF-013 — Auto-detect misclassifies Test Plan as Bug Report
**Severity:** High · **Component:** evaluator.html · **Fixed in:** evaluator v1.3.8

**Description:** A document explicitly titled "test plan," with repeated
verbatim mentions of "Test Plan Identifier," "Test Plan ID," etc., was
auto-detected as "Bug Report" and scored FAIL (0/100) against completely
inapplicable criteria (Steps to Reproduce, Severity Rationale, and so on).

**Root cause:** Same underlying class of bug as DEF-002. `detectType()`
counted keyword *presence* (boolean: does this keyword appear anywhere,
yes/no) rather than *frequency*. This means a document repeating "test
plan" five times scored no higher on that signal than a document
mentioning it once — while a single incidental match on a generic word
shared with an unrelated rubric (e.g., "environment," which any test
plan's Environmental Needs section would naturally contain, is also a
Bug Report keyword) counted equally toward that other rubric. With
enough small generic-word overlaps, an unrelated rubric could edge out
the correct one even though the document's actual dominant, repeated
signal pointed clearly elsewhere.

**Resolution:** Changed scoring from a boolean presence check to counting
total occurrences of each keyword. Verified via simulation: a
reconstructed version of the failing document (deliberately including a
couple of incidental "environment"/"priority" mentions to mirror the
likely real cause) now correctly classifies as Test Plan, while the
earlier Risk Assessment fix (DEF-002) and two other spot-checked document
types (Bug Report, Test Cases) still classify correctly — no regression.

---

### DEF-014 — Evaluation fails with "Unterminated string in JSON" error
**Severity:** Medium · **Component:** evaluator.html · **Fixed in:** evaluator v1.3.8

**Description:** Explicitly selecting "Test Plan" as the type (bypassing
auto-detect) and evaluating via Google/Gemini 2.5 Flash failed outright
with `Evaluation failed: Unterminated string in JSON at position 193
(line 6 column 106)` instead of returning a score.

**Root cause:** `max_tokens`/`maxOutputTokens` was hardcoded to 1500
across all providers. The expected JSON response includes a rationale
per scoring dimension, a top-issues list, and a full improvement prompt
— verbose enough that some models (apparently including Gemini 2.5
Flash on this response) can exceed 1500 tokens before finishing, cutting
the JSON off mid-string. `JSON.parse()` on a truncated string throws
exactly this "unterminated string" class of error.

**Resolution:** Raised the token ceiling to 2500 across all three
provider branches (Anthropic, Google, OpenAI-compatible). As
defense-in-depth, also improved the error message shown for this
specific failure signature ("unterminated string" / "unexpected end of
JSON input") to explain what likely happened and suggest retrying or
switching models, rather than surfacing the raw JS parser error text.

---

## Format notes

- New defect → add a summary row + detail section, status **Open**.
- Include Severity (Critical/High/Medium/Low), Component, Root Cause, and
  Resolution once fixed — the same fields AmbitQA's own Bug Report rubric
  scores for, so this doubles as a dogfooding example if useful for the
  video or portfolio.
- "Fixed In" references the version where the fix shipped; use "—" for
  non-versioned files (docs, config).
