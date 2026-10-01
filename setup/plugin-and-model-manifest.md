# Plugin and model manifest

## ComfyUI and H3 nodes

Use a current ComfyUI release with the official MiniMax H3 workflow templates.

Expected H3 node types in the supplied workflows include:

- `MiniMaxH3ImageToVideo`
- `MiniMaxH3ReferenceToVideo`
- H3 video/audio encoding and decoding nodes supplied by the current template/node implementation
- standard ComfyUI model, CLIP, VAE, sampler, scheduler, video, image, and audio nodes

Official documentation and templates:

- https://docs.comfy.org/tutorials/video/minimax/minimax-h3
- https://github.com/Comfy-Org/workflow_templates/tree/main/templates

## Diffusion models

Store in `ComfyUI/models/diffusion_models/`.

### FL2VA / image and boundary workflows

`minimax_h3_fl2va_pruned_int8_convrot.safetensors`

https://huggingface.co/Comfy-Org/MiniMax-H3/blob/main/diffusion_models/minimax_h3_fl2va_pruned_int8_convrot.safetensors

### REF2VA workflows

`minimax_h3_ref2va_pruned_int8_convrot.safetensors`

https://huggingface.co/Comfy-Org/MiniMax-H3/blob/main/diffusion_models/minimax_h3_ref2va_pruned_int8_convrot.safetensors

## Text encoder

Store in `ComfyUI/models/text_encoders/`.

`qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors`

https://huggingface.co/Comfy-Org/MiniMax-H3/blob/main/text_encoders/qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors

## VAEs

Store both in `ComfyUI/models/vae/`.

`minimax_h3_video_vae_fp16.safetensors`

https://huggingface.co/Comfy-Org/MiniMax-H3/blob/main/vae/minimax_h3_video_vae_fp16.safetensors

`minimax_h3_audio_vae_fp32.safetensors`

https://huggingface.co/Comfy-Org/MiniMax-H3/blob/main/vae/minimax_h3_audio_vae_fp32.safetensors

## Turbo extension

Custom node:

https://github.com/Larryvrh/ComfyUI-MiniMax-H3-Turbo

Clone it into `ComfyUI/custom_nodes/`, install its requirements if requested, and restart ComfyUI.

Turbo LoRA repository:

https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora

Tested filename:

`minimax_h3_turbo_v4_step600_ema.safetensors`

Store the LoRA where the installed Turbo node expects ComfyUI LoRA weights, normally `ComfyUI/models/loras/`.

Expected Turbo nodes:

- `MiniMaxH3TurboLoRA`
- `MiniMaxH3TurboSampler`

## Notes

Workflow JSON files preserve the exact model filenames used during production. If an upstream repository changes naming or folder conventions, follow the current official documentation and update the loader nodes rather than renaming files blindly.