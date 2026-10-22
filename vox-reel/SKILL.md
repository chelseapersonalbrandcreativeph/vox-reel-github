---
name: vox-reel
description: Design and animate vertical (9:16) explainer reels in the Vox "box" editorial motion style - paper and graph-paper grounds, yellow sticker tags, word-by-word kinetic type, red pill captions, hand-drawn strokes, page-peel transitions, black-grid list cards and halftone serif word drums - built and rendered with HyperFrames. Use when the user asks for a "Vox style", "box style", editorial explainer, paper-collage reel, or wants a short/reel/TikTok that feels "unscrollable" with graphic-only motion design (no presenter).
---

# Vox-style vertical reel

A reel in this style is a **printed page that keeps changing its mind**. Every half-second something is stuck on,
written in, highlighted, peeled away or swapped. Nothing glides, glows or floats. The viewer can't scroll because
the page never sits still long enough to be "done", but every individual element, once it lands, is dead still and
readable.

Built with HyperFrames (`/hyperframes`). Read that skill's contract first; this skill only adds the look, the
pacing and a kit of ready-made moves. The kit lives in the `kit/` folder next to this file; copy from it with
absolute paths.

Requires Node 18+ (HyperFrames runs through `npx hyperframes`). The HyperFrames plugin (`/hyperframes`) is recommended: it adds the render contract and review workflow this skill builds on.

## Why it works (the five forces)

1. **Constant micro-change (the 0.4 s rule).** A new visual event lands every 0.25-0.6 s: a word appears, a sticker
   slaps, a pill swaps, a line draws. The *layout* changes every 2-4 s. The eye is always rewarded, never bored.
2. **Words land on the voice, one at a time.** Headlines build word by word ("WHAT" -> "WHAT MAKES" -> logo ->
   "SO" -> "satisfying?"). The viewer reads at the speed of the narration, so reading *is* watching.
3. **Tactile, analog materials.** Off-white paper, graph paper, grain, torn-edge stickers, a felt-marker underline,
   a typewriter subline, halftone dots. It looks *made by hand*, so it feels human and trustworthy, not templated.
4. **Hard value contrast between scenes.** Light paper -> black grid -> graph paper -> photo cards -> black grid ->
   paper. Every layout change also flips brightness, which resets attention like a cut in a film.
5. **One accent with a job.** Yellow = "this is the subject" (sticker, highlighter, selection box). Red = "say this
   out loud" (pill captions, "*SCREENSHOT THIS*"). Never decorative, never both on the same word.

## Brand tokens

| Token | Value | Use |
| --- | --- | --- |
| `--paper` | `#F5F2EB` | default light ground (with 3-4% grain) |
| `--grid-paper` | `#E8E6E0`, lines `#CFCCC3` 1 px every 36 px | "notebook" scenes |
| `--night` | `#141414`, lines `#2A2A2A` 1 px every 72 px | list / resource scenes |
| `--ink` | `#262626` | every word meant to be read on light grounds |
| `--chalk` | `#F2F2F2` | words on night grounds |
| `--vox-yellow` | `#FFE81F` | sticker tags, highlighter, selection box, italic accent word on grid paper |
| `--pill-red` | `#D3242B` | caption pills, callouts |
| `--cyan` | `#33C6F2` | rare: the one italic accent word on the night ground |

Type (all bundled in HyperFrames except the two hand faces, which the kit ships as `@font-face` from Google Fonts):

| Role | Face | Setting |
| --- | --- | --- |
| Kicker caps ("WHAT MAKES") | Montserrat 600 | 54-64 px, tracking +0.12em, ink |
| Hero grotesk ("SECRET?") | Archivo Black | 140-180 px, tracking -0.01em |
| Serif accent ("satisfying?", "their") | Playfair Display 900 italic | 110-150 px, yellow on grid paper, ink on paper, cyan on night |
| Sticker word ("Vox") | Playfair Display 900 | on a yellow tag rotated -4 deg, 6-10 px rough edge |
| Halftone drum words ("SOUND") | Playfair Display 800 caps | 150 px; inactive = dot-filled + outlined, active = solid ink in a yellow box |
| Pill captions | Oswald 700 caps | 40-48 px white on red, radius 999, padding 10/26 |
| Typewriter subline ("TACTILE SOUND DESIGN") | Special Elite | 44-52 px, tracking 0.08em, typed 22-28 chars/s |
| Scribble annotation ("(kinda too)") | Caveat 600 | 44 px, with a hand-drawn arrow |
| List body ("PAPER MOVEMENT") | Oswald 500 caps / Inter 600 caps | 34-40 px, chalk on night |

## The frame types (pick 5-7 per reel)

