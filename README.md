# ShipLog 📦

> Your package tracking history becomes a commit log. Every status change is a git commit in your own repository.

You have pasted a tracking number into a random third party website before. You likely wondered what happened to that data. This is an alternative: self-hosted tracking that runs as your own agent. It lives in your repository, runs on your Cloudflare account, and communicates directly with carrier APIs when you tell it to.

**Live demo:** https://the-fleet.casey-digennaro.workers.dev/shiplog

---

## Why This Exists
Most package trackers sell your location history, pattern data, and purchase signals. You don't need another account, another app, or another database you can't export. This writes tracking history to git, a reliable, portable history tool you already use.

---

## Quick Start
1.  **Fork this repository** to your GitHub account.
2.  **Deploy** to your Cloudflare Workers account:
    ```bash
    npm install && wrangler deploy
    ```
3.  **Add** your carrier API keys as encrypted Worker secrets.
4.  **Add** tracking numbers to your fork's `packages.json` file.

The scheduled worker begins checking for updates and commits status changes directly to your repository.

---

## How It Works
ShipLog is a scheduled Cloudflare Worker that reads tracking numbers from your repo's `packages.json` file, queries carrier APIs using your credentials, and commits status changes back to your git history. Data flows only between your Worker and the carriers you authorize.

---

## What You Control
-   **Immutable History:** Package status is stored as git commits. You can diff, browse, search, and archive it like any other code.
-   **Your Infrastructure:** Runs on your Cloudflare Workers account; no external servers or middlemen see your data.
-   **Zero Dependencies:** No npm packages. No silent updates or hidden calls.
-   **Encrypted Secrets:** API keys are stored as Worker secrets, never in your repository.
-   **Fork-First:** You own the entire copy. If the original repo disappears, your fork continues working.

---

## Limitations
-