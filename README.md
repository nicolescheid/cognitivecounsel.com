# Cognitive Counsel

> Pattern illumination through five cognitive systems.

[cognitivecounsel.com](https://cognitivecounsel.com) — the sister site to [Cognitive Council](https://cognitivecouncil.com). Where Council gives you **multiple perspectives on your question**, Counsel turns the mirror around and illuminates the **patterns underneath** — the things you can't see about yourself because you're inside them.

It's designed to be used after Council (a "from=council" handoff carries your session and reactions through), but also works as a direct entry point if you want to go straight to pattern work.

## How it flows

1. **Loading / Gate / Transition** — three mount-time entry points:
   - **Transition**: arriving from Council via `?from=council&t=...` — your Council session is restored and a "Why do I…" pattern question is pre-suggested.
   - **Gate**: no Council history detected — encourages starting with Council first, with an option to skip ahead.
   - **Intake**: returning visitor or skip-ahead — direct entry into pattern work.
2. **Counsel Socratic intake** — 2-3 short threshold questions tailored to whether you came from Council.
3. **Pattern detection** — the system reads your full context and identifies 1-3 distinct patterns operating in your question, each named and described in a single line.
4. **Pattern selection** — you choose which pattern to explore first. Already-explored ones are marked so you can come back for the others.
5. **Stepped illumination** — the five systems analyse the chosen pattern in parallel, then reveal one card at a time so you can sit with each before moving on.
6. **Full overview** — see all five at once, copy/PDF, return to other detected patterns, or take a new question to Council.

## The five systems

Each system has the same role as in Council, refocused on pattern recognition rather than decision support:

| System | Pattern lens |
|---|---|
| 🧠 **Prefrontal Cortex** | Decision patterns, strategic blind spots |
| ❤️ **Limbic System** | Emotional patterns, what you avoid feeling |
| ⚙️ **Basal Ganglia** | Behavioral patterns, the gap between what you say and do |
| 🌊 **Default Mode Network** | Identity patterns, the story you live without knowing it |
| ⚡ **Salience Network** | Attention patterns, what you focus on to avoid what matters |

## Tech

Single-file static site — no build step required.

- React 18 (UMD, in-browser)
- Babel standalone (in-browser JSX transform)
- Tailwind CSS (CDN)
- jsPDF (PDF export)
- marked + DOMPurify (sanitised markdown rendering)

Backend dependencies (separate services):
- `api.cognitivecouncil.com` — Anthropic Claude API proxy (shared with Council)
- `transfer.cognitivecouncil.com` — short-lived session token store for the Council → Counsel handoff

## Running locally

It's just an HTML file:

```bash
python -m http.server 8000
# or
npx serve .
```

Then open `http://localhost:8000`.

API calls hit the production backend, so you need network access for the systems to actually respond.

## Recent changes (v2.4)

- **Parallel pattern analysis** — the five systems now examine your pattern concurrently (previously sequential, ~2-3 min wait → ~30-45s with progressive feedback).
- **Per-card retry** — individual systems can be retried if they fail without redoing the whole illumination.
- **Exponential backoff** in `callAPI` for transient errors.
- **Toast notifications** replace the old `alert()` dialogs.
- **DOMPurify** sanitisation on all rendered markdown.
- **Session persistence** — in-progress state saved to localStorage with a resume banner on return (24h TTL). The longer multi-step Counsel funnel (intake → questions → detection → selection → illumination) is no longer destroyed by a stray refresh.

## Privacy

Conversations are processed through Anthropic's Claude API. No data is stored by this application. Anthropic retains conversations for 30 days for safety monitoring — see their [privacy policy](https://www.anthropic.com/legal/privacy).

Google Analytics is loaded only after user consent via the cookie banner.

## Credits

Created by Nicole Scheid & Claude (Anthropic).

## License

[MIT](LICENSE)