| # | Frame | Ground | What happens |
| --- | --- | --- | --- |
| F1 | **Word-stack title** | paper | kicker caps word by word -> sticker slaps in -> hero word -> serif italic word -> marker underline draws |
| F2 | **Night punch** | night grid | one short line: cyan italic + giant halftone/outline word; a small object cut-out slides in from a corner |
| F3 | **Notebook reveal** | grid paper | arrives by **page peel**; yellow italic word over a hero grotesk word; typewriter subline types; sticker docks low-right, rotated |
| F4 | **Card grid** | paper with vignette | 2x2 rounded photo cards (radius 28) with caps labels; a red pill hops card to card, swapping words every 0.3-0.5 s; each image slowly pushes in (looks like video) |
| F5 | **Black-grid list** | night grid | caps title, 8-20 list rows type in fast (40-60 ms stagger), list scrolls up; red "*SCREENSHOT THIS*" pill pops at the side |
| F6 | **Resource rows** | night grid | logo chip + bold domain per row, rows land 0.25 s apart, red pill under them swaps words |
| F7 | **Word drum** | paper | stacked halftone serif words, a yellow box selects one, the drum steps up to center it, a hand arrow + scribble note writes in |
| F8 | **Payoff line** | paper | 2-3 line sentence built word by word, one word gets the yellow highlighter swipe; sticker sign-off |

