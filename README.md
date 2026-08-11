<p align="center">
  <img src="images/banner.png" alt="Adaptive Cover Controller">
</p>

# Adaptive Cover Controller

<p align="center">

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2025.7%2B-41BDF5?logo=homeassistant&logoColor=white)
![Blueprint](https://img.shields.io/badge/Blueprint-Automation-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Version](https://img.shields.io/badge/Version-v2.0-orange)

</p>

An intelligent Home Assistant blueprint that automatically protects curtains,
blinds and shutters from direct sunlight.

Using the sun's real-time azimuth and elevation, the controller decides when
protection is required. Optional weather, cloud cover, occupancy and schedule
validation ensure covers only move when it actually makes sense.

Each cover runs as its own automation, making it easy to create independent
protection zones for every room in your home.

---

# ✨ Highlights

- ☀️ Sun position aware (azimuth & elevation)
- 🌤 Optional weather validation
- ☁️ Cloud cover validation with hysteresis
- 👤 Occupancy aware
- 🌙 Night lock
- 🕒 Scheduled morning opening
- ✋ Manual override detection
- 🔄 Automatic recovery after manual override
- 🚀 Startup recovery after Home Assistant restart
- ⏱ Periodic synchronization
- 🪟 Supports curtains, blinds and shutters

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

Click the button below to import the blueprint directly into Home Assistant.

[![Open your Home Assistant instance and import this blueprint.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/wgumaa/Adaptive-Cover-Controller/main/blueprint/adaptive_cover_controller.yaml)

---

## Option 2 — Manual Installation

1. Download

```
adaptive_cover_controller.yaml
```

from the **blueprint** folder.

2. Copy it to

```
config/blueprints/automation/
```

3. Reload Blueprints.

4. Create a new automation using **Adaptive Cover Controller**.

---

# 📋 Requirements

- Home Assistant **2025.7** or newer
- One cover entity
- One Controller Mode helper per cover (when using Manual Override)

---

# ⚙️ Configuration

Each automation controls **one cover**.

## Required

Configure:

- Cover entity
- Controller Mode helper
- Sun azimuth start
- Sun azimuth end
- Protection position

---

## Controller Mode Helper

Create one **Input Select** helper for every cover with these options:

```
normal
automation
manual
```

The helper allows the blueprint to distinguish between:

- Normal operation
- Automation-controlled movement
- Manual user override

> **Important**
>
> Every cover requires its own helper.
> Do not share helpers between automations.

---

## Optional Modules

Enable only the features you need.

- Weather validation
- Cloud cover validation
- Occupancy validation
- Tilt control
- Night lock
- Scheduled morning opening

Each cover can have completely different settings.

---

# ☀️ Why Adaptive?

Unlike simple time-based automations, Adaptive Cover Controller continuously
evaluates real-world conditions before moving a cover.

This greatly reduces unnecessary movement while still protecting rooms from
direct sunlight whenever it is actually needed.

---

# 🧠 Manual Override

When a user manually moves a cover:

1. Manual mode is detected automatically.
2. Automation pauses immediately.
3. The user has full control.

Automation resumes only after the cover is manually returned to the position
currently requested by the controller.

This prevents the automation from fighting manual adjustments.

---

# 🔄 How It Works

The controller continuously evaluates:

1. Sun azimuth
2. Sun elevation
3. Weather (optional)
4. Cloud cover (optional)
5. Occupancy (optional)
6. Night lock
7. Opening schedule

If all enabled conditions are satisfied, the cover moves to its protection
position.

When protection is no longer required, the cover automatically returns to its
normal position.

To avoid unnecessary commands, movement is requested only when the cover is
idle and not already at the requested position.

Automatic recovery also occurs after:

- Home Assistant restarts
- Missed state changes
- Periodic synchronization

---

# 💡 Example Use Cases

### Bedroom

- Morning sun protection
- Night lock enabled

### Living Room

- Afternoon protection
- Cloud cover validation enabled

### Office

- Occupancy validation enabled
- Manual override enabled

### Conservatory

- Maximum sun protection
- Weather disabled

---

# ❓ Frequently Asked Questions

### Can I use multiple covers?

Yes.

Create one automation per cover.

---

### Do I need a helper?

Only if you want Manual Override detection.

---

### Can every room have different settings?

Yes.

Each automation is completely independent.

---

### Does it work with shutters?

Yes.

It supports:

- Curtains
- Roller blinds
- Venetian blinds
- Shutters

---

### Does it work after Home Assistant restarts?

Yes.

The blueprint automatically restores its state and re-evaluates whether
protection is required.

---

# ❤️ Contributing

Bug reports, suggestions and improvements are always welcome.

If you find this blueprint useful, please consider starring the repository.

---

# 📄 License

Released under the **MIT License**.