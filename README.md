# MISSION ARCHITECT

### Design it. Aim it. Fly it. Earn it.

**A browser-based space mission design, launch, and operations simulator powered by real NASA data.**

![NASA Space Apps](https://img.shields.io/badge/NASA%20Space%20Apps-2026-0B3D91?style=for-the-badge&logo=nasa&logoColor=white)
![Status](https://img.shields.io/badge/status-in%20development-yellow?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)
![Made with JavaScript](https://img.shields.io/badge/made%20with-JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

---

## Overview

Mission Architect is a browser game where you run missions to real planets in the solar system. You pick a destination, choose a rocket family, then fill a 15-slot two-stage vehicle with real parts — engines, tanks, avionics, power systems, payloads — inside a fully rotatable 3D assembly view. Every part carries a description, a real-world analogue, and a codex entry. When you launch, your vehicle behaves exactly as your design predicts: a missing avionics bay means no steering, a missing interstage means no stage separation, a bad thrust-to-weight ratio means the rocket never leaves the pad. On the way to your target, real-time NASA space weather and randomised hazards test your design's weaknesses. The debrief names the exact decision that caused the outcome. XP is earned by succeeding with a lean budget; it is lost heavily by failing early with a broken build. Every description in the game is a teaching moment, and every failure is something you could have seen coming.

| Field | Detail |
|---|---|
| Platform | Browser (HTML/CSS/JS), no install |
| Genre | Mission design + launch + operations simulator |
| View | 3D rocket builder, 2D flight map |
| Session length | 30 to 60 minutes per mission |
| Audience | Students, space fans, STEM classrooms |
| Difficulty tiers | Cadet / Flight / Architect |
| Worlds | 10 destinations, all data-driven |
| Monetization | None |

---

## The Player Flow

```
LANDING PAGE
    |
    v
SIGN UP / GUEST
    |
    v
INTRO SEQUENCE          (once per account, skippable after 5s)
    |
    v
MAIN HUB                (rank, XP, unlocked planets, saved rockets)
    |
    v
PLANET SELECT           (10 planets, locked by XP)
    |
    v
MISSION BRIEF           (objective, budget, difficulty)
    |
    v
ROCKET SELECT           (family template)
    |
    v
ROCKET BUILDER          (15-slot 3D assembly, live validation, visible flex)
    |
    v
DESIGN REVIEW           (engineer verdict: Go / Go-with-concerns / No-Go)
    |
    v
TRAJECTORY PLANNER      (launch window, hazards overlay, delta-V check)
    |
    v
LAUNCH DAY              (Go/No-Go poll, ignition, ascent)
    |
    v
FLIGHT                  (sol-by-sol, event cards, resource management)
    |
    v
ARRIVAL                 (orbit insertion or landing)
    |
    v
DEBRIEF                 (outcome, decision trace, cause of failure, XP)
    |
    v
back to MAIN HUB
```

Eleven screens. Each is a distinct state. The player moves forward or backward, never sideways.

---

## Account and Intro

### Account

Firebase Auth with email, Google, or guest mode. Per-user data at `users/{uid}` as a single JSON blob containing:

- Callsign
- Total XP
- Rank
- Unlocked planets
- Mission history with scores
- Best run per planet
- Saved rocket designs
- Intro-seen flag

### Intro sequence

Six panels, roughly 10 seconds each, skippable after 5 seconds. Plays once per account.

1. **Black screen, radio static.** "In 2041, humanity sent the first crewed mission to Mars. It never came back."
2. **A dark mission control room.** "The agency that built it was shut down within a year. The records were sealed."
3. **A single bright star on a starfield.** "Last month, a university telescope picked up a signal from low Mars orbit. Repeating. Old encryption."
4. **A small team in a hangar.** "Nine nations, eleven universities, one goal. Build a new agency from the ground up."
5. **A blank nameplate.** "You are the mission architect."
6. **A map of the solar system, most planets greyed out.** "One planet at a time. Earn your way out."

Then the main hub appears.

---

## Main Hub

The home screen. Shows:

- Callsign and current rank
- XP bar with progress to next rank
- Unlocked planets (clickable cards)
- Recent missions (last 5 runs with outcome and score)
- **Saved Rockets** tab (see Saved Rocket Designs section)
- **Codex** tab
- **New Mission** button

---

## Planet Select

A grid of ten cards, one per planet, sorted by tier.

| Planet | Tier | Distance from Earth | Base budget | Base XP | Primary hazard |
|---|---|---|---|---|---|
| Moon | 1 | 0.003 AU | $80M | 100 | Micrometeoroids |
| Mars | 2 | 0.5–2.5 AU | $180M | 250 | Dust storms |
| Venus | 2 | 0.3–1.7 AU | $170M | 250 | Heat, pressure |
| Mercury | 3 | 0.6–1.4 AU | $260M | 400 | Solar radiation, heat |
| Ceres | 3 | 1.8–3.8 AU | $340M | 400 | Micrometeoroids |
| Europa | 4 | 4.2–6.2 AU | $580M | 600 | Jupiter radiation belts |
| Titan | 5 | 8.5–10.5 AU | $760M | 800 | Extreme cold, low solar |
| Uranus | 6 | 17–21 AU | $1.2B | 1000 | Long comms delay |
| Triton | 6 | 28–32 AU | $1.4B | 1000 | Extreme cold |
| Pluto | 7 | 30–49 AU | $1.9B | 1200 | Low solar, long delay |

Rank thresholds:

| Rank | XP | Unlocks |
|---|---|---|
| Cadet | 0 | Moon |
| Systems Officer | 500 | Mars, Venus |
| Flight Director | 1,500 | Mercury, Ceres |
| Mission Architect | 4,000 | Europa |
| Chief Architect | 8,000 | Titan |
| Director of Operations | 15,000 | Uranus, Triton |
| Administrator | 25,000 | Pluto |

---

## Mission Brief

Each planet has one mission type. The brief shows:

- Planet name and description
- Objective (one sentence)
- Three difficulty options: Cadet (0.5x XP), Flight (1.0x), Architect (1.5x)
- Base budget and base XP for the chosen difficulty
- Primary hazard for this planet, with a one-line description
- Recommended rocket family
- **Begin Mission** button

Mission objectives by planet:

| Planet | Type | Objective |
|---|---|---|
| Moon | Flyby | Pass within 100 km and return 20 images |
| Mars | Orbiter | Enter orbit and map the surface for 30 sols |
| Venus | Atmospheric probe | Survive 30 minutes in the atmosphere |
| Mercury | Orbiter | Enter orbit and map the surface |
| Ceres | Lander | Land and analyze soil samples |
| Europa | Flyby | Pass within 500 km and scan the ice shell |
| Titan | Lander | Land and measure the atmosphere |
| Uranus | Flyby | Pass within 10,000 km and return atmospheric data |
| Triton | Flyby | Pass within 1,000 km and return surface imagery |
| Pluto | Flyby | Pass within 2,000 km and return all science data |

---

## Rocket Select

Before the builder opens, the player chooses a rocket family.

| Family | Stages | Active slots | Payload to LEO | Base cost | Best for |
|---|---|---|---|---|---|
| Sounding Rocket | 1 | 6 | 50 kg | $5M | Learning the interface, lunar flybys |
| Small Orbital | 2 | 10 | 300 kg | $15M | Lunar missions, small probes |
| Medium Orbital | 2 | 15 | 8,000 kg | $65M | Mars and Venus orbiters, small landers |
| Heavy Orbital | 2 + boosters | 15 + 4 | 26,000 kg | $140M | Mars landers, outer planet orbiters |
| Super-Heavy | 2 + boosters | 15 + 6 | 60,000+ kg | $600M | Europa, Titan, Uranus, Triton, Pluto |
| Custom | player-defined | 15 | player-defined | $0 + parts | Experienced players |

Each family card shows:

- The family name
- A 3D preview of the template's empty shape
- A one-line description
- Payload to LEO
- Base cost
- Recommended for tag
- Select button

The chosen family is shown at the top of the build screen. The player can return to Rocket Select at any point before launch.

If the player has saved rocket designs, this screen also shows a **Load Saved Design** section.

---

## Rocket Builder: 15 Slots in 3D

### The 3D scene

Built with Three.js and OrbitControls. The rocket sits at origin with a subtle grid floor and a starfield background.

Controls:

- Left-drag: rotate around the rocket
- Scroll: zoom in and out
- Right-drag: pan
- Click a part: select it

### How parts are rendered

Every part is a procedurally generated 3D mesh — cylinder, cone, frustum, box, torus — scaled to its real dimensions in metres. Materials use PBR (physically based rendering) with metalness, roughness, and clearcoat so aluminium looks like aluminium and ablative heat shields look chalky.

The rocket is a `THREE.Group`. Adding a part adds a child mesh at the correct Y-offset. Rotating the group rotates the rocket.

Upgrade path: the loader is designed so a GLB model can be dropped in per part-id and replace the primitive. The game ships with zero external asset dependencies and upgrades to full 3D models when a modeller is available.

### Structural flex

The rocket visibly bends and sways as the design changes. This is not a cosmetic animation — it is a physical readout of the vehicle.

Each part has a stiffness value. The builder computes a simple beam-deflection model every time a part is added:

```
deflection = (sum of point loads above this point) * (height above base)^2
           / (2 * flexural_rigidity * cross_section)
```

For the player this means: a tall rocket with heavy parts near the top visibly bends more than a short rocket with parts low down. A stack with a light upper stage and a heavy lower stage stands nearly straight. A stack with the centre of mass high up wobbles in the viewport, and a small flex warning appears in the meters panel.

The visual is subtle at first — a slight sway. As mass distribution gets worse, the sway grows. The player learns by watching the rocket, not by reading a warning. The physical readout is the lesson.

### The 15 slots

| # | Slot | Stage | Mandatory | Description |
|---|---|---|---|---|
| 1 | Engine Cluster | 1 | Yes | Main engines, sea-level optimised |
| 2 | Aft Skirt / Thrust Structure | 1 | Yes | Transfers thrust from engines to tanks |
| 3 | Oxidizer Tank | 1 | Yes | LOX, N2O4, or H2O2 |
| 4 | Fuel Tank | 1 | Yes | RP-1, LH2, or CH4 |
| 5 | Intertank Structure | 1 | Yes | Connects the two tanks |
| 6 | Pressurant System | 1 | Yes | Helium COPVs and regulators |
| 7 | Grid Fins / Aero Surfaces | 1 | Optional | Atmospheric control surfaces |
| 8 | Interstage Adapter | between | Yes | Separates stage 1 from stage 2 |
| 9 | Stage Separation System | between | Yes | Pyrotechnics or hot-staging ring |
| 10 | Upper Stage Engine | 2 | Yes | Vacuum-optimised |
| 11 | Upper Stage Tank | 2 | Yes | High-efficiency propellant |
| 12 | Avionics Bay | 2 | Yes | Flight computer, IMU, star trackers |
| 13 | Power System | 2 | Yes | Solar, RTG, batteries |
| 14 | Payload Bay | 2 | Yes | Instruments, lander, return capsule |
| 15 | Fairing / Nose Cone | top | Yes for atmosphere | Aerodynamic cover, jettisoned at max-Q |

Optional appendages:

- Side boosters (0–4 on Medium, 0–6 on Heavy and Super-Heavy)
- Reaction Control System (RCS) clusters

### The build flow

**Step 1.** The 3D scene loads with an empty wireframe placeholder for every slot. Each placeholder is a translucent outline showing where the part belongs.

**Step 2.** The player clicks a slot. The parts list on the right filters to show only parts that fit that slot and that satisfy the template's size-class limit.

**Step 3.** The player clicks a part in the list. A spec card opens showing:

- Name
- One-line description
- Mass, cost, power draw, and every other stat
- Real-world analogue ("Flown on Falcon 9, 2010 to present")
- Codex link
- Install button

**Step 4.** The part mesh animates into the slot (300 ms slide and settle). The wireframe disappears. Meters update live. The flex visual updates.

**Step 5.** The engineer's bottom bar updates with warnings based on the dependency state.

**Step 6.** Repeat until the design is complete or the player chooses to launch with faults.

### Live meters

Always visible on the left:

| Meter | What it shows |
|---|---|
| Mass | Dry mass, wet mass, structural mass, margin vs template max |
| Cost | Running total vs mission budget |
| Power | Generation vs load at the target world's sunlight |
| Thrust-to-Weight | Whether the vehicle can lift off |
| Delta-V | What the vehicle can do after escaping Earth |
| Center of Mass | Live COM indicator |
| Flex | Visual sway and a numerical deflection value |

### Sample part entry

Every part in `parts.json` follows this shape:

```json
{
  "id": "engine_merlin_1d",
  "name": "Merlin 1D",
  "slot": "engine_cluster",
  "size_class": "M",
  "description": "A sea-level optimised kerolox engine with a pintle injector. Reliable, restartable, and the workhorse of the Falcon 9 first stage.",
  "heritage": "Flown on Falcon 9, 2010 to present",
  "codex": "merlin_engine",
  "dimensions": { "type": "cylinder", "height_m": 2.9, "diameter_m": 0.92 },
  "mass_kg": 470,
  "cost_usd": 800000,
  "power_w": 0,
  "thrust_kN": 845,
  "isp_s": 282,
  "reliability": 0.995,
  "stiffness": 0.85,
  "requires": ["fuel_tank", "oxidizer_tank", "thrust_structure"],
  "supports": ["grid_fins", "booster_mount"],
  "conflicts_with": []
}
```

Every field is used by the engine. `dimensions` drives the 3D mesh. `stiffness` drives the flex. `requires` and `supports` drive the validator. `reliability` drives the launch roll. `heritage`, `description`, and `codex` drive the educational layer.

---

## Validation and Failure

### The requirements graph

Each part declares `requires`, `supports`, and `conflicts_with`. The validator walks the graph and produces a fault list. Faults have four severities:

| Severity | Meaning |
|---|---|
| Info | Optional improvement |
| Caution | Reduces reliability but not fatal |
| Critical | The vehicle cannot complete the mission without this |
| Block | The vehicle cannot launch at all |

Cautions can be overridden with one click. Criticals and Blocks can also be overridden. Every override is logged with a timestamp.

### Failure modes at launch

The launch sequence reads the fault log and determines what happens.

| Fault | Timing | Outcome |
|---|---|---|
| No engine at all | T-0 | Launch aborted. Never ignites. |
| No fuel tank | T-0 | Aborted by ground software. |
| No thrust structure | T+2 s | Engines rip free. Destroyed on the pad. |
| Engine without oxidizer | T+8 s | Oxidizer-starved burn. Thrust at 20%. Crashes at T+90 s. |
| Thrust-to-weight below 1.0 | T-0 | Cannot lift off. Sits on the pad. |
| No avionics | T+22 s | No gimbal control. Range safety destroys it at T+70 s. |
| No interstage | T+160 s | Stage separation fails. Tumbles and burns up. |
| No separation system | T+160 s | Same as above. |
| No fairing (atmospheric launch) | T+45 s | Payload destroyed by aerodynamic loads. |
| Weak structure (no aft skirt) | T+35 s | Max-Q structural failure. Breaks apart. |
| Excessive flex | T+50 s | Vehicle bends beyond structural limit. Breaks apart. |
| Engine too small for wet mass | T-0 | Insufficient thrust. Topples on the pad. |

Each fault has its own animation and its own debrief entry.

### Random faults

Even a fault-free vehicle has a small chance of anomaly. Base reliability:

```
reliability = 0.98
              * product(part.reliability for every part)
              * (1 - 0.15 * number_of_unmitigated_criticals)
              * (1 - 0.05 * number_of_unmitigated_cautions)
              * launch_weather_factor
```

Clean vehicle: 97–99% launch success. Two criticals: 65–75%. Four criticals: under 50%.

---

## Saved Rocket Designs

Players can save and name their rocket designs and reuse them on future missions.

### Saving

After the design review (or at any point in the builder), the player clicks **Save Design**. A small dialog asks for a name. The design is stored at `users/{uid}/rockets/{rocket_id}` as a JSON object containing:

- Design name
- Template family
- Full slot map (part IDs)
- Total mass, cost, delta-V at time of save
- Creation date
- Optional note from the player

### Loading

On the Rocket Select screen, a **Load Saved Design** section shows all saved rockets. Clicking one opens the builder with every part pre-installed.

### Sharing

Saved designs are private by default. A player can toggle **Public** on any design, which adds it to a global community list at `public_rockets/`. Other players can browse and load public designs.

### Why this matters

A player who spends 30 minutes building a good Medium Orbital vehicle for Mars can reuse it for Venus without rebuilding from scratch. This rewards the design effort and encourages experimentation.

---

## Trajectory Planner

A top-down solar system view with the chosen vehicle at Earth. The player adjusts:

- Launch date (window strip along the bottom)
- Transit speed (fast vs cheap slider)
- Gravity assist (optional: Venus, Earth, Jupiter flybys)

Real trajectory math runs live: Hohmann transfers, phase-error corrections, delta-V totals.

### Hazards overlay

The trajectory line is overlaid with hazard markers from three sources.

**Real-time NASA data:**

- NASA DONKI for solar flares, CMEs, and SEP events
- NASA NeoWs for near-Earth asteroid approaches
- CCMC ISWA for continuous space weather

**Randomised hazards from the planet profile:**

- Dust storms, micrometeoroids, thermal stress, radiation belt passages, comms blackouts

**Design-triggered hazards:**

- No radiation shielding: solar flares are 2x more likely to cause damage
- Solar panels without dust protection: dust storms do 3x damage
- No backup comms: blackouts last 2x longer

The player sees a hazard forecast on the trajectory line. Known hazards get icons. Unknown hazards show as "?" markers.

### Pre-launch checks

Before launch, the screen shows:

- Delta-V required vs available
- Transit time
- Budget remaining
- Hazard list with one-line descriptions of each
- Estimated survivability (percentage based on shielding vs hazards)

Launch is disabled if delta-V required exceeds available.

---

## Launch Day

A short sequence with a Go/No-Go poll.

| Station | Report |
|---|---|
| Weather | Green / Yellow / Red |
| Range | Green / Yellow / Red |
| Vehicle | Green / Yellow / Red (based on reliability) |
| Spacecraft | Green / Yellow / Red (based on faults) |
| Staff | Green / Yellow / Red |

The player can hold for another day (costs budget, may close the window) or launch through a Yellow/Red.

Then the ignition sequence plays out based on the fault log. Either the vehicle climbs, or one of the failure modes triggers.

---

## Flight

Sol-by-sol flight with a live map, resource bars, and event cards.

### Resources

Three bars, each starting at 100:

- Power: drains constantly, drops fast on events
- Data: grows when payload is active, drops on sensor glitches
- Hull: stays at 100 unless damaged

If Power or Hull hits zero, the mission fails immediately.

### Events

Every 20–40 sols, an event fires. The sim pauses. The event card shows what is happening and 2–4 response options. Options are filtered by the vehicle's design: a rocket without radiation shielding never sees the "route power to shielding" option because there is no shielding.

| Event | Trigger | Responses |
|---|---|---|
| Solar flare | DONKI data or random | Shield (if installed), safe mode, ride it out |
| Dust storm | Near dusty planet | Clean panels, ration power, ignore |
| Micrometeoroid | Random | Repair, patch, ignore |
| Comms blackout | Behind Sun | Wait, switch band, boost power |
| Sensor glitch | Random | Diagnose, skip, recalibrate |
| Course drift | Cumulative navigation error | Correct (costs fuel), accept |

Every event card has a one-line description of the physics behind it. The player reads it, chooses, and learns.

### Arrival

When the vehicle reaches the target, the mission resolves based on resources remaining, objective completion, and the success of orbit insertion, landing, or flyby.

---

## Debrief

Four sections.

### Section 1: Outcome

Clear success or failure. Named cause. Short narrative paragraph.

### Section 2: Decision trace

A timeline of the mission with every key decision marked. For each decision:

- What the player chose
- What the alternative was
- What the outcome was

### Section 3: The cause of failure (if failed)

The debrief names the exact decision that caused the outcome.

Example:

> **FAILURE: LAUNCH VEHICLE DESTROYED AT T+22 SECONDS**
>
> The vehicle had no avionics bay. It could not gimbal the engine or correct for atmospheric drift. Range safety destroyed it.
>
> **The decision that caused this:** At build time, you clicked "Launch anyway" on a rocket with a Critical avionics warning.
>
> **The part you did not install:** An avionics bay. The cheapest option is the Apollo-class guidance unit at $8M, 8 kg. Its codex entry explains what a flight computer does.

### Section 4: XP

XP change, new total, rank progress.

No coaching suggestions. The player reads the decision trace, reads the part descriptions they skipped, and figures out the pattern themselves. Every part in the game carries a description that explains its purpose. Every hazard carries a description. Every failure mode carries an explanation. The teaching is in the data, not in a hand-holding screen.

If the player wants more detail, they can click any part name in the debrief to open its codex entry. That is the discovery loop.

---

## XP System

### On success

```
xp_gain = base_xp
        * difficulty_multiplier
        * (1.0 - 0.35 * budget_used_ratio)
```

`budget_used_ratio` is `actual_cost / base_budget`. Spend 40% → keep 86% of XP. Spend 95% → keep 67%.

| Scenario | XP (Flight-tier Mars) |
|---|---|
| Success, 40% budget | 215 |
| Success, 60% budget | 189 |
| Success, 80% budget | 167 |
| Success, 95% budget | 156 |

### On failure

```
fail_progress = 0.0 (pad) to 1.0 (arrived)

xp_loss = base_xp
        * difficulty_multiplier
        * (1.25 - fail_progress)
```

| Failure point | Progress | XP lost (Flight-tier Mars) |
|---|---|---|
| Pad explosion | 0.0 | -312 |
| Ascent failure | 0.15 | -275 |
| Cruise failure | 0.50 | -187 |
| Arrival failure | 0.85 | -100 |
| Orbit insertion failed | 0.95 | -75 |

XP never drops below zero.

---

## Codex

Every part, hazard, planet, and physics concept has a codex entry. Clicking any underlined term in the game opens its entry.

Entries are short (three to five sentences) and explain:

- What the thing is
- Why it exists in real missions
- What happens if you get it wrong

Example entries:

**Avionics Bay.** The electronics that steer the rocket. Contains the flight computer, inertial measurement unit, and star trackers. Without it, the vehicle cannot gimbal its engine or correct for atmospheric drift. Every orbital rocket carries one. The cheapest flight computer that meets mission requirements costs $8M.

**Merlin 1D.** A sea-level optimised kerolox engine. Uses a pintle injector for stable combustion across a wide throttle range. Flown on Falcon 9 since 2010. Reliability is one of the highest in the industry. Not suitable for vacuum operation — a separate vacuum engine is required for the upper stage.

**Micrometeoroid.** A small piece of rock or metal travelling at several kilometres per second. Impacts of objects larger than a millimetre can puncture thin hulls. Missions to the outer solar system carry shielding. The Moon's surface is bombarded constantly, which is why lunar habitats need protective layers.

**Hohmann Transfer.** The most fuel-efficient path between two circular orbits. Used for most interplanetary missions. Requires the two planets to be in the correct relative positions at launch, which is why launch windows exist. Missing a window means waiting months for the next one.

Every codex entry links to related entries, so the player can wander the tree and build their own understanding.

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| 3D rendering | Three.js + OrbitControls | Standard, well-documented, handles the rotatable rocket view |
| Part meshes | Procedural primitives with PBR materials | Zero external assets, upgrades to GLB later |
| Flex simulation | Simple beam-deflection model per part | ~50 lines of math, visible result |
| UI panels | HTML + CSS overlay | Fast to build meters, lists, dialogs |
| State | Single store + event bus | Simple, debuggable |
| Save data | Firebase Realtime DB + Firebase Auth | Known from previous work |
| Build | Vite | Fast reload, simple production build |
| Hosting | Vercel | Free tier, easy deploys |
| Language | Vanilla JavaScript | No framework tax on a solo build |

### File structure

```
mission-architect/
|-- index.html
|-- css/
|   |-- style.css
|   |-- screens.css
|-- js/
|   |-- main.js
|   |-- auth.js
|   |-- engine/
|   |   |-- state.js
|   |   |-- validate.js
|   |   |-- orbital.js
|   |   |-- hazards.js
|   |   |-- xp.js
|   |   |-- flex.js
|   |-- three/
|   |   |-- scene.js
|   |   |-- parts3d.js
|   |   |-- rocket.js
|   |   |-- flexVisual.js
|   |-- screens/
|   |   |-- hub.js
|   |   |-- intro.js
|   |   |-- planets.js
|   |   |-- brief.js
|   |   |-- rocketSelect.js
|   |   |-- builder.js
|   |   |-- review.js
|   |   |-- trajectory.js
|   |   |-- launch.js
|   |   |-- flight.js
|   |   |-- debrief.js
|   |-- api/
|       |-- nasa.js
|       |-- firebase.js
|-- data/
    |-- core/
    |   |-- bodies.json
    |   |-- parts.json
    |   |-- templates.json
    |   |-- hazards.json
    |-- codex/
    |   |-- entries.json
    |-- missions/
        |-- moon_flyby.json
        |-- mars_orbiter.json
        |-- ...
```

---

## Build Order: 7 Weeks

### Week 1: Data foundation

- `bodies.json`, `parts.json` (40+ parts), `templates.json`, `hazards.json`, `codex.json`
- `validate.js` with the requirements graph (pure functions)
- `flex.js` with the beam-deflection math
- Unit tests

### Week 2: 3D builder

- Three.js scene with OrbitControls
- Slot placeholders as wireframes
- Click slot → parts list → install → mesh appears
- Live meters and flex visual

### Week 3: Validation and launch

- Engineer warnings and override logging
- Failure-mode animations
- Launch day sequence with Go/No-Go

### Week 4: Trajectory and flight

- Trajectory planner with hazard overlay
- Live NASA API integration (DONKI, NeoWs)
- Flight screen with event cards

### Week 5: Debrief, XP, saved rockets

- Decision trace
- Failure-cause explanation
- XP formulas
- Firebase auth and save
- Saved rocket designs with public sharing

### Week 6: Intro, polish, playtest

- Six-panel intro
- Codex
- Art pass, sound
- Playtest with 4 friends
- Cut what does not work

### Week 7: Submit

- Demo video
- Write-up
- Submit

**MVP:** Moon and Mars playable end to end, Flight difficulty only, 6 hazard types, working XP, working flex, working saved rockets.

**Cut list if running short:**

1. Intro sequence (replace with a static panel)
2. Sound
3. Difficulty tiers other than Flight
4. Live NASA data (fall back to bundled snapshots)
5. Planets beyond Mars (ship as locked cards)
6. Public rocket sharing (keep private save only)

---

## What Ships at Submission

A browser game where a player can:

1. Sign up, watch a 60-second intro, land on a hub
2. Pick Moon or Mars
3. Choose a rocket family
4. Build a 15-slot two-stage vehicle in a rotatable 3D view, with visible flex
5. Watch the vehicle respond to every design choice in real time
6. Launch with faults if they choose, and see exactly why it failed
7. Fly the mission with real-time hazards
8. Arrive or fail, with a debrief that names the cause
9. Earn or lose XP, climb a rank ladder
10. Save the design and reuse it

Every part has a description. Every hazard has a description. Every failure mode has an explanation. Nothing is hidden. Nothing is auto-explained. The player discovers by reading and by failing, and the game respects them enough to let them figure it out.

---

## One-Line Pitch

> Mission Architect is a browser game where you assemble a real two-stage rocket in 3D, launch it with every part's physics enforced, fly it through real space weather, and learn by reading and by failing. Nothing is hidden. Everything is yours.

---

## Contact

**Project Lead:** Dreamxhava
**Project Teammates:** @doppelganger , @y0han.sv, @Arizu_The_Aura
**Event:** 2026 NASA Space Apps Challenge, Space Mission Design Game
**Submission Date:** November 10, 2026

---

*Mission Architect, Version 5.0, Design Document*
