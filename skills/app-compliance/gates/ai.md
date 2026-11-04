# AI gates

Applies when the app shows AI-generated text, images, audio or video, or lets people talk to an AI.
Using customer data to train models is PRIV-6, not here.
Evidence: [`research/03-app-accessibility-ip-and-ai.md`](../research/03-app-accessibility-ip-and-ai.md) section 7.

## AI-1 People know they are talking to an AI

- **Rule:** EU AI Act Art 50(1), applying from 2 August 2026, requires chat and agent systems to tell people they are interacting with AI, at the latest at first interaction, in an accessible way.
  The Commission's guidelines say a disclosure only in the terms, an invisible watermark, a generic "assistant" label, a human-like avatar, or a blanket "this site uses AI" does not suffice.
  California's BOT Act and Utah's AI law reward a clear upfront disclosure.
  California's companion chatbot law (SB 243, in force since 1 January 2026) requires, for any human-like bot able to meet social needs: an AI notice if a person could be misled, and a published suicide and self-harm protocol referring users to crisis services; for users known to be minors, also a reminder at least every 3 hours to take a break and that the bot is not human, and a block on sexually explicit content.
  Bots used only for customer service, business operations, productivity or analysis are outside SB 243.
- **Build:** A persistent "AI" badge on the assistant's identity and a first-message disclosure ("You're chatting with an AI assistant").
  No human name or photo for a bot.
  The bot answers truthfully when asked whether it is an AI.
  The disclosure is real text with an accessible name, not color or an icon alone.
  If the bot is companion-style, or might be: the SB 243 duties above, and whether it is a "companion chatbot" recorded as an owner question for a lawyer.
- **Done when:** a test opens the chat and finds the disclosure in the first assistant message and the badge on every assistant message; and the record shows the companion-chatbot question answered, with the SB 243 duties built and tested when the answer is yes.

## AI-2 Generated content is labelled and marked

- **Rule:** EU Art 50(2) requires providers to mark generated audio, image, video and text in a machine-readable, detectable way; Art 50(4) requires disclosing deepfakes, and AI text published to inform the public unless it had human editorial review.
  The Commission's guidelines (not the Act's text) treat short outputs such as captions, alt text, UI labels and source code as outside Art 50(2).
  California's AI Transparency Act (in force 2 August 2026; since SB 1000 on 30 September 2026 with no user threshold) requires latent disclosures in generated images, video and audio, carrying provider name, system name and version, creation time, a unique identifier and whether content was created or altered, permanent or extraordinarily difficult to remove; and a free verification tool, or a clear link to a compliant third-party one.
- **Build:** Generated images, audio and video carry C2PA Content Credentials with a `c2pa.created` action, `digitalSourceType` of `http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia`, and the California fields above.
  Image pipelines (resize, convert, CDN transforms) keep provenance metadata.
  A visible "AI-generated" label wherever such media or substantive generated text is shown.
  Generated text is stored with a generation flag and exposed in HTML (a `data-` attribute) and the API.
  A link to a verification tool from the UI.
  Two owner questions for a lawyer, recorded until answered: whether we are a California "covered provider" when we only call a third-party model's API, and whether C2PA metadata plus the linked tool meets the "permanent" and "compliant tool" tests.
- **Done when:** a test generates each media type and reads back, after the full delivery pipeline, a C2PA manifest with every California field; the visible label is present; generated text carries the flag; the verification link resolves; and both owner questions are in the record.

## AI-3 AI is never used to fake people or proof

- **Rule:** The FTC review rule bans AI-generated fake reviews, and presenting AI output as a named human invites Section 5 deception action.
  A July 2026 FTC proposed policy statement (not final) would also treat steering AI output toward undisclosed aims as possibly deceptive.
- **Build:** The agent generates no reviews, testimonials, personas presented as customers, or "team" members.
  AI capability claims follow CLAIM-1.
- **Done when:** every person, quote and rating shown in the app traces to a real source record.
