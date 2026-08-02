---
name: lean-startup
description: Applies Eric Ries's "The Lean Startup" framework (Build-Measure-Learn loop, validated learning, MVP, innovation accounting, pivot vs. persevere, actionable vs. vanity metrics, five whys, small batches, split testing) to plan or evaluate a feature, product, or business idea. Use this skill whenever the user wants a "lean startup approach," mentions "validated learning," "MVP," "minimum viable product," "build-measure-learn," "pivot," "innovation accounting," or asks how to test a risky assumption before building something fully — even if they don't say "lean startup" by name. Also use when the user is deciding whether to keep or kill a feature/initiative based on data.
---

# The Lean Startup

Apply this skill to structure plans, feature proposals, or decisions around Eric Ries's core idea: treat a new product, feature, or business idea as a series of experiments that test unproven assumptions, not a spec to be built in full.

## Core concepts

**Leap-of-faith assumptions** — Every new idea rests on assumptions that could be wrong. The two biggest: the *value hypothesis* (will people actually want/use this?) and the *growth hypothesis* (how will this spread/scale?). Identify these explicitly before proposing a build plan.

**Build-Measure-Learn loop** — The core cycle. Go in reverse when planning: decide what you need to *learn*, figure out what *metric* answers that, then design the *minimum* thing to build to get that data. Most people plan forward (build → measure → learn) and waste effort; lean planning starts from the learning goal.

**MVP (Minimum Viable Product)** — Not a smaller/crappier version of the final product. It's the smallest experiment that generates validated learning about a leap-of-faith assumption, with the least effort. An MVP can be a landing page, a concierge manual process, a Wizard-of-Oz fake front-end, a single feature — whatever tests the riskiest assumption fastest. When proposing an MVP, always name which assumption it tests.

**Validated learning** — Progress means *proof* that assumptions hold (or don't), backed by data from real customer behavior — not opinions, not "we shipped X features." If a plan can't say what would count as disproof, it isn't validated learning yet.

**Innovation accounting** — Track progress with a small number of actionable metrics tied to the hypotheses, not vanity metrics (total signups, pageviews, cumulative totals — numbers that only go up and don't inform decisions). Prefer cohort-based, per-customer, ratio metrics that can go up or down and drive a decision.

**Actionable vs. vanity metrics** — A metric is actionable only if: it shows clear cause and effect, it's understandable/memorable, and it changes behavior. If a metric can't fail a test, it's vanity — call this out when a user proposes success metrics.

**Pivot or persevere** — After each Build-Measure-Learn loop, force an explicit decision: does the data support the hypothesis (persevere) or not (pivot — a structured course correction that keeps one foot rooted in what was learned, e.g. zoom-in, zoom-out, customer segment, platform, value-capture pivot)? Don't let a plan drift without this checkpoint.

**Small batches / continuous deployment** — Prefer small batch sizes over big-batch, big-bang launches. Small batches surface problems faster and shorten the feedback loop, even if there's per-unit overhead.

**Five Whys** — When something breaks or underperforms, root-cause it by asking "why" repeatedly, and pair each fix with a proportional investment in prevention (not just a patch).

## How to apply this

When the user asks for a lean-startup approach to something, structure the response around these steps rather than jumping to a full build plan:

1. **State the leap-of-faith assumptions** — what has to be true for this to work? Separate value hypothesis from growth hypothesis.
2. **Rank assumptions by risk** — which one, if wrong, kills the idea? Test that one first.
3. **Design the smallest MVP** that produces evidence on the riskiest assumption. Say explicitly what it is NOT going to include, and why that's fine.
4. **Define the actionable metric(s)** that will judge the experiment — and what result would count as failure, not just success. Flag any vanity metrics the user proposes.
5. **Set a pivot/persevere checkpoint** — when will this be evaluated, and what happens in each branch?
6. If relevant, note which kind of pivot would apply if the data disappoints (zoom-in, zoom-out, customer segment, platform, means-vs-ends, etc.)

Keep the tone practical — this is a planning lens, not a lecture on the book. Don't cite chapter/page numbers or dump definitions the user didn't ask for; apply the concepts to their actual situation.
