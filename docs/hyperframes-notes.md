# HyperFrames Research Notes

**Project**: Corporate AI Story Reels  
**Date**: 2026-11-17  
**Phase**: 0 — Documentation & Environment Verification  

---

## 1. How a Composition is Defined

### HTML Structure & Required Attributes

A **composition** is an HTML file that defines a self-contained visual scene with explicit timing metadata. The root element must carry these `data-*` attributes:

| Attribute | Purpose | Example |
|-----------|---------|---------|
| `data-composition-id` | Unique identifier for this composition | `"code-typing"` |
| `data-start` | Start time in seconds (relative to parent) | `"0"` |
| `data-duration` | Duration in seconds | `"5"` |
| `data-track-index` | Z-order / layer index | `"0"` |
| `data-width` | Canvas width in pixels | `"1920"` |
| `data-height` | Canvas height in pixels | `"1080"` |

**Reference**: `vendor/hyperframes/docs/concepts/data-attributes.mdx`, `vendor/hyperframes/registry/blocks/code-typing/code-typing.html:231-238`

### Composition Root Element Pattern

```html
<div
  id="root"
  data-composition-id="code-typing"
  data-start="0"
  data-duration="5"
  data-width="1920"
  data-height="1080"
>
  <!-- Scene content -->
</div>
```

### Timing Model

- **Global timeline**: Each composition has its own timeline (0 to `data-duration`)
- **Nested compositions**: Child compositions inherit parent's timebase; their `data-start` is relative to parent
- **Frame precision**: Rendering seeks to exact frame times (1/30s at 30fps)
- **Deterministic seeks**: No `Date.now()`, `performance.now()`, or unseeded randomness — animation state derives purely from timeline position

**Reference**: `vendor/hyperframes/docs/concepts/compositions.mdx`, `vendor/hyperframes/docs/concepts/determinism.mdx`

### Layout Ignore

Elements with `data-layout-ignore` are excluded from automatic layout calculations (useful for backgrounds, glows, decorative elements):

```html
<div class="bg-glow a" data-layout-ignore></div>
```

**Reference**: `vendor/hyperframes/registry/blocks/code-typing/code-typing.html:239-242`

---

## 2. How Animation is Driven (GSAP) & Time Control

### GSAP Contract

HyperFrames uses **GSAP 3.x** with **paused timelines** registered on `window.__timelines[compositionId]`:

```javascript
window.__timelines = window.__timelines || {};
var tl = gsap.timeline({ paused: true });
// ... build timeline ...
window.__timelines["code-typing"] = tl;  // Register AFTER fully built
```

**Critical Rule**: Register the timeline **only after** it's fully constructed. The runtime treats "key present in `window.__timelines`" as "ready to nest". An empty timeline registered prematurely → blank render when used as sub-composition.

**Reference**: `vendor/hyperframes/docs/guides/gsap-animation.mdx`, `vendor/hyperframes/registry/blocks/code-typing/code-typing.html:734-755`

### Time Control During Render

- **Engine seeks timeline**: On each frame, the renderer calls `tl.seek(frameTime)` — no `play()`, no `progress()` animation
- **No autonomous animation**: Timelines never run on their own; they are **scrubbed** by the render engine
- **Deterministic**: Same seek time → same visual state, every render

### Font Loading Gate

Animation setup **must wait for `document.fonts.ready`** before measuring glyph metrics (FLIP, bounding rects):

```javascript
document.fonts.ready.then(function () {
  // Build timeline here — glyph metrics are final
  tl.from("#editor", { opacity: 0, scale: 0.985, duration: 0.5 }, 0);
  buildEffect(tl, surface, spec);
  window.__timelines["code-typing"] = tl;
  if (typeof window.__hfForceTimelineRebind === "function") {
    window.__hfForceTimelineRebind(); // Re-nest now populated
  }
});
```

**Reference**: `vendor/hyperframes/registry/blocks/code-typing/code-typing.html:746-755`

### Animation Patterns Used in Registry Blocks

