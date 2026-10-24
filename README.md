# ITZFIZZ Scroll Hero

A scroll-driven hero section built with **Next.js (App Router)**, **React**, **JavaScript**, **Tailwind CSS**, **GSAP** and **GSAP ScrollTrigger**. No other runtime libraries.

## Run it

```bash
npm install
npm run dev      # http://localhost:3000
npm run build && npm start   # production check
```

Requires Node 18.17+. The headline font (Space Grotesk) is loaded through `next/font/google`, so the first build needs internet access.

## Structure

```
app/
  layout.js        font + metadata
  page.js          renders <Hero /> plus spacer content
  globals.css      Tailwind layers, page background, grain overlay
components/
  Hero.jsx         layout + all GSAP animation
  Car.jsx          original inline-SVG top-down car (no image assets)
```

## How the animation works

**Page load** (`gsap.context`, one timeline in `Hero.jsx`)
1. Green band rises and fades in.
2. Headline reveals letter by letter through an overflow mask (`yPercent` + stagger).
3. Car glides in from the right.
4. The four stat cards arrive one after another, with a count-up on each percentage.
5. Scroll hint fades in last.

**Scroll** (`gsap.matchMedia` + `ScrollTrigger`, `scrub: 1`, section pinned)
- The car drives left across the band while rotating and scaling up.
- Headline drifts up and softens.
- Stat cards move with a gentle opposing parallax.
- Scroll hint fades out.
- Everything is tied to scroll progress, so scrolling back up reverses it exactly.
- Desktop/tablet and mobile use different distances, rotation and scale.

**Design decisions worth knowing**
- Intro and scroll animations target *different wrapper elements* (`data-car-intro` vs `data-car-scroll`, `data-stat` vs `data-stat-wrap`) so they never fight over the same transform.
- `prefers-reduced-motion` is respected: content simply appears and the scroll pin is skipped.
- Statistics are original placeholder content.
