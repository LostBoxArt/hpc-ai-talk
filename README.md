# AI Agents in HPC Environments

A self-contained, single-file HTML presentation for a **45-minute technical talk**
on how modern AI agents — LLMs plus tools plus memory plus a reasoning loop —
can actually be useful inside an HPC environment, delivered entirely on
**on-prem hardware** (2× A100 40 GB, Qwen3-class model, vLLM or SGLang).

> **Live deck:** once GitHub Pages is enabled on this repo (see below),
> the deck is viewable directly at
> **https://lostboxart.github.io/hpc-ai-talk/**.
> Until then, clone and open [`index.html`](./index.html) in any modern browser.

---

## What this is

The whole presentation — every slide, every SVG icon, every CSS animation,
every line of JavaScript — lives in a single ~300 KB HTML file. No build
step. No CDN. No dependencies. No libraries. Not even Three.js. Open
`index.html` in a browser and it runs offline.

The deck is aimed at **HPC engineers, sysadmins, and researchers** who have
heard about "AI agents" but aren't sure what that actually means for their
cluster, their on-call rotation, or their users — and who want an honest
look at where agents help, where they don't, and what deploying them on
hardware they already own actually looks like.

## What it covers (main deck, ~26 slides)

A progressive path from concepts to a live demo to on-prem reality:

| Section | Time | Content |
| --- | --- | --- |
| 01 — Introduction | 5 min | HPC context, why agents matter now |
| 02 — What is an AI agent? | 8 min | Definitions, scripts vs. automation vs. agents, taxonomy |
| 03 — How agents work | 8 min | LLM loops, tool use, memory, planning |
| 04 — Agents in HPC | 8 min | Scheduling, monitoring, troubleshooting |
| 05 — Live demo | 6 min | "Why is my GPU job pending?" walkthrough |
| 06 — On-prem deployment | 5 min | 2× A100, Qwen3.6, self-improving, swappable brain |
| 07 — Summary & future | 5 min | Honest limits, what's next |

### The on-prem thesis

A core argument of the talk is that you don't need to send your HPC
telemetry to a managed API to get useful agent behavior. The deck argues
for running a frontier open-weights model (Qwen3-class, 35B total / ~3B
active MoE, FP8 / AWQ-4bit) on two A100 40 GB GPUs you already own,
served with vLLM (≥ 0.19) or SGLang (≥ 0.5.10). Empirically that gets you
roughly **9–14 concurrent sessions, ~1,100 total tok/s, 25–30 tok/s per
user** on moderate context lengths — at a marginal cost that is
essentially the cost of the power cable.

## Three "sidebar" side-tracks from slide 1

Each is a fully independent 5-slide detour branch, with its own navigation
chrome and palette, that you can skip into and out of without affecting the
main deck. They exist so the talk can adapt on the fly depending on how
much the room already knows.

| Sidebar | Palette | Point |
| --- | --- | --- |
| **New to LLMs?** | cyan / teal | A 5-page primer: what an LLM actually is — tokens, pre-training, fine-tuning, autoregressive generation, context windows, attention. |
| **What's a harness?** | amber / rose | Why modern dev work has moved from copy-pasting chat output into a harness (Cursor, Claude Code, Codex, Aider, OpenHands, goose, Continue, Pi-style CLIs) — and what that implies for HPC. |
| **Show & tell** | violet / fuchsia | Three **live interactive demos** of what SOTA models can do in a browser, all implemented in-file with no libraries: <ol><li>A **draggable 3D lattice** — pure Canvas projection math, 27 nodes, 54 edges, depth-sorted, lit via radial gradients, idle-rotating, with momentum after drag release.</li><li>A **live force-directed graph generator** — click *Regenerate* and a fresh random knowledge graph settles in real time via repulsion + spring-edge + damped physics. Four themes (HPC stack, Agent anatomy, On-prem ops, Dev harness).</li><li>A **typewriter-then-execute code panel** — pick a prompt, watch the code "type out" with live syntax highlighting, then watch that exact source get `eval`'d into the preview canvas. Three demos: spiral, interfering sine waves, three-body orbital sim.</li></ol> |

Opening any sidebar closes the other two. Escape returns to the main talk.

## Presenter controls

| Key | Action |
| --- | --- |
| `→` / `space` / `PageDown` | Next slide |
| `←` / `PageUp` | Previous slide |
| `Home` / `End` | First / last slide |
| `O` | Overview (grid of all slides, click any to jump) |
| `S` | Speaker notes overlay |
| `T` | Talk timer (start / pause, does not reset) |
| `F` | Toggle fullscreen |
| `?` | Keyboard shortcut help |
| `Esc` | Exit any overlay or sidebar |
| `#N` in URL | Deep-link to slide N |

Touch/swipe works on tablets. Print (`⌘P`) hides sidebars and overlays
and produces one page per slide.

## Running it

Any of these:

```bash
# The simple way — just open the file
open index.html                               # macOS
xdg-open index.html                           # Linux
start index.html                              # Windows

# Or serve it locally (nice for the #N hash links)
python3 -m http.server 8000                   # then http://localhost:8000/
```

## Publishing with GitHub Pages

This repo is structured so Pages works with zero configuration — the
presentation is at `index.html` in the repo root.

1. Go to **Settings → Pages** on this repo.
2. Under *Build and deployment → Source*, pick **Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Save.
4. In ~30 seconds the deck is live at
   **https://lostboxart.github.io/hpc-ai-talk/**.

## Design constraints

The deck deliberately obeys a set of rules that make it portable to
offline demo environments (conference rooms with no WiFi, air-gapped
government HPC sites, airplane wifi, etc.):

- **Single HTML file.** Everything ships inline: CSS, JavaScript, SVG
  icons, fonts via system stacks, animations, 3D math, physics.
- **No external dependencies.** No Three.js, D3, React, jQuery, syntax
  highlighter, icon pack, web font, image, or CDN. Nothing is downloaded
  when the file is opened.
- **Pure web platform.** CSS custom properties, `clamp()`, `color-mix()`,
  `grid`, `flex`, `aspect-ratio`, `prefers-reduced-motion`, keyframe and
  `requestAnimationFrame` animations.
- **Demos are lazy and polite.** The three "Show & tell" demos initialize
  only the first time the sidebar opens, and their animation loops gate
  on `slide.classList.contains('active')` so they spend zero CPU while
  the main talk is in front of the audience.
- **Accessible.** ARIA roles on overlays, focus management on open/close,
  keyboard nav first, `:focus-visible` rings, motion reductions honored.
- **Responsive** down to ~900 px viewports.

## Repo layout

```
hpc-ai-talk/
├── index.html   the entire presentation (~300 KB, ~5,900 lines)
├── README.md    this file
└── .gitignore
```

## Credits

Written by **Dennis B** (`@LostBoxArt`) for a public talk.

The deck itself was built in a coding harness — the same class of tool
the "What's a harness?" sidebar describes — as a meta-demonstration of
the thesis being argued.

## License

All rights reserved unless and until a `LICENSE` file is added.
If you'd like to use, remix, or present (parts of) this deck, open an
issue first.
