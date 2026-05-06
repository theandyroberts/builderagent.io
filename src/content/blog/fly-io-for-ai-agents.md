---
title: "fly.io for AI agents: why we're building BuilderAgent"
description: "fly.io changed deployment by treating servers as a side effect of intent. BuilderAgent does the same for AI agents — you describe the goal, the platform handles the rest."
publishedAt: 2026-05-06
author: "BuilderAgent Team"
tags: ["product", "philosophy", "platform"]
---

A few years ago, deploying a web app meant doing real work. You picked a cloud, learned a console, sized a VM, configured a load balancer, set up a CI pipeline, wrote a Dockerfile, debugged a Dockerfile, swore at a Dockerfile. None of that was your product. All of it stood between you and shipping.

Then fly.io did something simple and obvious: they made deployment a side effect of intent. `fly launch`, then your app exists at a URL. Servers, networking, edge — all handled. The server stopped being something you owned and started being something the platform managed for you.

We think AI agents are at the same moment.

## The agent-deployment tax in 2026

If you sat down today to ship an "agent" — say, one that monitors a website daily and emails you a digest — here's what you'd own end-to-end:

- A model router that picks the right LLM and falls back when one's degraded.
- A vector store for memory, plus the embedding pipeline that fills it.
- A queue and retry policy for the actual work loops.
- A scheduling layer that fires the loop on the right cadence.
- A state machine that survives crashes and model upgrades.
- A web server to publish results.
- An OAuth dance for every external API the agent touches.
- A cost dashboard so the bill doesn't surprise you.
- An observability stack so you can debug when it goes sideways.

None of that is your agent. All of it is the tax you pay before your agent runs once.

## What if the platform owned all of it?

That's the bet behind BuilderAgent. We took everything in that list and put it inside a single hosted product. You don't pick a model — we pick the best one and rotate every two hours. You don't manage state — your agent has a persistent file system and memory that survive upgrades. You don't set up retries — the loop is the unit of execution. You don't wire OAuth — there are 800+ integrations pre-wired and ready.

What you do is name your agent and describe the goal. The platform handles the rest.

## The fly.io tells

Three things tell you a platform has crossed the "owned by intent" line. fly.io has all three. We've tried to copy them deliberately:

**1. The unit of deployment matches your mental model.**
On fly.io, the unit is "an app at a URL". On BuilderAgent, the unit is "an agent at a goal". Not "a model call", not "a function", not "a workflow". A single conceptual thing that exists in the world and does its job.

**2. The defaults are good enough that you don't reach for the controls.**
fly.io picks regions, sizing, and runtime defaults that are right for 90% of cases. We pick models, memory limits, scheduling, and recovery policies the same way. If you need to override, you can — but you almost never need to.

**3. The bill is honest.**
fly.io shows you what you're paying for, and the price doesn't surprise you. Our Standard tier is $29/month with no usage caps. The price is the price.

## What we're not doing

We're not building a new agent framework. OpenClaw — the open-source runtime under the hood — is excellent, has a community, and is moving fast. We're the cloud platform that lets you run it without owning a server.

We're not trying to replace Claude or GPT. The frontier models are a commodity, and the right one keeps changing. Our job is to use them well.

We're not building a low-code agent builder. Plain-language goals are easier than dragging boxes around a canvas, and they're more powerful too. The "code" is your description of the work.

## When BuilderAgent isn't right

If your agent is a one-shot enrichment that runs inside an existing app, you don't need us — a function call to an LLM is fine. If you need full custody of weights and infrastructure, you need to host OpenClaw yourself. If you want to build the platform layer, by all means do; we'd rather use a competitor's product than be the only option.

But if you've been meaning to ship an agent and you've found yourself reaching for Docker, you're in the gap we're trying to fill.

---

*Want to see what `builder deploy` feels like? [Read the quickstart](/docs) or [start a Standard plan](/pricing) — your agent is online in under two minutes.*
