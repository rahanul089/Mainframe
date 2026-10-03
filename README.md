# Mainframe

A full-screen hero landing page for the creative agency **Mainframe**, built with React, TypeScript, Vite and Tailwind CSS.

The background video is not played automatically. It scrubs forward and backward as you move the mouse horizontally. A typewriter greeting, a set of action pills and a responsive navbar sit on top.

## Features

- **Mouse-scrubbed background video:** horizontal mouse movement seeks the video, with seek-flood protection (`seeked` handler)
- **Typewriter intro:** custom `useTypewriter` hook with a blinking cursor
- **Action pills:** fade and slide in 400ms after load, independent of the typewriter
- **Copy-to-clipboard:** the "Reach us: hello@mainframe.co" pill copies the email
- **Responsive navbar:** desktop links, plus a mobile hamburger with an animated full-screen overlay

## Tech stack

| Tool | Purpose |
| --- | --- |
| React 18 | UI |
| TypeScript | Type safety |
| Vite 5 | Dev server and build |
| Tailwind CSS 3 | Styling |

No other UI libraries are used.

## Getting started

Requires Node.js 18 or newer.

```bash
npm install
npm run dev
```

Open the local URL printed in the terminal (usually http://localhost:5173).

## Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Type-check and build for production into `dist/` |
| `npm run preview` | Preview the production build locally |

## Project structure

```
mainframe/
├── index.html            # Font stylesheet links
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── postcss.config.js
├── tsconfig*.json
└── src/
    ├── main.tsx          # React entry point
    ├── App.tsx           # Video, navbar, hero, useTypewriter hook
    ├── index.css         # Tailwind layers, font variables, blink keyframes
    └── vite-env.d.ts
```

## Customisation

All of the following live in `src/App.tsx`:

| What | Where |
| --- | --- |
| Video source | `VIDEO_SRC` |
| Scrub speed | `SENSITIVITY` (default `0.8`) |
| Contact email | `EMAIL` |
| Typewriter text | `INTRO` |
| Nav links | `NAV_LINKS` |
| Action buttons | `PILLS` |

Fonts are loaded in `index.html` and mapped to `--font-heading` and `--font-body` in `src/index.css`. Only the logo text uses the heading font.

## Deploy

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Mainframe hero"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### 2. Host on Vercel

1. Go to [vercel.com](https://vercel.com) and choose **Add New → Project**.
2. Import your GitHub repository.
3. Vercel detects Vite automatically (build command `npm run build`, output directory `dist`).
4. Click **Deploy**.

Every push to `main` redeploys automatically.

## Notes

- The video only responds to a mouse. On touch devices it stays on its first frame.
- Browsers can be slow to seek long or large videos. A video encoded with frequent keyframes scrubs more smoothly.
