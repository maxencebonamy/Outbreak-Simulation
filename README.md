# Outbreak Simulation

A cellular automaton simulating the spread of an epidemic on a grid.

Cells of a grid are healthy, infected, immunized or dead. Infection spreads between adjacent cells according to configurable probabilities, and the simulation is displayed in a Pygame window. When it ends, the evolution of each population is plotted as curves.

## Table of contents

- [Outbreak Simulation](#outbreak-simulation)
	- [Table of contents](#table-of-contents)
	- [How it works](#how-it-works)
	- [Tech stack](#tech-stack)
	- [Repository structure](#repository-structure)
	- [Prerequisites](#prerequisites)
	- [Installation](#installation)
	- [Configuration](#configuration)
	- [Running locally](#running-locally)
	- [License](#license)

## How it works

1. **Grid creation**: the window is divided into square cells. All cells start healthy.
2. **Initial state**: a fraction of the cells is infected and a fraction is vaccinated (immunized), both at random positions.
3. **Infection**: at each frame, a healthy cell can be infected by each of its infected neighbors (up to 8 around it), with the probability `INFECTION_RATE` per neighbor.
4. **Evolution of an infected cell**: at each frame, an infected cell dies with the probability `FATALITY_RATE / RECOVERY_TIME`. Otherwise it recovers with the probability `1 / RECOVERY_TIME`. A recovered cell becomes immunized with the probability `IMMUNITY_RATE`, and healthy again otherwise.
5. **End**: the simulation stops when no infected cell remains, or when the window is closed.
6. **Curves**: the percentage of healthy, infected, immunized and dead cells over time is plotted with Matplotlib.

Cell colors: green for healthy, red for infected, blue for immunized, black for dead.

## Tech stack

| Layer | Technologies |
| --- | --- |
| Language | Python 3 |
| Display | Pygame |
| Plotting | Matplotlib |

## Repository structure

```
.
├── assets/
│   └── icon.png     Window icon
├── script/
│   ├── cell.py      Cell: position, state and drawing
│   ├── grid.py      Grid: initialization, update, display and curves
│   └── state.py     Cell states and their colors
├── config.py        Simulation parameters
└── main.py          Entry point and main loop
```

`config.py` is imported with `from config import *` by the other modules, which also get `pygame` and `Vector2` through it. Paths such as `assets/icon.png` are relative, so the program must be started from the repository root.

## Prerequisites

- [Python](https://www.python.org/) 3
- [pip](https://pip.pypa.io/)

## Installation

```bash
git clone git@github.com:maxencebonamy/Outbreak-Simulation.git
cd Outbreak-Simulation
pip install pygame matplotlib
```

The repository declares no dependency file and no Python version.

## Configuration

Parameters are constants in `config.py`. Edit the file before starting the simulation.

| Variable | Description | Example |
| --- | --- | --- |
| `WINDOW_SIZE` | Window dimensions, in pixels | `Vector2(1280, 720)` |
| `WINDOW_FPS` | Number of frames displayed per second | `60` |
| `CELL_SIZE` | Cell dimensions, in pixels | `10` |
| `INFECTION_RATE` | Probability that a healthy cell is infected by an adjacent infected cell | `0.1` |
| `FATALITY_RATE` | Probability that an infected cell dies | `0.05` |
| `RECOVERY_TIME` | Average time to recovery, in frames | `5` |
| `IMMUNITY_RATE` | Probability that a recovered cell becomes immune | `0.2` |
| `INFECTED_RATE` | Initial rate of infected cells | `0.001` |
| `VACCINATED_RATE` | Initial rate of vaccinated cells, considered immune | `0.01` |

The values in the Example column are the ones set in the repository.

## Running locally

```bash
python main.py
```

The simulation runs in a Pygame window. Once it ends or the window is closed, a Matplotlib window shows the curves.

## License

This project is licensed under the [MIT License](LICENSE).
