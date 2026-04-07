# ShipLog
> Self-hosted package tracking with a repo-agent captain. Powered by Cocapn Fleet.

You have pasted a tracking number into a random third party website before. You likely wondered what happened to that data.

This is an alternative: self-hosted package tracking that runs as your own agent. It lives in your repository, runs on your Cloudflare account, and communicates directly with carrier APIs when you tell it to.

**Live demo:** https://the-fleet.casey-digennaro.workers.dev/shiplog

---

## Why this exists
Most consumer package tracking services build profiles from your delivery history as part of their business model. ShipLog was built to offer a different approach. There is no central service operated by us. We never see your tracking numbers, your addresses, or your API keys. This agent runs on your infrastructure.

## What makes this different
This is not another tracking app or a third-party API.
- You fork this code first. You own the entire copy.
- It runs entirely on your Cloudflare Workers account.
- There is no server operated by us in the loop.
- If this repository disappears, your fork will keep working.
- You control its terms and your data.

## How it works
ShipLog is a scheduled Cloudflare Worker that:
1. Reads tracking numbers from your repository's `packages.json` file.
2. Checks status directly with carrier APIs using your credentials.
3. Commits status changes back to your repository's git history.
4. Can send notifications if you configure them.

Data stays with you. Information passes only to the official carrier APIs you authorize.

## Features
- Status history stored as immutable git commits.
- API keys stored as encrypted Worker secrets, never in code.
- Runs on the Cloudflare Workers free tier for typical use.
- Configurable check schedule via `wrangler.toml`.
- No runtime dependencies outside of Cloudflare's platform.
- No external databases or mandatory accounts.
- Compatible with the Cocapn Fleet protocol.
- Supports UPS and USPS.

## Limitations
Only UPS and USPS are implemented. Adding other carriers requires modifying your fork's code. This is a template designed for you to adapt, not a complete commercial service.

## Quick start
1. **Fork this repository** to your GitHub account.
2. Deploy to Cloudflare Workers:
   ```bash
   npm install && wrangler deploy
   ```
3. Add your carrier API keys as Worker secrets.
4. Add tracking numbers to `packages.json` in your repo.

It will begin checking for updates on the schedule you set in `wrangler.toml`.

## Configuration
After deployment, add your API keys:
```bash
wrangler secret put UPS_API_KEY
wrangler secret put USPS_API_KEY
```

## Development
ShipLog follows the Cocapn Fleet fork-first philosophy. The intended path is to fork and adapt it. Bug fixes and tested, minimal carrier additions are welcome as pull requests.

## License
MIT

Attribution: Superinstance & Lucineer (DiGennaro et al.)

---

<div>
  <strong>Fleet:</strong> <a href="https://the-fleet.casey-digennaro.workers.dev">the-fleet</a> ·
  <strong>Cocapn:</strong> <a href="https://cocapn.ai">cocapn.ai</a>
</div>