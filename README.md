# 💍 Scavenger Hunt Proposal App

A web-based, GPS-powered scavenger hunt that ends in a marriage proposal —
built for Safari on iPhone. She follows clues from place to place; the app
watches her location and **automatically unlocks** a personal message and the
next clue the moment she arrives at each spot. The final clue leads her to
you, and the app pops the question with a confetti-filled proposal screen.

Everything is one file (`index.html`) — no build step, no dependencies, no
server-side code.

## How the hunt works

1. You pick a handful of meaningful locations (first date spot, favorite
   park, etc.) and write a clue that leads to each one.
2. She opens the link on her iPhone and taps **Begin** — Safari asks for
   location permission right then.
3. As she walks, a live status chip shows how far away she is
   ("1.2 km away" → "So close… keep going ♥").
4. When she steps inside the stop's radius, the app celebrates, shows a
   **personal arrival message** you wrote for that place, then reveals the
   next clue.
5. Make the **last stop wherever you're waiting with the ring** — after she
   arrives, the app plays a slow message buildup and then asks
   **"Will you marry me?"** with confetti.

Progress is saved on her phone (localStorage), so closing Safari or a dead
battery won't lose her place. The screen is kept awake while she navigates
(Screen Wake Lock, supported in modern iOS Safari).

### Built-in safety nets (GPS is never 100%)

- **Backup code words** — every stop also has a secret `code`. If GPS
  misbehaves, she can tap *"Trouble with your location?"* and type the word
  instead. Keep a screenshot of the codes with you on the day.
- **Permission denied** — the app explains exactly how to re-enable
  location (Safari's ᴀA menu → Website Settings → Location → Allow) and
  offers the code path automatically.
- **No GPS fix after 20 seconds** — same thing: a gentle nudge plus the
  backup code input appears on its own. The hunt can never get stuck.
- **Jitter protection** — arrival requires one high-accuracy fix or two
  consecutive in-radius fixes, so a single wild GPS reading can't
  teleport her to the finish line.

## Customize it

Open `index.html` and edit the `CONFIG` object at the top of the
`<script>` section. It's clearly marked `✏️ EDIT THIS SECTION`:

- **`herName` / `yourName`** — your names.
- **`introTitle` / `introMessage`** — the welcome screen.
- **`showDistance`** — set `false` to hide the "1.2 km away" readout if
  you'd rather she navigate purely from the clue.
- **`stops`** — the heart of the hunt. Each stop has:
  - `emoji` — shown big on the clue card
  - `title` — short name for the stop
  - `clue` — the riddle/clue text (use `\n` for line breaks)
  - `hint` — revealed only if she taps "Need a hint?"
  - `arrivalMessage` — the personal note shown the moment she arrives
  - `lat` / `lng` — the spot's coordinates (see below)
  - `radius` — how close (in meters) counts as "arrived"
  - `code` — the backup secret word for this stop
- **`buildupLines`** — the lines shown one at a time before the question.
- **`proposalQuestion` / `celebrationMessage`** — the big moment.

Add or remove stops freely — the progress hearts and clue numbering adapt
automatically. A stop with no `lat`/`lng` becomes a code-word-only stop.

### Getting coordinates

- **Google Maps:** press-and-hold on the exact spot — the `lat, lng` pair
  appears in the info card. Copy both numbers.
- **Apple Maps:** drop a pin → swipe up on the place card → tap the
  coordinates to copy.

### Picking a radius (meters)

| Location type | Suggested radius |
|---|---|
| Open outdoor spot (park, overlook) | 35–50 |
| Street address / storefront | 50–60 |
| Indoors (café, restaurant) | 60–80 |

GPS drifts indoors, so be generous there. **Keep stops at least ~150 m
apart** — if two stops overlap, she may unlock the next one instantly while
still standing at the previous one.

## Rehearse it (important!)

- **Couch rehearsal:** add `?demo=1` to the URL — every clue gets a
  "Simulate arrival" button so you can click through the entire flow.
- **Reset:** tap the small **"made with ♥"** text at the bottom of the
  screen **5 times quickly** to secretly wipe all progress.
- **Real rehearsal:** walk the actual route once with your own phone.
  Check that each stop unlocks where you expect; widen any radius that
  feels finicky.

## Deploy it (free, ~2 minutes)

Geolocation **requires HTTPS**, so the app must be served from a proper
host (all of the options below are HTTPS by default — opening the file
directly or over plain HTTP won't be able to use GPS).

The easiest option is **GitHub Pages**:

1. In this repo on GitHub, go to **Settings → Pages**.
2. Under *Build and deployment*, choose **Deploy from a branch**, pick your
   branch and the `/ (root)` folder, and save.
3. Your app will be live at `https://<username>.github.io/<repo>/` in about
   a minute.

Any static host works too (Netlify Drop, Vercel, Cloudflare Pages — just
drag `index.html` in).

### Tips for the day

- Text her the link, or make it feel more polished: open the link in
  Safari beforehand and tap **Share → Add to Home Screen** — it launches
  full-screen like a native app.
- Ask her to keep Safari open while walking (iOS pauses GPS for
  backgrounded tabs); the app re-checks the moment she returns to it
  either way.
- Charge her phone. Charge your phone. Bring tissues. 💍
