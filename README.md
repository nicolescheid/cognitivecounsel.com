# Cognitive Counsel

> A thinking tool for examining a recurring pattern in yourself.

[cognitivecounsel.com](https://cognitivecounsel.com) — the sister site to [Cognitive Council](https://cognitivecouncil.com). **Council** helps with the specific decision in front of you; **Counsel** is for the pattern that turns up across a lot of them — the thing you catch yourself doing again and again.

It isn't a chatbot, and it won't tell you who you are. The looking stays yours: you name a pattern, the tool points to the cognitive tendencies that *might* sit underneath it and the established exercises you can use to examine it yourself. A map and a librarian, never an oracle.

## How it flows

1. **Welcome** — what the tool is (and isn't).
2. **Query** — name a pattern you keep noticing ("Why do I always…").
3. **Socratic intake** — the tool privately reads your pattern and generates 4 tailored questions: a concrete recent instance, where else it shows up (breadth), what it might protect or cost (function), and your history with it. *You* do the looking; answers stay in your browser.
4. **Guide** — two things, neither a verdict about you:
   - **What might be underneath** *(conditional)* — when a well-established mechanism is genuinely relevant, it's surfaced as a tappable primer. Framed as a possibility ("might"), never the explanation for who you are. Skipped when nothing clearly fits.
   - **Exercises to examine it yourself** — 2–3 established techniques for looking at a pattern (ABC / functional analysis, values clarification, behavioural experiments, if-then plans), drawn from named traditions (CBT, ACT, behavioural science), each with a "why this might fit" from your own words.
5. **Exercise** — step through a chosen exercise interactively, filling it in yourself. At the end you see your own words back, with a closing question (never an interpretation), and can copy or download your work.

### Design principles ("the line we hold")

This is the **dispositional** sibling of Council's situational tool, built to the same anti-oracle rules:

- **The engine reasons, but never narrates a verdict about the user.** It picks which primers and exercises to surface; it does **not** name, diagnose, or "illuminate" your pattern. You named it — the tool helps you investigate it.
- **Hypotheses, not diagnoses.** Mechanisms are always "what *might* be underneath."
- **Whitelist of mechanisms.** The model may only name mechanisms in the vetted, static primer set (`primers` in `index.html`, shared verbatim with Council). Keeps replication-failed pop-neuroscience out by construction.
- **Established, not outdated.** Exercises are recognised techniques in current use; a `BLOCKLIST` excludes discredited ones.
- **Open loop.** The exercise leaves with you. The AI never grades or interprets your answers.
- **House style.** Copy and generated text follow `HOUSE_STYLE` (shared with Council) to avoid AI-writing tells.

### What changed from v2.4

The old Counsel was an oracle: it *detected and named your patterns* ("The Permission Seeker…"), had five voices *illuminate* them, and leaned on a "probably right but not ready to admit it" flinch signal. That whole engine is gone. The intake survives, reframed; everything downstream is now education + self-directed exercises. The Council→Counsel token handoff is also removed — the two are sister sites that link to each other, not a funnel.

## Tech

Single-file static site — no build step required.

- React 18 (UMD, in-browser) · Babel standalone · Tailwind (CDN) · jsPDF · marked + DOMPurify

Backend dependency (shared with Council):
- `api.cognitivecouncil.com/api/chat` — Anthropic Claude API proxy. The client sends the full prompt in `message` with a `systemRole` label (`intake_analyst`, `question_generator`, `guide_select`, `exercise_build`).

## Running locally

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`. API calls hit the production backend, so you need network access for intake and exercises to generate.

## Privacy

Your answers and exercise responses stay in your browser (localStorage). Intake questions and exercise scaffolds are generated through Anthropic's Claude API; nothing you write is stored by this application. Anthropic retains API conversations for 30 days for safety monitoring — see their [privacy policy](https://www.anthropic.com/legal/privacy).

Google Analytics is loaded only after user consent via the cookie banner.

## Credits

Created by Nicole Scheid & Claude (Anthropic).

## License

[MIT](LICENSE)
