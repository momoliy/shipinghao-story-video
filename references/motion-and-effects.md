# Motion and effects (动效与视频效果)

Motion is part of the visual style, not improvisation at assembly time. It is locked once in VISUAL_STYLE as `MOTION_STYLE.md` and applied mechanically in PREVIEW and FINAL_RENDER. Do not invent new motion types, transitions, or subtitle looks during assembly; a change goes back to VISUAL_STYLE as `需要返工`.

## Audience default

The default preset is `steady` (稳重), tuned for history and story content watched by middle-aged and older viewers: slow, small, predictable motion; few transition types; large high-contrast subtitles. Offer `lively` (轻快) only when the brief targets a younger audience or the user asks for faster motion. Record the preset and every changed value in `MOTION_STYLE.md`.

| Item | `steady` (default) | `lively` |
| --- | --- | --- |
| Zoom per image | 100% → 106–108% over the full shot | 100% → 110–115% |
| Pan per image | ≤ 5% of frame width | ≤ 10% of frame width |
| Easing | ease-in-out, no bounce | ease-out allowed |
| Within-chapter transition | crossfade 0.5 s | crossfade 0.3 s or cut on beat |
| Chapter change | fade through black 0.8 s | whip/slide ≤ 0.4 s, at most one type |
| Hard cut | only on an emphatic narration beat | allowed on beats |
| Forbidden | rotation, shake, flash, glitch, spin, 3D flips | shake, flash strobe |

## Image motion rules

- Each image gets exactly one move: push in, pull out, pan left/right, or pan up/down. Choose from content: close-up of a person → slow push in; wide scene → pan along the main direction of the scene; reveal or ending → pull out.
- Alternate direction between neighbouring shots; never repeat the same move more than three shots in a row.
- Move from the start of the shot's audio range to its end; no still frames longer than 1 s unless the storyboard marks `hold`.
- Never move a face out of frame or into the subtitle zone.
- Images must have enough margin for the move. IMAGE_PROMPTS asks for compositions with the main subject away from frame edges and outside the subtitle zone; render images at least 10% larger than the output frame when the generator allows.

## Subtitles

- One sentence or clause at a time, timed to Doubao timestamps; never show text ahead of the voice.
- Default font: Source Han Sans / 思源黑体 Bold (or another font the user owns or that is free for commercial use). Record the actual font file and licence in `MOTION_STYLE.md`.
- Default size: about 5.5% of frame height for 16:9, about 4.5% of frame height for 9:16. White text, 3–4 px dark stroke, soft shadow. For `steady`, do not go smaller.
- Line length: 16:9 up to 18 Chinese characters per line; 9:16 up to 13. Prefer one line; never more than two.
- Position: 16:9 bottom centre with 8–10% bottom margin. 9:16 at roughly 68–75% of frame height, clear of the platform's bottom caption/UI area and right-side buttons (keep about 20% bottom and 15% right free).
- Subtitle appearance: fade in 0.15 s; no bouncing, typewriter, or per-character colour effects in `steady`.
- Keyword highlight (optional): at most one highlighted word per sentence, in the style's accent colour.

## Text cards (文字卡)

- Use for person names, places, dates/eras, key numbers, and book titles when the storyboard `text_card` column asks for one.
- Default: serif font (Source Han Serif / 思源宋体), upper-left or upper-right safe area, fade + 3% rise over 0.4 s, hold at least 2.5 s, fade out 0.3 s.
- Never overlap subtitles or faces. At most one text card on screen at a time.

## Opening and ending

- Opening hook (first 3 s): first image starts already moving (slightly faster push in is allowed even in `steady`), optional one title/hook card, no black frames before the first word.
- Ending: hold the last image 1.5–2 s with a slow pull out. Optional call-to-action card (for example the book title for book-selling videos) only when the brief asks for it.

## Music under motion

Transitions do not duck or swell the music unless `MOTION_STYLE.md` says so. Narration stays dominant.

## Pilot

In VISUAL_STYLE, after the image pilot is chosen, assemble a 10–15 s motion pilot from those pilot images with real Doubao audio if available (otherwise the voice audition sample). It must show one push, one pan, one within-chapter transition, one chapter transition, subtitles, and one text card. The user confirms the pilot before IMAGE_PROMPTS.

## Preview checks

Before showing the preview, check and list in `review/motion-qc.md`:

- every shot has a motion entry and it matches `MOTION_STYLE.md`;
- no subtitle collides with a face, a text card, or the platform UI safe area;
- no subtitle line exceeds the length limit or appears before its audio;
- no face leaves the frame during a move;
- no forbidden effect is present;
- transitions at chapter boundaries match the storyboard;
- representative frames at the opening, each chapter change, and the ending.

Machine checks do not replace a full human watch.

## Implementation

When HyperFrames is available, load its mandatory entry point and implement these rules through its routed animation, media, and caption instructions. Keep the motion values in one shared config derived from `MOTION_STYLE.md` rather than hard-coding them per shot, so a style change is one edit.
