---
name: lab
description: Use when the user wants to see variations of a visual or interaction thing and pick one, says "lab", "lab this", "6 variations", "sims", "show me options", or when a design choice (animation, entrance, loader, shape, layout) is a matter of taste rather than correctness.
---

# Lab: six ways, the user picks

## Overview
The user decides taste by seeing, not by reading options. Build six live variants side by side on one local page, they pick or mix, the pick ships in one line. The bar is an emotional "wauw" moment, not "works".

## Steps
1. **Pin what varies.** Shape, motion, timing, copy? If it could be two of these, ask once (AskUserQuestion), then go.
2. **Make it pluggable in the real code first.** One hook param (`cross: fn`, `pending: fn`), default = current behaviour, unchanged. Variants call the same helpers the product uses, so the pick ports as-is.
3. **Build `<project>/lab/<thing>.html`.** Copy the nearest existing lab page for layout and CSS.
   - **A = current**, the baseline. **B–F = five truly different ideas**, not tweaks of one.
   - **F (#6) = Claude's pick**: creative liberty, what Claude thinks is fun and what the user would like best. Label it `<b>F · name</b> (Claude's pick): …`.
   - **Vary the feel, not just the idea**: mix hard-cut, smooth and elastic motion across panels so taste has range to pick from.
   - Label each in one line: `<b>B · stamp</b>: what it does`. Short, plain words: the user scans, not reads.
   - Controls, every lab, no exceptions: **loop button, on by default** (repeats forever; show how long one run takes in seconds), **in context** (the full real flow), **fresh input**, **tempo**. Add a control for any real-world variable (wait time, failure).
   - Slow or network steps: fake with timers. Never hit the network, never spend gas.
4. **Build it inline, visibly.** The user wants to watch the edits happen. No background subagent unless they ask for one.
5. **Verify before handing over.** `node` syntax check, headless screenshot with a throwaway profile (`chromium --headless=new --user-data-dir=$(mktemp -d) --virtual-time-budget=… --screenshot=…`), look at it. Then `xdg-open` the lab URL right away, unasked, the moment it is done.
6. **The user picks.** "Combine E and F" = add **G** as a new panel; never overwrite a variant.
   - **Zoom** ("zoom in on the pulsing", "6 more like D"): a new round page (`<thing>2.html`, `3`…). Every variant they did not pick is gone. **A = the pick as it stands**; B–F = five variations *inside* that direction (rhythm, intensity, shape, what answers it), not new directions. Earlier round pages stay on disk as a record.
7. **Ship the pick.** Make it the default via the hook, bump the script `?v=` cache buster, keep the lab page as a record, commit with what was picked and why in the message.

## Common mistakes
| Mistake | Fix |
|---|---|
| Six tweaks of one idea | Five different mechanisms; the variety is the point |
| Lab reimplements product code | Hook in the real file, lab passes functions in |
| No baseline | A is always what exists now |
| Mode switch leaves old runs drawing | Replace canvases (`cloneNode`) on restart |
| Picking for them | Show, then wait. No "I recommend C" unless asked |
