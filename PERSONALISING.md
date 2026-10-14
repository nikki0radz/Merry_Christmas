# A little Christmas magic

A personal Christmas card experience from Nicole. Enter a first name, answer a shared-memory question, and unwrap a unique card.

Five demo layouts: traditional letter, photo scrapbook, winter postcard, interactive gift, and golden party card. Responsive, keyboard accessible, reduced-motion aware, and no sign-in needed.

## Publish

The included GitHub Actions workflow deploys the static site to GitHub Pages. If initial setup requires owner administration, select **Settings → Pages → Source → GitHub Actions**, then rerun **Publish Christmas cards** in Actions.

## Personalise

The public `cards.json` contains names, questions, and encrypted card payloads. Each payload contains `name`, `style`, `images`, `wishes`, and (for scrapbook) `captions`. Styles are `letter`, `scrapbook`, `postcard`, `gift`, and `party`. The answer itself is not published. Answers are NFKC normalised, trimmed, lowercased, and repeated whitespace is collapsed.

To replace a card, encrypt its JSON with AES-256-GCM using a key derived from its normalised secret answer via PBKDF2-SHA256 (250,000 iterations, random 16-byte salt, random 12-byte IV). Store salt and IV as base64, and ciphertext followed by the 16-byte authentication tag as base64 in `content`. Keep plaintext source and answers outside this public repository. First names must be unique; people sharing a name will need an extra identifier in a future version.

This protects the message from casual source inspection, but short answers can be guessed offline. Use long shared-memory phrases for real cards. Placeholder photos are public Unsplash URLs and are not private. Sensitive personal photos would need encrypted assets or a server-backed solution. Names and questions remain public.

## Local preview

Serve this directory over localhost, for example `python -m http.server 8000`. Open http://localhost:8000. Web Crypto requires HTTPS or localhost.

Stock photos are placeholders from Unsplash. Google Fonts supplies DM Sans and Playfair Display, with local fallback fonts. Failed photos show a festive fallback.
