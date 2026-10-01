# Reference inputs and privacy

The workflow JSON files retain the original input **filenames** so the graph structure is reproducible. The underlying Walter identity images, voice sample, generated clips, and other private/copyrighted source media are intentionally not distributed.

Before queuing a workflow:

1. Open every `LoadImage`, `LoadVideo`, and `LoadAudio` node.
2. Replace the unavailable filename with your own approved asset.
3. Keep each reference's role aligned with the prompt: identity, wardrobe, staging, object, continuity video, or dialogue audio.
4. Verify that no private path, token, hostname, or unrelated image appears in the graph.
5. Run one short draft before starting a batch.

For REF2VA character tests, provide clean canonical images with consistent identity and wardrobe. For recurring props, create a separate canonical object reference. For first/last-frame workflows, use approved boundary frames from your own edit.

Do not publish biometric references or voice samples without permission.