# Unlock PDF

A small web app for iPhone that removes the open password from a PDF, such as a bank statement, CAS or Form 16, so you can send the unlocked copy to your CA.

- The PDF is unlocked inside the browser. Nothing is uploaded to a server.
- Works with AES-256, AES-128 and RC4 encrypted PDFs, and also removes print and copy restrictions.
- Add several PDFs at once. A password that works on one file is tried on the others.
- On iPhone, **Share** opens the share sheet, so you can send the file straight to WhatsApp or Mail, or save it to Files.

## Using it on iPhone

1. Open the app's URL in Safari.
2. Tap **Share**, then **Add to Home Screen**. It now opens like a normal app.
3. Type the password, tap **Choose PDFs**, and pick the statements.
4. Tap **Share** on a file (or **Share all** at the bottom) and send it to your CA.

## Hosting

The app is plain static files in this folder; there is no build step. It has to be served over `http(s)://` (opening `index.html` as a local file won't load the WebAssembly engine).

**GitHub Pages** (free for public repos): every push to `main` that changes this folder runs the `Publish Unlock PDF to GitHub Pages` workflow, which copies it to the `gh-pages` branch. GitHub Pages serves that branch at `https://<owner>.github.io/<repo>/`. If the site doesn't show up, go to **Settings → Pages** and set **Source** to **Deploy from a branch**, branch `gh-pages`, folder `/ (root)`. On a fork, you may also need to turn on workflows in the **Actions** tab.

**Anywhere else:** upload the contents of `pdf-unlock/` to any static host (Netlify, Vercel, Cloudflare Pages, S3).

**Locally:** `python3 -m http.server 8080 --directory pdf-unlock`, then open `http://localhost:8080`.

## How it works

The page runs [qpdf](https://qpdf.readthedocs.io/) compiled to WebAssembly and calls `qpdf --password=… --decrypt in.pdf out.pdf`. That removes the encryption and leaves the rest of the file untouched, so text stays selectable and the layout doesn't change. If WebAssembly is blocked or qpdf can't read a file, the page falls back to [@cantoo/pdf-lib](https://github.com/cantoo-scribe/pdf-lib), a pure JavaScript library that can also decrypt PDFs.

| File                   | Purpose                                                |
| ---------------------- | ------------------------------------------------------ |
| `index.html`           | The whole app: markup, styles and script               |
| `manifest.webmanifest` | Name and icons for Add to Home Screen                  |
| `icons/`               | App icons                                              |
| `vendor/`              | qpdf (WebAssembly) and pdf-lib, see `vendor/NOTICE.md` |
