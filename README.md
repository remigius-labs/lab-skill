# lab-skill

A [Claude Code](https://claude.com/claude-code) skill for picking design by seeing it. Say "lab this" and Claude builds six live variants of an animation, loader, shape or layout side by side on one local page. You flick through them and pick one, and the pick ships into the real code.

## Install

```sh
git clone https://github.com/remigius-labs/lab-skill
cp -r lab-skill/lab ~/.claude/skills/lab
```

Claude Code picks it up on the next session.

## How it works

- **A** is what exists now, **B–E** are four different ideas, **F** is Claude's own pick
- Variants mix hard-cut, smooth and elastic motion, so taste has range
- Every lab page has loop, in-context, fresh-input and tempo controls
- "Combine E and F" adds G; "zoom in on D" builds a new round of six inside that direction
- The pick goes live through a hook in the real code; the lab page stays as a record

## Limits

Built for web front ends (HTML, CSS, canvas, JS). Slow or network steps are faked with timers, so a lab never spends gas or calls an API.

## License

MIT
