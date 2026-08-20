---
name: save-master-resume
description: Save or replace resume/MASTER.md from content the user pasted or attached. Use when they say this is their resume, update the master, replace the template, or save as MASTER.
---

# Save the master resume

Use this when the user provides their real resume (paste, attachment, or file path) and wants it stored as the source of truth.

## Procedure

1. Read the current `resume/MASTER.md` so you know what you are replacing.
2. Convert their content into clean markdown with these sections when the source has them:
   - Contact
   - Summary
   - Skills
   - Experience
   - Projects
   - Education
   - Optional extras they already have (certifications, publications, volunteer) — do not invent empty sections
3. Preserve **every factual claim**: employers, titles, dates, locations, degrees, tools, metrics, bullets. Do not upgrade titles, round up numbers, or add impact they did not write.
4. Light cleanup only: consistent heading levels, bullet markers, date formatting, obvious typos. Do not "improve" accomplishments while saving.
5. Remove leftover template placeholders (`[YOUR NAME]`, `EXAMPLE —` bullets, etc.) unless the user's content still includes them on purpose.
6. Overwrite `resume/MASTER.md`.
7. Tell the user it is saved, list any sections that were missing (so they can add them), and remind them they can now paste a JD to tailor.

## Do not

- Do not tailor while saving unless they also provided a JD and asked for both.
- Do not write anything into `tailored/` as part of this skill.
- Do not invent contact details, links, or skills to "complete" the template.
