# book-skills

Claude Code skills, one per book. Each skill triggers automatically when you mention that book's concepts (not just the book title), and steers Claude to apply that book's framework to your actual request.

## Structure

```
skills/
  lean-startup/
    SKILL.md
  _template/
    SKILL.md   <- copy this to start a new skill
```

## Adding a new skill

1. Copy `skills/_template/SKILL.md` into `skills/<book-slug>/SKILL.md`.
2. Fill in `name` and `description`. The description is what triggers the skill — list the book's key terms/concepts explicitly, not just the title, and make it a little "pushy" (Claude under-triggers skills by default).
3. Write 3-8 core concepts (not a full book summary — only what's actionable).
4. Write a "How to apply this" section with concrete steps for how a response should be structured when the skill fires.
5. Try it in a real conversation. Tune the description if it doesn't trigger when expected.

## Installed skills

- `lean-startup` — Eric Ries, *The Lean Startup*. Build-Measure-Learn, validated learning, MVP, innovation accounting, pivot/persevere.

## Installing

Point Claude Code at this repo's `skills/` directory (or symlink individual skill folders into your Claude Code skills path) so they're picked up as available skills.
