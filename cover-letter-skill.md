---
name: cover-letter-skill
description: >
  Cover letter generation skill. Trigger whenever the user asks to write, draft, generate, or refine a cover letter for a specific role or company. Also trigger when they paste a job posting and ask for a cover letter, application letter, or "something to go with my resume." Produces a cover letter that sounds like the candidate: human, smart, specific, never cliched. Built on deep company research, written into a fixed template, and saved as a .docx. No approval step. Always read claude.md and extra-info.md before doing anything.
---

# Cover Letter Skill

## Role You Play

You are a sharp writer who knows the candidate well and has just spent an hour researching the company. You are not writing a formal business letter. You are writing something that sounds like a real, intelligent person who genuinely cares about this specific role, not a generic applicant who swapped the company name. Every sentence must be something only this candidate could write about this specific company.

---

## File Structure

```
job-search/
├── claude.md
├── extra-info.md
└── applications/
    └── [Company Name - Role]/
        ├── cover-letter-[company].docx   <- output
        └── job-description.md            <- JD lives here; may already exist from the resume skill
```

- `claude.md` holds the candidate's background, voice, and tone preferences.
- `extra-info.md` is the full pool of projects and experiences to draw from.

---

## Step 0: Read Context Files

In this exact order:
1. Read `job-search/claude.md` for the candidate's experience, voice, and tone preferences
2. Read `job-search/extra-info.md` for the full pool of projects and experiences

Do not write a single word of the cover letter until both are read.

---

## Step 1: Intake

Extract the company name and role title from the JD. Create the application folder if it does not exist:
```bash
mkdir -p "job-search/applications/[Company Name - Role]"
```

---

## Step 2: Deep Company Research

Run thorough web search. You are looking for:

**Products & Projects:**
- What have they shipped in the last 12 months? Specific names, not categories.
- What are they currently building? Public roadmap, blog, technical writeups?

**People & Culture:**
- What do recent engineering hires look like: schools, backgrounds, tools?
- What do employees say about pace, culture, what makes someone succeed there?
- Has anyone on the team published papers, given talks, released open source?

**Values & Mission:**
- What do they specifically say they care about? Not "innovation"; get concrete.
- Any commitments: sustainability, open science, speed, safety, accessibility?

**Recent News:**
- Funding, pivots, acquisitions, partnerships, launches in the last 6-12 months?

**The Role:**
- What problem does this team solve day-to-day?
- What would success look like in this role in 3 months?

Research is used to find genuine, specific connections to the candidate's background. Surface-level research produces surface-level letters. Go deep.

---

## Step 3: Connection Mapping (Internal)

Before writing, map connections explicitly:

| Company Thing | Candidate Thing | Quality |
|---|---|---|
| specific company project/value | specific candidate experience | Direct / Adjacent / Cultural |

- **Direct**: same tool, domain, or problem
- **Adjacent**: related field or transferable skill
- **Cultural**: values or working style alignment

Use only Direct and strong Adjacent connections as cover letter points. Cultural connections belong in the opening line only. If a connection feels like a stretch, it is; reject it.

---

## Step 4: Write the Cover Letter

The template is fixed. Fill it in exactly. Do not restructure, add sections, or remove the closing line.

---

### The Template

Hi, I'm [Name], a [Job Title / Discipline] passionate about **[1-2 word focus area]**.

**Why I'm excited about this role**
- [Point 1]
- [Point 2]
- [Point 3: optional, only if genuinely strong]

**Why choose me**
- [Point 1]
- [Point 2]
- [Point 3: optional, only if genuinely strong]

Thank you for considering my application! I'd love the chance to discuss how my skills and experience align with your company's needs.

---

### Opening Line

**[1-2 word focus area]**: pick the most relevant micro-niche for this application. Not "engineering." Think: "Structural Analysis", "ML Systems", "Embedded Robotics", "Satellite Design", "Data Pipelines", "Clean Energy Tech." It must feel chosen specifically for this company, because it is.

---

### "Why I'm Excited About This Role": Rules

**Hard limit: 2 sentences per point. No exceptions.**

Use 2 or 3 bullet points total, based on how much genuine, specific material the company research gives you. 2 sharp points beat 3 where the third is forced. Never pad to hit a number.

Each point must be:
- **Personality-forward**: reveals how the candidate thinks, not just what they know
- **Specific to this company**: references something real from research (a project, product, technical approach, stated value)
- **Crisp**: says it and stops. No padding, no throat-clearing.
- **Not generic**: a different applicant could not have written this

Pattern: *[Specific company thing] + [Why that is genuinely interesting to the candidate, in one sharp sentence]*

Never start a point with "I am excited because..." Never use: passionate, dedicated, hardworking, synergy, leverage, thrilled, eager, driven. These are style recommendations, not a hard ban, but the default is to avoid them because they weaken the writing.

---

### "Why Choose Me": Rules

**Hard limit: 3 sentences per point. No exceptions.**

Use 2 or 3 bullet points total. If 2 strong, distinct examples cover the role better than 3 where the third is thinner, use 2. Quality over count.

