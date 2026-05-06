# Hash Generator

**SIG-HSH-001 · v0.1**

A browser-based hash generator for chain-of-custody documentation. Generates SHA-256 hard bindings and pHash soft bindings for files, text, and URLs. All hashing runs client-side. No file, text, or URL content is transmitted to any server.

Embedded at: https://signalandshadow.io/hash-generator
Standalone: https://[username].github.io/[repo-name]/

## Features

- **SHA-256.** Generated for any file type, text string, or fetched URL body.
- **pHash.** 32×32 perceptual hash for image inputs (JPEG, PNG, GIF, WebP).
- **Chain-of-custody block.** Output formatted for direct paste into MIP Analyser reports and SS-DOSSIER sections.
- **Client-side only.** Uses the WebCrypto API. No server transmission of source material.

## Deployment

Hosted on GitHub Pages from the `main` branch root. Any push to `main` triggers a redeploy (typically 30 to 90 seconds).

## Embed mode

The page detects iframe context automatically. When loaded inside an iframe (or with `?embed=1`), the status bar, hero, and footer are hidden, leaving only the tool UI. Suitable for embedding inside `signalandshadow.io/hash-generator`.

The page posts its height to the parent window via `postMessage` with type `ss-hash-generator-height`, allowing the parent to auto-resize the iframe.

### Iframe snippet for the parent page

```html
<iframe
  src="https://[username].github.io/[repo-name]/?embed=1"
  style="width: 100%; border: 0; min-height: 800px;"
  id="hash-generator-frame"
  title="Hash Generator">
</iframe>
<script>
  window.addEventListener('message', (e) => {
    if (e.data && e.data.type === 'ss-hash-generator-height') {
      document.getElementById('hash-generator-frame').style.height = e.data.height + 'px';
    }
  });
</script>
```

## Local development

Single-file static site, no build step.

```
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Standards

Built and verified under **LST-001 v1.0.3**.

## Licence

MIT. See `LICENSE`.

## Maintainer

Derek Bowler · Signal & Shadow · Versoix, Geneva
