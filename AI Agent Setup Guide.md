# AI Agent Setup Guide

## What nobody tells you before you set up your first AI agent

---

## What you're actually setting up

An AI agent is not a chatbot. It's a persistent process that runs on your machine 24/7, communicates via Telegram or Discord, runs scheduled tasks while you sleep, remembers everything across sessions, and can control your computer — browser, files, apps, APIs.

The gap between the demo and daily use is real. People posting "my agent built a full app overnight" have spent weeks tuning. Expect a week of refinement before it feels like a teammate instead of a babysitting job.

---

## The 7 things that actually matter

**1. Don't run everything through your best model.**

This is the #1 mistake. Heartbeats, cron checks, and routine tasks don't need Opus or Sonnet. Set up tiered routing: cheap models (Haiku, Gemini Flash, Kimi) for grunt work, expensive models for thinking. People cut per-request costs from 20-40k tokens down to 1.5k just by routing smarter. This is the "Brains & Muscles" pattern:

- **Brain** = the orchestrator. Decides *what* to do. Needs to be smart. (Opus, Sonnet, GPT-4o)
- **Muscles** = workers. Do the *actual work*. Can be cheap. (Haiku for summaries, Codex for code, Brave for search, Gemini Flash for formatting)

This single pattern cuts costs by 50-80%.

**2. Your agent needs rules. A lot of them.**

Out of the box, it will loop, repeat itself, forget context, and make weird decisions. You need guardrails — a SOUL.md (identity), an OPERATING_CONTRACT.md (rules), and skills (behavioral instructions). The agents that work well are the ones with heavily customized instruction sets. You are the conductor.

The three files that matter:
- **SOUL.md** — who the agent is, how it behaves, what it values. Without this, every session starts from zero. With it, the agent starts making decisions you agree with before you ask.
- **USER.md** — who you are, your goals, your preferences. The more specific you are about your goals, the more useful the agent becomes.
- **OPERATING_CONTRACT.md** — non-negotiable rules. "Never spend money without approval. Never post publicly without review. Never delete files without listing them first. If you're repeating the same action more than twice, stop — you might be looping." Specific rules work. Vague instructions don't.

**3. "Work on this overnight" doesn't work the way you think.**

If you close the chat, the agent forgets. Sessions are stateful only while open. For background work, you need cron jobs with isolated session targets — these spin up independent agent sessions that run on a schedule and message you results. One-off deferred tasks need a queue paired with a cron that checks it.

**4. Start with ONE thing working end-to-end.**

Don't set up email + calendar + Telegram + web scraping + cron all at once. Every integration is a separate failure mode. Get one workflow working perfectly (like a morning briefing), verify it actually fires, then add the next. One automation working reliably beats ten that are broken.

**5. Save what works.**

Context gets lost over time as sessions compact. Fill in your workspace docs (USER.md, MEMORY.md, HEARTBEAT.md) and store important decisions somewhere persistent. The less your agent has to re-learn, the better it performs.

Think in three tiers:
- **Constitutional memory** — never expires. Security rules, your identity, hard constraints.
- **Strategic memory** — refreshed quarterly. Current projects, goals, creative direction.
- **Operational memory** — auto-archives after 30 days. Current bugs, temporary workarounds, session context. This is the clutter that makes your agent dumb if you don't clean it up.

Set up nightly memory maintenance — a scheduled task that reviews the day's sessions, persists important decisions to files, and prunes stale context. This is the single most important automation for long-term agent quality.

**6. The model matters more than you think.**

Chat quality ≠ agent quality. Models need to handle tool calls reliably. Claude Sonnet/Opus, GPT-5.2, and Kimi K2 handle tool calls well. Avoid models that produce malformed tool calls (test before committing) — some cause infinite retry loops. Cheap models are fine for simple tasks but unreliable as the primary brain.

**7. You're not bad at this. It's genuinely hard right now.**

These platforms are not finished products. If you're spending the first two weeks babysitting, burning tokens, and watching your agent loop — that's normal. The people posting success stories have spent weeks tuning. The gap between the demo and daily use is closing fast, but it's still there.

---

## The mindset shift

Most people use AI agents like chatbots: ask a question, get an answer, done. That's 5% of what an agent can do.

**Don't ask your agent questions. Give it standing orders.**

- Instead of "What's trending?" → "Every morning at 7am, tell me what's trending. If something is blowing up, alert me immediately."
- Instead of "Summarize this article" → "Whenever I share a URL, automatically summarize it and file it in my research folder."
- Instead of "Help me write a tweet" → "Build a skill that drafts tweets in my voice. When I say 'draft tweets about X', give me 5 options."

**The rule of thumb:** Done it 3 times → make it a skill. Do it daily → make it a cron job. Do it weekly → make it a scheduled task. The only tasks left for you should be the ones that genuinely require your judgment.

---

## What NOT to do

1. **Don't give it admin/root access.** Run the agent as a non-privileged user.
2. **Don't let it post publicly without review.** Always gate social media, emails, and public content behind your approval.
3. **Don't ignore costs.** Set spending limits day one. A runaway loop can burn through $50 in an hour.
4. **Don't skip identity files.** Without SOUL.md and OPERATING_CONTRACT.md, you get a generic assistant that loops and forgets.
5. **Don't hardcode API keys.** Use secrets management. API keys in config files = one git push away from compromise.
6. **Don't try to set up everything at once.** One integration at a time. Every new tool is a new failure mode.
7. **Don't expect "work on this overnight" to just work.** Background work needs cron jobs, not an open chat window.
8. **Don't forget to verify.** After setting up any cron job, check that it actually fires. If the "Next" column shows a time in the past, something is broken.

