---
name: hackathon-ideas
description: Find, cut and rank hackathon project ideas that solve a real, specific problem at its root, against a specific hackathon's rules, tracks, judging criteria, required tech and deadline. Use when choosing what to build for a hackathon, or when comparing or stress-testing candidate hackathon ideas.
---

# Hackathon ideas

We build ideas that solve a real problem at its **root cause**, for a specific person, backed by **evidence** that the problem exists, and resting on an **insight**: the non-obvious fact that makes this solution work where the usual approaches fail.
Small and simple is welcome; common is not.
An idea earns a place only when it would still matter after the hackathon, and a judge could not have guessed it from the track name.

A hackathon is won on its **judging criteria**, inside its **deadline**, through a **demo moment**: the few seconds of the video or live demo where a judge sees the thing work and gets it.
Every fact about the hackathon comes from its official pages, cited by link.

## Steps

1. **Read the brief.** From the official hackathon page, rules and FAQ (ask for the link if you don't have one), record with source links: tracks and prizes, judging criteria and their weights, required or sponsor technology, eligibility and rules that disqualify (team size, pre-existing code, region, licensing), submission requirements (video length, repo, live demo, write-up), and the deadline with the time left.
   Then ask the user, in at most 3 questions, what the brief cannot tell you: team size and skills, hours available, and any domain they know first-hand or a track they lean toward.
   Done when every field above has a cited value or is marked "not published".
   When no judging criteria are published, use four equal criteria common across hackathon rubrics (idea originality, technical implementation, potential impact, design and presentation), and label them as our fallback in the output.
2. **Write the obvious list.** Before any research, write the 10 ideas most teams will submit for these tracks and this tech: the first things anyone would say.
   These ideas, and anything that is a light variation of them, are struck in step 5.
3. **Find real problems.** This is the deepest step; spend the most effort here.
   Go where people describe their problems in their own words, inside the domains the tracks and the team's first-hand knowledge point to: forums, subreddits, GitHub issues, support and community threads, app store reviews, professional groups, public complaints and regulator reports.
   Look especially for **workarounds**: spreadsheets, scripts, manual double entry, printouts, group chats, paid assistants doing a machine's job; each workaround marks a problem people already pay for with time.
   For each problem, ask why until you reach a structural cause, not a symptom.
   Done when the notes hold at least 10 distinct problems, each with a specific person and situation, at least one quote or data point with a link, the workaround they use today, and the root cause.
4. **Research the field.** Read past winners of this hackathon or series (its project gallery, for example on Devpost), the sponsor's recent launches and stated wishes for the required tech, and any public submissions already in this edition.
   Done when the notes list at least five past or current projects and the sponsor's stated priorities, all with links.
5. **Generate, then cut hard.** Write at least 20 ideas, each built from one problem in step 3.
   Each idea names: the person and situation, the evidence link, the root cause it removes, the insight, what it does, its demo moment, and what the required tech contributes that the solution could not do without.
   Then strike, with a one-line reason each, every idea that:
   - is on the obvious list or a light variation of it;
   - cannot name a specific person and situation, or has no evidence link;
   - treats a symptom while the root cause stays in place;
   - is a thin wrapper, where the required tech or AI could be swapped for a form, a search box or a template with little loss;
   - has an insight anyone would say first;
   - closely matches an existing product, a past winner or a current submission (search for its nearest neighbours and record them);
   - breaks a rule, or cannot reach a working demo moment in the time left with this team's skills.
   Done when every idea is struck with a reason or kept, and at least five are kept; when fewer survive, go back to step 3 for more problems rather than loosening the cuts.
6. **Score the survivors.** Score each kept idea 1 to 5 on every judging criterion, with the hackathon's weights and a one-line justification per score, plus three of our own: depth (strength of the evidence and how fully it removes the root cause), buildability in the time left, and demo strength.
   Rank by the weighted judging score plus depth, breaking ties on buildability.
7. **Write the shortlist.** For the top three, write:
   - **Pitch**: one sentence a judge would repeat.
   - **The problem**: the person, the situation, the evidence quotes with links, today's workaround, and the root cause.
   - **The insight**: the non-obvious fact, and why existing tools miss it.
   - **Nearest neighbours**: the closest existing products or projects found, and the concrete difference.
   - **Targets**: track and prizes it competes for.
   - **Scores**: the scoring table from step 6.
   - **Demo script**: what happens in the first 30 seconds of the video, showing the person's problem and then its removal.
   - **Cut line**: what must work for the demo, and what is nice to have, so the team knows what to drop when time runs short.
   - **Riskiest assumption**: the technical or product bet most likely to fail, and a spike of an hour or less that tests it before committing.

## Output

Write one file per hackathon at `docs/hackathons/<event-slug>.md`, updated in place on later runs: the brief with links, the obvious list, the problem notes with evidence, the field research, all generated ideas with their strike reasons, the scoring table, and the shortlist.
In the session, show the shortlist and the deadline, then ask the user to pick one idea.
When the team commits to an idea, it passes the `app-compliance` skill before anyone outside the judges uses it, and the `showcase` skill makes its demo video and README for the submission.
