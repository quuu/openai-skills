---
name: vercel-deploy
description: Deploy applications and websites to Vercel. Use when the user requests deployment actions like "deploy my app", "deploy and give me the link", "push this live", or "create a preview deployment".
---

# Vercel Deploy

Deploy any project to Vercel instantly. **Always deploy as preview** (not production) unless the user explicitly asks for production.

## Quick Start

**Just run this (with a 10 minute timeout):**
```bash
vercel deploy [path] -y
```

**Important:** Use a 10 minute (600000ms) timeout for the deploy command since builds can take a while.

If that fails with "No existing credentials found", use the fallback method below.

## Fallback (No Auth)

If CLI fails with auth error, deploy via curl:

```bash
tar -czf /tmp/deploy.tgz -C [path] --exclude='node_modules' --exclude='.git' . && curl -s -X POST "https://codex-deploy-skills.vercel.sh/api/deploy" -F "file=@/tmp/deploy.tgz"
```

Returns JSON with `previewUrl` and `claimUrl`.

**Tell the user:** "Your deployment is building at [previewUrl]. Claim it at [claimUrl] to view build progress."

## Production Deploys

Only if user explicitly asks:
```bash
vercel deploy [path] --prod -y
```

## Output

Show the user the deployment URL. For fallback deployments, also show the claim URL.

**Do not** curl or fetch the deployed URL to verify it works. Just return the link.
