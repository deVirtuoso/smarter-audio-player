# Smarter Audio Player — public site

Static pages served by GitHub Pages. Contains only the public-facing homepage,
privacy policy, terms of service, and consent-screen logo. No app source code
lives here — this repo is safe to make public.

## Files

- `index.html` — homepage.
- `privacy.html` — privacy policy (referenced by Google's OAuth consent screen
  and by Google Play's Data Safety declarations).
- `terms.html` — terms of service (referenced by Google's OAuth consent screen).
- `logo.png` — 120×120 PNG for the OAuth consent-screen logo.

## Before you push

Search and replace the following placeholders across all three HTML files:

| Placeholder | Replace with |
|---|---|
| `REPLACE_WITH_YOUR_SUPPORT_EMAIL` | Your public support address, e.g. `support@yourdomain.com` |
| `REPLACE_WITH_DATE_YOU_PUBLISH` | Today's date, ISO format, e.g. `2026-09-15` |
| `REPLACE_WITH_YOUR_COUNTRY_OR_STATE` | e.g. `England and Wales`, `Scotland`, `California, USA` |

On Windows PowerShell you can do all three in one pass:

```powershell
Get-ChildItem *.html | ForEach-Object {
  (Get-Content $_ -Raw) `
    -replace 'REPLACE_WITH_YOUR_SUPPORT_EMAIL', 'you@example.com' `
    -replace 'REPLACE_WITH_DATE_YOU_PUBLISH', (Get-Date -Format 'yyyy-MM-dd') `
    -replace 'REPLACE_WITH_YOUR_COUNTRY_OR_STATE', 'England and Wales' `
  | Set-Content $_
}
```

## Push to GitHub

Create a new **public** repository on GitHub (e.g. `smarter-audio-player`). Do not
add a README on GitHub's side — this repo already has one.

From this folder (`site/`):

```bash
git init
git add .
git commit -m "Initial public site (privacy, terms, homepage, logo)"
git branch -M main
git remote add origin https://github.com/<your-username>/smarter-audio-player.git
git push -u origin main
```

## Turn on GitHub Pages

1. On GitHub, open the new repository.
2. **Settings → Pages**.
3. **Build and deployment → Source:** `Deploy from a branch`.
4. **Branch:** `main` / `(root)`. Save.
5. Wait ~30 seconds. The page banner shows the live URL, typically
   `https://<your-username>.github.io/smarter-audio-player/`.

## Pin the URLs into the OAuth consent screen

Once Pages is live, paste these into the Google Cloud Console → OAuth consent
screen form:

- **Application home page:** `https://<user>.github.io/smarter-audio-player/`
- **Application privacy policy link:** `https://<user>.github.io/smarter-audio-player/privacy.html`
- **Application terms of service link:** `https://<user>.github.io/smarter-audio-player/terms.html`
- **Authorised domains:** `github.io` (Google auto-strips subdomains; `github.io` covers all pages there)
- **App logo:** upload `logo.png` from this folder.

## Custom domain (optional, later)

If you'd like the site at your own domain instead of `github.io`, add a
`CNAME` file with the domain, point a DNS `CNAME` record at
`<user>.github.io`, and re-paste the new URLs into the OAuth consent screen.
Google's verification will then re-check the domain.

## Sanity check locally

Any static server works. Simplest, without installing anything, using Python:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000/`.
