# Sri Lanka Driving Licence Practice Test 🇱🇰

An interactive bilingual web application to help candidates prepare for the **Sri Lanka Department of Motor Traffic (DMT) written driving examination** — available in **English** and **සිංහල (Sinhala)**.

## Live Demo

**GitHub Pages:** https://jan1tha.github.io/sl-driving-test/

## Features

- **Bilingual** — full English and Sinhala (සිංහල) support; toggle with the `EN` / `සිං` buttons in the header
- **Two official question banks** — 96 English questions and 171 Sinhala-medium questions sourced from the official DMT question bank
- **40 random questions** per session — different every time
- **Visual signs** — 27 questions display the actual road sign, traffic signal, or road marking as an inline SVG illustration (including animated flashing lights)
- **Instant feedback** — correct/wrong verdict with the right answer shown after each question
- **Results & review** — score, pass/fail verdict, and a full question-by-question breakdown at the end
- **Pass threshold: 80% (32/40)** — same as the real exam
- Works on desktop and mobile; no installation or internet connection required after load

## Question Banks

### English — 96 questions

| Topic | Questions | Visual signs |
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

### සිංහල (Sinhala) — 171 questions

Full official DMT Sinhala question bank (Q1–Q172 from the official PDF, Q153 blank/skipped).

| විෂය | ප්‍රශ්න | දෘශ්‍ය සංඥා |
|---|---|---|
| මාර්ග සංඥා | 50 | ඔව් — සංඥා ප්‍රශ්න සියල්ල |
| ආරක්ෂිත ධාවනය | 35 | — |
| රිය නඩත්තු | 25 | — |
| රථ ගමනාගමන ආලෝකය | 19 | ඔව් — ආලෝක සංඥා |
| මාර්ග ලකුණු | 14 | ඔව් — මාර්ග රූප සටහන් |
| රථ වාහන රෙගුලාසි | 11 | — |
| රිය නතර කිරීම | 6 | — |
| හදිසි & ප්‍රථමාධාර | 5 | — |
| ද්‍රුතගාමී මාර්ග | 4 | — |
| පාද ගමනාකරු | 1 | — |
| වේග සීමා | 1 | — |

## Local Usage

No installation or server required — open directly in any browser:

```bash
open index.html
```

## Deploying to WSO2 Choreo

### Prerequisites
- A [Choreo](https://console.choreo.dev) account
- This repository connected to Choreo

### Steps

1. **Log in** to [Choreo Console](https://console.choreo.dev)

2. **Create a new component**
   - Go to your project → **Components** → **+ Create**
   - Select component type: **Web Application**
   - Connect your GitHub account and select this repository (`jan1tha/sl-driving-test`)
   - Branch: `main`

3. **Configure the build**
   - Build pack: **Docker**
   - Dockerfile path: `Dockerfile`
   - Docker context: `.`

4. **Deploy**
   - Click **Deploy** → **Build & Deploy**
   - Choreo builds the Docker image and deploys it
   - The public URL appears in the **Endpoints** tab

5. **Access**
   - The app is served on port `8080` inside the container; Choreo maps it to HTTPS

### Architecture

```
Browser → Choreo / GitHub Pages (HTTPS) → nginx container (port 8080) → index.html
```

The entire application is a single `index.html` file served by an nginx:alpine container.

## Project Structure

```
driving-test/
├── index.html              # Entire application — HTML + CSS + JS (both language banks)
├── Dockerfile              # nginx:alpine container for Choreo deployment
├── nginx.conf              # nginx config (port 8080, gzip, security headers)
├── .choreo/
│   └── component.yaml      # Choreo component schema
├── CLAUDE.md               # Developer context and AI assistant notes
└── README.md               # This file
```

## Contributing / Extending

All content lives in `index.html`. See `CLAUDE.md` for detailed instructions on:
- Adding English questions to `QUESTIONS`
- Adding Sinhala questions to `QUESTIONS_SI`
- Adding new SVG road signs to `const S`

## Disclaimer

This is a practice tool based on publicly available DMT exam topics. Always study the official [Department of Motor Traffic](https://dmt.gov.lk) handbook as the primary source.
