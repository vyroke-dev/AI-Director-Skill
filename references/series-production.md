# Serialized AI Anime/Manju Production Protocol

Load for 漫剧, 动漫短剧, multi-episode storytelling, recurring characters, or a request to make a whole episode. This is an original provider-independent workflow, not a reproduction of Higgsfield internals.

## Hierarchy and creative responsibility

**Series bible → season arc → episode outline → scene beats → shot plans → renders → editorial → evidence-based QA**. Preserve approved decisions at each level. A shot may be visually excellent and still wrong if it breaks the story.

Before a new episode: load the latest approved series bible, previous episode exit states, current character/wardrobe/location/prop records, unresolved plot threads, dialogue/voice records, and available references. If they are unavailable, mark them missing and do not invent past canon.

Make an `episode_id`, stable `scene_id` and `shot_id`; connect every shot to an objective and its source beat. A suggested working directory under the user's *project* (not the installed Skill) is:

```text
production/
  series-bible.md
  canon/characters.md
  canon/locations.md
  canon/props.md
  canon/voices.md
  episodes/EP001/episode-plan.md
  episodes/EP001/shot-list.json
  episodes/EP001/continuity-ledger.md
  episodes/EP001/generation-ledger.jsonl
  episodes/EP001/review.md
```

Never overwrite user files or claim the directory exists until you inspect/create it with authorized file tools. Do not put production assets inside the installed Skill folder.

## Series bible / canon ledger

For each character save: stable ID, approved visual references, distinct silhouette, hairstyle/color, face markers, wardrobe variants, relative size, personality, emotional baseline, voice ID or reference (if actually available), relationships, and forbidden drift. Keep immutable identity traits separate from **scene state** (mud, tears, injury, costume changes, carried prop, emotional state). Annotate every change with episode, scene, shot and reason.

For each location: approved establishing image / map if available; entrances/exits, doors, windows, landmark positions, lighting sources, day/night state, orientation/180-degree axis. For each prop: owner, which hand, orientation, condition and handoff history. Do not promise pixel-perfect consistency from text only; if a model supports conditioning, use actual approved references.

At every cut check: last visible state → next visible state; screen direction/eyeline, body positions, clothing and held objects, geography and ambient sound, dialogue and time jump. Track unresolved changes and who approved them. A deliberate continuity break requires a stated narrative reason.

## Direct episode breakdown

1. Read the script without dropping dialogue or rewriting plot twists. Identify hook, stakes, escalation, reversal, cliffhanger and episode-to-episode handoff. Record any proposed script change separately for approval.
2. Divide into scenes with dramatic purpose, place, time, involved characters, dialogue, and continuity entry/exit.
3. Divide scenes into shots; include shot ID, duration, visual objective, shot size, angle, lens *intent*, composition, action timeline, one primary camera move (unless deliberately combined), frame start/end, cast/prop/location refs, eyelines, entry/exit state and audio cues.
4. Give a coverage pattern justified by the dramatic beat: establishing/relationship framing, readable action or performance, reaction, motivated insert, breathing room. Avoid relentless close-ups or purposeless zooms.
5. For dialogue, plan master/over-shoulder/singles/reactions or deliberate alternative coverage. Attribute each line to a speaker, annotate overlap and off-screen lines, and reserve readable mouth time. Voice and lip-sync are separate operations unless the chosen model truly supports synchronized generation.
6. For action, map spatial axes and causal beats before camera motion. Avoid impossible teleportation and too many actions within the model's short generation window.
7. Specify editorial pace and transition reasoning. A 'single shot' is an editorial requirement, not a guarantee from a generator. Multi-cut output requires a verified model feature or external editor.
8. For each shot draft: reference-frame prompt → motion/action prompt → dialogue/audio notes → negative/avoid constraints appropriate to the selected model. Do not force Higgsfield-specific syntax onto other models.

## Approval and state governance

Use statuses `planned`, `review_required`, `approved`, `submitted`, `in_progress`, `completed`, `failed`, `rejected`. A shot completion does not mean approval. Lock approved canon, scene intents and good renders. When an edit touches a locked element, show affected episodes/shots and ask before a destructive canon rewrite.

Scope revisions by smallest dependency graph: shot change → adjacent continuity → dependent audio/edits → final QA. Record the old and new versions, reviewer reason and evidence. Never regenerate the entire episode to repair one shot unless the dependencies justify it.

## QA gates

- **Script gate:** no missing beat, ambiguous speaker, unapproved plot change.
- **Preflight gate:** all references and model capabilities verified; estimated paid spend/caps approved, no hidden API keys.
- **Continuity gate:** cross-shot/cross-episode identity, geography, wardrobe, props, voice and chronology agree.
- **Editorial gate:** duration, dramatic rhythm, cut motivation, audio bridge, readability on target screen.
- **Media gate:** view or inspect real frames/clip/audio before claiming quality; if inspection cannot be performed report `not_verified`.

For production handoff, produce a human-readable episode plan plus structured files the agent can actually save; current `assets/project.schema.json` remains the **v1 single-film JSON contract**. Do not pretend it already validates multi-episode structures. Keep series ledgers separate unless and until an explicit versioned schema and validator are implemented.

## Example: scene-to-shot handoff

Scene EP01-S03: heroine discovers an empty medicine vial; rival hears her footsteps. The reveal is **the missing medicine**, not a random camera flourish.
- EP01-S03-SH01, 4 s: corridor geography; heroine enters from screen left, follows window light.
- EP01-S03-SH02, 3 s: her **right** hand lifts the labeled empty vial; match the previous position of her hand and the vial.
- EP01-S03-SH03, 4 s: heroine reaction; her eyeline stays toward frame right; one breath before dialogue.
- EP01-S03-SH04, 3 s: rival reacts behind the door; transition establishes that the sound came from the corridor.

Every reference remains `planned` until an actual asset URI or file is recorded; these are shot directions, not generated results.
