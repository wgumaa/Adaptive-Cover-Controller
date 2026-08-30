<p align="center">
  <img src="images/banner.png" alt="Adaptive Cover Controller">
</p>

# Adaptive Cover Controller

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.7%2B-41BDF5?logo=homeassistant&logoColor=white)
![Blueprint](https://img.shields.io/badge/Blueprint-Automation-blue)
![License](https://img.shields.io/badge/License-MIT-green)

Adaptive Cover Controller is a Home Assistant blueprint for automatically controlling curtains, blinds and shutters based on the sun's position.

Protection is determined using the sun's azimuth and elevation, with optional weather, effective sky obstruction, occupancy and schedule validation. Each cover runs as its own automation and can be configured independently.

---

> [!NOTE]
> **AI-assisted development**
>
> This project was developed using AI as an engineering tool - not as a replacement for engineering.
>
> AI assisted with brainstorming, code reviews, documentation and iterative refinement, while all architectural decisions, implementation choices and real-world testing were carried out by the project author.

## Installation

### Import using My Home Assistant (recommended)

[![Open your Home Assistant instance and import this blueprint.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/wgumaa/Adaptive-Cover-Controller/main/blueprint/adaptive_cover_controller.yaml)

### Manual installation

Copy:

```text
adaptive_cover_controller.yaml
```

to:

```text
config/blueprints/automation/
```

Reload Blueprints and create a new automation using **Adaptive Cover Controller**.

---

## Features

- Sun position control using azimuth and elevation
- Optional weather validation
- Optional effective sky obstruction validation with hysteresis — accepts a plain cloud-cover-percentage sensor, or a more sophisticated computed obstruction sensor if you have one
- Optional occupancy validation
- Three-tier protection level (FULL / PARTIAL / NONE) — tilt-capable covers can hold position and adjust tilt instead of fully opening on light cloud
- Adaptive tilt for Venetian blinds, reacting continuously to live sky obstruction
- Scheduled opening
- Night lock
- Manual override detection, with a configurable timeout to automatically resume automatic control
- Automatic recovery after Home Assistant restarts
- Individual configuration for every cover

---

## Configuration

Each automation controls a single cover.

The blueprint is organised into the following sections:

- Cover
- Sun Protection
- Positions
- Schedule
- Manual Override
- Occupancy
- Weather Validation
- Effective Sky Obstruction
- Blind Features
- Advanced

### Manual Override

If Manual Override is enabled, create one Input Select helper for each cover with the following options:

```text
normal
automation
manual
```

Do not share the same helper between multiple covers.

A manual change is detected automatically and pauses the automation until either the cover is returned to the position the automation would choose, or the configured **Manual override timeout** elapses — whichever comes first. Set the timeout to `0` to disable it and require a matching position to resume automatically.

---

## Blueprint

<p align="center">
<img src="images/blueprint_configuration1.png" width="900">
</p>

---

## How It Works

Sun position, weather validation and occupancy validation form a single gate. If any of them fail, the cover fully opens (or stays open) — no further checks are needed.

Once the gate passes, effective sky obstruction sets the protection level:

- **FULL** — obstruction is low enough that full sun protection is needed. The cover moves to its protection position (and, for tilt-capable covers, its protection tilt).
- **PARTIAL** — tilt-capable covers only. Obstruction has risen, but the sun is still in the configured window, so the cover stays in position rather than fully reopening — only the tilt angle adjusts, continuously, to the live reading. Covers without tilt don't have this middle state; they simply reopen once obstruction rises far enough.
- **NONE** — either the gate failed, or (for covers without tilt) obstruction is high enough that protection isn't needed at all.

Before any movement happens — protecting or returning — the automation checks that the cover is idle, isn't currently held in manual override, and that Home Assistant is fully running. Returning to the normal position additionally respects the configured opening schedule and night lock.

To avoid unnecessary movement, commands are only sent when the requested position or tilt differs from the current state.

<p align="center">
<img src="images/how-it-works.png" width="1000">
</p>

---

## Requirements

- Home Assistant 2025.7 or later
- One supported cover entity
- One Input Select helper per cover when using Manual Override

---

## License

Released under the MIT License.
