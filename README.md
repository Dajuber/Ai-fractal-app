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

## `fractal-ai-test2.html` — Hybrid Fusion Explorer

The second experiment expands the formula library to **10 formulas** and adds Mandelbulb3D-style **formula fusion**:

- **Formulas**: Mandelbulb (sine & cosine variants), Quaternion z²+c (4D), Bristorbrot, Tetra fold (Sierpinski), Menger sponge fold, Mandelbox (Amazing Box), rotated Kaleido-IFS, Octahedron fold, Sphere-fold scale (Amazing-Surf style)
- **3 formula slots with repeat counts** — in *Interleave* mode the iteration loop cycles through the slots exactly like Mandelbulb3D hybrids (e.g. 2× Menger fold, then 1× bulb power, repeat)
- **4 more fusion modes** that combine the finished distance fields of slots 1 and 2: **Morph blend** (lerp between two fractals), **Smooth union** (weld), **Intersection**, and **Difference** (carve B out of A)
- Adaptive distance-estimator blending per formula class (escape-time / IFS / box-fold) plus a **Step detail** slider (MB3D's raystep multiplier) to trade speed for hole-free surfaces
- Julia mode with a 4D constant, animatable 4D slice, and **8 curated presets** (Menger × Bulb, Mandelbox, Quaternion × Tetra 4D, Bristorbrot × KIFS, morph/weld/carve demos…)
- Same lighting, refraction, shadows, fog, and **live fractal-driven sound** engine — the synth probes the *fused* field, so it hears the hybrid

## `fractal-ai-test3.html` — Navigator Edition

The third experiment adds on-screen flight controls and grows the library to **16 formulas**:

- **3D navigation pad** (bottom-right corner): a virtual joystick that flies the camera through the horizontal view plane, ▲/▼ buttons for vertical movement, a ⌂ re-center button, and a **vertical zoom/dezoom slider** (log scale, synced with the mouse wheel)
- **6 new formulas**: Quaternion z³+c (4D), Buffalo bulb (abs), Amazing Surf (xy box fold), Cube fold (Cantor), plus two Mandelbulb3D-style *transforms* — **Twist** and **Sphere inversion** — that warp any hybrid they're interleaved into
- **New parameters**: bailout, fold offset, sphere-fold radius, twist amount, inversion radius, and a surface-detail control
- **13 presets** including Amazing Surf, Buffalo Bulb, Quaternion cube, Twisted Menger, and the negative-scale Inverted Mandelbox

## Controls

- **Drag** to orbit the camera, **scroll** to zoom
- Resolution presets (Low → Ultra), field of view, auto-rotate
- `☰` button hides the panel for full-screen viewing
