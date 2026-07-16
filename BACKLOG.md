# AmbitQA — Backlog

Ideas and improvements, done and not-yet-done. Not a roadmap with dates —
a working record of what's shipped and a place to capture what's next
before it's forgotten. Add, reprioritize, or delete freely.

---

## chatbot.html

### Open
- [ ] **"Clear all attachments" button** — each attachment currently has
  its own individual `×` remove button (works well for removing one of
  several), but there's no single action to clear all pending attachments
  at once. Small addition: a button near the attachment preview area,
  visible only when `pendingAttachments.length > 0`, calling something
  like `pendingAttachments = []; renderAttachmentPreview();`

### Done
- [x] Core chatbot built: 11 STLC modes (All Phases, Requirements Review,
  Test Planning, Test Design, Test Execution, Defect Management, Test
  Closure, Test Automation, API Testing, Security Testing, Performance
  Testing), RAG knowledge base with source citations, multi-modal
  attachments (screenshots/PDFs/HTML), 5 export formats, target-URL
  fetching, autosuggestions, resizable 3-column layout, light/dark mode
- [x] Stop generation button (AbortController)
- [x] User message copy-on-hover button
- [x] Provider-switch modal flow with "Keep current" cancel, per-provider
  key placeholders, slow-provider patience messages
- [x] Scroll-to-top / scroll-to-bottom navigation buttons — took several
  root-cause fixes to get fully right:
  - DOM-timing bug (buttons declared after `</script>` closed, so init
    ran against `null` and silently no-op'd) — fixed via `DOMContentLoaded`
  - Positioning anchored to raw viewport instead of the chat column's
    actual edge (landed on top of the right sidebar when open) — fixed
    with dynamic `getBoundingClientRect()`-based offset
  - Vertical collision with the input bar's send/stop buttons (hardcoded
    rem offset didn't track the input bar's real height) — fixed by
    deriving position from the input bar's actual layout
  - Staleness on panel toggle — `ResizeObserver` alone didn't reliably
    catch a sibling flipping to/from `display:none`; added an explicit
    reposition call from `togglePanel()` as a fallback
- [x] Hardened target-page CORS fetch: added a third fallback proxy
  (codetabs.com) and a short automatic retry pass before giving up
- [x] Deployed a dedicated Cloudflare Worker (`ambitqa-cors-proxy`) as the
  primary target-page fetch method, replacing sole reliance on flaky free
  public proxies (which turned out to apply per-referrer rate limiting) —
  free proxies kept as fallback
- [x] Added standalone 🔬 Evaluate Artifact nav button to launch the
  Evaluator directly, without needing a chatbot response first
- [x] Fixed: standalone Evaluate Artifact launch showed a stale artifact
  left over in sessionStorage from an earlier per-response Evaluate
  click — now explicitly cleared for a genuinely blank launch
- [x] Added 🔑 Change Key button for re-entering/fixing the active
  provider's key without switching providers away and back — this
  already existed in code but was invisible due to a CSS scoping bug
  (.home-badge styling was scoped to .nav-left only); fixed
- [x] Fixed multi-provider support — previously every request silently
  went to Anthropic regardless of the selected provider (function was
  literally named callClaude()); rewrote as callLLM() with proper
  routing for Anthropic (native), Google (Gemini format), and
  OpenAI-compatible (OpenAI/xAI/OpenRouter/Custom), including correct
  per-provider image/PDF handling
- [x] Updated deprecated default model IDs for Google (Gemini 1.5 series
  fully shut down), xAI (grok-beta deprecated), and OpenAI (GPT-4o-era
  models superseded) to current model IDs
- [x] Evaluator launch now passes the chatbot's active provider/model via
  sessionStorage, so the Evaluator opens pre-selected to match instead
  of always defaulting to Anthropic
- [x] Added Risk Assessment / Risk Register as a first-class deliverable
  type (previously only implicitly covered)

---

## evaluator.html

### Done
- [x] Core evaluator built: standalone artifact scoring engine, rubric-based
  PASS/WARN/FAIL verdict with dimension breakdown, red-flag pre-scan,
  improvement-prompt generation, sessionStorage integration with chatbot
- [x] Expanded from 9 to 12 weighted rubrics: added API Test Cases,
  Security Test Cases, and Performance Test Plan/Script
- [x] Added Risk Assessment / Risk Register rubric (13th) — previously
  these were misclassified by keyword auto-detect into an unrelated
  rubric (Security Test Cases), scoring them against criteria that never
  applied
- [x] Added multi-provider support (previously Anthropic-only, same
  hardcoded-endpoint pattern as chatbot's old bug) — mirrors chatbot's
  mechanism with Provider/Model dropdowns, per-provider key memory
  (persisted, unlike chatbot's session-only keys), and pre-selection
  when launched from the chatbot
- [x] Added click-to-browse file upload — the artifact drop zone
  previously only accepted drag-and-drop, no file-picker fallback
- [x] Added ✕ Clear button to reset the artifact text, file input,
  type dropdown, and any previous results back to a fresh state in one
  click

---

## Site / brand / ops

### Done
- [x] Rebranded QA Nexus → AmbitQA (naming research, USPTO trademark
  check, LinkedIn search, Google competition check — all clear)
- [x] Purchased ambitqa.com and hiteshkapur.com via Cloudflare
- [x] Configured GitHub Pages custom domain + DNS (A records + CNAME,
  DNS-only/grey cloud) with HTTPS enforced
- [x] Set up Cloudflare Email Routing (hk@ambitqa.com,
  hitesh@ambitqa.com → Gmail)
- [x] Created staging repo (ambitqa-dev) for test-before-production
  workflow
- [x] Set up Calendly with AmbitQA branding
- [x] Consulting positioning: README.md Hire Me section, LICENSE
  (All Rights Reserved), HIRE_ME.md, LinkedIn profile updates
  (headline + About section)
- [x] Video script drafted (SUBMISSION_GUIDE.md), later adapted into a
  voiceover-optimized version (AmbitQA_Video_Script_Voiceover.md) for
  screen-recording + AI narration, including:
  - Restructured into short, TTS-friendly sentences with explicit
    on-screen-action cues
  - Beat 3 revised to set a real target URL before generating, so the
    demoed artifact is actually grounded and scores well when evaluated
  - Removed all "narrate during generation" moments in favor of a
    stop-recording/resume-recording technique, since AI generation time
    is unpredictable and shouldn't be fought during editing
  - Beat 4's automation demo clarified: pick one framework (Playwright),
    pre-generate off-camera against the same target for consistency
  - Export demo swapped from Jira CSV to HTML (Jira CSV only appears on
    test-case/bug-report content, not the test plan shown in the demo)
- [x] README.md comprehensively updated: version numbers (chatbot and
  Evaluator now tracked independently), rubric count, current model
  names, Cloudflare Worker architecture, accurate privacy/security
  section (chatbot session-only vs. Evaluator persisted keys), full
  changelog through current versions
- [x] This backlog itself — didn't exist before, now does

---

## Format notes

- Keep entries short — a sentence or two of "what" and "why enough to
  remember it" is enough; implementation detail can wait until it's
  actually picked up (or is already captured above for completed work).
- [ ] open, [x] done (or just delete once shipped — whichever you prefer).
- No need to prioritize/order rigorously; skim top-to-bottom per section
  when picking what's next.
