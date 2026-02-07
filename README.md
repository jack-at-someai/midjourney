# Midjourney Tools

Manual coded tools for accessing and interacting with Midjourney. Built to handle prompt generation, image retrieval, job management, and other Midjourney workflows without relying on third-party wrappers.

## Setup

### 1. Install dependency

```
pip install anthropic
```

### 2. Get your Anthropic API key

1. Go to [console.anthropic.com](https://console.anthropic.com/)
2. Sign up or log in
3. Navigate to **API Keys** in the left sidebar (or go directly to [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys))
4. Click **Create Key**, give it a name like "midjourney-tools"
5. Copy the key (starts with `sk-ant-api03-...`)

### 3. Set the key permanently

```
setx ANTHROPIC_API_KEY sk-ant-api03-your-key-here
```

Then **restart your terminal** so the env var takes effect.

### 4. Verify

```
mj "test prompt" --ar 1:1
mjlab --style solarpunk --describe "small greenhouse lab" --prompt-only
```

Both `mj` and `mjlab` are on PATH.

---

## The Pipeline

The core idea: funnel all your references, context, and ideas through one command that produces a ready-to-paste Midjourney prompt.

```
                                    +------------------+
  your files ----+                  |                  |
  (specs, notes, |                  |     Claude       |
   floor plans,  +---> mjlab -----> | (synthesizes an  |----> /imagine prompt: ...
   research docs)|       |         |  isometric MJ    |        (copied to clipboard,
                 |       |         |  prompt from      |         paste into Discord)
  --style        +-------+         |  your context)   |
  --acres                          |                  |
  --focus                          +------------------+
  --describe
```

**Step by step:**
1. You point `mjlab` at your files and pick a style
2. Claude reads everything and generates a detailed isometric lab prompt
3. The prompt gets piped through `mj` which injects `--ar`, `--stylize`, `--v`, etc.
4. The final `/imagine prompt: ...` is copied to your clipboard
5. Paste into Midjourney on Discord

---

## mj -- Prompt Builder CLI

Compose structured Midjourney prompts with full parameter support, save reusable templates, generate variations, and auto-copy to clipboard.

### Quick Examples

```bash
# Basic prompt with params -- builds and copies to clipboard
mj "a cat wearing a top hat" --ar 16:9 --v 6.1

# Style raw + high stylize for artistic output
mj "cyberpunk city at night" --style raw --chaos 50 --stylize 750

# Negative prompt to exclude things
mj "serene mountain landscape" --no "people, cars, buildings" --ar 3:2

# Character reference from a URL
mj "portrait of a warrior" --cref https://example.com/face.jpg --cw 80

# Generate 5 variations with chaos sweep from 10 to 90
mj "a cat in a garden" --variations 5 --chaos 10-90
```

### Templates & History

```bash
# Save a reusable template
mj save cyberpunk "neon city, rain, reflections, volumetric lighting" --ar 16:9 --style raw --stylize 750

# Use it with a new subject injected
mj --template cyberpunk --subject "a samurai on a motorcycle"

# List all saved templates
mj templates

# See your last 20 prompts
mj history

# Delete a template
mj delete cyberpunk
```

### All Parameters

`--ar` `--v` `--style` `--stylize` `--chaos` `--weird` `--quality` `--repeat` `--seed` `--stop` `--tile` `--niji` `--cref` `--sref` `--cw` `--sw` `--iw` `--no` `--personalize`

---

## mjlab -- AI-Powered Research Lab Prompt Generator

Feed context files (specs, notes, floor plans) to Claude, which synthesizes an isometric bird's-eye-view Midjourney prompt for a research lab campus in your chosen punk aesthetic.

### Quick Examples

```bash
# Solarpunk lab from a description (no files needed)
mjlab --style solarpunk --describe "quantum computing lab with rooftop greenhouses and a central courtyard"

# Feed it your actual spec files
mjlab --files lab-spec.md budget.md floor-plan.txt --style solarpunk --acres 5

# Cyberpunk, 10-acre campus, emphasize a specific wing
mjlab --files *.md --style cyberpunk --acres 10 --focus "AI research wing"

# Generate 3 different takes and bump up the stylize
mjlab --files notes.md --style biopunk --variations 3 --stylize 800 --chaos 30

# Just see what Claude generates without piping to mj
mjlab --style steampunk --describe "clockwork biotech lab" --prompt-only

# Save the result as a reusable mj template for later
mjlab --files spec.md --style solarpunk --save-template my-lab

# List all available punk styles
mjlab --list-styles
```

### Styles

| Style | Vibe |
|---|---|
| **solarpunk** (default) | Utopian sustainable future, nature + technology harmony, golden light, living walls |
| **cyberpunk** | Neon dystopian megastructure, dense vertical infrastructure, chrome and holographics |
| **steampunk** | Victorian-era industrial institute, ornate brass clockwork, gas lamps |
| **biopunk** | Living architecture, genetically engineered materials, organic growth patterns |
| **lunarpunk** | Nocturnal mystical sanctuary, moonlit serenity, iridescent pearl surfaces |
| **dieselpunk** | WWII-era industrial complex, brutalist efficiency, riveted steel plate |
| **atompunk** | 1950s space-age optimism, Googie architecture, chrome and pastels |

### All Flags

| Flag | Default | Description |
|---|---|---|
| `--files` / `-f` | -- | Context files (specs, notes, plans). Supports globs. |
| `--style` / `-s` | solarpunk | Punk aesthetic |
| `--acres` / `-a` | 3 | Campus size in acres |
| `--focus` | -- | Area to emphasize (e.g. "biotech wing") |
| `--describe` / `-d` | -- | Freeform description (use instead of or alongside files) |
| `--variations` | 1 | Re-roll Claude N times for different takes |
| `--save-template` | -- | Save the result as a reusable `mj` template |
| `--prompt-only` | -- | Show Claude's output without piping to `mj` |
| `--raw` | -- | Print bare prompt text only |
| `--model` | claude-sonnet-4-5 | Claude model to use |
| `--no-copy` | -- | Don't auto-copy to clipboard |

Plus all standard MJ params: `--ar`, `--v`, `--stylize`, `--chaos`, `--seed`, `--tile`.

---

## Planned

- **Image Retrieval** -- Fetch and organize generated images by job ID
- **Job Management** -- Track, queue, and manage generation jobs
- **Gallery Viewer** -- Local viewer for browsing and comparing outputs
