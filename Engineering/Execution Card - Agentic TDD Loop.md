# Execution Card - Agentic TDD Loop

Use this card at the start of any agent project.

## 1) Define Outcome (2-3 lines)
- Problem:
- Desired outcome:
- Non-goals:

## 2) Slice the Work
- Break into atomic steps (each step solvable in one focused pass).
- For each step, define:
  - **Input contract**
  - **Output contract**
  - **Definition of Done**

## 3) Tests Before Build
For each step, write tests first:
- Happy path
- Edge cases
- Adversarial/failure cases
- Idempotency/retry behavior (if relevant)

## 4) Run Step Loop (TDD)
1. Implement **Step N only**
2. Run tests for Step N
3. If fail: diagnose → smallest fix → re-test
4. If pass: commit and move to next step

## 5) Control Risk
- Approval-gate external/irreversible actions
- Least privilege for tools and data
- Log every action with correlation ID

## 6) Integrate + Regress
- Run full regression suite
- Validate end-to-end result is explainable
- Confirm audit trail is complete

## 7) Capture Learnings
- Record failure modes
- Record fixes that worked
- Add new fixtures to prevent repeat failures

---

## Prompt Template (copy/paste)
```text
Implement Step {N}: {Step Name}
Goal: {single outcome}
Inputs: {schema + sample}
Constraints: Do not modify other steps
Definition of Done:
- {test 1}
- {test 2}
- {test 3}
Return:
1) What you changed
2) Test results (pass/fail)
3) Known limits
4) Next minimal improvement
```

---

## Quick Red Flags
- “Do everything” prompt
- No pass/fail tests
- Changing multiple steps at once
- No logs/evidence for decisions
- Automating actions without approval boundaries

## Quality Gate (must be all ✅)
- [ ] Every step has tests
- [ ] Step outputs match contracts
- [ ] Regression suite green
- [ ] Decision trace is explainable
- [ ] Risk controls active
