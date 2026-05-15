# gamma-co

React-style SPA that injects GTM ~500ms after first paint. Tests TraceConverge's ability to detect lazy-loaded analytics. Default persona: **Gamma Co** (also serves permission-gap tests since Gamma Co is the persona where access is deliberately downgraded).

**Live URL:** `https://cpaynejz.github.io/gamma-co/`

## Test plan scenarios served

- TC-3.1.4 SPA / lazy-loaded GTM detection
- TC-3.5.3 permission-gap (READ but not EDIT access on Gamma's GTM account)

## How to configure

Edit `index.html` and replace the placeholder:

```js
var GTM_ID = '__GTM_CONTAINER_ID__';
```

with your real GTM container ID:

```js
var GTM_ID = 'GTM-ABCDEF';
```

Commit and push.

For the "no GTM at all" baseline (TC-1.2.1 greenfield), leave the placeholder unchanged — the script no-ops when it's not a real ID.

## What this tests

- Whether Discovery's Playwright probe waits long enough for client-side GTM injection
- Whether GTM ID extraction from runtime DOM works when the snippet is not in the initial HTML
- Whether the lazy-load timing affects classification correctness

If Discovery fails to detect GTM here even when configured, that's a bug worth filing — many real customer sites use lazy GTM injection (especially privacy-focused or performance-tuned ones).
