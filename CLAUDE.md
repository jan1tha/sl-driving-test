# Sri Lanka Driving Licence Practice Test — Project Context

## What this is
A fully self-contained static single-page web app for practising the Sri Lanka Department of Motor Traffic (DMT) written driving licence examination. No framework, no build step, no dependencies — one file: `index.html`.

## Tech stack
- Pure HTML5 / CSS3 / Vanilla JavaScript
- All SVG road signs and markings are drawn inline (no image assets)
- Deployed as a containerised static site via nginx on WSO2 Choreo

## Question bank
- **96 questions** across 13 categories, randomly shuffled each session
- **40 questions** selected per session (same as real DMT exam)
- **Pass threshold: 80% (32/40)** — same as official exam
- **27 questions** show inline SVG illustrations of the actual sign/signal/marking

| Category | Count | Has illustrations |
|---|---|---|
| Traffic Signs | 15 | Yes — all 15 show SVG signs |
| Road Rules | 11 | — |
| Safe Driving | 12 | — |
| Traffic Regulations | 10 | — |
| Vehicle Maintenance | 8 | — |
| Miscellaneous | 8 | — |
| Road Markings | 7 | Yes — 6 of 7 show SVG diagrams |
| Traffic Lights | 5 | Yes — all 5 show animated SVG lights |
| Speed Limits | 5 | — |
| Emergency & First Aid | 5 | Yes — railway crossing signal (animated) |
| Pedestrians & Cyclists | 4 | — |
| Parking | 3 | — |
| Motorway & Expressway | 3 | — |

## Key data structures
- `const S` — SVG strings keyed by sign name (e.g. `S.noEntry`, `S.ltAmber`)
- `const QUESTIONS` — array of `{ category, q, img?, opts[], ans }` objects
- `img` is optional; if present, the SVG is rendered between the question text and answer options

## Adding questions
Add an object to `QUESTIONS` in `index.html`:
```js
{
  category: "Traffic Signs",   // one of the 13 categories
  q: "What does this sign mean?",
  img: S.noEntry,              // optional — reference an S.xxx key or omit
  opts: ["Option A", "Option B", "Option C", "Option D"],
  ans: 1                       // 0-indexed index of the correct option
}
```

## Adding a new SVG sign
Add an entry to `const S` before `const QUESTIONS`:
```js
mySign: `<svg viewBox="0 0 120 120" width="120" height="120" xmlns="http://www.w3.org/2000/svg">...</svg>`,
```
Then reference `S.mySign` in a question's `img` field.

## Deployment — Choreo
The app runs inside an nginx:alpine container listening on port 8080.
- `Dockerfile` — builds the container image
- `nginx.conf` — nginx server block (port 8080, gzip, security headers)
- `.choreo/component.yaml` — Choreo component schema

See README.md for step-by-step Choreo deployment instructions.

## Local development
Just open `index.html` in any browser. No server needed.
