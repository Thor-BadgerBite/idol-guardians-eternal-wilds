# 🎮 Idol Guardians: Eternal Wilds

**A Skill-Based, Extraction Pet RPG on Roblox**

> Enter a living wild world full of powerful creatures, capture unique companions, build your unstoppable base — but be careful, other players lurk in the shadows.

[![Version](https://img.shields.io/badge/version-1.0.0--alpha-blue.svg)](https://github.com/yourusername/idol-guardians)
[![Status](https://img.shields.io/badge/status-in%20development-yellow.svg)](https://github.com/yourusername/idol-guardians)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](./LICENSE)
[![Roblox](https://img.shields.io/badge/platform-Roblox-red.svg)](https://www.roblox.com)

---

## 📋 Table of Contents

- [What Makes This Different?](#-what-makes-this-different)
- [Overview](#-overview)
- [Core Player Fantasy](#-core-player-fantasy)
- [Combat System](#️-combat-system-unique-mechanic)
- [Pet System](#-pet-system-dual-role)
- [World & Map System](#-world--map-system)
- [Capture System](#-capture-system)
- [Inventory & Extraction](#-inventory--extraction-mechanics)
- [Base Building](#-base-building-system)
- [Co-Op PvE](#-co-op-pve-expeditions)
- [PvPvE Mode](#️-pvpve-mode-high-risk-high-reward)
- [Economy & Rewards](#-economy--rewards)
- [Balance & Progression](#-balance--progression)
- [Leaderboards & Seasons](#-leaderboards--seasons)
- [UI Preview](#-ui-preview)
- [Technical Architecture](#-technical-architecture)
- [Development Tools](#-development-tools--workflow)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Development Roadmap](#-development-roadmap)
- [Documentation](#-documentation)
- [FAQ](#-frequently-asked-questions)
- [Community](#-community)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 What Makes This Different?

### **Unlike Other Roblox Pet Games:**

❌ **NOT** another "click to collect" simulator  
❌ **NOT** pay-to-win gacha mechanics  
❌ **NOT** mindless grinding with no skill expression  
❌ **NOT** generic sword spam combat

### **What We ARE:**

✅ **Skill-Based Timing Combat** (like rhythm games meets Dark Souls parrying)  
✅ **Real Extraction Tension** (Tarkov/Hunt Showdown-style risk/reward)  
✅ **Semi-Procedural Worlds** (every expedition is unique)  
✅ **Fair PvPvE** (anti-grief systems built-in from day 1)  
✅ **Mobile-First Design** (one-tap defense, optimized UI, not a PC port)  
✅ **Infinite Progression** (endless scaling, always something to chase)

### **Target Audience**

| Audience | Age | What They Get |
|----------|-----|---------------|
| **Primary** | 9-16 | Accessible controls, dopamine-rich progression, social play |
| **Secondary** | 17-25 | Deep mechanics, competitive leaderboards, trading economy |
| **Tertiary** | Content Creators | Spectator-friendly combat, hype moments, creator codes |

---

## 🚀 Overview

**Idol Guardians: Eternal Wilds** is an ambitious Roblox experience that blends:

- 🌍 **Open World Exploration** - Semi-procedural maps that never repeat
- 🐾 **Pet Capture & Evolution** - Collect, merge, evolve, and build the ultimate roster
- 🗺️ **Semi-Procedural Generation** - Unique biome layouts every expedition
- ⚔️ **Skill-Based Combat** - Timing > stats, mobile-friendly, spectator-ready
- 🏠 **Base Building & Automation** - Persistent upgrades and passive systems
- ♾️ **Endless Progression** - Infinite levels, infinite skill trees, infinite challenge
- 🤝 **Trading & Social** - Auction house, squad play, social hubs
- 🏆 **Competitive Leaderboards** - Seasonal rankings and PvPvE tournaments

**This experience is deliberately infinite** — there's always a higher wave, rarer pet, stronger build, and deeper challenge to chase.

---

## 🎯 Core Player Fantasy

> **"Enter a dangerous wild world, defeat powerful creatures, capture them as companions, extract them back to your base while surviving threats — and grow an absurdly strong roster of evolving elemental pets while climbing leaderboards."**

### **Players Will Feel:**

- 😰 **Tension** - Every extraction is risky, cargo creates vulnerability
- 🎉 **Reward** - Rare pets and loot feel earned, not given
- 📈 **Growth** - Infinite progression means always improving
- 🤝 **Social** - Co-op squads, trading economy, shared victories
- ⚔️ **Competition** - PvPvE stakes and seasonal leaderboards

---

## ⚔️ Combat System (Unique Mechanic)

### **🎮 Skill-Based Timing Combat**

**Not your typical Roblox spam-click system!**

Combat is a **rhythm-inspired, timing-based mini-game** where skill matters more than stats.

### **How Combat Works:**

```
1. Enemy Pet Attacks
   ↓
2. Shrinking Circle Appears (random position on screen)
   ↓
3. Player Must Tap Correct Button at Perfect Timing
   ↓
4. Outcome Determines Damage Distribution
```

### **Three Defense Actions:**

| Button | Color | Used For | Perfect Effect |
|--------|-------|----------|----------------|
| **DODGE** | 🔵 Blue | Physical attacks, melee strikes | Complete evasion |
| **BLOCK** | 🟢 Green | Elemental attacks, projectiles | Absorb damage |
| **COUNTER** | 🔴 Red | Punish enemy openings | Bonus damage dealt |

### **Timing Results:**

```lua
✅ PERFECT (center of circle):
   → Player/Companion take 0 damage
   → Companion counterattacks for 100% damage
   → Combo chain continues

⚠️ GOOD (medium zone):
   → Player/Companion take 50% damage
   → Companion counterattacks for 50% damage

❌ MISS (outside zones):
   → Player/Companion take 100% damage
   → No counterattack
   → Combo chain breaks
```

### **What Makes It Special:**

✅ **Mobile-Optimized**: Single-tap defense, no complex controls  
✅ **Skill > Stats**: Perfect timing beats higher-level opponents  
✅ **Endless Depth**: Rare enemies have complex combo attack patterns  
✅ **Spectator-Friendly**: Clutch plays create hype moments for viewers  
✅ **Fair Challenge**: No pay-to-win, skill expression matters  
✅ **Scalable Difficulty**: Common pets = slow/easy, Legendary = fast/brutal

### **Random Position System:**

Circles appear at **1 of 8 random positions** on screen:

```
┌─────────────────────────────────┐
│  [1]      [2]      [3]          │
│                                 │
│  [4]   Pet Image   [5]          │
│                                 │
│  [6]      [7]      [8]          │
└─────────────────────────────────┘
```

This prevents muscle memory cheese and forces spatial awareness.

### **Combo Attacks (Rare+ Enemies):**

High-tier enemies chain multiple attacks:

```
StormDrake uses: TRIPLE THUNDER STRIKE!

Hit 1: [DODGE] at position [2] → 0.5s window
Hit 2: [BLOCK] at position [6] → 0.4s window
Hit 3: [COUNTER] at position [4] → 0.3s window (FASTER!)

Perfect all 3 = PERFECT CHAIN! 
  → +150% damage on final hit
  → 0 damage taken
  → Gold text + screen flash
```

### **HP System (Hybrid Distribution):**

Three separate HP pools interact dynamically:

```
┌─────────────────────────────────┐
│ PLAYER HP: ████████ 100/100     │
│ COMPANION HP: ██████ 75/100     │
│ ENEMY HP: ████████████ 250/250  │
└─────────────────────────────────┘
```

**When Companion is Alive:**
```
Enemy deals 30 damage
  → Companion absorbs 80% (24 damage)
  → Player takes 20% (6 damage)
  
Result:
  Companion HP: 75 → 51
  Player HP: 100 → 94
```

**When Companion is Fainted:**
```
Enemy deals 30 damage
  → Player takes 100% (30 damage)
  
Result:
  Companion HP: 0 (fainted)
  Player HP: 94 → 64
```

**Why This Works:**
- Companion feels like a **guardian** (actively protecting you)
- Losing companion is **scary** (vulnerability spike)
- Strategic resource management (heal companion vs heal self)

📖 **[Full Combat System Documentation →](./COMBAT_SYSTEM_DESIGN.md)**

---

## 🐾 Pet System (Dual Role)

Pets serve **two distinct purposes** in the game:

### **1️⃣ Wild Pets (Capture Targets)**

These are creatures that:
- ✅ Roam the procedurally-generated world
- ✅ Appear in biomes, dungeons, and random encounters
- ✅ Must be defeated in combat and captured
- ✅ Added to your collection/cargo when captured
- ✅ Can be leveled, evolved, merged, and traded

**Examples:** ForestSprite, BranchStalker, StormDrake, VoidLord

---

### **2️⃣ Companion Pets (Your Active Guardian)**

One pet from your collection is **equipped as your companion**:

- ✅ Fights alongside you in combat
- ✅ Has separate HP pool that absorbs damage
- ✅ Automatically counterattacks when you defend perfectly
- ✅ Provides passive/active abilities
- ✅ **Never permanently lost** (only faints during run, restored at base)

**Three Companion Archetypes:**

| Archetype | HP | Attack | Defense | Best For |
|-----------|----|----|---------|----------|
| **Tank** (Stone/Nature) | 100 | 30 | 80% absorption | Safe exploration, new players |
| **DPS** (Fire/Lightning) | 50 | 60 | 40% absorption | Fast clears, skilled players |
| **Balanced** (Water/Air) | 75 | 40 | 60% absorption | Versatile, all-around gameplay |
| **Support** (Light/Nature) | 60 | 35 | 70% absorption | Healing-focused, team utility |

**Strategic Choice:**  
Do you bring a **Tank** for maximum safety, or a **DPS** for risky speed clears?

---

### **📊 Pet Attributes (All Pets)**

Every pet (wild or companion) has:

| Attribute | Description |
|-----------|-------------|
| **Rarity Tier** | Common → Uncommon → Rare → Epic → Legendary → Mythic → Unique |
| **Elemental Affinity** | 🔥 Fire, 💧 Water, 🌪️ Air, 🪨 Stone, ⚡ Lightning, 🌿 Nature, 🌑 Void, 🌟 Light |
| **Star Level** | ★☆☆☆☆ → ★★★★★ (merge identical pets to increase stars) |
| **Infinite Levels** | No level cap, exponential XP scaling |
| **Skill Tree** | Massive modular trees with infinite scaling nodes |

---

### **✨ Rarity Tiers**

| Tier | Spawn Rate | Difficulty | Notes |
|------|-----------|------------|-------|
| **Common** | 70% | Easy | Most frequent, simple patterns |
| **Uncommon** | 20% | Moderate | Slightly rarer, 2 attack types |
| **Rare** | 7% | Challenging | Noticeable threat, combos |
| **Epic** | 2% | Hard | Harder to find, complex patterns |
| **Legendary** | 0.8% | Very Hard | Highly sought, multi-phase |
| **Mythic** | 0.2% | Extreme | Very rare, boss mechanics |
| **Unique** | 0.1% | Ultra | Seasonal/event-only, ultimate challenge |

---

### **🌟 Star System**

Stars represent **quality** and **potential**:

- Merge **two identical pets** → increase star level
- Higher stars = better stat growth multipliers
- Higher stars = more skill points per level
- Higher stars = unlock deeper skill tree branches
- ★★★★★ pets are **massively** stronger than ★☆☆☆☆

**Example:**
```
ForestSprite ★☆☆☆☆ (Level 50): 200 HP, 40 Attack
ForestSprite ★★★★★ (Level 50): 400 HP, 80 Attack
```

---

### **🧠 Skill Trees & Evolution**

Each pet has a **massive modular skill tree** with:

- 🎯 **Core Identity Branch** - Defines pet's role
- 🔥 **Element Branch** - Amplifies elemental affinity
- 🛠️ **Utility Branch** - Capture bonuses, economy, support
- 🧬 **Mutation Branch** - Late-game hybrid transformations

**Key Feature:** Skill trees have **infinite scaling nodes**

```
Example Node: "Flame Intensity"
  Rank 1: +5% fire damage
  Rank 2: +5% fire damage
  Rank 3: +5% fire damage
  ...
  Rank 100: +500% fire damage
  (No cap, costs scale exponentially)
```

---

### **🧬 Merge / Fusion / Mutation**

- **Merge**: Combine identical pets → increase stars
- **Fuse**: Combine different species → chance to create hybrid mutation
- **Mutations**: Rare variants (e.g., Shadow ForestSprite, Neon BranchStalker)

Mutations form a **huge collectible endgame** with trading value.

---

### **🎨 Pet Customization**

- **Skins**: Toy, Shadow, Neon, Pixel, Holographic
- **Aura Particles**: Trails and ambient effects
- **SFX**: Custom sound effects
- **Naming**: Visible in leaderboards and trades

📖 **[Pet System Deep Dive →](./PET_SYSTEM_DESIGN.md)** *(coming soon)*

---

## 🌍 World & Map System

The game world is **semi-procedurally generated** on every expedition.

### **🌐 World Generation Rules**

- ✅ **Base/Spawn is always at center** (safe zone)
- ✅ **Difficulty scales with distance** from base
- ✅ **Biomes placed using weighted randomness**
- ✅ **Rare biomes appear farther from spawn**
- ✅ **Dungeons spawn randomly** with themes
- ✅ **Each run has unique layout** (no two maps identical)

### **🧱 Biome Types**

Each biome has:
- Unique **pet species pools**
- Unique **resources**
- Unique **environmental hazards**
- Elemental **identity focus**

| Biome | Element | Focus | Threats |
|-------|---------|-------|---------|
| **Forest** | 🌿 Nature | Balanced enemies | Poison, entanglement |
| **Stone Wastes** | 🪨 Stone | Defensive mobs | Slow zones, rockfalls |
| **Volcanic Rift** | 🔥 Fire | Aggressive foes | Burn damage, lava |
| **Marshlands** | 💧 Water | Healing hazards | Drowning, cursed water |
| **Storm Plateau** | ⚡ Lightning | Fast enemies | Chain lightning, storms |
| **Sky Ruins** | 🌪️ Air | Mobility challenges | Updrafts, falls |
| **Void Scar** | 🌑 Void | Ultra-rare encounters | Corruption, sanity drain |

### **🏰 Dungeon Placement**

- Random number of dungeons per expedition
- Random locations (biased toward mid/far/deep zones)
- Random themes tied to biomes:
  - 🔥 Fire Shrine
  - 🪨 Stone Tomb
  - 💧 Flooded Ruins
  - 🌪️ Sky Arena
  - 🌑 Void Laboratory

**Dungeon Rewards:**
- Guaranteed high-rarity pet encounters
- Exclusive mutation chances
- Legendary crafting materials

📖 **[World Generation Technical Design →](./WORLD_GENERATION_DESIGN.md)** *(coming soon)*

---

## 🎯 Capture System

Inspired by **Palworld** and **Tarkov extraction mechanics**.

### **How Capture Works (Step-by-Step):**

```
1. ENCOUNTER
   └─ Find a wild pet (roaming, dungeon, or boss)

2. COMBAT
   └─ Defeat it using timing-based combat system
   └─ Reduce enemy HP to 0

3. WEAKENED STATE
   └─ Enemy enters capture window (doesn't die)
   └─ Brief opportunity to capture (5-10 seconds)

4. CAPTURE ATTEMPT
   └─ Player uses capture tool (different tiers)
   └─ Server rolls capture chance

5. OUTCOME
   ✅ SUCCESS:
      └─ Pet added to cargo (consumes 1 cargo slot)
      └─ Cargo pressure activates (increased aggro)
   
   ❌ FAILURE:
      └─ Pet escapes
      └─ Loot chest spawns (reward fallback)
```

---

### **📊 Capture Success Formula**

```lua
CaptureChance = BaseRate 
  + (TimingQuality * 0.10)        -- Perfect combat performance = bonus
  + (CaptureToolTier * 0.05)      -- Better tools help
  + (CompanionAbility)            -- Some companions boost capture
  - (PetRarity * 0.15)            -- Rarer pets = harder to catch
  - (PetStars * 0.05)             -- Higher star quality = harder
```

**Example:**
```
Rare BranchStalker ★★★☆☆
Base capture rate: 30%
Perfect combat bonus: +10%
Master Capture Tool: +15%
Companion "Tamer's Bond" ability: +10%
Rarity penalty: -15%
Star penalty: -10%

Final Capture Chance: 40%
```

---

### **🎁 Failed Capture Reward (Anti-Frustration)**

**Design Philosophy:** No fight is ever wasted.

If capture **fails**, you still receive:

- 💰 **Currency** (proportional to enemy rarity)
- 📦 **Resource Chest** (crafting materials)
- 🎲 **Chance at lower-tier pet** (e.g., fail to catch Legendary → get Epic)
- ⭐ **Capture bonus points** (accumulate toward guaranteed rare capture)

---

### **🧰 Capture Tool Tiers**

| Tool Tier | Capture Bonus | Cost | Unlock |
|-----------|---------------|------|--------|
| **Basic Net** | +0% | Free | Start |
| **Reinforced Cage** | +5% | 100 | Level 5 |
| **Elemental Seal** | +10% | 500 | Level 15 |
| **Master Capture Tool** | +15% | 2000 | Level 30 |
| **Mythic Containment** | +25% | 10000 | Level 50 |

---

### **💥 Capture Difficulty Factors**

| Factor | Effect on Capture |
|--------|-------------------|
| **Pet Weakened State Quality** | More HP remaining = harder |
| **Combat Performance** | Perfect chain = easier |
| **Pet Rarity** | Legendary much harder than Common |
| **Pet Star Level** | ★★★★★ harder than ★☆☆☆☆ |
| **Player Capture Skill** | Skill tree upgrades help |
| **Companion Abilities** | Some pets boost capture chance |
| **Time of Day** | Night = slightly harder (optional) |

📖 **[Capture System Mechanics →](./CAPTURE_SYSTEM_DESIGN.md)** *(coming soon)*

---

## 🧳 Inventory & Extraction Mechanics

### **🎒 Cargo Capacity (Limited Slots)**

Players have **limited pet cargo slots** per expedition:

- **Starting:** 1 slot
- **Max (with upgrades):** 6 slots

Each captured pet consumes **1 cargo slot**.

**Strategic Choices:**
- Do you capture 1 Legendary or 3 Commons?
- Do you risk going deeper for rarer spawns?
- Do you extract early with guaranteed loot?

---

### **📦 Base Storage Capacity (Also Limited)**

Your base vault has **limited unprocessed pet storage**:

- **Starting:** 3 slots
- **Max (with vault upgrades):** 20+ slots

Extracted pets go here first, then you:
- Transfer to permanent collection
- Merge for stars
- Sell/trade
- Fuse for mutations

---

### **🎒 Loadout & Loss (Extraction Risk)**

**Before Each Expedition, Choose:**
- ⚔️ Weapons/Armor
- 💊 Healing consumables
- 🎣 Capture tools
- 🐾 Active companion pet

**If You Die (Before Extracting):**

```
❌ Items carried are lost (weapons, tools, consumables)
❌ Captured pets in cargo are LOST
✅ Base upgrades are kept (never lost)
✅ Companion pet is kept (only fainted, not lost)
✅ Currency/XP partially retained (50%)
```

**This creates extraction tension.**

---

### **❤️ Health & Limited Sustain**

- HP does **not** fully regenerate between fights
- Healing items are **limited per run** (1-3 uses)
- Resurrection scrolls are **rare and expensive**

**This prevents endless farming in one expedition.**

---

### **📤 Extraction Pressure (Returning with Loot)**

When you have captured pets in cargo:

```
⚠️ Aggro radius increases
⚠️ Additional hunters spawn (PvE)
⚠️ Movement speed slightly reduced
⚠️ Companion pet takes more damage (stressed)
```

**Optional Timed Events:**
- "Rescue Raid" - Wild pets attempt to free captured ally
- Survive timer to keep cargo
- Environmental disasters (storms, eruptions)

**Players must balance:**
- Greed (more loot = more risk)
- Safety (extract early = guaranteed rewards)
- Route planning (avoid dangerous zones)

---

### **🏁 Extraction Points**

Map has **multiple extraction gates**:

- Each closes after certain time
- Shorter routes = less safe (more enemies)
- Longer routes = safer but slower
- Strategic decision based on cargo value

📖 **[Extraction System Design →](./EXTRACTION_SYSTEM_DESIGN.md)** *(coming soon)*

---

## 🏠 Base Building System

Players own a **persistent home base** with upgradable facilities.

### **🏗️ Core Buildings (Upgradeable Tiers)**

| Building | Function | Upgrades |
|----------|----------|----------|
| **Storage Vault** | Increases pet storage slots | Tier 1-10 (3 → 20+ slots) |
| **Training Grounds** | Passive XP gain for stored pets | Tier 1-10 (XP rate increases) |
| **Capture Lab** | Improves capture success rate | Tier 1-10 (+1% per tier) |
| **Money Station** | Assign pets to generate currency/sec | Tier 1-10 (slots & rate increase) |
| **Armorsmith** | Craft/upgrade armor | Tier 1-10 (unlock better gear) |
| **Weaponsmith** | Craft/upgrade weapons | Tier 1-10 (unlock better weapons) |
| **Breeding Hall** | Pet breeding & hybrid creation | Tier 1-5 (unlock rare combos) |
| **Trading Hall** | Access auction house & player trades | Tier 1-3 (reduce fees) |
| **Defense Grid** | Reduces extraction raid intensity | Tier 1-5 (fewer ambushes) |
| **Workshop** | Craft consumables (potions, tools) | Tier 1-10 (unlock recipes) |

---

### **♾️ Soft Endless Scaling**

- Building upgrades go to **very high tiers** (Tier 50+)
- Costs scale exponentially
- Always something to grind toward
- Never truly "finished" with base

---

### **💰 Passive Income (Money Station)**

Assign pets to generate currency while offline:

```
1 Common pet: +10 currency/hour
1 Rare pet: +100 currency/hour
1 Legendary pet: +1000 currency/hour

Money Station Tier 5: 5 pet slots
Total: 1 Legendary + 4 Rares = 1,400 currency/hour
```

**This rewards collection diversity.**

📖 **[Base Building System →](./BASE_BUILDING_DESIGN.md)** *(coming soon)*

---

## 🤝 Co-Op PvE Expeditions

Players can team up in **squads** for safer expeditions.

### **👥 Squad Sizes**

- Solo (1 player)
- Duo (2 players)
- Squad (3-4 players)

---

### **🎁 Shared Encounters & Loot**

- Squad fights bosses together
- Captured pet becomes **squad cargo objective** (temporary)
- At extraction, reward distribution system activates

---

### **🎲 Loot Distribution Options**

To reduce drama and support social play:

**Option 1: Dice Roll**
- Random weighted roll among squad members
- Weighted by contribution (damage dealt, heals, etc.)

**Option 2: Pass/Need System**
- Like MMO dungeon loot
- Players vote on who gets pet
- Prevents ninja looting

**Option 3: Pre-Agreed Ownership**
- Squad leader assigns loot before run
- Clear expectations

**Option 4: Everyone Gets Copy (Solo Mode)**
- Easier but less valuable

---

### **🤝 Squad Synergies**

- Companions can **stack buffs** (e.g., Tank + DPS combo)
- Shared healing pools
- Revive downed teammates (limited uses)
- Coordinated extraction routes

📖 **[Co-Op System Design →](./COOP_SYSTEM_DESIGN.md)** *(coming soon)*

---

## ⚔️ PvPvE Mode (High Risk, High Reward)

A **unique competitive mode** with strict anti-grief systems.

### **🎯 Core Idea**

PvPvE map is:
- Harder enemies (higher rarity spawns)
- Rarer pets (better loot)
- More rewarding (2x currency, unique mutations)
- **PvP enabled** - players can ambush others carrying loot

---

### **⚔️ PvP Combat: "Pet Duel Boss Race"**

**NOT simple "gun down the player" PvP!**

When Player A attacks Player B:

```
┌─────────────────────────────────────────┐
│ DUEL SYSTEM                             │
├─────────────────────────────────────────┤
│ Both players' COMPANION PETS fight      │
│ using the same combat system:           │
│                                         │
│ • Same timing mechanics                 │
│ • Same circle shrinking                 │
│ • Same Perfect/Good/Miss outcomes       │
│                                         │
│ First to defeat opponent's companion:   │
│ ✅ Winner claims opponent's cargo       │
│ ❌ Loser loses loot but keeps companion │
│                                         │
│ Both players keep their companion pet   │
│ (companions only faint, never lost)     │
└─────────────────────────────────────────┘
```

**Why This Works:**
- ✅ **Fair fights** (skill-based, not gear-based)
- ✅ **Spectator-friendly** (exciting duels to watch)
- ✅ **Less toxic** (not instant death cheese)
- ✅ **Build variety** (Tank vs DPS strategies)

---

### **🛡️ Anti-Grief Protection (CRITICAL)**

These rules prevent toxicity:

#### **1️⃣ Level/Power Brackets**
```
Players only matched with similar:
  • Player level ±5
  • Companion rarity ±1 tier
  • Total playtime within 50%
```

#### **2️⃣ No-Loot Protection**
```
IF player carries no valuable cargo:
  → Cannot be targeted
  OR
  → Attacker receives no reward (pointless)
```

#### **3️⃣ Staked PvP (Required)**
```
To initiate PvP, attacker must stake:
  • Currency (e.g., 500)
  • Items (e.g., 1 capture tool)

IF attacker loses:
  → Defender gains the stake
  → Attacker loses stake + time

This kills griefing entirely.
```

#### **4️⃣ Safe Extraction Zones**
```
Small anti-combat radius near base gate:
  • PvP disabled within 50 studs
  • OR extraction "bubble" activates final 10 seconds
```

#### **5️⃣ Anti-Camping Systems**
```
If player stays near extraction too long:
  • Revealed on mini-map
  • Debuff applied (-25% defense)
  • PvE hunters spawn nearby
```

---

### **🎁 PvPvE Loot Rules**

- Only loot-carrying players are valid targets (optional rule)
- Attacker stakes resources to attack
- Winner claims:
  - Opponent's cargo (or 50% of it)
  - Bonus PvP currency/tokens
  - PvP leaderboard points

**PvPvE Exclusive Rewards:**
- Higher rarity pet pools (Legendary/Unique more common)
- PvP-only mutation variants (e.g., "Duelist" skins)
- Special crafting materials
- Seasonal tokens

📖 **[PvPvE System Design →](./PVPVE_SYSTEM_DESIGN.md)** *(coming soon)*

---

## 💰 Economy & Rewards

### **💵 Currency Types**

| Currency | Source | Used For |
|----------|--------|----------|
| **Glow Cash** | Main currency | Pet upgrades, base buildings, consumables |
| **Hype Crystals** | Rare drops, events | High-tier upgrades, legendary tools |
| **Encore Tokens** | Prestige resets | Prestige bonuses, seasonal items |
| **Star Shards** | Premium/events | Cosmetics, QoL upgrades, NOT power |

---

### **📈 Currency Scaling**

Rewards scale exponentially with:

- 🗺️ **Depth reached** (farther from base = more currency)
- 🐾 **Pet rarity defeated** (Legendary kills = 10x Common)
- ⚔️ **PvPvE wins** (high-risk bonus)
- 🏆 **Seasonal milestones** (leaderboard ranks)
- ⭐ **Perfect combat chains** (skill bonus)

**Example Scaling:**
```
Common pet kill: 10 Glow Cash
Rare pet kill: 100 Glow Cash
Legendary pet kill: 1,000 Glow Cash
Unique pet kill: 10,000 Glow Cash
```

---

### **🔄 Economy Sinks (Prevent Inflation)**

- Base building costs (exponential)
- Pet fusion costs (high-tier)
- Consumable purchases (repeated)
- Trading fees (5-10%)
- Seasonal exclusive items (limited time)

---

### **🛒 Trading & Auction House**

- Player-to-player trading (direct)
- Auction house (bid system)
- Creator codes (revenue share)
- Pet rental system (advanced)

📖 **[Economy Design Document →](./ECONOMY_DESIGN.md)** *(coming soon)*

---

## 📊 Balance & Progression

### **🐾 Enemy Stats by Rarity**

| Rarity | Base HP | Attack | Shrink Time | Perfect Zone | Attacks/Fight | Combos |
|--------|---------|--------|-------------|--------------|---------------|--------|
| **Common** | 100 | 20 | 2.0s | 30% | 3-4 | None |
| **Uncommon** | 150 | 25 | 1.5s | 25% | 4-5 | Rare |
| **Rare** | 250 | 35 | 1.0s | 15% | 5-6 | Common |
| **Epic** | 400 | 50 | 0.7s | 10% | 6-8 | Frequent |
| **Legendary** | 600 | 70 | 0.4s | 5% | 8-10 | Very Common |
| **Mythic** | 800 | 90 | 0.3s | 3% | 10-12 | Always |
| **Unique** | 1000+ | 100+ | 0.3s | 3% | 10-15 | Multi-phase |

---

### **🛡️ Companion Archetype Stats**

| Type | Base HP | Base Attack | Defense % | HP/Level | ATK/Level |
|------|---------|-------------|-----------|----------|-----------|
| **Tank** | 100 | 30 | 80% | +5 | +2 |
| **DPS** | 50 | 60 | 40% | +2 | +4 |
| **Balanced** | 75 | 40 | 60% | +3 | +3 |
| **Support** | 60 | 35 | 70% | +3 | +2 |

**Companion Level 50 Example:**
```
Tank:     100 + (5*50) = 350 HP, 30 + (2*50) = 130 Attack
DPS:      50 + (2*50) = 150 HP, 60 + (4*50) = 260 Attack
Balanced: 75 + (3*50) = 225 HP, 40 + (3*50) = 190 Attack
```

---

### **📈 Distance Scaling (World Depth)**

Enemies get stronger the farther you venture:

```lua
distanceMultiplier = 1 + (distanceFromBase * 0.1)

-- Example: Rare pet at distance 20
BaseHP: 250
ScaledHP: 250 * (1 + 20*0.1) = 250 * 3 = 750 HP

BaseAttack: 35
ScaledAttack: 35 * 3 = 105 damage
```

---

### **⚡ Damage Multipliers**

#### **Timing-Based Damage Reduction:**
```
Perfect: 0%   damage taken (full dodge/block)
Good:    50%  damage taken
Miss:    100% damage taken
```

#### **Counterattack Damage:**
```
Perfect: 100% companion attack damage
Good:    50%  companion attack damage
Miss:    0%   no counterattack
```

#### **Combo Chain Bonuses:**
```
2-hit perfect combo: +25% final hit damage
3-hit perfect combo: +50% final hit damage
4-hit perfect combo: +100% final hit damage
5+ hit perfect combo: +150% final hit damage
```

---

### **♾️ Infinite Progression Systems**

- 📈 **Pet Levels**: No cap, exponential XP
- 🌲 **Skill Trees**: Infinite scaling nodes
- 🏠 **Base Buildings**: Tier 50+ upgrades
- 💰 **Currency**: Always useful (never capped)
- 🏆 **Leaderboards**: Seasonal resets

📖 **[Full Balance Spreadsheet →](./balance/)** *(coming soon)*

---

## 📊 Leaderboards & Seasons

### **🏆 Leaderboard Categories**

| Category | Metric | Reset |
|----------|--------|-------|
| **Max Expedition Depth** | Farthest distance from base | Seasonal |
| **Currency Per Second** | Passive + active income | Seasonal |
| **Rarest Pets Owned** | Unique/Mythic collection | Never |
| **PvPvE Wins** | Total duel victories | Seasonal |
| **Perfect Combat Chains** | Longest streak | Seasonal |
| **Group Rank** | Clan/guild progression | Seasonal |

---

### **🌟 Seasonal System**

**Seasons reset every 3 months:**

```
✅ Leaderboards reset (fresh competition)
✅ Seasonal unique pets (limited time)
✅ New mutation variants (cosmetic/minor stat)
✅ Special events (2x capture rate weekends)
✅ Exclusive rewards (top 100 players)

❌ Pet collection NOT reset
❌ Base buildings NOT reset
❌ Player level NOT reset
❌ Companion pets NOT reset
```

**Season Rewards:**
- Exclusive pet skins
- Seasonal titles/badges
- Currency bonuses
- Early access to updates

📖 **[Seasonal Content Plan →](./SEASONAL_CONTENT.md)** *(coming soon)*

---

## 🎨 UI Preview

### **Combat UI Layout (Mobile)**

```
┌─────────────────────────────────────────┐
│ ┌─────────────────────────────────────┐ │
│ │ BranchStalker (Rare)                │ │
│ │ HP: ████████████░░░░ 205/250        │ │
│ └─────────────────────────────────────┘ │
├─────────────────────────────────────────┤
│                                         │
│      [3D Pet Model Renders Here]        │
│                                         │
│              ◯◯◯◯◯                      │
│              ◯   ◯  ← Outer ring        │
│              ◯ ● ◯  ← Center dot        │
│              ◯   ◯     (shrinks)        │
│              ◯◯◯◯◯                      │
│         Position [7]                    │
│                                         │
├─────────────────────────────────────────┤
│ ┌─────────────────────────────────────┐ │
│ │ Player HP:    ████████░░ 89/100     │ │
│ │ Companion HP: ██████░░░░ 33/75      │ │
│ └─────────────────────────────────────┘ │
├─────────────────────────────────────────┤
│                                         │
│  [   DODGE   ]  [ BLOCK  ] [ COUNTER ] │
│      BLUE         GREEN        RED      │
│  (40% screen height - easy tapping)    │
│                                         │
└─────────────────────────────────────────┘
```

---

### **Desktop/PC Layout**

```
┌───────────────────────────────────────────────┐
│ Enemy: StormDrake (Legendary)                 │
│ HP: ████████████████ 450/600                  │
├───────────────────────────────────────────────┤
│                                               │
│                                               │
│         [3D Pet Model]        ◯               │
│                                ●  ← Circle    │
│                                               │
│                                               │
│         Q - DODGE (Blue)                      │
│         E - BLOCK (Green)                     │
│         SPACE - COUNTER (Red)                 │
│                                               │
│  Press key when circle overlaps center dot!   │
│                                               │
├───────────────────────────────────────────────┤
│ Player: ███████░░░ 75/100                     │
│ Companion: ██████░░░░ 40/75                   │
└───────────────────────────────────────────────┘
```

---

### **Visual Feedback Examples**

#### **Perfect Hit:**
```
✨ Bright green flash
🎆 Circle explodes outward (particle effect)
📝 "PERFECT!" text (gold, large)
📳 Vibration (mobile)
🔊 Satisfying chime sound
```

#### **Good Hit:**
```
💛 Yellow flash (subtle)
📝 "GOOD" text (medium size)
📳 Small vibration
🔊 Normal hit sound
```

#### **Miss:**
```
❌ Red flash
💥 Circle disappears instantly
📝 "MISS!" text (red, shake animation)
📳 Harsh vibration
🔊 Error/damage tone
💔 Player takes visible damage (screen shake)
```

📖 **[Full UI/UX Documentation →](./COMBAT_SYSTEM_DESIGN.md#visual-ui-system)**

---

## 🛠 Technical Architecture

### **⚙️ Core Server Services**

```
src/Server/Services/
├── WorldGeneratorService.lua       # Semi-procedural map generation
├── BiomeService.lua                 # Biome placement & rules
├── SpawnService.lua                 # Pet spawning (initial + refresh)
├── CombatService.lua                # Combat session management
├── DamageCalculationService.lua     # Damage formulas & validation
├── TimingValidationService.lua      # Anti-cheat timing checks
├── CompanionService.lua             # Companion stats & abilities
├── EnemyAIService.lua               # Enemy attack patterns
├── CaptureService.lua               # Capture chance & outcomes
├── ExtractionService.lua            # Extraction mechanics
├── PvPvEService.lua                 # Duel system & anti-grief
├── InventoryService.lua             # Cargo & storage management
├── BaseManagementService.lua        # Base building & upgrades
├── EconomyService.lua               # Currency & trading
├── LeaderboardService.lua           # Rankings & seasons
└── PlayerDataService.lua            # Data persistence (DataStores)
```

---

### **🔄 Shared Modules**

```
src/Shared/
├── CombatConstants.lua              # Balance tables & config
├── PetDefinitions.lua               # All pet stats & abilities
├── BiomeDefinitions.lua             # Biome data & spawn pools
├── AttackPatterns.lua               # Enemy attack sequences
├── AbilityDefinitions.lua           # Companion abilities
├── Config.lua                       # Global game config
└── Utils.lua                        # Helper functions
```

---

### **🖥️ Client Controllers**

```
src/Client/Controllers/
├── CombatUIController.lua           # Combat UI rendering
├── InputController.lua              # Button tap handling
├── AnimationController.lua          # Visual effects & tweens
├── CameraController.lua             # Camera systems
├── SoundController.lua              # Audio management
└── NetworkController.lua            # Client-server sync
```

---

### **📡 RemoteEvents (Client ↔ Server)**

```
ReplicatedStorage/RemoteEvents/
├── CombatStart                      # Initiate combat session
├── DefenseInput                     # Player defense tap
├── CombatUpdate                     # Round state updates
├── CombatEnd                        # Victory/defeat resolution
├── CaptureAttempt                   # Player attempts capture
├── ExtractionRequest                # Player initiates extraction
└── PvPDuelChallenge                 # PvP duel initiation
```

---

## 💻 Development Tools & Workflow

### **🔧 Required Tools**

| Tool | Purpose | Link |
|------|---------|------|
| **Roblox Studio** | Game development IDE | [Download](https://www.roblox.com/create) |
| **Visual Studio Code** | External code editor | [Download](https://code.visualstudio.com/) |
| **Git** | Version control | [Download](https://git-scm.com/) |
| **GitHub Desktop** | Git GUI (optional) | [Download](https://desktop.github.com/) |
| **Rojo** | Sync code to Roblox Studio | [Install Guide](https://rojo.space/) |
| **Aftman** | Tool version manager | [GitHub](https://github.com/LPGhatguy/aftman) |

---

### **✨ Optional but Recommended**

| Tool | Purpose | Link |
|------|---------|------|
| **Blender** | 3D modeling (pets, props) | [Download](https://www.blender.org/) |
| **Audacity** | Audio editing (SFX) | [Download](https://www.audacityteam.org/) |
| **Figma** | UI/UX design | [Web App](https://www.figma.com/) |
| **Adobe XD** | UI design (alternative) | [Download](https://www.adobe.com/products/xd.html) |
| **Google Sheets** | Balance tables & scaling | [Web App](https://sheets.google.com/) |

---

### **⚡ Recommended VS Code Extensions**

```
- Luau Language Server (JohnnyMorganz)
- Rojo (evaera)
- GitLens (Eric Amodio)
- Better Comments (Aaron Bond)
- Todo Tree (Gruntfuggly)
```

---

## 📁 Repository Structure

```
idol-guardians-eternal-wilds/
├── src/
│   ├── Server/
│   │   ├── Services/
│   │   │   ├── WorldGeneratorService.lua
│   │   │   ├── CombatService.lua
│   │   │   ├── CaptureService.lua
│   │   │   └── ... (all server services)
│   │   └── ServerMain.server.lua
│   │
│   ├── Client/
│   │   ├── Controllers/
│   │   │   ├── CombatUIController.lua
│   │   │   ├── InputController.lua
│   │   │   └── ... (all client controllers)
│   │   └── ClientMain.client.lua
│   │
│   └── Shared/
│       ├── CombatConstants.lua
│       ├── PetDefinitions.lua
│       ├── BiomeDefinitions.lua
│       └── ... (all shared modules)
│
├── assets/
│   ├── models/
│   ├── textures/
│   ├── audio/
│   └── ui/
│
├── docs/
│   ├── COMBAT_SYSTEM_DESIGN.md
│   ├── COMBAT_SYSTEM_README.md
│   ├── SETUP_GUIDE.md
│   └── ... (all documentation)
│
├── balance/
│   ├── enemy_stats.csv
│   ├── companion_stats.csv
│   └── economy_scaling.csv
│
├── tests/
│   ├── server/
│   └── client/
│
├── .gitignore
├── .gitattributes
├── aftman.toml
├── default.project.json
├── selene.toml
├── stylua.toml
├── LICENSE
└── README.md (this file)
```

---

## 🧪 Getting Started

### **📥 Clone the Repository**

```bash
git clone https://github.com/yourusername/idol-guardians-eternal-wilds.git
cd idol-guardians-eternal-wilds
```

---

### **⚙️ Install Tools**

```bash
# Install Aftman (tool manager)
# Follow instructions at: https://github.com/LPGhatguy/aftman

# Then install Rojo and other tools
aftman install
```

---

### **🚀 Start Development Server**

```bash
# Start Rojo server
rojo serve default.project.json
```

---

### **🔌 Connect Roblox Studio**

1. Open **Roblox Studio**
2. Install **Rojo plugin** from [rojo.space](https://rojo.space/)
3. Click **Rojo plugin icon** in Studio
4. Click **Connect** (should auto-detect localhost:34872)
5. Confirm sync

---

### **💻 Start Coding**

```bash
# Open project in VS Code
code .

# Edit files in src/
# Changes auto-sync to Studio via Rojo
```

---

### **🧪 Testing**

```bash
# Play in Studio to test
# Or publish to Roblox for multiplayer testing
```

📖 **[Full Setup Guide →](./docs/SETUP_GUIDE.md)** *(coming soon)*

---

## 📌 Development Roadmap

### **Phase 1 – Core Systems** (6-8 weeks)

#### **Week 1-2: World & Spawning**
- ✅ Semi-procedural world generation (grid-based)
- ✅ Biome placement system
- ✅ Pet spawn system (initial wave + refresh waves)
- ✅ Despawn timers (rarity-based lifetimes)
- ✅ Safe spawn radius (no base camping)

#### **Week 3-5: Combat System** ⭐ **CRITICAL PRIORITY**
- ✅ Timing-based defense mechanics
- ✅ Shrinking circle UI (8 random positions)
- ✅ Perfect/Good/Miss validation (server-side)
- ✅ Companion pet system (Tank/DPS/Balanced)
- ✅ Damage distribution (hybrid HP system)
- ✅ Basic enemy attack patterns (Common → Rare)
- ✅ Visual feedback (flashes, damage numbers)
- ✅ Mobile optimization

#### **Week 6: Capture & Inventory**
- ✅ Weakened state mechanics
- ✅ Capture chance calculation
- ✅ Loot chest fallback (failed captures)
- ✅ Cargo system (limited slots)
- ✅ Cargo pressure (aggro increase)

#### **Week 7-8: Extraction & Base**
- ✅ Extraction mechanics
- ✅ Multiple extraction points
- ✅ Base storage system
- ✅ Simple base upgrades (Vault, Training Grounds)
- ✅ Player data persistence (DataStores)

---

### **Phase 2 – Progression & Depth** (4-5 weeks)

#### **Week 9-10: Pet Progression**
- ✅ Pet leveling (infinite scaling)
- ✅ Skill tree framework (modular branches)
- ✅ Star system & merging
- ✅ Evolution milestones (Level 25, 50, 100)

#### **Week 11-12: Companion Abilities**
- ✅ Passive abilities (always active)
- ✅ Active abilities (auto-trigger)
- ✅ Ability balancing
- ✅ Ability visual effects

#### **Week 13: Base Automation**
- ✅ Money Station (passive income)
- ✅ Training Grounds (passive XP)
- ✅ Breeding Hall (pet fusion)
- ✅ Workshop (consumable crafting)

---

### **Phase 3 – PvPvE & Social** (4-5 weeks)

#### **Week 14-15: PvPvE System**
- ✅ Duel mechanics (companion vs companion)
- ✅ Anti-grief protections (level brackets, stakes)
- ✅ Safe zones & anti-camping
- ✅ PvPvE rewards (exclusive mutations)

#### **Week 16-17: Trading & Economy**
- ✅ Trading Hall (player-to-player trades)
- ✅ Auction house (bidding system)
- ✅ Currency sinks (prevent inflation)
- ✅ Economy balancing

#### **Week 18: Leaderboards**
- ✅ Seasonal rankings
- ✅ Multiple categories (depth, currency, PvPvE)
- ✅ Seasonal rewards
- ✅ Clan/guild system (optional)

---

### **Phase 4 – Polish & Content** (3-4 weeks)

#### **Week 19-20: Audio & VFX**
- ✅ Sound design (combat, UI, ambient)
- ✅ Particle effects (perfect hits, combos)
- ✅ Music (biome themes, combat tracks)
- ✅ Screen effects (flashes, shakes)

#### **Week 21: Balance Tuning**
- ✅ Playtest all systems
- ✅ Adjust damage numbers
- ✅ Adjust capture rates
- ✅ Adjust currency scaling

#### **Week 22: Mobile Optimization**
- ✅ Performance profiling
- ✅ UI scaling for small screens
- ✅ Touch control polish
- ✅ Network optimization

---

### **Phase 5 – Launch Prep** (2-3 weeks)

#### **Week 23-24: Content Creation**
- ✅ Tutorial system
- ✅ First seasonal event
- ✅ Unique/Mythic pets finalized
- ✅ Promotional materials

#### **Week 25: Soft Launch**
- ✅ Limited release (friends & testers)
- ✅ Bug fixes
- ✅ Community feedback integration
- ✅ Final polish

---

### **Post-Launch: Live Operations**

- 🔄 Weekly content updates
- 🔄 Seasonal events (every 3 months)
- 🔄 New biomes & pets
- 🔄 Balance patches
- 🔄 Community-driven features

---

## 📚 Documentation

### **📖 Core Systems Design Docs**

- [🎮 Combat System (Complete Design)](./COMBAT_SYSTEM_DESIGN.md) ✅ **Available Now**
- [⚔️ Combat Implementation Guide](./COMBAT_SYSTEM_README.md) ✅ **Available Now**
- [🗺️ World Generation Design](./docs/WORLD_GENERATION_DESIGN.md) *(coming soon)*
- [🐾 Pet System Design](./docs/PET_SYSTEM_DESIGN.md) *(coming soon)*
- [🎯 Capture System Design](./docs/CAPTURE_SYSTEM_DESIGN.md) *(coming soon)*
- [🏠 Base Building Design](./docs/BASE_BUILDING_DESIGN.md) *(coming soon)*
- [⚔️ PvPvE System Design](./docs/PVPVE_SYSTEM_DESIGN.md) *(coming soon)*
- [💰 Economy Design](./docs/ECONOMY_DESIGN.md) *(coming soon)*

---

### **🔧 Developer Guides**

- [🛠️ Setting Up Rojo + VS Code](./docs/SETUP_GUIDE.md) *(coming soon)*
- [🧪 Testing Guidelines](./docs/TESTING_GUIDE.md) *(coming soon)*
- [📊 Balance Spreadsheets](./balance/) *(coming soon)*
- [🎨 UI/UX Guidelines](./docs/UI_GUIDELINES.md) *(coming soon)*
- [🔊 Audio Design Guide](./docs/AUDIO_GUIDE.md) *(coming soon)*

---

### **📡 API Reference**

- [📡 Server Services API](./docs/api/SERVER_API.md) *(coming soon)*
- [🎨 Client Controllers API](./docs/api/CLIENT_API.md) *(coming soon)*
- [🔄 Shared Modules API](./docs/api/SHARED_API.md) *(coming soon)*

---

## ❓ Frequently Asked Questions

### **Q: Is this pay-to-win?**

**A:** Absolutely not. Combat is 100% skill-based — perfect timing beats higher stats every time. Premium currency (Star Shards) **only** buys:
- Cosmetic pet skins
- Base decorations
- Minor quality-of-life upgrades (NOT power)

You cannot buy stronger companions or better stats. Skill always wins.

---

### **Q: Can I play solo or do I need a team?**

**A:** Both are fully supported!

- **Solo**: Totally viable, balanced for single-player
- **Co-op PvE**: Optional, great for social play and shared rewards
- **PvPvE**: Entirely separate mode (optional, high-risk/reward)

You can enjoy the entire game solo if you prefer.

---

### **Q: What happens if I lose my companion pet in combat?**

**A:** Your companion only **faints** during an expedition. It's **fully restored** when you:
- Extract successfully back to base
- Die and respawn at base

You **never permanently lose** your companion pets. They're safe in your collection.

---

### **Q: How does the game stay interesting after 100+ hours?**

**A:** Multiple endgame loops:

- ♾️ **Infinite pet levels & skill trees** (always room to grow)
- 🌟 **Seasonal unique pets & events** (new content every 3 months)
- 🗺️ **Semi-procedural worlds** (every expedition is unique)
- ⚔️ **PvPvE competitive scene** (leaderboards, duels, stakes)
- 💰 **Trading economy & social meta** (market fluctuations, rare trades)
- 🧬 **Mutation hunting** (collectible rare variants)

There's always a rarer pet, deeper run, or higher rank to chase.

---

### **Q: Is mobile performance good?**

**A:** Yes! The game is **mobile-first** by design:

- ✅ Single-tap combat mechanics (no complex controls)
- ✅ Optimized UI scaling for small screens
- ✅ Performance profiling for 60 FPS on mid-range devices
- ✅ Network optimization for cellular connections
- ✅ Touch-friendly button sizes (40% screen height)

PC/Console are supported but mobile is the priority.

---

### **Q: Can I trade pets with other players?**

**A:** Yes! Trading system includes:

- Direct player-to-player trades
- Auction house (bidding system)
- Trading Hall building (unlocks at base tier 2)
- Trade fees (5-10% to prevent flipping)
- Scam protection (confirmation windows)

---

### **Q: How often are updates/new content?**

**A:** Planned cadence:

- 🐛 **Bug fixes**: As needed (weekly if critical)
- ⚖️ **Balance patches**: Bi-weekly
- 🆕 **Content updates**: Monthly (new pets, events)
- 🌟 **Seasonal resets**: Every 3 months (major content drops)

---

### **Q: Will there be a story/campaign?**

**A:** Not in the traditional sense. Instead:

- 🗺️ **Environmental storytelling** (biome lore, dungeon themes)
- 🐾 **Pet descriptions** (lore snippets)
- 🏛️ **Seasonal events** (narrative arcs)
- 🎭 **Optional side objectives** (challenges, achievements)

The focus is on **gameplay loops**, not linear story progression.

---

### **Q: What if I don't like PvP?**

**A:** PvPvE is **entirely optional**!

- PvE expeditions are the default (no PvP)
- PvPvE is a **separate mode** you opt into
- All content is accessible via PvE
- PvPvE only offers **cosmetic bonuses** and **leaderboard ranks** (not essential)

You can ignore PvPvE entirely and enjoy 100% of the game.

---

## 🌐 Community

### **🎮 Join the Community**

- **Discord**: [discord.gg/idolguardians](#) *(link when created)*
- **Twitter/X**: [@IdolGuardians](#) *(link when created)*
- **YouTube**: [youtube.com/IdolGuardians](#) *(link when created)*
- **TikTok**: [@IdolGuardians](#) *(link when created)*
- **Reddit**: [r/IdolGuardians](#) *(link when created)*

---

### **🧪 Playtesting Program**

Want to be an early tester?

1. Join our **Discord**
2. Sign up for **playtesting waves**
3. Provide feedback on balance & bugs
4. Get **exclusive tester badge** in-game

Early testers get:
- Early access to updates
- Exclusive pet skins
- Input on game direction
- Recognition in credits

---

### **🎥 Content Creator Support**

We support content creators with:

- 🎬 **Early access builds** (embargoed previews)
- 💰 **Creator codes** (revenue share program)
- 📊 **API for stat tracking** (leaderboards, analytics)
- 📺 **Spectator mode features** (camera tools)
- 🎁 **Exclusive cosmetics** (creator-branded pets)

**Interested?** Contact us via Discord!

---

### **📣 Community Events**

Planned community activities:

- 🏆 **Monthly tournaments** (PvPvE brackets)
- 🎨 **Pet design contests** (community-voted pets added to game)
- 📸 **Screenshot competitions** (best captures/moments)
- 🎭 **Roleplay events** (themed expeditions)
- 🎁 **Giveaways** (premium currency, rare pets)

---

## 🤝 Contributing

We welcome contributions from the community!

### **📜 Contribution Guidelines**

See [CONTRIBUTING.md](./CONTRIBUTING.md) *(coming soon)* for:

- **Code standards** (Luau style guide)
- **Pull request process** (branch naming, review flow)
- **Bug reporting** (templates, reproduction steps)
- **Feature suggestions** (proposal format)
- **Testing requirements** (what to test before PR)

---

### **🐛 Report a Bug**

Found a bug? Please:

1. Check [existing issues](https://github.com/yourusername/idol-guardians/issues)
2. Create new issue with:
   - Clear title
   - Steps to reproduce
   - Expected vs actual behavior
   - Screenshots/videos if applicable
   - Device/platform info

---

### **💡 Suggest a Feature**

Have an idea? We'd love to hear it!

1. Check [discussions](https://github.com/yourusername/idol-guardians/discussions)
2. Create new discussion with:
   - Problem you're trying to solve
   - Proposed solution
   - Alternative approaches considered
   - Why this benefits the game

---

### **🌟 Hall of Fame**

Top contributors will be recognized:

- 🏆 **In-game credits**
- 🎁 **Exclusive contributor pet skin**
- 📛 **Discord role & badge**
- 💬 **Direct line to dev team**

---

## 🏁 License

This project is licensed under the **MIT License** - see the [LICENSE](./LICENSE) file for details.

**TL;DR:** You can use, modify, and distribute this code, but must include the original license and copyright notice.

---

## ❤️ Thank You

Thank you for checking out **Idol Guardians: Eternal Wilds** — a deep, evolving, endless adventure on Roblox.

Whether you're a player, developer, content creator, or just curious — we're excited to have you here.

---

### **🚀 Ready to Start?**

- 🎮 [Play the Game](#) *(coming soon)*
- 💻 [Set Up Dev Environment](./docs/SETUP_GUIDE.md)
- 📖 [Read Combat System Design](./COMBAT_SYSTEM_DESIGN.md)
- 💬 [Join Discord](#)

---

**Built with ❤️ by the Idol Guardians team**

**Let's create something amazing together.**

---

*Last Updated: December 14, 2025 | Version 1.0.0-alpha*
