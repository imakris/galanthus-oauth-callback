# galanthus-oauth-callback

A tiny static page used as the OAuth redirect URI target for the
galanthus CLI.

When the user clicks **Authorise** on an OAuth provider's consent page,
the browser is redirected here with `?code=...&state=...` in the query
string. This page:

1. Reads the `code` (and `state`) from the URL via JavaScript.
2. Displays the code prominently with a **Copy** button.
3. Tells the user to switch back to the terminal and paste at the
   `code>` prompt.

No data is sent anywhere. The page runs entirely in the user's browser.

## Why this exists

The galanthus CLI needs the authorization code from the OAuth redirect to
exchange it for an access token. The common alternatives are:

- **Register a loopback URI (`http://localhost:PORT/callback`)** and run a
  local HTTP listener. Revolut Business rejects `http://` at the consent
  endpoint, so loopback does not work there.
- **Run a local HTTPS listener with a self-signed cert.** Works but bloats
  the CLI with TLS server code and makes the user click through a
  certificate warning.
- **Point the redirect at `https://example.com/` and have the user copy
  the URL out of the address bar.** Works, but the UX is fragile - users
  mis-select the URL, paste the wrong thing, or land on intermediate
  SSO/re-auth pages.

This page is the zero-infrastructure alternative: the user lands on an
actual page that tells them what to do and puts the code one click away.

## Hosting

Served via GitHub Pages from `master` branch, root folder.

## License

MIT.
