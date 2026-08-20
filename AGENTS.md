# Agent instructions — resume tailor

This repo is a Cursor workflow for tailoring one master resume to each job description (JD). There is no app server. You are the tailoring engine.

## Default behavior

When the user pastes a job description, attaches a posting, points at a file under `jobs/`, or asks to tailor/customize/adapt the resume:

1. Follow `.cursor/skills/tailor-resume/SKILL.md` exactly.
2. Read `resume/MASTER.md` and `resume/PROFILE.md` first.
3. Write the tailored resume to `tailored/<company>-<role>-YYYY-MM-DD.md`.
4. Reply with a short recap: what changed, keywords emphasized, and unsupported JD requirements (gaps). Never put gaps on the resume.

When the user pastes a resume and asks to save it as the master, follow `.cursor/skills/save-master-resume/SKILL.md` and overwrite `resume/MASTER.md`.

## Honesty (non-negotiable)

- NEVER invent jobs, titles, employers, dates, degrees, certifications, tools, or accomplishments.
- ONLY rephrase, reorder, emphasize, quantify (only if already implied or stated in the master/profile), and select from the master resume.
- Mirror JD keywords naturally, and only when they are truthful.
- If the JD asks for something not in the master resume, do not fabricate it. Mention it in the chat recap as a gap.
- Keep the same factual career history (employers, titles, dates, education).

## Placeholders

If `resume/MASTER.md` still contains `[PLACEHOLDERS]` or example bullets, warn the user, still produce a tailored *template* that shows the mapping, and tell them to paste their real resume into `resume/MASTER.md`.
