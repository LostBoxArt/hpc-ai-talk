# AI Agents in HPC Environments — Talk

A self-contained HTML presentation for a 45-minute technical talk on
**AI Agents in HPC Environments: Concepts, Architecture, and Practical Use**.

The whole deck is one file: [`ai-agents-hpc-presentation.html`](./ai-agents-hpc-presentation.html).
No build step, no dependencies, no CDN, no external assets — open it in any modern
browser and it runs.

## Running it

```bash
# any of these work:
open ai-agents-hpc-presentation.html          # macOS
xdg-open ai-agents-hpc-presentation.html      # Linux
python3 -m http.server 8000                   # then visit http://localhost:8000/
```

## Contents

The main deck is 26 slides covering:

1. Introduction — HPC context, why agents matter
2. What are AI agents? — definitions, scripts vs. agents, taxonomy
3. How agents work — LLM loops, tools, memory, planning
4. Agents in HPC — scheduling, monitoring, troubleshooting
5. Live demo — "Why is my GPU job pending?"
6. On-prem deployment — 2× A100, Qwen3.6, self-improving, swappable brain
7. Summary & future — takeaways, limits, what's next

### Three "sidebar" side-tracks from slide 1

Each is a fully separate 5-slide detour branch, independent of the main deck:

- **New to LLMs?** — 5-page primer on what an LLM actually is.
- **What's a harness?** — Cursor, Claude Code, Codex, and the shift from
  chat-era to harness-era development.
- **Show & tell** — three live interactive demos that actually run in the
  browser: a hand-rolled 3D lattice (pure Canvas, no Three.js), a live
  force-directed graph generator, and a typewriter-then-execute code demo
  covering a spiral, sine-wave grid, and 3-body orbital simulation.

## Presenter controls

| Key | Action |
| --- | --- |
| `→` / `space` / `PageDown` | Next slide |
| `←` / `PageUp` | Previous slide |
| `Home` / `End` | First / last slide |
| `#N` in URL | Deep-link to slide `N` |
| `O` | Overview (grid of slides) |
| `S` | Speaker notes |
| `T` | Talk timer (start / pause) |
| `F` | Fullscreen |
| `?` | Keyboard shortcut help |
| `Esc` | Exit any overlay / sidebar |

## Design constraints

- Single HTML file, no external dependencies (no Three.js, no CDN, no libraries).
- Pure HTML/CSS/JS. All SVG icons inline. All animations in CSS keyframes or
  `requestAnimationFrame`.
- All three sidebar demos are lazy-initialized and only animate while their
  slide is visible.
- Responsive down to ~900 px; print-friendly (sidebars hidden in print).
