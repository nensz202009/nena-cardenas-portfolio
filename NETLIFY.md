# Netlify Deploy Instructions

This repo has no site code yet, so these are generic setup steps to follow once
there's a project here. Update the build command/publish directory once you
know the framework (static HTML, Vite, Next.js, etc.).

## Option A: Git-based deploys (recommended)

1. Push this repo to GitHub (see git/GitHub setup below).
2. Go to https://app.netlify.com → **Add new site → Import an existing project**.
3. Choose **GitHub**, authorize Netlify if prompted, and select this repository.
4. Set build settings:
   - **Build command**: e.g. `npm run build` (leave blank for plain static HTML)
   - **Publish directory**: e.g. `dist`, `build`, `public`, or `.` for static sites
5. Click **Deploy site**. Netlify will auto-build on every push to `main`.
6. (Optional) Add a custom domain under **Site configuration → Domain management**.
7. (Optional) Add environment variables under **Site configuration → Environment variables**
   before the first deploy if the build needs them (API keys, etc.).

## Option B: Netlify CLI (manual/local deploys)

```bash
npm install -g netlify-cli
netlify login          # opens browser to authorize
netlify init            # links this folder to a Netlify site (or creates one)
netlify deploy          # draft/preview deploy
netlify deploy --prod   # production deploy
```

## Optional: netlify.toml

Add a `netlify.toml` at the repo root to pin build settings in version control:

```toml
[build]
  command = "npm run build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "20"
```

## Notes

- Netlify builds from whatever branch you configure (default `main`) — make sure
  local commits are pushed before expecting a deploy to pick them up.
- Preview deploys are created automatically for pull requests once the repo is linked.
- Do not commit secrets/API keys directly into `netlify.toml` or the repo — use
  Netlify's environment variables UI or `netlify env:set` instead.
