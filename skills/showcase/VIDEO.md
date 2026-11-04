# Demo video

The video is made by two committed scripts, so it can be made again after any change to the app.
The working reference is Fill Aloud: [`record_demo.py`](https://github.com/vipink1203/fill-aloud/blob/main/src/record_demo.py) and [`edit_demo.py`](https://github.com/vipink1203/fill-aloud/blob/main/src/edit_demo.py).
Start from them; adapt the takes and the cut list, keep the techniques.

## Record: `record_demo.py`

- Drive the real app with Playwright Chromium and capture it with a CDP screencast (`Page.startScreencast`), not Playwright's built-in video: the screencast gives every frame with its time, and the built-in video has no sound.
- Size the viewport for legibility in a 1920x1080 frame: the app sits on the left (for example 700x864 at device scale 1.25, giving 874x1080), a panel on the right.
- Every sound goes into a JSON timeline beside the take: `{at, seconds, who, text}` for the app's speech, the person's replies, and beeps.
  The edit is driven by this timeline, never by guessing times.
- Make the app's own speech audible: replace `speechSynthesis` in the page with a shim that asks the recorder to speak the text (macOS `say` to a WAV) and reports the real duration back, so the app waits as it would for a real voice.
- Speak the person's replies with a different `say` voice into a fake microphone (`getUserMedia` replaced); calls to the models are real, as in real use.
- One take per scene (for example `fill`, `spanish`, `upload`). Keep old takes in a folder rather than overwriting them.
- When a take fails, the app failed: reproduce it, fix the app, re-record. A stalled take is a bug a user would hit.
- Takes, narration and the video live in an ignored folder (`src/out/demo/`); none are committed.

## Narration and b-roll

- Narration: one generated clip per narration line (for example Higgsfield Seed Audio), trimmed of silence, named `n01.wav`, `n02.wav` and so on.
  Match its loudness to the app's speech, measured on the speech itself.
- B-roll is optional, only for the opening problem scene, never for the product.
  Label it on screen ("AI-generated footage") for as long as it plays.
- Disclose both in a footer on every app scene, for example: "Sample answers, not a real person. Waiting time shortened. Narrator's voice made with AI."

## Cut: `edit_demo.py`

- A **cut list** in code: shots (clip of a take from time t, freeze, full-frame image, b-roll), each quantized to whole frames at 30 fps, and sounds placed on one timeline.
- Keep every sound whole and shorten only the waiting between sounds; when picking a span of a take, end it before the next sound starts, so a cut never clips a word.
- Narration over app footage ducks the app's audio (about 0.2); if the line runs longer than the footage, freeze on a settled frame.
- Freeze only on a settled frame: never mid-transition, mid-fade, or on a blank page; check the raw take for the moment it settles.
- Draw panels, subtitles and cards as HTML in Playwright with the app's own font and colour tokens, then screenshot to PNG; one subtitle per sentence, `text-wrap: balance`.
- For architecture scenes, screenshot the project's architecture diagram (for example one made with archify) at device scale 2 with its toolbar hidden, and zoom onto the boxes each line is about.
- Mix sound in numpy at 48 kHz with 5 ms ramps at every edge, then `loudnorm=I=-16:TP=-1.5:LRA=11`.
- Render each shot to its own segment and join with the concat demuxer.
  End every segment's filter graph with `scale=out_range=tv,format=yuv420p,setsar=1`: screencast frames are full-range JPEG with an odd aspect ratio, and joining mixed formats silently drops shots.
- Fade in on the first shot, fade out on the last, mux with AAC and `+faststart`.

## Check

- **Frame check:** grab one frame every 6 seconds with direct seeks (`ffmpeg -ss T -i video -frames:v 1`), tile them into contact sheets, and look at every one.
  A `select` filter feeding `tile` misreports which frames exist; use seeks.
  Look for missing scenes, frozen transitions, cut-off text, orphan words, and anything that looks off; fix it in the cut, not by explaining it.
- **Sound check:** `volumedetect` over windows where narration should be (speech level) and gaps where it should not be (silence).
- Frame count equals the cut list's total; video and audio durations match to a frame.
- Length: under the event's limit; under 3 minutes when none is published, unless the content needs more and the owner agrees.
