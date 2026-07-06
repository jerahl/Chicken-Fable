# 💍 Scavenger Hunt Proposal App

A web-based scavenger hunt that ends in a marriage proposal — built for Safari
on iPhone. She follows clues from place to place, unlocking each one with a
secret code word you've hidden at that real-world location. The final clue
leads her to you, and the app pops the question with a confetti-filled
proposal screen.

Everything is one file (`index.html`) — no build step, no dependencies, no
server-side code.

## How the hunt works

1. You pick a handful of meaningful locations (first date spot, favorite park,
   etc.) and write a clue that leads to each one.
2. At each location you hide a card or note with that stop's **code word**
   (or have a friend there to hand it over).
3. She opens the link on her iPhone, reads the first clue, goes to the spot,
   finds the word, and types it in to unlock the next clue.
4. Make the **last stop wherever you're waiting with the ring** — after she
   unlocks it, the app plays a slow message buildup and then asks
   **"Will you marry me?"** with confetti.

Progress is saved on her phone (localStorage), so closing Safari or a dead
battery won't lose her place.

## Customize it

Open `index.html` and edit the `CONFIG` object at the top of the
`<script>` section. It's clearly marked `✏️ EDIT THIS SECTION`:

- **`herName` / `yourName`** — your names.
- **`introTitle` / `introMessage`** — the welcome screen.
- **`stops`** — the heart of the hunt. Each stop has:
  - `emoji` — shown big on the clue card
  - `title` — short name for the stop
  - `clue` — the riddle/clue text (use `\n` for line breaks)
  - `hint` — revealed only if she taps "Need a hint?"
  - `code` — the secret word hidden at that location
    (case- and whitespace-insensitive when she types it)
- **`buildupLines`** — the lines shown one at a time before the question.
- **`proposalQuestion` / `celebrationMessage`** — the big moment.

Add or remove stops freely — the progress hearts and clue numbering adapt
automatically.

## Rehearse it (important!)

Tap the small **"made with ♥"** text at the bottom of the screen **5 times
quickly** to secretly reset all progress. Walk through the entire flow
yourself at least once before the big day.

## Deploy it (free, ~2 minutes)

The easiest option is **GitHub Pages**:

1. In this repo on GitHub, go to **Settings → Pages**.
2. Under *Build and deployment*, choose **Deploy from a branch**, pick your
   branch and the `/ (root)` folder, and save.
3. Your app will be live at `https://<username>.github.io/<repo>/` in about a
   minute.

Any static host works too (Netlify Drop, Vercel, Cloudflare Pages — just drag
`index.html` in).

### Tips for the day

- Text her the link, or make it feel more polished: open the link in Safari,
  tap **Share → Add to Home Screen** on her phone beforehand — it launches
  full-screen like a native app.
- The page works offline once loaded — no network is required to check codes.
- Keep a screenshot of the code words with you in case a hidden card goes
  missing — you can casually "help her find it."
