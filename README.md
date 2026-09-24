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

The easiest hosting option is GitHub Pages: **Settings → Pages → Deploy from branch → `main` / root**. After that, add the page to your phone's home screen.

Local testing:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