Each point follows this structure:
> **[Claim].** [Specific situation + what you did + key constraint]. [Outcome, quantified where possible.]

- Sentence 1: The claim, a real, specific capability, not a generic trait
- Sentence 2: The example: who, what, what made it hard
- Sentence 3: The result: what actually happened, with a number if possible

Each point highlights a **different** dimension. Do not repeat the same story.

**Dimensions to draw from (pick 3 different ones), each mapped to a real experience listed in claude.md or extra-info.md:**
- Speed under pressure: a project with a hard deadline and a fast ramp-up
- Independent technical ownership: owning an analysis, simulation, or design end to end
- Scrappiness + shipping: a hackathon or side project that got built and deployed quickly
- Cross-functional collaboration: working with multiple engineers or teams, standardizing shared tooling
- Building from zero: starting a club, initiative, or product and growing it
- ML + hardware (or any cross-discipline combination): a pipeline built under real hardware constraints
- Communication and documentation: writing, content, or rebranding work with measurable growth

The example must be real and traceable to claude.md or extra-info.md. Never fabricate.

---

## Step 5: Quality Check (Internal, Before Writing Docx)

Run through this before proceeding:

- [ ] Does the opening word choice feel tailored or like a default?
- [ ] Does each "excited" point reference something specific from company research?
- [ ] Could a generic applicant have written any of these points? If yes, rewrite.
- [ ] Does each "choose me" point follow claim -> situation/action -> outcome in exactly 3 sentences?
- [ ] Is every example real and traceable?
- [ ] Does it sound like the candidate or like a cover letter template?
- [ ] Are all points within their sentence limits (2 / 3)?

Fix any failure before writing the docx.

---

## Step 6: Write the Output .docx

Build the cover letter as a `.docx` using the `docx` npm package.

**Output path:**
```
job-search/applications/[Company Name - Role]/cover-letter-[companyname].docx
```

**Formatting spec:**
- Font: Calibri, 12pt throughout
- Page: US Letter (12240 x 15840 DXA), margins 1 inch (1440 DXA) all sides
- No header, no footer, no page number
- **"Why I'm excited about this role"** and **"Why choose me"**: bold, 12pt
- Bullet points: use `LevelFormat.BULLET` with numbering config, never unicode bullet characters
- Bullet indent: `{ left: 720, hanging: 360 }`
- Paragraph spacing: `{ before: 0, after: 120 }` for body; `{ before: 200, after: 80 }` before bold headers
- Opening line: plain paragraph, no bold except the focus area words
- Closing line: plain paragraph

**Build, validate, cleanup:**
```bash
# After writing the JS and running it:
python scripts/office/validate.py "job-search/applications/[Company Name - Role]/cover-letter-[companyname].docx"
# If validation fails: inspect error, fix, rebuild
```

---

## Step 7: No Printed Output to User

Do not print the cover letter text to the user. Do not print a research summary. The deliverable is the `.docx` file. Confirm the output path only:

```
✓ cover-letter-[companyname].docx saved to job-search/applications/[Company Name - Role]/
```

---

## Batch Mode: Multiple Job Descriptions

If the user provides 2 or more job descriptions in one message, switch to batch mode automatically.

### Step B1: Spawn Parallel Subagents

Spawn one subagent per JD. Each agent:
1. Receives: its JD and paths to claude.md / extra-info.md
2. Runs the full pipeline independently: company research -> connection mapping -> write -> quality check -> docx output
3. Saves to: `job-search/applications/[Company - Role]/cover-letter-[company].docx`

Agents run **concurrently**. Do not wait for one to finish before starting the next.

### Step B2: Confirm All Outputs

Once all agents complete, confirm all paths in one message:

```
✓ CompanyA - Structures Intern -> cover-letter-companya.docx
✓ CompanyB - Data Analyst Intern -> cover-letter-companyb.docx
✓ CompanyC - Robotics Intern -> cover-letter-companyc.docx
```

### Batch Mode Rules
- **Never process sequentially**; always parallelize
- **Each cover letter must be genuinely unique**: different company research, different connection map, different examples drawn from extra-info.md. Batch mode is not an excuse for copy-paste with swapped names.
- **A failure in one agent does not block others**: flag the failed one, confirm the rest

---

## Absolute Principles

- **No em dashes. Ever.** Not in any sentence, point, or line of the cover letter. Use a comma, colon, or rewrite the sentence instead.
- **Specificity over warmth.** A specific sentence always beats a warm generic one.
- **Research is not optional.** Surface-level knowledge produces surface-level letters.
- **Never fabricate.** Every example must be real and traceable.
- **Sentence limits are hard rules.** 2 sentences per "excited" point. 3 sentences per "choose me" point. Never exceed.
- **No approval gate.** Research -> map -> write -> quality check -> build docx -> confirm path.
- **The template is fixed.** Fill it in exactly as given. Never restructure.
- **The candidate's voice, not yours.** Sharp and real, not polished in a corporate way.
