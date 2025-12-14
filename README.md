# 🎮 Idol Guardians: Eternal Wilds

**A semi-procedural, pet capture, extraction RPG experience on Roblox with endless progression, coop PvE, high-risk PvPvE, base automation, and deep pet evolution.**

---

## 🚀 Overview

**Idol Guardians: Eternal Wilds** is an ambitious Roblox game that blends:

- Open world exploration
- Pet capture & evolution
- Semi-procedural map generation
- High-intensity PvE and PvPvE
- Base building & automation
- Endless progression loops
- Trading & social mechanics
- Competitive leaderboards

This experience is **deliberately infinite** — there’s *always a higher wave, rarer pet, stronger build and deeper challenge* to chase.

---

## 🎯 Core Player Fantasy

> *“Enter a living wild world full of powerful creatures, capture unique companions, build up your base, and become unstoppable — but be careful, other players lurk in the shadows.”*

Players will feel:
- Tension (risk extraction)
- Reward (rare pets & loot)
- Growth (infinite progression)
- Social (co-op, trade, leaderboards)
- Competition (PvPvE & seasons)

---

## 🌍 World & Map System

The game world is **semi-procedurally generated** on every expedition:

### 🌐 World Rules
- Base is always at the center
- Difficulty scales with distance from base
- Biomes are placed using weighted randomness
- Rare biomes appear farther out
- Dungeons and themed regions appear randomly
- Each run has unique zone placement

### 🧱 Biome Types
Each biome hosts its own:
- Enemy pools
- Environmental hazards
- Resource types
- Pet ecosystem

Examples include:
| Biome | Element | Focus |
|-------|---------|-------|
| Forest | Nature | Balanced enemies |
| Stone Wastes | Stone | Defensive mobs |
| Volcanic Rift | Fire | Aggressive foes |
| Marshlands | Water | Healing hazards |
| Storm Plateau | Lightning | Fast enemies |
| Sky Ruins | Air | Mobility challenges |
| Void Scar | Void | Ultra-rare encounters |

---

## 🐾 Pet System

Pets are your companions and progression engines:

### 📊 Pet Attributes
Each pet has:
- Rarity Tier (Common → Unique)
- Elemental Affinity (Fire, Water, Air, etc.)
- Star Level ★☆☆☆☆ → ★★★★★
- Infinite levels
- Evolving skill trees

### ✨ Rarity Tiers
| Tier | Meaning |
|------|---------|
| Common | Most frequent |
| Uncommon | Slightly rarer |
| Rare | Noticeable challenge |
| Epic | Harder to find |
| Legendary | Highly sought |
| Mythic | Very rare |
| Unique | Ultra-rare / seasonal |

### 🌟 Star System
Pets are ranked by stars:
- Merge identical pets to increase stars
- Stars unlock deeper skill nodes and scaling multipliers

---

## 🧠 Skill Trees & Evolution

Each pet has a massive skill tree with:
- Core branch (identity)
- Elemental branch
- Utility branch
- Mutation branch

Skill trees do *not* have finite caps — they expand as pets level.

---

## 🎯 Capture System

Inspired by extraction games (like *Palworld*):

1) You encounter a roaming boss pet
2) You battle waves of minions
3) Pet is weakened
4) You attempt capture

💥 Capture odds depend on:
- Pet HP & rarity
- Capture tool tier
- Player skill
- Companion bonuses

If capture fails:
- The pet escapes
- A loot chest spawns with resources or lower-tier pets

No fight is ever wasted.

---

## 🧱 Inventory & Extraction Mechanics

### 🧳 Inventory Limits
Players start with limited:
- Held items
- Pet cargo slots

These expand as you level and upgrade your base.

### 📦 Extraction
Captured pets become cargo:
- Slow player movement
- Increase aggro and danger
- Trigger roaming threats

Extraction success requires:
- Route planning
- Avoiding stronger enemies
- Time management under pressure

Death results in:
- Loss of pets in cargo
- Loss of held items
- Partial retention of base rewards

---

## 🏠 Base System

Players own a persistent home base with upgradable facilities:

