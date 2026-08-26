# 🌌 Fractal GPU Explorer

A browser-based fractal renderer that uses **WebGL fragment shaders** for GPU-accelerated rendering. Every pixel is computed independently on the GPU in parallel — enabling smooth real-time exploration of the Mandelbrot set, Julia sets, and other fractals at deep zoom levels.

## Features

- **5 fractal types**: Mandelbrot, Julia, Burning Ship, Tricorn (Mandelbar), Multibrot (z^n + c)
- **6 color palettes**: Cosmic, Fire, Ocean, Electric, Forest, Grayscale
- **Smooth coloring** using renormalized escape time (no banding artifacts)
- **Interactive zoom & pan**: mouse wheel zoom toward cursor, drag to pan, touch support
- **Julia set parameter control**: adjust the complex constant c in real-time
- **Adjustable iteration depth**: 32 to 2000 iterations
- **Color cycling**: speed and offset controls for palette exploration
- **Screenshot export**: save the current view as PNG
- **Keyboard shortcuts** for fast control
- **Single file, no dependencies**: just open `index.html` in any WebGL-capable browser

## Quick Start

```bash
# No build step required — just open in a browser:
python3 -m http.server 8080
# Then visit http://localhost:8080
```

Or simply double-click `index.html` to open it directly.

## Controls

| Action | Input |
|--------|-------|
| Zoom in/out | Mouse wheel (zooms toward cursor) |
| Pan | Click and drag |
| Toggle panel | `H` |
| Reset view | `R` |
| Save screenshot | `S` |
| Random palette | `Space` |
| Switch fractal | `1`–`5` |

## How It Works

The renderer uses a full-screen quad drawn via a single WebGL triangle strip. A fragment shader runs for every pixel on screen, mapping each pixel to a point in the complex plane and iterating the fractal formula (e.g., z = z² + c for the Mandelbrot set). The GPU's parallel architecture evaluates all pixels simultaneously, making this approach dramatically faster than CPU-based rendering.

**Smooth coloring** uses the renormalized escape-time formula:

```
μ = i + 1 − log(log(|z|)) / log(2)
```

This produces continuous color gradients instead of the discrete bands seen with integer iteration counts.

## Tech

- Pure WebGL 1.0 + GLSL ES 1.00
- No libraries, no build step, no dependencies
- Single self-contained HTML file (~24 KB)

## License

MIT