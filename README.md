<div align="center">

# MISSION ARCHITECT

### Design it. Aim it. Fly it. Earn it.

**A browser-based space mission design, launch, and operations simulator powered by real NASA data.**

![NASA Space Apps](https://img.shields.io/badge/NASA%20Space%20Apps-2026-0B3D91?style=for-the-badge&logo=nasa&logoColor=white)
![Status](https://img.shields.io/badge/status-in%20development-yellow?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)
![Made with JavaScript](https://img.shields.io/badge/made%20with-JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

[Overview](#overview) · [Features](#features) · [Gameplay](#gameplay) · [NASA Data](#nasa-data-integration) · [Tech Stack](#tech-stack) · [Roadmap](#development-roadmap) · [Setup](#getting-started)

</div>

---

## Overview

Mission Architect is an interactive browser game where players design a spacecraft by dragging real parts onto a chassis, aim the launch with real orbital mechanics, fly through the real solar system dodging real asteroids, and earn a mission credit score — all powered by live NASA data.

The design phase is a puzzle. The launch is a skill test. The flight is a survival game. The debrief is a grade.

Built for the 2026 NASA Space Apps Challenge under the Space Mission Design Game category.

| Field | Detail |
|---|---|
| Platform | Browser (HTML/CSS/JS) — no install required |
| Genre | Mission design + orbital mechanics + operations simulator |
| Session Length | 30–60 minutes per mission |
| Audience | Students (beginner–intermediate), space enthusiasts, STEM learners |
| Difficulty Tiers | Cadet / Flight / Architect |

---

## The Challenge We're Solving

The official brief asks for a game where students can:

> *"Design, manage, and simulate a complete space mission while making engineering decisions, managing limited resources, and evaluating how each choice shapes the success of their mission."*

Mission Architect answers every requirement as a playable feature, not a menu, not a form, not a quiz.

| Challenge Requirement | How Mission Architect Delivers |
|---|---|
| Mission objectives | Each mission has explicit scientific goals with multiple success criteria |
| Spacecraft design | Drag-and-drop physical assembly inside a launch fairing |
| Scientific instruments | 8+ real instruments with mass, power, cost, and science return |
| Launch vehicles | Real vehicles with real payload capacities and reliability stats |
| Budgets | Hard budget cap with live tracking |
| Power | Live power budget (watts) that drains during operations |
| Mass | Center-of-gravity tracking; launch vehicle capacity constraint |
| Communications | Low-gain / high-gain / relay trade-offs |
| Orbital constraints | Launch angle affects trajectory, fuel, and intercept |
| Concept to operation | 5 complete phases: Select, Build, Aim, Fly, Debrief |
| Engineering decisions | Every drag, slider, and click has a real trade-off |
| Limited resources | Budget, mass, power, fuel, data, and time are all constrained |
| How choices shape success | Debrief shows exact cause-and-effect of every decision |

---

## Features

- Drag-and-drop spacecraft builder with physical parts, live mass/cost/power meters, and center-of-gravity warnings
- Launch angle GUI with real-time trajectory preview and real orbital math (Tsiolkovsky + Hohmann transfers)
- Live operations map where you fly through the real solar system with real planet positions and real asteroids
- Interactive events where you click on broken parts, reroute power, clean solar panels, realign comms
- Mission Credit Score with persistent progression, 7 rank tiers, and unlockables
- Codex with real NASA references for every instrument, vehicle, and event
- Real NASA data — launch windows, planet ephemeris, near-Earth objects, space weather, Mars weather
- Firebase leaderboards for global rankings per mission
- No install — runs in any modern browser

---

## Gameplay

Every mission runs through five phases.

### Phase 1 — Mission Select

A live mission board showing real upcoming launch windows. Each mission offers different vehicles, budgets, and destinations.

You learn that launch windows are constrained, vehicles have limits, and every mission is different.

### Phase 2 — Build (Drag and Drop)

A blueprint grid inside a launch fairing. Drag parts from a library onto the chassis.

**Part library (minimum viable set):**

| Part | Mass | Cost | Power | Notes |
|---|---|---|---|---|
| RTG (Pu-238) | 90 kg | $180M | +300 W | 14-year lifetime |
| Solar Array | 400 kg | $40M | +340 W | Dust-sensitive |
| Mass Spectrometer | 60 kg | $120M | -30 W | Organic detection |
| Camera Suite | 40 kg | $80M | -20 W | Imaging |
| Drill | 150 kg | $200M | -200 W | Sample retrieval |
| High-Gain Antenna | 200 kg | $180M | -40 W | 10 Mbps |
| Low-Gain Antenna | 30 kg | $20M | -10 W | 1 kbps |
| Radiation Shield | 120 kg | $90M | -40 W | Crew protection |
| Fuel Tank | variable | variable | — | Delta-V budget |
| Engine (Chemical) | fixed | fixed | — | Thrust |

Live meters react on every drag: mass, cost, power, delta-V. Center-of-gravity warnings appear when parts are off-balance. Volume conflicts flash when the fairing is overfilled.

You learn that mass, power, budget, and volume are all connected. Adding one thing means removing another.

### Phase 3 — Aim (Launch Angle GUI)

The signature feature. A launch control panel with physical sliders.

- Launch Angle (0°–90°)
- Burn Duration (minutes)
- Staging Altitude (km)
- Propellant Load (%)

**Real-time feedback:**
- Trajectory preview redraws as sliders move
- Predicted outcome panel updates live (escape velocity, fuel remaining, intercept status, flight time, margin)

**The math under the hood:**

```
Tsiolkovsky Rocket Equation:
  delta-v = v_exhaust * ln(m_total / m_dry)

Hohmann Transfer:
  a_transfer = (r_earth + r_mars) / 2
  t_flight   = pi * sqrt(a^3 / mu_sun)
  delta-v_1  = sqrt(mu_sun/r_earth) * (sqrt(2*r_mars/(r_earth+r_mars)) - 1)

Escape Velocity:
  v_escape   = sqrt(2*mu_earth / r)
```

Simplified for browser performance, but mathematically correct.

You learn that launch angle matters, escape velocity is real, fuel is finite, and margins are tight.

### Phase 4 — Fly (Operations Game)

Real-time mission map with time controls (1x to 64x).

**You respond to real events:**
- Asteroid alerts (NeoWs data)
- Solar storms (NOAA space weather)
- Comms blackouts (DSN scheduling)
- Mars dust storms (MEDA / REMS data)

**You interact with the spacecraft:**
- Clean dust off solar panels
- Realign the comms dish
- Run diagnostics on the drill
- Boost radiation shielding (costs power)

**You face the arrival problem:** Enter orbit or land at Mars. This requires fuel you saved — or didn't.

You learn that competing demands are real, triage is a skill, and design decisions come back.

### Phase 5 — Debrief (Credit System)

**Score breakdown (out of 1000):**

| Category | Max Points |
|---|---|
| Objective completion | 250 |
| Resource efficiency | 150 |
| Science return | 150 |
| Spacecraft survival | 150 |
| Budget management | 150 |
| Design elegance | 150 |

**Rating tiers:**

| Score | Rating |
|---|---|
| 900–1000 | EXCEPTIONAL |
| 750–899 | FLIGHT DIRECTOR |
| 600–749 | SYSTEMS OFFICER |
| 400–599 | CADET |
| 0–399 | MISSION FAILED (credits still earned) |

You learn that every decision has measurable consequences and optimization is a skill.

---

## NASA Data Integration

| Feature | API Source | Usage |
|---|---|---|
| Launch windows | Space Devs Launch Library 2 | Populates mission board |
| Planet positions | JPL Horizons | Real ephemeris for trajectory math |
| Asteroid hazards | NASA NeoWs | Real near-Earth objects as events |
| Space weather | NOAA SWPC | Solar storm events |
| Mars weather | InSight / MEDA / REMS | Arrival conditions at Mars |
| Delta-V targets | JPL NHATS | Accessible asteroid database |
| Part specs | JPL datasheets | Real mass/power/cost values |

### Caching Strategy

The game never depends on a live API call during gameplay.

1. On first load, fetch all required data once
2. Cache in localStorage for offline play
3. Bundle fallback JSON in case APIs fail
4. Refresh launch windows once per 24 hours
5. Optional live events for daily challenge missions

The result: always playable, always fast, always real.

---

## Tech Stack

| Layer | Technology | Reason |
|---|---|---|
| Frontend | Vanilla JS + HTML + CSS | Solo-coder friendly, no framework bugs |
| Rendering | HTML Canvas + SVG | Trajectory curves, space map, animations |
| Drag and Drop | Native HTML5 API | Zero dependencies |
| State | Single state object + localStorage | Simple, debuggable |
| Backend | Vercel Serverless Functions | Hide API keys, proxy NASA calls |
| Database | Firebase Realtime DB | Leaderboards, saved designs |
| Build | Vite | Fast dev reload, simple production build |

### Project Structure

```
mission-architect/
|
|-- index.html
|-- css/
|   |-- style.css
|   |-- screens.css
|   |-- animations.css
|
|-- js/
|   |-- main.js              (entry point)
|   |-- engine/
|   |   |-- state.js         (game state)
|   |   |-- orbital.js       (trajectory math)
|   |   |-- credits.js       (scoring)
|   |   |-- events.js        (event system)
|   |-- screens/
|   |   |-- select.js
|   |   |-- build.js
|   |   |-- aim.js
|   |   |-- fly.js
|   |   |-- debrief.js
|   |-- ui/
|   |   |-- meters.js
|   |   |-- canvas.js
|   |   |-- dragdrop.js
|   |-- api/
|       |-- nasa.js          (API wrappers)
|       |-- cache.js         (localStorage caching)
|
|-- data/
|   |-- parts.json           (instrument library)
|   |-- vehicles.json        (launch vehicles)
|   |-- missions/
|   |   |-- mars-jezero.json (mission profile)
|   |-- fallback/
|       |-- launches.json
|       |-- asteroids.json
|       |-- weather.json
|
|-- assets/
    |-- icons/
    |-- sounds/
    |-- fonts/
```

### Performance Targets

- First paint: under 1 second
- API cache warm: under 3 seconds
- Trajectory recalc: under 16 ms (60 FPS slider)
- Mission flight sim: 64x without frame drops
- Total bundle: under 500 KB gzipped

---

## Visual Design

The aesthetic is NASA-punk: dark backgrounds, cyan and amber accents, monospace fonts, blueprint grid lines.

- **Mission Select** — full-screen departure board with glowing accents and animated countdowns
- **Build** — blueprint grid, draggable part cards, wireframe fairing, live meters, center-of-gravity dot
- **Aim** — Earth sphere, Mars target, redrawing trajectory, responsive sliders, particle exhaust on launch
- **Fly** — parallax starfield, glowing spacecraft trail, asteroid warning halos, clickable parts
- **Debrief** — animated credit counter, radial charts, damaged spacecraft render, decision log

Sound is minimal: low ambient hum, distinct alert tones, launch rumble, success chime, failure tone (soft, not harsh).

---

## Educational Value

| Concept | How It's Taught |
|---|---|
| Mass budgets | Drag a part, watch the meter spike |
| Power budgets | Instruments draw watts; sources supply them |
| Delta-V | Slider changes fuel remaining |
| Escape velocity | Trajectory dips back to Earth if too slow |
| Hohmann transfers | Real math behind the trajectory curve |
| Orbital mechanics | Launch angle changes the path in real time |
| Comms delay | Events happen before messages can arrive |
| Triage under pressure | Can't fix everything; must prioritize |
| Engineering trade-offs | Every choice closes a door |
| Real NASA data | Live APIs make the sim feel alive |

**Standards alignment:**
- NGSS MS-ETS1-1 through MS-ETS1-4 (Engineering Design)
- NGSS MS-PS2-4 (Gravitational interactions)
- NGSS MS-PS3-1 (Energy transfer)
- CCSS Mathematical modeling, quantitative reasoning

**Difficulty modes:**
- Cadet — guided, pre-made designs, gentle events (20 min)
- Flight — full design, standard events (45 min)
- Architect — no guardrails, random conditions, cascading failures (60+ min)

---

## Why This Wins

- Maps 1:1 to the challenge brief — every requirement is a playable feature
- Uses real NASA data, not invented and not decorative
- The launch angle GUI is unique — real orbital math on a slider
- It's a game, not a form — drag, aim, fly, earn
- Persistent progression with credits, ranks, unlocks, and leaderboards
- Scales to many worlds — one engine, N missions, JSON-driven
- Solo-coder feasible — vanilla JS, Canvas, Firebase

The pitch: this isn't just a Mars game. It's a platform. Today we're showing Mars. Tomorrow the Moon, Europa, Titan — one JSON file each.

---

## Development Roadmap

### Week 1 — Foundation
- [ ] HTML/CSS/JS skeleton
- [ ] Drag-and-drop system
- [ ] Part library (8 parts)
- [ ] Live mass/cost/power meters
- [ ] Save and load design to localStorage

### Week 2 — Launch GUI
- [ ] Trajectory preview canvas
- [ ] Launch angle slider
- [ ] Real math: Tsiolkovsky + Hohmann transfer
- [ ] Predicted outcome panel
- [ ] Launch sequence animation

### Week 3 — Flight Engine
- [ ] Solar system map canvas
- [ ] Spacecraft position from trajectory
- [ ] Time controls (1x–64x)
- [ ] Resource drain system
- [ ] First 5 events

### Week 4 — Flight Depth
- [ ] 15 more events
- [ ] Clickable spacecraft parts
- [ ] Power rerouting (drag cables)
- [ ] Instrument management
- [ ] Arrival burn / orbit insertion

### Week 5 — Debrief and Credits
- [ ] Credit scoring system
- [ ] Mission report screen
- [ ] Decision log
- [ ] Codex entries
- [ ] Firebase leaderboard
- [ ] Milestone: v1.0 submittable

### Week 6 — NASA Data Integration
- [ ] Space Devs API for launch windows
- [ ] JPL Horizons for planet positions
- [ ] NeoWs for asteroids
- [ ] Caching layer
- [ ] Fallback data

### Week 7 — Polish and Submit
- [ ] Art pass on every screen
- [ ] Sound effects
- [ ] Playtest with real users
- [ ] Demo video
- [ ] Submit on Nov 10

---

## Getting Started

### Prerequisites

- Node.js (v18 or higher)
- A modern browser (Chrome, Firefox, Safari, Edge)
- Free API keys:
  - NASA API key (NeoWs, Horizons)
  - Space Devs API key
  - Firebase project (for leaderboards)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/mission-architect.git
cd mission-architect

# Install dependencies
npm install

# Add your API keys
cp .env.example .env
# then edit .env with your keys

# Start the dev server
npm run dev
```

Open `http://localhost:5173` in your browser.

### Build for production

```bash
npm run build
npm run preview
```

### Environment Variables

```env
VITE_NASA_API_KEY=your_nasa_key_here
VITE_SPACEDEVS_API_KEY=your_spacedevs_key_here
VITE_FIREBASE_API_KEY=your_firebase_key_here
VITE_FIREBASE_DB_URL=your_firebase_url_here
```

---

## Testing

- Manual playtest with 3–4 friends per week
- Rocket math validated against NASA published values
- API fallback tested by disabling network
- Performance measured with Chrome DevTools, target 60 FPS on slider drags
- Cross-browser checked on Chrome, Firefox, Safari

---

## Stretch Goals

Post-submission features, not in scope for Nov 10.

- Multiplayer mode — 4 players as Science Lead, Engineer, PM, Flight Director
- Additional destinations — Moon, Europa, Titan as JSON data files
- Community missions — players author their own mission JSONs
- Real-time daily challenge — uses today's actual Mars weather
- Mobile companion app — watch your mission fly while away
- Historical reenactments — replay Apollo, Voyager, Perseverance
- AI mission advisor — suggests design improvements

---

## Contributing

This is currently a solo submission for the 2026 NASA Space Apps Challenge. After the event, contributions will be welcome.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

Distributed under the MIT License. See `LICENSE` for more information.

---

## Acknowledgments

- NASA Space Apps Challenge, for the challenge brief
- NASA JPL, for Horizons, NeoWs, NHATS datasets
- The Space Devs, for the Launch Library 2 API
- NOAA SWPC, for space weather data
- NASA, JPL, and MIT, for open-access orbital mechanics references

---

## Appendix — Glossary

- Delta-V — Change in velocity. The currency of spaceflight.
- RTG — Radioisotope Thermoelectric Generator. Nuclear power source.
- Hohmann Transfer — The most fuel-efficient orbit-to-orbit transfer.
- Escape Velocity — Speed needed to leave a body's gravity permanently.
- Optical Depth — Measure of atmospheric dust blocking sunlight.
- NeoWs — NASA's Near Earth Object Web Service.
- NHATS — Near Earth Object Human Space Flight Accessible Targets Study.
- MEDA — Mars Environmental Dynamics Analyzer (on Perseverance).
- REMS — Rover Environmental Monitoring Station (on Curiosity).

---

## Contact

**Project Lead:** Savindu
**Event:** 2026 NASA Space Apps Challenge
**Submission Date:** November 10, 2026

---

<div align="center">

*Mission Architect — Version 1.0 — Design Document*

</div>
