<div align="center">

# MISSION ARCHITECT: FRONTIER

### Build the base. Pick the world. Design the mission. Run it.

**A 2D browser game where you grow a space agency from a broken launch pad to the edge of the solar system, one world at a time.**

![NASA Space Apps](https://img.shields.io/badge/NASA%20Space%20Apps-2026-0B3D91?style=for-the-badge&logo=nasa&logoColor=white)
![Status](https://img.shields.io/badge/status-in%20development-yellow?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)
![Made with JavaScript](https://img.shields.io/badge/made%20with-JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

[Overview](#overview) · [Challenge Map](#the-challenge-and-how-each-requirement-is-played) · [Intro](#intro) · [Story](#story) · [Space Center](#the-space-center-base-building) · [Worlds](#the-solar-system-map-pick-a-world) · [Mission Flow](#mission-flow) · [Data Architecture](#data-driven-architecture-one-engine-every-planet) · [Roadmap](#development-roadmap)

</div>

---

## Overview

Mission Architect: Frontier is a 2D browser game with two layers that feed each other.

The first layer is a base builder in the style of Clash of Clans. You start with a cracked launch pad on a small plot of land and place buildings on a grid: a Mission Control room, an Assembly Hall, a Fuel Depot, a Tracking Station, a Test Facility. Buildings produce resources. Resources pay for missions.

The second layer is the mission itself. You open the Solar System map, pick a world, and run a complete mission to it: negotiate the goals, build the spacecraft part by part, choose a launch date, launch, fly the cruise, land or enter orbit, run daily operations, and face a debrief that traces every result back to a decision you made.

When a mission succeeds you unlock a plot on that world and build an outpost there, which sends resources home and pushes your reach further out. Moon first, then Mars, then everything else.

| Field | Detail |
|---|---|
| Platform | Browser (HTML/CSS/JS), no install |
| Genre | Base builder + mission design simulator |
| View | 2D top-down, flat vector art |
| Session length | 10 to 20 minutes per mission, 45 to 60 minutes per chapter |
| Audience | Students (middle school through early college), space fans, STEM classrooms |
| Difficulty tiers | Cadet / Flight / Architect |
| Worlds | 10 destination systems, all driven by one dataset |
| Monetization | None. No timers to skip, no premium currency |

---

## What Changed From Version 1

| Problem in v1 | Fix in Frontier |
|---|---|
| The middle of the game was a slider and a wait for a result | Every stage now has a task with a skill or a puzzle in it: packing parts, choosing a window, allocating link time, diagnosing faults, scheduling a day of operations |
| It felt like a form, not a game | The home screen is a living base you build, upgrade, and rearrange. Missions are what the base exists to serve |
| One Mars mission, hard to expand | One engine, one dataset. Every planet is a row of data, so ten worlds ship at once |
| Choices did not carry forward | Skipped tests become hidden faults. Overridden warnings show up in the debrief. Outposts change what you can afford next |
| Launch angle was the signature feature | Replaced by launch-window selection driven by real orbital geometry, which is how real mission design works |
| Resources were only numbers on a meter | Resources are earned by buildings you placed, and spent on things you can see |

---

## The Challenge and How Each Requirement Is Played

The brief asks for a game where participants "design, manage, and simulate a complete space mission while making engineering decisions, managing limited resources, and evaluating how each choice shapes the success of their mission."

Every requirement below is a system the player touches, not a text box.

| Challenge requirement | Playable system | Where it lives |
|---|---|---|
| Mission objectives | Charter board: pick Threshold goals (must succeed) and Baseline goals (nice to have) from the target world's science list | Mission Flow, Stage 1 |
| Spacecraft design | Drag parts into bays on a cutaway spacecraft, with shapes that must fit | Spacecraft Builder |
| Scientific instruments | 12+ instruments with mass, power, data volume, and science value, gated by research | Parts library, Research tree |
| Launch vehicles | 4 vehicle classes with payload limits and reliability; payload to departure energy solved with the rocket equation | Vehicles, Stage 2 and 3 |
| Budgets | Funds earned by the base and spent on parts, tests, launches, and operations; hard cap per mission | Space Center, Charter |
| Power | Source and load meters that use the target world's actual sunlight; cable routing layer; RTG vs solar decisions | Builder power layer, Daily Planner |
| Mass | Bay limits, launcher capacity, center-of-mass offset, dry vs wet mass driving delta-v | Builder meters |
| Communications | Antenna choices, data rate that falls with distance, light delay, limited Deep Space Network time | Builder, Cruise, Tracking Station |
| Orbital constraints | Launch windows from real synodic periods, transfer time vs delta-v, gravity assists, orbit insertion | Aim stage, Cruise |
| Concept to operation | Charter, Build, Aim, Launch and Cruise, Arrival and Operations, Debrief, in one continuous flow | Mission Flow |
| Engineering decisions | Every part, slider, and test has a cost that closes another option | Everywhere |
| Limited resources | Funds, materials, propellant, power, data, link time, calendar time | Everywhere |
| How each choice shapes success | Debrief decision trace: each score item is linked to the choice that caused it | Debrief |

---

## Intro

### Opening sequence (about 60 seconds, skippable)

Six panels, flat illustrations, light text, ambient sound. Each panel holds for a few seconds.

**Panel 1 (black screen, radio static)**

> Nine years ago, the Kepler Range launch complex sent its last spacecraft to the Moon.
> Tern-1 landed near the south pole, sent back four minutes of data, and went silent.

**Panel 2 (the pad, overgrown, gates chained)**

> The program that built it lost its funding within the year.
> The investigators never found a cause. The gates were chained. The fuel tanks were sold for scrap.

**Panel 3 (a small university dish turning at night)**

> Last month, a tracking dish at a university in the south picked up a faint signal from the lunar surface.
> A transmitter, waking up at each lunar sunrise, repeating one short packet.
> Nobody could read more than the header.

**Panel 4 (a table of flags from nine countries)**

> Nine small nations and eleven universities pooled their money to reopen the site.
> It is not enough to build a real space agency. It is enough to build a small one, if it is run well.
> They call themselves the Meridian Compact.

**Panel 5 (a hand-drawn name badge: PROGRAM DIRECTOR)**

> They hired you.

**Panel 6 (the cracked pad, sunrise)**

> You have a rusted launch pad, a hangar with a leaking roof, a crate of donated parts, four staff, and one rule from the board:
> "Finish what you start. Then earn the next one."

### The first 60 seconds of play

The opening ends on the empty base. There is no menu. The Flight Director speaks in a dialogue box and the game teaches by doing:

1. Tomas Reyes: "The board gave us enough for three buildings. Start with Mission Control." The player drags the building onto the grid.
2. Collect the first Funds bubble that floats above the building (tap to collect).
3. Place the Assembly Hall and the Launch Pad.
4. The world map lights up with a single glowing target: the Moon.
5. Tomas: "First job is simple. Fly past it and take a picture. You will learn more from the first launch than from any briefing."

The player is inside the first mission within two minutes.

---

## Story

### Setting

Near future. Launch costs have fallen but not enough. The Meridian Compact is a coalition too small to compete with the big agencies, so it works differently: small missions, careful margins, and a plan to build a chain of relays and outposts outward from the Moon, each world funding the next.

### Cast

Each character is the voice of one competing demand from the brief, so the trade-offs arrive as conversations rather than menus.

| Character | Role | Wants | Shows up in |
|---|---|---|---|
| Tomas Reyes | Flight Director, mentor, former Tern-1 operator | Discipline, margins, "never fly what you cannot talk to" | Tutorial, Launch Day, Cruise |
| Dr. Amara Okafor | Chief Engineer | Mass reserve, power reserve, tested hardware | Builder warnings, Design Review |
| Dr. Lucas Ferreira | Lead Scientist | More instruments, more data, more ambitious targets | Charter, Builder, Daily Planner |
| Ines Marchetti | Compact Budget Chair | Lower cost, on-time delivery, fewer surprises | Charter, Debrief, audits |
| Cole Draper | CEO of Vanta Orbital, a private rival | To win contracts with cheaper, riskier missions | Contract board, news ticker |

### The through-line: the Tern-1 log

Chapter 1 is a mystery with a real answer. The player recovers the Tern-1 lander's decision log, which is stored in the lander's memory and readable only up close.

The reveal, at the end of Chapter 1: Tern-1 landed in a shadowed crater near the pole and had four minutes of battery. The design review had flagged the battery as too small. The Lead Scientist wanted to keep the extra instrument that used the mass. The Budget Chair refused the extra funds. Every stakeholder made a reasonable decision. Nobody owned the risk.

The last line of the log: *"If you are reading this, write down why you decided, not only what."*

This becomes the game's principle. The Debrief decision log is the successor of the Tern-1 log. When the player overrides a Chief Engineer warning, it is written down. If the mission fails later, the debrief shows the line.

### Chapters

The chapter order follows real difficulty: energy cost, environment, and communication delay.

| Ch | Title | World | New constraint taught | Mission types | Story beat |
|---|---|---|---|---|---|
| 1 | First Light | Moon | Mass, budget, rocket equation, launch basics | Flyby, orbiter, lander | Recover the Tern-1 log |
| 2 | Red Window | Mars | Power, dust, EDL, 26-month windows | Relay orbiter, rover | First outpost; Vanta Orbital appears |
| 3 | Hothouse | Venus | Heat, crushing pressure, short survival time | Orbiter, atmospheric probe, lander | Cole Draper undercuts a contract |
| 4 | Scorched Orbit | Mercury | Gravity assists, extreme sunlight, heat | Orbiter | The assist puzzle |
| 5 | The Belt | Ceres | Ion propulsion, microgravity, first fuel from local ice | Orbiter, lander, sample return | Outposts start paying for the next mission |
| 6 | Storm Belt | Jupiter system | Radiation | Orbiter, Europa flyby, Ganymede lander | Shielding vs mass |
| 7 | Ringed Dark | Saturn system | Sunlight too weak for solar, RTG required, long delay | Orbiter, Titan lander, Enceladus plume flythrough | The Titan drone descent |
| 8 | Ice Giants | Uranus, Neptune | Multi-year cruise, autonomy | Flyby probes, Triton flyby | You cannot fix it from Earth |
| 9 | Last Relay | Pluto | Longest delay, minimum power | Flyby, orbiter | Chain complete |

### Anomaly Files

Every failure in the game is modeled on a real one. When something goes wrong, the debrief opens the matching file: what really happened, what the lesson was, and which of your choices caused the same pattern.

| File | Year | What happened | Design lesson |
|---|---|---|---|
| Mars Climate Orbiter | 1999 | Navigation software used pound-force seconds where newton seconds were expected; the craft passed too low at Mars | Interface and unit checks |
| Mars Polar Lander | 1999 | A false touchdown signal from the legs most likely shut the engines off too early | Sensor logic in landing |
| Genesis | 2004 | Deceleration sensors were installed backwards and the parachute never deployed | Verify assembly, test it |
| Beagle 2 | 2003 | Landed, but the solar panels probably did not fully open and blocked the antenna | Deployment mechanisms |
| Schiaparelli | 2016 | A sensor saturated, giving a wrong altitude estimate; the parachute was released early | Sensor margins in descent |
| Philae | 2014 | Anchoring harpoons failed, the lander bounced and settled in shadow | Power and site selection |
| Opportunity | 2018 | A global dust storm starved the solar panels of power and contact was lost | Power margin, dust |
| Apollo 13 | 1970 | An oxygen tank failed; the crew rationed power to get home | Triage under constraints (sandbox scenario) |

### Ending

The Last Relay comes online at Pluto. The map shows every world you reached, connected by a line of links back to the pad you started with. The Compact votes to fund a next phase. The final screen is an empty Charter board with the title "Next mission" and the cursor blinking in the first field.

---

## Core Loops

```
                     +----------------------------------+
                     |          SPACE CENTER            |
                     |   build, upgrade, collect        |
                     +----------+-----------------------+
                                | Funds, Materials,
                                | Propellant, Research
                                v
   +-------------+      +---------------+      +-------------------+
   |  WORLD MAP  | ---> |    MISSION    | ---> |      DEBRIEF      |
   |  pick a     |      | Charter       |      | score, decision   |
   |  planet     |      | Build         |      | trace, Codex,     |
   +-------------+      | Aim           |      | credits           |
         ^              | Launch/Cruise |      +---------+---------+
         |              | Arrive/Ops    |                |
         |              +---------------+                |
         |                                               v
         |              +---------------+      +-------------------+
         +--------------|   OUTPOSTS    | <----|  UNLOCKS: new     |
                        | build on the  |      |  worlds, parts,   |
                        | world you won |      |  buildings        |
                        +---------------+      +-------------------+
```

**Base loop (2 to 5 minutes):** collect, build, upgrade, position buildings for safety and bonuses.
**Mission loop (10 to 20 minutes):** run a mission on one world.
**Expansion loop (per chapter):** an outpost turns a one-time success into a permanent income and reach.

### How time works

The game does not run on real-time build timers. Time is the **Program Calendar**, which advances only when the player acts:

- Pressing End Week advances one week. Buildings finish, production accrues, contracts age.
- Launching and flying a mission advances the calendar by the mission duration, compressed into playable decision points.
- Launch windows, construction, and testing all use calendar time, which is why timing them well matters.

This keeps the Clash of Clans feeling of tapping resources and upgrading buildings without forcing anyone to wait in real time. The only waiting in the game is a choice the player makes.

### Anti-idle rules

1. Every stage has an active task (packing, choosing, allocating, scheduling, diagnosing).
2. Time warp always stops at an event or a decision point.
3. No stage can be finished by pressing a single Go button. Autopilot options exist but cost score.
4. The player cannot joystick the spacecraft. They plan and command it from Earth, which is how operations actually work.
5. Failure is never a hard game over. A failed mission yields a debrief, a lesson, and partial credits.

---

## The Space Center (Base Building)

A 36 by 36 tile grid, top-down, with pan and zoom. Buildings are 2x2 to 4x4 tiles. Each tap on a building's production bubble collects its output.

### Resources

| Resource | Source | Spent on |
|---|---|---|
| Funds ($M) | Funding Office, contract rewards, mission bonuses, outposts | Buildings, parts, tests, launches, operations |
| Materials | Fabrication Shop, outposts | Buildings, spacecraft hardware |
| Propellant (tonnes) | Propellant Plant, outposts on ice-rich worlds | Vehicle and spacecraft fuel loads |
| Research (RP) | Research Lab, Data Center | Tech tree |
| Data (DU) | Missions | Converted to Research and Reputation at the Data Center |
| Reputation | Debrief scores, layout score | Unlocking mission tiers and board funding |
| Base Power (kW) | Solar Farm | Running buildings; deficits slow production |

### Buildings

The MVP column marks what ships in the first submittable build.

| Building | Size | What it does | What upgrades change | Challenge link | MVP |
|---|---|---|---|---|---|
| Mission Control | 4x4 | Center of the base; gates world tiers and how many missions can run at once | Missions in parallel (1 to 3), max tier | Operations | Yes |
| Assembly Hall | 4x3 | Opens the Spacecraft Builder | Max spacecraft mass, bay count, part shapes | Spacecraft design, mass | Yes |
| Launch Pad | 4x4 | Launches vehicles | Max vehicle class, turnaround time | Launch vehicles | Yes |
| Vehicle Integration Building | 3x3 | Stores and prepares vehicles | Unlocks larger vehicle classes | Launch vehicles | No |
| Test Facility | 3x3 | Runs thermal-vacuum, vibration, radiation, and software tests | Test coverage and speed | Engineering decisions, risk | Yes |
| Research Lab | 3x3 | Produces Research; opens the tech tree | Research rate, tree depth | Scientific instruments | Yes |
| Tracking Station | 2x2 | Sets link capacity: DSN hours per week, maximum data rate, maximum distance | Dish size, hours per week | Communications | Yes |
| Solar Farm | 2x2 | Base power | Output per tile | Power | Yes |
| Fuel Depot | 2x2 | Stores propellant | Capacity | Propellant, launch safety | Yes |
| Propellant Plant | 3x2 | Produces propellant | Rate | Propellant | No |
| Fabrication Shop | 3x3 | Produces Materials | Rate | Budget, mass | Yes |
| Data Center | 3x2 | Converts returned data to Research and Reputation | Conversion rate | Data | No |
| Funding Office | 3x3 | Produces Funds and Reputation through public engagement | Rate | Budget | Yes |
| Workshop | 2x2 | Adds a builder (max 4) | Build speed | Resource limits | Yes |
| Warehouse | 2x2 | Raises storage caps | Capacity | Resource limits | No |

### Layout rules (the small puzzle in the base)

Placement matters, which gives the base the "arrange it well" feel.

| Rule | Effect |
|---|---|
| Fuel Depot within 3 tiles of the Launch Pad | Launch failure damages more of the base and raises insurance cost. Keep it away |
| Test Facility adjacent to Assembly Hall | Tests cost 20% less |
| Tracking Station with clear ground within 2 tiles in every direction | Full link capacity. Blocked dishes lose capacity |
| Solar Farm not shaded by 3x3 or larger buildings | Full base power |

A layout score (0 to 100) grants small Reputation rewards. Buildings can be moved freely for a small Materials fee.

### Base events (short, non-punishing)

| Event | Effect | Response |
|---|---|---|
| Storm front | Launch weather is red for a few days | Wait, or launch with a risk penalty |
| Budget audit | The Budget Chair asks for a reserve | Keep 10% of Funds unspent or lose Reputation |
| Equipment failure | A building drops to half output | Pay a repair fee or accept slower output |
| Supplier delay | Material prices spike for a few weeks | Buy now, or wait it out |

---

## The Solar System Map (Pick a World)

This is the screen the concept started from: you pick a planet and move from there.

A flat 2D solar system with planet orbits drawn from real positions. Tapping a world opens a card generated from its data.

### World card

| Field | Example (Mars) |
|---|---|
| Unlock status | Tier 2, requires Mission Control Lv 2 and Moon orbiter success |
| Next launch window | In 41 days (window quality: 92%) |
| Departure delta-v from low Earth orbit | 3.6 km/s |
| Typical transit time | About 259 days for the cheapest transfer |
| One-way light delay | 3 to 22 minutes |
| Sunlight | 43% of Earth |
| Radiation | Tier 2 |
| Landing type | Thin atmosphere: parachute plus rockets |
| Mission types available | Flyby, orbiter, lander, rover, sample return |
| Science targets | 6 |
| Hazards | Dust storms, radiation, cold nights |

Every value is read from data. No card is hand-written.

### Unlock tiers

| Tier | Worlds | Gate |
|---|---|---|
| 1 | Moon | Start |
| 2 | Mars, Venus | Mission Control Lv 2, Chapter 1 complete |
| 3 | Mercury, Ceres | Mission Control Lv 3, 3 successful missions |
| 4 | Jupiter system | Mission Control Lv 4, RTG research |
| 5 | Saturn system | Mission Control Lv 5, Tracking Station Lv 3 |
| 6 | Uranus, Neptune | Mission Control Lv 6, autonomy research |
| 7 | Pluto | Mission Control Lv 7, relay chain to Neptune |

### World data: physical values

Approximate real values, used as the starting constants. The full set is in `data/core/bodies.json`.

| Body | Radius (km) | Surface gravity (m/s2) | Atmosphere | Surface temperature | Sunlight at mean distance (W/m2) |
|---|---|---|---|---|---|
| Moon | 1,737 | 1.62 | None | -170 to 120 C | 1,361 |
| Mercury | 2,440 | 3.70 | None | -180 to 430 C | about 9,100 |
| Venus | 6,052 | 8.87 | CO2, about 92 bar | about 465 C | about 2,600 |
| Mars | 3,390 | 3.71 | CO2, about 0.006 bar | -125 to 20 C typical | about 590 |
| Ceres | 473 | 0.28 | None | about -105 C | about 177 |
| Jupiter (Europa, Ganymede) | 69,911 | 24.8 | Gas giant, no surface | Europa about -170 C | about 50 |
| Saturn (Titan, Enceladus) | 58,232 | 10.4 | Gas giant, no surface | Titan about -179 C | about 15 |
| Uranus | 25,362 | 8.9 | Gas giant, no surface | about -195 C at cloud level | about 3.7 |
| Neptune (Triton) | 24,622 | 11.2 | Gas giant, no surface | about -200 C at cloud level | about 1.5 |
| Pluto | 1,188 | 0.62 | Very thin nitrogen | about -230 C | about 0.9 |

Titan has a dense nitrogen atmosphere (about 1.45 bar at the surface). Europa's surface sits inside one of the harshest radiation environments in the solar system. Both are handled by rules, not hand-coded exceptions (see the data section).

### World data: mission values (computed)

These are computed by the generator from orbital data. They are the classical Hohmann transfer values from a 200 km circular Earth orbit and are the game's baseline. Real missions often fly faster or use gravity assists, so the game lets the player trade delta-v and assists for time.

| Target | Departure delta-v (km/s) | Cheapest transfer time | Launch window spacing | One-way light delay |
|---|---|---|---|---|
| Moon | 3.1 | 3 to 5 days | about monthly | 1.3 seconds |
| Venus | 3.5 | 146 days | 19 months | 2.3 to 14 minutes |
| Mars | 3.6 | 259 days | 26 months | 3 to 22 minutes |
| Mercury | 5.6 | 105 days | 116 days | 5 to 12 minutes |
| Ceres | 4.9 | 1.3 years | 15 months | 15 to 31 minutes |
| Jupiter | 6.3 | 2.7 years | 13 months | 35 to 52 minutes |
| Saturn | 7.3 | 6.1 years | 12.4 months | 67 to 92 minutes |
| Uranus | 8.0 | 16 years | 12.2 months | 2.4 to 2.9 hours |
| Neptune | 8.3 | 30.6 years | 12.1 months | 4.0 to 4.3 hours |
| Pluto | 8.4 | 45.6 years | 12.1 months | 4 to 7 hours |

Cruise time in play is not proportional to real transit time. Cruise is a sequence of decision points (course corrections, link passes, events), so a long transit simply has more calendar time between them. Every cruise, from Moon to Pluto, is designed to take 3 to 8 minutes of play.

---

## Mission Flow

Six stages. Each has a task, a decision that closes other options, and something that can go wrong.

### Stage 1: Charter

**What you do:** Choose a world and a mission type (flyby, orbiter, lander, rover, sample return, outpost module). The Charter board shows objective cards drawn from the world's science targets. Stakeholders attach demands. You sort cards into **Threshold** (must succeed or the mission is a failure) and **Baseline** (nice to have).

**The decision:** Every Threshold card raises the reward and the pressure. The Lead Scientist pushes for more. The Budget Chair sets the cap. The Chief Engineer prices the risk.

**Output:** A scoring rubric for this mission, a budget cap, a target launch window, and a bonus if a contract is attached.

### Stage 2: Build

Three sub-steps: assemble, test, review.

**2a. Assemble (Spacecraft Builder)**

1. Pick a bus (Small, Medium, Large). It fixes the number of bays and the dry mass.
2. Drag parts into bays. Parts have shapes (1x1, 1x2, 2x2, L-shapes) and must fit, like packing a suitcase. Instruments also need an external mount (deck, boom, underside).
3. Switch layers to route and check systems:
   - **Structure:** where parts sit, center of mass
   - **Power:** draw cables from sources to consumers; set priorities when load exceeds supply
   - **Thermal:** heaters and radiators against the target world's temperature range
   - **Data:** storage and link budget
4. Fill propellant tanks. The delta-v meter updates from the rocket equation.
5. Choose a launch vehicle. The vehicle's payload limit is the ceiling.

Live meters react on every drag:

| Meter | What it shows |
|---|---|
| Mass | Dry mass, wet mass, and margin against the vehicle capacity |
| Cost | Running total against the Charter cap |
| Power | Generation against load, computed for the target world's sunlight |
| Delta-v | What the spacecraft can do by itself after launch |
| Data rate | What the antenna delivers at the target world's distance |
| Thermal margin | Coverage of the target's temperature range |
| Radiation tolerance | Part tolerance against the target's radiation tier |
| Center of mass | Off-balance parts push the marker off center |

**Engineer feedback:** the Chief Engineer comments in plain language at three levels: information, caution, and block. Cautions can be **overridden** with one click. Overrides are logged and shown in the debrief.

> "Mass margin is 3%. Most programs keep 20 to 30% at this stage. Override?"

**2b. Test (Test Facility)**

Each design has hidden faults generated from its weaknesses. Tests reveal them so you can fix them before launch.

| Test | Finds | Cost and time |
|---|---|---|
| Thermal-vacuum | Heater, radiator, and insulation faults | Medium funds, 2 weeks |
| Vibration | Loose parts, deployment failures, structural faults | Low funds, 1 week |
| Radiation | Electronics that fail in high-radiation worlds | Medium funds, 2 weeks |
| Software | Timing, unit mismatches, edge cases | Low funds, 1 week |
| Full system | Interaction faults between subsystems | High funds, 4 weeks |

Hidden fault model, used the same way for every subsystem:

```
fault_chance = base_rate
             * environment_severity          (from the world's tags)
             * (1 - margin) ^ k              (from your design margins)
             * (1 - test_coverage)           (from tests you paid for)
```

Untested faults appear during flight as events. Tested faults show up early and can be fixed.

**2c. Design Review**

The Chief Engineer gives a verdict: **Go**, **Go with concerns**, or **No-Go**. You can still launch on a No-Go. The verdict and your override are logged.

### Stage 3: Aim

**What you do:** Choose the launch date and the shape of the transfer on a 2D solar system view.

**The window strip.** A timeline of upcoming launch windows. Bar height is the energy needed on each date. Lower is cheaper, but launch dates are limited by calendar time. Waiting for a better window costs weeks of program time and funds.

**The transfer controls:**

| Control | Effect |
|---|---|
| Launch date | Moves along the window strip; off-optimal dates cost extra delta-v |
| Time of flight | Faster costs more delta-v; the cheapest is the Hohmann time |
| Gravity assist | Optional flybys (Venus, Earth, Jupiter) that trade time and complexity for delta-v |
| Propellant load | More fuel adds delta-v and mass; capacity limits apply |
| Engine | Chemical (high thrust) or ion (very efficient, low thrust, needs power) |

**The trajectory preview:** The Sun, Earth's orbit, the target's orbit, and the transfer arc are drawn using real positions for the chosen date. The arc redraws as controls change (under 16 ms).

**The prediction panel (live):**

- Delta-v required vs available (launcher plus spacecraft)
- Arrival date and transit time
- Capture cost at the target
- Margin after all burns
- Light delay and sunlight at arrival
- Departure quality (how close to the optimal date)

The math is visible with a "Show the math" toggle (rocket equation, Hohmann transfer, phase error).

### Stage 4: Launch and Cruise

**Launch day.**

- **Go/No-Go poll.** Weather, range, vehicle, spacecraft (test results), and staff each report green, yellow, or red with probabilities. Holding for a day costs funds and may close the window. Launching on a yellow is a gamble.
- **Ascent mini-game (45 seconds, optional).** Keep the flight path inside a corridor, time the staging with a key press, and pass through maximum aerodynamic pressure with the throttle low. A clean ascent delivers a precise orbit and saves course-correction fuel. Autopilot is available at a small score penalty.

**Cruise (Mission Control console).** The main layout is three panels:

- **Left:** Solar system map with the craft, path, and a navigation error ellipse that grows over time
- **Center:** Subsystem gauges (power, thermal, comms, data storage, propellant)
- **Right:** Command timeline with uplink times

**The core cruise decisions:**

| Decision | Mechanic |
|---|---|
| Course correction (TCM) | Navigation error grows. Correct early and it is cheap; wait and it costs more delta-v |
| Link time allocation | Each week you have limited Deep Space Network hours (set by the Tracking Station). Split between tracking (shrinks the error ellipse), data return (science), commanding (uplinks), and health checks |
| Power profile | Choose cruise, hibernate, or science mode; each changes the drain |
| Anomaly diagnosis | Telemetry graphs go wrong (a bus voltage dip, a battery heating up, a comms dropout). Choose which tests to run; each costs time and power. A wrong diagnosis makes it worse |
| Opportunity science | Optional targets during cruise, including real near-Earth asteroid passes from NASA data |
| Space weather | A solar flare warning arrives at the speed of light; the particle front arrives later. It is a race between your safing command and the radiation |

**Light-delay commanding.** Two clocks sit at the top: Earth time and craft time. A command takes the one-way light time to arrive, so you are always planning for a future the spacecraft has not reached yet. If a problem starts and the craft has no autonomy, it waits in safe mode for your command. If it has an autonomy package (a part you bought), it handles known faults itself. This is why outer-planet missions require autonomy: at 4 hours of delay you cannot help in time.

### Stage 5: Arrival and Operations

**Orbit insertion.** A short timing task. The capture burn happens while the craft is out of contact or with delayed telemetry, so the burn sequence is loaded in advance. Accuracy depends on navigation error and burn timing. On worlds with an atmosphere you can choose **aerobraking** (needs a heat shield): much cheaper in delta-v, but takes weeks of calendar time and carries risk.

**Landing (lander and rover missions).**

1. **Site selection.** A tile map generated for the world shows slope, rock hazard, and science value. Exciting sites are dangerous. Flat plains are safe and dull.
2. **EDL setup.** Configure the descent timeline before arrival: heat shield jettison, parachute deploy height, radar switch-on, retro-rocket timing. The world's data decides which stages exist (see the EDL rules in the data section).
3. **Monte Carlo ellipse.** A scatter of about 200 predicted landing points shows the odds and the hazard fraction of your site.
4. **The descent.** A 30-second animated descent with telemetry callouts. You cannot intervene. This is the "seven minutes of terror", and it is tense because every choice was made earlier.

**Daily Planner (the operations puzzle).** After landing or orbit insertion, each operating cycle is a scheduling grid.

- The timeline is 24 slots. Sunlight availability follows the world's day and night pattern
- Activity blocks (drive, image, spectrometer run, drill, sample, downlink, heat, charge) are dragged into slots
- Each block has duration, power draw, data volume, and science value
- Constraints: the battery cannot go below zero, storage cannot overflow, thermal windows must be respected, and downlink windows are limited
- **Science only counts when it is sent home.** Data sitting on the craft is worth nothing until the downlink slot moves it.

Over cycles, wear and environment reduce the budget: dust dims solar panels, RTG output decays a few percent per year, wheels and drills wear, radiation accumulates in electronics. When the primary mission length is reached, you may keep operating for **Extended Mission** points until something fails.

### Stage 6: Debrief

Detailed in [Scoring and Debrief](#scoring-and-debrief).

---

## Spacecraft Builder: Parts and Vehicles

Values are tuned for gameplay and based on real orders of magnitude. The full library lives in `parts.json`.

### Sample parts

| Part | Category | Mass (kg) | Power (W) | Cost ($M) | Bays | Notes |
|---|---|---|---|---|---|---|
| Small bus | Structure | 60 | 0 | 15 | 4 bays | Flyby and small probes |
| Medium bus | Structure | 250 | 0 | 40 | 9 bays | Orbiters, small landers |
| Large bus | Structure | 900 | 0 | 110 | 16 bays | Rovers, large orbiters |
| Solar wing (small) | Power | 12 | +400 at 1 AU | 8 | 1 | Output scales with 1 / distance squared; dust-sensitive |
| Solar wing (large) | Power | 40 | +1,500 at 1 AU | 22 | 2 | Same scaling |
| RTG (radioisotope) | Power | 45 | +110 | 150 | 2 | Works anywhere; output decays about 4% per year |
| Battery pack | Power | 10 | storage 1,500 Wh | 6 | 1 | Bridges night and eclipse |
| Low-gain antenna | Comms | 2 | -5 | 2 | 1 | 2 kbps at 1 AU, scales with 1 / distance squared |
| High-gain antenna | Comms | 40 | -100 | 30 | 2 | 1,000 kbps at 1 AU, needs pointing |
| UHF relay radio | Comms | 4 | -20 | 5 | 1 | Fast short-range link to a nearby orbiter |
| Flight computer | Avionics | 8 | -15 | 10 | 1 | Standard |
| Rad-hard computer | Avionics | 12 | -20 | 25 | 1 | Required at high radiation |
| Autonomy package | Avionics | 3 | -5 | 20 | 1 | Levels 1 to 3; handles known faults during delay |
| Insulation blankets | Thermal | 5 | 0 | 3 | 1 | Passive |
| Heater kit | Thermal | 4 | -30 | 4 | 1 | For cold worlds |
| Radiator | Thermal | 8 | 0 | 6 | 1 | For hot worlds |
| Radiation vault | Protection | 25 | 0 | 18 | 2 | Cuts radiation dose to electronics |
| Chemical engine | Propulsion | 40 | 0 | 12 | 2 | Specific impulse 320 s, high thrust |
| Ion thruster | Propulsion | 35 | -2,000 | 45 | 2 | Specific impulse 3,000 s, low thrust, needs solar power |
| Heat shield / aeroshell | EDL | 15% of entry mass | 0 | 20 | outside | Needed for atmospheric entry |
| Parachute | EDL | 25 | 0 | 8 | 1 | Only works in thin or dense atmospheres |
| Landing legs / descent engines | EDL | 60 | 0 | 15 | outside | Powered landing |
| Panoramic camera | Instrument | 3 | -8 | 8 | 1 | Imaging |
| Mass spectrometer | Instrument | 40 | -45 | 60 | 2 | Detects organics, chemistry |
| Laser spectrometer | Instrument | 10 | -20 | 30 | 1 | Remote chemistry |
| Ground-penetrating radar | Instrument | 3 | -10 | 15 | 1 | Subsurface ice |
| Seismometer | Instrument | 10 | -5 | 25 | 1 | Landers only |
| Magnetometer boom | Instrument | 2 | -2 | 6 | 1 | Orbiters and flybys |
| Radiation detector | Instrument | 2 | -3 | 4 | 1 | Cheap science and dose data |
| Weather station | Instrument | 1.5 | -2 | 5 | 1 | Landers and rovers |
| Radar sounder | Instrument | 40 | -60 | 70 | 2 | Icy moons |
| Drill and sample cache | Instrument | 60 | -60 | 90 | 2 | Sample return |

### Launch vehicles

Vehicle classes are modeled on real vehicle types. Payload to departure energy is solved with the rocket equation on the upper stage.

| Vehicle | Class | Payload to low Earth orbit | Launch cost | Reliability |
|---|---|---|---|---|
| Lark | Small | 300 kg | $10M | 94% |
| Harrier | Medium | 8,000 kg | $60M | 97% |
| Condor | Heavy | 22,000 kg | $120M | 97.5% |
| Colossus | Super-heavy | 60,000 kg | $600M | 93% (new vehicle) |

```
delta_v_upper = Isp * g0 * ln((m_dry_stage + m_prop + payload) / (m_dry_stage + payload))
payload_at_departure = payload where delta_v_upper = required departure delta-v
                       (capped at payload to low Earth orbit)
```

### Mission archetypes

Archetypes are generic templates. The world decides which are allowed.

| Archetype | Required parts | Typical objectives |
|---|---|---|
| Flyby | Bus, power, comms, camera | Imaging, fields and particles |
| Orbiter | Above, plus engine and propellant for capture | Mapping, atmosphere, relay |
| Lander | Above, plus EDL parts and landing system | Surface chemistry, seismology, weather |
| Rover | Lander parts, plus mobility, larger bus | Sampling, traverse science |
| Sample return | Lander parts, plus drill, cache, return stage | Returned samples (high value) |
| Outpost module | Cargo bus, landing system | Unlocks an outpost plot |

---

## Outposts

After a successful orbiter or landing mission on a world, you unlock an outpost plot: a small 12 by 12 grid on that world, built the same way as the Space Center. Outposts are how one success becomes a long-term advantage.

| Outpost building | Function |
|---|---|
| Relay Antenna | Extends link range; boosts data rate for missions to nearby worlds |
| Solar Field or RTG Store | Power for outpost buildings (uses the world's actual sunlight) |
| Ice Extractor | Produces water. Water becomes propellant, sending Propellant to the Space Center |
| Regolith Processor | Produces Materials from local rock |
| Science Station | Continuous small science return; feeds Research and Data |
| Shelter | Protects outpost buildings from local hazards |

Outposts obey their world's hazards. Dust storms cover solar fields. Radiation degrades electronics without shelters. Cold nights need heaters. Long delay means you cannot fix things in time, so outposts need autonomy.

The economy loop is deliberate: Moon ice becomes propellant, propellant makes a Mars mission cheaper, a Mars outpost feeds the next tier, and so on.

---

## Scoring and Debrief

### Score (out of 1,000)

| Category | Max | What it measures |
|---|---|---|
| Objectives | 250 | Threshold and Baseline cards achieved |
| Science return | 150 | Data downlinked (not just collected) and instrument variety |
| Margins kept | 150 | Mass, power, and delta-v reserves at each phase |
| Budget | 150 | Cost against the Charter cap |
| Survival | 150 | Health of the spacecraft at the end, extended-mission time |
| Design efficiency | 150 | Science per kilogram, per watt, per dollar |

| Score | Rating |
|---|---|
| 900 to 1,000 | Exceptional |
| 750 to 899 | Flight Director |
| 600 to 749 | Systems Officer |
| 400 to 599 | Cadet |
| 0 to 399 | Mission Failed (credits still earned) |

Mission outcomes use NASA-style tiers: **Minimum Success**, **Full Success**, and **Extended Mission**.

### The decision trace

The debrief replays the mission on a timeline and pins each result to the choice that caused it.

- The exact decision that caused each loss of points
- Every overridden Chief Engineer warning, shown with the outcome
- Every skipped test, with the fault it would have caught
- What a different choice would have changed (shown with the numbers)
- The matching Anomaly File if the failure mirrors a real one

### Outputs

| Output | Use |
|---|---|
| Score screen | Rating, breakdown, credits earned |
| Decision log | The successor of the Tern-1 log |
| Codex unlocks | Part, world, and anomaly entries with NASA references |
| Mission Design Report | Auto-generated: mass budget, power budget, delta-v budget, link budget, cost breakdown, risk register. Exports as a printable page for classrooms |

---

## Progression and Modes

**Credits** earned at debrief unlock research nodes. **Reputation** unlocks world tiers and board funding.

| Research branch | Sample unlocks |
|---|---|
| Propulsion | Ion thruster, aerobraking, gravity assist planning |
| Power | Larger arrays, RTG, better batteries |
| Communications | X-band, Ka-band high-gain antenna, optical link terminal |
| Thermal and protection | Radiators, radiation vault, heat-tolerant electronics |
| Autonomy | Levels 1 to 3 |
| Science | Each instrument, in tiers |
| Infrastructure | Building upgrades, outpost buildings |

| Rank | Requirement |
|---|---|
| Cadet | Start |
| Systems Officer | Complete Chapter 2 |
| Flight Director | Complete Chapter 6 |
| Architect | Complete Chapter 9 |

| Mode | Description |
|---|---|
| Campaign | The nine chapters |
| Contracts | Generated missions with deadlines and rewards; Vanta Orbital may take them if you wait |
| Sandbox | Unlimited funds, any world unlocked |
| Historical scenario | Apollo 13 style triage; Mars Climate Orbiter "find the bug" |
| Classroom (stretch) | Teacher code, assigned missions, report of student scores and key decisions |

| Difficulty | What changes |
|---|---|
| Cadet | Guided, pre-made designs, gentle events (about 20 minutes) |
| Flight | Full design, standard events (about 45 minutes) |
| Architect | No guardrails, random conditions, cascading failures (60+ minutes) |

---

## Interface

### Style

Flat 2D top-down, dark backgrounds, a strict palette of cyan and amber accents, monospace text for data and a clean sans-serif for dialogue. Blueprint grid lines behind the builder. The base looks like a small, real launch complex seen from above.

Art approach for a small team:

- Buildings and parts drawn as simple layered vector shapes so they can be recolored and upgraded by changing a level tag
- World surfaces are generated from seeded noise with a palette per world, so no world needs hand-painted terrain
- Character portraits are simple bust illustrations with 3 expressions each

### Screens

**Space Center**

```
+----------------------------------------------------------------------------+
| Funds 42.0M  Materials 310  Propellant 120 t  Research 18  Rep 4          |
| Year 1, Week 14           Next window: Moon in 6 days       Base Power OK  |
+----------------------------------------------------------------------------+
|                                                              |  BUILD      |
|   36 x 36 tile grid, pan and zoom                            |  MISSIONS   |
|                                                              |  WORLD MAP  |
|      [Launch Pad]      [Assembly Hall]     [Mission          |  RESEARCH   |
|                                             Control]         |  CODEX      |
|      [Fuel Depot]      [Test Facility]     [Dish]            |             |
|                                                              |             |
+----------------------------------------------------------------------------+
| Builders 1/2   Queue: Solar Farm (3 wk)         [End Week]   [Next Event]  |
+----------------------------------------------------------------------------+
```

**Spacecraft Builder**

```
+----------------------------------------------------------------------------+
| PARTS: Bus | Power | Comms | Science | Thermal | Propulsion | EDL            |
+--------------+---------------------------------------------+---------------+
| part cards   |  CUTAWAY VIEW (bays, mounts)                | METERS        |
| drag to bay  |                                             | Mass 812/1200 |
|              |  layer: [Structure] [Power] [Thermal] [Data]| Cost 340/500  |
|              |                                             | Power +410/-380|
|              |                                             | Delta-v 1.9   |
|              |                                             | Link 120 kbps |
+--------------+---------------------------------------------+---------------+
| Chief Engineer: "Battery is 12% under the recommended size."               |
|                                              [Fix it]   [Override]        |
+----------------------------------------------------------------------------+
```

**Aim**

```
+----------------------------------------------------------------------------+
| WINDOW STRIP:  |||||||||  |||||||  ||||  |||  ||||||  (pick a date)        |
+------------------------------------------------+---------------------------+
|  Sun, Earth orbit, target orbit, transfer arc  | PREDICTION                |
|  (redraws as you change controls)              | Delta-v needed 5.4 / 5.9  |
|                                                | Margin 0.5 km/s           |
|                                                | Arrival day 262           |
|  Time of flight [-----o------]                 | Delay at arrival 14 min   |
|  Gravity assist [ ] Venus  [ ] Earth           | Sunlight at arrival 43%   |
+------------------------------------------------+---------------------------+
```

**Cruise console**

```
+----------------------------------------------------------------------------+
| Earth time 2027-03-02 14:10     Craft time 2027-03-02 14:00     Delay 10 m |
+---------------------------+-------------------------+----------------------+
| SOLAR SYSTEM MAP          | SUBSYSTEMS              | COMMAND TIMELINE     |
| craft, path, error        | Power   Thermal  Comms  | queued: TCM-2        |
| ellipse                   | Data    Propellant      | uplink in 10 min     |
+---------------------------+-------------------------+----------------------+
| DSN link time: [Track 4h] [Data 6h] [Command 2h]     Warp: [1][8][64][512] |
+----------------------------------------------------------------------------+
```

### Sound

A low ambient hum, distinct alert tones per severity, radio chatter clips, a launch rumble, a success chime, and a soft, non-harsh failure tone.

---

## Handling the Game

### Controls

| Input | Action |
|---|---|
| Left click or tap | Select, place, collect resources |
| Drag | Move buildings, drag parts, draw power cables, drag the window cursor |
| Right click or two-finger tap | Cancel, remove |
| Mouse wheel or pinch | Zoom the base or map |
| Middle-drag or WASD | Pan |
| R | Rotate a part or building |
| Space | Pause and resume |
| 1 to 5 | Time warp levels |
| Tab | Cycle console panels |
| F | End week in the Space Center |
| H | Ask the flight controller for a hint (score cost on harder tiers) |
| M | Toggle "Show the math" |
| Esc | Menu |

### First hour

| Minutes | What happens |
|---|---|
| 0 to 5 | Intro, place Mission Control, Assembly Hall, Launch Pad; collect first resources |
| 5 to 15 | Guided Moon flyby (Cadet tier): builder, aim, launch, and debrief in miniature |
| 15 to 30 | Expand the base, build the Tracking Station, fly the lunar orbiter |
| 30 to 45 | Lunar lander: EDL setup and the Daily Planner for the first time |
| 45 to 60 | Tern-1 log recovered; Mars unlocked; first Charter with real conflicts |

### Accessibility

Colorblind-safe palette variants, adjustable text size, all alerts carry an icon and a sound (never color alone), and full keyboard navigation in the builder.

---

## Data-Driven Architecture: One Engine, Every Planet

This is the core technical idea. The engine contains zero planet-specific code. Everything that varies by world is data, and most of that data is derived by rules from a small set of real physical values.

### Principles

1. **One dataset, ten systems on day one.** A world is a row in `bodies.json` plus an optional flavor file.
2. **Rules, not exceptions.** Titan does not have a special case. It has a thick atmosphere, low gravity, and weak sunlight, and the rules produce the right behavior.
3. **Derive first, hand-tune second.** Values like transfer delta-v, launch windows, and light delay are computed by a script. Only story text and art choices are written by hand.
4. **Balance in one place.** Every tunable constant lives in `balance.json`.
5. **Deterministic worlds.** Terrain, hazards, and events use seeds, so any run can be replayed.

### Three data layers

| Layer | Contents | Written by |
|---|---|---|
| Physical | Real constants: orbit, radius, gravity, atmosphere, temperature, radiation tier, rotation | Once, from NASA references |
| Rules | Tag thresholds and effect tables shared by all worlds | Once |
| Flavor | Display name, palette, science target text, story hooks, unlock gate | Per world, short; auto-defaults if missing |

### Folder layout

```
data/
  core/
    bodies.json         real physical data, one entry per body
    tag_rules.json      thresholds that turn physical data into tags
    effects.json        tag -> gameplay effect table
    parts.json
    vehicles.json
    buildings.json
    outpost_buildings.json
    events.json         generic events keyed on tags
    contracts.json      contract templates
    balance.json        all tunable constants
  worlds/
    moon.flavor.json
    mars.flavor.json
    ...                 one small file per world (optional)
  generated/            output of tools/generate.mjs; committed as fallback
    systems.json        merged and derived data per world
    windows.json        launch windows 2026 to 2060
  snapshots/            offline copies of NASA API responses
tools/
  generate.mjs          derives everything from core data
  validate.mjs          schema and sanity checks
```

### Physical entry (example: Mars)

```json
{
  "id": "mars",
  "name": "Mars",
  "kind": "planet",
  "parent": "sun",
  "orbit": { "semiMajorAxisAU": 1.524, "eccentricity": 0.093, "periodDays": 687 },
  "radiusKm": 3390,
  "muKm3s2": 42828,
  "gravity": 3.71,
  "rotationHours": 24.6,
  "atmosphere": { "pressureBar": 0.006, "composition": "CO2", "scaleHeightKm": 11 },
  "temperatureC": { "min": -125, "max": 20 },
  "radiationTier": 2,
  "dust": true,
  "hasSurface": true
}
```

### Tag rules

```json
[
  { "tag": "vacuum",               "when": "atmosphere.pressureBar == 0" },
  { "tag": "thin_atmosphere",      "when": "atmosphere.pressureBar > 0 && atmosphere.pressureBar < 0.05" },
  { "tag": "dense_atmosphere",     "when": "atmosphere.pressureBar >= 0.05 && atmosphere.pressureBar < 10" },
  { "tag": "crushing_atmosphere",  "when": "atmosphere.pressureBar >= 10" },
  { "tag": "no_surface",           "when": "hasSurface == false" },
  { "tag": "solar_marginal",       "when": "solarFluxWm2 < 100" },
  { "tag": "solar_infeasible",     "when": "solarFluxWm2 < 10" },
  { "tag": "extreme_heat",         "when": "temperatureC.max > 300" },
  { "tag": "extreme_cold",         "when": "temperatureC.min < -150" },
  { "tag": "high_radiation",       "when": "radiationTier >= 4" },
  { "tag": "microgravity",         "when": "gravity < 0.5" },
  { "tag": "long_delay",           "when": "lightTimeMaxMin > 20" },
  { "tag": "dust",                 "when": "dust == true" }
]
```

### Effects: how tags change gameplay for every world at once

| Tag | Effect | System that reads it |
|---|---|---|
| vacuum | No parachute or aerobraking; propulsive landing only | EDL, Arrival |
| thin_atmosphere | Aeroshell, parachute, and retro rockets | EDL |
| dense_atmosphere | Parachute plus drag descent; aerial vehicles possible | EDL, Ops |
| crushing_atmosphere | Survival clock on the surface; pressure vessel needed | Builder, Ops |
| no_surface | Only orbiters, flybys, and atmospheric probes | Charter |
| solar_marginal | Solar output warning in Builder; large arrays needed | Builder |
| solar_infeasible | Solar option blocked; RTG required | Builder |
| extreme_heat | Radiator required; higher thermal fault chance | Builder, Tests |
| extreme_cold | Heater required; battery derating | Builder, Ops |
| high_radiation | Rad-hard computer or vault required; dose accumulates | Builder, Tests, Ops |
| microgravity | Anchoring and hop mechanics instead of rolling | Landing, Ops |
| long_delay | Autonomy strongly advised; commands slow | Cruise, Ops |
| dust | Solar output loss events; wheel wear | Ops, Events |

### Derived values (generator)

The script reads each body and computes everything the game needs.

```js
// tools/derive.mjs
const MU_SUN   = 1.32712440018e11;   // km^3/s^2
const AU       = 1.495978707e8;      // km
const MU_EARTH = 398600.4418;        // km^3/s^2
const R_LEO    = 6378.137 + 200;     // km, 200 km orbit
const G0       = 9.80665;            // m/s^2
const SOLAR_1AU = 1361;              // W/m^2
const LIGHT_MIN_PER_AU = 8.317;      // minutes

export function hohmannVInf(r2AU) {
  const r1 = AU, r2 = r2AU * AU;
  const vEarth = Math.sqrt(MU_SUN / r1);
  return Math.abs(vEarth * (Math.sqrt(2 * r2 / (r1 + r2)) - 1));   // km/s
}

export function departureDv(vInf) {
  const vCirc = Math.sqrt(MU_EARTH / R_LEO);
  return Math.sqrt(vInf * vInf + 2 * vCirc * vCirc) - vCirc;        // km/s from LEO
}

export function hohmannDays(r2AU) {
  const a = ((AU + r2AU * AU) / 2);
  return Math.PI * Math.sqrt(a ** 3 / MU_SUN) / 86400;
}

export function synodicDays(aAU) {
  return 365.25 / Math.abs(1 - 1 / Math.pow(aAU, 1.5));
}

export function solarFlux(dAU)      { return SOLAR_1AU / (dAU * dAU); }
export function lightMinutes(dAU)   { return dAU * LIGHT_MIN_PER_AU; }
export function dataRateKbps(baseKbpsAt1AU, dAU) { return baseKbpsAt1AU / (dAU * dAU); }
export function rocketDv(ispSec, m0, m1) { return ispSec * G0 * Math.log(m0 / m1) / 1000; }

export function deriveBody(body, balance) {
  const a = body.orbit.semiMajorAxisAU;
  const vInf = hohmannVInf(a);
  return {
    ...body,
    solarFluxWm2: solarFlux(a),
    departureDvKmS: departureDv(vInf),
    hohmannDays: hohmannDays(a),
    synodicDays: synodicDays(a),
    lightTimeMinMin: lightMinutes(Math.max(a - 1, 0.01)),
    lightTimeMaxMin: lightMinutes(a + 1),
  };
}
```

Sanity check values (built into unit tests): Mars departure delta-v about 3.6 km/s, Mars Hohmann time about 259 days, Mars window spacing about 780 days, Venus window spacing about 584 days.

### Generic event definition (example)

One event applies to every world that has the tag. Adding a world with the `dust` tag automatically adds dust storms to it.

```json
{
  "id": "dust_storm",
  "requires": { "tags": ["dust", "thin_atmosphere"], "phase": ["arrival", "surface"] },
  "weight": 1.0,
  "durationDays": [20, 90],
  "effects": [
    { "stat": "solarOutput", "op": "multiply", "value": 0.35 },
    { "stat": "temperatureSwing", "op": "multiply", "value": 0.7 }
  ],
  "responses": [
    { "id": "hibernate", "label": "Enter hibernation mode", "cost": { "power": 0 }, "effect": "reduceLoad:0.8" },
    { "id": "continue",  "label": "Keep operating",          "cost": { "power": 40 }, "effect": "riskFault:0.15" }
  ]
}
```

### Flavor file (example)

```json
{
  "id": "mars",
  "displayName": "Mars",
  "subtitle": "The red window",
  "palette": { "ground": "#8a4b2d", "sky": "#c9a27a", "accent": "#e07a3f" },
  "unlock": { "missionControlLevel": 2, "requiresMissions": ["moon_orbiter"] },
  "scienceTargets": [
    { "id": "organics", "label": "Detect organic compounds in rock", "needs": ["chemistry"], "value": 40 },
    { "id": "ice_map",  "label": "Map subsurface ice",               "needs": ["radar"],     "value": 30 },
    { "id": "cache",    "label": "Collect and cache samples",        "needs": ["sample"],    "value": 60 }
  ],
  "storyHooks": ["kestrel_cache", "vanta_contract"],
  "codex": ["mars_overview", "dust_storms", "jezero_crater"]
}
```

Any field missing from a flavor file falls back to a generated default (palette from surface temperature and atmosphere, generic science targets by tag, template dialogue). A new world is playable the moment its physical entry exists.

### Adding a new world: checklist

1. Add one entry to `bodies.json` with real physical values.
2. Optionally add `worlds/<id>.flavor.json`.
3. Run `npm run gen`. It derives windows, transfer costs, tags, and terrain seeds, then runs `validate.mjs`.
4. The world appears on the map with a correct card, correct hazards, generated contracts, and generated terrain.

No engine code changes.

### Generic rules the engine applies to every world

| System | Reads from data |
|---|---|
| Solar power | `solarFluxWm2` and dust tag |
| Thermal margin | `temperatureC` range against thermal parts |
| Radiation | `radiationTier` against tolerance of parts; dose accumulates per cycle |
| Comms | Range from `lightTimeMinMin` to `lightTimeMaxMin`; data rate by distance |
| Delta-v | `departureDvKmS`, capture cost from `muKm3s2` and orbit choice |
| EDL | Tags: vacuum, thin, dense, crushing, no_surface |
| Daily Planner | `rotationHours` and day-night pattern; sunlight curve |
| Contracts | Templates filled with world values and reward scaling by tier |
| Terrain | Seeded noise and the world palette; hazard layers for slope and rocks |

### Balance file

All tunable constants sit together so tuning never touches code.

```json
{
  "transfer": {
    "fastTransferPenalty": 1.2,
    "phaseErrorPenaltyAt30Deg": 0.5
  },
  "margins": { "recommendedMassMargin": 0.25, "recommendedPowerMargin": 0.15 },
  "rtg": { "decayPerYear": 0.04 },
  "dust": { "panelLossPerCycle": 0.004 },
  "edl": { "baseStageReliability": 0.97 },
  "scoring": { "objectives": 250, "science": 150, "margins": 150, "budget": 150, "survival": 150, "design": 150 }
}
```

---

## Simulation Math

Simplified for browser speed but mathematically correct.

```
Rocket equation:
  delta_v = Isp * g0 * ln(m_wet / m_dry)

Hohmann transfer (circular, coplanar):
  a_transfer = (r1 + r2) / 2
  t_flight   = pi * sqrt(a_transfer^3 / mu_sun)
  v_infinity = | v1 * ( sqrt(2*r2 / (r1 + r2)) - 1 ) |
  departure_dv_from_LEO = sqrt(v_inf^2 + 2*v_circ^2) - v_circ

Synodic period (launch window spacing):
  S = 1 / | 1/T_earth - 1/T_target |

Phase error for an off-optimal launch date:
  phase_error_deg = |days_from_optimal| * (360 / S)
  departure_dv    = dv_hohmann * (1 + 0.5 * (phase_error_deg / 30)^2)
                    * (1 + 1.2 * max(0, T_hohmann / T_chosen - 1))

Solar power at distance d (AU):
  P = P_1AU / d^2     (times dust factor and sun-angle factor)

Data rate at distance d (AU):
  rate = rate_1AU / d^2

Light delay (one-way):
  minutes = distance_AU * 8.317

Radiation dose accumulation:
  dose_per_cycle = world_dose_rate * cycle_length * (1 - shielding)
  fault_chance rises as accumulated_dose approaches part tolerance

EDL success:
  P = product(stage_reliability_i * (1 - hazard_i)) * (1 - site_hazard)
  landing scatter: Monte Carlo of ~200 points from navigation error + wind + timing
```

The constants in the transfer penalty are tunable. Formulas are validated against published NASA values in unit tests.

---

## NASA Data Integration

Real data is used for setup and flavor. **The game never depends on a live API during play.**

| Feature | Source | Usage | Fallback |
|---|---|---|---|
| Planet positions | JPL Horizons | Ephemeris table 2026 to 2060, used for the map and window math | Bundled snapshot |
| Asteroid events | NASA NeoWs | Real near-Earth close approaches as cruise events and news ticker items | Bundled list |
| Space weather | NASA DONKI | Real solar flare and storm history as event templates | Bundled list |
| Launch news | Launch Library 2 | News ticker and contract inspiration | Bundled list |
| Terrain images | NASA Trek and image libraries | Codex images, landing site backgrounds | Bundled images |
| Mars weather and dust | Mars mission datasets (PDS) | Dust storm profiles and temperature swings | Bundled table |
| Part specs | Published mission datasheets | Order of magnitude for mass, power, and data | Already in parts.json |

Notes:

- Use a build step to fetch snapshots and commit them. Most players need no live calls at all.
- The InSight weather feed is not live any more (the mission ended in 2022). Use archived Mars datasets.
- Check the status and rate limits of each API on the first day of development.
- NASA media is generally free to use, but check the licensing note for every image before bundling it.

---

## Tech Stack

| Layer | Technology | Reason |
|---|---|---|
| Game rendering | Phaser 3 (scenes, tilemap-style grids, input) with Canvas | A scene per stage, camera pan and zoom, and hit testing come built in. Plain Canvas also works, at the cost of writing those pieces |
| UI panels | HTML and CSS overlay | Fast to build meters, tables, and dialogue; accessible |
| Language | Vanilla JS or TypeScript | TypeScript helps because the data schemas are large |
| Build | Vite | Fast reload, simple production build |
| Tests | Vitest | The physics module is pure functions and easy to check against known values |
| State | One store with an event bus; save to localStorage and export to JSON | Simple and debuggable |
| Data pipeline | Node scripts in `tools/` | Generates and validates all world data |
| Leaderboard (optional) | Firebase Realtime Database | Only if time allows |

### Project structure

```
mission-architect-frontier/
|-- index.html
|-- data/                    (see Data-Driven Architecture)
|-- tools/
|   |-- generate.mjs
|   |-- derive.mjs
|   |-- validate.mjs
|-- src/
|   |-- main.js
|   |-- core/
|   |   |-- store.js         (game state, save and load)
|   |   |-- calendar.js      (program calendar)
|   |   |-- physics.js       (pure functions: rocket, transfer, power, link)
|   |   |-- tags.js          (tag rules and effect lookups)
|   |   |-- events.js        (generic event engine)
|   |   |-- scoring.js       (score and decision trace)
|   |   |-- contracts.js     (contract generator)
|   |-- scenes/
|   |   |-- Boot.js
|   |   |-- SpaceCenter.js
|   |   |-- WorldMap.js
|   |   |-- Charter.js
|   |   |-- Builder.js
|   |   |-- Aim.js
|   |   |-- Launch.js
|   |   |-- Cruise.js
|   |   |-- Arrival.js
|   |   |-- Ops.js
|   |   |-- Outpost.js
|   |   |-- Debrief.js
|   |-- ui/
|   |   |-- panels.js
|   |   |-- meters.js
|   |   |-- dialogue.js
|   |-- gen/
|       |-- terrain.js       (seeded terrain and hazard layers)
|-- assets/
    |-- art/
    |-- audio/
    |-- fonts/
```

### Performance targets

- First paint under 2 seconds on a mid-range laptop
- 60 FPS on the base and map screens
- Trajectory recalculation under 16 ms, so slider drags stay smooth
- Cruise at the highest time warp without frame drops
- Total first-load transfer under 2 MB

---

## Development Roadmap

Today is September 20, 2026. Submission is November 10, 2026. That is seven weeks and two days.

The plan builds one complete vertical slice first, then widens it. Because the engine is data-driven, all ten systems exist from week 1; the work is making each stage playable and then adding content.

### Week 1 (Sep 21 to Sep 27): Data and engine foundation
- [ ] Repository, Vite, Phaser boot, folder structure
- [ ] `bodies.json` for all 10 systems with real values
- [ ] `derive.mjs` and `generate.mjs`; unit tests for Hohmann, window spacing, light delay
- [ ] `parts.json`, `vehicles.json`, `buildings.json`, `balance.json` (first pass)
- [ ] Store, calendar, save and load
- [ ] Space Center grid: place, move, and remove buildings

### Week 2 (Sep 28 to Oct 4): Space Center and World Map
- [ ] Resource production and tap-to-collect
- [ ] Build queue, builders, upgrades, layout rules
- [ ] World Map with cards generated from data
- [ ] Charter screen with objective cards and Threshold / Baseline sorting
- [ ] Base events (storm, audit)

### Week 3 (Oct 5 to Oct 11): Spacecraft Builder
- [ ] Bay grid, part shapes, mounts, drag and drop
- [ ] Live meters (mass, cost, power, delta-v, link, thermal, radiation)
- [ ] Power and thermal layers
- [ ] Engineer feedback and overrides
- [ ] Vehicle selection with rocket-equation payload check
- [ ] Test Facility and hidden fault model, Design Review

### Week 4 (Oct 12 to Oct 18): Aim, Launch, and Cruise
- [ ] Window strip and trajectory preview
- [ ] Prediction panel and "Show the math" toggle
- [ ] Go/No-Go poll (ascent mini-game is optional; autopilot first)
- [ ] Cruise console with two clocks, light delay, command timeline
- [ ] DSN link allocation, navigation ellipse, TCM
- [ ] Generic event engine with the first 10 tag-based events
- [ ] **Checkpoint: one complete Moon mission from base to launch to arrival**

### Week 5 (Oct 19 to Oct 25): Arrival, Operations, Debrief
- [ ] Orbit insertion and aerobraking option
- [ ] Site selection map, EDL setup, Monte Carlo ellipse, descent animation
- [ ] Daily Planner with power, storage, thermal, and downlink constraints
- [ ] Debrief: score, decision trace, Anomaly Files
- [ ] Mission Design Report export
- [ ] Outposts: Moon and Mars plots and 4 buildings
- [ ] **Checkpoint: Moon and Mars playable end to end**

### Week 6 (Oct 26 to Nov 1): Content across all worlds
- [ ] Flavor files for all 10 systems (short, using defaults where needed)
- [ ] Contract generator
- [ ] Remaining events (about 20 total)
- [ ] Story: full dialogue for Chapters 1 and 2, condensed for the rest
- [ ] Tern-1 log sequence
- [ ] Research tree and Codex
- [ ] NASA data snapshots bundled

### Week 7 (Nov 2 to Nov 8): Polish and submission
- [ ] Art pass on every screen
- [ ] Sound
- [ ] Playtesting with 4 to 6 real players; balance pass using `balance.json`
- [ ] Tutorial and Cadet mode pass
- [ ] Demo video and submission write-up

### Nov 9 to Nov 10: Buffer and submission

### Cut list (in order, if time runs short)

1. Ascent mini-game (keep autopilot)
2. Outposts on worlds other than Moon and Mars
3. Firebase leaderboard
4. Contracts and Vanta Orbital
5. Sound beyond the essentials
6. Chapters 8 and 9 story text (keep worlds playable with template dialogue)

### Definition of the submittable build

- Moon and Mars playable through all six stages
- All ten worlds present on the map, playable through the generic flow
- Save and load works
- Debrief shows a decision trace
- Runs offline from bundled data

---

## Testing

- Playtest with 3 to 4 people every week from Week 3
- Physics validated against published NASA values through unit tests
- Data validated on every build (`validate.mjs`)
- API fallback tested with the network disabled
- Performance measured in Chrome DevTools
- Cross-browser: Chrome, Firefox, Safari, Edge
- Tutorial tested with someone who has never seen the game

---

## Stretch Goals

Not in scope for November 10.

- Classroom mode with teacher codes and reports
- Community missions written as JSON
- Historical reenactments (Apollo, Voyager, Perseverance)
- Multiplayer roles (Science Lead, Engineer, Flight Director, Budget Chair)
- More destinations (asteroids, Triton landers, comets) as data files
- Daily challenge based on real space weather
- Mobile-friendly layout pass

---

## License

Distributed under the MIT License. See `LICENSE` for details.

---

## Acknowledgments

- NASA Space Apps Challenge, for the challenge brief
- NASA JPL, for Horizons and small-body data
- NASA, for NeoWs, DONKI, image libraries, and mission datasheets
- The Space Devs, for the Launch Library 2 API
- Published mission failure reports that inspired the Anomaly Files

---

## Appendix: Glossary

- **Delta-v:** Change in velocity. The currency of spaceflight.
- **Hohmann transfer:** The most fuel-efficient transfer between two circular orbits.
- **Synodic period:** Time between repeats of the same alignment of two planets. Sets launch window spacing.
- **Launch window:** A period when the planets are positioned well enough for a low-energy transfer.
- **TCM:** Trajectory Correction Maneuver. A small burn to fix drift.
- **DSN:** Deep Space Network. NASA's set of large dishes for talking to distant spacecraft.
- **Light delay:** The time a signal takes to travel between Earth and the spacecraft.
- **RTG:** Radioisotope Thermoelectric Generator. A nuclear power source that works far from the Sun.
- **EDL:** Entry, Descent, and Landing.
- **Aerobraking:** Using atmospheric drag to slow down and save fuel.
- **Margin:** Reserve kept above the calculated requirement.
- **Autonomy:** Onboard software that handles known faults without waiting for commands.
- **Extended mission:** Operation beyond the planned primary mission.

---

## Contact

**Project Lead:** Savindu
**Event:** 2026 NASA Space Apps Challenge, Space Mission Design Game
**Submission Date:** November 10, 2026

---

<div align="center">

*Mission Architect: Frontier, Version 2.0, Design Document*

</div>
