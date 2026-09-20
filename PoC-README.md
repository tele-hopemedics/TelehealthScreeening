# Git-based CMS PoC (Sveltia) — Hope Medics screening

## Files (put them at these paths in your repo)
- content/services.json   -> the editable content
- admin/config.yml        -> what the CMS form looks like + which repo/branch
- admin/index.html        -> loads the Sveltia CMS admin at /admin/

## Fastest proof (no OAuth, ~5 min)
1. Commit the three files above to your repo (edit repo/branch in config.yml).
2. Create a GitHub fine-grained PAT: GitHub > Settings > Developer settings >
   Fine-grained tokens > repo access = TelehealthScreeening, Permissions:
   Contents = Read and write. Copy it.
3. Open  https://tele-hopemedics.github.io/TelehealthScreeening/admin/
4. Sign in with a token, paste the PAT.
5. Edit a service label -> Publish. Sveltia commits to content/services.json;
   GitHub Pages redeploys in ~1 min.

## Wire the prototype to read it (see loader snippet in the chat)
Replace the tile-building block so the page fetches content/services.json and
falls back to the bundled defaults if the file is missing.

## Verify the loop
Edit a service label in /admin/ -> a commit appears on the repo -> the live
prototype shows the new label. That is the whole config-without-rebuild loop.

## Later (for non-dev editors: a "Sign in with GitHub" button instead of a PAT)
Deploy the free `sveltia-cms-auth` Cloudflare Worker, register a GitHub OAuth
app, set its env vars, and add `base_url: <worker-url>` under backend in config.yml.
