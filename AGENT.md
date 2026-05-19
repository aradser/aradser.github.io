# aradser.github.io

Personal GitHub Pages site with two independent mini-projects.

## Structure

```
index.html          # Lecture landing page (RS2021)
kalgav/
  index.html        # Kalgav backpack-picker app
  kits/             # Kit images (<code>_<slug>.jpg)
prism.js / prism.css  # Syntax highlighting (used by root index.html)
```

---

## Root page — Lecture QR code target

`index.html` is the URL encoded in a QR code shown at the RS2021 lecture. It contains:
- A link to the Google Slides presentation
- Syntax-highlighted Swift/RealityKit source for "Dig the Diglett", an AR game built with ARView where Digletts spawn on detected surfaces and the player taps to dig them out.

No build step. Plain HTML + Prism.js for syntax highlighting.

---

## Kalgav (`kalgav/`) — Backpack kit picker

Hebrew RTL single-page app (no framework, no build). Backpack designs were extracted from a supplier PDF and are stored as local JPEGs in `kalgav/kits/`.

### What it does

Lets a child swipe through ~50 backpack kit designs (Tinder-style) and pick a favourite:

| Feature | Detail |
|---|---|
| Browse / swipe | Drag or use ♥ / ✕ buttons; right = like, left = skip |
| Gender filter | All / בנים (boys) / בנות (girls) |
| Liked list | Grid of saved favourites, filterable by category |
| VS mode | Elimination tournament of liked kits → single winner |
| Lightbox | Tap any image to zoom full-screen |
| Undo | Reverts the last swipe |
| Persistence | `localStorage` — survives page refresh |

### Kit data

Hardcoded `KITS` array at the top of `kalgav/index.html`. Each entry:

```js
{ code: "93609", name: "משחק כדורגל", cat: "sports", gender: "boys",
  img: "https://aradser.github.io/kalgav/kits/93609_soccer-game.jpg" }
```

Categories: `characters`, `sports`, `animals`, `fantasy`, `themes`.

### Adding / editing kits

1. Drop the image into `kalgav/kits/` as `<code>_<slug>.jpg`.
2. Add an entry to the `KITS` array in `kalgav/index.html`.
3. No rebuild needed — push and GitHub Pages serves it.

### localStorage keys

| Key | Contents |
|---|---|
| `kalgav_likes_v2` | JSON array of liked kit codes |
| `kalgav_seen_v2` | JSON array of swiped-on kit codes |
| `kalgav_gender_v2` | Active gender filter string |

---

## Deployment

GitHub Pages — push to `main`, the site updates automatically. No CI, no build pipeline.
