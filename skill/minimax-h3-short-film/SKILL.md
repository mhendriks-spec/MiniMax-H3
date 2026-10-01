---
name: minimax-h3-short-film
description: Build coherent MiniMax H3 short films with continuity.
version: 0.1.0
author: Walter, Hermes Agent
license: MIT
platforms: [linux, windows]
metadata:
  hermes:
    tags: [minimax-h3, comfyui, short-film, video, continuity]
    related_skills: [comfyui, youtube-video-production]
---

# MiniMax H3 Short Film

Build a multi-shot MiniMax H3 film through ComfyUI while preserving characters, props, movement, dialogue, audio, and edit continuity. Treat isolated visual quality and whole-film coherence as separate engineering problems.

## When to Use

Use when:

- planning or generating a narrative MiniMax H3 film with multiple shots;
- using H3 REF2VA, FL2VA, Turbo LoRA, or Turbo Sampler workflows;
- resuming a long H3 render after a client, network, DNS, or sleep interruption;
- comparing H3 resolutions, samplers, LoRAs, or step counts;
- preparing an evidence-led YouTube video about the production.

Do not use for a single disposable clip where continuity, dialogue, and reproducibility do not matter.

## Prerequisites

- A reachable ComfyUI server with the required H3 nodes and models.
- API-format workflow JSON.
- `ffmpeg` and `ffprobe` for assembly and technical verification.
- Enough storage for references, per-shot workflows, raw clips, proxies, audio, and finals.
- A project directory containing all manifests and outputs.

Before rendering, inspect ComfyUI `/object_info` and first-party model/node documentation. Do not infer exact LoRA, Turbo, scheduler, step, resolution, or frame-count behavior from generic diffusion knowledge.

## Baseline Learned from the First Film

The proven fast draft baseline was:

- MiniMax H3 REF2VA INT8 model;
- H3 Turbo v4 step-600 EMA LoRA;
- MiniMax H3 Turbo Sampler;
- 6 sampling steps;
- 736×416 pixels;
- 362 frames at 24 fps, about 15 seconds;
- three character reference images;
- generated stereo dialogue, effects, and music inside each shot.

This is a baseline, not a universal optimum. Preserve exact filenames and node parameters from the installed workflow rather than guessing them.

## Mandatory Continuity Rules

A film plan is incomplete until all six rules below are explicitly addressed.

### 1. Hand off the previous shot's final frame

- Extract a clean end-frame candidate from every approved shot.
- Use that frame as the next shot's opening visual reference when the installed H3 workflow supports it.
- Prefer an appropriate FL2VA or image-conditioned workflow for boundary continuity; verify the exact installed node inputs first.
- If direct frame conditioning is unavailable, create a boundary reference image and describe matching camera position, pose, lighting, object placement, and motion direction in the next prompt.
- Never claim continuity was conditioned if only prose was reused.

Completion criterion: every adjacent shot pair has a documented visual handoff or a deliberate discontinuity.

### 2. Provide edit handles

- Reserve roughly 0.5–1.5 seconds of stable material at the beginning and end of each shot.
- Put the main action inside the shot rather than landing the musical or visual climax on the final frame by default.
- For a 15-second clip, a useful prompt rhythm is: 0–1s settle, 1–13.5s action, 13.5–15s settle or transition.
- Generate longer clips only if supported and verified; do not silently assume arbitrary frame counts work.
- Plan cuts, crossfades, J-cuts, L-cuts, or match cuts before generation.

Completion criterion: every shot manifest contains `head_handle`, `tail_handle`, and `planned_transition`.

### 3. Use a common music plan

- Do not let twenty independent clips define the final score by accident.
- For edit-friendly production, ask H3 primarily for dialogue, breathing, ambience, Foley, and effects, with no music or restrained temporary music.
- Build or select the shared score after the story timing is known.
- Maintain a music map containing theme, intensity, tempo, key or tonal character, start/end energy, and transition points.
- If generated clip music is retained, inspect every boundary and use stems, fades, bridges, or replacement audio as needed.
- Never hide hard musical discontinuities under a visual-only review.

