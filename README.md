# Split the Check 🧾

A single-file bill splitter for dinners where everyone ordered their own thing.

**Live:** https://ritvik-v.github.io/split-the-check/

- **Scan a photo** of the receipt — parsed by Google's Gemini API using your own free
  [AI Studio](https://aistudio.google.com/apikey) key, pasted once and stored only in your
  browser's localStorage. Handles angled shots, an itemized customer copy plus a merchant
  copy with a handwritten tip in one photo, and quantity columns.
- **No key? Paste text** — copy the text off the photo (iPhone Live Text / Google Lens) and
  paste it in; the built-in parser handles duplicated copies, decimal-less handwritten
  amounts ("Tip 37 48"), and payment-line noise.
- Assign each item to one or more people; shared items split evenly, penny-exact.
- Tax and tip divide proportionally to what each person ordered.
- Everything else stays in `localStorage`; there is no server.

## Security notes

- The Gemini key is sent only to `generativelanguage.googleapis.com`, in a request header
  (never in a URL). A `Content-Security-Policy` allows no external scripts and no network
  destination other than Gemini, so injected code would have nowhere to send the key.
- Harden your key on Google's side: restrict it to HTTP referrer
  `https://ritvik-v.github.io/*` and to the Generative Language API only, and keep it a
  free-tier key with no billing account attached.
- On a shared computer, use the **Remove key** button when you're done.

No build step — `index.html` is the whole app. Tests live outside the repo and run with
Node (parser unit tests, jsdom flow tests, Puppeteer browser tests).
