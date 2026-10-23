# Clyde's Archive Word Game: Update Notes

## Update 2: title page, About page, animation and fixes

Replace `index.html` only. `words.js` and `background.png` are unchanged from update 1.

- **Title page:** the game now opens on a page with just **Archive Word Games!** and a **Play** button. Pressing Enter also works. Play opens the game menu, which has Wordle, Hangman, Anagram, Word Search, How to play, Settings and About, plus a small "Back to title" button. Pressing Play counts as the first tap, so the background music starts there.
- **Hard mode moved:** it is now a switch on the **Wordle** screen, above Start game, and has been removed from Settings. The "Hard" tag still shows on the board.
- **Game descriptions on hover:** the menu shows only the game titles, and the description slides in when you hover over a game or tab to it with the keyboard. On touch screens, which have no hover, the descriptions stay visible.
- **Background upload fix:** uploads were already being applied, but big photos (phone photos especially) were too large for browser storage and failed to save. The new colours were saved but the picture was not, so after a reload only the colours had changed. Uploaded pictures are now shrunk to at most 1920 px and saved, so the background stays after a reload. A 40 MB test image came out at about 1.4 MB. If saving still fails, the picture is used for that visit only, you are told so, and the colour change is not saved on its own. "Use default" restores the original.
- **Animation:** rising glass bubbles and slow drifting glows sit behind every screen. The title also floats gently and the Play button pulses. The bubbles take on the background colours, pause when the tab is hidden, and are switched off for people who have "reduce motion" turned on.
- **About page:** it describes Archive Word Games! as Clyde Justine Nate's passion project and an ongoing one, with more word games being added and some still in development. It also has a short line about you and Email and LinkedIn buttons. Contact details come from your resume: Naga City, Camarines Sur, clydeernate@gmail.com and linkedin.com/in/clydejustinenate. **Your phone number is left out** on purpose because the page is public; it is easy to add.

---


## Update 1: words, music, sliders and game options

Replace `index.html` and `words.js` in your game folder with the new versions. `background.png` is unchanged.

## What changed

### 1. `words.js`: every dictionary word, 5 to 16 letters
- `allowed[n]` now holds **every** word of exactly `n` letters from `words_dictionary.json`, for n = 5 to 16. That is **354,000+ words**; it was about 108,000 before.
  - Only plain a-z words are kept. The two hyphenated entries (`jean-christophe`, `jean-pierre`) are excluded.
  - Counts per length: 5 → 15,918 · 6 → 29,874 · 7 → 41,997 · 8 → 51,626 · 9 → 53,403 · 10 → 45,872 · 11 → 37,538 · 12 → 29,124 · 13 → 20,944 · 14 → 14,148 · 15 → 8,846 · 16 → 5,182.
- `answers[n]` is the list of **common words the secret word is picked from**. Picking secret words from all 354,000 entries would make most games unwinnable, because the dictionary is full of obscure words.
  - Every length from 5 to 16 now has answers. Length 16 had none before. Lengths 12 to 16 were expanded.
  - Every answer is checked to be in `allowed`, with the right length and only a-z letters.
- A few old answers were dropped because they are **not in your dictionary**: `google, hazmat, qwerty, regexp, tarball, website, bytecode, codename, copyleft, homepage, segfault, timezone, workflow, multipart, passphrase, standalone, workaround, highlighter`.
- The file is about 3.7 MB. It loads once, and the game still opens quickly.

### 2. Background music is on by default
- `music` now defaults to **on**.
- Browsers block audio until the person interacts with the page, so the music starts on the **first tap or key press**. This is a browser rule and can't be bypassed.
- Settings saved by the old version (which defaulted to off) are not carried over, so existing players also get music on. If they turn it off now, that choice is remembered.
- The music button and the Settings toggle show the correct on/off state.

### 3. Sliders are visible
- The old sliders removed the browser's default look but only styled the track for Chrome and Safari. In **Firefox they had no track or thumb**.
- Sliders now have an explicit track, a coloured filled part, a white outline and a large thumb in Chrome, Safari, Edge and Firefox. This applies to Music volume and Glass transparency, plus the three new sliders below.
- I tested this in Chromium. I couldn't run Firefox here, so the Firefox styles are written to its standard slider rules but not tested.

### 4. New game options
| Game | New option | Range | Where |
|---|---|---|---|
| **Wordle** | Word length **slider** (replaces the 5/6/7/8 buttons) | 5 to 16 letters | Menu → Wordle |
| **Hangman** | Word length slider (new screen before the game) | 5 to 16 letters | Menu → Hangman |
| **Word Search** | Number of hidden words slider (new screen before the game) | 3 to 15 words | Menu → Word Search |

- Your choices are saved.
- **Resume game** buttons appear on each setup screen while a game is in progress. Starting a new game asks for confirmation first.
- The end-of-game popups have a **Change length** or **Change word count** button.
- **Wordle with long words:** the tile gap shrinks and the panel widens on large screens so 16 tiles always fit on one row. Tile flip animation is sped up for long words so a guess doesn't take several seconds.
- **Hangman:** picks a word of exactly the length you chose.
- **Word Search:** the grid grows with the word count, with a live "Grid size" hint on the slider screen.

  | Words | Grid |
  |---|---|
  | 3 to 6 | 8×8 |
  | 7 to 9 | 10×10 |
  | 10 to 12 | 12×12 |
  | 13 to 15 | 14×14 |

  - If a word can't be placed, the game rebuilds with new words, so the grid always contains exactly the number you asked for. The words never overlap each other as substrings.
  - It now uses words of 5 to 9 letters. The 8×8 grid still uses 5 to 7.

### 5. Other fixes
- `index.html` now loads **`words.js`** directly. Before, it tried `words_3.js` first, which could silently override your new list if an old copy was in the folder.
- If `words.js` ever fails to load, the built-in backup list still works for 5 to 8 letters, and the sliders cap themselves at 8.
- The Anagram game and the "valid alternative word" check use the full dictionary.
- Updated the "How to play" text and the menu descriptions to match.

## How it was tested
Automated checks in headless Chromium:
- `words.js` structure: every list has the right word length, only a-z letters, no duplicates, and every answer is in `allowed`.
- Wordle at 5, 8, 9, 12, 13 and 16 letters: the secret word is in the dictionary, the board fits on screen, and the game can be won. An obscure dictionary word is accepted as a guess and gibberish is rejected.
- Hangman at 5, 11 and 16 letters, and winning a round.
- Word Search at 3, 5, 6, 7, 10, 13 and 15 words: correct word count and grid size, grid fits the panel, and 40 out of 40 builds placed every word at each count from 3 to 15. A full game was also solved by selecting each word.
- Old saved settings are migrated, and music toggles and persists.
- No JavaScript errors in any run.
