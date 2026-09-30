# AgentMatch AI — functional MVP

AgentMatch is a local demo for profile analysis, simulated agent introductions, compatibility scoring, and rankings. The supplied directory retains 30 people and their LinkedIn and Instagram URLs.

## Source Collection

The app accepts exactly the supplied LinkedIn and Instagram profile URLs as source references. It validates those URLs, keeps the links clickable, and maintains a separate `sourceStatus` (`retrieved` or `unavailable`) and source-specific evidence list for each source.

Automated collection from LinkedIn or Instagram is **disabled** in this build. LinkedIn's current User Agreement prohibits automated scraping/copying of profiles, and Meta states that automated collection from its products without permission violates its terms. No authorized official profile-content API credentials or permissions are configured here. The server therefore makes no HTTP requests to those social platforms, records both source statuses as `unavailable`, keeps evidence arrays empty, and explains that the demo fallback is in use. A future authorized official API integration may populate evidence; it must use only the two supplied sources.

The system does not bypass authentication, login, CAPTCHA, private-account settings, access controls, redirects, or rate limits. It does not use Google/search results, Wikipedia, news, Crunchbase, or any other site as profile information. Official policy references: [LinkedIn User Agreement](https://www.linkedin.com/legal/user-agreement) and [Meta on automated collection](https://about.fb.com/news/2021/04/how-we-combat-scraping/).

## DEMO MODE

When authorized source retrieval or AI analysis is unavailable, the app uses **DEMO MODE — GENERATED TEST DATA**. The 30-person directory remains available, but generated interests, hobbies, communication signals, conversations, compatibility scores, and rankings are synthetic. They are not claims about the named people and are never labeled source-backed. The UI shows `Public source unavailable — using DEMO MODE for demonstration.` and records why each source is unavailable.

The source-analysis endpoint and profile UI are ready to display source-specific evidence/status and source-backed AI interpretations if an authorized official API adapter is configured. The current build cannot produce source-backed profiles from the LinkedIn/Instagram URLs alone.

## Architecture

- **Frontend:** responsive single-file UI in `agentmatch-prototype.html`.
- **Backend:** Express 5 API in `server.js`.
- **Storage:** SQLite at `data/agentmatch.sqlite`; added people and profile analysis/status/evidence persist across restarts.
- **LLM:** optional OpenAI-compatible Chat Completions call. It is used only after both authorized source evidence arrays are populated. The server prompt limits analysis to those excerpts and rejects evidence quotes that are not exact excerpt matches.
- **Source adapter:** explicitly disabled until authorized official LinkedIn and Instagram API access is configured. No social platform requests or login automation are performed by this build.

## API

- `GET /api/health` — backend status, people count, and LLM configuration.
- `GET /api/people` — all 30 directory records and locally added people with profile, `sourceStatus`, and `sourceEvidence`.
- `POST /api/analyze-profile` — accepts `name`, `linkedin`, and `instagram` (plus optional existing person `id`); validates and stores the references, returns source status/evidence, profile fields, mode, and fallback explanation. Because authorized retrieval is not configured, the current endpoint returns empty evidence and a labeled demo profile.
- `POST /api/date` — returns the existing multi-turn AI agent simulation, shared signals, differences, compatibility score, and data-mode label.
- `POST /api/rank` — returns a sorted match ranking for a selected person; each result identifies its mode.
- `POST /api/demo/run` — generates one demo date per person and rankings for the first record.

## Local setup

Requirements: Node.js 22.13 or newer (uses the built-in SQLite module).

1. Keep `server.js`, `agentmatch-prototype.html`, `package.json`, and `attached_assets/` together.
2. Optionally set `OPENAI_API_KEY` in a local `.env` file. Never commit `.env` or put the key in browser code. An LLM key alone does not enable social-source retrieval.
3. Run `npm install`, then `npm start`.
4. Open `http://localhost:3000`.

## Demo flow

1. Click **RUN FULL DEMO** to load all 30 profiles, date simulations, and initial rankings.
2. Open **People**, choose **View profile**, then **Analyze Profile**. Review the per-source unavailable status, the explicit fallback message, and the synthetic analysis labels.
3. Choose **Start Dating** to open the existing Agent A/B conversation and compatibility result.
4. Open **Rankings**, select a person, run the match engine, then choose **View Date**.
5. Use **Add Person** to submit a name and both URLs. The same `/api/analyze-profile` status and demo-fallback behavior runs for new entries.
