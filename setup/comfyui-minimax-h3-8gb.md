# ComfyUI MiniMax H3 setup for an 8GB workflow

This guide matches the workflows distributed with the video. It documents what was actually tested; it does not claim that every H3 configuration fits every 8GB GPU.

## 1. Install or update ComfyUI

Use a current ComfyUI release and start with the official MiniMax H3 templates:

- Tutorial: https://docs.comfy.org/tutorials/video/minimax/minimax-h3
- ComfyUI: https://www.comfy.org/download
- Official H3 model repository: https://huggingface.co/Comfy-Org/MiniMax-H3
- Official T2V workflow: https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_t2v.json
- Official I2V/first-last-frame workflow: https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_i2v.json
- Official R2V workflow: https://github.com/Comfy-Org/workflow_templates/blob/main/templates/video_minimax_h3_r2v.json

## 2. Install the tested model files

See [plugin-and-model-manifest.md](plugin-and-model-manifest.md) for exact names, links, and folders.

Required categories:

- H3 INT8 diffusion model for the workflow mode;
- Qwen3-VL H3 text encoder;
- H3 video VAE;
- H3 audio VAE;
- optional H3 Turbo LoRA and Turbo custom node.

## 3. Import the smallest workflow first

Import:

`../workflows/01-first-h3-test-exact.json`

This exact first test used:

- 736×416;
- 243 frames at 24 fps;
- 20 steps;
- `simple` scheduler;
- no Turbo node;
- native video and audio.

Replace unavailable input/output filenames and queue one short job. Confirm the output MP4 contains both video and audio before adding complexity.

## 4. Add Turbo

Install the Turbo node from:

https://github.com/Larryvrh/ComfyUI-MiniMax-H3-Turbo

Install a compatible LoRA from:

https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora

The Roman and Last Garden drafts used six Turbo steps. The final opening-film segments used eight steps.

## 5. Add references only when needed

- REF2VA: use for recurring identity, wardrobe, object, environment, motion, or audio references.
- I2V/FL2VA: use approved first/last frames for exact boundaries and transformations.
- Replace private reference filenames with your own files; see [reference-inputs.md](../examples/reference-inputs.md).

## 6. Tested settings

### Fast draft baseline

- 736×416
- 24 fps
- 362 frames, about 15 seconds
- Turbo strength 1.0
- six steps
- three character references in The Last Garden
- generated stereo audio

### Higher-quality segmented production

- 1280×736 native generation
- 24 fps
- 124 frames, about five seconds per segment
- Turbo v4 step-600 EMA
- eight steps
- `low_vram=true` on transformation segments
- approved final frame handed to the next segment

1280×736 was the largest native production resolution successfully used here. A reliable native 1920×1080 generation workflow was not proven on the 8GB card. The final 1920×1080 file is the Remotion/YouTube delivery master.

## 7. Validate every result

- decode with `ffmpeg`/`ffprobe`;
- review real-time playback;
- inspect duplicate people and object drift;
- transcribe every spoken line;
- audition music and ambience across cuts;
- preserve exact workflow JSON, prompt, seed, references, and settings.

Use the included [QC checklist](../examples/qc-checklist.md) and [shot manifest](../skill/minimax-h3-short-film/templates/shot-manifest.yaml).