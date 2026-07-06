# AI Fractals App — 3D / 4D Fractal Explorer

A single-file HTML app that renders **3D and 4D fractals in real time** with WebGL raymarching, inspired by the famous **Mandelbulb3D** desktop application. It includes full lighting (soft shadows, refraction, ambient occlusion, fog) and a **live sound synthesizer driven by the fractal itself**.

**Just open `index.html` in any modern browser.** No build step, no dependencies.

## Fractal formulas

| Mode | Formula |
|---|---|
| Mandelbulb (power) | White–Nylander triplex power formula `z → zⁿ + c`, adjustable power 2–12 |
| Juliabulb (3D Julia) | Same power formula with a fixed Julia constant `(Cx, Cy, Cz)` |
| Quaternion Julia (4D) | True 4-dimensional `z → z² + c` in quaternion space, sliced into 3D by the **4D Slice (w)** slider — animate it to morph through the 4th dimension |
| Tetra Fold (Sierpinski) | Tetrahedral folding IFS (Sierpinski tetrahedron) with adjustable fold scale |
| TetraFold × Power hybrid | Mandelbulb3D-style hybrid: each iteration applies the tetrahedral fold, then the triplex power step |

## Rendering features (Mandelbulb3D-inspired)

- **Distance-estimator raymarching** with per-formula analytic DE
- **Color pickers** — base, orbit-trap palette, glow, background, fog; palette shift & mix controls
- **Lighting** — positionable colored key light (azimuth/elevation), intensity, specular highlights
- **Soft shadows** — penumbra shadow marching with adjustable strength & softness
- **Refraction** — view rays are refracted through the surface (adjustable amount and index of refraction, with total-internal-reflection fallback) blended with Fresnel reflection
- **Ambient occlusion** and **rim glow**
- **Fog** — exponential-squared distance fog with its own color, plus volumetric-style surface glow

## Live fractal-driven sound

The synthesizer (Web Audio API) doesn't just play a drone — it **probes the fractal's distance field on the CPU every frame**, mirroring the exact shader formulas:

- **Surface distance** at the probe point → low-pass filter cutoff (flying close to the fractal opens the sound up)
- **Orbit trap** value → harmonic detune / shimmer
- **Fractal power** → the musical interval between voices
- **Iteration count** → LFO wobble rate
- **Camera azimuth** → stereo panning

Change any fractal parameter or move the camera and the sound follows in real time. Controls: volume, base pitch, harmonic richness, reactivity.

## Controls

- **Drag** to orbit the camera, **scroll** to zoom
- Resolution presets (Low → Ultra), field of view, auto-rotate
- `☰` button hides the panel for full-screen viewing
