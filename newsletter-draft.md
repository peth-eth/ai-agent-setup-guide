# What Nobody Tells You Before You Set Up Your First AI Agent

I spent two weeks babysitting an AI agent that burned through tokens doing absolutely nothing useful. It sent me 47 empty Telegram check-ins overnight. "No pending tasks. No updates." Forty-seven times. At $0.15 per message.

So here's what actually matters if you're about to set one up yourself.

## It will be dumb. That's on you.

Out of the box, your agent loops, repeats itself, forgets everything between sessions & makes decisions that'll make you question the entire premise of artificial intelligence. The fix isn't a better model. It's three text files.

**SOUL.md** tells it who it is - personality, autonomy level, communication style. Without this, every session starts from scratch. It doesn't know if you want it terse or chatty, proactive or cautious. With a good SOUL.md, it starts making decisions you agree with before you even ask.

**OPERATING_CONTRACT.md** is the rules. "Never spend money without asking. Never post publicly without my review. If you're doing the same thing more than twice, stop - you're probably looping." That last one alone would've saved me from those 47 messages.

**USER.md** is who you are & what you care about. The more specific your goals, the more useful it gets. Vague goals produce vague agents.

## Your expensive model is doing janitor work

Heartbeats, cron checks, simple formatting - none of this needs Opus. One person was paying $8/day because their heartbeat checks ran through their best model. That's paying a brain surgeon to check if you're breathing.

The fix: **Brains & Muscles.** Smart model handles thinking & decisions. Cheap models (Haiku, Gemini Flash) handle the boring stuff - summaries, formatting, lookups. Same quality where it matters, 50-80% less money leaving your wallet.

## "Work on this overnight" does not work

Close the chat, context is gone. The agent doesn't remember.

People who have agents shipping code while they sleep use cron jobs with isolated sessions - scheduled tasks that spin up fresh, do their thing & message you results. Not an open chat window & a prayer.

## What people are actually doing with these

Someone's agent calls wedding guests via AI voice to confirm attendance & dietary preferences. Fully automated. The host just reads the summary.

Another person's agent monitors their home server, runs health checks & self-heals common issues. Only pings when it can't fix something on its own.

One lunatic gave their agent an actual C Corp - Stripe, email, website - with the mission "make money with no human employees." Their role became strategic nudges from the couch.

Multi-agent content factories running in Discord. Research agent, writing agent, thumbnail agent, each in their own channel, with an orchestrator coordinating the whole thing.

And the mundane stuff that's honestly more useful than all of the above - a morning brief before you wake up. Something that tracks everyone you interact with & nudges you about people you haven't talked to in 30 days. A nightly self-review where the agent identifies its own problems & files tickets for you to approve.

(40+ verified use cases at [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases) if you want the full list)

## The actual mindset shift

Stop using your agent like a chatbot. Ask question, get answer, done - that's 5% of what you built.

Give it standing orders. Not "what's trending" but "every morning at 7am, tell me what's trending & if something explodes in my niche, alert me immediately." Not "summarize this" but "whenever I share a URL, summarize it & file it automatically."

Done something 3 times? Make it a skill. Do it daily? Cron job. Weekly? Scheduled task. The only things left should be stuff that actually requires your brain.

## Go set it up

You don't need a guide for the installation. Paste this into Claude Code:

> "Help me set up a 24/7 AI agent from scratch using [OpenClaw / Hermes]. Step by step: install, Telegram, identity files (SOUL.md, USER.md, OPERATING_CONTRACT.md), model routing (cheap models for grunt work, smart for thinking), security, and a daily morning brief. One step at a time, confirm each works before moving on."

Set spending limits day one. A runaway loop burns $50/hour.

Don't set up everything at once. One working automation beats ten broken ones.

And if you're spending the first week feeling like you're terrible at this - you're not. These platforms aren't finished products. The people posting success stories spent weeks tuning. You'll get there.
