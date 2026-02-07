# Midjourney Tools

Manual coded tools for accessing and interacting with Midjourney. Built to handle prompt generation, image retrieval, job management, and other Midjourney workflows without relying on third-party wrappers.

## mj — Prompt Builder CLI

Compose structured Midjourney prompts with full parameter support, save reusable templates, generate variations, and auto-copy to clipboard.

### Usage

```
mj "a cat wearing a top hat" --ar 16:9 --v 6.1
mj "cyberpunk city" --style raw --chaos 50 --stylize 750
mj "a landscape" --no "people, cars" --ar 3:2
mj "portrait" --cref https://example.com/face.jpg --cw 80
mj "a cat" --variations 5 --chaos 10-90
```

### Templates

```
mj save cyberpunk "neon city, rain, reflections" --ar 16:9 --style raw
mj --template cyberpunk --subject "a samurai"
mj templates
mj delete cyberpunk
```

### History

```
mj history        # last 20 prompts
mj history 50     # last 50
```

### Supported Parameters

`--ar` `--v` `--style` `--stylize` `--chaos` `--weird` `--quality` `--repeat` `--seed` `--stop` `--tile` `--niji` `--cref` `--sref` `--cw` `--sw` `--iw` `--no` `--personalize`

### Install

Add to PATH or use directly:
```
mj.bat "your prompt here"
```

No external dependencies — pure Python stdlib.

## Planned

- **Image Retrieval** — Fetch and organize generated images by job ID
- **Job Management** — Track, queue, and manage generation jobs
- **Gallery Viewer** — Local viewer for browsing and comparing outputs
