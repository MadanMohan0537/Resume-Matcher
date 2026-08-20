---
name: tailor-resume
description: Tailor resume/MASTER.md to a job description. Use whenever the user pastes a JD, attaches a posting, points at jobs/, or asks to tailor, customize, adapt, or target the resume for a role.
---

# Tailor resume to a job description

Run this skill end-to-end. Do not skip steps. Do not invent facts.

## Inputs

| Source | Path / place | Required |
|---|---|---|
| Master resume | `resume/MASTER.md` | Yes — always read it |
| Profile / constraints | `resume/PROFILE.md` | If the file exists |
| Job description | User message, attachments, and/or `jobs/` | Yes — you need a JD |
| Output directory | `tailored/` | Write here |

If the user names a file under `jobs/`, use that JD. If they paste a JD in chat, use the pasted text (it wins over an older file). If both exist and conflict, prefer the chat paste and mention that you did.

## Honesty rules (stop if you would break these)

- NEVER invent jobs, titles, employers, dates, degrees, certifications, tools, or accomplishments.
- NEVER add a metric that is not already stated or clearly implied in MASTER or PROFILE.
- ONLY rephrase, reorder, emphasize, and select from the master resume.
- New bullets are allowed only as truthful restatements of facts already in the master resume (same work, clearer wording, JD-aligned keywords).
- If the JD asks for a skill, domain, tool, or credential that is not in the master resume, do **not** put it on the resume. Record it as a gap for the chat recap.
- Keep the same employers, titles, dates, and education. Do not merge, split, or rename companies. Do not promote or demote titles.
- Honor `resume/PROFILE.md`: must-keep bullets stay; banned claims stay out; voice and length constraints win over JD pressure.

## Procedure

### 1. Load source of truth

Read `resume/MASTER.md`. If `resume/PROFILE.md` exists, read it.

Detect placeholders: bracket tokens like `[YOUR NAME]`, `[COMPANY]`, `[JOB TITLE]`, and bullets that start with `EXAMPLE —`. If any remain, set `master_is_template = true`. You will still produce a tailored template (step 6) and warn in the recap.

### 2. Load the job description

Collect the JD from the user message and/or `jobs/`. If no JD is present, ask for one (company + role + the posting text, or a path under `jobs/`). Do not invent a JD.

### 3. Extract JD signals (work from the posting, not guesses)

Write a short internal checklist (do not dump this into the resume file):

- Company name and role title (for the filename)
- Seniority (intern / junior / mid / senior / staff / principal / manager)
- Domain / industry (e.g. fintech, healthcare, developer tools)
- Must-have skills and keywords (tools, languages, methods, certifications the posting requires)
- Nice-to-have skills
- Core responsibilities (what the person will actually do)
- Soft-signal terms worth mirroring if truthful (e.g. "cross-functional", "ownership", "on-call")

Slugify for the filename:

- Lowercase
- Replace any run of non-alphanumeric characters with a single `-`
- Strip leading/trailing `-`
- If company or role is missing, use `unknown-company` or `unknown-role`

Output path:

```
tailored/<company>-<role>-YYYY-MM-DD.md
```

Use today's date. If that file already exists, add `-2`, `-3`, etc. Do not overwrite a previous tailored resume unless the user asked to replace it.

### 4. Map MASTER → JD (select and align, do not fabricate)

- **Summary:** Rewrite from master facts so it matches this role's seniority, domain, and top keywords. One short paragraph. No new employers, titles, or years of experience.
- **Skills:** Reorder to put JD-relevant skills first. Drop skills only if PROFILE allows and they add noise. Never add a skill that is not in MASTER or PROFILE.
- **Experience:** Prefer editing existing bullets over writing new ones.
  - Keep bullets that already match; tighten wording and weave in truthful JD keywords.
  - Refine bullets that are related but weakly worded so they highlight the JD-relevant part of the same work.
  - Demote or drop bullets that are true but irrelevant to this JD, unless PROFILE marks them must-keep.
  - Do not reorder jobs (chronological career history stays intact). You may reorder bullets *within* a job.
- **Projects:** Include or lead with projects that support the JD; omit unrelated ones if space is tight.
- **Education / certs:** Copy factually. Include a certification only if it is in MASTER or PROFILE.

Quantify only when the number is already in MASTER/PROFILE, or the master already implies a countable fact you are not stretching (e.g. "a small team" must not become "led 12 engineers").

### 5. Length and format

- Default to **one page** for intern / early / mid career; **two pages max** for senior+ or if PROFILE says so.
- Match MASTER structure: contact, summary, skills, experience, projects, education (omit a section only if MASTER has no content for it).
- Implied first person, no "I". Action verb + what + impact.
- ATS-friendly markdown: simple headings, no tables, no images, no columns.
- The tailored file is the resume only — no "gaps", no cover letter, no commentary, no HTML comments.

### 6. Placeholder / template mode

If `master_is_template` is true:

- Still write `tailored/<company>-<role>-YYYY-MM-DD.md` as a **demonstration of mapping** (summary/skills/bullets aligned to this JD, placeholders left in for identity facts).
- Keep `[PLACEHOLDERS]` for name, contact, employers, dates, school — do not invent a fake identity.
- Replace or rewrite `EXAMPLE —` bullets into JD-aligned *example* bullets that are still clearly marked `EXAMPLE —` so the user cannot submit them by accident.
- In the recap, warn that MASTER is not filled in and they must paste their real resume before applying.

### 7. Recap to the user (after the file is written)

Keep it brief:

1. **Output path** of the tailored resume.
2. **What changed** — summary, skill order, which jobs' bullets were refined or dropped.
3. **Keywords emphasized** — the JD terms you mirrored, and only those supported by MASTER.
4. **Gaps** — JD must-haves with no support in MASTER. These stay off the resume. Optionally suggest truthful ways to address them later (coursework, projects to add to MASTER if they actually exist).
5. **Template warning** if MASTER was not filled in.

Do not reprint the full resume in chat unless the user asks.

## Quick checks before you finish

- [ ] Employers, titles, dates, degrees match MASTER
- [ ] No tool, skill, or metric appears that MASTER/PROFILE does not support
- [ ] Must-keep bullets from PROFILE are present
- [ ] Banned claims from PROFILE are absent
- [ ] Filename is slugified and dated
- [ ] Recap includes changes, keywords, and gaps
