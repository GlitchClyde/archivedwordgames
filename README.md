# Archive Word Games

Two classic word games in one page: **Wordle** (5 to 8 letters) and **Hangman**. It runs entirely in your browser, with no sign-up, no server and no tracking.

![Preview: frosted-glass menu over a lake view](background.png)

## Play

1. Keep these three files in the same folder:
   - `index.html` (the game)
   - `words.js` (word lists)
   - `background.png` (default backdrop)
2. Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari).

To host it online, upload the folder to any static host (GitHub Pages, Netlify, Cloudflare Pages).

## How to play

**Wordle.** Choose a word length, then guess the hidden word in six tries. After each guess, tiles show how close you were:

| Tile | Meaning |
| --- | --- |
| Green | Right letter, right spot |
| Blue | Letter is in the word, wrong spot |
| Dark | Letter is not in the word |

**Hard mode** requires every revealed hint to be used in your next guess.

**Hangman.** Pick letters to uncover the word. Each wrong letter adds a part to the drawing, and six misses end the game.

You can use the on-screen keys or your keyboard (letters, `Enter`, `Backspace`).

## Features

- Wordle with 5, 6, 7 or 8 letter words, plus an optional hard mode
- Hangman with words of 6 to 12 letters
- Win/loss stats and streaks for Wordle, saved on your device
- **Share result** button that copies an emoji grid of your guesses
- Adjustable glass transparency
- Upload your own background image. The game colors adapt to it automatically
- Color-blind friendly palette (orange and blue, with a dot on correct letters)
- Responsive layout that fits phones, tablets and desktops
- Keyboard accessible, screen reader labels on the board, and reduced-motion support

## Settings

Open **Settings** from the main menu.

| Setting | What it does |
| --- | --- |
| Hard mode | Applies to your next new Wordle game |
| Color-blind colors | Switches to an orange and blue palette |
| Glass transparency | Shows more or less of the background through the panels |
| Background | Upload an image, or return to the default |
| Reset all settings | Restores defaults. Your current game is unaffected |

Settings, stats and your uploaded background are stored in your browser's `localStorage`. They never leave your device.

## Project structure

```
index.html      Markup, styles and game logic (single file)
words.js        Word lists: allowed[n] for valid guesses, answers[n] for secret words
background.png  Default background image
```

### Customizing the word lists

`words.js` defines `window.WORD_DATA` with two objects keyed by word length (5 to 16). Each value is a space-separated string of lowercase words.

- `allowed[n]`: every word accepted as a guess
- `answers[n]`: words the game can pick as the secret word. Every answer is also accepted as a guess

Hangman picks from the answers of lengths 6 to 12.

### Troubleshooting

- **"Word list missing" message:** `words.js` must sit in the same folder as `index.html`.
- **Colors don't change after uploading an image:** very gray images have no dominant hue, so the default blue is used.
- **Upload isn't remembered:** very large images can exceed browser storage. The background then lasts until you close the page.

## Browser support

Any current version of Chrome, Edge, Firefox or Safari. The frosted-glass look uses `backdrop-filter`. Browsers without it show a darker solid panel instead.
