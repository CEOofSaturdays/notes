# Coding Agent Process Guide

A practical operating guide for using coding agents to ship reliable software fast.

## Objective
Use coding agents for execution speed **without sacrificing correctness, security, or maintainability**.

---

## 1) Start with a tight brief
Before prompting the agent, define:
- **Problem statement** (what is broken / missing)
- **Outcome** (what “done” looks like)
- **Scope boundaries** (what not to touch)
- **Constraints** (language, frameworks, style, latency, cost)

### Brief template
```text
Task: {what to build/fix}
Outcome: {observable result}
In scope: {files/components}
Out of scope: {explicit exclusions}
Constraints: {tech + policy + perf}
```

---

## 2) Force stepwise execution
Never ask a coding agent to “build everything.”

Break into small steps:
1. Understand codebase + locate touchpoints
2. Propose plan
3. Implement Step N only
4. Run tests/lint/type checks
5. Review diff and risks
6. Repeat

---

## 3) Require tests before trust
For each step, define tests first:
- Unit tests for logic
- Integration tests for interfaces
- Regression tests for previously fixed bugs
- Failure-path tests (timeouts, nulls, malformed input)

If tests are weak, output quality will be weak.

---

## 4) Use a strict prompting contract

```text
Implement Step {N}: {name}
Goal: {single step outcome}
Inputs: {context + file paths}
Constraints:
- Do not modify files outside {allowed paths}
- Keep public APIs unchanged unless specified
- Add/update tests for behavior changes
Definition of Done:
- {test criteria 1}
- {test criteria 2}
Return:
1) Summary of changes
2) Files changed
3) Test results
4) Remaining risks
```

---

## 5) Verify every iteration
After each step:
- Run tests
- Run lint + type checks
- Check diff size and blast radius
- Confirm no secrets/tokens added
- Confirm no unintended dependency changes

### Command checklist (example)
```bash
npm test
npm run lint
npm run typecheck
git diff --stat
```

---

## 6) Control risk and permissions
- Use least privilege for tools and credentials
- Gate external side effects (emails, payments, prod writes)
- Prefer dry-run modes first
- Keep rollback path clear

**Rule:** if a step is irreversible, require explicit approval.

---

## 7) Handle failures with a loop, not guesswork
When tests fail:
1. Capture exact failure
2. Form 1-3 hypotheses
3. Change one variable
4. Re-run affected tests
5. Promote fix only when stable

Avoid random multi-change retries.

---

## 8) Integration and release discipline
Before merging:
- Full regression pass
- Changelog/update notes
- Performance sanity check
- Security sanity check
- Observability hooks in place (logs/metrics)

After release:
- Monitor for regressions
- Capture lessons into playbook
- Add fixtures for new edge cases

---

## 9) Anti-patterns (do not do)
- “Here’s the repo, improve it” prompts
- Merging large unreviewed agent diffs
- Skipping tests because output “looks right”
- Allowing unrestricted file writes
- No audit trail of what changed and why

---

## 10) Definition of high-quality agent-assisted engineering
A coding-agent workflow is high quality when it is:
- **Deterministic** (repeatable outcomes)
- **Observable** (clear logs and evidence)
- **Tested** (green, meaningful test suite)
- **Scoped** (small controlled changes)
- **Recoverable** (safe rollback path)
- **Secure** (least privilege + explicit approvals)

---

## Quick one-page runbook
1. Write brief
2. Slice steps
3. Define tests
4. Prompt one step
5. Run checks
6. Review diff
7. Merge small
8. Monitor + learn

