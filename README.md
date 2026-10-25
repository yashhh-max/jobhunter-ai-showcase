# JobHunter AI

**An autonomous agent that finds jobs, internships, hackathons and tech events, builds a true resume for each one, applies, and asks its owner for help only when a human is needed.**

**Live site: [jobhunter-ai-mauve.vercel.app](https://jobhunter-ai-mauve.vercel.app)** (a private, single-owner app: the sign-in page is public, the data is not)

> This repository is a project showcase. The source code is private and is not published here. The video uses sample data only.

[![JobHunter AI walkthrough](demo-preview.gif)](demo.mp4)

[Watch the full walkthrough (demo.mp4, 52 seconds)](demo.mp4)

## What it does

- **Discover.** Pulls fresh postings from Greenhouse, Lever, RemoteOK and LinkedIn every hour, keeps only roles in the owner's field that are open to India-based juniors, skips unpaid roles, off-stack roles and scam patterns, and scores each posting against the owner's profile.
- **Tailor.** Builds a one-page LaTeX resume and a cover letter per job from a single master resume. A no-fabrication rule means it never adds a skill, project or date the owner does not have. A final check compares every resume with the master: one page, readable by applicant-tracking systems, real facts only.
- **ATS score on every application.** Each generated resume gets an internal ATS-alignment score out of 100 (sections, contact details, how many of the job's skills the resume truthfully covers, job-title words, one page). Skills the owner lacks are never added to raise it. It is saved with the application and shown in the app (Sent, Needs you, Overview) and in the email the owner receives for every application.
- **Apply.** Sends the resume by email from the owner's own Gmail when a posting names an address, or fills the company form with a browser. Dropdowns and standard questions (country, sponsorship, previous employment) are answered truthfully, and roles that need another country's work permit are skipped. An application counts as sent only when a confirmation is seen or an email really went out.
- **Ask for help.** If a CAPTCHA or a new question appears, it pauses and sends a phone alert and an email with a link. It never bypasses a CAPTCHA. Answers are saved and reused.
- **Hackathons and tech events in Hyderabad.** Finds in-person and hybrid events from Devfolio, Unstop, Meetup, Luma and Eventbrite, alerts the owner, adds events to a calendar feed, and registers automatically where a plain Google Form allows it. Pages that need a login or show a CAPTCHA are handed to the owner with the reason.
- **Fill extension and Apply kit.** A Chrome extension fills any application form and attaches the right resume on a laptop. On a phone, a kit page offers the resume download and one-tap copy for every answer.
- **Follow up.** Reads the inbox (read-only) for replies, tracks approvals and declines, adds interviews to the owner's iPhone calendar, and emails interview prep. A built-in bank of 55 internship questions comes with full answers that use only the owner's real facts.
- **Safeguards.** If Gmail rejects the login, the agent says so on the dashboard and on the phone and pauses email steps. A watchdog alerts if a scheduled run goes missing.
- **Runs on free tiers.** Scheduled runs use GitHub Actions, the database is Neon Postgres, the API is on Render and the site is on Vercel. No server stays on at home.

## How it fits together

```
Sources (Greenhouse, Lever, RemoteOK, LinkedIn) + Hyderabad events
        |
   Filters: field, India, seniority, unpaid, scams  ->  match score  ->  auto-apply / watch / reject
        |
   Resume + cover letter (LaTeX, one page, master-resume check, ATS score)
        |
   Email apply  or  company form (Playwright)  or  event registration (Google Forms)
        |                         |
   proof of sending       needs a person? -> phone alert + email -> Apply kit / Fill extension
        |
   Inbox check -> interview invite -> calendar + prep with answers
```

## Built with

Python and FastAPI, SQLAlchemy (async) with Postgres, Playwright, LaTeX, Next.js and React with Tailwind, a Chrome extension, GitHub Actions for scheduling, Neon, Render and Vercel for hosting, ntfy for phone push. The backend has 490+ automated tests.

## What I worked on

I designed and built the whole system: discovery and filtering, the resume engine and its safety rules, the form-filling, email and event-registration flows, the human-in-the-loop handoff, inbox tracking, interview prep, the browser extension, the web app and its design, and the free-tier hosting setup.

## Status

A working personal tool, used by its owner only. It is not a service for others and is not affiliated with any employer, event organiser or job board.

## Contact

Yashwanth: [GitHub @yashhh-max](https://github.com/yashhh-max)
