# philia_socialfit_invite_fe

Static Origins / Keys to the City invitation page for SocialFit Dubai First Wave.

## Run

Serve this folder over HTTP (not `file://`). Example:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080/SocialFit-Founder-Key-Invitation-v138.html`.

## API

The page posts applications, Ask SocialFit, and the voice token to the Philia backend.

- Same host as the API: no extra config.
- Separate host: set the API origin, e.g.
  `http://localhost:8080/SocialFit-Founder-Key-Invitation-v138.html?api=http://localhost:8000`

Endpoints used:

- `POST /api/socialfit/invite/keys-to-the-city/submit/`
- `POST /api/ask-socialfit`
- `POST /api/realtime-token`

Voice still uses OpenAI Realtime in the browser. The backend only mints a short-lived token.

The Keys film is inlined in the HTML as a data URI, so the page does not need a separate video file.
