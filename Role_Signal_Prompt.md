<!-- prompts/role_signals.user.md -->

## USER
You are running the **Role-Specific Signals module**.

### Inputs
- **role_preset:** `{{ $('Edit Fields').item.json.role_present }}`
- **resume_text:** `{{ $('Edit Fields').item.json.resume_text }}`

### Tasks
1) Extract **present role signals** with **direct evidence quotes** from resume_text.
2) Extract **missing core signals** for the selected role_preset only, with:
   - why it matters
   - suggested_if_true flag
   - proof_request
   - evidence_bullet_frame
3) Score role signals **out of 20**:
   - If computed score > 20, **clamp to 20** and explain why in signal_summary.
4) Return **missing_core_signals ONLY for the selected role_preset**.  
   Do not include irrelevant signals from other roles.

### Return ONLY valid JSON matching this schema
```json
{
  "role_signal_score": number,
  "present_signals": [
    {
      "signal": string,
      "evidence_quote": string,
      "why_it_counts": string
    }
  ],
  "missing_core_signals": [
    {
      "signal": string,
      "why_it_matters": string,
      "suggested_if_true": boolean,
      "proof_request": string,
      "evidence_bullet_frame": string
    }
  ],
  "signal_summary": string
}
