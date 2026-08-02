---
name: ai-modern-approach
description: Applies the framework from Stuart Russell & Peter Norvig's "Artificial Intelligence: A Modern Approach" (AIMA) — the rational-agent model (PEAS, environment properties), search (uninformed, informed/heuristic A*, adversarial minimax/alpha-beta), constraint satisfaction, knowledge representation and logical inference, reasoning under uncertainty (Bayesian networks, Markov models), and Markov Decision Processes / reinforcement learning — to problems that involve designing an agent, choosing a search or planning algorithm, modeling uncertainty, or picking the right AI technique for a task. Use whenever the user wants an "AI: a modern approach" or "AIMA" lens, mentions "rational agent," "PEAS," "heuristic search," "A* search," "minimax," "alpha-beta pruning," "constraint satisfaction," "Bayesian network," "Markov decision process," or is deciding which class of algorithm/approach fits an AI or search/optimization problem — even if they don't name the book.
---

# Artificial Intelligence: A Modern Approach

Apply this skill when the user is designing an intelligent agent, choosing between search/planning/reasoning techniques, or modeling a decision problem under uncertainty — use AIMA's agent-and-environment framing to pick the right class of solution instead of jumping straight to an algorithm.

## Core concepts

**Rational agent & PEAS** — Frame any agent-design problem by its Performance measure (what defines success), Environment, Actuators (what it can do), and Sensors (what it can perceive). A "rational" agent is one that, given what it has perceived, acts to maximize expected performance — not one that's guaranteed correct or omniscient. When the user is designing an agent/bot/pipeline, start by making PEAS explicit; vague agent designs usually trace back to a vague performance measure.

**Environment properties** — Classify the environment before picking an approach: fully vs. partially observable, deterministic vs. stochastic, episodic vs. sequential, static vs. dynamic, discrete vs. continuous, single- vs. multi-agent. These properties directly determine which technique class is even appropriate (e.g. classical search assumes deterministic/fully-observable; POMDPs and RL exist because that assumption breaks).

**Agent architectures** — Match the agent's internal structure to what the task needs: simple reflex (condition-action rules, no memory), model-based reflex (tracks internal state to handle partial observability), goal-based (searches/plans toward an explicit goal), utility-based (optimizes a scalar utility, not just a boolean goal — needed when there are tradeoffs between outcomes), and learning agents (improve performance from experience). Don't default to the most complex architecture — pick the simplest one that satisfies the performance measure.

**Uninformed vs. informed search** — For deterministic, discrete problems reducible to search: uninformed search (BFS, DFS, uniform-cost) explores blindly and guarantees correctness but scales poorly; informed/heuristic search (greedy best-first, A*) uses a heuristic to guide exploration efficiently. A* is optimal only if the heuristic is admissible (never overestimates true cost) — and efficient if it's also consistent. When proposing a heuristic, check whether it's actually admissible, not just "reasonable-sounding."

**Adversarial search (game theory)** — For sequential, multi-agent, zero-sum-ish settings, use minimax (assume the opponent plays optimally against you) with alpha-beta pruning to cut the search space without changing the result. For large game trees, evaluation functions approximate deep search with heuristics at a cutoff depth — flag the accuracy/speed tradeoff this introduces.

**Constraint Satisfaction Problems (CSPs)** — When a problem is really "assign values to variables subject to constraints" (scheduling, resource allocation, configuration) rather than a path-finding problem, model it as a CSP: variables, domains, constraints. Techniques like backtracking + constraint propagation (arc consistency) usually beat generic search for these — recognizing a problem as a CSP in disguise is often the highest-leverage move.

**Knowledge representation & logical inference** — For problems needing explicit facts and rules (not just pattern-matching), propositional logic is simple but limited; first-order logic adds objects, relations, and quantifiers for expressive but harder-to-automate reasoning. Inference approaches (forward/backward chaining, resolution) trade completeness against efficiency — pick based on whether the domain needs guaranteed-correct conclusions or fast plausible ones.

**Reasoning under uncertainty** — When the environment is stochastic or only partially observable, prefer probabilistic models over brittle rule-based logic. Bayesian networks compactly represent conditional dependencies between variables and support inference about unseen variables given evidence. Hidden Markov Models / Kalman filters handle uncertainty that evolves over time (tracking, sequential state estimation).

**Markov Decision Processes & reinforcement learning** — For sequential decision-making under uncertainty where the agent gets rewards over time, model as an MDP (states, actions, transition probabilities, rewards) and solve for a policy (value iteration, policy iteration) when the model is known. When the transition/reward model isn't known in advance, that's the reinforcement-learning regime — the agent must learn a policy from experience, trading off exploration vs. exploitation.

## How to apply this

1. **Start from PEAS** when the user is designing an agent — force the performance measure and environment to be explicit before discussing algorithms.
2. **Classify the environment** (observable? deterministic? episodic? discrete? single-agent?) — this narrows the viable technique family fast and prevents applying classical search to a problem that actually needs POMDPs/RL, or vice versa.
3. **Check if the problem is secretly a CSP** before reaching for general search — scheduling/allocation/configuration problems usually are, and CSP techniques are far more efficient.
4. **For search/planning problems**, recommend uninformed vs. informed vs. adversarial search based on the structure (single-agent path problem vs. two-player zero-sum), and sanity-check any proposed heuristic for admissibility.
5. **For uncertainty**, prefer a probabilistic model (Bayesian network, HMM) over ad hoc rules when the domain is genuinely stochastic or evidence-based.
6. **For sequential decisions under uncertainty with rewards**, frame it as an MDP; only reach for RL if the transition/reward model truly isn't known ahead of time (otherwise planning on a known MDP is simpler and more reliable).

Keep this grounded in the user's actual system/problem — apply the relevant piece(s) of the framework, don't lecture through the whole book's taxonomy every time.