---

## What people are actually using these for

Not hypotheticals — these are real workflows running daily for real people. Sorted by how quickly you'll see value.

### Start here (week 1)

**Morning brief** — Weather, top news in your niche, your tasks for the day, one proactive suggestion. Under 200 words, delivered to Telegram before you wake up. This is the universal first automation.

**Nightly self-review** — Agent reviews its own performance: what did it handle well, where did you have to step in, what friction points need a new skill or rule? Files improvement tickets for your review. This is how the agent gets better over time.

**Personal CRM** — Track every person you interact with: name, how you met, topics discussed, last contact date. Every Monday, get a digest of people you should reconnect with (no contact in 30+ days).

**Inbox declutter** — Summarize newsletters and batch them into one daily digest email. Never scroll through promotional emails again.

### Once you're comfortable (weeks 2-4)

**Content pipeline** — Agent scans your sources for trending topics, drafts content in your voice, queues for approval, publishes on schedule. Works for tweets, threads, newsletters, blog posts.

**Research & intelligence** — Monitor Twitter/Reddit/HN/arXiv for topics you care about. Daily or weekly digests with summaries and key takeaways. One person built a 109-source tech news aggregator with quality scoring.

**Autonomous coding** — Agent builds tools, reviews PRs, fixes bugs, ships features while you sleep. One person has their agent build surprise mini-apps overnight based on brain-dumped goals.

**Meeting notes & action items** — Feed meeting transcripts, get structured summaries with action items automatically created in Jira/Linear/Todoist, assigned to the right person.

**Health & symptom tracker** — Log food and symptoms via chat, agent identifies triggers and patterns over time. Scheduled check-in reminders so you don't forget to log.

### Power user territory

**Multi-agent content factory** — Research agent, writing agent, and thumbnail agent working in dedicated Discord channels. One orchestrator coordinates.

**Self-healing home server** — Infrastructure agent with SSH access runs cron health checks, auto-fixes common issues, alerts you only when it can't self-repair.

**Business agent** — Give the agent ownership of an actual business entity. Set a mission ("make $X with no human employees"), give it Stripe/email/website access, step back to strategic nudges. Real people are doing this.

**Travel assistant** — Parses booking confirmation emails into structured data. Proactively sends trip overviews, packing lists, checkout reminders, missing booking alerts. Readonly — it never touches your bookings.

**Family calendar & household** — Aggregate all family calendars into one morning briefing. Monitor messages for appointments. Track household inventory and maintenance schedules.

**Event guest confirmation** — Call a guest list one-by-one via AI voice to confirm attendance, collect dietary preferences, compile a summary. Fully automated.

**Prediction market autopilot** — Paper trading on Polymarket with backtesting, strategy analysis, and daily performance reports.

### The full community list

The community maintains 40+ verified use cases at [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). Every submission has been tested for at least a day before inclusion. Worth browsing for inspiration.

---

## The life automation audit

Once your agent is stable (give it at least a week), this is the highest-leverage exercise you can do. Send this to your agent:

> "Let's do a life automation audit. Walk me through each area of my life — morning routine, work, communication, finances, health, learning, social media, home, evening — and for each one, ask me what I do repeatedly. Then categorize each task: automate fully, automate with approval, assist only, or keep manual. Build a prioritized implementation plan starting with the highest-impact, lowest-effort automations."

This typically surfaces 10-20 automations people didn't realize they could delegate.

---

## Going deeper

Once you're comfortable with the basics, explore:

- **Multi-agent setups** — Your main agent becomes a planner that delegates to specialists (research agent, coding agent, content agent).
- **Mission Control** — A custom dashboard with approval queues, task tracking, content pipelines.
- **Local models** — Run models via Ollama for free unlimited tokens. Great for coding and summarization. Requires Mac Mini or better.
- **Content pipelines** — Automated research → draft → review → publish. The agent does 80%; you do the final review.
- **Discord as structured output** — Use Telegram for conversation, Discord for organized streams: #alerts, #research, #drafts, #approvals, #daily-log.
- **Dedicated hardware** — An old laptop, Raspberry Pi ($50), or Mac Mini ($600) running 24/7. Your daily computer can sleep; the agent never does.

Don't rush into these. A well-configured single agent with good identity files and a few reliable automations will transform your workflow more than a complex multi-agent setup you don't maintain.

---

## Now go set it up

You don't need this guide open while you do it. Just paste this into Claude Code:

> "Help me set up a 24/7 AI agent from scratch. I want to use [OpenClaw / Hermes / other]. Walk me through it step by step: install, messaging (Telegram/Discord), identity files (SOUL.md, USER.md, OPERATING_CONTRACT.md), model routing (brains & muscles pattern — cheap models for grunt work, smart models for thinking), security (lock messaging to my user ID, bind gateway to localhost, secrets management), and my first cron automation (a daily morning brief). One step at a time. After each step, confirm it's working before moving on."

That's it. Claude already knows how to do the setup. What it doesn't know — and what this guide covers — is the hard-won wisdom about what actually matters once it's running.
