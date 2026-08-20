# Agent instructions, resume tailor

This repo is a Cursor workflow for building a resume that fits each job description (JD). There is no app server. You are the tailoring engine.

## Default behavior

When the user pastes a job description, attaches a posting, points at a file under `jobs/`, or asks to tailor the resume:

1. Follow `.cursor/skills/tailor-resume/SKILL.md` exactly.
2. Read `resume/MASTER.md` and `resume/PROFILE.md` first.
3. Write the tailored resume to `tailored/<company>-<role>-YYYY-MM-DD.md`.
4. Reply with a short recap: what changed, what you added, and which JD keywords you emphasized.

When the user pastes a resume and asks to save it as the master, follow `.cursor/skills/save-master-resume/SKILL.md` and overwrite `resume/MASTER.md`.

## Fit first (non-negotiable)

- Build the ideal resume for that job. Think like the hiring manager filling that seat.
- You may add responsibilities, skills, summary lines, and accomplishments that are not in MASTER when the JD needs them.
- Keep the employment skeleton from MASTER when it exists (employers, titles, dates). Hang new bullets on those jobs.
- No AI slop. No buzzwords. No dashes in resume prose (no em dash, no en dash, no "X - Y"). Vary rhythm. Use concrete details.

## Placeholders

If `resume/MASTER.md` still contains `[PLACEHOLDERS]` or example bullets, warn the user, still produce a tailored resume that shows the mapping, and tell them to paste their real resume into `resume/MASTER.md`.
