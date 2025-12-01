<!-- docs/portfolio-cv-positioning.md -->

# Portfolio Impact + CV Positioning

This project is a strong “product-meets-AI-automation” story. Here’s how to position it in your portfolio and resume.

---

## ✅ What this project demonstrates

### Product skills
- Built an end-to-end user workflow with clear UX states (JD present vs missing).
- Designed adaptive scoring logic to avoid misleading UX.
- Turned complex model outputs into a polished user-facing artifact (email).
- Iterated based on failure cases (schema drift, parsing issues, UI inconsistencies).

### Technical skills
- Prompt engineering with hard rules and schema guarantees.
- Multi-stage LLM orchestration (ATS → Job Match → Impact → Role Signals → Rewrite → Summary).
- Robust JSON extraction / sanitization for model outputs.
- HTML email generation with conditional rendering and scoring normalization.
- n8n automation + integrations (PDF extraction, OpenAI, Gmail).

### Business value
- Replaces manual resume review time.
- Improves ATS-readiness + job alignment clarity for candidates.
- Scales across roles with preset-aware evaluation.

---

## 🧾 Resume positioning

### Best section to place it
Choose based on your profile:
- **Projects** (recommended)
- **Experience** (if used in production or for your org)
- **Portfolio / AI Automation** (if you have a dedicated section)

### Title options
Pick one based on your target role:

**For Product / PM roles**
- *AI Resume Diagnostic & JD Match Automation (n8n + LLMs)*
- *LLM-Driven Resume Coach Pipeline*

**For Data / ML / Automation roles**
- *Multi-Stage LLM Resume Scoring + Rewrite System*
- *ATS + Job Match Analyzer using n8n & OpenAI*

---

## ✍️ Bullet templates (copy/paste)

Use 2–4 bullets max, tailored to your role.

### Product-leaning bullets
- Built a multi-module AI resume diagnostic pipeline in n8n that scores ATS structure, impact, role signals, and JD fit, delivering a personalized HTML report to users.
- Designed adaptive scoring logic that renormalizes results when JD is missing, improving UX clarity and avoiding misleading “0-score” penalties.
- Iterated on prompt + parsing failure modes to ensure evidence-first coaching and strict JSON schema compliance across modules.

### Tech-leaning bullets
- Orchestrated a 6-stage LLM workflow (ATS, Job Match, Impact, Role Signals, Bullet Rewrite, Final Summary) with robust JSON extraction and schema hard-rules.
- Implemented fault-tolerant parsing for double-encoded model outputs and schema drift, producing consistent downstream fields for automation.
- Generated responsive HTML email reports with conditional rendering (JD present/absent), score bands, and placeholder tracking.

### If you want a “results” bullet
Only add if you can defend it with proof:
- Reduced manual resume review effort by **[X]%** and cut turnaround time from **[A] → [B]** minutes via automated scoring + rewrites.

---

## 🗂️ What to include in my portfolio page

1. **1-liner problem statement**
   - “Candidates don’t know why they’re filtered by ATS or where they mismatch a JD — I built an automated coach that explains this clearly.”

2. **Workflow diagram (screenshot)**
   - Use the node graph you shared.

3. **Key design choices**
   - Evidence-first rules
   - Adaptive JD skipping + renormalization
   - “Strong/Weak/Missing” evidence signaling
   - Bullet rewrite with placeholders

4. **Example output**
   - One anonymized email screenshot (JD present)
   - One with JD absent

5. **Tech stack**
   - n8n, OpenAI, Gmail, PDF extraction, JS parsing, HTML templating.

---

## ⭐ How to talk about it in interviews

Use this structure:
1. **Problem**
2. **Why it matters**
3. **Approach**
4. **Tradeoffs**
5. **Impact**
6. **Next steps**

---



You *can* say:
- “Designed to be production-safe”
- “Evidence-first and ATS-aligned”
- “Robust against common LLM output failures”

---

## Optional add-ons (if you have time)

- Add a small public demo form
- Add anonymized before/after examples
- Add a short Loom walkthrough
