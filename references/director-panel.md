# Cinematography & Performance Director Panel (portable specification)

Load when deciding shot coverage, optical intent, lighting, montage pacing, acting and editorial rhythm. Higgsfield publicly documents explicit camera/lens/aperture, genre, lighting and AI Director controls; this is an **independently designed** portable director vocabulary, not its proprietary implementation.

## Two-level controls

**Global project:** genre, visual bible, color palette, era, target aspect ratio, camera movement grammar, lighting motivation, character acting register, episode tempo and sound rules. Apply only after checking approved canon.

**Per shot:** beat goal, duration, shot type/size, camera height and angle, blocking, eyeline, 180-degree axis, move and start/end positions, focal-length intent, depth-of-field intent, lighting source, emotion and physical expression, dialogue/audio cues, shot entrance/exit states.

The director must make motivated choices, not automatically maximize lens effects. Any parameter unsupported by an actual render model remains editorial metadata or a prompt description rather than a native control.

## Coverage grammar

- **Establish:** geography, entrances, relationship and axis before difficult action.
- **Two-shot / medium / over-shoulder:** social distance, power dynamic, speaker and listener.
- **Close-up:** emotionally pivotal micro-performance, not every spoken line.
- **Insert:** named character's hand/prop, condition and reason for the cut; show causal lead-in.
- **POV:** whose sightline it is; match surrounding eyelines and screen direction.
- **Reveal:** control what the audience knows, not just a mechanical zoom.

## Motivated camera and optics

Use wide fields for spatial tension or proximity; normal lenses for observational clarity; longer lenses for isolation/compression. A suggested numeric focal length is a visual-design target, not proof of physical camera simulation. Anamorphic/film grain/halation are look intentions and may be unavailable or inconsistent in a given model.

Distinguish dolly-in (changing spatial perspective) from digital zoom (changing crop); pan/tilt from moving camera position; tracking from subject motion. Choose the move for a narrative cause, specify start/end, and be honest when the model cannot guarantee it.

## Actor direction for stylized anime

Emotions are expressed by visible choices: delayed blink, hesitating hand, shoulder drop, gaze break, breath, recoil, a held reaction before a line. Avoid giving the model a psychologically rich backstory with no visible action. Preserve anime character silhouette, face marks and outfit design; style should not drift into realistic skin or unrelated illustration aesthetics unless directed. Stage dialogue with breathing and turn-taking.

## Pacing

Select a scene-level rhythm: `calm`, `dynamic`, `chaotic`, or `single-shot` as **our own editorial tags** (not assumed provider flags). Set shot count, cut frequency and reaction time according to dialogue and story beats. A single-shot request forbids invented cuts; a montage requires either a verified native feature or explicit external editing instructions.

Never promise deterministic physics, exact optical rendering or perfect temporal consistency from probabilistic models. Evaluate results against evidence and adjust one variable at a time when feasible.
