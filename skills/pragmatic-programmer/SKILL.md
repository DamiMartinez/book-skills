---
name: pragmatic-programmer
description: Applies Andrew Hunt & David Thomas's "The Pragmatic Programmer" (20th Anniversary / 2nd Edition, 2019) framework — DRY, orthogonality, reversibility, tracer bullets, broken windows, good-enough software, Design by Contract, decoupling and the Law of Demeter, programming by coincidence, refactoring, property-based testing, naming, requirements gathering, automation, and pragmatic team practices — to software design, code review, debugging, refactoring, requirements, and engineering-practice questions. Use whenever the user wants a "pragmatic programmer approach," mentions "DRY," "orthogonality," "tracer bullet," "broken windows," "programming by coincidence," "Design by Contract," "Law of Demeter," or asks how to design a module, reduce coupling, write better tests, gather requirements, or build good engineering habits — even if they don't name the book.
---

# The Pragmatic Programmer

Apply this skill to day-to-day software design, coding-practice, debugging, and requirements questions using the Pragmatic Programmer's checklist-style principles, drawn from the 2019 20th Anniversary (2nd) Edition.

## Core concepts

**DRY — Don't Repeat Yourself** — Every piece of knowledge (not just code text) should have a single, unambiguous, authoritative representation in the system. Duplicated logic, duplicated data schemas, duplicated documentation-vs-code all count. When reviewing code or a design, look for knowledge duplication, not just copy-pasted lines.

**Orthogonality** — Design components so a change in one has no ripple effect on unrelated ones. Ask "if I change this, what else could break that has no logical connection to it?" Low orthogonality shows up as fragile systems where small changes cause surprising failures elsewhere.

**Reversibility** — Avoid decisions that are hard to undo (a specific vendor, a rigid architecture, a hardcoded assumption) when a reversible alternative is available at similar cost. Not every decision needs maximum flexibility — but flag when a design bakes in an assumption (a database choice, a third-party API) that will be expensive to change later.

**Tracer bullets & prototypes** — For unclear or risky requirements, build a thin end-to-end skeleton that actually runs (a tracer bullet) to get real feedback fast, as opposed to a throwaway prototype meant to explore/discard one specific unknown. Know which one the situation calls for: tracer bullets get kept and built on; prototypes get thrown away once they've answered their question.

**Broken windows & boiled frogs** — Visible small decay (a broken window: sloppy code, a "TODO" left too long, a hacky workaround) signals that decay is acceptable and invites more of it — fix it or explicitly flag/timestamp it. "Boiled frog" is the danger of not noticing gradual degradation because no single step looks alarming — periodically zoom out and reassess from scratch.

**Good-enough software** — Software is a negotiation with the user about quality vs. cost vs. time, not an unlimited pursuit of perfection. Help the user find the right-sized target for the situation instead of defaulting to "more polish is always better."

**Design by Contract & assertive programming** — Make a function/module's preconditions, postconditions, and invariants explicit (in code or comments), and use assertions to make "this should never happen" states fail loudly instead of silently. Exceptions should signal genuinely exceptional conditions, not be used for routine control flow.

**Decoupling & the Law of Demeter** — A module should only talk to its immediate collaborators, not reach through them to their internals ("don't talk to strangers"). High coupling between modules is one of the biggest sources of fragile, hard-to-change systems — when reviewing a design, trace how many other modules a change would ripple through.

**Temporal coupling & concurrency** — Distinguish things that must happen in a specific order from things that only happen to be written in that order — the latter is hidden coupling that limits concurrency and flexibility. When relevant, think in terms of workflow/activity diagrams (what can run in parallel) rather than a linear script.

**Programming by coincidence vs. deliberately** — If code works but you're not sure *why*, that's programming by coincidence — dangerous, because you can't tell working code from accidentally-working code. Push for understanding why something works, not just confirmation that it does (relevant to debugging and to reviewing unfamiliar/inherited code).

**Refactoring & test-driven confidence** — Refactor early and often in small steps backed by tests, rather than let cruft accumulate for a "big rewrite" later. Property-based testing (asserting general properties/invariants across generated inputs) catches edge cases example-based tests miss — suggest it for logic with clear invariants (parsers, math, serialization).

**Naming things** — Names should reflect what something *is* or *does* in the problem domain — a good name is a design decision, not a formality. Poor or misleading names are a signal of an unclear underlying design, not just a style nitpick.

**Requirements: "solving impossible puzzles" & "not until you're ready"** — Question given constraints — many "requirements" are actually just the requester's default solution, not the real constraint. Dig for the real requirement, and don't over-commit to a plan before you have enough information; it's fine to explicitly defer a decision.

**Automation & ruthless testing** — Anything done by hand more than once (builds, deploys, environment setup, testing) should be automated — manual repeated procedures are a source of both wasted effort and inconsistent results. Testing should be integrated continuously, not treated as a separate late phase.

**Pragmatic teams** — The same individual principles (DRY, orthogonality, automation, no broken windows) apply at the team level — a team can have organizational duplication, coupling, or decay just like a codebase can.

## How to apply this

When the user brings a design, code-review, debugging, refactoring, or requirements question, route it through the relevant principle(s) rather than generic advice:

1. **Identify which concern is actually in play** — duplication (DRY), fragility from unrelated changes (orthogonality/coupling), a hard-to-reverse decision, unclear requirements, decaying code quality, or a testing/automation gap. Don't invoke every concept every time — pick what fits.
2. **For design/architecture questions** — check coupling and orthogonality first; trace what a change would ripple into.
3. **For debugging** — ask "do you know why this works/fails, or does it just seem to?" to catch programming-by-coincidence; suggest assertions/contracts to make hidden assumptions explicit.
4. **For refactoring or legacy-code cleanup** — treat visible small decay as a broken window worth naming, and push small test-backed steps over a big-bang rewrite.
5. **For requirements gathering** — probe whether a stated requirement is the real constraint or a default solution in disguise; flag premature commitment.
6. **For testing questions** — suggest property-based tests where there's a clear invariant, and flag manual/repeated steps that should be automated.

Keep it concrete and tied to the user's actual code/situation — this is a working engineer's checklist, not a book summary to recite.
