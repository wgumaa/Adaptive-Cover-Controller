<p align="center">
  <img src="images/banner.png" alt="Adaptive Cover Controller">
</p>

# Adaptive Cover Controller

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.7%2B-41BDF5?logo=homeassistant&logoColor=white)
![Blueprint](https://img.shields.io/badge/Blueprint-Automation-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Version](https://img.shields.io/badge/Version-v2.0-orange)

An intelligent Home Assistant blueprint that automatically protects curtains, blinds and shutters from direct sunlight.

Using the sun's real-time azimuth and elevation, Adaptive Cover Controller determines when protection is required. Optional weather, cloud cover, occupancy and scheduling validation ensure covers only move when it actually makes sense.

Each cover runs as its own automation, allowing every room in your home to have completely independent protection zones and behaviour.

---

# 🚀 Quick Start

Get started in just a few minutes:

1. Import the blueprint into Home Assistant.
2. Create one automation for each cover.
3. Configure the sun protection zone.
4. (Optional) Enable weather, cloud cover, occupancy or scheduling.
5. Enjoy intelligent automatic sun protection.

---

# ✨ Highlights

| Feature | Description |
|----------|-------------|
| ☀️ Sun Position | Uses the sun's azimuth and elevation to determine when protection is required. |
| 🌤 Weather Validation | Optionally ignore protection during unsuitable weather conditions. |
| ☁️ Cloud Cover | Optional hysteresis prevents unnecessary cover movement. |
| 👤 Occupancy | Only protect rooms when occupied, if desired. |
| 🌙 Night Lock | Prevent automatic opening overnight. |
| 🕒 Scheduled Opening | Independent weekday and weekend opening times. |
| ✋ Manual Override | Automatically detects and respects manual movement. |
| 🔄 Automatic Recovery | Startup and periodic synchronization prevent missed events. |
| 🪟 Wide Compatibility | Supports curtains, blinds and shutters. |

---

# 📸 Blueprint

## Main Configuration

<p align="center">
<img src="images/blueprint_configuration1.png" width="900">
</p>

## Optional Features

<p align="center">
<img src="images/blueprint_configuration2.png" width="900">
</p>

---

# 🚀 Installation

## Option 1 — Import into Home Assistant (Recommended)

Import the blueprint directly into your Home Assistant instance.

[![Open your Home Assistant instance and import this blueprint.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/wgumaa/Adaptive-Cover-Controller/main/blueprint/adaptive_cover_controller.yaml)

---

## Option 2 — Manual Installation

1. Download:

```text
adaptive_cover_controller.yaml
```

from the **blueprint** folder.

2. Copy it to:

```text
config/blueprints/automation/
```

3. Reload Blueprints.

4. Create a new automation using **Adaptive Cover Controller**.

---

# 📋 Requirements

- Home Assistant **2025.7** or newer
- One supported cover entity
- One Controller Mode helper per cover (when using Manual Override)

---

# ⚙️ Configuration

Each automation controls **one individual cover**, allowing every room to have its own behaviour and protection settings.

## Required Settings

Configure:

- Cover entity
- Controller Mode helper
- Sun azimuth start
- Sun azimuth end
- Minimum elevation
- Protection position
- Normal position

---

## Controller Mode Helper

Create one **Dropdown Helper** for every cover with the following options:

```text
normal
automation
manual
```

The helper is used to distinguish between:

- Normal operation
- Automation-controlled movement
- Manual user control

> **Important**
>
> Every cover requires its own helper.
> Do not reuse the same helper across multiple automations.

---

## Optional Modules

Enable only the features you need.

- Weather validation
- Cloud cover validation
- Occupancy validation
- Tilt control
- Night lock
- Scheduled opening

Each automation can be configured independently, allowing every room to behave differently.

---

# ☀️ Why Adaptive?

Unlike simple time-based automations, Adaptive Cover Controller continuously evaluates real-world conditions before moving a cover.

By combining the sun's position with optional weather, cloud cover, occupancy and scheduling validation, the blueprint helps reduce unnecessary movement while maintaining effective protection from direct sunlight.

---

# 🧠 Manual Override

The blueprint automatically detects when a cover is moved manually.

When manual movement is detected:

1. Manual mode is activated.
2. Automation immediately pauses.
3. The user retains full control.

Automatic operation resumes only after the cover is manually returned to the position currently requested by the controller.

This prevents the automation from repeatedly fighting manual adjustments.

---

# 🔄 How It Works

Adaptive Cover Controller continuously evaluates the sun's position together with any optional validation modules you've enabled. Covers only move when **all configured conditions are satisfied**, helping to reduce unnecessary movement while maintaining effective protection from direct sunlight.

<p align="center">
  <img src="images/how-it-works.png" width="1000" alt="Adaptive Cover Controller decision flow">
</p>

The controller evaluates the following conditions:

1. ☀️ Sun azimuth and elevation
2. 🌤 Weather validation *(optional)*
3. ☁️ Cloud cover validation *(optional)*
4. 👤 Occupancy validation *(optional)*
5. 🌙 Night lock
6. 🕒 Scheduled opening
7. 🔄 System state and manual override

If every enabled condition passes, the cover moves to the configured **Protection Position**.

If protection is no longer required, the cover automatically returns to its configured **Normal Position**.

To avoid unnecessary commands, movement only occurs when the cover is idle and not already at the requested position.

The blueprint also automatically recovers after:

- 🚀 Home Assistant restarts
- 🔄 Missed state changes
- ⏱ Periodic synchronization

---

# 💡 Real World Examples

### 🛏 Bedroom

- Morning sun protection
- Night lock enabled

### 🛋 Living Room

- Afternoon sun protection
- Cloud cover validation enabled

### 💻 Home Office

- Occupancy validation enabled
- Manual override enabled

### 🌿 Conservatory

- Maximum sun protection
- Weather validation disabled

---

# ❓ Frequently Asked Questions

### Can I control multiple covers?

Yes.

Create one automation for every cover.

---

### Do I need the Controller Mode helper?

Only if you enable Manual Override detection.

---

### Can every room have different settings?

Yes.

Each automation is completely independent.

---

### Does it support shutters?

Yes.

It supports curtains, roller blinds, Venetian blinds and shutters that expose standard Home Assistant cover controls.

---

### Does it work after Home Assistant restarts?

Yes.

The blueprint automatically restores its state and immediately re-evaluates whether protection is required.

---

# ❤️ Support

If you find this blueprint useful, please consider:

- ⭐ Starring the repository
- 🐞 Reporting bugs
- 💡 Suggesting new features
- 🤝 Contributing improvements

Every contribution helps improve the project for the Home Assistant community.

---

# 📄 License

Released under the **MIT License**.