# Grand Bazaar — Game Design Document

**Version:** 1.1  
**Last Updated:** 2026-04-01  
**Status:** Playable Prototype (Mockup)  
**Platform:** Mobile / Tablet (iOS + Android)  
**Tech Stack:** HTML5 + JavaScript + Capacitor  

---

## Game Concept

Grand Bazaar is an idle/incremental trade empire game inspired by **Idle Planet Miner**, re-themed from sci-fi to a historical trade setting.

The player manages trade zones (forests, farms, mines, ancient cities) that produce resources. Resources are carried by **caravans** to the **Grand Bazaar** — a central marketplace where the player sells them for **Crowns** (main currency). The player expands their empire by unlocking new zones, upgrading production, crafting advanced goods, and eventually resetting the world for **Legacy Seals** (prestige currency) to earn permanent upgrades.

**Core Fantasy:** Build a thriving trade empire across historical civilizations.

---

## Core Mechanics

### 1. Resource Production (Idle)
- Zones produce resources automatically 24/7, even when the app is closed
- No tap-to-collect — fully idle production
- Each zone has 2 resources with different yields and base rates
- Production increases via zone upgrades

### 2. Caravan Transport
- Resources don't teleport — **caravans** carry them from zones to Grand Bazaar
- Each zone starts with 1 caravan, upgradeable to max 5
- Caravans have 3 properties: Speed, Cargo capacity, Count
- Caravan types vary by zone: horses (European), camels (desert), boats (coastal)
- Multiple caravans operate independently on the same route

### 3. Grand Bazaar (Selling)
- Resources accumulate at the Bazaar after caravans deliver them
- Player sells resources individually with a percentage slider (25%/50%/75%/100%)
- Sell All option available as secondary action
- Sell prices are fixed per resource + multiplied by prestige upgrades

### 4. Crafting
- Combine raw resources into higher-value crafted goods
- Timer-based: each recipe takes time (5s to 480s)
- 1 craft slot at start, max 3 (unlock via crafts or upgrades)
- **Craft 1** (manual) or **Auto-Craft** (toggle, repeats while resources available)
- Crafted goods can be sold at Grand Bazaar for premium prices
- Some crafted items are utility items (Maps for Scouting)

### 5. Scouting & Zone Discovery
- New zones beyond the starter 3 are **hidden** by default
- To discover zones, the player must:
  1. **Craft a Map** (e.g., Map Lv1 requires Tools + Provisions + Scout Kits)
  2. **Open Scouting screen** and use the Map
  3. **Zones are instantly discovered** and appear on the world map
  4. **Pay Crowns for diplomacy** to establish a trade deal and unlock the zone
- Map Lv1 discovers 3 zones (Athenai, Roma, Alexandria)
- Map Lv2-4 will discover more advanced zones (future content)
- On prestige reset, all scouted zones **revert to hidden** — Maps must be crafted again

### 6. Zone Upgrades (5 per zone)
| Upgrade | Effect | Scaling |
|---------|--------|---------|
| Production Rate | Increase resource output | ×1.45 to ×1.60 |
| Caravan Speed | Faster delivery to Bazaar | ×1.45 to ×1.60 |
| Cargo | More resources per trip | ×1.45 to ×1.60 |
| Multi-Harvest | +1% double harvest chance (cap Lv25) | ×1.55 |
| Extra Caravan | +1 caravan on route (cap Lv4, max 5) | ×2.20 |

### 7. Prestige System
- **Milestones:** 6 tiers (25K, 50K, 100K, 250K, 500K, 1M Crowns)
- Progress bar visible on HUD at all times
- At any reached milestone, player can **Reset World** to earn **Legacy Seals**
- Reset wipes: Crowns, zones, upgrades, resources, crafted items, discovered zones
- Persists: Legacy Seals, prestige upgrades, cosmetics, achievements
- Each run is faster due to accumulated prestige upgrades

### 8. Prestige Upgrades (10 available)
| Upgrade | Effect | Cost |
|---------|--------|------|
| Starting Crowns | +1,000 starting Crowns | 1 Seal |
| Production Boost | +25% all production | 2 Seals |
| Better Prices | +15% all sell prices | 2 Seals |
| Quick Start | Start with Fermă unlocked | 3 Seals |
| Offline Boost | 2x offline earnings | 3 Seals |
| Auto-Sell Permanent | Auto-sell persists on reset | 4 Seals |
| Crown Magnet | +50% Crowns from sales | 5 Seals |
| Zone Rush | -30% zone unlock costs | 5 Seals |
| Legacy Trader | +1 bonus Seal per prestige | 8 Seals |
| Grand Merchant | Start with 3 zones unlocked | 10 Seals |

---

## Zones

### Starter Zones (always visible, buy with Crowns)

| Zone | Icon | Resources | Base Income/s | Unlock Cost |
|------|------|-----------|---------------|-------------|
| Pădure (Forest) | 🌲 | Wood (1.0/s, 2🪙) + Food (0.4/s, 3🪙) | 3.2/s | Free |
| Fermă (Farm) | 🌾 | Food (1.2/s, 3🪙) + Wood (0.3/s, 2🪙) | 4.2/s | 500🪙 |
| Mină (Mine) | ⛰️ | Stone (0.6/s, 5🪙) + Iron (0.3/s, 10🪙) | 6.0/s | 2,500🪙 |

