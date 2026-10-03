<div align="center">

# Mainframe®

**A full-screen, interactive hero landing page for a creative agency.**
Move your mouse to scrub the film. Say hello to A.R.I.A.

![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?logo=tailwindcss&logoColor=white)
![Deploy](https://img.shields.io/badge/Deploy-Vercel-000000?logo=vercel&logoColor=white)

[Live demo](https://your-project.vercel.app) · [Report an issue](../../issues)

<!-- Add a screenshot or GIF here:
![Mainframe hero](./docs/preview.png) -->

</div>

---

## About

Mainframe is a single-screen landing page for a fictional creative agency. The idea is simple: instead of a looping background video, the visitor controls the film. Moving the mouse left or right moves the video forward or backward, so the page feels hands-on from the first second.

On top of the video, an assistant called **A.R.I.A** (Adaptive Response Interface Agent) greets visitors with a typewritten message and offers a few ways to get started: pitch an idea, join the team, say hello, or see how the studio works.

## Highlights

| Feature | What it does |
| --- | --- |
| **Mouse-scrubbed video** | Horizontal mouse movement seeks the background video. It never autoplays. |
| **Seek-flood protection** | The next seek is queued from the `seeked` event, so fast mouse movement doesn't overload the video decoder. |
| **Typewriter greeting** | A custom `useTypewriter` hook reveals the message character by character with a blinking cursor. |
| **Action pills** | Five pill buttons fade and slide in shortly after load, without waiting for the typing to finish. |
| **One-click email copy** | The contact pill copies `hello@mainframe.co` to the clipboard. |
| **Responsive navbar** | Inline links on desktop, and an animated hamburger with a blurred full-screen menu on mobile. |
| **Custom typography** | A two-font system: a medium-weight heading face for the logo and a regular body face everywhere else. |

## How the video scrubbing works

1. A `mousemove` listener on `window` tracks the previous X position.
2. The horizontal movement is converted into a time offset:

   ```
   offset = (deltaX / window.innerWidth) × SENSITIVITY × video.duration
   ```

3. The target time is clamped between `0` and `video.duration`, then applied to `video.currentTime`.
4. If the video is still seeking, the new target waits. When the `seeked` event fires, the video jumps to the latest target.

`SENSITIVITY` defaults to `0.8`. Higher values make the video move faster per mouse movement.

## Tech stack

- **React 18** for the UI
- **TypeScript** for type safety
- **Vite 5** for the dev server and production build
- **Tailwind CSS 3** for styling

No other UI libraries are used.

## Getting started

Requires **Node.js 18 or newer**.

```bash
# 1. Install dependencies
npm install

# 2. Start the dev server
npm run dev
```

Then open http://localhost:5173.

| Command | Description |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Type-check and build for production into `dist/` |
| `npm run preview` | Preview the production build locally |

## Project structure

```
mainframe/
├── index.html           # Font stylesheet links
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── postcss.config.js
├── tsconfig*.json
└── src/
    ├── main.tsx         # React entry point
    ├── App.tsx          # Video, navbar, hero and useTypewriter hook
    ├── index.css        # Tailwind layers, font variables, blink keyframes
    └── vite-env.d.ts
```

## Customising

Most content lives at the top of `src/App.tsx`:

| Constant | Controls |
| --- | --- |
| `VIDEO_SRC` | The background video URL |
| `SENSITIVITY` | How fast the video scrubs |
| `EMAIL` | The contact address that gets copied |
| `INTRO` | The typewriter message |
| `NAV_LINKS` | Navbar and mobile menu links |
| `PILLS` | The white action buttons |

Fonts are loaded in `index.html` and exposed as `--font-heading` and `--font-body` in `src/index.css`.

## Deployment

### GitHub

```bash
git init
git add .
git commit -m "Mainframe hero"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### Vercel

1. Go to [vercel.com](https://vercel.com) and choose **Add New → Project**.
2. Import the GitHub repository.
3. Vercel detects Vite automatically (build command `npm run build`, output directory `dist`).
4. Click **Deploy**. Every push to `main` redeploys.

## Known limitations

- Video scrubbing needs a mouse, so on touch devices the video stays on its first frame.
- Seeking can feel choppy on long or heavily compressed videos. A video encoded with frequent keyframes scrubs more smoothly.

## License

Add a license of your choice (for example [MIT](https://choosealicense.com/licenses/mit/)) before sharing the repository publicly.