| Pattern | Description | Example Block |
|---------|-------------|---------------|
| **Token-by-token fade** | Per-character/token opacity wave with caret glide | `code-typing` |
| **FLIP transitions** | Measure start/end rects, animate transform delta | `code-diff`, `claude-exchange` |
| **Scene crossfade** | Opacity swap between `.scene` divs | `code-typing` (line 118-123) |
| **Staggered reveals** | `gsap.to(elements, { opacity: 1, stagger: 0.05 })` | `message-thread-reveal` |
| **Typewriter with caret** | Per-char reveal + moving cursor | `code-typing` (lines 665-726) |

---

## 3. How Audio is Attached and Synced

### Native `<audio>` Elements with Timing Attributes

Audio elements live in the composition HTML with the same `data-*` timing attributes:

```html
<audio 
  id="music" 
  src="music.wav" 
  data-start="0" 
  data-duration="30" 
  loop
></audio>
<audio 
  id="voiceover" 
  src="vo.wav" 
  data-start="1.5" 
  data-duration="12"
></audio>
<audio 
  id="sfx-whoosh" 
  src="whoosh.wav" 
  data-start="3.2" 
  data-duration="0.8"
></audio>
```

**Reference**: `vendor/hyperframes/docs/guides/voice-and-audio.mdx:92-103`

### Loop Support

- `loop` attribute repeats audio until `data-duration` ends
- `data-media-start` sets source in-point for each repeat
- Playback speed/rate automation applies to repeated audio
- Video elements with `data-has-audio="true"` also loop their sound

### Music Ducking (Voiceover Carve)

- **Automatic**: Engine detects voice vs music stems and dips music only during speech
- **Manual control**: "voiceover carve" feature in Studio app (`/studio/audio-effects#make-music-sit-under-narration`)
- **Timing**: Duck starts at voice onset, ends at voice offset — speech already ended doesn't create new dip

**Reference**: `vendor/hyperframes/docs/guides/voice-and-audio.mdx:125-130`

### Audio Sources

| Source | Free (Local) | HeyGen (Cloud) |
|--------|--------------|----------------|
| **Voice** | Kokoro TTS (multi-language) | HeyGen voices + custom clones |
| **Music** | Local tracks / generation | 10,000-track catalog |
| **SFX** | Bundled set + Openverse | Same + HeyGen library |
| **Captions** | Local Whisper/Parakeet | HeyGen transcription |

**Reference**: `vendor/hyperframes/docs/guides/voice-and-audio.mdx:34-45`

### Audio Analysis CLI

```bash
# Analyze reference soundtrack (6 stems: vocals, drums, bass, guitar, piano, other)
npx hyperframes audio reference.mp4 --read --quality best

# Transcribe local audio
npx hyperframes transcribe interview.mp4 --language es
```

**Reference**: `vendor/hyperframes/docs/guides/voice-and-audio.mdx:59-83`

---

## 4. How Rendering Works: CLI, Dependencies, Output

### CLI Commands

```bash
# Lint composition (validate structure, determinism)
npx hyperframes lint

# Check render (dry-run, validate assets)
npx hyperframes check

# Render to MP4
npx hyperframes render --output output.mp4

# Render with quality tier
npx hyperframes render --output output.mp4 --quality best   # 4K/HDR available
npx hyperframes render --output output.mp4 --quality draft  # Fast preview

# Preview locally (opens browser editor)
npx hyperframes preview
```

**Reference**: `vendor/hyperframes/docs/guides/rendering.mdx`, `vendor/hyperframes/docs/developers/cli.mdx`

### Required Dependencies

| Dependency | Version | Purpose |
|------------|---------|---------|
| **Node.js** | 22+ | Runtime for CLI & build |
| **bun** | Latest | Package manager (faster installs) |
| **FFmpeg** | 6+ | Video encoding (H.264, HEVC, ProRes) |
| **GSAP** | 3.12+ | Animation engine (loaded via CDN) |
| **Chrome/Chromium** | Latest | Headless rendering backend |

