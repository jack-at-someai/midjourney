# Midjourney Tools

Manual coded tools for accessing and interacting with Midjourney. Built to handle prompt generation, image retrieval, job management, and other Midjourney workflows without relying on third-party wrappers.

## Setup

```
pip install anthropic
setx ANTHROPIC_API_KEY sk-ant-...
```

Both `mj` and `mjlab` are on PATH after install.

## mj — Prompt Builder CLI

Compose structured Midjourney prompts with full parameter support, save reusable templates, generate variations, and auto-copy to clipboard.

```
mj "a cat wearing a top hat" --ar 16:9 --v 6.1
mj "cyberpunk city" --style raw --chaos 50 --stylize 750
mj "a landscape" --no "people, cars" --ar 3:2
mj "portrait" --cref https://example.com/face.jpg --cw 80
mj "a cat" --variations 5 --chaos 10-90
```

### Templates & History

```
mj save cyberpunk "neon city, rain, reflections" --ar 16:9 --style raw
mj --template cyberpunk --subject "a samurai"
mj templates
mj history
```

### All Parameters

`--ar` `--v` `--style` `--stylize` `--chaos` `--weird` `--quality` `--repeat` `--seed` `--stop` `--tile` `--niji` `--cref` `--sref` `--cw` `--sw` `--iw` `--no` `--personalize`

## mjlab — AI-Powered Research Lab Prompt Generator

Feed context files (specs, notes, floor plans) to Claude, which synthesizes an isometric bird's-eye-view Midjourney prompt for a research lab campus in your chosen punk aesthetic. The pipeline: **your files -> Claude -> MJ prompt -> clipboard**.

```
mjlab --files spec.md notes.txt --style solarpunk
mjlab --files *.md --style cyberpunk --acres 5 --focus "quantum wing"
mjlab --style steampunk --acres 2 --describe "biotech lab with clock tower"
mjlab --style biopunk --stylize 800 --chaos 30 --variations 3
mjlab --list-styles
```

### Styles

| Style | Vibe |
|---|---|
| **solarpunk** (default) | Utopian sustainable future, nature + technology harmony |
| **cyberpunk** | Neon dystopian megastructure, dense vertical infrastructure |
| **steampunk** | Victorian-era industrial institute, brass clockwork |
| **biopunk** | Living architecture, genetically engineered building materials |
| **lunarpunk** | Nocturnal mystical sanctuary, moonlit serenity |
| **dieselpunk** | WWII-era industrial complex, brutalist efficiency |
| **atompunk** | 1950s space-age optimism, Googie architecture |

### Flags

| Flag | Default | Description |
|---|---|---|
| `--files` / `-f` | — | Context files (specs, notes). Supports globs. |
| `--style` / `-s` | solarpunk | Punk aesthetic |
| `--acres` / `-a` | 3 | Campus size |
| `--focus` | — | Area to emphasize (e.g. "biotech wing") |
| `--describe` / `-d` | — | Freeform description |
| `--variations` | 1 | Re-roll Claude N times |
| `--save-template` | — | Save result as an `mj` template |
| `--prompt-only` | — | Show Claude's output without piping to `mj` |

Plus all standard MJ params: `--ar`, `--stylize`, `--chaos`, `--seed`, `--tile`.

## Planned

- **Image Retrieval** — Fetch and organize generated images by job ID
- **Job Management** — Track, queue, and manage generation jobs
- **Gallery Viewer** — Local viewer for browsing and comparing outputs
