# Sri Lanka Driving Licence Practice Test 🇱🇰

An interactive web application to help candidates prepare for the **Sri Lanka Department of Motor Traffic (DMT) written driving examination**.

## Features

- **96-question bank** covering all official exam topics
- **40 random questions** per session — different every time
- **Visual signs** — 27 questions display the actual road sign, traffic signal, or road marking as an SVG illustration (including animated flashing lights)
- **Instant feedback** — see whether you were right and what the correct answer is after each question
- **Results & review** — score, pass/fail verdict, and a full question-by-question breakdown at the end
- **Pass threshold: 80% (32/40)** — same as the real exam
- Works on desktop and mobile

## Topics Covered

| Topic | Questions |
|---|---|
| Traffic Signs | 15 |
| Road Rules | 11 |
| Safe Driving | 12 |
| Traffic Regulations | 10 |
| Vehicle Maintenance | 8 |
| Miscellaneous | 8 |
| Road Markings | 7 |
| Traffic Lights | 5 |
| Speed Limits | 5 |
| Emergency & First Aid | 5 |
| Pedestrians & Cyclists | 4 |
| Parking | 3 |
| Motorway & Expressway | 3 |

## Local Usage

No installation or server required — just open the file in a browser:

```bash
open index.html
```

## Deploying to WSO2 Choreo

### Prerequisites
- A [Choreo](https://console.choreo.dev) account
- This repository pushed to GitHub

### Steps

1. **Log in** to [Choreo Console](https://console.choreo.dev)

2. **Create a new component**
   - Go to your project → **Components** → **+ Create**
   - Select component type: **Web Application**
   - Connect your GitHub account and select this repository
   - Branch: `main`

3. **Configure the build**
   - Build pack: **Docker**
   - Dockerfile path: `Dockerfile`
   - Docker context: `.`

4. **Deploy**
   - Click **Deploy** → **Build & Deploy**
   - Choreo will build the Docker image, push it, and deploy the app
   - Once deployed, the public URL is shown in the **Endpoints** tab

5. **Access**
   - Open the public URL from the Choreo Endpoints tab
   - The app is served on port `8080` inside the container; Choreo maps it to HTTPS

### Architecture

```
Browser → Choreo (HTTPS) → nginx container (port 8080) → index.html
```

The entire application is a single `index.html` file served by an nginx:alpine container.

## Project Structure

```
driving-test/
├── index.html              # The entire application (HTML + CSS + JS)
├── Dockerfile              # nginx-based container for Choreo
├── nginx.conf              # nginx server configuration (port 8080)
├── .choreo/
│   └── component.yaml      # Choreo component schema
├── CLAUDE.md               # AI assistant context and developer notes
└── README.md               # This file
```

## Contributing / Extending

To add questions, edit the `QUESTIONS` array in `index.html`. See `CLAUDE.md` for detailed instructions on adding questions and new SVG signs.

## Disclaimer

This is a practice tool based on publicly available DMT exam topics. Always study the official [Department of Motor Traffic](https://dmt.gov.lk) handbook as the primary source.