### Scoutable Zones (Map Lv1 — requires Scouting)

| Zone | Icon | Resources | Base Income/s | Diplomacy Cost |
|------|------|-----------|---------------|----------------|
| Athenai | 🏛️ | Olive Oil (0.6/s, 20🪙) + Pottery (0.3/s, 28🪙) | 20.4/s | 8,000🪙 |
| Roma | 🏟️ | Wine (0.5/s, 30🪙) + Weapons (0.2/s, 55🪙) | 26.0/s | 25,000🪙 |
| Alexandria | 📜 | Papyrus (0.4/s, 38🪙) + Spices (0.15/s, 70🪙) | 25.7/s | 60,000🪙 |

### Future Zones (Map Lv2-4)
- Constantinople, Venetia, and more TBD

---

## Craft Recipes

### Basic Recipes
| Recipe | Ingredients | Timer | Sell Price |
|--------|------------|-------|-----------|
| Planks | 5 Wood | 5s | 8🪙 |
| Bricks | 8 Stone + 2 Wood | 8s | 18🪙 |
| Tools | 3 Planks + 5 Iron | 15s | 35🪙 |
| Provisions | 10 Food + 3 Wood | 12s | 25🪙 |
| Scout Kit | 2 Tools + 5 Provisions | 30s | 80🪙 |
| Steel Bar | 8 Iron + 3 Stone | 20s | 50🪙 |

### Scouting Maps (not sellable)
| Recipe | Ingredients | Timer | Discovers |
|--------|------------|-------|-----------|
| Map Lv1 | 5 Tools + 10 Provisions + 3 Scout Kits | 60s | Athenai, Roma, Alexandria |
| Map Lv2 | TBD | 120s | Future zones |
| Map Lv3 | TBD | 240s | Future zones |
| Map Lv4 | TBD | 480s | Future zones |

### Advanced Recipes (from new zones)
| Recipe | Ingredients | Timer | Sell Price |
|--------|------------|-------|-----------|
| Olive Press | 5 Olive Oil + 3 Planks | 18s | 45🪙 |
| Scrolls | 8 Papyrus + 2 Tools | 25s | 65🪙 |
| Spiced Wine | 5 Wine + 3 Spices | 22s | 75🪙 |
| War Gear | 3 Weapons + 5 Steel Bar | 35s | 120🪙 |

---

## Monetization Plan (Future)

| Type | Description |
|------|-------------|
| Rewarded Ads | 2x production for 30 min, instant sell bonus, speed up craft timers |
| Premium Currency | Gems — for cosmetics, speed-ups, QoL |
| Cosmetic Themes | Zone skins, caravan skins, UI themes |
| Starter Bundle | Gems + starting Crowns + exclusive cosmetic |
| QoL Upgrades | Permanent auto-sell, 2x offline, remove ads, extra craft slots |

---

## Tech Stack

- **Code:** HTML5 + JavaScript (single file, no frameworks)
- **Packaging:** Capacitor (iOS + Android from same codebase)
- **Graphics:** Emoji + CSS (prototype) → AI art + asset packs (MVP) → Freelancer (launch)
- **Save:** localStorage with auto-save every 5 seconds
- **Testing:** Chrome DevTools device mode + Safari on iPhone via WiFi

---

## File Structure

```
/home/kali/1/
├── game.html        # Playable prototype (all game logic)
├── index.html       # Design board / mockup document
├── DESIGN.md        # This document
├── .gitignore       # Excludes inspiration/
└── inspiration/     # Reference screenshots (not in git)
```

---

## Current State (v1.1)

### Implemented
- 6 zones (3 starter + 3 scoutable)
- 5 upgrades per zone with exponential scaling
- Multi-caravan transport system with visual animation
- Grand Bazaar with per-resource selling and percentage slider
- 14 craft recipes (6 basic + 4 maps + 4 advanced)
- Timer-based crafting with auto-craft toggle
- Scouting system: craft Maps → discover zones → diplomacy unlock
- 3 zone states: hidden, discovered, unlocked
- Prestige milestones (6 tiers) with Legacy Seals
- Prestige upgrades shop (10 upgrades)
- Save/load via localStorage with auto-save
- Wipe save option
- Mobile-responsive phone frame UI

### Not Yet Implemented
- Offline earnings calculation
- Extra craft slot unlocking
- Sound / haptics
- Capacitor mobile build
- Actual monetization (ads, IAP)
- Map Lv2-4 zone content
- Dynamic market demand
- Managers / automation characters
- Achievements
- Settings screen

---

## Roadmap

| Version | Features |
|---------|----------|
| v1.0 ✅ | Core prototype: 3 zones, crafting, prestige, save/load |
| v1.1 ✅ | Scouting system, 3 new zones, map crafting, advanced recipes |
| v1.2 | Extra craft slots, offline earnings, balancing pass |
| v1.3 | Sound, haptics, visual polish |
| v2.0 | Capacitor mobile build, monetization integration |
| v2.1 | Map Lv2-4, more zones (Constantinople, Venetia) |
| v3.0 | Managers, automation, market demand |
