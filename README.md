# philia_socialfit_invite_fe

Static Origins / Keys to the City invitation page for SocialFit Dubai First Wave.

## Run

Serve this folder over HTTP (not `file://`). Example:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080/SocialFit-Founder-Key-Invitation-v138.html`.

## Deploy (invite.socialfit.philia.life)

Copy the HTML **and** the icon files onto the nginx root (`/var/www/philia_socialfit_invite_fe/` or equivalent):

- `SocialFit-Founder-Key-Invitation-v138.html` (as `index.html`)
- `favicon.ico`
- `apple-touch-icon.png`
- `favicon/` (pngs + `site.webmanifest`)

Browsers always request `/favicon.ico`. If that file is missing, `try_files … /index.html` serves the whole 2.4MB page a second time.

Paste `nginx.invite.snippet.conf` into the invite `server { }` block (favicon exact-match + gzip), then:

```bash
sudo nginx -t && sudo systemctl reload nginx
```

Confirm with:

```bash
curl -sI https://invite.socialfit.philia.life/favicon.ico
curl -sI -H 'Accept-Encoding: gzip' https://invite.socialfit.philia.life/
```

`/favicon.ico` must be a small `image/x-icon` (about 15KB), not `text/html`. The HTML response should include `Content-Encoding: gzip`.

## API

The page posts applications, Ask SocialFit, and the voice token to the Philia backend.

- Production default: `https://api.philia.life`.
- Local override: `?api=http://localhost:8000` or set `window.SOCIALFIT_API_BASE`.

Endpoints used:

- `POST /api/socialfit/invite/keys-to-the-city/submit/`
- `POST /api/ask-socialfit`
- `POST /api/realtime-token`

Voice still uses OpenAI Realtime in the browser. The backend only mints a short-lived token.

The Keys film is inlined in the HTML as a data URI, so the page does not need a separate video file.