Frame 0 is never empty: the first word and a texture are already on screen (it's the thumbnail).

## Motion vocabulary (implemented in `kit/scenes-*/`)

| Move | Numbers |
| --- | --- |
| `wordOn` - word appears | hard on (0 -> 1 in 1 frame) **or** scale 1.18 -> 1 in 0.16 s `back.out(2)`; never fade-slide-up |
| `stickerSlap` | scale 1.6 -> 1, rotate -14 -> -4 deg, 0.28 s `back.out(1.8)`, then a 2-frame 3 px jolt; badge pops 0.1 s later |
| `markerDraw` | SVG stroke dashoffset 100% -> 0 in 0.35-0.5 s `power2.out` (felt marker underline / circle / arrow) |
| `typeOn` | letter by letter at 24 chars/s, Special Elite |
| `highlight` | yellow bar scaleX 0 -> 1 from left, 0.22 s `power3.out`, sits behind the word at 70% of its x-height |
| `pillSwap` | red pill text swaps every 0.3-0.5 s on the narration chunk; each swap: scale 0.85 -> 1 in 0.12 s |
| `pillHop` | pill jumps to the next card: 0.18 s `power3.inOut` with 8 px horizontal blur |
| `pagePeel` | the outgoing page folds from the top-right corner along a diagonal in 0.55 s `power2.in`, the back of the page (grey, shaded) shows on the flap, revealing the next scene underneath |
| `listType` | rows appear 50 ms apart, hard-on; whole list then scrolls up at constant speed |
| `drumStep` | word drum moves up one row in 0.3 s `power3.out`; selection box snaps (no ease) |
| `imagePush` | photo scale 1.0 -> 1.06 across its whole on-screen time, linear, under 4% grain + 1-frame flicker |
| `onTwos` | graphics moves are quantized to 12 fps (every second frame) for the hand-animated, stop-motion feel; text reveals stay at full frame rate |

Rules:
- **Land and freeze.** A word that has landed never drifts, breathes or pulses. Motion moves to the next element.
- **Cut on the curve.** Scene changes happen at the fastest frame of a move (mid-peel, mid-whip), never after a fade.
- **Max 3 transition kinds per reel:** page peel, hard cut on a value flip, and a whip/pill-hop. No crossfades.
- **Layout reflows as words add.** When a stack grows, the whole stack re-centers in 0.2 s `power3.out`.
- Exits are fast (0.12-0.2 s) or are simply the next scene covering the old one.

## Pacing template (vertical, 22-30 s)

```
0.0-3.2   F1 word-stack hook (question). Frame 0 shows first word + texture.
3.2-5.6   F2 night punch: "it's not X" / "it's the ___"
5.6-9.5   F3 notebook reveal (via page peel): the answer in 2-3 words + typewriter subline
9.5-14    F4 card grid: 4 evidence cards, pill walks the story
14-18     F5/F6 black-grid list: timeline / resources / steps (screenshot bait)
18-22     F7 word drum: the category, with the subject selected + scribble aside
22-26+    F8 payoff line + sticker sign-off, hold >= 2 s
```

Vertical safe band (1080x1920): no text above y=168; all words between 168 and 1330 px; below 1330 only texture;
keep 100 px clear on the right for the action rail. Reading text >= 34 px. Max ~5 words per line.

## Sound

The style lives on **tactile foley**: paper slide on peels, a marker squeak on underlines, a sticker "thwack", a
soft typewriter tick on `typeOn`, a click/pop on pill swaps (every 2nd swap only). One light lo-fi or pizzicato bed
at ~95-110 BPM if available, ducked under any voiceover (0.14). Without a voiceover, the type is the narrator: keep
every line on screen for 0.5 s + 0.3 s/word.

## The kit (`kit/`)

| File | What it is |
| --- | --- |
| `index-pencil.html`, `index-explainer.html` | Root compositions of the two example reels. The `<head>` holds the whole design system: brand tokens, type-role classes (`.k-caps`, `.k-hero`, `.k-serif`, `.k-serif-i`), grounds (`.g-paper`, `.g-grid`, `.g-night`), `.sticker`, `.pill`, `.play-badge` (explainer), `.halftone`, `.pencil`-style photo cut-out, the print-grain overlay, and `window.VOX` helpers. Scenes inherit all of it. Their `<audio>` tags show worked SFX timing; the sound files themselves are fetched per project (step 4). |
| `VOX.twos(ease, dur)` | Quantises any GSAP ease to 15 steps/s: stop-motion "on twos" for stickers, objects and cut-outs |
| `VOX.peel(tl, pageSel, flapSel, at, dur)` | Real page-peel: clips the outgoing page along a moving diagonal fold and mirrors the lifted part onto a flap (back-of-paper gradient + drop shadow). The next scene's host must start `dur` seconds before this one ends, at a lower z-index. |
| `scenes-pencil/` | "Why are pencils yellow?" (29.7 s, with real photos): `hook` F1 word stack, `wood` F2 night punch + peel, `answer` F3 notebook reveal, `cards` F4 2x2 photo cards with hopping pill, `history` F5/F6 black-grid timeline + peel, `drum` F7 word drum, `payoff` F8 highlighter payoff |
| `scenes-explainer/` | "How are Vox-style videos made?" (28 s, words only): `hook`, `wonder` (halftone -> solid word + peel), `created` (typewriter + hand circle), `look` (portrait frames slapped down like prints), `best` (red strike-throughs + peel), `want` (sticker + selection box), `cta` (giant sticker + hand arrow) |
| `example-assets/` | Public-domain / CC images used by the pencil example (credits in `CREDITS.md`) |
| `fonts/` | Special Elite (typewriter, Apache 2.0) and Caveat (scribble, OFL) woff2; every other face is bundled in HyperFrames |
| `img/grain.png` | 512 px print-grain tile used by the root overlay (soft-light, 0.32, shifted every 2nd frame) |

Copy the scenes you need, change the copy and images, keep the numbers.

## Build steps

1. Write a script as **beats of <= 5 words** each; mark one subject word per line (yellow) and one say-it-out-loud
   chunk (red pill). Research the facts first; prefer "most" over a statistic you can't source.
2. Map beats to frame types with the pacing template. Alternate light/dark grounds.
3. Gather real imagery (public domain / CC0 / CC BY: Wikimedia Commons API with `iiurlwidth=1200`, Library of
   Congress, Openverse) into `assets/img/`. For a hero object, mask it out of a plain-background photo with a CSS
   `clip-path` polygon on a cropped band (the AI background remover is tuned for people and fails on objects).
4. Sound: tactile foley via `npx hyperframes media-use resolve --type sfx --intent "<page turn paper | marker pen
   squeak | sticker slap | typewriter key | pop | paper slide | mouse click | camera shutter>"`; music bed from
   Openverse (`license=cc0,by`) when HeyGen isn't signed in. Measure each file with `npx hyperframes audio <f>
   --json` and start it at `picture_time + 1 frame - moments.peak`. Spread SFX over tracks so none overlap.
5. `npx hyperframes init <name> --example blank --resolution portrait`. Replace `index.html` with
   `kit/index-pencil.html` or `kit/index-explainer.html` (then rewrite its scene hosts and `<audio>` tags), copy `kit/fonts` -> `assets/fonts`, `kit/img/grain.png` -> `assets/img/`, and the
   scene files you need into `compositions/`. Any scene using Special Elite / Caveat declares its own `@font-face`.
6. Timeline rules that bite: only `fromTo`; when an element's property is tweened a second time, pass
   `immediateRender: false` on the later tween or it overwrites the start state; SVG strokes start with
   `opacity: 0` so the round cap doesn't leave a dot; no CSS filters on photos.
7. `check`, `snapshot --review`, fix P0/P1, render with `--quality delivery`. Expected, deliberate warnings: text
   overlap mid-peel, yellow serif contrast (the ink offset shadow carries it), pill chunks under the read floor
   when a voiceover carries the sentence.

## Banned in this style

Glow, neon, gradients, glass cards, floating particles, fade-and-slide-up on every element, drifting landed
titles, centered-everything with no stickers or tilt, logos docked in a corner, more than one yellow focus per
frame, red used for anything but say-it-out-loud captions, crossfades between scenes, empty frame 0.
