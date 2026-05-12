# Sri Lanka Driving Licence Practice Test — Project Context

## What this is
A fully self-contained bilingual single-page web app for practising the Sri Lanka Department of Motor Traffic (DMT) written driving licence examination. Supports **English** and **Sinhala (සිංහල)**. No framework, no build step, no dependencies — one file: `index.html`.

## Tech stack
- Pure HTML5 / CSS3 / Vanilla JavaScript
- All SVG road signs, traffic lights, and road markings drawn inline (no image assets)
- Bilingual: English and Sinhala with a header toggle
- Hosted on GitHub Pages and deployable to WSO2 Choreo via Docker/nginx

## Question banks

### English (`const QUESTIONS`) — 96 questions
| Category | Count | Has SVG illustrations |
|---|---|---|
| Traffic Signs | 15 | Yes — all 15 |
| Road Rules | 11 | — |
| Safe Driving | 12 | — |
| Traffic Regulations | 10 | — |
| Vehicle Maintenance | 8 | — |
| Miscellaneous | 8 | — |
| Road Markings | 7 | Yes — 6 of 7 |
| Traffic Lights | 5 | Yes — all 5 (animated) |
| Speed Limits | 5 | — |
| Emergency & First Aid | 5 | Yes — railway crossing (animated) |
| Pedestrians & Cyclists | 4 | — |
| Parking | 3 | — |
| Motorway & Expressway | 3 | — |

### Sinhala (`const QUESTIONS_SI`) — 171 questions
Full official DMT Sinhala-medium question bank (Q1–Q172, Q153 blank/skipped). All 171 questions sourced from the official PDF. Same SVG keys as English bank (signs are language-neutral).

| Category (Sinhala) | Count | Has SVG illustrations |
|---|---|---|
| මාර්ග සංඥා | 50 | Yes — all sign questions |
| ආරක්ෂිත ධාවනය | 35 | — |
| රිය නඩත්තු | 25 | — |
| රථ ගමනාගමන ආලෝකය | 19 | Yes — traffic lights |
| මාර්ග ලකුණු | 14 | Yes — incl. road diagram |
| රථ වාහන රෙගුලාසි | 11 | — |
| රිය නතර කිරීම | 6 | — |
| හදිසි & ප්‍රථමාධාර | 5 | — |
| ද්‍රුතගාමී මාර්ග | 4 | — |
| පාද ගමනාකරු | 1 | — |
| වේග සීමා | 1 | — |

## Key data structures

### SVGs
```js
const S = { noEntry: `<svg.../>`, ltAmber: `<svg.../>`, mkBroken: `<svg.../>`, ... }
```
All signs are stored here. Keys used by both English and Sinhala question banks.

### Question object shape
```js
{
  category: "Traffic Signs",  // string — English for QUESTIONS, Sinhala for QUESTIONS_SI
  q: "What does this sign mean?",
  img: S.noEntry,             // optional — any S.xxx key; omit for text-only questions
  opts: ["A", "B", "C", "D"],
  ans: 1                      // 0-indexed correct option
}
```

### Language system
```js
const UI = { en: { title, h2, nameLbl, fbCorrect, passMsg, ... },
             si: { ... } }   // all UI strings in both languages
let lang = 'en';             // current language; set by setLang('en'|'si')
```
`setLang(l)` updates all static DOM text and resets to the welcome screen. The question bank used is chosen at `startTest()` / `retakeTest()` based on `lang`.

### Session flow
1. User selects language (EN / සිං) → `setLang()`
2. User enters name → `startTest()` → shuffles correct bank → picks 40
3. `renderQuestion()` — renders question, optional SVG sign, 4 options
4. `selectOption(idx)` — locks options, shows feedback
5. `nextQuestion()` — advances index; on Q40 calls `showResults()`
6. `showResults()` — computes score, renders review table, pass/fail
7. `retakeTest()` / `goHome()` — restart or return to welcome

## Adding English questions
Append to `const QUESTIONS` in `index.html`:
```js
{
  category: "Traffic Signs",
  q: "What does this sign mean?",
  img: S.noEntry,              // omit if no sign image needed
  opts: ["Option A", "Option B", "Option C", "Option D"],
  ans: 1
}
```

## Adding Sinhala questions
Append to `const QUESTIONS_SI` in `index.html` — same shape, Sinhala text, same `S.xxx` SVG keys:
```js
{
  category: "මාර්ග සංඥා",
  q: "මෙම සංඥාව දකින විට?",
  img: S.noEntry,
  opts: ["A", "B", "C", "D"],
  ans: 1
}
```

## Adding a new SVG sign
Add to `const S` (before `const QUESTIONS`):
```js
mySign: `<svg viewBox="0 0 120 120" width="120" height="120" xmlns="http://www.w3.org/2000/svg">...</svg>`,
```
Then reference `S.mySign` in any question's `img` field in either bank.

## Deployment

### GitHub Pages (live)
URL: `https://jan1tha.github.io/sl-driving-test/`
Auto-deploys on every push to `main`. No config needed.

### WSO2 Choreo (Docker)
The app runs in an nginx:alpine container on port 8080.
- `Dockerfile` — builds the image
- `nginx.conf` — port 8080, gzip, security headers, SPA routing
- `.choreo/component.yaml` — Choreo component schema (`schemaVersion: "1.0"`)

In Choreo: create a **Web Application** component, build pack **Docker**, Dockerfile path `Dockerfile`.

## Local development
```bash
open index.html   # no server required
```
