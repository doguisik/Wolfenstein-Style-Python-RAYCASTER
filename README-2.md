# From-Scratch 2.5D Raycasting Engine

A Wolfenstein 3D / DOOM–inspired raycasting engine built entirely from scratch in Python — including hand-written sine, cosine, and square root functions (no `math` module). Rendering is accelerated with NumPy, windowing/input use `tkinter`, and textures use Pillow.

Built for the *Principles of Programming* course by Layan Imseeh, Dogu Isik, and Yousef Aicha (April 2026).

## Features

- Textured walls, floors, and ceilings
- Billboarded NPC sprites with a Z-buffer for correct occlusion
- Distance-based lighting and fog
- Mini-map overlay and FPS counter
- Weapon/hand sprite with bobbing animation
- Procedurally generated textures when no image assets are found
- Hand-implemented `sin`, `cos` (Maclaurin series) and `sqrt` (Newton–Raphson), with both scalar and vectorized (NumPy) versions

## How it works

The player is modeled as a camera with a position, direction vector, and camera plane. For every screen column, a ray is cast into a 2D tile-based map and stepped through the grid using the **DDA (Digital Differential Analysis)** algorithm. The perpendicular distance to the nearest wall is used (to avoid fisheye distortion) to compute wall slice height, texture offset, lighting, and fog. Floors, ceilings, and sprites are rendered using vectorized NumPy operations rather than per-pixel Python loops.

Full technical write-up, including the math derivations and performance benchmarks, is in [`RAYCASTER_REPORT_FINAL.pdf`](./RAYCASTER_REPORT_FINAL.pdf).

## Performance

Measured at 640×400 pixels on a standard laptop: ~11ms per frame (~90 fps ceiling), with the engine running at roughly 40–60 fps at 640×400 and up to 120 fps at 320×200.

## Requirements

- Python 3.x
- `numpy`
- `Pillow`
- `tkinter` (usually bundled with Python)

```bash
pip install numpy pillow
```

## Usage

Open and run `Raycaster.ipynb` in Jupyter:

```bash
jupyter notebook Raycaster.ipynb
```

Controls: **WASD** / **Arrow keys** to move and look, **Q** to quit.

## Limitations

The engine is built on a flat 2D grid, so it cannot support multiple floors, varying ceiling heights, or stacked rooms. Sprites are not affected by lighting or fog. The per-column wall-drawing loop remains the main performance bottleneck.

## References

- Lodev, L. (2004). *Raycasting Tutorial.* https://lodev.org/cgtutor/raycasting.html
- Abramowitz, M. & Stegun, I. A. (1972). *Handbook of Mathematical Functions.* Dover Publications.
- id Software (1993). *DOOM source code release.* https://github.com/id-Software/DOOM

## License

This project is licensed under the MIT License — see [LICENSE](./LICENSE) for details.
