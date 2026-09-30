# Submission notes

## Overall explanation (under 200 characters)
AgentMatch pairs profile signals, simulates opt-in agent introductions, and ranks matches. Demo traits are synthetic; pasted source text can be analyzed with an optional LLM.

## Technical section (under 500 characters)
No Instagram or LinkedIn scraping is used. The app accepts HTTPS profile URLs as references and analyzes only text a user explicitly pastes. Express 5 validates and stores profiles in SQLite; optional server-side OpenAI Chat Completions extracts interests and evidence from supplied text. Matching uses transparent tag overlap. Demo profiles and conversations are synthetic and labeled as such.

## Three-minute recording outline

- **0:00–0:20 — Start the demo:** Show 30 records and point out the synthetic-data label.
- **0:20–0:55 — Inspect profiles:** Open two profile pages; show both profile links, interests, hobbies, analysis mode, and evidence/unavailable fields. State clearly that link URLs are not fetched.
- **0:55–1:45 — Watch the agents date:** Return to Overview, run the full demo, and advance through several of the per-person date simulations. Show the conversation proposing an opt-in, low-pressure introduction.
- **1:45–2:25 — Rankings:** Open Rankings, select a person, run the match engine, and explain the shared-tag score and its limits.
- **2:25–3:00 — Add a person:** Enter name plus LinkedIn and public Instagram URLs; explain that actual analysis requires permitted text pasted by the user and a configured server-side API key. The links alone do not yield profile facts.

## Availability

The project is a local Node application. No public GitHub repository, hosted demo URL, or recorded/YouTube video is configured in this workspace. Do not submit placeholder links as if these deliverables exist.
