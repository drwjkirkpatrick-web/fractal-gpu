# 🔥 Fractal GPU Explorer

A browser-based fractal renderer that uses **WebGL fragment shaders** for GPU-accelerated rendering. Every pixel is computed independently on the GPU in parallel — enabling smooth real-time exploration of fractals at deep zoom levels.

## Features

- **45 fractal types** with dynamic shader generation:
  - Mandelbrot Set, Julia Set, Burning Ship
  - Tricorn (Mandelbar), Multibrot (zⁿ + c)
  - Phoenix, Celtic, Perpendicular Burning Ship
  - C-Squared, Sine Mandelbrot, Cosine Mandelbrot
  - Exp Mandelbrot, Buffalo, Rational (z² + c/z), Tan Mandelbrot
  - Newton (z³ − 1), Nova, Absolute C, Manowar
  - Lambda, Ducks, Perp. Celtic, Sin Z² + C
  - Cubic (z³ + c), Rational z² + c/z²
  - Spider, Z² + 1/C, Z² × C, Quartic
  - Quintic, Mandelbar Julia, Z² + C³, Z² + Re(C)
  - 1/(Z²+C), Bicorn
  - **Heart Mandelbrot**, **Z² − C**, **Z³ − C**, **Log**
  - **Asin**, **Cube Tricorn**, **Magnet Type I**, **Collatz**
  - **Sqrt Mandelbrot**, **Z·C + Z²**
- **6 color palettes**: Cosmic, Fire, Ocean, Electric, Forest, Grayscale
- **Smooth coloring** using renormalized escape time (no banding artifacts)
- **Interactive zoom & pan**: mouse wheel zoom toward cursor, drag to pan, touch support
- **Fractal-specific parameter controls**: Julia constant, Multibrot exponent, Phoenix parameter
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
| Switch fractal | `1`–`0` (first 10 types) |

## How It Works

The renderer uses dynamic shader generation: when you select a fractal type, a focused fragment shader containing only that formula is compiled at runtime. This avoids the performance penalty of a single static shader with 100 `if/else` branches, keeping GPU utilization high even as the formula collection grows toward 100 fractals.

A full-screen quad drawn via a single WebGL triangle strip triggers the fragment shader, which runs for every pixel on screen in parallel. Each pixel maps to a point in the complex plane, and the fractal formula is iterated until either escape (|z| > 16) or the maximum iteration count is reached.

**Smooth coloring** uses the renormalized escape-time formula:

```
μ = i + 1 − log(log(|z|)) / log(2)
```

This produces continuous color gradients instead of the discrete bands seen with integer iteration counts.

## Tech

- Pure WebGL 1.0 + GLSL ES 1.00
- Dynamic runtime shader compilation per fractal formula
- No libraries, no build step, no dependencies
- Single self-contained HTML file

## License

MIT
