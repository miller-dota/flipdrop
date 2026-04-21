# FlipDrop

A minimal coin toss app built with React. Features a real 3D flip animation using a King Charles III £2 silver coin (2023).

---

## Stack

- React 18
- DM Mono (Google Fonts)
- Pure CSS 3D animation — no animation libraries

---

## Getting Started

```bash
npx create-react-app flipdrop
cd flipdrop
```

Replace `src/App.js` with `FlipDrop.jsx`, then:

```bash
npm start
```

---

## Usage

```jsx
import FlipDrop from './FlipDrop';

export default function App() {
  return <FlipDrop />;
}
```

---

## Features

- 3D coin flip animation with randomised spin count
- Lands correctly on heads or tails every time
- Result label fades in after the coin settles
- Running tally — heads / total / tails
- Fully self-contained — coin images are base64 embedded, no external assets needed

---

## Coin

| Face   | Design                          |
|--------|---------------------------------|
| Heads  | King Charles III portrait       |
| Tails  | Royal Cypher with crown, 2023   |

Denomination: £2 · Royal Mint · 2023

---

## Customisation

| What             | Where in code              |
|------------------|----------------------------|
| Coin images      | `HEADS` / `TAILS` constants |
| Flip duration    | `animation: toss 1.5s`     |
| Font             | `@import` at top of styles |
| Button style     | `.btn` class               |

---

## Font

Uses **DM Mono** via Google Fonts. To use Departure Mono instead, replace the import:

```css
@import url('https://fonts.googleapis.com/css2?family=DM+Mono...');
```

with a local font-face pointing to your Departure Mono files, then update `font-family` to `'Departure Mono', monospace`.

---

## License

MIT
