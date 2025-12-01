
<!-- README.md -->

# AI Resume Diagnostic + JD Match (n8n Workflow)

An end-to-end **AI resume review pipeline** built in **n8n** that:
- extracts resume text from PDF,
- scores it across ATS structure, impact, role signals, and JD match,
- rewrites weak bullets with evidence-safe placeholders,
- generates an adaptive “final coach summary” JSON,
- sends a clean, branded HTML email to the user.

Designed for early- to- mid career roles with strict **evidence-first** coaching and ATS compatibility.

<img width="1199" height="72" alt="image" src="https://github.com/user-attachments/assets/6153a8fc-6ee9-4b25-8616-2e34e48d22a6" />

---

## 🚀 What it does

### Inputs
- Resume PDF (uploaded via n8n form)
- Optional Job Description text

### Outputs
- A structured JSON diagnostic (machine-readable)
- A user-friendly HTML email (adaptive when JD is missing)

### Scoring modules
| Module | Max Score | Purpose |
|---|---:|---|
| ATS / Structure | 20 | Formatting, parsing readiness, keyword hygiene |
| Impact | 30 | Measurable outcomes + clarity of achievements |
| Role Signals | 20 | Role-aligned competencies & framing |
| Job Match | 30 | JD keyword / responsibility fit (skips if JD absent) |

When JD is absent, Job Match is **not scored** and the overall score is **renormalized** across the remaining modules.

---

## 🧠 Key Design Principles

### Evidence-First Coaching
The system never invents tools, metrics, or experiences.
- Keywords count as “present” **only** if directly quoted from the resume.
- Missing keywords can be suggested **only with proof requests** + bullet frames.
- Weak evidence is explicitly labeled as “weak”.

### Adaptive UX
- If JD is missing:
  - Job Match card shows **no score**, only “Not assessed — JD not provided”
  - Job Match section collapses to a 1-line note
  - Overall score reweights ATS + Impact + Role Signals to /100

### Clean Separation of Concerns
Each module is responsible for one job:
- extraction
- scoring
- rewriting
- final synthesis
- parsing
- beautification

---

## 🧩 Workflow Overview (Nodes)

1. **On form submission**
2. **Extract from file** (PDF → text)
3. **Edit fields** (normalize inputs)
4. **Bullet extractor**
5. **ATS module**
6. **Job Match module** *(skips if JD missing)*
7. **Impact module**
8. **weak bullets** (parser for Impact.weak_bullets)
9. **Role Signals module**
10. **Bullets Rewrite module**
11. **Final Summary module**
12. **Parse Summary** (robust JSON extraction)
13. **Beautify Mail** (HTML email)
14. **Send a message** (Gmail)

---

## 🛠️ Setup

### Prerequisites
- n8n instance (cloud or self-hosted)
- OpenAI credentials connected to n8n
- Gmail node configured for outbound emails

### Import workflow
1. Clone the repo
2. Import the workflow JSON into n8n:
   - n8n → Workflows → Import from File
3. Update these nodes:
   - OpenAI credential selectors
   - Gmail sender configuration
   - Form fields (if your form schema differs)

---

## 🧪 Testing

### Test cases to validate:
1. **Resume only**
   - JD empty or missing
   - Verify Job Match skipped JSON
   - Verify overall score renormalized
   - Verify Job Match section is short
2. **Resume + JD**
   - Verify JD keywords extracted
   - Verify strong/weak/missing statuses
   - Verify Job Match score shown
3. **Bad formatting / special chars**
   - Ensure ATS module catches parsing risk
4. **Weak bullets**
   - Confirm placeholders appear in rewrites + “Info to Fill Placeholders”

---
**Output**

<img width="1440" height="731" alt="image" src="https://github.com/user-attachments/assets/c65007d7-c851-4b8c-80d5-d34efeab1cc6" />


## 📦 Repo Contents
1. /workflow/
2. resume-diagnostic-n8n.json
3. /prompts/
4. ats.prompt.md
5. impact.prompt.md
6. jobmatch.prompt.md
7. rolesignals.prompt.md
8. bullets-rewrite.prompt.md
9. final-summary.prompt.md
10. /scripts/
11. parse-summary.js
12. beautify-mail.js
13. /docs/
14. portfolio-cv-positioning.md
15. README.md
16. Praveen Soni _ Detailed Resume Review (Score_ 64_100).pdf