Completion criterion: one film-level score plan exists and every clip boundary has been auditioned.

### 4. Plan audio and movement continuously

For each shot, define:

- incoming ambience and outgoing ambience;
- expected dialogue and speaker;
- sound-effect cues;
- music state;
- camera entry and exit movement;
- actor entry and exit positions;
- screen direction;
- object trajectories;
- intended cut point.

Carry these states into the next shot. A character leaving frame right should not reappear moving left without an intentional reset or reverse angle.

Completion criterion: adjacent rows in the shot manifest agree on incoming/outgoing audio and movement state.

### 5. Promote discovered props and non-human characters into references

- Treat every recurring robot, creature, vehicle, and machine as a character asset, not as background decoration.
- Before its first production shot, build a canonical multi-view reference library and one approved conditioning frame. Do not begin a recurring non-human character from text alone.
- Maintain separate character, wardrobe, environment, vehicle, creature, robot, and prop bibles.
- After an important object first appears, select or generate a canonical still showing its shape, scale, materials, colors, damage, lights, and markings.
- Give the object a stable ID and reference it in every later shot.
- Update the bible when the story intentionally changes the object.
- Do not expect repeated prose alone to preserve a complex newly invented object.

Completion criterion: every recurring story object has a canonical artifact or is marked intentionally variable.

### 6. Explicitly prevent figure duplication

Every character prompt must specify:

- exact number of visible people;
- exact cast members allowed in frame;
- who must not appear;
- one physical instance of each person;
- no duplicates, clones, twins, doubles, ghost copies, extra bodies, repeated faces, mirrored duplicates, or background versions;
- whether reflections, screens, photographs, and holograms are allowed.

Also reduce ambiguity in staging: assign each person a unique side, pose, action, and trajectory. Avoid repeatedly naming absent reference characters unless the node requires all references; if all references must be loaded, state clearly which images are identity references only and which characters are absent.

Completion criterion: every shot has `visible_cast_count`, `allowed_cast`, `absent_cast`, and an anti-duplication clause.

## Preproduction Procedure

### 1. Create the film bible

Record:

- premise, duration, aspect ratio, frame rate, and target delivery resolution;
- visual rules and color script;
- character identity and wardrobe references;
- environment references;
- recurring prop references;
- dialogue language and exact lines;
- score and sound approach;
- continuity exceptions.

Completion criterion: every recurring visual element has a stable name and source artifact.

### 2. Build a boundary-aware shot manifest

Each shot row must include:

- shot number, title, story purpose, estimated duration;
- incoming frame state and outgoing frame state;
- camera start/end position and motion;
- actor start/end position and screen direction;
- visible cast count, allowed and absent cast;
- prop state and reference IDs;
- exact expected dialogue;
- ambience, effects, and music state;
- head/tail handles and planned transition;
- workflow mode, seed, resolution, frames, steps, LoRA, sampler;
- status, prompt ID, output path, and QC result.

Completion criterion: no shot begins from an undefined state unless it is an intentional establishing reset.

### 3. Run continuity review before GPU work

Review every adjacent pair for:

- matching cast and wardrobe;
- compatible pose and screen direction;
- matching environment and lighting;
- stable recurring props;
- plausible camera geometry;
- compatible dialogue and ambience;
- usable edit handles;
- music continuity.

Completion criterion: every boundary is labeled `match`, `planned cut`, or `needs reference`.

## Prompt Construction

Use a structured prompt in this order:

1. global visual and physical realism rules;
2. reference-image roles and identity restrictions;
3. exact visible cast and anti-duplication clause;
4. incoming continuity state;
5. timed action beats with head and tail handles;
6. outgoing continuity state;
7. exact spoken lines, language, and speaker;
8. ambience, Foley, effects, and music restriction;
9. exclusions: subtitles, logos, extra people, anatomy failures, unwanted cuts.

Do not overload one shot with several incompatible camera moves, emotional turns, dialogue exchanges, and object transformations. Split complex action into more shots with explicit boundaries.

