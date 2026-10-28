# QOLDAN v0.3 — clean deployment repository

Interactive learning prototype with Explorer / Researcher modes, engineering simulations, knowledge-transfer challenge and optional AI feedback from OpenRouter.

**Important:** Do not put any API keys in GitHub, HTML, JavaScript, screenshots, or this README. Add the `OPENROUTER_API_KEY` environment variable in the Netlify UI.

## Repository layout

```text
qoldan-launch/
├── netlify.toml       (publish = "public")
├── public/            (site to publish)
│   ├── index.html
│   ├── app.js
│   ├── styles.css
│   ├── qoldan-logo.webp
│   └── favicon.svg
├── netlify/
│   └── functions/
│       └── ai.mjs    (secure backend)
├── .gitignore
├── START_HERE_RU.md
└── README.md
```

There is **no** `site/`, `dist/`, `package.json` or `npm run build` step. Netlify publishes the existing `public/` folder directly and deploys `netlify/functions` separately.

## Deploy

1. Create a **new PUBLIC** GitHub repository and push the exact files shown above with folders intact. Keep all API keys out of Git. Public GitHub avoids Netlify's private-repository deploy restriction for unrecognized contributors.
2. In Netlify: **Add new project → Import an existing project → GitHub → select repository**.
3. Branch: `main`. Base directory: blank. **Build command: blank**. Publish directory: `public`. Deploy. (The root `netlify.toml` sets publish and functions paths.)
4. Confirm homepage works on phone and laptop. Confirm `/.netlify/functions/ai` responds with 405 for GET: this means the function exists and accepts POST only (not a missing endpoint).
5. Under **Project configuration → Environment variables** add `OPENROUTER_API_KEY` with the **NEW**, unshared key; use default/all scopes on Free plan. Trigger a new deploy to apply it.
6. Open Researcher mode, write scientific background, and click **Check reasoning**. Make sure you get a real response. If rate-limited, the built-in mission still works.

See **START_HERE_RU.md** for detailed steps, troubleshooting and security.

## Science model

Idealised battery and constant-resistance circuits: `I = V/R`; `P = V×I`; `E = V×Ah`; `runtime = E/P`. The 20 W minimum is a fictional engineering constraint, not a universal illumination standard. The initial correct module is 6 Ω and the independent transfer challenge is 8 Ω.

## Data and limitations

LocalStorage holds anonymous results in the user's browser; downloading a JSON report is manual. No accounts, subscriptions or automatically collected telemetry. When AI is used, submitted text is transmitted to OpenRouter and a third-party model provider, so users must avoid sensitive or identifying information. AI feedback is formative, not a verified scientific grade.

OpenRouter free routing (`openrouter/free`) is rate limited and not guaranteed available. AI endpoint uses best-effort in-memory rate limiting, which is NOT a globally reliable abuse prevention control. Suitable for a small supervised pilot; add real distributed rate limiting and abuse prevention for a larger public launch.
