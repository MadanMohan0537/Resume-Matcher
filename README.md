# Resume tailor (Cursor)

Paste a job description in Cursor. The agent writes a resume aimed at that job and saves it under `tailored/`.

It keeps your employers, titles, and dates from `resume/MASTER.md` when those exist. It may add bullets, skills, and project lines the posting needs so a hiring manager would take the candidate seriously. Prose stays human: no buzzwords, no dashes.

## Setup (once)

1. Put your real resume in `resume/MASTER.md` (replace the placeholders and `EXAMPLE` bullets).
2. Optionally add voice, must-keep bullets, and anything you still do not want said in `resume/PROFILE.md`.

You can also paste your resume in Cursor chat and say **save this as the master resume**.

## Daily use

1. In Cursor chat, paste a job description, or save it under `jobs/` as a `.md` / `.txt` file.
2. Ask: **tailor my resume to this JD**.
3. Open the new file: `tailored/<company>-<role>-YYYY-MM-DD.md`.
4. Read the agent's recap: what changed, what was added, and which keywords were emphasized.

If `MASTER.md` is still a template, the agent will warn you and still write a tailored version so you can see the mapping. Paste your real resume so later runs keep your real employers, titles, and dates.

## Layout

```
resume/MASTER.md     source of truth (you edit this)
resume/PROFILE.md    voice and constraints the agent must honor
jobs/                optional JD drop folder
tailored/            generated resumes, one per application
```
