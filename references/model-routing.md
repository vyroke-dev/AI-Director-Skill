# Bring-Your-Own-Model Routing & Production Preflight

Load for render requests, model choices, prompt conversion, local inference, APIs or MCP tools. **The user's own available models come first.** Higgsfield is neither necessary nor a default.

## Capability discovery (no invented model support)

Inspect only available, authorized Agent tools/connectors, local project configuration, installed model endpoints and official provider schemas. Produce a `capability_matrix` for each genuine model containing: model ID/version; invocation tool; task (image/video/audio/lip-sync/edit/upscale); T2I/T2V/I2V/reference-conditioning/multiple-frame inputs; permitted aspect ratios, duration, resolution, frame rates; audio support; output formats; queue/poll/cancel; pricing or local compute limits; and reference to the capability evidence. Mark unknown fields `unknown` and do **not** convert them into confident capabilities.

No tool means provide a model-agnostic shot pack and explicit `not_available` execution status. Do not demand account secrets in chat or write tokens to production files. Never claim a generic `generate_video` endpoint exists. Inspect schemas before invocation.

## Model selection

For each planned shot, choose from *verified user-available* models based on:
1. Required inputs/outputs and format support (hard constraints).
2. Visual identity and reference conditioning for recurring characters (hard constraints when canon requires it).
3. Performance, motion type, audio/lip-sync needs, and editing/extension (task suitability).
4. Quality evidence from actual tests, not reputation claims.
5. Estimated cost, latency, resource quotas and retry budget.

When no single model supports the whole task, decompose: reference stills / backgrounds → motion clips → speech/audio → lip-sync if authorized/supported → editor/compositor → upscaling/QC. Do not assume the existence of an editor; hand off commands or edit decision lists when absent. Explain why the selected model fits **this shot**, with alternatives only when useful.

## Prompt compilation

Generate a stable, provider-neutral **director specification** first: story beat; subject IDs/references; character action (timeline and causality); blocking; camera framing/angle/move/lens intent; look/light; audio/dialogue; continuity entry/exit; avoid list. Next compile that specification to each model's *documented* accepted inputs, removing unsupported flags. Never pass `lens_mm`, `aperture_f`, references, negative prompts or emotions as literal API fields unless documented. Treat focal length and aperture as camera-direction intent if no native parameter exists.

For I2V, prioritize the approved still reference; specify what changes over time and what should stay fixed instead of repeating every visible detail. For T2V, explicitly describe essential characters and setting. A reference chip such as `@heroine` is just a **local asset alias** until translated to an actual URI or provider token; do not assume any provider recognizes it. No general-purpose prompt formula guarantees consistency.

## Paid execution gate

Before every paid submission or batch: show concrete model ID, shot IDs, reference inputs, duration/resolution, estimated cost and credits **only if verified**, max attempts and total budget cap. Obtain authorization unless a still-valid explicit authorization already covers the exact scope and ceiling. Unknown pricing requires user decision before spend, not a fabricated zero price. No autonomous credit spending by default.

Persist `shot_id` → `model_id` → `job_id` → output URI → attempt → observed status, with an idempotency/request key when available. Poll via a documented endpoint. On timeout, query existing job status before any resubmission to avoid duplicate bills. On uncertainty, pause and surface the ambiguity. Stop at budget or attempt limits, retain successful assets, and isolate failures.

## Quality-driven rerouting

Inspect actual outputs (or clearly label review as unavailable). Diagnose identity drift, motion physics, geography, anatomy, pacing, lip sync, text rendering, reference mismatch and audio. Try a targeted prompt/reference repair or a verified alternative model only when necessary, with the user's existing cost approval still valid. Record the failure cause and new attempt evidence; never blindly regenerate.

## Example capability entry (illustrative, not a real service)

```json
{
  "model_id": "user-video-model",
  "task": "image-to-video",
  "invocation": "available-agent-tool-name",
  "reference_images": "verified",
  "native_audio": "unknown",
  "duration_options_s": [4, 6],
  "pricing": "unknown",
  "schema_source": "provider docs or tool definition to be recorded"
}
```
