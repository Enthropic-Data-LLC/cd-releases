# Cellular Defense — signed release log

Every release of the web app at https://app.cellulardefense.net is listed here,
in order, with its signature. A release manifest gives the SHA-256 of every file
the server publishes and the exact Content-Security-Policy header.

- `releases/NNNN.json` and `.sig` — every release, never rewritten
- `latest.json` and `.sig` — the newest; anything older on the live site is a rollback
- `allowed_signers` — the release key (an `sk-ecdsa` key on a hardware security key)

Verify a manifest:

```bash
ssh-keygen -Y verify -f allowed_signers -I cd-release@cellulardefense.net \
  -n cd-release@cellulardefense.net -s latest.json.sig < latest.json
```

Check the live site against it: the browser extension
("Cellular Defense — Verify") does this on every visit; or run
`release/verify-site.mjs` from the app's source.

This log is append-only by convention and by its git history: a release that
disappears or changes here is itself evidence of tampering.
