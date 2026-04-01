---
title: What Shipping at Shopify Scale Teaches You
description: Three years of working on infrastructure that had to stay up while millions of merchants ran their businesses on it. What sticks with you.
pubDate: 2023-09-04
tags:
  - engineering
  - shopify
  - scale
  - reliability
---

When you work at a company where a ten-minute outage makes international news, you develop certain instincts.

Not paranoia exactly. Something more like a deep respect for the blast radius of a change, combined with genuine confidence that you can ship fast if the process is right.

I joined Shopify as a senior engineer working on platform infrastructure. My first week, a senior colleague walked me through our deploy process and said something I've thought about often since: "We deploy hundreds of times a day. The way we do that safely is by making each deploy small, observable, and reversible."

That sentence contains most of what I learned in three years.

## Small

The most dangerous deploys are the ones that bundle too much. A small deploy is easy to understand, easy to test, and — crucially — easy to roll back when something goes wrong.

At Shopify, the constraint was cultural as much as technical. PRs were small. Feature flags were ubiquitous. The philosophy was: merge early, ship incrementally, keep main deployable at all times.

The discipline this requires is real. It's easier to write a big PR. You can keep all the context in your head, make all the changes at once, and feel like you're moving fast. But you're borrowing against the complexity of the review, the deploy, and the eventual rollback you might need.

## Observable

You can't be confident about what you can't see.

At the scale Shopify operated, observability wasn't optional. We invested heavily in instrumentation, dashboards, and alerting. Every significant deploy was watched. Engineers were expected to be watching.

The thing that changed how I thought about this: it's not enough to observe that your deploy succeeded. You need to observe that the *behaviour* you expected actually happened. Those are different things. A deploy can succeed and still introduce a performance regression that won't surface in your deployment dashboard.

Building good metrics into features before shipping them is a discipline that pays off every time.

## Reversible

The ability to roll back quickly is a force multiplier for shipping speed.

If a rollback takes thirty seconds, you can ship aggressively. If it takes thirty minutes, you're much more conservative. The deploy cadence of a team is directly tied to how fast they can recover from a bad one.

Feature flags give you granular reversibility — you can turn off a feature for a subset of users without rolling back the entire deploy. That's powerful, but it only works if the flags are cleaned up afterward. The discipline to remove old flags is as important as the discipline to add them.

## What I carried forward

When I moved into engineering management, these three instincts shaped how I led teams. Not as rules, but as lenses:

Is this change too large? Can we break it up?
Do we have the observability to know if it's working?
What does rollback look like, and have we actually tested it?

The specifics change with the codebase and the team. But the questions stay useful.

---

*Written based on my time as a senior engineer at Shopify, 2019–2022.*