## REF2VA and FL2VA Routing

- Use REF2VA when identity or appearance references are the dominant requirement.
- Consider FL2VA or another boundary-conditioned workflow when first/last-frame control is essential.
- Do not assume the two modes can be combined in one graph. Inspect installed node schemas and documentation.
- When a mode cannot carry all needed references, prioritize boundary continuity, then use prompt and canonical stills to retain identity and props; verify the result visually.

## Transformation and Voice-Reference Pattern

The currently inspected H3 node schemas support a useful two-shot pattern:

- `MiniMaxH3ImageToVideo` accepts optional `first_frame` and `last_frame` images. Use it for exact boundary handoff, transformation, or a controlled visual arrival state.
- `MiniMaxH3ReferenceToVideo` accepts up to nine reference images, three reference videos, three matching reference-video audio tracks, and three standalone reference audios. Use it for identity, object, motion, environment, and potential speaker/voice guidance.
- Confirm these inputs against the live `/object_info` schema before every new project because custom-node versions can change.

For a complex transformation followed by dialogue:

1. Render a no-dialogue FL2VA shot from the previous clip's final frame to a canonical target frame.
2. Use that result as a REF2VA reference video for a separate interaction/dialogue shot.
3. Add character and recurring-object reference images.
4. Add the intended speaker sample as `ref_audio` when supported, but verify the actual output voice; a reference-audio input does not by itself prove successful voice cloning.
5. If voice identity fails, generate the exact line through the approved external voice preset, replace only the dialogue audio, and verify lip timing manually.

Do not attempt a trained LoRA first when a clean multi-pose character library is already available. Test image/video references before spending time on training.

Completion criterion: the transformation preserves the non-transforming subjects, the dialogue scene starts from the approved arrival state, and the final voice has explicit proof of origin.

## Rendering and Recovery

The orchestrator must be idempotent.

- Validate an existing clip with minimum size, `ffprobe`, expected duration, video stream, and audio stream before skipping it.
- Persist per-shot status, prompt ID, workflow JSON, seed, attempt, timing, and output path.
- Retry transient HTTP, DNS, and timeout failures with bounded backoff.
- A client timeout does not prove ComfyUI stopped.
- Before resubmitting, inspect `/queue` and `/history/<prompt_id>`.
- Adopt a matching running prompt instead of starting a duplicate.
- Poll both `/history/<prompt_id>` and `/queue`; history alone cannot distinguish a running job from a prompt lost during a ComfyUI restart.
- Emit periodic heartbeats containing prompt ID, queue state, and elapsed time.
- If the server disappears and later returns with the prompt absent from both queue and history, mark the prompt lost after a short grace period and resubmit only that missing shot.
- When the local monitor restarts, adopt the persisted running prompt ID before considering any resubmission.
- Bound automatic lost-prompt resubmissions so a repeatedly crashing server cannot loop forever.
- Download and validate a completed server output before marking success.
- Never interrupt a running ComfyUI job merely because the polling client disconnected.
- Prevent workstation sleep during long batches when authorized, or render one shot at a time with resumable state.

Completion criterion: restarting the orchestrator neither duplicates valid shots nor loses a still-running server job.

## Draft-First Strategy

1. Generate one representative draft at the fast baseline.
2. Review identity, duplication, motion, prompt following, speech, and edit handles.
3. Fix the manifest or prompt before batching the full film.
4. Generate boundary-critical shots early, not only in numerical order.
5. Approve canonical props as soon as they appear and feed them into later shots.
6. Assemble a rough cut before expensive high-step or high-resolution passes.

## Dialogue Verification

Prompted English is not proof of actual English.

After generation:

- extract audio from every clip;
- transcribe with Whisper or an equivalent recognizer;
- perform language identification;
- compare recognized speech against expected lines;
- listen manually to low-confidence segments;
- record missing, invented, distorted, or unintelligible words;
- check whether the correct character appears to speak.

