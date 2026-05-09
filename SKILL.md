---
name: ultra-plan
description: Use only when the user explicitly asks for ultra-plan, a multi-agent planning workflow, or detailed planning before implementation.
metadata:
  short-description: Multi-agent planning before coding
---

# ultra-plan

Use this skill to run a planning-first implementation workflow for non-trivial coding tasks.

This skill is intended to be explicit-call only. Do not trigger it merely because a task involves planning. Use it when the user names `ultra-plan`, asks to use the ultra-plan workflow, or explicitly requests this multi-agent planning protocol.

## Core Contract

- Planning comes before implementation.
- Do not modify files, stage changes, commit, or implement code until the user explicitly approves the final plan in chat.
- Chat approval is the only approval signal.
- Use read-only agents for exploration and review.
- Keep review feedback blocker-level and requirement-focused.

## Planning Workflow

1. Spawn parallel read-only exploration agents.
   - Do not fork context.
   - Spawn at most 5 concurrent agents.
   - Each agent prompt must be self-contained and include workspace path, task background, exploration scope, suggested files/directories, read-only constraint, and expected output.
   - Agents must not edit files, stage changes, commit, or run destructive commands.

2. Cover these exploration areas:
   - Existing code and architecture.
   - Files likely requiring modification.
   - Risks, edge cases, dependencies, and regression tests.
   - External/domain research only if current outside information is necessary.

3. Synthesize the findings into a detailed implementation plan.

4. Spawn one additional read-only review agent to critique the plan for blocker-level issues only:
   - unclear scope boundaries,
   - missing acceptance criteria,
   - risky assumptions,
   - unverified dependencies,
   - missing regression tests,
   - likely side effects.

5. Incorporate blocker-level review feedback, then present the final plan and ask for approval before implementation.

## Final Plan Requirements

The final plan must include:

- Implementation strategy summary.
- Ordered list of files to create or modify with exact expected changes.
- Step-by-step execution sequence.
- Testing and verification procedures.
- Risks, mitigations, and open assumptions.
- Clear acceptance criteria.
- Explicit approval question before implementation.

## After Approval

1. Track execution progress.
2. Make only the approved changes.
3. Run agreed validation commands when feasible.
4. If code changes were made, spawn read-only post-change review agents to inspect the git diff and validation results for requirement coverage, regressions, side effects, missed edge cases, and test gaps.
5. Implement blocker-level fixes by default.
6. Report final changes, validation results, residual risks, and follow-up recommendations.
