# Open Canvas

Keep every decision a project makes, where the whole team can see it.

Open Canvas is a Mac app plus a small command, `canvas`, that your coding agents (Claude Code, Codex) use. While you work, your agent records the big decisions as they're made: direction, scope, audience, platform, design language, and what got dropped. They go into your repository under `.canvas/`, so everyone gets them with `git pull`, and the app shows them as a board you can read, accept and build on.

The agent does the recording. You see what happened in the app, and only a person accepts a decision.

## Install

1. Download **Open Canvas** from [Releases](../../releases) and drag it to Applications.
2. Ask your agent to set itself up:

   > Run `"/Applications/Open Canvas.app/Contents/Helpers/canvas" setup`

   This installs the `open-canvas` and `canvas-explorer` skills for Claude Code (`~/.claude/skills`) and Codex (`~/.codex/skills`), and puts `canvas` on your PATH.
3. In a project's repository, ask your agent: "Set up Open Canvas here." It runs `canvas init`.

Only want the command? Each release also has `canvas-<version>-macos.zip` (signed and notarised) and the skills on their own. The skills are also in [`skills/`](skills).

## How a project's record works

`canvas init` creates:

```
.canvas/
  canvas.json        names the project
  events/            the record: one small file per decision, comment, acceptance or dismissal
  decisions/         a readable page per accepted decision, and an index of drafts waiting
  README.md
```

and adds a short note to `AGENTS.md` (and `CLAUDE.md` if you have one) so every agent knows to record decisions. It never commits; you review and commit it like any other change.

- **Nothing to merge.** Every event is its own file, written once and never edited, so two people recording at the same time never conflict.
- **Drafts until accepted.** An agent's decision arrives as a draft. A person accepts it in the app, and that acceptance is recorded too.
- **Private stays private.** Your chats, library, attachments and anything nobody accepted stay on your Mac. Only what you share goes in `.canvas/`.
- **Readable without the app.** Browse `.canvas/decisions/` on GitHub, or run `canvas decisions` in a terminal.

## Projects that already exist

Ask your agent to catch the project up. It runs `canvas init`, reads the history (README, docs, `git log`, design notes, and your chats if the project is in Open Canvas), and records the decisions that shaped it with their dates, as drafts for you to accept.

## The command

```sh
canvas decided --title "Lead with the work" --decision "The home page opens on case studies." --why "People skim for work first."
canvas decisions                 # accepted decisions, drafts waiting, open suggestions
canvas board                     # everything in time order
canvas show CARD                 # one card, what it builds on, its comments
canvas direction --from CARD --title T --body B
canvas comment --card CARD --text T
canvas init                      # start a repository's record
canvas setup                     # install the skills for your agents
canvas --help
```

Who recorded something comes from `git config user.name`, with the agent noted alongside. Names are self-declared, not verified accounts.

## Requirements

macOS 14 or later. Claude Code or Codex for the agent side.

## Feedback

Open an issue in this repository.
