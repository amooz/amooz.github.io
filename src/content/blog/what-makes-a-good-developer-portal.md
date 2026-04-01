---
title: What Makes a Good Developer Portal?
description: After spending two years building OpsLevel's developer portal product, here's what I learned about what engineers actually need from internal tooling.
pubDate: 2024-03-15
tags:
  - developer experience
  - platform engineering
  - leadership
---

A developer portal is one of those things that sounds straightforward until you try to build one.

The naive version is a documentation site with some links. Ship a Confluence page, call it a portal, move on. Most companies start there. And most developers immediately stop using it.

The problem isn't the documentation. It's that documentation is only part of what a developer portal needs to do.

## What developers actually need

When an engineer joins a new team or picks up an unfamiliar service, they have a set of questions they need answered quickly:

- What does this service do?
- Who owns it?
- Is it healthy right now?
- How do I deploy it?
- Where do the logs live?
- What does it depend on, and what depends on it?

A good developer portal answers all of these in one place, connected to live data rather than hand-maintained docs.

The "connected to live data" part is where most portals fail. Docs go stale. Nobody updates the runbook after the oncall rotation changes. The architecture diagram reflects a topology from eighteen months ago. Engineers learn quickly not to trust the portal, so they stop going there, so nobody maintains it, so it gets worse.

## The two jobs of a portal

I've come to think of a developer portal as having two distinct jobs:

**Job one: reduce time-to-understanding.** A new engineer should be able to go from "I've never touched this service" to "I understand what it does, who to ask, and where the relevant dashboards are" in under five minutes. That's the onboarding use case, and it's the one people think about most.

**Job two: reduce cognitive overhead for owners.** The engineers who run a service day-to-day should be able to see its full context — dependencies, deployment history, open incidents, outstanding tech debt — without switching between four tools. That's the operational use case, and it's where portals earn or lose their reputation.

Most portals do job one passably and job one only. They're reference docs with a nice UI. Job two is harder because it requires real integrations: your CI/CD system, your incident tracker, your observability stack, your dependency graph. But job two is where you get daily active users instead of monthly.

## What I'd build differently

At OpsLevel, we spent a lot of time on the integration layer — pulling service metadata, scorecards, and health signals from the systems that already knew about them. That was the right call. The manual-entry approach to service catalogs doesn't scale and doesn't stay accurate.

If I were starting a developer portal from scratch today, I'd focus on:

1. **Automatic discovery first.** Import from your infrastructure-as-code, your Kubernetes clusters, your GitHub repos. Make it hard to have an undiscovered service.
2. **Ownership as a first-class concept.** Every service has a team. Every team has an oncall. That should be queryable.
3. **Scorecards that drive behaviour.** Not just "here's how you're doing" but "here's the three things you should fix this sprint."
4. **Integrations before features.** A portal that shows your actual Datadog dashboards is more valuable than one with a beautiful custom charting system that shows nothing real.

The tools in this space have gotten genuinely good. Backstage, OpsLevel, Cortex, Port — any of them will get you somewhere real. The choice between them matters less than the commitment to keeping the data current.

---

*This post is drawn from my time leading engineering at OpsLevel. Opinions are mine.*
