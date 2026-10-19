# Claude Skills

Reusable skill files for Claude: resume tailoring, cover letter writing, and mobile-first UI design.

| File | What it does |
|---|---|
| `resume-skill.md` | Tailors a master resume to a job description |
| `cover-letter-skill.md` | Writes a researched, fixed-template cover letter |
| `ui-design-learnings.md` | Rules and a checklist for calm, mobile-first UIs |

## What you need to add

The UI skill works as is. The resume and cover letter skills read your personal files, which are not included here. Create this folder:

```
job-search/
├── claude.md              # your background, voice, tone, and hard rules
├── extra-info.md          # your full pool of projects and experiences
├── resume-template.docx   # your master resume (the skill never edits it)
└── Application Tracker.xlsx   # optional, for the resume skill's match score log
```

Then:
1. Edit the cover letter template line in `cover-letter-skill.md` (`Hi, I'm [Name], a [Job Title / Discipline]...`) with your own details.
2. Install each file as a skill (a folder with the file renamed to `SKILL.md`), or paste it into your Claude project instructions.
3. The skills also expect the Word-file helper scripts (`scripts/office/`) and `pandoc`, `python`, and the `docx` npm package to be available.
