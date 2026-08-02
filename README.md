# book-skills

A collection of [Claude Code skills](https://docs.claude.com/en/docs/claude-code/skills), one per book. Each skill packages a book's core framework so Claude applies it automatically whenever you mention the book's ideas — not just when you say the book's title.

Example: with the `lean-startup` skill installed, asking Claude to "help me plan this new feature, I want a lean approach" or "how do I validate this before building it" will make Claude structure its answer around Build-Measure-Learn, MVPs, and actionable metrics — no need to say "use the lean startup skill."

## Available skills

| Skill | Book | Topic |
|---|---|---|
| [`lean-startup`](skills/lean-startup/SKILL.md) | *The Lean Startup* — Eric Ries | Product/startup validation: MVP, Build-Measure-Learn, validated learning, pivot vs. persevere |
| [`high-output-management`](skills/high-output-management/SKILL.md) | *High Output Management* — Andrew S. Grove | Management: managerial leverage, task-relevant maturity, one-on-ones, indicators, decision-making |
| [`hard-thing-about-hard-things`](skills/hard-thing-about-hard-things/SKILL.md) | *The Hard Thing About Hard Things* — Ben Horowitz | Leadership under pressure: wartime/peacetime CEO, no-easy-answers decisions, firing/layoffs, Law of Crappy People |
| [`pragmatic-programmer`](skills/pragmatic-programmer/SKILL.md) | *The Pragmatic Programmer*, 20th Anniversary Ed. — Hunt & Thomas | Engineering practice: DRY, orthogonality, coupling, Design by Contract, refactoring, requirements, automation |
| [`ai-modern-approach`](skills/ai-modern-approach/SKILL.md) | *Artificial Intelligence: A Modern Approach* — Russell & Norvig | AI/algorithm design: PEAS, agent architectures, search (uninformed/A*/minimax), CSPs, Bayesian networks, MDPs |
| [`machine-learning-mitchell`](skills/machine-learning-mitchell/SKILL.md) | *Machine Learning* — Tom M. Mitchell | ML fundamentals: T/P/E framing, bias-variance, evaluation methodology, MAP/naive Bayes, PAC learning, algorithm selection |

More skills (product management, programming languages, design patterns, system architecture, data engineering, etc.) get added over time — see [Contributing](#contributing).

## Installation

Skills are plain folders with a `SKILL.md` file. Claude Code discovers them from a `skills/` directory — either globally (available in every project) or per-project (available only in that repo).

**1. Clone this repo:**

```bash
git clone https://github.com/DamiMartinez/book-skills.git
```

**2. Install a skill** — pick one:

- **Global (recommended)** — available in every Claude Code session on your machine:

  ```bash
  ln -s "$(pwd)/book-skills/skills/lean-startup" ~/.claude/skills/lean-startup
  ```

- **Per-project** — available only inside one project:

  ```bash
  mkdir -p /path/to/your-project/.claude/skills
  ln -s "$(pwd)/book-skills/skills/lean-startup" /path/to/your-project/.claude/skills/lean-startup
  ```

  (Symlinking keeps the skill up to date when you `git pull` this repo. Copying the folder instead works too, it just won't auto-update.)

**3. Repeat step 2 for each skill you want**, or install all of them at once:

```bash
for skill in book-skills/skills/*/; do
  name=$(basename "$skill")
  [ "$name" = "_template" ] && continue
  ln -s "$(pwd)/$skill" ~/.claude/skills/"$name"
done
```

No restart needed — Claude Code picks up skills at the start of a session.

## How triggering works

Claude Code decides whether to use a skill based on its `description` field, matched against what you're asking. You don't need to name the book or the skill — mentioning the book's concepts (e.g. "validated learning," "MVP," "build-measure-learn") is enough. Skills only kick in for tasks substantial enough to benefit from them; simple one-off questions may not trigger one even if related.

## Contributing

Adding a skill for a new book:

1. Copy the template: `cp -r skills/_template skills/<book-slug>`
2. Fill in `SKILL.md`:
   - `description` — list the book's key terms explicitly (not just the title); this is what makes the skill trigger correctly
   - **Core concepts** — 3-8 ideas actually worth applying, not a full book summary
   - **How to apply this** — concrete steps for how Claude should structure its response when the skill fires
3. Test it in a real conversation and tune the description if it doesn't trigger as expected
4. Update the table above and open a PR

Keep each skill focused on what's *actionable* from the book, not exhaustive coverage of it.

## License

[MIT](LICENSE)
