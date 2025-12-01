**User Prompt**

You are running the Final Coach Summary module.

Inputs:
- role_preset: {{ $('Edit Fields').item.json.role_present }}
- ats_module_output: {{ $('ATS').item.json.output[0].content[0].text }}
- job_match_output: {{ $('Job Match').item.json.output[0].content[0].text }}
- impact_output: {{ $('Impact').item.json.output[0].content[0].text }}
- role_signals_output: {{ $json.output[0].content[0].text }}
- rewritten_bullets_output: {{ $json.output[0].content[0].text }}

Hard rules:
1) Output ONLY valid JSON. NO comments, NO trailing text.
2) role_signals_output.role_signal_score is out of 20. Never exceed 20.
3) In bullet_review, original_bullet MUST be a string from rewritten_bullets_output.rewritten_bullets[].original_text.
4) If rewritten_bullets_output is missing or empty, return bullet_review as [].
5) Do not use generic phrases without specific supporting details.
6) Top strengths must be 5–7 items unless resume truly lacks content.
7) In bullet_review, extract placeholders from recommended_text AND list them in info_needed_from_user.
8) Never invent skills, tools, employers, metrics, or outcomes.

ADAPTIVE RULE (execute before scoring):

If job_match_output.job_match_skipped is true:
- Do NOT analyze JD or mention JD/Job Match anywhere.
- Include placeholder job_match card with NO score.
- Renormalize overall_score to /100 using only ATS + Impact + Role Signals:
  overall_score = round(
    (ats_output.ats_score/20*100 * 0.25) +
    (impact_output.impact_score/30*100 * 0.45) +
    (role_signals_output.role_signal_score/20*100 * 0.30)
  )
- score_breakdown must be:
  {
    "ats": { "score": <0-20>, "notes": "..." },
    "impact": { "score": <0-30>, "notes": "..." },
    "role_signals": { "score": <0-20>, "notes": "..." },
    "job_match": { "skipped": true, "notes": "Not assessed — JD not provided" }
  }
- Omit job_match_section entirely.

Else (JD exists):
- overall_score = ats_score (0–20)
                + job_match_score (0–30)
                + impact_score (0–30)
                + role_signals_score (0–20)
- score_breakdown includes job_match with score out of 30.
- Create job_match_section by RELAYING job_match_output.

Tasks:
1) Compute overall_score correctly.
2) Provide breakdown notes.
3) Produce top_strengths with evidence.
4) Produce top_fixes ranked by ROI.
5) Build bullet_review from rewritten_bullets_output.rewritten_bullets.
6) info_needed_from_user includes placeholders + missing evidence for fixes.
7) seven_step_plan realistic and tied to top fixes.
8) End with 1-sentence CTA inviting JD re-score.

Return ONLY valid JSON in this schema:

{
  "role_preset": string,
  "overall_score": number,

  "score_breakdown": {
    "ats": { "score": number, "notes": string },
    "impact": { "score": number, "notes": string },
    "role_signals": { "score": number, "notes": string },
    "job_match": {
      "score": number,           
      "skipped": boolean,        
      "notes": string
    }
  },

  "summary": string,

  "top_strengths": [
    { "strength": string, "evidence": string }
  ],

  "top_fixes": [
    {
      "fix": string,
      "why_it_matters": string,
      "expected_score_lift": number,
      "how_to_do_it": string,
      "evidence_reference": string
    }
  ],

  "bullet_review": [
    {
      "original_bullet": string,
      "original_score_0_to_8": number|null,
      "why_weak": string,
      "recommended_version": "A"|"B"|"C",
      "recommended_text": string,
      "why_this_version": string,
      "placeholders_to_fill": [string]
    }
  ],

  "info_needed_from_user": [string],

  "seven_step_plan": [
    { "step": number, "task": string, "output_expected": string }
  ],

  "job_match_section": {        
    "match_verdict": string,
    "subscores_explained": string,
    "top_jd_requirements": [
      {
        "requirement": string,
        "importance": "must_have"|"nice_to_have",
        "status": "Strong"|"Missing"|"Weak",
        "resume_evidence": string|null
      }
    ],
    "top_gaps": [
      {
        "gap": string,
        "why_it_matters": string,
        "suggested_if_true": boolean,
        "proof_request": string,
        "bullet_frame_to_add_evidence": string
      }
    ],
    "anti_stuffing_warning": string|null
  },

  "cta": string
}

Now generate the final detailed review.
