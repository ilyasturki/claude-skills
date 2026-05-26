---
name: readme
description: Write or refresh a README that earns the reader's attention — short, honest, with a real visual. Tailored to the project type.
---

## User's Prompt

$ARGUMENTS

## Context

- Tree: !`ls -A`
- Manifest: !`cat package.json pyproject.toml Cargo.toml flake.nix go.mod 2>/dev/null | head -60`
- Existing README: !`test -f README.md && wc -l README.md || echo "no README"`

## North star

**A stranger should understand what this is and who it's for in 10 seconds.** That is the README's only real job. Every section earns its place against that goal, or it gets cut.

## Your Task

1. **Deep-analyze the project before deciding anything else.** Do not skim.
   - Read the manifest and the entry point(s): `src/index.*`, `main.*`, `cmd/*`, `bin/*`, `app/page.*`, the binary in `package.json#bin`, etc.
   - Open 2–5 representative source files to confirm what the code actually does (not what it claims to do).
   - Glance at any spec/design doc, CHANGELOG, or recent commits if easy.
   - Write down (to yourself, not the README): a one-sentence answer — *what is this, concretely, and who is it for*. If you can't write it, keep reading until you can. This sentence becomes the README's opening line.

2. **Classify.** Each kind gets a different README shape — do NOT force one template on all.
   - **CLI** — installs a binary, usage is shell commands.
   - **TUI** — interactive terminal app.
   - **Web app** — dev server, visual UI.
   - **Library** — API imported by other code.
   - **Service** — backend, no end-user UI.
   - **Config / dotfiles** — declarative setup.

3. **If a README already exists, audit it against the north star *before* touching it.** In order:
   - Does the first sentence make the project obvious in 10 seconds?
   - Is there a visual? Is it current?
   - Any anti-patterns from the list below?
   - Then decide and tell the user which path you're taking:
     - **leave alone** — already good, nothing to do.
     - **patch** — small surgical edits via Edit (e.g. tighten the opening sentence, refresh a stale screenshot, cut a bloated section).
     - **rewrite** — fundamentally off; start over.

4. **Generate the visual FIRST** (when rewriting, or when there isn't one yet). It's the README's most important line after the opening sentence. Skip only when genuinely not applicable (library, service, dotfiles).
   - **TUI** → write a 5–15s `.tape`, run `vhs`, embed the gif.
   - **CLI** → run a real command, embed the colored output as a fenced block; use `vhs` if animation matters.
   - **Web app** → start the dev server, screenshot the main view (Chrome MCP if loaded, else Playwright via `npx`). Short clip instead if the UI is interactive.
   - **Library** → no image; the smallest possible usage snippet IS the visual.
   - Save under `docs/` or `assets/`. Reference with relative paths.
   - If generation fails (build error, missing tool), write the README without the visual and note it at the end. Don't block.

5. **Write.** Skeleton — drop any section that doesn't earn its place:

````
# name

The sentence from step 1: what it is, who it's for, what makes it worth using. Concrete, no marketing. One sentence — not three.

[visual]

## Install (or Try it)
Shortest path to running it. One command if possible.

## Usage
1–3 examples that show the shape — not a reference.

## [type-specific, only if useful]
CLI: non-obvious flags • Library: API surface • Web app: config/deploy • Service: how to run locally
````

Cap the whole README at ~100 lines. Anything longer goes in `docs/`.

## Anti-patterns — do NOT write these

- An opening that takes 3 sentences to say what the project is.
- "Blazingly fast" / "production-ready" / "robust" / "enterprise-grade" — empty adjectives.
- Feature list of 10+ emoji bullets where half restate each other.
- "Why X?" section that just restates what X is.
- Generic "clone, install, run" steps the reader already knows.
- Auto-generated API tables that dominate the page.
- Badge wall taller than the description.
- Boilerplate "Contributing" / "Code of Conduct" / "Built with ❤️" footers — link out instead.
- Table of contents for a README that fits on one screen.

## Rules

- Deep-analyze first. The opening sentence is the whole README — earn it by understanding the code, not by guessing from the name.
- Read the code before writing. Do not invent features or claim capabilities the code doesn't have.
- Concrete over abstract: *"Converts FFmpeg args to JSON"* beats *"A flexible media toolkit"*.
- If an existing README already passes the north star, leave it alone. Do not rewrite for the sake of rewriting.
- If you rewrite, preserve the existing voice unless it's actively bad.
- If the UI changed, regenerate the visual — never embed a stale screenshot.
- Don't commit. Leave changes in the working tree.
