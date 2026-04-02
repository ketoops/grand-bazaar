# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Grand Bazaar is an idle/incremental trade empire game (inspired by Idle Planet Miner) built as a single-page HTML5 + JavaScript app. The user is a non-programmer who tests in Chrome DevTools device mode and Safari on iPhone. All code is written by Claude.

## Architecture

The entire game lives in **two files**:
- **`game.html`** (~4400 lines) — The playable game. Contains CSS, HTML, and all JS in a single file. No frameworks, no build step, no modules.
- **`index.html`** (~2300 lines) — A design board / mockup document (not the game itself).
- **`DESIGN.md`** — Game design document with zone data, recipes, mechanics, and roadmap.

### game.html Structure (top to bottom)

1. **CSS** (lines ~7–1050) — All styles, including dark/light theme via CSS variables on `:root[data-theme]`
2. **HTML** (lines ~1050–1260) — Screen containers: map, zone detail, bazaar, crafting, prestige, scouting, global upgrades, stats, achievements
3. **`<script>`** (lines ~1260–end) — All game logic in plain JS (no classes, `var`-based, `forEach` callbacks):
   - **Data tables** (~1265–1800): `ZONES[]` (20 zones across 5 rings), `CRAFT_RECIPES[]`, `SCOUTING_MAPS[]`, `GLOBAL_UPGRADES[]`, `PRESTIGE_MILESTONES[]`, `PRESTIGE_UPGRADES[]`
   - **Game state** (`G` object, ~1800–1845): created by `createFreshState()`, holds crowns, zones, bazaar, craft slots, prestige data
   - **Save/Load** (~1930–2025): `saveGame()` / `loadGame()` via localStorage key `grandBazaarSave`, auto-save every 5s
   - **Math helpers** (~2029–2195): `upgradeCost()`, `getZoneProductionRate()`, `getCaravanSpeed()`, `getCargoCapacity()`, `calcPrestigeSeals()`, etc.
   - **Game tick** (~2201): `tick()` — runs every 100ms, handles production, caravan transport, storage
   - **Crafting logic** (~2273–2415): timer-based crafting, auto-craft, craft queue
   - **Scouting logic** (~2417–2535): map discovery system
   - **Bazaar/selling** (~2538–2645): resource selling with percentage slider, sell-all, auto-sell
   - **Upgrades & prestige** (~2647–2775): zone upgrades (5 types), global upgrades, prestige reset
   - **Render functions** (~2973–3700): `renderHUD()`, `renderMap()`, `renderBazaar()`, `renderCraft()`, `renderPrestige()`, etc.
   - **Map system** (~3778–4230): pannable/zoomable map with zone nodes, caravan animations, particle effects
   - **God mode** (~4331–4360): debug cheats (`toggleGodMode()`, give crowns/seals/resources)

### Key Patterns

- **Global state object `G`**: All mutable game state. Modified directly by game functions.
- **Zone upgrade cost formula**: `upgradeCost(unlockCost, _, level)` uses quadratic scaling: `base * (1 + level * 0.15) * (1.12 ^ level)`. Defined once, used for all 5 upgrade types.
- **Production math**: IPM-style quadratic formulas. Each zone has base rates; upgrades multiply via `getZoneProductionRate()`, `getCaravanSpeed()`, `getCargoCapacity()`.
- **Screens**: Shown/hidden via `showScreen(id)` toggling `display:none`. No routing.
- **No build system**: Open `game.html` directly in a browser. No `npm`, no bundler, no server needed.

## Development & Testing

- **Run**: Open `game.html` in any browser. Use Chrome DevTools device mode for mobile simulation.
- **Debug**: Toggle god mode in-game (or call `toggleGodMode()` in console) for instant crowns/seals/resources.
- **Save**: Game auto-saves to localStorage every 5s. Call `wipeSave()` in console to reset.
- **No tests**: There is no test suite. Testing is manual in-browser.

## Math Model (Critical)

All zone balancing uses the IPM quadratic formulas defined in the math helpers section. When adding new zones or rebalancing, use `upgradeCost()` and the existing getter functions — do not introduce new formulas. See `project_math_model.md` in memory for the full specification.

## Important Conventions

- All code uses `var` (not `let`/`const`) and `function` declarations (not arrow functions) for consistency with the existing codebase.
- Zone data in `ZONES[]` includes map positioning (`x`, `y`, `ring`), visual data (`icon`, `color`), and game data (`resources`, `unlockCost`). All 20 zones are defined even if not yet discoverable.
- Prestige reset (`resetForPrestige()`) wipes crowns, zones, upgrades, resources, and discovered zones but preserves Legacy Seals and prestige upgrades.
- The game has both dark and light themes via CSS variables.
