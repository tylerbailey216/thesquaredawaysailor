## Deployment hardening (recommended)

When you host this static site, serve it over HTTPS with restrictive headers:

- `Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; font-src 'self' data:; connect-src 'self'; object-src 'none'; base-uri 'self'; form-action 'self'; frame-ancestors 'self'; worker-src 'self' blob:`
- `X-Frame-Options: SAMEORIGIN` (redundant with the CSP `frame-ancestors`)
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Permissions-Policy: microphone=(), camera=(), geolocation=()`
- `Cross-Origin-Resource-Policy: same-origin`

Notes:
- Keep `script-src` limited to `'self'` by serving `pdf-lib.min.js` locally (already vendored).
- Inline `<style>` blocks require `'unsafe-inline'` for styles; avoid adding inline scripts so you can keep `script-src 'self'`.
- If you add new third-party assets, prefer vendoring them locally and updating CSP accordingly.

## Local testing

The in-page `<meta http-equiv="Content-Security-Policy">` is relaxed so the tools work when opened directly from the filesystem. Browsers ignore `frame-ancestors` in meta; rely on the header in production for clickjacking protection.
