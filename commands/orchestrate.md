---
description: Run a larger task across worker subagents via the orchestrator (decompose, delegate, verify, aggregate).
argument-hint: "[goal]"
allowed-tools: Agent, TodoWrite, Read, Grep, Glob
---

# Orchestrate

Delegate this goal to the `orchestrator` subagent, which will decompose it into
subtasks, dispatch them to worker subagents (implementer / tester / reviewer), verify
each result against its acceptance criteria, and report back.

**Goal:** $ARGUMENTS

Hand the goal to the orchestrator now. Do not implement it yourself.
