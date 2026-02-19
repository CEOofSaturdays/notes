# Peter Steinberger — Dev Philosophy Guide

Created: 2026-02-19

A practical distillation from Lex Fridman Podcast #491 + Peter’s posts/interviews.

## Core Philosophy

1. **Agentic engineering > raw vibe coding**
   - Use AI as an active collaborator in loops, not just autocomplete.
   - Let agents run, then review, steer, and correct.

2. **Build from real pain, not hype**
   - Find problems that should obviously exist in solved form.
   - Ship the missing thing.

3. **Fun is a force multiplier**
   - Creative/playful environments can out-iterate “too serious” teams.
   - Weirdness can improve velocity and community pull.

4. **Less tooling, better outcomes**
   - Keep stack minimal and sharp.
   - Too many integrations/tools pollute context and reduce quality.

5. **Context is the scarce resource**
   - Plan for bigger tasks, then execute in clear loops.
   - Protect context quality as a first-class concern.

6. **Human steering is non-negotiable**
   - Don’t fully abdicate.
   - Delegation + verification is the real modern dev skill.

7. **Build infra for both humans and agents**
   - Internal CLIs/admin pages/scaffolding multiply throughput.
   - Don’t just ship features — improve the system that ships features.

8. **Test where risk is high**
   - For meaningful changes, generate/write tests in the same context as the changes.
   - Use tests as drift correction and confidence tooling.

9. **Power requires security discipline**
   - Agent access implies serious threat modeling.
   - Openness and safety must scale together.

10. **Builder identity over empire-building**
    - Prioritize making useful things and shipping impact.
    - Company-building is optional; building is the constant.

## Practical Operating Model (Steinberger-style)

- Pick one real pain point.
- Build a thin working loop immediately.
- Keep toolchain brutally small.
- Run a few agents only where blast radius is controlled.
- Steer aggressively at architecture/schema decisions.
- Add tests for risky diffs.
- Refactor after speed bursts to avoid debt accumulation.
- Preserve fun to sustain intensity.

## Key Tensions to Manage

- **Speed vs. debt:** move fast, then clean up intentionally.
- **Automation vs. control:** autonomy is useful, oversight is mandatory.
- **Breadth vs. context quality:** adding tools can lower effectiveness.
- **Intensity vs. sustainability:** high-output cycles need recovery.

## One-line summary

> Build fast with agents, steer hard with human judgment, keep context clean, simplify tools, and optimize for shipped outcomes over theatre.