### Output Specification (Target for This Project)

| Parameter | Value |
|-----------|-------|
| **Resolution** | 1080 × 1920 (9:16 vertical) |
| **Frame Rate** | 30 fps |
| **Video Codec** | H.264 (MP4) |
| **Audio Codec** | AAC |
| **Audio Level** | ~-14 LUFS (broadcast standard) |
| **Color Space** | Rec.709 (SDR) — HDR optional via `--quality best` |

**Reference**: `vendor/hyperframes/docs/guides/rendering.mdx`, build prompt requirements

### Quality Tiers

| Tier | Resolution | Use Case |
|------|------------|----------|
| `draft` | 540×960 @ 15fps | Rapid iteration |
| `high` | 1080×1920 @ 30fps | **Production default** |
| `best` | 2160×3840 @ 30fps + HDR | Archive / 4K deliverables |

### Deterministic Rendering Requirements

From `vendor/hyperframes/docs/concepts/determinism.mdx`:

- ❌ No `Date.now()`, `performance.now()`, `new Date()`
- ❌ No unseeded `Math.random()` — use seeded PRNG if needed
- ❌ No network fetches during render (all assets local)
- ❌ No `setTimeout`/`setInterval` — use timeline position
- ✅ All animation driven by `tl.seek(frameTime)`
- ✅ Fonts preloaded via `<link rel="preload">` or `@font-face`
- ✅ Images/audio referenced by local path or data: URI

---

## 5. Claude Code Plugin / Skill / MCP Server

### Skills System (Primary Integration)

HyperFrames provides **Claude Code skills** (not a plugin/extension):

```bash
# Install skills into your project folder
npx hyperframes skills update
# OR
npx skills add heygen-com/hyperframes
```

Then restart Claude Code in that folder. Skills expose:
- `/hyperframes` slash command for video generation
- Prompting guidance for media/audio
- Registry block knowledge

**Reference**: `vendor/hyperframes/README.md` (Skills section), `vendor/hyperframes/docs/quickstart.mdx:57-62`, `vendor/hyperframes/CLAUDE.md`

### MCP Server (HeyGen Cloud)

For **cloud rendering without local setup**, HyperFrames offers an MCP connector for Claude.ai / ChatGPT:

- Builds and renders in HeyGen cloud
- Requires HeyGen API key
- No local project folder — trades control for convenience

**Reference**: `vendor/hyperframes/docs/quickstart.mdx:108-112`, `vendor/hyperframes/docs/guides/voice-and-audio.mdx:43-45`

### No Native VS Code Extension / CLI Plugin

- No `hyperframes` binary installed globally (runs via `npx`)
- No dedicated VS Code extension (skills work in any agent)
- Studio app is separate Electron app (Mac/Win/Linux)

---

## 6. Known Limitations & Gotchas

### Composition & Nesting

| Gotcha | Impact | Workaround |
|--------|--------|------------|
| **Empty timeline registration** | Blank render as sub-composition | Register `window.__timelines[id]` **after** `document.fonts.ready` + build complete |
| **`data-layout-ignore` on root** | Breaks layout engine | Only on decorative children (backgrounds, glows) |
| **Nested composition timing** | Child `data-start` relative to parent | Document timebases explicitly in comments |
| **Variable resolution** | Parent variables don't auto-propagate | Pass via `data-var-*` on child root element |

**Reference**: `vendor/hyperframes/docs/concepts/compositions.mdx`, `vendor/hyperframes/registry/blocks/code-typing/code-typing.html:743-755`

### Animation & GSAP

| Gotcha | Impact | Workaround |
|--------|--------|------------|
| **CSS transitions** | Break under non-sequential frame seeking | Use only GSAP timelines (paused) |
| **`tl.play()` / `tl.progress()`** | Won't work — engine seeks | Build static timeline; let engine `seek()` |
| **Font metrics before `fonts.ready`** | Wrong FLIP rects, jittery text | Always wrap build in `document.fonts.ready.then()` |
| **Unseeded randomness** | Non-deterministic renders | Use `gsap.utils.random(seed, min, max)` or custom PRNG |

