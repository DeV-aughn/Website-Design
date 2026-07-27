# AURUM & NOIR — The Eclipse

**The Product.** An award-style cinematic "3D scroll" website for a fictional Swiss luxury
watch brand launching its tourbillon chronograph, the *Eclipse*.

Scrolling drives everything: a 360° hero orbit scrubbed as a canvas frame sequence, a macro
fly-through of the dial, an exploded engineering view with spec callouts, an atmosphere
interlude (black marble, smoke, a single spotlight) behind the *Edition of 88* reveal, and a
private waitlist.

## Run it

```bash
python -m http.server 8801
```

Open http://localhost:8801. No build step, no dependencies — one HTML file plus frames.

## How it works

- **Scroll-scrubbed video** — each clip is pre-extracted to 96 JPEG frames, preloaded, and
  drawn to a sticky full-viewport canvas mapped to scroll position (the Apple product-page
  technique).
- **Smoothness without wheel hijacking** — the page scrolls natively; a lerped shadow value
  chases the real scroll position each animation frame and all visuals render from it. Wheel
  input can never be swallowed by a scroll library, but the scrub still glides.
- **Everything else** — pinned captions, count-up spec callouts, staged story reveals, gold
  dust particles, pill-morphing nav, `prefers-reduced-motion` support, mobile layout.

## Asset pipeline (100% local)

All imagery was generated on-machine through [WanGP](https://github.com/deepbeepmeep/Wan2GP)
driven over its MCP server:

| Asset | Model |
|---|---|
| Hero product shot | Krea 2 raw (image) |
| Orbit / macro / assembly clips | LTX-2 2.3 Distilled 1.1 22B (image-to-video) |
| Atmosphere still | Qwen Image Edit Plus 2 (scene recomposition) |
| Upscaling | FlashVSR ×2 via WanGP postprocessing |

Dial typography follows the rule: diffusion makes pixels, code makes type.

*Fictional brand. All product imagery AI-generated. Made with WanGP.*
