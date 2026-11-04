---
name: showcase
description: Make a project's public showcase - a demo video cut from recordings of the real running app, with AI narration and labelled AI b-roll, plus a professional README with real screenshots, a name check and a clean public repo. Use when preparing a hackathon or launch submission, making a demo video of an app, or making a repo or README look professional.
---

# Showcase

A **showcase** is everything a stranger sees of a project: the demo video, the README, the repo page.
Every frame and every claim comes from the real app and the project's proven evidence; nothing is mocked up.
Say only what the project has shown: when it keeps a list of what is proven and what is not, every claim comes from the proven part; when it keeps none, write that list first, with the test or script behind each line.

## Steps

1. **Rules.** Find the event's or launch's own rules: what to submit (repo, video host, length, fields), judging criteria with weights, deadline with time zone, rules on AI-generated content.
   Read the primary pages (with a research skill, if you have one); when a page needs a login, say so and name what could not be checked.
   Done when every criterion is mapped to the scene or README section that serves it.
2. **Name.** Ask whether the project's name is a product name or only a category ("Accessible PDF Forms" is a category).
   If it is a category, search for clashes and offer two or three names with the owner; the owner picks.
   Done when the name is settled, before any frame or screenshot shows it.
3. **Script.** Write `docs/demo-video.md`: scenes in order, each tagged with the criterion it serves, narration one sentence per line, and a "Lines never to say" list copied from the project's can't-claim list.
   Done when every narrated number is under Proven in the README.
4. **Video.** Record the real app and cut the video by following [VIDEO.md](VIDEO.md).
   Done when the frame check and the sound check in VIDEO.md both pass on the final file.
5. **README.** Rewrite the README by following [REPO.md](REPO.md), with screenshots taken from the recordings.
   Done when every link and image resolves and the page has no em dash.
6. **Repo.** Before anything goes public, run the hygiene checks in [REPO.md](REPO.md#before-it-goes-public).
   Making a repo public, renaming it, and pushing are the owner's calls: ask, then do exactly that.
   Done when the public page shows the new README and its images load for someone signed out.
7. **Hand-off.** Give the owner the upload steps for the video host, including its AI-content question, and the one link still missing from the README.

## Spend

Paid generation (narration voice, b-roll, model calls during recording) is spent once: preflight its cost, cache every output, and never pay again for a re-render.
A re-cut of the video re-uses the takes and the narration; only a change to the app itself needs a new take.
