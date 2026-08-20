# Resume tailor (Cursor)

Paste a job description in Cursor. The agent writes a **one-page** resume aimed at that job and saves it under `tailored/`. The summary is 2 to 3 lines, never more.

It keeps your employers, titles, and dates from `resume/MASTER.md`. It may add bullets, skills, and project lines the posting needs so a hiring manager would take the candidate seriously. Prose stays human: no buzzwords, no dashes.

`resume/MASTER.md` is already filled with the ideal resume. Edit it there if facts change.

## Setup

1. Keep `resume/MASTER.md` current (this is the source of truth).
2. Optionally edit voice, must-keep bullets, and limits in `resume/PROFILE.md`.

You can also paste an updated resume in Cursor chat and say **save this as the master resume**.

## Daily use

1. In Cursor chat, paste a job description, or save it under `jobs/` as a `.md` / `.txt` file.
2. Ask: **tailor my resume to this JD**.
3. Open the new file: `tailored/<company>-<role>-YYYY-MM-DD.md`.
4. Read the agent's recap: what changed, what was added, and which keywords were emphasized.

## Layout

```
resume/MASTER.md     source of truth (you edit this)
resume/PROFILE.md    voice and constraints the agent must honor
jobs/                optional JD drop folder
tailored/            generated resumes, one per application
```