Keep both the expected line and the transcript in the QC report. Do not describe gibberish as successful dialogue because the prompt requested English.

## Visual and Edit QC

Inspect real playback, not only stills.

For every clip, record timecodes for:

- duplicate people or repeated faces;
- identity, costume, hair, tattoo, scar, or prosthetic drift;
- helmet/hair and other physical-intersection errors;
- extra limbs, anatomy errors, teleportation, or object morphing;
- prop and environment inconsistency;
- camera discontinuity and screen-direction reversal;
- dialogue mismatch;
- audio artifacts;
- music peaks landing on unusable hard cuts;
- insufficient head or tail handles.

Create contact sheets for overview, but perform final decisions from audio-enabled playback.

## Assembly

- Preserve raw clips unchanged.
- Create a reversible rough-cut project or manifest.
- Apply planned handles and transitions.
- Build the common score and ambience bed across scene boundaries.
- Use J-cuts and L-cuts where dialogue or ambience should bridge shots.
- Re-render only clips whose defects materially damage the story.
- Verify the final with `ffprobe` and full playback.
- Do not final-render or publish before Walter approves the reviewed cut.

## Step and Resolution Benchmark

When quality is uncertain, compare controlled variants rather than assuming more steps are better.

- Keep prompt, seed, references, duration, and workflow constant where technically possible.
- Compare 6, 8, and one higher documented step count before committing to 20.
- Include 20 steps only if the LoRA/sampler documentation supports or meaningfully permits it.
- Record wall time, peak VRAM, failures, low-VRAM mode, output size, and visual/audio findings.
- Test native Full HD separately from upscaling.
- Never label an upscaled 736×416 render as native 1920×1080 generation.
- On limited VRAM, a failed native test is a useful benchmark result; report it honestly.

Compare:

- faces, hands, hair, and fine detail;
- motion stability and temporal coherence;
- cast duplication;
- identity, wardrobe, prop, and environment consistency;
- prompt and dialogue adherence;
- audio intelligibility;
- render time per delivered second.

## Evidence-Led YouTube Follow-Up

Preserve:

- workflow JSONs and exact model filenames;
- prompts, seeds, steps, frame counts, and resolutions;
- render logs and recovery events;
- representative successes and failures;
- transcripts against expected dialogue;
- QC timecodes;
- controlled benchmark outputs.

Explain LoRA, Turbo mode, sampler, and step recommendations only after checking the concrete implementation documentation. Show real clips for every quality claim and include workflow-design mistakes as part of the production story.

## Pitfalls

1. A beautiful isolated clip can still be unusable in a film.
2. Reusing character references does not preserve newly invented props.
3. Independent per-shot music naturally creates hard audio cuts.
4. Strong standalone 15-second arcs can fight whole-film pacing.
5. More steps may add time without improving a Turbo-distilled workflow.
6. Native Full HD may exceed practical VRAM even when low-resolution drafts work.
7. A polling timeout can coexist with a healthy server-side render.
8. Contact sheets cannot reveal language, music, pacing, or motion defects.
9. Prompt exclusions reduce duplication risk but do not guarantee exact cast count.
10. Loading references for absent characters may still encourage unwanted appearances.

## Verification Checklist

- [ ] Film, character, environment, wardrobe, and prop bibles exist.
- [ ] Every boundary has a visual handoff or deliberate discontinuity.
- [ ] Every shot has head/tail handles and a planned transition.
- [ ] One film-level music and audio plan exists.
- [ ] Actor, camera, and object movement states flow across shots.
- [ ] Recurring discovered objects have canonical reference artifacts.
- [ ] Every prompt states exact cast count and forbids duplication.
- [ ] The renderer can resume without duplicating jobs.
- [ ] All clips pass technical and real-playback QC.
- [ ] Speech is transcribed and compared with prompted dialogue.
- [ ] Music boundaries are auditioned.
- [ ] Step/resolution claims come from documented, controlled tests.
- [ ] Raw proof artifacts are preserved for the YouTube follow-up.
- [ ] Walter has approved the reviewed cut before final render or publication.
