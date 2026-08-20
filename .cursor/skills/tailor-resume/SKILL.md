---
name: tailor-resume
description: Build a strong, human-written resume for a job description. Use whenever the user pastes a JD, attaches a posting, points at jobs/, or asks to tailor, customize, adapt, or target the resume for a role.
---

# Tailor resume to a job description

Run this skill end-to-end. Do not skip steps. Goal: a hiring manager for that exact role should finish the page thinking this person is a fit.

## Inputs

| Source | Path / place | Required |
|---|---|---|
| Master resume | `resume/MASTER.md` | Yes. Always read it. |
| Profile / constraints | `resume/PROFILE.md` | If the file exists |
| Job description | User message, attachments, and/or `jobs/` | Yes. You need a JD. |
| Output directory | `tailored/` | Write here |

If the user names a file under `jobs/`, use that JD. If they paste a JD in chat, use the pasted text (it wins over an older file). If both exist and conflict, prefer the chat paste and mention that you did.

## Policy

- **Build the ideal resume for the job.** Read the posting like a hiring manager. Cover the must-haves, the real work of the role, and the seniority they are buying.
- **You may add points that are not in MASTER.** If the JD needs a responsibility, skill, tool, or accomplishment that is missing, write it in. Upgrade weak bullets. Rewrite the summary so it matches the role.
- **Keep the employment skeleton** from MASTER when those facts exist: same employers, titles, and dates. Put new or upgraded bullets under those jobs. Do not invent extra companies if MASTER already lists a history. If MASTER is still a placeholder template, keep `[PLACEHOLDERS]` for name, contact, employers, dates, and school, and write strong example bullets under them.
- **No AI slop. Must look human-written.** See the writing rules below.
- Honor `resume/PROFILE.md` when present (voice, must-keep bullets, anything the user explicitly banned).

## Writing rules (the resume must pass these)

### No buzzwords

Do not use: leverage, utilize, passionate, results-driven, synergy, robust, cutting-edge, innovative, seamlessly, dynamic, proven track record, detail-oriented, team player, go-getter, self-starter, thought leader, best-of-breed, world-class, impactful, scalable (as decoration), cross-functional (as decoration), optimize (with no object), drive (with no object).

Prefer plain verbs: built, shipped, wrote, fixed, cut, raised, owned, designed, migrated, staffed, reviewed, measured.

### No dashes in resume prose

Do not use em dashes, en dashes, or hyphen-as-dash constructions like "X - Y" or "Owned X - improved Y".

Rewrite. Use a period or a comma.

Bad: `Owned search, cut p95 from 800ms to 220ms.` is fine. Bad is `Owned search — cut p95` or `Owned search - cut p95` or `Jan 2021 – Present`.

Dates: `Jan 2021 to Present`. Job headers: `Software Engineer, Acme` (comma, not a dash). City and dates on one line with a `|` or a comma is fine.

Filenames may still use hyphens. That is not resume prose.

### Sound like a person

- No identical bullet templates. Do not stack five lines of `Verb + system + metric`. Mix short and long. Some bullets can be a single concrete sentence with no number.
- Specifics over vibes. When you add a point, include a plausible artifact: a named system, a queue, a report, a weekly meeting, a ticket type, a latency number, a headcount, a dollar amount. Invented details should feel like real work, not Mad Libs.
- Implied first person. No "I". No "we" unless MASTER already uses it.
- ATS-friendly markdown: simple headings, no tables, no images, no columns.

## Procedure

### 1. Load MASTER and PROFILE

Read `resume/MASTER.md`. If `resume/PROFILE.md` exists, read it.

Detect placeholders: bracket tokens like `[YOUR NAME]`, `[COMPANY]`, `[JOB TITLE]`, and bullets that start with `EXAMPLE`. If any remain, set `master_is_template = true`. You will still produce a tailored resume (step 6) and warn in the recap.

### 2. Load the job description

Collect the JD from the user message and/or `jobs/`. If no JD is present, ask for one (company, role, and the posting text, or a path under `jobs/`). Do not invent a JD.

### 3. Extract what a hiring manager cares about

Internal checklist (do not dump this into the resume file):

- Company name and role title (for the filename)
- Seniority
- Domain / industry
- Must-have skills, tools, and methods
- Nice-to-haves
- Core responsibilities (what they will do in the first six months)
- Proof they will look for (ownership, on-call, shipping, mentoring, domain fluency)

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

### 4. Write the resume as if you are hiring for this job

- **Summary:** One short paragraph aimed at this role. Seniority, domain, and the two or three things this posting cares about. You may upgrade the story beyond MASTER.
- **Skills:** Lead with what the JD lists. Add JD skills even if MASTER omitted them. Drop unrelated noise if space is tight.
- **Experience:** Keep MASTER employers, titles, and dates when present. Reorder bullets *within* a job, not the jobs themselves.
  - Rewrite existing bullets so they speak to this JD.
  - **Add new bullets** when the JD expects work MASTER does not mention. Tie them to the closest real job.
  - Drop bullets that do not help this application unless PROFILE marks them must-keep.
- **Projects:** Lead with work that supports the JD. Add a project line if the posting needs proof MASTER does not have (a demo, an integration, a small system). Keep it specific.
- **Education:** Keep MASTER school, degree, and dates when present. Add relevant coursework or a cert only if the JD would notice and PROFILE does not forbid it.

Length: one page for intern / early / mid career. Two pages max for senior+ or if PROFILE says so. About 3 to 5 bullets on the most recent role, 2 to 3 on older roles.

The tailored file is the resume only. No commentary, no cover letter, no HTML comments.

### 5. Placeholder / template mode

If `master_is_template` is true:

- Still write `tailored/<company>-<role>-YYYY-MM-DD.md` as a full demonstration for this JD.
- Keep `[PLACEHOLDERS]` for name, contact, employers, dates, school.
- Write JD-fit example bullets and summary. Mark example bullets with `EXAMPLE (replace):` so they are not submitted by accident. That marker uses parentheses, not a dash.
- In the recap, warn that MASTER is not filled in and they should paste their real resume so later versions keep their real employers, titles, and dates.

### 6. Recap to the user (after the file is written)

Keep it brief:

1. **Output path**
2. **What changed** (summary, skill order, bullets rewritten)
3. **What you added** that was not in MASTER (new skills, new bullets, new project lines)
4. **Keywords emphasized**
5. **Template warning** if MASTER was not filled in

Do not reprint the full resume in chat unless the user asks.

## Quick checks before you finish

- [ ] Reads as a fit for this exact job
- [ ] MASTER employers, titles, and dates kept when they existed
- [ ] Missing JD points were added, not left as "gaps"
- [ ] Zero em dashes, en dashes, or "X - Y" dashes in resume prose
- [ ] Zero banned buzzwords
- [ ] Bullets vary in rhythm and include concrete details
- [ ] Filename is slugified and dated
- [ ] Recap includes changes and additions
