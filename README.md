# ultra-plan

`ultra-plan` is a Codex skill for planning-first coding work. It helps Codex create an implementation plan before making code changes, using multi-agent exploration and review when appropriate.

## Install

Install it as a user-level Codex skill:

```bash
uv run python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo JettHu/ultra-plan \
  --path . \
  --name ultra-plan
```

Restart Codex after installation so the skill is loaded.

## Use

Invoke it explicitly:

```text
Use $ultra-plan to create a detailed implementation plan before coding.
```
