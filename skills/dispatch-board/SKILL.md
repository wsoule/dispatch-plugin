---
name: dispatch-board
description: Use when the project is tracked on a Dispatch task board (a .dispatch/ folder in the repo, or the user mentions Dispatch, the board, a task id like t-1a2b3c, or a milestone like e-1a2b3c). Covers claiming work, posting a plan, staying inside the task's declared files, messaging other agents, and saving lessons to shared memory with the dispatch MCP tools.
---

# Working from a Dispatch board

Dispatch is a task board that people and coding agents share. Work arrives as
tasks, not chat messages: each task has a title, a description, acceptance
criteria, the files it may write, and the tasks it waits on. The `dispatch`
MCP server from this plugin reads and writes that board through the Dispatch
app running on this machine.

## Before you start

The Dispatch app (or `dispatch serve`) must be running for this project. If a
dispatch tool reports that it can't reach the daemon, tell the user to open
the project in Dispatch, then stop. Don't create a `.dispatch/` folder
yourself; `dispatch init` does that.

## Taking work

1. Call `task_next` to see the ready task at the top of the queue. If the user
   named a task id, call `task_get` with it instead.
2. Read the whole task with `task_get`: its description, acceptance criteria,
   `writes` (the files it may change) and `blockedBy`. Don't start a task whose
   blockers aren't finished.
3. Claim it with `task_save` (set yourself as assignee) so no other agent picks
   it up.
4. Post a short plan with `task_comment` before editing anything: what you'll
   change, and how you'll check each acceptance criterion.

## While you work

- Change only the files in the task's `writes`. If you need another file, say
  so in a `task_comment` and ask the user; don't widen the scope on your own.
- If you have a question only a person can answer, ask it in a
  `task_comment` and wait, rather than guessing.
- Another agent may own related work. Use `agent_list` to see who is active,
  `msg_send` to tell them about an overlap before it becomes a conflict, and
  `inbox_read` to pick up messages addressed to you.
- Use `run_list` to see what is already running, so you don't duplicate it.

## Remembering

When you learn something the next agent will need (a hazard, a convention, a
decision), save it with `memory_save`. Use `scope: "team"` for project facts
and keep each entry to one fact. Search first with `memory_search` so you
don't save a duplicate. Team memories wait for a person to approve them, and
a new agent's first save may wait for approval too; that's expected.

## Finishing

Finish with a `task_comment` that says what changed, how each acceptance
criterion was checked, and anything left over. Don't mark the task landed
yourself: a person reviews the work and lands it through Dispatch's merge
queue.

## Docs

Specs and plans live as Dispatch docs. Read the ones linked to your task with
`doc_read`, find others with `doc_search` or `doc_list`, and save a plan with
`doc_save`, linking it to the task.
