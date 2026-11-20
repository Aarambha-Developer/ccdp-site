# CCDP website

Static site for Creative Children Development Programme (CCDP), Pokhara, Nepal.
Served by Cloudflare Workers static assets; no build step.

```
public/            the whole site (index.html, video.mp4, img/)
wrangler.jsonc     Cloudflare Worker config
docs-handover.md   content-editing guide and go-live placeholders checklist
```

## Develop and deploy

Requires Node 22.12 or newer.

```bash
npm install
npm run dev      # local preview
npm run deploy   # publish to Cloudflare (needs `npx wrangler login` or CLOUDFLARE_API_TOKEN)
```

Before going live, replace the placeholders listed in `docs-handover.md` (section 4).
