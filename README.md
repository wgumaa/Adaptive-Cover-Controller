<p align="center">
  <img src="images/banner.png" alt="Adaptive Cover Controller">
</p>

<h1 align="center">Adaptive Cover Controller</h1>

<p align="center">
An intelligent Home Assistant blueprint that automatically protects curtains, blinds and shutters from direct sunlight using the sun's position and optional environmental validation.
</p>

<p align="center">

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.7%2B-41BDF5?logo=homeassistant&logoColor=white)
![Blueprint](https://img.shields.io/badge/Blueprint-Automation-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Version](https://img.shields.io/badge/Version-v2.0-orange)

</p>

---

## 🚀 Quick Start

Get up and running in just a few minutes.

1. Import the blueprint into Home Assistant.
2. Create one automation for each cover.
3. Configure the sun protection zone.
4. (Optional) Enable weather, cloud cover, occupancy or scheduling.
5. Sit back and let Adaptive Cover Controller protect your home.

---

## 🎯 Why You'll Love It

Unlike simple time-based automations, Adaptive Cover Controller continuously evaluates real-world conditions before moving a cover.

It intelligently combines:

- ☀️ Sun azimuth & elevation
- 🌤 Weather conditions
- ☁️ Cloud cover
- 👤 Occupancy
- 🕒 Schedules
- 🌙 Night lock

The result is a controller that moves your covers only when protection is genuinely required, reducing unnecessary movement while maintaining comfort throughout the day.

---

## ✨ Highlights

| Feature | Description |
|----------|-------------|
| ☀️ Sun Position | Uses the sun's azimuth and elevation for intelligent positioning. |
| 🌤 Weather Validation | Ignore protection during unsuitable weather conditions. |
| ☁️ Cloud Cover | Optional hysteresis prevents unnecessary movement. |
| 👤 Occupancy | Only protect occupied rooms if desired. |
| 🌙 Night Lock | Prevent automatic opening overnight. |
| 🕒 Scheduling | Independent weekday and weekend opening times. |
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

Create one **Dropdown Helper** for every cover containing:

```text
normal
automation
manual
```

The helper allows the blueprint to distinguish between:

- Normal operation
- Automation-controlled movement
- Manual user control

> **Important**
>
> Every cover requires its own helper.
> Do not share helpers between multiple automations.

---

## Optional Modules

Enable only the features you need.

- Weather validation
- Cloud cover validation
- Occupancy validation
- Tilt control
- Night lock
- Scheduled opening

Every automation can be configured independently, allowing different rooms to behave differently.

---

# 🧠 Manual Override

Adaptive Cover Controller automatically detects when a user manually moves a cover.

When this happens:

1. Manual mode is activated.
2. Automation immediately pauses.
3. Full user control is respected.

Automation resumes only after the cover has been manually returned to the position currently requested by the controller.

This prevents the automation from repeatedly fighting manual adjustments.

---

# 🔄 How It Works

The controller continuously evaluates:

1. Sun azimuth
2. Sun elevation
3. Weather (optional)
4. Cloud cover (optional)
5. Occupancy (optional)
6. Night lock
7. Scheduled opening

When every enabled condition is satisfied, the cover moves to the configured protection position.

Once protection is no longer required, the controller automatically returns the cover to its normal position.

To minimise unnecessary commands, movement only occurs when the cover is idle and not already at the requested position.

Automatic recovery also occurs after:

- Home Assistant restarts
- Missed events
- Periodic synchronization

---

# 🏡 Real World Examples

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

# ✅ Compatibility

Adaptive Cover Controller works with most Home Assistant cover entities, including:

- Curtains
- Roller blinds
- Venetian blinds
- Interior shutters
- Exterior shutters

Supports:

- Open / Close
- Position control
- Optional tilt control

---

# ❓ Frequently Asked Questions

### Can I control multiple covers?

Yes.

Create one automation for each cover.

---

### Can every room have different settings?

Absolutely.

Each automation is completely independent.

---

### Do I need the Controller Mode helper?

Only if you enable Manual Override detection.

---

### Does it work after Home Assistant restarts?

Yes.

The blueprint automatically restores its state and immediately re-evaluates whether protection is required.

---

### Does it support shutters?

Yes.

It supports curtains, blinds and shutters that expose standard Home Assistant cover controls.

---

# ❤️ Support

If you find this blueprint useful, please consider:

⭐ Starring the repository

🐞 Reporting bugs

💡 Suggesting new features

🤝 Contributing improvements

Every contribution helps improve the project for the Home Assistant community.

---

# 📄 License

Released under the **MIT License**.

---

<p align="center">

Made with ❤️ for the Home Assistant community.

</p>