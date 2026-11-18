# 📚 Vocab Master III

> **Collect words. Master them. Play with them.**
> A local-first vocabulary vault with Cambridge Dictionary lookups **and example sentences**, photo scanning, flashcards, four study modes, a scored Sentence Lab, and **ten word games** — including a bullet-hell **3D boss arena** with seven selectable AI strengths — all in a single HTML file.

![Single file](https://img.shields.io/badge/single--file-HTML-4d7dff?style=flat-square)
![No build step](https://img.shields.io/badge/build-none-22c55e?style=flat-square)
![Local first](https://img.shields.io/badge/data-localStorage-8b5cf6?style=flat-square)
![Games](https://img.shields.io/badge/games-10-f5a524?style=flat-square)
![Storage](https://img.shields.io/badge/storage-v5-ec4899?style=flat-square)

---

## What's new in III

- **Example sentences everywhere, automatically.** Cambridge examples (`.examp / .dexamp / .eg`) and fallback-API examples are fetched with every lookup, shown in Look up suggestions, flashcards, Sentence Lab, Photo Scan and the word drawer, **saved with the word**, preserved through import / export / share / edit — and **auto-backfilled onto words you saved before this version** the moment you open them.
- **Ten games, sorted by difficulty from 10 → 1.** Each tab carries its difficulty badge; the Games view opens on the hardest.
- **Five new games:** Spelling Master (6), Worldy Birds (7), Squaredle (8), Solitaire · Word Chain (9), Word Boss 3D (10).
- **Word Boss 3D became a real boss fight.** Ten telegraphed, dodgeable skills instead of bullet spam; seven AI strengths from **Easy** to **Extreme Demon**; and on PC **the fight does not stop while you type** — the boss keeps casting and can hit you, so you dodge with the arrow keys and slide with Shift without leaving the word box.
- **Difficulty scale rescaled to /10** across every game.
- **Storage v5** with automatic migration from v4 / v3 / legacy saves — words, mastered flags, stats, cloud link and boss settings all carry over.

---

## Contents

- [Quick start](#quick-start)
- [Features](#features)
  - [Library & sets](#library--sets)
  - [Photo Scan](#photo-scan)
  - [Sentence Lab](#sentence-lab)
  - [Flashcards](#flashcards)
  - [Learn · Test · Spelling](#learn--test--spelling)
  - [Word Games](#word-games)
  - [Word drawer](#word-drawer)
- [Word Boss 3D in depth](#word-boss-3d-in-depth)
- [Dictionary & data sources](#dictionary--data-sources)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Data & storage](#data--storage)
- [Import & export format](#import--export-format)
- [Cloud save & sharing](#cloud-save--sharing)
- [Privacy & offline behavior](#privacy--offline-behavior)
- [Browser support](#browser-support)
- [Troubleshooting](#troubleshooting)
- [Tech stack](#tech-stack)
- [Code map](#code-map)

---

## Quick start

No installation, no build step, no dependencies to manage.

1. Save the app as **`vocab-master.html`**.
2. Open it in a modern browser — double-clicking the file works.
3. *(Optional, recommended on strict browsers)* serve it locally:

   ```bash
   python -m http.server 8000
   # then visit http://localhost:8000/vocab-master.html
   ```

4. Add your first word with **Look up**, or tap **Scan photo** and point your camera at a page.
5. Open **Word Games → Word Boss 3D**, pick an AI strength, and enter the arena.

> **Internet is needed** for the first load (fonts, icons), dictionary lookups, the extended game word list, the first photo scan (OCR engine), and the first boss fight (Three.js). Everything else — your vault, study modes, Sentence Lab, and all games with the built-in word list — works offline.

---

## Features

### Library & sets

The home screen, library and set page are the heart of the app.

- **Look up** a word, idiom or phrasal verb (hyphens and short phrases accepted). Cambridge suggestions appear with checkboxes, part-of-speech tags **and an italic example sentence** — keep the meanings you want, and optionally add your own meaning or translation.
- **Saved words list** with live search across words *and* definitions, a part-of-speech filter, and five sort modes: Custom order, A→Z, Z→A, Newest, Oldest.
- **Drag to reorder** when *Custom order* is selected.
- **Bulk selection** — select all filtered words, delete in one action, and **Undo** from the toast.
- **Multiple sets** — create, rename, switch and delete collections (at least one is always kept). The sidebar shows live counts of words, mastered words and sets.
- **Import / Export** any set as a portable `.words` file, or share it as a link that lands in someone else's Library automatically.

### Photo Scan

Turn any page, screen or sign into vocabulary — with context-aware meaning selection.

1. Tap **Scan photo · one meaning · fast add** and choose or take a photo.
2. The image is downscaled for speed and read **locally** by the OCR engine (progress bar included).
3. Detected words appear as tappable chips (stop-words filtered, up to 60 candidates). Words already in your set are marked ✓ and skipped by auto-advance.
4. Tap a word. Every Cambridge sense is ranked against **the sentence from your photo** — word overlap with definitions, examples and guide words, plus a part-of-speech hint from the preceding word.
5. You see **exactly one meaning**, with the photo sentence quoted underneath and the matched example sentence.
   - **Not this one** cycles to the next candidate, one at a time.
   - **Skip** moves on without saving.
6. **⚡ Add to set** saves the word with that single meaning (and its example) and jumps to the next scanned word.

Photos are processed **entirely in your browser** and never uploaded.

### Sentence Lab

Active recall through writing: pick a set word, use it, get graded.

- Choose the target word from a dropdown or hit **Random**; its meanings **and examples** are shown, with a pronunciation button.
- Write one sentence (live word count; **Ctrl/⌘ + Enter** to check).
- Inflections count: `-s`, `-es`, `-ed`, `-ing`, `y → ies/ied`, dropped-e forms, and consonant doubling (*run → running*).
- Roughly twenty grammar and style rules run instantly, offline, plus **usage detection** (e.g. an adjective left dangling after *a/an*).

**Penalties**

| Check | Points |
|---|---|
| Missing the target word | score capped at **30** |
| Target word present but misused | score capped at **50** |
| Sentence under 4 words | −10 |
| "should/could/would **of**" instead of "…have" | −6 |
| No capital letter at the start | −5 |
| No ending punctuation (`. ! ?`) | −5 |
| Looks like more than one sentence | −5 |
| Lowercase pronoun "i" | −5 |
| ALL CAPS | −5 |
| "your welcome" → "you're welcome" | −5 |
| Over 60 words | −5 |
| Wrong article **a / an** (sound-aware: *an hour*, *a university*) | −4 each (max 2) |
| Repeated word ("the the") | −4 |
| Missing apostrophe (*dont, isnt, im, ive…*) | −4 |
| "alot" → "a lot" | −4 |
| "its a / its very…" → "it's" | −4 |
| Space before punctuation / missing space after | −3 |
| Unbalanced parentheses or quotation marks | −3 |
| Doubled `!!` or `??` | −2 |
| Extra spaces between words | −2 |
| Adjective misuse (*a delusional*, *very* + noun) | −15 … −20 |

**Bonuses**

| Achieved | Points |
|---|---|
| Each additional set word used | +4 (up to +12) |
| A linking word (*because, although, however, unless…*) | +5 |
| Good sentence length (8–24 words) | +5 |
| Varied vocabulary (≥80% unique words, 8+ words) | +3 |

Score = `100 − penalties + bonuses`, clamped to 0–100.

| Score | Grade |
|---|---|
| 90–100 | Excellent! 🏆 |
| 75–89 | Great job! |
| 60–74 | Good — fix the small issues |
| 0–59 | Needs work — try again |

**Attempts, Best and Average** persist between sessions.

### Flashcards

- Paper-style 3D flip cards: word on the front, all meanings **plus example sentences** on the back.
- Flip with a tap or **Space**, browse with **← / →**, shuffle and restart anytime.
- Mark **I know this** or **Still learning** — mastered words get a green badge everywhere.
- Pronounce the word or any definition.
- Opening a card whose meanings lack examples quietly fetches and attaches them.

### Learn · Test · Spelling

| Mode | Direction | Details |
|---|---|---|
| **Learn** | word → definition | Multiple choice, 2–6 options, distractors drawn from your own set, 10 pts per correct answer |
| **Test** | definition → word | Part of speech shown, type the word, immediate right/wrong feedback with the answer |
| **Spelling** | audio → spelling | Text-to-speech, hint button reveals part of speech, definition and letter count; misspellings shown struck-through |

### Word Games

Ten complete games, ordered hardest first. Every word you discover or play becomes a tappable chip — open it to see its Cambridge meaning and example, and add it to your set without leaving the game.

| # | Game | Difficulty | Board / format | Clear or score by | Run ends |
|---|---|---|---|---|---|
| 1 | **Word Boss 3D** | 10/10 | 3D arena | Type words to fire bolts; dodge ten boss skills | You run out of HP (endless levels) |
| 2 | **Solitaire · Word Chain** | 9/10 | apple → entertainment → table | Next word starts with the last letter | 3 timeouts, or a dead end (+50) |
| 3 | **Squaredle** | 8/10 | 5×5 letter grid | Connected paths spelling 4+ letter words | All main words found |
| 4 | **Worldy Birds** | 7/10 | Side-scrolling pipes | Type the pipe word before the bird arrives | One crash |
| 5 | **Spelling Master** | 6/10 | 8 spoken rounds | Type before the voice finishes | After round 8 |
| 6 | **Vocabtetris** | 5/10 | 13×13 | Falling letter blocks; words across or down clear | Stack reaches the top |
| 7 | **Vocablocky** | 4/10 | 9×9 | Placing pieces; straight runs spelling words clear | No remaining piece fits |
| 8 | **Endless Scrabble** | 3/10 | 9×9 | Classic tile play with bonus squares | Board completely filled (win!) |
| 9 | **Spelling Bee** | 2/10 | 7 or 10 letters | Words of 4+ letters using the hive | All possible words found |
| 10 | **Wordle** | 1/10 | 4 / 5 / 6 letters | Guess in six tries | Solved or out of guesses |

**Solitaire · Word Chain** — the amber tile shows the letter your next word must start with. Dictionary words only, no repeats, and a countdown that shrinks from 22 s toward 8 s as the chain grows. Three hearts (each timeout costs one) and three hints (−5 pts each). Score = 2 pts per letter + seconds left, +10 for words of 8+ letters; reaching a dead end awards **+50** and completes the chain. Minimum length 3 / 4 / 5 is selectable. Keys: `H` hint, `N` new chain.

**Squaredle** — swipe or click adjacent tiles horizontally, vertically or diagonally; no tile reuse inside one word, paths can wind in any shape. Finding words fills a bar that unlocks three hint tiers at 25 / 50 / 75 %: ★ words starting on each tile, ★★ words using each tile, ★★★ first-letter-and-length hints in the list. Rotate the grid to spot new patterns; tap the word count to see the lengths of the remaining words. Main words score `len × 10`; valid English words outside the puzzle count as **bonus words** at `len × 5`.

**Worldy Birds** — the bird flies on its own and every pipe carries a word. Type it to blast the pipe open before impact; wrong letters are ignored, and the further away the pipe, the bigger the distance bonus. Speed and word length rise with your score.

**Spelling Master** — the word is spoken aloud; start typing immediately. Submit before the voice ends for a **+15 LIGHTNING** bonus; afterwards the speed bonus decays. Eight rounds, `10 + 2 × letters` per correct spelling, preferring your own set's words.

**Vocabtetris** — steer and rotate letter tetrominoes; any contiguous run spelling a dictionary word clears, gravity drops survivors and can trigger **chain reactions**. Threshold configurable (2 / 3 / 4 letters). Scoring: `(cells × 15 + words × 10) × chain`.

**Vocablocky** — drag or tap pieces (single cells up to 3×3 squares) onto the grid. Words of the chosen minimum length clear for `(cells × 10 + words × 10)`; valid shorter words still earn small points.

**Endless Scrabble** — a 7-tile rack, no turn limit. First word must cover the center ★; later words must connect with no gaps. TW / DW / TL / DL squares multiply scores; using all 7 tiles earns **+50 bingo**.

**Spelling Bee** — every word must contain the amber center letter. 4-letter words score 1, longer words score their length, and a **pangram** earns +7 (Classic) or +20 (Special).

**Wordle** — green/yellow/gray feedback with animated reveals, on-screen and physical keyboard, persistent **Wins / Streak / Score**. Faster solves earn `(7 − guesses) × 20`.

Game word validation uses a full English word list when online, with a built-in offline list as fallback — the badge above the games shows which is active and how many words it contains.

### Word drawer

Tap any word anywhere in the app:

- Meanings with parts of speech, **Cambridge example sentences**, and a source badge.
- **Edit** meanings (add/remove rows, change part of speech — examples survive edits to unchanged rows), **delete** with undo, toggle **mastered**, hear pronunciation.
- Old words missing examples are backfilled automatically on open.
- For words found in games that aren't in your set yet: one-tap **Add to current set**.

---

## Word Boss 3D in depth

An endless first-person arena. Words are your weapon; reading telegraphs is your defence.

### The loop

- **Boss HP = level² × 100** (mobile: **level² × 50**). Defeat it, level up, forever.
- Each level clear grants **+1 heal item** and **+25 HP**; your best level is saved.
- Green **heal orbs** spawn around the arena (max 3 at a time) — walk over one to bank a heal.
- Words **cannot repeat** during a run.

### Damage formula

```
damage = length bonus + sum of letter points
```

| Word length | Bonus |
|---|---|
| 1–2 | 0 |
| 3 | 1 |
| 4 | 2 |
| 5 | 4 |
| 6 | 6 |
| 7 or more | 12 + length × 2 |

| Points | Letters |
|---|---|
| 1 | A E I O U L N S T R D G |
| 2 | B C M P F H V W Y |
| 4 | K J X |
| 6 | Q Z |

*Example:* `quiz` → Q6 + U1 + I1 + Z6 = 14 letter points, + 2 length bonus = **16 damage**.

### AI strength

Pick a tier in Setup, or change it live from the Pause panel. Higher tiers unlock more skills, attack faster, fly faster bullets and give you shorter warnings.

| Tier | Skills | Attack rate | Bullet speed | Warning | Hit damage |
|---|---|---|---|---|---|
| Easy | 2 | ×0.37 | ×0.78 | 1.25 s | 6 |
| Medium | 3 | ×0.45 | ×0.92 | 1.05 s | 8 |
| Hard | 4 | ×0.56 | ×1.05 | 0.90 s | 10 |
| Insane | 5 | ×0.69 | ×1.18 | 0.75 s | 12 |
| Easy Demon | 6 | ×0.87 | ×1.32 | 0.62 s | 14 |
| Hard Demon | 8 | ×1.09 | ×1.48 | 0.50 s | 16 |
| Extreme Demon | 10 | ×1.39 | ×1.66 | 0.38 s | 18 |

Attack cadence also tightens as the level rises, and from Hard Demon upward the boss can chain a second cast right after the first.

### The ten skills — and how to dodge them

| Skill | Unlocked at | What it does | Counter |
|---|---|---|---|
| **Aimed Bolt** | Easy | 1–3 fast shots that lead your position | Strafe sideways |
| **Spread Fan** | Easy | An arc of 7–11 bullets; a second offset volley at Easy Demon+ | Slip between the spokes, or slide |
| **Radial Burst** | Medium | A full ring from the boss, doubled half a beat later at Insane+ | Stand in the gap between spokes |
| **Sky Rain** | Hard | Amber ground rings mark impact zones, then orbs fall | Leave the marked circles before they land |
| **Sweep Laser** | Insane | A telegraphed beam sweeps across the arena | Outrun the sweep or slide through it |
| **Spiral Storm** | Easy Demon | A rotating multi-arm emitter runs for 2.3 s | Circle-strafe with the rotation |
| **Bullet Wall** | Hard Demon | A wall of bullets rolls across with one or two gaps | Find the gap |
| **Hunter Orbs** | Hard Demon | Slow homing orbs track you for 6 s | Kite them, or clear them with Nova |
| **Ground Slam** | Extreme Demon | Three expanding shockwave rings | Outrun them or slide through the ring |
| **Cross Lasers** | Extreme Demon | Four beams at 90°, slowly rotating | Stand in a quadrant and turn with them |

Every cast announces its name in the tier's colour, and big skills show a translucent telegraph before they arm — so a death is always readable, never random.

### Typing under fire

- **PC:** opening the word box does **not** pause the fight. Time slows to 60 %, the boss keeps casting, and it adds extra aimed pressure while you type. **Arrow keys move and Shift slides without leaving the input**, so you can dodge mid-word. `Esc` closes the box.
- **Mobile:** the fight pauses while you type, because the keyboard covers the arena.

### Controls

| Action | Desktop | Touch |
|---|---|---|
| Move | `W A S D` or arrow keys | Left half of the arena = virtual pad |
| Look | Mouse (click arena to lock pointer) | Drag the right half |
| Slide (i-frames, 2 s cooldown) | `E` — or `Shift` while typing | **SLIDE** button |
| Word Nova (clears bullets & shockwaves, damages a close boss, 12 s cooldown) | `Q` | **NOVA** button |
| Use heal item (+40 HP) | `H` | **HEAL ×n** button |
| Open the word box | **M1** by default — rebindable to M2, `F` or `T` | **TYPE** button |
| Pause | `P` | **Pause** button |

Look sensitivity is adjustable from **0.4 to 3.0** in Setup.

---

## Dictionary & data sources

| Purpose | Source | Behavior |
|---|---|---|
| Word meanings & examples | `dictionary.cambridge.org` | Fetched through **three CORS proxies in parallel** — first success wins (6 s timeout each). Examples read from `.examp`, `.dexamp`, `.eg`. |
| Meaning fallback | `api.dictionaryapi.dev` | Races alongside Cambridge with a **1.2 s head start** for Cambridge (5 s timeout); its `example` field is used too. The UI badges which source answered. |
| Definition cache | your browser | Every successful lookup is stored (up to **400 words**) — repeat lookups are instant, even offline. |
| Game word validation | `dwyl/english-words` | Downloaded via jsDelivr, then GitHub raw as backup; falls back to the built-in offline list. |
| Fresh vocabulary | Cambridge Dictionary blog | New-words feed refreshed daily; entries join the game and grammar dictionaries and can be saved to a set in one tap. |
| Photo OCR | Tesseract.js 5.1.1 (jsDelivr) | Lazy-loaded on first scan; recognition runs **locally** on a downscaled image. |
| 3D engine | Three.js r128 (cdnjs) | Lazy-loaded on the first boss fight, then browser-cached. |
| Cloud save & short links | jsonblob.com · json.extendsclass.com | Anonymous bins, no account and no API key; the first reachable provider wins. |
| Fonts & icons | Fontsource (Inter, Space Grotesk, Fraunces) + Font Awesome 6.4 | Loaded from CDNs, then browser-cached. |

Stale results are discarded: if you start a new search before the previous one finishes, only the newest result is shown.

---

## Keyboard shortcuts

| Where | Keys | Action |
|---|---|---|
| Anywhere | `Esc` | Close modal / drawer / word box |
| Set page | `Enter` (in the word field) | Look up |
| Flashcards | `Space` / `←` `→` | Flip / previous / next |
| Sentence Lab | `Ctrl/⌘ + Enter` | Check & score |
| Word Boss 3D | `W A S D` / arrows | Move |
| Word Boss 3D | `E` · `Q` · `H` · `P` | Slide · Nova · Heal · Pause |
| Word Boss 3D | `M1` / `M2` / `F` / `T` | Open the word box (rebindable) |
| Word Boss 3D — **while typing** | arrows · `Shift` · `Esc` | Dodge · slide · close |
| Solitaire | `H` · `N` | Hint · new chain |
| Squaredle | `Enter` · `Backspace` · `Esc` | Submit · step back · clear path |
| Vocabtetris | `←` `→` / `↑` / `↓` / `Space` / `P` | Move / rotate / soft drop / hard drop / pause |
| Spelling Bee | `A–Z` / `Backspace` / `Enter` | Type / delete / submit |
| Wordle | `A–Z` / `Backspace` / `Enter` | Type / delete / guess |

All games also have full on-screen touch controls.

---

## Data & storage

Everything lives in your browser's `localStorage` — no account, no server, no analytics.

| Key | Contents |
|---|---|
| `vocabMaster.v5` | Sets and words (with examples), active set, sound preference, best scores (Tetris, Blocky, Scrabble, Bee, Spelling Master, Birds, Squaredle, Solitaire, Boss level), Wordle wins/streak/score, Sentence Lab attempts/best/total, recents, cloud reference, boss config (`sens`, `atk`, `ai`) |
| `vocabMaster.defs.v1` | Cached definitions with source and examples (max 400 entries, oldest evicted) |
| `vocabMaster.newwords.v1` | Cambridge new-words feed |

**Migration:** on first run, data from `vocabMaster.v4`, `vocabMaster.v3`, `vocabMasterVaults` and `vocabMasterActiveVault` is imported automatically — words, mastered flags, stats, recents and cloud link included. The old demo sets *Everyday English* and *Exam Sprint* are dropped; every set you created is preserved.

**Reset everything** (browser DevTools console):

```js
localStorage.removeItem("vocabMaster.v5");
localStorage.removeItem("vocabMaster.defs.v1");
localStorage.removeItem("vocabMaster.newwords.v1");
location.reload();
```

> Data is per browser **and per origin**. Moving the file, switching browsers, or using private mode starts fresh — use **Export** or **Cloud save** to carry your collection with you.

---

## Import & export format

Export produces `VocabMaster_<set-name>_<YYYY-MM-DD>.words` — a plain JSON array (native save dialog where supported, otherwise a download). Import accepts `.words`, `.json` or `.txt` containing that array (or an object with a `words` array). Duplicates are skipped; `known`, `addedAt` and `ex` are preserved.

```json
[
  {
    "id": "lx3k9ab12cd",
    "word": "serendipity",
    "definitions": [
      {
        "pos": "noun",
        "def": "The fact of finding interesting or valuable things by chance.",
        "ex": "There is a real element of serendipity in archaeological discovery."
      }
    ],
    "addedAt": 1763000000000,
    "known": false
  }
]
```

Valid `pos` values: `noun`, `verb`, `adj`, `adv`, `phrase`, `other`. The `ex` field is optional and holds the example sentence.

---

## Cloud save & sharing

- **Free cloud save, no account and no API key.** Create a save and you get a secret **sync code**; enter it on any device (Cloud → Restore) to load and keep syncing the same data. Changes auto-push a few seconds after you make them, and the app syncs on visit.
- **Share a set as a link.** Opening the link adds the set straight to the recipient's **Library** — no import button, no copy dialog. Two formats are produced: a self-contained `#setdata=` link and a shorter `#set=` cloud link.
- Anyone holding a sync code can read that save; free anonymous storage may expire after long inactivity, so keep an **Export** for permanent backups.

---

## Privacy & offline behavior

- **Photos never leave your device** — OCR runs in the browser.
- Network requests go only to the dictionary sources/proxies, the anonymous cloud bins, and the public CDNs listed above. Your set contents are never sent anywhere except a cloud save you explicitly create.
- No tracking, no cookies, no telemetry.

| Capability | Offline? |
|---|---|
| Set management, flashcards, all quizzes, Sentence Lab | ✅ Fully |
| All ten games (Word Boss 3D after its first load) | ✅ With the built-in word list |
| Lookups of previously cached words, with examples | ✅ Instant from cache |
| New dictionary lookups / first photo scan / first boss fight | ❌ Internet required once |

---

## Browser support

Recent evergreen browsers — Chrome, Edge, Firefox and Safari (2023 or newer). The app uses standard web APIs (`localStorage`, Fetch + AbortController, DOMParser, Canvas, WebGL, WebAudio, SpeechSynthesis, Pointer Lock, drag & drop). The native file-save dialog is a progressive enhancement with a download fallback.

The layout is fully responsive: the sidebar becomes a bottom navigation bar on tablets and phones, game boards scale down, and Word Boss 3D swaps to a touch pad, drag-to-look and on-screen buttons on coarse-pointer devices (with the boss HP formula halved to match).

---

## Troubleshooting

**Lookups feel slow or fail.**
Public CORS proxies are occasionally rate-limited. The app already races three of them plus a fallback and caches every success — a word looked up once opens instantly forever after.

**An old word has no example sentence.**
Open it in the drawer or on a flashcard while online; the example is fetched and attached automatically, once per word.

**Photo scan says "No English words found".**
Try a sharper, closer, well-lit shot. OCR typos and proper names won't match a dictionary — use **Skip**, or add the word manually.

**The scan engine or 3D engine won't load.**
Both download once from a CDN on first use and are browser-cached afterwards. Check your connection for that first run.

**The boss arena ignores my mouse.**
Click the arena once to lock the pointer. Pressing `Esc` releases it and pauses the fight; click Resume and then the arena to lock again.

**I keep dying while typing on PC.**
That is intentional — the fight continues. Use the **arrow keys** to dodge and **Shift** to slide without leaving the word box, keep words short when the arena is busy, and drop the AI strength or clear bullets with `Q`.

**No pronunciation.**
Unmute with the speaker button in the top bar. Some browsers require a user interaction before audio, and available voices vary by platform; the Spelling Quiz hint works as a fallback.

**My words disappeared.**
Data is tied to the browser profile and the file's origin. Private windows clear on close. Export or cloud-save regularly if your collection matters.

**Something behaves oddly when opening the file directly.**
Serve it over `http://localhost` — a few browsers restrict CDN or storage behavior on `file://` pages.

---

## Tech stack

- **Vanilla JavaScript** — one IIFE, zero frameworks, zero build tooling
- **Web APIs:** localStorage · Fetch + AbortController · DOMParser · Canvas / createImageBitmap · WebGL (via Three.js) · WebAudio (procedural sound effects) · SpeechSynthesis · Pointer Lock · File System Access (optional) · HTML drag & drop
- **CDN libraries:** Three.js r128 (boss arena) · Tesseract.js 5.1.1 (OCR) · Font Awesome 6.4 · Fontsource variable fonts — Inter, Space Grotesk, Fraunces
- **Design:** dark aurora theme with drifting light fields and film grain, glass cards, paper-textured flashcards, palette-tinted scrollbars, staggered motion, telegraphed bullet-hell VFX with camera shake and hit vignette, and full mobile responsiveness

---

## Code map

```
.
├── vocab-master.html   ← the entire application (HTML + CSS + JS)
└── README.md
```

Inside the single `<script>`, sections are marked with comment banners:

```
helpers → persistent state & migration → toasts → sound & speech → modal
→ navigation → sets → home → library → set page
→ word list (search/filter/sort/drag/bulk/undo)
→ Cambridge lookup (parallel proxies, examples, cache) → import/export
→ word drawer (example backfill) → flashcards → Learn → Test → Spelling
→ game dictionary → Cambridge auto-update → games hub (difficulty order)
→ Vocabtetris → Vocablocky → Scrabble → Spelling Bee → Wordle
→ photo scan → Sentence Lab → free cloud → add-to-library & sharing → account
→ Spelling Master → Worldy Birds → Squaredle → Solitaire (word chain)
→ Word Boss 3D (AI tiers, skills, telegraphs, hazards)
→ global event delegation → drag & drop → keyboard router → init
```

All UI events flow through one delegated `data-action` handler, so every button in every view is wired through the same predictable path. The boss arena runs a single `requestAnimationFrame` loop with shared geometry and materials, and every hazard array is cleared on restart, level change and pause — no duplicated loops, listeners or timers.

---

*Built for word lovers. Collect something wonderful today. 🐝*
