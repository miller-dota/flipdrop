# FlipDrop

![React](https://img.shields.io/badge/React-18-61dafb?style=flat-square&logo=react) ![License](https://img.shields.io/badge/license-MIT-green?style=flat-square) ![Stars](https://img.shields.io/github/stars/yourusername/flipdrop?style=flat-square) ![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)

**A minimal, zero-dependency coin toss app built with React.** Features a real 3D flip animation using an authentic King Charles III £2 silver coin (Royal Mint, 2023). No backend. No API keys. No installs beyond React itself.

Built with pure CSS 3D transforms — no animation libraries, no bloat. One file, self-contained, drop it in and go.

---

> **💡 Tip — Self-Contained by Design**
>
> Both coin faces (heads and tails) are base64-encoded directly inside `FlipDrop.jsx`. No external assets, no broken image paths, no CDN dependencies. The file works anywhere React works.

---

<div style="text-align: center;">
  <img src="flipdrop demo.png" alt="isolated" width="600"/>
</div>

<img src="flipdrop motion.gif" width="400" />

## Features

- 🪙 **Real 3D Flip Animation** — CSS `rotateY` with perspective gives a true coin-in-air effect
- ✅ **Always Lands Correctly** — result is decided first, then the animation lands on the matching face
- 🎲 **Randomised Spin Count** — each flip spins a different number of times so it never feels scripted
- 📊 **Live Tally** — running count of heads, tails, and total flips
- 🔤 **DM Mono Typography** — clean monospace font throughout; swap to Departure Mono with one line
- 🖤 **White Single UI** — pure white background, no gradients, no shadows, no noise
- 📦 **Zero External Assets** — coin images are embedded as base64, fully portable
- ⚡ **Single File** — entire app lives in one `.jsx` file, no component splitting needed

---

## Installation

**Requirements:** Node.js 16+ · React 18+

### Quick Start (Create React App)

```bash
npx create-react-app flipdrop
cd flipdrop
cp path/to/FlipDrop.jsx src/FlipDrop.jsx
```

Update `src/App.js`:

```jsx
import FlipDrop from './FlipDrop';

export default function App() {
  return <FlipDrop />;
}
```

Then run:

```bash
npm start
```

### Quick Start (Vite)

```bash
npm create vite@latest flipdrop -- --template react
cd flipdrop
npm install
cp path/to/FlipDrop.jsx src/FlipDrop.jsx
```

Update `src/App.jsx` the same way, then:

```bash
npm run dev
```

---

## Usage

### Basic

```jsx
import FlipDrop from './FlipDrop';

// Renders full-page coin toss UI
export default function App() {
  return <FlipDrop />;
}
```

### Toss Flow

1. Open the app — the coin displays heads side by default
2. Click **Flip** — the coin launches into a randomised 3D spin
3. The coin settles on the correct face (heads or tails)
4. The result label fades in below the coin
5. The tally updates — heads / total / tails

---

## Customisation

| What | Where in code | Example |
|---|---|---|
| Coin images | `HEADS` / `TAILS` constants | Swap in any base64 PNG |
| Flip duration | `animation: toss 1.5s` | Change `1.5s` to taste |
| Coin size | `.coin-stage` width/height | Default `220px` |
| Font family | `@import` + `font-family` | See Font section below |
| Button style | `.btn` class | Border, padding, colours |
| Brand name | `.brand` in JSX | `Flip<span>Drop</span>` |

### Swapping the Coin Images

Convert any PNG to base64 and replace the constants at the top of `FlipDrop.jsx`:

```bash
base64 -w 0 my-heads.png > heads.b64
base64 -w 0 my-tails.png > tails.b64
```

Then paste the output into:

```js
const HEADS = "data:image/png;base64,YOUR_BASE64_HERE";
const TAILS = "data:image/png;base64,YOUR_BASE64_HERE";
```

### Changing the Font

**DM Mono** (default) is loaded via Google Fonts. To use **Departure Mono** locally:

1. Download Departure Mono from [departuremono.com](https://departuremono.com)
2. Place the `.woff2` file in your `public/` folder
3. Replace the `@import` line at the top of the styles string:

```css
@font-face {
  font-family: 'Departure Mono';
  src: url('/DepartureMono-Regular.woff2') format('woff2');
  font-weight: 400;
}
```

4. Update `font-family` in `body`:

```css
body {
  font-family: 'Departure Mono', monospace;
}
```

---

## Project Structure

```
FlipDrop/
├── src/
│   ├── FlipDrop.jsx        # Entire app — styles, logic, markup
│   └── App.jsx             # Entry point (just renders <FlipDrop />)
├── public/
│   └── index.html          # Standard CRA/Vite shell
├── package.json
└── README.md
```

### Key Components (inside FlipDrop.jsx)

- **`HEADS` / `TAILS`** — Base64-encoded coin face images
- **`styles`** — Full CSS string injected via `<style>` tag
- **`FlipDrop()`** — Main component; owns all state
- **`toss()`** — Decides result, calculates end rotation, triggers animation
- **`.coin-wrap.spinning`** — CSS keyframe `toss` drives the 3D flip
- **`.tally`** — Renders heads / total / tails after the first flip

---

## Coin

| Face | Design |
|---|---|
| **Heads** | King Charles III portrait · effigy by Martin Jennings |
| **Tails** | Royal Cypher with St Edward's Crown · floral emblems of the four nations |

**Denomination:** £2 · Royal Mint · 2023  
**Material:** .999 fine silver (bullion coin)

---

## Development

### Animation Details

The flip uses CSS custom properties to pass the landing rotation into the keyframe:

```css
.coin-wrap.spinning {
  animation: toss 1.5s cubic-bezier(0.33, 0, 0.66, 1) forwards;
}

@keyframes toss {
  0%   { transform: rotateY(0deg) translateY(0px); }
  50%  { transform: rotateY(900deg) translateY(-80px); }
  100% { transform: rotateY(var(--end)) translateY(0px); }
}
```

- **Heads** lands at `n × 360°` (front face visible)
- **Tails** lands at `n × 360° + 180°` (back face visible)
- `backface-visibility: hidden` on each face ensures only one shows at a time

### State

```js
const [spin, setSpin]       // Animation running flag
const [result, setResult]   // "heads" | "tails" | null
const [show, setShow]       // Controls fade-in of result label
const [end, setEnd]         // CSS rotation value passed to keyframe
const [counts, setCounts]   // { heads: n, tails: n }
```

---

## Credits

FlipDrop was designed and built as a clean single-UI React experiment. Coin imagery courtesy of the [Royal Mint](https://www.royalmint.com). Typography by [DM Mono](https://fonts.google.com/specimen/DM+Mono).

---

## License

MIT — see `LICENSE` for details.

---

## Support

- 🐛 **Report issues** — GitHub Issues
- 💬 **Discussions** — GitHub Discussions

---

*© 2025 FlipDrop. All rights reserved.*
