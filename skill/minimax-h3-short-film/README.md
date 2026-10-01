# Installing the MiniMax H3 short-film skill

This folder is a self-contained Hermes skill package.

## Files

- `SKILL.md` — production procedure, continuity rules, recovery logic, dialogue checks, and final QC
- `templates/shot-manifest.yaml` — reusable boundary-aware film manifest

## Install

Copy the complete `minimax-h3-short-film` folder into your Hermes skills directory, preserving the folder structure. A typical local layout is:

```text
~/.hermes/skills/minimax-h3-short-film/
├── SKILL.md
└── templates/
    └── shot-manifest.yaml
```

Start a new Hermes session or reload skills after copying it.

The skill assumes access to ComfyUI, API-format H3 workflows, `ffmpeg`, and `ffprobe`. Update workflow paths, reference inputs, and model filenames for your own environment.

## Safety and privacy

Do not publish private hostnames, API credentials, identity reference images, or voice samples. The example workflows in this repository include input filenames but omit the underlying private media.