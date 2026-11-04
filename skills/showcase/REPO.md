# README and repo

The working reference is the Fill Aloud README: [github.com/vipink1203/fill-aloud](https://github.com/vipink1203/fill-aloud).

## Layout, in order

1. Name as the title, a bold one-line pitch, then one sentence of what it does.
2. Three or four badges at most: license, language version, the main model or platform, the event.
3. A hero image of real app screens (below).
4. One line naming the event and track, with a link, and the tools the rules care about.
5. The problem, with one real quote from the people who have it, sourced.
6. What it does, as numbered steps a stranger can follow.
7. A screenshot row (a three-column table) with short captions, plus the real output (for example the filled form).
8. How it uses the sponsor's models: a table of model, what it does here, and a link to the code; then one line on how each output is checked.
9. How it works: the architecture diagram as an image, linking to the interactive HTML and the design doc.
10. What is proven and what is not, copied from the project's evidence, with the scripts that show each.
11. Privacy: what leaves the computer and what does not.
12. Run it, tests, cost, debugging, repository layout, license and asset licences.
13. Keep any section another tool reads, such as a dashboard or a docs site.

Write plain sentences, one per line; no em dashes; then read it once more for signs of AI writing (inflated words, stacked adjectives, vague claims) and rewrite them plainly.

## Screenshots

- Take every screenshot from the recorded takes (`ffmpeg -ss T -i take.mp4 -frames:v 1`), at moments found in the take's timeline: a read-back on screen, an answer, the finished output.
- Look at each one before using it: a screen showing a glitch or a defect is a bug to report, not a screenshot to use; pick a clean moment and tell the owner about the defect.
- Hero: three screens side by side on the app's own background colour (sample it from a frame), padded evenly, faded into the background at the bottom where the cards are cut, and the fade must not dim the key content.
- Diagram: screenshot the diagram's HTML with any toolbar hidden, clipped to the title and drawing by measured bounds, not a fixed crop.
- Put images in `docs/images/` and keep only the ones the README uses.

## Before it goes public

- Scan the whole history, not just the tree: keys (search for the start of the real key), `.env`, voice or video recordings, uploaded user files, debug folders, local absolute paths.
- Ignore receipts that record local paths (for example archify's `architecture.*.json`).
- Sample data is visibly made up and says so.
- Commit authorship and co-author lines follow the owner's instructions; ask when none are given.
- Set the repo's description and topics; after a rename, check the old URL redirects and update the local remote.
- Run the project's tests and lint after the last code change.
