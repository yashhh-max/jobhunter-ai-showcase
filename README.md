# JobHunter AI

**An autonomous agent that finds jobs and internships, tailors the resume with true facts only, applies, and asks its owner for help only when a human is needed.**

**Live site: [jobhunter-ai-mauve.vercel.app](https://jobhunter-ai-mauve.vercel.app)** (a private, single-owner app: the sign-in page is public, the data is not)

> This repository is a project showcase. The source code is private and is not published here.

[![JobHunter AI walkthrough](demo-preview.gif)](demo.mp4)

[Watch the full walkthrough (demo.mp4)](demo.mp4)

## What it does

- **Discover.** Pulls fresh postings from Greenhouse, Lever, RemoteOK and LinkedIn on a schedule, keeps only roles in the owner's field that are open to India-based juniors, and scores each one against the owner's profile. A score threshold routes it to auto-apply, watch or reject.
- **Tailor.** Builds a one-page LaTeX resume and a cover letter per job from a single master resume. It reorders skills and projects and rewrites the summary for the role. A no-fabrication rule means it never adds a skill, project or date the owner does not have, and a quality gate flags weak tailoring.
- **Apply.** Fills and submits company career-page forms with Playwright. Where a posting names an email address, it sends the application from the owner's Gmail instead. A job is marked as sent only when a confirmation is seen or an email really went out.
- **Ask for help.** If a CAPTCHA, a new question or an agreement needs a person, it pauses, emails and pushes to the owner's phone with a link, and resumes after the answer. It does not try to bypass CAPTCHAs. Answers are saved and reused.
- **Follow up.** Reads the inbox (read-only) for replies, tracks approvals and declines, adds interviews to the owner's iPhone calendar, and emails interview prep.
- **Runs on free tiers.** Scheduled runs use GitHub Actions, the database is Neon Postgres, the API is on Render and the site is on Vercel. No server stays on at home.

## How it fits together

```
Sources (Greenhouse, Lever, RemoteOK, LinkedIn)
        |
   Domain + eligibility filter  ->  match score  ->  auto-apply / watch / reject
        |
   Resume + cover letter tailoring (LaTeX, one page, no-fabrication rule, quality gate)
        |
   Playwright form submit  or  apply-by-email
        |                          |
   confirmation seen?        needs a person? -> email + phone push -> resume
        |
   Inbox check -> interview invite -> calendar + prep notes
```

## Built with

Python and FastAPI, SQLAlchemy (async) with Postgres, Playwright, LaTeX, Next.js and React with Tailwind, GitHub Actions for scheduling, Neon, Render and Vercel for hosting, ntfy for phone push. The backend has 450+ automated tests.

## What I worked on

I designed and built the whole system: discovery and filtering, the resume tailoring engine and its safety rules, the form-filling and email-apply flows, the human-in-the-loop handoff, inbox tracking, the interview-prep and calendar features, the web app, and the free-tier hosting setup.

## Status

A working personal tool, used by its owner only. It is not a service for others and is not affiliated with any employer or job board.

## Contact

Yashwanth: [GitHub @yashhh-max](https://github.com/yashhh-max)
