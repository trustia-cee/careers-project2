# Technical Test - Trustia | Senior Developer (CDI)

> This test is designed for **experienced developers** applying for a permanent position.
> It evaluates not only your ability to deliver, but your **judgment, taste, speed, and how you collaborate with AI tools**.

---

## Ground Rules (read carefully — these are eliminatory)

1. **All code must be written in English** (variable names, functions, comments, commit messages, documentation).
2. **The user-facing interface must be fully multilingual** (i18n) — minimum `EN` and `FR`, easy to extend.
3. **PostgreSQL is mandatory** — no SQLite, no MySQL, no "it also works with...".
4. **The README is part of the evaluation.** A reviewer must be able to run the full project with **a single command** (`docker compose up` or equivalent). Any setup requiring manual steps beyond cloning + one command is **eliminatory**.
5. **AI tools are mandatory** on this test. We expect you to use them. What we evaluate is **how** you use them — your prompts, your review process, and the decisions you made about when *not* to trust AI output. Be ready to explain this.
6. **Response time matters.** The clock starts when you receive this test. Speed + quality = strong signal.
7. **Your code is your portfolio.** Alongside the project, you must deliver a personal portfolio website (see Exercise 4) presenting previous work with screenshots and/or live links.

---

## Exercise 1 — Code Review & Refactor

We will provide you with a small Python/Django module (≈ 200 lines) that **works but is badly written**: N+1 queries, poor naming, dead code, missing type hints, no tests, a subtle bug.

Your job:

- Deliver a clean, refactored version.
- Write a **short `REVIEW.md`** (max 1 page) listing every issue you found, how you fixed it, and the reasoning behind each decision.
- Add unit tests that would have caught the bug.
- Explicitly flag which parts were generated or suggested by AI, and which you rewrote by hand and why.

We are not looking for perfection — we are looking for **judgment**. Over-engineering is penalized.

> The source module will be sent in a separate email once you confirm you have started the test.

---

## Exercise 2 — Full-Stack Application

Build a small SaaS-style application: **a product catalog with invoicing, multi-user, multilingual, with an admin dashboard**.

### Functional scope

**Authentication & authorization**

- Email + password sign-up / login
- Role-based access: `admin`, `manager`, `viewer`
- JWT or session-based auth (justify your choice in the README)
- Password reset flow (email can be mocked via console log)

**Products**

- CRUD: id, name, description, price, VAT rate, expiration date, stock, category, image
- Search + filter + sort + pagination (server-side)
- Bulk import from CSV
- Soft delete + audit log (who changed what, when)

**Invoicing**

- Create invoice, add products with quantity, apply discount
- Automatic total with VAT breakdown
- Invoice PDF export
- Invoice statuses: `draft`, `sent`, `paid`, `overdue`
- Prevent editing once `sent`

**Dashboard**

- Revenue over time, top products, overdue invoices
- Must load in under **500 ms** on a dataset of 10,000 products + 5,000 invoices (we will test)

### Technical constraints

- **Backend**: Django or FastAPI (your choice, justify it)
- **Database**: PostgreSQL, with proper indexes and migrations
- **Frontend**: your choice (React, Vue, Svelte, HTMX, Django templates) — but the design must be **modern, clean, and responsive**. Ugly UI is eliminatory.
- **i18n**: minimum EN + FR, with a language switcher; all strings externalized
- **Caching**: use Redis (or equivalent) where it makes sense — explain your choices
- **Tests**: at least one meaningful test per layer (model, view, integration). 100% coverage is not the goal, relevance is.
- **CI**: a working GitHub Actions (or equivalent) pipeline running linting + tests on every push
- **Docker**: full `docker-compose.yml` with Postgres, Redis, backend, frontend — one command boots the whole thing with seed data
- **Seed data**: provide a seed script that creates a realistic dataset (≥ 10,000 products, ≥ 5,000 invoices) so the dashboard performance claim can be verified

### Performance requirement

Document in the README:

- The **three slowest queries** of your app and how you optimized them (EXPLAIN output welcome)
- Your caching strategy
- Any noteworthy architectural decision and its trade-offs

