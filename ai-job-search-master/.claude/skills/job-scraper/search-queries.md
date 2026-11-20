# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Primary (your market's job boards):
- **indeed.com** - Indeed India job listings (filter: Chennai)
- **linkedin.com/jobs** - LinkedIn job listings (filter: Chennai, India)
- **naukri.com** - Naukri India tech job listings (filter: Chennai)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for tech companies in Chennai

## Query Categories

Queries are grouped by priority.

### Priority 1: AI & Python Backend Engineering

These match your strongest and most desired career direction.

```
site:indeed.com/viewjob "Python Developer" Chennai
site:indeed.com/viewjob "AI Engineer" Chennai
site:indeed.com/viewjob "Backend Developer" "Python" Chennai
site:linkedin.com/jobs "Python Developer" Chennai
site:linkedin.com/jobs "AI Engineer" Chennai
site:linkedin.com/jobs "Python Backend" Chennai
```

### Priority 2: LLM & Chatbot Engineering

These match your generative AI and chatbot specialization.

```
site:indeed.com/viewjob "LLM Engineer" Chennai
site:indeed.com/viewjob "Chatbot Developer" Chennai
site:indeed.com/viewjob "Generative AI Developer" Chennai
site:linkedin.com/jobs "LLM" Chennai
site:linkedin.com/jobs "Chatbot" Chennai
site:linkedin.com/jobs "Generative AI Engineer" Chennai
```

### Priority 3: Adjacent AI / Backend Roles

Adjacent roles you could pivot into.

```
site:indeed.com/viewjob "Machine Learning Engineer" "Python" Chennai
site:indeed.com/viewjob "FastAPI Developer" Chennai
site:linkedin.com/jobs "Machine Learning Engineer" Chennai
site:linkedin.com/jobs "FastAPI" Chennai
```

### Priority 4: Broader Technical / Backend Roles

Wider net for general technical roles.

```
site:indeed.com/viewjob "Software Engineer" "Python" Chennai
site:linkedin.com/jobs "Software Engineer" "Python" Chennai
site:indeed.com/viewjob "API Developer" "Python" Chennai
```

## Location Filter

When evaluating results, verify the job location is strictly Chennai or Remote/Hybrid based out of Chennai:
- Chennai and surrounding tech hubs (OMR, Guindy, Tidel Park, Siruseri, Velachery, Ambattur)
- Remote (accepting candidates located in Chennai)
- Exclude roles requiring relocation outside Chennai

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
