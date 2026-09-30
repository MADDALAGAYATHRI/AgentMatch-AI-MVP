## Deployment

Run the Express server on a Node.js 22.13+ host and expose its configured `PORT`. The server serves the frontend and API from the same origin, so no separate frontend build or CORS configuration is needed. Persist the `data/` directory if added people and analyses should survive deployments. Configure secrets through the host's environment settings; do not deploy a populated `.env` file.

The app remains usable without `OPENAI_API_KEY` through its clearly labeled DEMO MODE. In the current build, LinkedIn and Instagram retrieval is intentionally disabled because authorized official API access is not configured. Therefore, the demo uses deterministic generated test data for profile attributes, agent conversations, compatibility scores, and rankings.

## Limitations

- LinkedIn and Instagram content is not automatically scraped in the current build.
- Source evidence remains empty when authorized retrieval is unavailable.
- Generated profile attributes and compatibility results are synthetic demo data.
- The application does not represent generated conversations as statements made by the real people.
- An authorized official API integration would be required for source-backed profile analysis.
- The current MVP does not bypass login, CAPTCHA, privacy controls, or other platform restrictions.

## License

This project was developed as an Agentic AI MVP / technical assignment demonstration.

Deployed URL LINK https://agentmatch-ai-mvp.onrender.com/
