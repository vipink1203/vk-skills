# vk-skills

**Agent skills for shipping real apps: pick the right idea, pass the legal gates, and show the work.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Skills: 3](https://img.shields.io/badge/skills-3-2ea44f)](#skills)
[![Works with Claude Code](https://img.shields.io/badge/works%20with-Claude%20Code-D97757)](#install)
[![skills.sh](https://img.shields.io/badge/install-npx%20skills-000000)](https://github.com/vercel-labs/skills)

Three skills that cover a project's life outside the code: choosing what to build, making it safe to put in front of real people, and presenting it to strangers.
Each one is a step-by-step procedure with a "done when" check at every step, so the agent does the same thorough work on every run instead of stopping when it feels finished.
They work with any agent that reads [Agent Skills](https://github.com/vercel-labs/skills) (`SKILL.md` folders), and were built and used with Claude Code.

## Skills

| Skill | Use it when | What you get |
| --- | --- | --- |
| [**hackathon-ideas**](skills/hackathon-ideas/SKILL.md) | Choosing what to build for a hackathon, or stress-testing candidate ideas | A ranked shortlist of ideas that each solve a real problem at its root, with evidence links, scores against the official judging criteria, a demo script and the riskiest assumption to test first |
| [**app-compliance**](skills/app-compliance/SKILL.md) | Before an app reaches real users, and whenever a change touches personal data, cookies, signup, payments, emails, marketing copy, dependencies or AI features | A compliance record: a data map built from the code and live traffic, and a pass or fail on every gate for privacy, consent, terms, payments, claims, accessibility, licenses, user content and AI labelling |
| [**showcase**](skills/showcase/SKILL.md) | Preparing a hackathon or launch submission, making a demo video, or making a repo look professional | A demo video cut from recordings of the real running app with narration and captions, a README with real screenshots, a name check, and a repo checked clean before it goes public |

They chain: `hackathon-ideas` picks the idea, `app-compliance` makes it safe to launch, `showcase` presents it.

## Install

**With the skills CLI** (Claude Code, Codex, Cursor and other agents):

```sh
npx skills add vipink1203/vk-skills
```

Add `-g` to install for every project, or `--skill showcase` to install one skill.

**As a Claude Code plugin:**

```text
/plugin marketplace add vipink1203/vk-skills
/plugin install vk-skills@vk-skills
```

**By hand:** copy a folder from [`skills/`](skills/) into your project's `.claude/skills/` (or `~/.claude/skills/` for every project).

Then ask for what you need in plain words, for example "find hackathon ideas for this event", "run the compliance gates on this app", or "make the demo video and README for the submission".
The agent picks the matching skill from its description; you can also call one by name, such as `/showcase`.

## How they are written

- **Primary sources only.** Every fact about a hackathon comes from its official pages, and every compliance rule cites the law or regulator page it was checked against, in [`skills/app-compliance/research/`](skills/app-compliance/research/), dated 2026-10-31.
- **Done when, not done-ish.** Every step ends on a check the agent can verify, such as "the code search and the traffic capture show nothing absent from the data map".
- **Evidence or nothing.** A claim, badge or number in an app, a README or a demo video must point at a test, a script or a source that shows it.
- **The owner decides.** The agent drafts and checks; signing, registering, publishing and legal judgement stay with a person, and the skills say so where it matters.

`app-compliance` is engineering against researched law, not legal advice.
When its research notes are more than six months old, the skill tells the agent to re-check the sources it relies on.

## In practice

[Fill Aloud](https://github.com/vipink1203/fill-aloud), which fills in any PDF form by talking, was chosen with `hackathon-ideas` for the Meta Global AI Developer Hackathon 2026, and `showcase` is the process that made its demo video and README, written down.

## Also worth installing

Skills by other authors that these pair well with:

- [emilkowalski/skills](https://github.com/emilkowalski/skills): interface and animation craft.
- [mattpocock/skills](https://github.com/mattpocock/skills): engineering workflows, including research, TDD and specs.
- [tt-a1i/archify](https://github.com/tt-a1i/archify): architecture diagrams, which `showcase` uses for its "how it works" scene.
- [heygen-com/hyperframes](https://github.com/heygen-com/hyperframes): HTML-to-video compositions, for motion graphics beyond a screen recording.
- [wheresryan22/anatomy](https://github.com/wheresryan22/anatomy): interactive isometric figures that explain a system.

## Contributing

Issues and pull requests are welcome.
A change to a skill keeps its shape: numbered steps, each ending on a "done when" check, and any new fact linked to a primary source.

## License

[MIT](LICENSE).
