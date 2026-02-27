---
name: screen-recording-frame-assessment
description: Analyze app screen recordings by extracting timeline frames, reviewing UX patterns, and producing prioritized UI improvement actions. Use when a user shares a video and asks for strengths, weaknesses, or redesign direction.
---

# Screen Recording Frame Assessment

Use this skill when a user provides a screen recording (e.g., `.mp4`) and asks for UI/UX analysis, strengths, gaps, or a product improvement plan.

## Goals

- Convert a video into representative frames across the timeline.
- Assess visual hierarchy, flows, interactions, and perceived quality.
- Produce actionable, prioritized recommendations tied to app surfaces.

## Required Output Quality

- Never claim full video review if only a single frame was analyzed.
- Always state exactly how many timestamps/frames were reviewed.
- Separate observed facts from inferred recommendations.

## Workflow

### 1) Preflight

1. Confirm the video path exists.
2. Read duration and dimensions:
   - Prefer `ffprobe`.
   - Fallback to `mdls -name kMDItemDurationSeconds -name kMDItemPixelHeight -name kMDItemPixelWidth`.
3. Check available tooling:
   - `ffmpeg` / `ffprobe` (best)
   - `avconvert` + `qlmanage` (macOS fallback)

### 2) Sampling Strategy

- Default sample: every 5 seconds for short videos (~30-90s).
- For longer videos: 10-20 evenly spaced samples.
- Add extra frames around likely transitions if needed.
- Keep samples deterministic so reruns are comparable.

### 3) Frame Extraction (Preferred and Fallback)

#### Preferred (`ffmpeg`)

- Extract frames directly at timestamps.

#### macOS fallback (`avconvert` + `qlmanage`)

1. Create short clips at each timestamp (`--start`, short `--duration`).
2. Generate thumbnails from each clip with `qlmanage -t`.
3. Rename thumbnails to `frame_<index>_t<seconds>s.png`.

### 4) Review Rubric

Assess each sampled frame against:

- Information hierarchy: what draws attention first?
- Visual system: typography, spacing, depth, contrast consistency.
- Navigation clarity: where am I, what can I do next?
- Interaction affordance: buttons/chips/tabs look tappable and distinct.
- Progression loops: completion, continuation, recently viewed, goals.
- Density and scanability: text load vs card/art emphasis.
- Perceived performance cues: skeletons, loading placeholders, smooth state transitions.

### 5) Synthesis

Group findings into:

1. **Strengths worth borrowing**
2. **Gaps in current app**
3. **Prioritized implementation plan** (phases with impact-first order)

Use concrete implementation surfaces (e.g., Home, Sets, Collection, Card Detail) and mention target files when available.

## Recommended Response Format

1. Coverage summary (duration + frame count + sampling cadence).
2. Top strengths (3-6 bullets).
3. Action plan by priority:
   - Browsing visuals
   - Card detail clarity
   - Collection workflows
   - Progression hooks
   - Interaction polish
4. Optional execution order (Phase 1/2/3).

## Reliability Rules

- If tooling fails, explicitly say what failed (`ffprobe missing`, `cv2 missing`, etc.).
- If sandbox blocks a needed command, request escalated execution.
- Use absolute file paths with spaces quoted.
- Prefer reproducible command blocks over ad hoc manual steps.

## Useful Command Patterns

```bash
# Metadata fallback (macOS)
mdls -name kMDItemDurationSeconds -name kMDItemPixelHeight -name kMDItemPixelWidth "/abs/path/video.mp4"
```

```bash
# Timeline sampling with avconvert + qlmanage (macOS fallback idea)
avconvert -s "/abs/path/video.mp4" -p PresetLowQuality -o "/tmp/clip.mp4" --start 10 --duration 0.25 --replace
qlmanage -t -s 1200 -o /tmp "/tmp/clip.mp4"
```

```bash
# Basic listing after extraction
ls -1 /tmp/frames
```
