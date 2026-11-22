# INNER SIGNAL — WebGL2 / Living ASCII

An original, 150-second, seven-chapter audiovisual experience inspired by Chetaslua's [ASCII concept](https://x.com/chetaslua/status/2123689803350978666).

## Open

Open `index.html` in a modern browser. The site has no JavaScript libraries or build step. A Google Fonts connection is optional: it falls back to the system's monospace font when offline.

The preferred renderer is **native WebGL2** (not Three.js). On browsers where WebGL2 is disabled, the same page automatically switches to an interactive Canvas2D compatibility mode.

## Explore

- **Space** — play / pause
- **← / →** — seek by one second
- **1–7** — jump to a chapter
- **H** — rendering debug overlay
- **R** — switch between raw 3D and ASCII (WebGL2 only)
- Drag the timeline or use the chapter navigation on the left
- Toggle ambient audio, fullscreen, and rendering quality using the lower controls

## Capture and debug

- `?t=42` — pause on a selected second
- `?scene=4` — pause at chapter four
- `?raw` — show the underlying 3D scene in place of the ASCII compositor
- `?record` — render a fixed 1920 × 1080 canvas with on-screen controls hidden
- `await window.renderFrame(73.4)` — render a deterministic frame at a specific time (the history pass is reset for frame capture)
- `await window.renderAudio()` — produce a 150-second stereo WAV `Blob` using `OfflineAudioContext`
- `window.DURATION === 150` and `window.FPS === 30` — capture metadata

## Implementation details

1. A raymarched 3D environment with seven spatially connected rooms, computed distance geometry, normals, depth, procedural lighting and atmosphere.
2. A **persistent 2,600-particle memory swarm** whose deterministic particle IDs are reshaped into successive room materials.
3. A procedurally generated glyph atlas, sorted using measured font-ink coverage, with gradient-informed edge strokes.
4. Depth-aware ASCII cell scaling, motion flicker, per-scene three-stop color gradients, spatial bloom approximation, subtle film grain, vignette and phosphor history.
5. Continuous camera movement through world coordinates rather than scene-to-scene frame dissolves.
6. An interactive cinematic player with captions, chapter navigation, debug info, audio and capture hooks.

## Credits

Created by Anirudh Nadipally with ChatGPT (OpenAI). Concept inspired by Chetaslua's ASCII experiment on X; all code and scenes in this piece are new.

## Changes in this version

- Captions and lower controls sit on a dark backing so they stay readable over the glyph field.
- Chapter 7 (The Face) gives more of the swarm to the eyes, brows, nose and lips, so the face resolves clearly.
- Entering the experience turns ambient sound on.
- Fixed `?record` mode, which failed to start (it removed the intro, then tried to hide it).

## Validation and limitations

JavaScript syntax was checked. The WebGL shader stages compiled and linked in a native OpenGL ES 3.2 (Mesa) context, and sample real 3D and ASCII passes rendered without GL errors. Browser automation in the available environment does **not** expose WebGL, so browser-based WebGL visual performance and frame-rate goals have **not** been measured. The Canvas2D compatibility path was exercised at all seven chapters, including a pixel-identical repeated timestamp test.

This is an original interpretation, not a pixel-perfect reproduction of the referenced video or the original prompt's complete specifications. In particular, it uses native WebGL2 rather than Three.js, approximates rather than fully simulates volumetric shadows and sound effects, and does not claim 60 fps or 33 ms/frame across devices.