**Reference**: `vendor/hyperframes/docs/guides/gsap-animation.mdx`, `vendor/hyperframes/docs/concepts/determinism.mdx`

### Audio

| Gotcha | Impact | Workaround |
|--------|--------|------------|
| **Audio sync drift** | Long videos drift vs timeline | Use `data-media-start` for precise in-points; keep clips < 30s |
| **Loop gap** | Audible gap at loop boundary | Ensure source file loops cleanly (zero-crossing) |
| **Music ducking false positives** | SFX ducked as voice | Tag stems explicitly; use voiceover carve for precision |

**Reference**: `vendor/hyperframes/docs/guides/voice-and-audio.mdx:92-130`

### Rendering & CLI

| Gotcha | Impact | Workaround |
|--------|--------|------------|
| **FFmpeg missing** | Render fails silently | `npx hyperframes check` validates deps first |
| **Font not embedded** | Glyphs missing in output | Preload via `<link rel="preload" as="font" crossorigin>` |
| **Large asset memory** | OOM on 4K renders | Use `draft` quality for iteration; split into sub-compositions |
| **Windows path length** | `ENOENT` on deep nests | Enable long paths: `git config --system core.longpaths true` |

**Reference**: `vendor/hyperframes/docs/developers/cli.mdx`, `vendor/hyperframes/docs/guides/rendering.mdx`

### Registry Blocks (Component Library)

| Limitation | Notes |
|------------|-------|
| **~450 blocks** but not all vertical (9:16) | Many are 16:9 (1920×1080) — need adaptation |
| **No official "Corporate UI" category** | Build from primitives: `code-diff`, `claude-exchange`, `chatgpt-exchange`, `message-thread-reveal`, `code-typing` |
| **Blocks hardcode dimensions** | Must override `data-width`/`data-height` on composition root for 1080×1920 |
| **Token data baked at author time** | `window.__TOKENS` generated by Shiki Magic Move — dynamic code needs rebuild |

**Reference**: `vendor/hyperframes/README.md` (Registry section), examined blocks

---

## Verification: Render a Repo Example End-to-End

### Test Plan

```bash
cd vendor/hyperframes

# 1. Install dependencies
bun install

# 2. Pick a simple registry block (code-typing)
# 3. Lint it
npx hyperframes lint registry/blocks/code-typing/code-typing.html

# 4. Check render
npx hyperframes check registry/blocks/code-typing/code-typing.html

# 5. Render to MP4 (draft quality for speed)
npx hyperframes render registry/blocks/code-typing/code-typing.html --output test-output.mp4 --quality draft

# 6. Verify output exists and plays
# (manual: open test-output.mp4)
```

### Expected Result

- ✅ Lint passes (no determinism violations)
- ✅ Check passes (assets resolve, timeline registers)
- ✅ Render produces `test-output.mp4` (~5s, 1080×1920 or 1920×1080 depending on block)
- ✅ Video plays: editor fades in, code types character-by-character with caret

### Notes for This Project

- `code-typing` block is **landscape** (1920×1080) — will need vertical adaptation
- `claude-exchange` is **portrait** (1080×1920) — perfect reference for our format
- All registry blocks assume landscape unless noted; vertical blocks are rare

---

## Next Steps (Phase 0b → Phase 1)

1. **Phase 0b**: Write `docs/algorithm-notes.md` with platform ranking signal research (TikTok/Reels/Shorts)
2. **Phase 1**: Create `story/bible.md` — series title, world, protagonist, cast, personal stake, tone rules, motifs
3. **Phase 2**: Create `story/season-1-outline.md` — 20-episode table with laws/concepts
4. **Phase 3**: Write 20 episode scripts in `story/episodes/ep-XX.md`
5. **Phase 4**: Build visual system & HyperFrames components (adapt registry blocks for 9:16 corporate UI)
6. **Phase 5-8**: Engagement playbook, publishing guide, production runbook