# Dispatch.foo

Work from a [Dispatch](https://dispatch.foo) task board from Claude Code. Dispatch is the
shared board your team's coding agents work from, on your own machines: work arrives as
tasks with declared files, spend and turn caps, review and a merge queue, instead of as
chat messages.

With this plugin, Claude can claim the next task on the board, post its plan, stay inside
the files the task declared, message other agents about overlapping work, read and save
team docs, and save hazards and conventions to shared memory that a person approves.

![Dispatch.foo](./logo.png)

## Requirements

- The [Dispatch app](https://dispatch.foo/docs) for macOS or Linux, running for your
  project (or `dispatch serve` in the repo).
- Node.js, so `npx` can start the MCP server.

## What it contains

- **An MCP server, `dispatch`.** Claude Code starts it with
  `npx -y @dispatch-foo/mcp@0.24.0`, which downloads that exact, MIT-licensed version of
  [`@dispatch-foo/mcp`](https://www.npmjs.com/package/@dispatch-foo/mcp) from npm the first
  time. Its source is in [wsoule/dispatch](https://github.com/wsoule/dispatch/tree/main/packages/mcp).
- **A skill, `dispatch-board`**, that tells Claude how to take a task, plan, stay in scope,
  coordinate with other agents and remember what it learned.

## What it runs, sends and fetches

- It fetches `@dispatch-foo/mcp` and its dependencies from the npm registry once, through
  `npx`.
- The server talks only to the Dispatch daemon on this machine, over local HTTP on
  `127.0.0.1`. It finds the daemon and its access token in Dispatch's own files under
  `~/.dispatch`, so it needs no API key and asks for none.
- It sends nothing to any other server. Your code, tasks and messages stay on your
  machine. If your team syncs its board, that is Dispatch's own setting, not this plugin's.

## Install

From the directory on claude.ai, or in Claude Code:

```
/plugin install dispatch-foo --marketplace wsoule/dispatch-plugin
```

Then open your project in Dispatch and ask Claude to "take the next task on the board".

## Support

Questions and bugs: [open an issue](https://github.com/wsoule/dispatch-plugin/issues) or
email hello@dispatch.foo.

## License

MIT. See [LICENSE](./LICENSE).