---

## Exercise 3 — AI-Powered Feature

You must integrate **at least one AI-powered feature** into the application. Examples (pick one or propose your own):

- Smart semantic search on products (embeddings + vector search)
- Automatic product categorization from name + description
- Natural-language query on the dashboard ("revenue last quarter for category X")
- Assistant that drafts an invoice from a short description

Constraints:

- The AI call must be **abstracted behind an interface** so the provider can be swapped.
- Handle failure, rate limits, and cost. Show the reviewer you thought about what happens when the API is down or slow.
- In the README, explain: what you chose, why, the prompt(s) you designed, how you evaluated output quality, and how you would monitor it in production.

A flashy but brittle integration scores lower than a modest, well-engineered one.

---

## Exercise 4 — Personal Portfolio Website

Deliver a **separate personal portfolio website** (can live in the same repo under `/portfolio` or its own repo — your call).

Requirements:

- Ultra-modern design. Treat this as a showcase of your frontend taste.
- Presents **at least 3 past personal or professional projects**, each with:
  - A short description (problem, solution, your role)
  - Screenshots **or** a link to a live demo **or** a link to the source code
  - The tech stack used
- About section: who you are, what you're looking for
- Must be deployed and accessible via a public URL (Vercel, Netlify, Render, GitHub Pages, or your own hosting — free tiers are fine)
- Responsive, accessible, fast (Lighthouse ≥ 90 on performance and accessibility will be checked)

This site is the first thing we will look at. Make it count.

---

## Submission Format

A **public Git repository** (GitHub / GitLab) containing:

```
/backend           # Exercise 2 backend
/frontend          # Exercise 2 frontend (or integrated)
/portfolio         # Exercise 4 (or separate repo linked in README)
/refactor          # Exercise 1 refactored code + REVIEW.md
docker-compose.yml
README.md          # see below
```

### README.md must include

- One-command launch instructions (and nothing else to make it run)
- Project architecture overview (one diagram is welcome, not mandatory)
- List of default seeded accounts (admin / manager / viewer) with passwords
- Your three slowest queries + how you optimized them
- Your AI integration: choice, prompt, evaluation, fallback strategy
- How to run the tests
- A short note on your use of AI during this test: which tools, for what, where you rejected AI output and why

**Complex or unclear launch instructions = eliminatory.** We will test on a clean machine.

---

## Response Email

Send your submission to **jacques.zhuang@trustia.ai** with:

- The link to the public repository
- The link to the deployed portfolio
- **Why you?** A short paragraph on your motivation for joining Trustia
- Your **strengths** (3 max) and your **weaknesses** (at least 2, honestly)
- **Bonus, strongly encouraged**: a short video (≤ 3 minutes) presenting yourself and walking through your project

---

## Evaluation Grid

| Criterion                                   | Weight |
| ------------------------------------------- | -----: |
| Code quality, readability, architecture     |   25 % |
| Performance & PostgreSQL usage              |   15 % |
| UI / UX polish and i18n                     |   15 % |
| AI integration and reasoning                |   10 % |
| Portfolio website (taste + content)         |   15 % |
| README clarity + one-command launch         |   10 % |
| Response speed                              |    5 % |
| Self-awareness in the email (strengths/weaknesses, video) | 5 % |

---

## Stack (suggested, not imposed)

- Python 3.11+ / Django 5 **or** FastAPI
- PostgreSQL 15+
- Redis
- React / Vue / Svelte / HTMX
- Docker + Docker Compose
- Any AI provider (OpenAI, Anthropic, Mistral, local model — your call)

---

## Use of AI Tools

- **AI use is expected and required** on this test.
- We will evaluate **how** you use it, not whether you use it.
- Be ready to discuss your prompts, your review workflow, and the moments you chose to write code by hand.

---

## Deadline

We do not set a hard deadline, but **speed is part of the evaluation**. Tell us when you start, and send your submission when you are satisfied. A polished delivery in 4 days beats a sloppy one in 10.

Good luck.

**— The Trustia Team**
