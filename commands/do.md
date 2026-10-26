---
description: Run a goal across the company — the coordinator routes it to the right department agents, verifies results, and holds anything outbound as a draft for you to send.
argument-hint: "[goal]"
allowed-tools: Agent, TodoWrite, Read, Grep, Glob
---

# Do

Delegate this goal to the `coordinator` subagent, which will decide which departments
(engineering / research / content / data) to involve, delegate to them, verify each
result against its acceptance criteria, and aggregate — stopping at a human approval
gate before any outward action.

**Goal:** $ARGUMENTS

Hand the goal to the coordinator now. Do not do the work yourself.
