---
name: video-edit
description: Turns one raw talking-head take into a finished vertical short video (1080x1920) for Instagram Reels or YouTube Shorts. Times words with Whisper, cuts pauses and retakes, storyboards beats from moves.md, renders graphics that change on exact words, checks safe zones with screenshots, mixes music, and exports final.mp4 with the cut list. Use when the user says "edit my video", "make a reel", "video-edit", or shares a raw take.
---

# Video edit

## Goal
Turn the raw take into a finished video of the asked length for the asked audience.
One take in, one file out. A plan or a still frame is not the deliverable.

## Inputs to confirm first
- Raw take file, target length in seconds, audience.
- If any is missing, ask before starting.

## Folder
```
my-video/
  raw-take.mov    one take, mistakes fine
  references/     5 outlier videos
  moves.md        built on the first run
  brand.md        colours, font, captions
  notes.md        every note, as a rule
  best.mp4        the edit to beat
```
Read brand.md, moves.md and notes.md before any work. Rules in notes.md win over this file.

## Tools (this cloud setup is Linux)
- ffmpeg (installed), Node + Playwright with Chromium (installed, do not reinstall).
- Whisper: `faster-whisper` in Python, `word_timestamps=True`.
- On a Mac instead: `brew install ffmpeg node`, `pip3 install mlx-whisper`, `npm install puppeteer`.

## References (first run, or when references/ changes)
- Outliers only: 5x that creator's usual views.
- Pull one frame per second (`ffmpeg -vf fps=1`) and the transcript of each.
- List the hook, the pace (cuts and graphic changes per 10s) and the layouts.
- Keep moves seen in 2+ videos. Save them to moves.md.

## Workflow
1. Whisper times every word. Save words.json.
2. Cut pauses to 0.25s, only in true silence (check audio level, not just word gaps), and drop retakes. Keep every word whole. Show the cut list first and wait.
3. Storyboard: one still per beat, from moves.md. Wait for a yes before any render.
4. A new graphic every 2 seconds, top half, face below. Each one changes on its exact word.
5. Each object slams in on its word and lands with no bounce (fast ease-out, no overshoot).
6. Real app icons and real screens, never a stand-in. If one needs a login, ask the user for a screenshot or screen recording. Never ask for passwords.
7. Turn the first sentence into the hook, animated on the words.
8. Music 12 dB under the voice.

## Checks (run them, do not just claim them)
- Screenshot every 0.25s. Flag overlaps and crops, fix, then check again.
- Nothing in the top 220px, the bottom 400px or the 130px button column on the right.
- Put it beside best.mp4. Count graphic changes. Fewer than best.mp4? Add beats and render again.

## Notes
The user gives one note at a time. Save each to notes.md as a rule for every video.

## Export
H.264, 1080x1920, -14 LUFS (`loudnorm=I=-14`). Save as final.mp4 with cutlist.md beside it.
