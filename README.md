# Encrypt This

A single-page site for encrypting and decrypting text with a password. Paste a note from your phone, encrypt it, and save the output. Paste the output back later with the same password to get the note back.

Everything runs in the browser through the Web Crypto API. There is no server, no storage, and no network requests.

## How it works

- **Key derivation:** PBKDF2-SHA256, 600,000 iterations, random 16-byte salt
- **Cipher:** AES-256-GCM with a random 12-byte nonce (a wrong password or edited ciphertext fails to decrypt)
- **Output format:** `ET1:` + base64(`salt | nonce | ciphertext+tag`)

If you forget the password, the text can't be recovered.

## Running it

Open `index.html` over `https://` or `http://localhost`. Browsers only expose Web Crypto in secure contexts, so the page won't work from a plain `http://` host.

## Hosting

The site is hosted on Netlify, which is connected to this repo. Every push to `main` deploys automatically. There is no build step: the build command is empty and the publish directory is the repo root. Netlify serves the custom subdomain on andrewfbutler.com and provides the HTTPS certificate.

To set it up again from scratch:

1. In Netlify, go to **Add new site → Import from Git** and choose this repo. Leave the build command empty and set the publish directory to `/`.
2. Under **Domain management**, add the subdomain. If Netlify DNS manages andrewfbutler.com, it creates the DNS record and certificate automatically.

On your phone, open the site and use **Add to Home Screen** so it works like an app.

## Local testing

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