| Building | Function |
|----------|----------|
| Storage Vault | Increase pet slots |
| Training Grounds | Passive pet XP gain |
| Capture Lab | Improves capture efficiency |
| Money Generators | Assign pets to generate currency |
| Armorsmith | Gear improvements |
| Weaponsmith | Weapon mods |
| Breeding Hall | Pet breeding & hybrids |
| Trading Hall | Auction house & player trade |

Bases evolve with player growth and resources.

---

## 💰 Economy & Rewards

### Currency Types
- **Glow Cash** – main in-game currency
- **Hype Crystals** – rare upgrade tokens
- **Encore Tokens** – prestige resets
- **Star Shards** – premium / event currency

### Scaling & Progression
Currency rewards scale exponentially with:
- Depth reached
- Pet rarity defeated
- PvPvE wins
- Seasonal milestones

---

## 🤝 Co-Op PvE Expeditions

Players can team up into squads:
- Share loot via roll system (need/pass)
- Coordinate capture and extraction
- Combined pet synergies
- Shared world threats and rewards

---

## ⚔️ PvPvE Mode (High Risk vs. High Reward)

A unique competitive mode where:
- Players can engage others who are extracting loot
- PvP is resolved via **companion pet duels**
- Attacker must defeat defender’s active pet
- The victor claims carried loot
- Balance systems prevent abuse

### PvP Protection Rules
✔ Level bracket scaling  
✔ No loot = unattackable  
✔ PvP stakes (attacker must risk resource)  
✔ Safe zone near extraction gates  
✔ Anti-camping reveal mechanics  

---

## 📊 Leaderboards & Seasons

Leaderboards track:
- Max expedition depth
- Currency per second
- Rarest pets
- PvPvE wins
- Group rank

Seasons reset:
- Leaderboards
- Seasonal pets
- Mutation modifiers
- Special events

---

## 🧠 Player Retention & Psychology

The game maximizes:
- Big number rewards
- Progression guarantees
- Collection obsession
- Social competitiveness
- High-stakes extractions
- PvPvE risk/reward tension

All systems are designed to push the player back for “just one more run.”

---

## 🛠 Technical Architecture

### Core Services (Server)
- `WorldGeneratorService`
- `BiomeService`
- `PetService`
- `CaptureService`
- `PvPvEService`
- `InventoryService`
- `EconomyService`
- `LeaderboardService`
- `BaseManagementService`

### Shared Modules
- `PetDefinitions`
- `BiomeDefinitions`
- `Config`
- `Utils`

### Client
- UI handlers
- Player controllers
- Feedback & effects

---

## 💻 Dev Tools & Workflow

### Required Tools
- **Roblox Studio**
- **Visual Studio Code**
- **GitHub Desktop**
- **Rojo CLI**
- **Roblox Rojo plugin**
- **Aftman** (tool installer)

### Optional Tools
- **Blender** (assets/models)
- **Audacity** (audio)
- **Figma/Adobe XD** (UI design)
- **Google Sheets** (balance and scaling)

---

## 📁 Repo Structure (Rojo + Git)
/
├─ src/
│ ├─ Server/
│ │ ├─ Services/
│ │ │ ├─ WorldGeneratorService.lua
│ │ │ └─ ...
│ │ └─ ServerMain.server.lua
│ ├─ Shared/
│ │ ├─ BiomeDefinitions.lua
│ │ └─ ...
│ └─ Client/
│ └─ ClientMain.client.lua
├─ default.project.json
├─ aftman.toml
├─ .gitignore
├─ README.md


---

## 🧪 Getting Started (Quick Setup)

1) Clone the repo  
2) Run:
   ```bash
   aftman install
   rojo serve default.project.json


Open Roblox Studio

Connect Rojo plugin

Begin coding

📌 Development Roadmap
Phase 1 – Core

World generation

Pet encounters

Base capture system

Inventory limits

Phase 2 – Progression

Pet skill trees

Star leveling

Base automation

Phase 3 – PvPvE

Duel mechanics

Leaderboards

Trading economy

Seasonal content

🧾 Contribution & Support

Everyone is welcome to contribute!
Please follow the project’s code standards and branching model in the CONTRIBUTING.md file (to be created).

🏁 License

This project is open source (as determined by the GitHub repo’s license).

❤️ Thank You!

Thanks for checking out Idol Guardians: Eternal Wilds — a deep, evolving, endless adventure on Roblox.
