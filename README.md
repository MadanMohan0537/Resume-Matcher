# Resume tailor (Cursor)

Paste a job description in Cursor. The agent refines `resume/MASTER.md` to that JD and writes a tailored copy under `tailored/`.

It will not invent jobs, titles, dates, degrees, tools, or accomplishments. It only rephrases, reorders, and emphasizes what is already in the master resume.

## Setup (once)

1. Put your real resume in `resume/MASTER.md` (replace the placeholders and `EXAMPLE —` bullets).
2. Optionally add voice, must-keep bullets, and banned claims in `resume/PROFILE.md`.

You can also paste your resume in Cursor chat and say **save this as the master resume**.

## Daily use

1. In Cursor chat, paste a job description — or save it under `jobs/` as a `.md` / `.txt` file.
2. Ask: **tailor my resume to this JD**.
3. Open the new file: `tailored/<company>-<role>-YYYY-MM-DD.md`.
4. Read the agent's recap: what changed, which keywords were emphasized, and any JD requirements your master resume does not support.

Gaps stay in chat, not on the resume.

If `MASTER.md` is still a template, the agent will warn you and still write a tailored *template* so you can see the mapping. Paste your real resume before you apply.

## Layout

```
resume/MASTER.md     source of truth (you edit this)
resume/PROFILE.md    constraints the agent must honor
jobs/                optional JD drop folder
tailored/            generated resumes, one per application
```
