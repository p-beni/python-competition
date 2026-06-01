# OSNI — Orbit Simulation with Numerical Integration

A real-time, interactive 2D gravitational simulation built in Python. Watch planets, moons, and asteroids orbit each other under Newtonian gravity — then reach in and move them.

---

## Features

- **Real-time simulation** using Euler numerical integration and Newton's law of gravitation
- **Interactive controls** — drag bodies, redirect velocities, spawn new objects mid-simulation
- **Energy tracking** — monitors system energy drift as a proxy for simulation accuracy
- **Preset library** — Solar System, three- and four-body problems, satellite scenarios, and more
- **Export/import** — save any simulation state as a JSON preset and reload it later
- **Auto-scaling viewport** — the view always adjusts to keep all bodies in frame

---

## Getting Started

### Requirements

```
Python 3.x
numpy
matplotlib
tkinter  (usually bundled with Python)
```

Install dependencies:

```bash
pip install numpy matplotlib
```

### Run

```bash
python main.py
```

A menu will open. Pick a preset or use the default Solar System, then click **Start Simulation**.

---

## Controls

| Input | Action |
|---|---|
| `Space` | Pause / Resume |
| `U` | Increase timestep `dt` (faster, less accurate) |
| `J` | Decrease timestep `dt` (slower, more accurate) |
| `Shift` | Increase mass of body to be created (×10) |
| `Ctrl` | Decrease mass of body to be created (÷10) |

**While paused:**

| Input | Action |
|---|---|
| Hover over body | Highlight that body's trajectory |
| Left-click + drag | Move a body |
| Right-click body | Select body (prints data to console) |
| Left-click (selected) | Point velocity toward cursor |
| Arrow keys (selected) | Nudge velocity by 200 m/s |
| Middle-click | Spawn new body at cursor position |
| `V` | Toggle velocity vectors |
| `E` | Export current layout as a new preset |

---

## Presets

Presets live in the `presets/` folder as JSON files. Each file is a list of bodies:

```json
[
  {
    "name": "Earth",
    "mass": 5.972e24,
    "position": [0.0, 0.0],
    "velocity": [0.0, 0.0]
  }
]
```

| Preset | Description |
|---|---|
| `SolarSystem` | The inner Solar System |
| `Threebody1–3` | Three-body problem configurations |
| `Fourbody1–3` | Four-body problem configurations |
| `Sat1`, `Sat2` | Satellite orbit scenarios |
| `Custom` | User-defined starting point |

Create your own by editing any JSON, or export a paused simulation with `E`.

---

## Project Structure

```
.
├── main.py             # Simulation loop and visualization
├── Satelliteobject.py  # Satellite class with mouse/keyboard interaction
├── myfunctions.py      # Physics: gravity, energy, import/export, time
├── eventhandler.py     # Global key/mouse events and simulation mode state
├── menu.py             # Tkinter launch menu
└── presets/            # JSON preset files
```

---

## How It Works

Each timestep `dt`, every pair of bodies exchanges a gravitational force computed from Newton's law. Velocities are updated by Euler integration, then positions are stepped forward. Close encounters (distance < 500 km) use elastic collision velocity exchange to prevent numerical divergence.

System energy (kinetic + potential) is tracked continuously. The percentage drift from `t = 0` is displayed next to the simulation — smaller `dt` keeps this number close to zero.

---

*Disclaimer: AI was used to debug the code and to learn new syntaxes.*
