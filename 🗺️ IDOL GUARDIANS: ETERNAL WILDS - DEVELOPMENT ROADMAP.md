# 🗺️ IDOL GUARDIANS: ETERNAL WILDS - DEVELOPMENT ROADMAP
**Complete Implementation Guide & Feature Checklist**  
**Version:** 1.0  
**Last Updated:** January 4, 2026  
**Target Platform:** Roblox (Lua/Luau)  
**Development Timeline:** 22 months (MVP → Launch)

---

## 📋 TABLE OF CONTENTS

### **SECTION 1: OVERVIEW**
1. How to Use This Document
2. Development Philosophy
3. Tech Stack & Tools
4. Project Structure
5. Design Document Reference Guide

### **SECTION 2: PHASE 1 - MVP (Months 1-6)**
6. MVP Milestone 1: Core Combat Prototype (Weeks 1-4)
7. MVP Milestone 2: Pet Capture System (Weeks 5-8)
8. MVP Milestone 3: Basic Progression (Weeks 9-12)
9. MVP Milestone 4: World Basics (Weeks 13-18)
10. MVP Milestone 5: Economy Foundation (Weeks 19-24)

### **SECTION 3: PHASE 2 - ALPHA (Months 7-12)**
11. Alpha Milestone 1: Combat Polish (Weeks 25-30)
12. Alpha Milestone 2: Full Pet System (Weeks 31-36)
13. Alpha Milestone 3: Base Building (Weeks 37-44)
14. Alpha Milestone 4: World Generation (Weeks 45-52)
15. Alpha Milestone 5: Multiplayer Foundation (Weeks 53-60)

### **SECTION 4: PHASE 3 - BETA (Months 13-18)**
16. Beta Milestone 1: Retention Features (Weeks 61-68)
17. Beta Milestone 2: Social Systems (Weeks 69-76)
18. Beta Milestone 3: UI/UX Polish (Weeks 77-84)
19. Beta Milestone 4: Performance Optimization (Weeks 85-92)

### **SECTION 5: PHASE 4 - LAUNCH (Months 19-22)**
20. Launch Milestone 1: Content Complete (Weeks 93-96)
21. Launch Milestone 2: Live Operations Prep (Weeks 97-100)

### **SECTION 6: TECHNICAL SPECIFICATIONS**
22. Database Schema
23. Network Architecture
24. Server-Client Communication
25. Anti-Cheat Implementation

### **SECTION 7: TESTING & QA**
26. Testing Checklist
27. Balance Testing
28. Performance Benchmarks

---

# SECTION 1: OVERVIEW

## 📖 HOW TO USE THIS DOCUMENT

### **For Claude Code:**

This document is your complete implementation guide. Follow these steps:

1. **Start at the beginning** - Build features in order (dependencies matter)
2. **Check off tasks as you complete them** - Update checkboxes: `[ ]` → `[x]`
3. **Read referenced design docs** - Each feature links to detailed specs
4. **Test before moving on** - Each milestone has acceptance criteria
5. **Update this document** - Add notes, mark blockers, track progress

### **Document Structure:**

```
Each Feature Entry Contains:
├─ Priority Level (Critical/High/Medium/Low)
├─ Estimated Time (hours/days/weeks)
├─ Dependencies (what must be built first)
├─ Design Doc Reference (where to find detailed specs)
├─ Implementation Notes (technical guidance)
├─ Acceptance Criteria (when is it "done")
└─ Checkbox [ ] for progress tracking
```

### **How to Track Progress:**

```markdown
Example:
- [x] ✅ COMPLETED: Feature is done and tested
- [ ] ⏳ IN PROGRESS: Currently working on this
- [ ] 🔒 BLOCKED: Waiting on dependency
- [ ] ❌ SKIPPED: Decided not to implement
- [ ] 📝 PLANNED: Not started yet
```

---

## 🎯 DEVELOPMENT PHILOSOPHY

### **Core Principles:**

**1. Start Small, Iterate Fast**
- Build minimum viable version of each system
- Test with real players (even just yourself)
- Iterate based on feedback, not assumptions

**2. Vertical Slice Before Horizontal Expansion**
- ONE complete gameplay loop beats many incomplete systems
- Example: Perfect combat for 1 enemy type > Mediocre combat for 10 types

**3. Fun First, Features Second**
- If core gameplay isn't fun, no amount of features will save it
- Test "is this fun?" at every step
- Cut features that don't add to fun factor

**4. Mobile-First Always**
- Design for mobile, port to PC (not reverse)
- Touch controls must feel responsive
- UI must be readable on small screens

**5. Performance Matters**
- Target: 60 FPS on mid-range mobile devices
- Profile regularly, optimize hotspots
- Don't premature optimize, but don't ignore performance

**6. Server Authority, Client Prediction**
- Server decides game state (anti-cheat)
- Client predicts for responsiveness
- Validate everything server-side

---

## 🛠️ TECH STACK & TOOLS

### **Primary Development:**

| Tool | Purpose | Version |
|------|---------|---------|
| **Roblox Studio** | Game engine | Latest stable |
| **Luau** | Programming language | Roblox's Lua variant |
| **Rojo** | External IDE sync | 7.x |
| **VS Code** | Code editor | Latest |
| **Selene** | Lua linter | Latest |
| **StyLua** | Code formatter | Latest |

### **Version Control:**

| Tool | Purpose |
|------|---------|
| **Git** | Version control |
| **GitHub** | Repository hosting |
| **GitHub Actions** | CI/CD pipeline |

### **Asset Management:**

| Tool | Purpose |
|------|---------|
| **Blender** | 3D modeling (pets, environments) |
| **Aseprite** | Pixel art / UI sprites |
| **Audacity** | Sound editing |

### **Project Management:**

| Tool | Purpose |
|------|---------|
| **This Document** | Master roadmap |
| **GitHub Issues** | Bug tracking |
| **GitHub Projects** | Sprint planning |
| **Trello/Notion** | Optional task boards |

---

## 📁 PROJECT STRUCTURE

### **Recommended Roblox Project Layout:**

```
IdolGuardiansEternalWilds/
│
├─ src/                          # Source code (synced with Rojo)
│  ├─ server/                    # ServerScriptService
│  │  ├─ services/               # Core server systems
│  │  │  ├─ CombatService.lua
│  │  │  ├─ PetService.lua
│  │  │  ├─ EconomyService.lua
│  │  │  ├─ WorldService.lua
│  │  │  └─ DataService.lua
│  │  ├─ modules/                # Shared server modules
│  │  └─ init.server.lua         # Server entry point
│  │
│  ├─ client/                    # StarterPlayer/StarterPlayerScripts
│  │  ├─ controllers/            # Client-side controllers
│  │  │  ├─ CombatController.lua
│  │  │  ├─ PetController.lua
│  │  │  ├─ UIController.lua
│  │  │  └─ InputController.lua
│  │  ├─ modules/                # Client modules
│  │  └─ init.client.lua         # Client entry point
│  │
│  ├─ shared/                    # ReplicatedStorage
│  │  ├─ modules/                # Shared utilities
│  │  │  ├─ Constants.lua        # Game constants
│  │  │  ├─ Types.lua            # Type definitions
│  │  │  ├─ Utils.lua            # Helper functions
│  │  │  └─ Formulas.lua         # Damage/stat calculations
│  │  ├─ data/                   # Static game data
│  │  │  ├─ PetData.lua          # Pet species definitions
│  │  │  ├─ BiomeData.lua        # Biome configurations
│  │  │  └─ ItemData.lua         # Item definitions
│  │  └─ network/                # Network events/functions
│  │     ├─ Events.lua           # RemoteEvents
│  │     └─ Functions.lua        # RemoteFunctions
│  │
│  └─ ui/                        # StarterGui
│     ├─ components/             # Reusable UI components
│     ├─ screens/                # Main UI screens
│     └─ hud/                    # HUD elements
│
├─ assets/                       # Game assets (not synced)
│  ├─ models/                    # 3D models
│  ├─ sounds/                    # Audio files
│  ├─ images/                    # Textures/sprites
│  └─ animations/                # Animation files
│
├─ docs/                         # Design documentation
│  ├─ COMBAT_SYSTEM_DESIGN.md
│  ├─ PET_SYSTEM_DESIGN_DOCUMENT.md
│  ├─ WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md
│  ├─ BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md
│  ├─ ECONOMY_CURRENCY_DESIGN_DOCUMENT.md
│  └─ DEVELOPMENT_ROADMAP.md    # This document
│
├─ tests/                        # Test scripts
│  ├─ unit/                      # Unit tests
│  └─ integration/               # Integration tests
│
├─ default.project.json          # Rojo project file
├─ .gitignore                    # Git ignore rules
├─ README.md                     # Project overview
├─ selene.toml                   # Linter config
└─ stylua.toml                   # Formatter config
```

---

## 📚 DESIGN DOCUMENT REFERENCE GUIDE

### **Quick Reference: Where to Find Specs**

| System | Document | Key Sections |
|--------|----------|--------------|
| **Combat Mechanics** | COMBAT_SYSTEM_DESIGN.md | Timing system, defense actions, combo chains |
| **Pet Stats & Formulas** | PET_SYSTEM_DESIGN_DOCUMENT.md | IV system, stat calculations, leveling |
| **Pet Capture** | PET_SYSTEM_DESIGN_DOCUMENT.md | Capture rates, modifiers |
| **Pet Training** | PET_SYSTEM_DESIGN_DOCUMENT.md | Training costs, time requirements |
| **Pet Breeding** | PET_SYSTEM_DESIGN_DOCUMENT.md | Breeding mechanics, IV inheritance |
| **Pet Merging** | PET_SYSTEM_DESIGN_DOCUMENT.md | Star system, merge costs |
| **Life Stages** | PET_SYSTEM_DESIGN_DOCUMENT.md | Real-time aging, stage bonuses |
| **World Generation** | WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md | Procedural biomes, spawn systems |
| **Biomes** | WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md | Biome types, environmental effects |
| **Dungeons** | WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md | Dungeon architecture, boss encounters |
| **Extraction Zones** | WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md | Safe zones, extraction mechanics |
| **Base Buildings** | BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md | Building types, upgrade costs, functions |
| **Currencies** | ECONOMY_CURRENCY_DESIGN_DOCUMENT.md | Glow Cash, Hype Crystals, earning rates |
| **Materials** | ECONOMY_CURRENCY_DESIGN_DOCUMENT.md | Elemental materials, drop rates |
| **Trading** | ECONOMY_CURRENCY_DESIGN_DOCUMENT.md | Market mechanics, auction house |
| **Multiplayer** | MULTIPLAYER_COMBAT_SYSTEM_DESIGN.md | Co-op, PvPvE, proximity engagement |

### **When You Need Specific Info:**

```
Q: How does pet stat calculation work?
A: PET_SYSTEM_DESIGN_DOCUMENT.md → Section on IV System & Stat Calculations

Q: What are combat damage formulas?
A: COMBAT_SYSTEM_DESIGN.md → Damage Calculation Section

Q: How do I price building upgrades?
A: BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md → Building Upgrade Cost Formula

Q: What's the currency earning rate for expeditions?
A: ECONOMY_CURRENCY_DESIGN_DOCUMENT.md → Glow Cash Earning Rates by Activity

Q: How do biomes spawn enemies?
A: WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md → Enemy Spawn System Section
```

---

# SECTION 2: PHASE 1 - MVP (MONTHS 1-6)

## 🎯 MVP GOALS

**What is MVP (Minimum Viable Product)?**

The absolute minimum features needed to prove the core gameplay loop is fun. If these systems aren't fun, the game won't work—so focus on quality over quantity.

**MVP Success Criteria:**
- [ ] Core combat feels satisfying (timing is rewarding)
- [ ] Capturing pets feels exciting (dopamine hit on success)
- [ ] Progression feels meaningful (levels/upgrades matter)
- [ ] Players want to keep playing (retention hook exists)

**What's NOT in MVP:**
- Multiplayer (single-player only)
- Most buildings (only 2-3 essential ones)
- Most pets (10-20 species is enough)
- Advanced features (breeding, merging, prestige, etc.)
- Polish (placeholder UI is fine)

---

## 📅 MVP MILESTONE 1: CORE COMBAT PROTOTYPE (WEEKS 1-4)

**Goal:** Build the absolute core combat loop. Player fights one enemy using timing-based defense. If this isn't fun, nothing else matters.

### **Week 1: Project Setup & Basic Scene**

**Priority:** CRITICAL  
**Time Estimate:** 20-30 hours  
**Dependencies:** None  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Introduction, Core Mechanics)

#### **Tasks:**

- [ ] **1.1 - Initialize Roblox Project**
  - Create new Roblox place
  - Set up Rojo sync (if using external editor)
  - Create folder structure (see Project Structure above)
  - Initialize Git repository
  - **Acceptance:** Project opens in Roblox Studio, Rojo syncs successfully

- [ ] **1.2 - Create Test Environment**
  - Build simple 100x100 stud flat arena (grass baseplate)
  - Add basic lighting (daytime, minimal shadows)
  - Add spawn point for player
  - **Acceptance:** Player spawns in test arena, can move around

- [ ] **1.3 - Set Up Constants Module**
  - Create `shared/modules/Constants.lua`
  - Define combat constants:
    ```lua
    local Constants = {
        Combat = {
            PERFECT_WINDOW_BASE = 0.15, -- seconds
            GOOD_WINDOW_BASE = 0.35,    -- seconds
            MISS_PENALTY = 0.5,         -- damage multiplier
            PERFECT_BONUS = 1.5,        -- damage multiplier
            SHRINK_TIME_BASE = 2.0,     -- seconds for circle shrink
        },
    }
    return Constants
    ```
  - **Acceptance:** Constants can be imported by other scripts

- [ ] **1.4 - Create Player Combat Controller (Basic)**
  - Create `client/controllers/CombatController.lua`
  - Set up remote events for combat actions
  - Implement basic input handling (mobile tap, PC click)
  - **Acceptance:** Player can trigger combat input (logs to console)

- [ ] **1.5 - Create Enemy NPC (Dummy)**
  - Create simple humanoid NPC (R15 rig)
  - Place enemy 10 studs from player spawn
  - Enemy has basic properties (HP, level)
  - Enemy does NOT move or attack yet (stationary dummy)
  - **Acceptance:** Enemy spawns, is visible, has HP attribute

**End of Week 1 Deliverable:** Empty test arena with player spawn and stationary enemy dummy.

---

### **Week 2: Timing Circle Mechanic**

**Priority:** CRITICAL  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 1 complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Timing System, Perfect/Good/Miss Windows)

#### **Tasks:**

- [ ] **2.1 - Create Combat UI (Timing Circles)**
  - Create ScreenGui in StarterGui
  - Add Frame for combat UI (centered, 300x300 pixels)
  - Create two ImageLabels:
    - Outer circle (static, 250px diameter, white border)
    - Inner circle (shrinking, 250px → 50px, colored border)
  - **Acceptance:** Circles render on screen when combat starts

- [ ] **2.2 - Implement Circle Shrink Animation**
  - Create `client/modules/TimingCircle.lua` module
  - Implement shrink animation using TweenService
  - Shrink from outer → inner over X seconds (from Constants)
  - **Formula:** `Duration = SHRINK_TIME_BASE` (2 seconds for now)
  - **Acceptance:** Circle shrinks smoothly, reaches center in 2 seconds

- [ ] **2.3 - Implement Hit Detection**
  - Detect when player taps/clicks
  - Calculate circle radius at moment of input
  - Determine if input was Perfect/Good/Miss:
    ```lua
    local function CalculateHitQuality(currentRadius, outerRadius)
        local progress = currentRadius / outerRadius -- 0 to 1
        
        if progress <= PERFECT_WINDOW_BASE then
            return "Perfect"
        elseif progress <= GOOD_WINDOW_BASE then
            return "Good"
        else
            return "Miss"
        end
    end
    ```
  - **Acceptance:** Console logs "Perfect", "Good", or "Miss" on input

- [ ] **2.4 - Add Visual Feedback**
  - On hit, show result text (Perfect/Good/Miss)
  - Use different colors:
    - Perfect: Gold (#FFD700)
    - Good: Blue (#4169E1)
    - Miss: Red (#FF6B6B)
  - Add screen flash effect (subtle)
  - **Acceptance:** Player sees immediate feedback on hit quality

- [ ] **2.5 - Add Audio Feedback**
  - Find/create 3 sound effects:
    - Perfect: High-pitched chime (satisfying)
    - Good: Medium chime (decent)
    - Miss: Low buzz (disappointing)
  - Play appropriate sound on each hit
  - **Acceptance:** Audio plays on every hit, sounds distinct

**End of Week 2 Deliverable:** Working timing circle that shrinks, detects hits, shows visual/audio feedback.

---

### **Week 3: Combat Damage & Enemy AI**

**Priority:** CRITICAL  
**Time Estimate:** 30-40 hours  
**Dependencies:** Week 1-2 complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Damage Calculations, Enemy Attack Patterns)

#### **Tasks:**

- [ ] **3.1 - Create Combat Service (Server)**
  - Create `server/services/CombatService.lua`
  - Handle combat state (whose turn, HP tracking)
  - Validate hit quality (server authority)
  - **Acceptance:** Server manages combat state, clients connect

- [ ] **3.2 - Implement Player Damage Calculation**
  - Create `shared/modules/Formulas.lua`
  - Implement damage formula:
    ```lua
    local function CalculatePlayerDamage(attack, defense, hitQuality)
        local baseDamage = attack - (defense * 0.5)
        local multiplier = 1.0
        
        if hitQuality == "Perfect" then
            multiplier = 1.5
        elseif hitQuality == "Good" then
            multiplier = 1.0
        elseif hitQuality == "Miss" then
            multiplier = 0.5
        end
        
        return math.max(1, math.floor(baseDamage * multiplier))
    end
    ```
  - **Acceptance:** Damage calculated correctly, varies by hit quality

- [ ] **3.3 - Implement Enemy Health System**
  - Add HP attribute to enemy NPC
  - Display HP bar above enemy (BillboardGui)
  - Update HP bar on damage
  - Enemy "dies" at 0 HP (disappears, combat ends)
  - **Acceptance:** Enemy HP depletes, dies when reaching 0

- [ ] **3.4 - Implement Enemy Attack Turn**
  - After player attacks, enemy attacks back
  - Enemy attack has 2-second telegraph (warning animation)
  - Player must defend using timing circle
  - If player misses defense, player takes damage
  - **Acceptance:** Turn-based combat works (player → enemy → player)

- [ ] **3.5 - Implement Player Health System**
  - Player has HP (from companion pet eventually, for now just player HP)
  - Add HP bar to HUD (top of screen)
  - Player takes damage on missed defense
  - Player "dies" at 0 HP (respawn, combat ends)
  - **Acceptance:** Player HP system works, respawns on death

**End of Week 3 Deliverable:** Complete turn-based combat loop. Player attacks enemy → Enemy attacks player → Repeat until someone dies.

---

### **Week 4: Combat Polish & Tuning**

**Priority:** HIGH  
**Time Estimate:** 20-30 hours  
**Dependencies:** Week 1-3 complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (All sections)

#### **Tasks:**

- [ ] **4.1 - Add Combat Animations**
  - Player attack animation (swing, punch, etc.)
  - Enemy attack animation (simple lunge)
  - Victory animation (player wins)
  - Defeat animation (player loses)
  - **Acceptance:** Animations play at appropriate times

- [ ] **4.2 - Add Particle Effects**
  - Hit effects (sparks on perfect, puff on good, nothing on miss)
  - Damage numbers (floating text showing damage dealt)
  - Victory effect (confetti/sparkles when enemy dies)
  - **Acceptance:** Effects add juice to combat

- [ ] **4.3 - Add Combo Counter (Basic)**
  - Track consecutive Perfect hits
  - Display combo count on screen
  - Reset combo on Good or Miss
  - Add visual excitement at high combos (5+, 10+)
  - **Acceptance:** Combo counter works, resets properly

- [ ] **4.4 - Playtest & Balance**
  - Test combat with different stats
  - Tune timing windows if too hard/easy
  - Adjust damage formulas for satisfying damage numbers
  - Test on mobile device (touch controls)
  - **Acceptance:** Combat feels fun and fair

- [ ] **4.5 - Add Multiple Enemy Types (2-3)**
  - Create 2-3 different enemy NPCs (different models)
  - Vary stats (HP, attack, defense)
  - Vary shrink speed (harder enemies = faster shrink)
  - **Acceptance:** Fighting different enemies feels distinct

**End of Week 4 Deliverable:** Polished combat prototype with 2-3 enemy types, animations, effects, combo system.

---

## ✅ MVP MILESTONE 1 ACCEPTANCE CRITERIA

**Before moving to Milestone 2, verify:**

- [x] Player can engage in combat with enemy
- [x] Timing circle shrinks smoothly with clear windows
- [x] Perfect/Good/Miss detection works reliably
- [x] Damage calculation uses correct formulas
- [x] Turn-based flow works (player → enemy → repeat)
- [x] Player and enemy HP systems function correctly
- [x] Combat has satisfying audio/visual feedback
- [x] Combo system tracks and displays correctly
- [x] Combat feels fun to repeat (most important!)

**If any of the above fails, do NOT proceed. Fix combat first.**

---

## 📅 MVP MILESTONE 2: PET CAPTURE SYSTEM (WEEKS 5-8)

**Goal:** Add the pet capture mechanic. After defeating enemy, player can attempt to capture it. This is the core progression hook.

### **Week 5: Basic Capture Mechanic**

**Priority:** CRITICAL  
**Time Estimate:** 25-35 hours  
**Dependencies:** Milestone 1 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Capture System)

#### **Tasks:**

- [ ] **5.1 - Create Pet Data Structure**
  - Create `shared/data/PetData.lua`
  - Define pet species data:
    ```lua
    local PetData = {
        ["FireWolf"] = {
            Name = "Fire Wolf",
            Element = "Fire",
            Rarity = "Common",
            BaseCaptureRate = 0.50, -- 50%
            BaseStats = {
                HP = 100,
                Attack = 30,
                Defense = 20,
            },
        },
        -- Add 5-10 species for MVP
    }
    return PetData
    ```
  - **Acceptance:** Pet data is centralized and accessible

- [ ] **5.2 - Implement Capture Attempt UI**
  - After combat victory, show "Capture" button
  - On click, trigger capture attempt
  - Show capture progress UI (loading bar or animation)
  - **Acceptance:** Player can initiate capture after winning

- [ ] **5.3 - Implement Capture Rate Calculation**
  - Create capture formula:
    ```lua
    local function CalculateCaptureRate(baseCaptureRate, modifiers)
        -- Base rate from pet rarity
        local rate = baseCaptureRate
        
        -- Apply item modifiers (none in MVP)
        -- Apply skill tree modifiers (none in MVP)
        
        -- Clamp between 0 and 1
        return math.clamp(rate, 0, 1)
    end
    ```
  - Roll random number (0-1), compare to capture rate
  - **Acceptance:** Capture succeeds/fails based on correct math

- [ ] **5.4 - Handle Capture Success**
  - On success, add pet to player's inventory (simple table for now)
  - Show success animation (pokeball catch animation style)
  - Display "You caught [PetName]!" message
  - Award Glow Cash reward (base: 10 × enemy level)
  - **Acceptance:** Pet is added to inventory, rewards given

- [ ] **5.5 - Handle Capture Failure**
  - On failure, pet escapes
  - Show failure animation (pet breaks free)
  - Award Glow Cash consolation reward (5 × enemy level)
  - Drop loot chest (contains materials)
  - **Acceptance:** Failure feels fair, still gives rewards

**End of Week 5 Deliverable:** Working capture system. Win combat → Attempt capture → Success or Fail → Rewards.

---

### **Week 6: Pet Inventory & Stats**

**Priority:** CRITICAL  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 5 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Pet Stats, IV System)

#### **Tasks:**

- [ ] **6.1 - Create Pet Instance System**
  - Create `shared/modules/PetInstance.lua`
  - Generate unique pet instances with:
    ```lua
    local PetInstance = {
        ID = GenerateUUID(),           -- Unique ID
        SpeciesID = "FireWolf",        -- Reference to PetData
        Level = 1,
        IVs = {                        -- Individual Values (0-31)
            HP = math.random(0, 31),
            Attack = math.random(0, 31),
            Defense = math.random(0, 31),
        },
        CaptureTime = os.time(),       -- When captured
    }
    ```
  - **Acceptance:** Each captured pet is unique with random IVs

- [ ] **6.2 - Implement Stat Calculation**
  - Create stat calculation formula:
    ```lua
    local function CalculateStat(baseStat, IV, level)
        local stat = math.floor(((2 * baseStat + IV) * level / 100) + 5)
        return stat
    end
    ```
  - Calculate final stats for pet instance
  - **Acceptance:** Stats calculated correctly, scale with level/IVs

- [ ] **6.3 - Create Pet Inventory UI**
  - Create ScreenGui for pet collection
  - Display list of captured pets
  - Show pet species, level, stats
  - Allow scrolling (pagination if many pets)
  - **Acceptance:** Player can view all captured pets

- [ ] **6.4 - Create Pet Detail View**
  - Click pet in inventory → Show detail screen
  - Display full stats, IVs, element, rarity
  - Show 3D model preview of pet
  - **Acceptance:** Player can inspect individual pets

- [ ] **6.5 - Implement Active Companion Slot**
  - Player can select 1 pet as "Active Companion"
  - Active companion appears in overworld with player
  - Active companion's stats used in combat (not player's)
  - **Acceptance:** Player can equip/unequip companions

**End of Week 6 Deliverable:** Pet inventory system with stat display, companion slot, unique pet instances with IVs.

---

### **Week 7: Companion Combat Integration**

**Priority:** HIGH  
**Time Estimate:** 20-30 hours  
**Dependencies:** Week 5-6 complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Companion System)

#### **Tasks:**

- [ ] **7.1 - Companion Follows Player**
  - Active companion spawns near player
  - Companion follows player using pathfinding
  - Companion stays within 10 studs of player
  - **Acceptance:** Companion follows player smoothly

- [ ] **7.2 - Companion Enters Combat**
  - When player engages enemy, companion is visible in combat
  - Companion HP bar replaces player HP bar (hybrid system)
  - Companion stats used in damage calculations
  - **Acceptance:** Companion participates in combat

- [ ] **7.3 - Implement Companion Damage Absorption**
  - Enemy attacks hit companion, not player
  - Companion absorbs damage using its HP
  - If companion HP reaches 0, companion "faints"
  - **Acceptance:** Companion takes damage intended for player

- [ ] **7.4 - Implement Companion Fainting**
  - At 0 HP, companion faints (falls down animation)
  - After faint, player HP is used for remaining combat
  - After combat, companion auto-revives at 50% HP
  - **Acceptance:** Faint system works, companion revives

- [ ] **7.5 - Add Companion Attack Animations**
  - Companion performs attack animation on player's turn
  - Different animations per element type
  - Attacks feel impactful (screen shake, effects)
  - **Acceptance:** Companion attacks feel satisfying

**End of Week 7 Deliverable:** Companion system integrated with combat. Companion follows player, fights alongside, takes damage.

---

### **Week 8: Capture Polish & Multiple Species**

**Priority:** MEDIUM  
**Time Estimate:** 20-30 hours  
**Dependencies:** Week 5-7 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Species Variety)

#### **Tasks:**

- [ ] **8.1 - Add 10-15 Pet Species**
  - Create data for 10-15 unique species
  - Vary elements (Fire, Water, Earth, Wind, Lightning)
  - Vary rarities (Common, Uncommon, Rare)
  - Vary stats (Tank, DPS, Balanced archetypes)
  - **Acceptance:** 10-15 distinct species available

- [ ] **8.2 - Create 3D Models for Pets**
  - Model 10-15 pet species (can use simple models)
  - Add basic animations (idle, walk, attack)
  - Import models to Roblox
  - **Acceptance:** All pets have visual models

- [ ] **8.3 - Add Rarity-Based Capture Rates**
  - Common: 50% base capture rate
  - Uncommon: 30% base capture rate
  - Rare: 15% base capture rate
  - Epic: 5% base capture rate (if any in MVP)
  - **Acceptance:** Rarer pets are harder to catch

- [ ] **8.4 - Add Capture Items (Basic)**
  - Create "Standard Ball" item (no modifier, free)
  - Create "Great Ball" item (+10% capture rate, costs Glow Cash)
  - Player can select ball before capture attempt
  - **Acceptance:** Items affect capture rate

- [ ] **8.5 - Add Collection Tracker**
  - Show "Species Seen: X / 15"
  - Show "Species Captured: Y / 15"
  - Mark species as "Seen" after first encounter
  - Mark species as "Captured" after first capture
  - **Acceptance:** Collection progress tracked

**End of Week 8 Deliverable:** 10-15 unique pet species, rarity-based capture rates, capture items, collection tracking.

---

## ✅ MVP MILESTONE 2 ACCEPTANCE CRITERIA

**Before moving to Milestone 3, verify:**

- [x] Pet capture works after winning combat
- [x] Capture rate calculation is correct
- [x] Success/failure both give appropriate rewards
- [x] Pet inventory displays all captured pets
- [x] Pet instances have unique IVs and stats
- [x] Player can equip companion pet
- [x] Companion follows player in overworld
- [x] Companion participates in combat correctly
- [x] 10-15 unique pet species exist
- [x] Collection tracker works

---

## 📅 MVP MILESTONE 3: BASIC PROGRESSION (WEEKS 9-12)

**Goal:** Add leveling and basic upgrade systems. Players need to feel progression over time.

### **Week 9: Pet Leveling System**

**Priority:** CRITICAL  
**Time Estimate:** 25-35 hours  
**Dependencies:** Milestone 2 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Training System)

#### **Tasks:**

- [ ] **9.1 - Implement XP System**
  - Pets gain XP from combat
  - XP formula: `XP Gained = Enemy Level × 10 × Rarity Multiplier`
  - Track XP per pet instance
  - **Acceptance:** Pets accumulate XP after combat

- [ ] **9.2 - Implement Leveling Formula**
  - XP required for next level:
    ```lua
    local function XPForLevel(level)
        return math.floor(100 * (level ^ 1.5))
    end
    ```
  - Pet levels up when XP >= XP required
  - Max level: 100 (for MVP)
  - **Acceptance:** Pets level up at correct XP thresholds

- [ ] **9.3 - Implement Stat Scaling**
  - Recalculate stats on level up
  - Use formula from Week 6 (includes level parameter)
  - Display stat increases ("+3 Attack!")
  - **Acceptance:** Stats increase with level

- [ ] **9.4 - Add Level Up Notification**
  - Show level up animation (flash, sparkles)
  - Display new level and stat gains
  - Play level up sound effect
  - **Acceptance:** Level ups feel satisfying

- [ ] **9.5 - Add XP Bar to HUD**
  - Show active companion's current XP / XP to next level
  - XP bar fills as pet gains XP
  - XP bar resets on level up
  - **Acceptance:** XP progress is always visible

**End of Week 9 Deliverable:** Pets gain XP, level up, stats increase with level.

---

### **Week 10: Player Account Leveling**

**Priority:** HIGH  
**Time Estimate:** 20-30 hours  
**Dependencies:** Week 9 complete  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Unlock Gates)

#### **Tasks:**

- [ ] **10.1 - Implement Player Account Level**
  - Separate from pet level (account-wide)
  - Player gains Account XP from activities
  - Account Level unlocks features/buildings
  - **Acceptance:** Player account levels independently

- [ ] **10.2 - Account XP Sources**
  - Complete expedition: 100 Account XP
  - Capture pet: 50 Account XP
  - Defeat enemy: 10 Account XP × Rarity
  - Level up pet: 25 Account XP
  - **Acceptance:** Account XP earned from multiple sources

- [ ] **10.3 - Account Level Rewards**
  - Level 5: Unlock Weaponsmith building
  - Level 10: Unlock Training Station building
  - Level 15: Unlock Workshop building
  - Level 20: Unlock second companion slot (future)
  - **Acceptance:** Features unlock at correct levels

- [ ] **10.4 - Create Profile UI**
  - Display player name, account level, account XP
  - Show unlocked features
  - Show total stats (pets captured, battles won, etc.)
  - **Acceptance:** Player can view profile

- [ ] **10.5 - Add Account Level Notifications**
  - Show notification on account level up
  - List newly unlocked features
  - Encourage player to try new features
  - **Acceptance:** Player knows when they unlock something

**End of Week 10 Deliverable:** Player account leveling system, feature unlocks at specific levels.

---

### **Week 11: Currency & Basic Economy**

**Priority:** CRITICAL  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 9-10 complete  
**Design Doc:** ECONOMY_CURRENCY_DESIGN_DOCUMENT.md (Glow Cash)

#### **Tasks:**

- [ ] **11.1 - Implement Glow Cash System**
  - Create currency data store
  - Track Glow Cash per player
  - Display Glow Cash in HUD (top-right corner)
  - **Acceptance:** Glow Cash tracked and displayed

- [ ] **11.2 - Glow Cash Earning Sources**
  - Defeat enemy: 10 × Enemy Level
  - Capture pet: 20 × Pet Level
  - Complete expedition: 100 × Depth Reached
  - Open chest: Random 50-200 Glow Cash
  - **Acceptance:** Players earn Glow Cash from activities

- [ ] **11.3 - Create Shop UI**
  - Simple vendor NPC at spawn
  - Shop UI displays purchasable items
  - Show item name, cost, description
  - **Acceptance:** Shop UI functional

- [ ] **11.4 - Add Basic Shop Items**
  - Health Potion: 100 Glow Cash (restore 25% HP)
  - Great Ball: 500 Glow Cash (+10% capture rate)
  - Revive: 200 Glow Cash (revive fainted companion)
  - Common Materials: 10 Glow Cash each
  - **Acceptance:** Items purchasable with Glow Cash

- [ ] **11.5 - Implement Item Inventory**
  - Track owned items
  - Display item inventory UI
  - Allow item usage (consume on use)
  - **Acceptance:** Players can buy, own, and use items

**End of Week 11 Deliverable:** Glow Cash economy, shop system, basic purchasable items.

---

### **Week 12: First Building - Weaponsmith**

**Priority:** HIGH  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 9-11 complete  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Weaponsmith)

#### **Tasks:**

- [ ] **12.1 - Create Base Building System**
  - Create instanced personal base (separate from overworld)
  - Player can teleport to base via NPC/button
  - Base has 16 building plots (grid layout)
  - **Acceptance:** Player has personal base instance

- [ ] **12.2 - Implement Weaponsmith Building**
  - Place Weaponsmith building on plot
  - Building has 10 upgrade levels
  - Each level increases crafting capabilities
  - **Acceptance:** Weaponsmith building exists

- [ ] **12.3 - Weapon Crafting System**
  - Create crafting UI (shows available recipes)
  - Weapons increase companion attack stat
  - Recipes require materials + Glow Cash
  - Example: "Iron Sword" - 50 Iron + 5,000 Glow Cash → +10 Attack
  - **Acceptance:** Players can craft weapons

- [ ] **12.4 - Equipment System**
  - Pets can equip 1 weapon
  - Weapon stats added to pet's base stats
  - Show equipped weapon in pet detail UI
  - **Acceptance:** Weapons boost pet stats

- [ ] **12.5 - Building Upgrade System**
  - Spend Glow Cash + materials to upgrade building
  - Upgrade takes time (5 minutes → 24 hours for higher levels)
  - Each level unlocks better recipes
  - **Acceptance:** Weaponsmith upgradable

**End of Week 12 Deliverable:** Personal base instance, Weaponsmith building, weapon crafting, equipment system.

---

## ✅ MVP MILESTONE 3 ACCEPTANCE CRITERIA

**Before moving to Milestone 4, verify:**

- [x] Pets gain XP and level up
- [x] Stats increase with pet level
- [x] Player account levels up independently
- [x] Features unlock at specific account levels
- [x] Glow Cash is earned and spent correctly
- [x] Shop sells basic items
- [x] Player has personal base instance
- [x] Weaponsmith building exists and functions
- [x] Weapons can be crafted and equipped
- [x] Building upgrades work with time/cost requirements

---

## 📅 MVP MILESTONE 4: WORLD BASICS (WEEKS 13-18)

**Goal:** Create the open world exploration foundation. Players need a world to explore, not just a test arena.

### **Week 13-14: Basic Biome System**

**Priority:** CRITICAL  
**Time Estimate:** 40-50 hours  
**Dependencies:** Milestone 3 complete  
**Design Doc:** WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md (Biome System)

#### **Tasks:**

- [ ] **13.1 - Create Base Hub Area**
  - Build safe spawn area (200x200 studs)
  - Add spawn point, NPC vendors, base portal
  - Add basic decorations (trees, rocks, buildings)
  - **Acceptance:** Safe hub area exists

- [ ] **13.2 - Create First Biome (Forest)**
  - Generate 500x500 stud forest biome
  - Use terrain tools (grass, trees)
  - Add decorative assets (rocks, bushes, flowers)
  - Add lighting/atmosphere (soft green tint)
  - **Acceptance:** Forest biome is explorable

- [ ] **13.3 - Create Second Biome (Badlands)**
  - Generate 500x500 stud desert/badlands biome
  - Use terrain tools (sand, rocks)
  - Add decorative assets (cacti, boulders, dead trees)
  - Add lighting/atmosphere (warm orange tint)
  - **Acceptance:** Badlands biome is explorable

- [ ] **13.4 - Implement Biome Transitions**
  - Create gradient between biomes (50-stud transition zone)
  - Blend terrain types (grass → sand)
  - Blend decorations (fewer trees near desert)
  - **Acceptance:** Transitions feel natural

- [ ] **13.5 - Add Distance Tracking**
  - Track player distance from base hub
  - Display distance in HUD (e.g., "1,234m from Base")
  - Distance affects rewards (deeper = better)
  - **Acceptance:** Distance tracked and displayed

**End of Week 14 Deliverable:** Base hub + 2 explorable biomes (Forest, Badlands) with transitions and distance tracking.

---

### **Week 15-16: Enemy Spawning System**

**Priority:** CRITICAL  
**Time Estimate:** 35-45 hours  
**Dependencies:** Week 13-14 complete  
**Design Doc:** WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md (Enemy Spawn System)

#### **Tasks:**

- [ ] **15.1 - Create Spawn Region System**
  - Define spawn regions in each biome
  - Regions have spawn rate, enemy pool
  - Regions spawn enemies when player nearby
  - **Acceptance:** Enemies spawn in designated regions

- [ ] **15.2 - Implement Enemy Pool per Biome**
  - Forest biome: Nature/Wind element pets
  - Badlands biome: Fire/Earth element pets
  - Each biome has 5-8 unique species
  - **Acceptance:** Biomes have distinct pet pools

- [ ] **15.3 - Implement Rarity-Based Spawning**
  - Common: 70% spawn rate
  - Uncommon: 20% spawn rate
  - Rare: 9% spawn rate
  - Epic: 1% spawn rate
  - **Acceptance:** Rarer pets spawn less frequently

- [ ] **15.4 - Implement Level Scaling**
  - Enemy level scales with distance from base
  - Formula: `Enemy Level = 1 + (Distance / 100)`
  - Example: 500m from base = Level 6 enemies
  - Cap at Level 20 for MVP
  - **Acceptance:** Enemy difficulty increases with depth

- [ ] **15.5 - Add Enemy AI (Roaming)**
  - Enemies roam within spawn region
  - Enemies use pathfinding to navigate terrain
  - Enemies idle/patrol when no player nearby
  - **Acceptance:** Enemies move naturally

- [ ] **15.6 - Add Aggro System**
  - Enemies aggro when player within 50 studs
  - Aggro'd enemies chase player
  - Combat initiates on collision (10 studs)
  - **Acceptance:** Players can engage enemies

**End of Week 16 Deliverable:** Enemies spawn in biomes, scale with depth, roam/aggro/engage players.

---

### **Week 17: Loot Chests & Resources**

**Priority:** HIGH  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 13-16 complete  
**Design Doc:** WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md (Loot System)

#### **Tasks:**

- [ ] **17.1 - Create Chest System**
  - Spawn chests randomly in biomes
  - Chests have rarity (Common, Uncommon, Rare)
  - Chests glow/sparkle (visible from distance)
  - **Acceptance:** Chests spawn and are visible

- [ ] **17.2 - Implement Chest Opening**
  - Player approaches chest → "Open" prompt
  - Opening takes 2 seconds (progress bar)
  - Chest despawns after opening
  - **Acceptance:** Players can open chests

- [ ] **17.3 - Implement Loot Tables**
  - Common chest: 100-500 Glow Cash + Common materials
  - Uncommon chest: 500-1,500 Glow Cash + Uncommon materials
  - Rare chest: 2,000-5,000 Glow Cash + Rare materials
  - **Acceptance:** Chests drop appropriate loot

- [ ] **17.4 - Create Material Drop System**
  - Materials drop from enemies and chests
  - Materials are element-specific (Fire materials in Badlands, etc.)
  - Materials used for crafting/building upgrades
  - **Acceptance:** Materials drop and are collectible

- [ ] **17.5 - Add Mining Nodes (Basic)**
  - Place Stone/Iron nodes in biomes
  - Player can harvest nodes (3-second channel)
  - Nodes respawn after 10 minutes
  - **Acceptance:** Resource gathering works

**End of Week 17 Deliverable:** Loot chests spawn, materials drop from enemies/chests/nodes, resource gathering system.

---

### **Week 18: Extraction Zone & Expedition Loop**

**Priority:** CRITICAL  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 13-17 complete  
**Design Doc:** WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md (Extraction System)

#### **Tasks:**

- [ ] **18.1 - Create Extraction Zone**
  - Designate safe zone at base hub
  - Extraction zone has glowing boundary (green)
  - Extraction zone is always safe (no combat)
  - **Acceptance:** Extraction zone clearly marked

- [ ] **18.2 - Implement Inventory Persistence**
  - Captured pets, items, currency saved when extracting
  - If player dies in world, loses everything (permadeath)
  - Player must return to extraction zone to save progress
  - **Acceptance:** Extraction saves progress

- [ ] **18.3 - Add Extraction Button/NPC**
  - In extraction zone, player can click "Extract" button
  - Extraction teleports player back to base
  - Show summary screen (pets captured, Glow Cash earned, XP gained)
  - **Acceptance:** Extraction completes expedition

- [ ] **18.4 - Implement Expedition Start**
  - Player clicks "Start Expedition" at base
  - Player teleports to world spawn point
  - New expedition instance generated (fresh state)
  - **Acceptance:** Expeditions can be started

- [ ] **18.5 - Add Risk/Reward Tension**
  - The deeper player goes, the better rewards
  - But also more risk of dying and losing everything
  - Add UI indicator showing unextracted loot value
  - **Acceptance:** Players feel tension (when to extract?)

**End of Week 18 Deliverable:** Complete expedition loop. Start expedition → Explore → Capture pets → Extract safely → Repeat.

---

## ✅ MVP MILESTONE 4 ACCEPTANCE CRITERIA

**Before moving to Milestone 5, verify:**

- [x] Base hub exists with safe zone
- [x] 2 explorable biomes (Forest, Badlands)
- [x] Enemies spawn in biomes with correct pools
- [x] Enemy difficulty scales with distance
- [x] Loot chests spawn and give rewards
- [x] Materials drop from enemies/chests/nodes
- [x] Extraction zone saves progress
- [x] Permadeath works (lose unextracted loot on death)
- [x] Complete expedition loop works
- [x] Players feel risk/reward tension

---

## 📅 MVP MILESTONE 5: ECONOMY FOUNDATION (WEEKS 19-24)

**Goal:** Expand economy with materials, more buildings, and currency sinks.

### **Week 19-20: Material System & Refinery**

**Priority:** HIGH  
**Time Estimate:** 35-45 hours  
**Dependencies:** Milestone 4 complete  
**Design Doc:** ECONOMY_CURRENCY_DESIGN_DOCUMENT.md (Materials System)

#### **Tasks:**

- [ ] **19.1 - Implement Elemental Material Tiers**
  - Create 5 tiers per element (Common → Legendary)
  - Example Fire: Ember Shard, Fire Crystal, Magma Core, Inferno Essence, Eternal Flame
  - Materials drop based on enemy rarity
  - **Acceptance:** All material tiers defined

- [ ] **19.2 - Create Material Inventory UI**
  - Show all owned materials organized by element
  - Display material count and storage limits
  - Show material icons and descriptions
  - **Acceptance:** Players can view material inventory

- [ ] **19.3 - Implement Material Conversion (Upconversion)**
  - 10 lower-tier → 1 higher-tier (+ 1,000 Glow Cash fee)
  - Example: 10 Ember Shard → 1 Fire Crystal
  - Conversion happens via Refinery building
  - **Acceptance:** Materials can be converted up

- [ ] **19.4 - Create Refinery Building**
  - Place Refinery on plot (unlock at Account Level 25)
  - Refinery allows material conversion
  - Higher levels reduce conversion cost
  - **Acceptance:** Refinery building functional

- [ ] **19.5 - Add Universal Resources**
  - Stone (common), Iron (uncommon), Crystal (rare)
  - Used for building upgrades (not element-specific)
  - Gathered from mining nodes
  - **Acceptance:** Universal resources exist

**End of Week 20 Deliverable:** Material system with 5 tiers per element, material conversion, Refinery building, universal resources.

---

### **Week 21: Training Station & Pet Training**

**Priority:** HIGH  
**Time Estimate:** 30-40 hours  
**Dependencies:** Week 19-20 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Training System), BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Training Station)

#### **Tasks:**

- [ ] **21.1 - Create Training Station Building**
  - Unlock at Account Level 12
  - Building has 10 upgrade levels
  - Each level increases training slots and speed
  - **Acceptance:** Training Station building exists

- [ ] **21.2 - Implement Training Queue System**
  - Players assign pets to training slots
  - Training takes real-world time (passive)
  - Training grants XP while offline
  - **Acceptance:** Pets train passively

- [ ] **21.3 - Training Cost Formula**
  - Training costs Glow Cash + materials
  - Cost formula:
    ```lua
    local function TrainingCost(petLevel, targetLevel)
        local baseCost = 1000
        local levelsToTrain = targetLevel - petLevel
        return baseCost * levelsToTrain
    end
    ```
  - **Acceptance:** Training costs calculated correctly

- [ ] **21.4 - Training Time Formula**
  - Training time scales with levels
  - Formula: `Time (hours) = (Target Level - Current Level) × 0.5`
  - Example: Level 10 → 20 = 5 hours
  - **Acceptance:** Training completes on schedule

- [ ] **21.5 - Add Training Notifications**
  - Notify player when training completes (in-game)
  - Show level gained and new stats
  - Allow instant collection from Training Station
  - **Acceptance:** Players notified of completed training

**End of Week 21 Deliverable:** Training Station building, passive pet training system with real-time progression.

---

### **Week 22: Workshop & Consumables**

**Priority:** MEDIUM  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 19-21 complete  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Workshop)

#### **Tasks:**

- [ ] **22.1 - Create Workshop Building**
  - Unlock at Account Level 15
  - Building has 10 upgrade levels
  - Each level unlocks more recipes
  - **Acceptance:** Workshop building exists

- [ ] **22.2 - Implement Consumable Crafting**
  - Craft consumables (potions, boosts)
  - Consumables are single-use items
  - Crafting requires materials + Glow Cash
  - **Acceptance:** Consumables craftable

- [ ] **22.3 - Create Consumable Recipes**
  - Health Potion: 5 Common materials + 100 Glow Cash
  - Capture Boost: 15 Uncommon materials + 500 Glow Cash
  - XP Boost: 25 Rare materials + 1,000 Glow Cash
  - Loot Boost: 50 Epic materials + 2,500 Glow Cash
  - **Acceptance:** 5-10 consumable recipes exist

- [ ] **22.4 - Implement Consumable Effects**
  - Health Potion: Restore 25% HP in combat
  - Capture Boost: +10% capture rate (1 hour)
  - XP Boost: +25% XP (1 hour)
  - Loot Boost: +50% loot quality (1 hour)
  - **Acceptance:** Consumables work as intended

- [ ] **22.5 - Add Buff Indicator UI**
  - Show active buffs in HUD (icons + timer)
  - Buffs stack duration (using 2 = 2 hours)
  - Buffs expire after time limit
  - **Acceptance:** Players see active buffs

**End of Week 22 Deliverable:** Workshop building, consumable crafting, buffs/boosts system.

---

### **Week 23: Armorsmith & Defense Gear**

**Priority:** MEDIUM  
**Time Estimate:** 20-30 hours  
**Dependencies:** Week 19-22 complete  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Armorsmith)

#### **Tasks:**

- [ ] **23.1 - Create Armorsmith Building**
  - Unlock at Account Level 18
  - Similar structure to Weaponsmith
  - Each level unlocks better armor recipes
  - **Acceptance:** Armorsmith building exists

- [ ] **23.2 - Implement Armor Crafting**
  - Craft armor pieces (helmet, chest, etc.)
  - Armor increases companion defense stat
  - Recipes require materials + Glow Cash
  - **Acceptance:** Armor craftable

- [ ] **23.3 - Add Armor Equipment Slots**
  - Pets can equip: 1 weapon + 1 armor
  - Show equipped gear in pet detail UI
  - Gear stats added to pet's base stats
  - **Acceptance:** Armor can be equipped

- [ ] **23.4 - Create Armor Progression Tiers**
  - Common armor: +5 Defense (cheap)
  - Uncommon armor: +10 Defense
  - Rare armor: +20 Defense
  - Epic armor: +40 Defense
  - **Acceptance:** Armor tiers scale correctly

- [ ] **23.5 - Add Gear Comparison UI**
  - Show before/after stats when equipping gear
  - Highlight stat changes (green = better, red = worse)
  - Allow quick-equip from inventory
  - **Acceptance:** Gear comparison helpful

**End of Week 23 Deliverable:** Armorsmith building, armor crafting, defense gear equipment.

---

### **Week 24: Warehouse & Storage Expansion**

**Priority:** LOW  
**Time Estimate:** 15-25 hours  
**Dependencies:** Week 19-23 complete  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Warehouse)

#### **Tasks:**

- [ ] **24.1 - Create Warehouse Building**
  - Unlock at Account Level 8
  - Building has 10 upgrade levels
  - Each level increases storage capacity
  - **Acceptance:** Warehouse building exists

- [ ] **24.2 - Implement Storage Limits**
  - Default storage: 1,000 items total
  - Storage includes materials, items, gear
  - Pets have separate storage (unlimited for MVP)
  - **Acceptance:** Storage limits enforced

- [ ] **24.3 - Storage Upgrade System**
  - Level 1: 1,000 items
  - Level 5: 2,500 items
  - Level 10: 5,000 items
  - Each level costs Glow Cash + materials
  - **Acceptance:** Warehouse upgrades increase storage

- [ ] **24.4 - Add Storage Full Warning**
  - Warn player when storage >90% full
  - Prevent looting if storage full
  - Suggest upgrading Warehouse
  - **Acceptance:** Players notified of storage issues

- [ ] **24.5 - Add Item Selling**
  - Sell unwanted items to NPC vendor
  - Sell price = 50% of buy price
  - Quick-sell option for bulk sales
  - **Acceptance:** Players can sell excess items

**End of Week 24 Deliverable:** Warehouse building, storage limits, inventory management, item selling.

---

## ✅ MVP MILESTONE 5 ACCEPTANCE CRITERIA

**Before moving to Phase 2 (Alpha), verify:**

- [x] Material system with tiers works
- [x] Material conversion (upconversion) functional
- [x] Refinery building allows conversions
- [x] Training Station enables passive training
- [x] Workshop crafts consumables
- [x] Consumables provide buffs
- [x] Armorsmith crafts armor
- [x] Armor can be equipped and boosts defense
- [x] Warehouse manages storage limits
- [x] Players can sell excess items

---

## 🎉 MVP PHASE COMPLETE!

**Congratulations!** You've built a functional MVP with:
- ✅ Combat system (timing-based, satisfying)
- ✅ Pet capture system (15+ species)
- ✅ Pet progression (leveling, stats, IVs)
- ✅ Companion system (follows player, fights)
- ✅ Account progression (levels unlock features)
- ✅ Economy (Glow Cash, materials, shops)
- ✅ World exploration (2 biomes, enemies, chests)
- ✅ Extraction loop (risk/reward tension)
- ✅ Base building (5 buildings, crafting, training)

**Next Steps:**
1. **Internal Playtesting** - Test with friends/family
2. **Balance Tuning** - Adjust numbers based on feedback
3. **Bug Fixing** - Fix critical issues before alpha
4. **Performance Testing** - Ensure 60 FPS on mobile

**After MVP is Stable:**
- Move to **Phase 2: Alpha** (expand systems)
- Add multiplayer, advanced pet systems, more content
- Prepare for closed alpha testing

---

# SECTION 3: PHASE 2 - ALPHA (MONTHS 7-12)

## 🎯 ALPHA GOALS

**What is Alpha?**

Alpha expands the MVP into a complete vertical slice. All core systems are polished and expanded. The game should feel "feature-complete" even if content is limited.

**Alpha Success Criteria:**
- [ ] All core systems polished (no placeholder art/UI)
- [ ] Advanced pet systems work (breeding, merging, life stages)
- [ ] Full base building (20 buildings, automation)
- [ ] World generation (procedural biomes, dungeons)
- [ ] Multiplayer foundation (Co-op expeditions)
- [ ] Ready for closed alpha testing with 50-100 players

**What's NOT in Alpha:**
- PvPvE (comes in Beta)
- Full event system (comes in Beta)
- Leaderboards (comes in Beta)
- Polish/optimization (comes in Beta)

---

## 📅 ALPHA MILESTONE 1: COMBAT POLISH (WEEKS 25-30)

**Goal:** Polish combat to AAA quality. Add advanced mechanics, multiple defense actions, combos, visual effects.

### **Week 25-26: Defense Action Variety**

**Priority:** HIGH  
**Time Estimate:** 35-45 hours  
**Dependencies:** MVP complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Defense Actions)

#### **Tasks:**

- [ ] **25.1 - Implement Three Defense Actions**
  - Dodge: Avoid damage entirely, no counterattack
  - Block: Reduce damage by 50%, no counterattack
  - Counter: Full damage taken, but counterattack deals 2x damage
  - **Acceptance:** All 3 defense actions available

- [ ] **25.2 - Add Defense Action Selection UI**
  - Show 3 buttons during enemy attack turn
  - Player selects Dodge/Block/Counter before timing circle
  - Selected action determines circle color and effect
  - **Acceptance:** Players can choose defense action

- [ ] **25.3 - Implement Action-Specific Timing**
  - Dodge: Smallest window (hardest)
  - Block: Medium window (moderate)
  - Counter: Largest window (easiest) but takes damage
  - **Acceptance:** Different actions have different difficulties

- [ ] **25.4 - Add Counterattack Mechanic**
  - On Perfect Counter, companion instantly counterattacks
  - Counterattack deals 2x normal damage
  - Counterattack uses unique animation
  - **Acceptance:** Counter defense works correctly

- [ ] **25.5 - Balance Defense Actions**
  - Test all 3 actions for viability
  - Ensure no single action is always best
  - Situational choices (low HP = block, high HP = counter)
  - **Acceptance:** All 3 actions are useful

**End of Week 26 Deliverable:** Three distinct defense actions (Dodge/Block/Counter) with different timing windows.

---

### **Week 27: Combo System Expansion**

**Priority:** MEDIUM  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 25-26 complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Combo System)

#### **Tasks:**

- [ ] **27.1 - Implement Combo Multipliers**
  - Combo 5+: +10% damage
  - Combo 10+: +25% damage
  - Combo 20+: +50% damage
  - Combo 50+: +100% damage
  - **Acceptance:** Damage scales with combo count

- [ ] **27.2 - Add Combo Visual Escalation**
  - Combo 1-4: Normal effects
  - Combo 5-9: Screen shake, particles
  - Combo 10-19: More particles, color shifts
  - Combo 20+: Screen flash, intense effects
  - **Acceptance:** High combos feel epic

- [ ] **27.3 - Add Combo Sound Escalation**
  - Different sound effects at combo milestones
  - Higher combos = higher pitched, more intense
  - "COMBO BREAK!" sound on combo reset
  - **Acceptance:** Audio feedback scales with combo

- [ ] **27.4 - Add Combo Rewards**
  - Bonus Glow Cash at end of combat (based on max combo)
  - Formula: `Bonus = Max Combo × 10 Glow Cash`
  - Show combo bonus in victory screen
  - **Acceptance:** High combos feel rewarding

- [ ] **27.5 - Add Combo Leaderboard (Local)**
  - Track player's highest combo (account-wide)
  - Display in profile UI
  - Set goal for players to beat their record
  - **Acceptance:** Combo records tracked

**End of Week 27 Deliverable:** Combo system with multipliers, escalating effects, and rewards.

---

### **Week 28-30: Combat Enemy Variety**

**Priority:** HIGH  
**Time Estimate:** 45-60 hours  
**Dependencies:** Week 25-27 complete  
**Design Doc:** COMBAT_SYSTEM_DESIGN.md (Enemy Types, Attack Patterns)

#### **Tasks:**

- [ ] **28.1 - Implement Multi-Hit Attack Patterns**
  - Some enemies attack 2-3 times per turn
  - Each hit requires separate timing circle
  - Miss one = break combo, take damage
  - **Acceptance:** Multi-hit enemies work

- [ ] **28.2 - Implement Combo Requirement Attacks**
  - Some Epic+ enemies require button combos (A+B+C)
  - Random button sequence shown before attack
  - Player must input correct sequence with timing
  - **Acceptance:** Combo attacks functional

- [ ] **28.3 - Add Status Effects (Basic)**
  - Burn: 5% HP damage per turn (3 turns)
  - Poison: 3% HP damage per turn (5 turns)
  - Slow: -20% timing window (2 turns)
  - **Acceptance:** Status effects apply and tick

- [ ] **28.4 - Add Enemy Special Abilities**
  - Some enemies heal on certain turns
  - Some enemies buff themselves (+attack)
  - Some enemies summon adds (additional enemies)
  - **Acceptance:** Special abilities work

- [ ] **28.5 - Create 10+ New Enemy Types**
  - Variety of rarities (Common → Legendary)
  - Variety of elements
  - Variety of attack patterns
  - **Acceptance:** 20-30 unique enemy types total

- [ ] **28.6 - Balance Enemy Difficulty Curve**
  - Test all enemy types at various levels
  - Ensure difficulty scales smoothly with depth
  - Legendary enemies feel challenging but fair
  - **Acceptance:** Difficulty curve feels good

**End of Week 30 Deliverable:** Advanced combat with multi-hit attacks, combos, status effects, special abilities, 20-30 unique enemies.

---

## ✅ ALPHA MILESTONE 1 ACCEPTANCE CRITERIA

**Before moving to Milestone 2, verify:**

- [x] Three defense actions (Dodge/Block/Counter) functional
- [x] Defense actions have distinct use cases
- [x] Combo system provides meaningful bonuses
- [x] Combo visual/audio escalation feels epic
- [x] Multi-hit attack patterns work
- [x] Button combo attacks functional
- [x] Status effects apply and tick correctly
- [x] Enemy special abilities functional
- [x] 20-30 unique enemy types exist
- [x] Combat feels polished and satisfying

---

## 📅 ALPHA MILESTONE 2: FULL PET SYSTEM (WEEKS 31-36)

**Goal:** Implement all advanced pet systems: breeding, merging, life stages, friendship.

### **Week 31-32: Breeding System**

**Priority:** HIGH  
**Time Estimate:** 40-50 hours  
**Dependencies:** Alpha M1 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Breeding & Fusion System)

#### **Tasks:**

- [ ] **31.1 - Create Breeding Station Building**
  - Unlock at Account Level 30
  - Building has 10 upgrade levels
  - Each level adds breeding slots and features
  - **Acceptance:** Breeding Station exists

- [ ] **31.2 - Implement Breeding Mechanic**
  - Select 2 adult pets as parents
  - Breeding costs Glow Cash (based on rarity)
  - Breeding takes 24-72 hours (real time)
  - Result: Pet Egg
  - **Acceptance:** Breeding produces eggs

- [ ] **31.3 - Implement IV Inheritance**
  - Child inherits 3 random IVs from each parent
  - Formula:
    ```lua
    local function InheritIVs(parent1, parent2)
        local childIVs = {}
        -- Randomly pick 3 stats from parent 1, 3 from parent 2
        local stats = {"HP", "Attack", "Defense"}
        -- Shuffle and split
        return childIVs
    end
    ```
  - **Acceptance:** IV inheritance works

- [ ] **31.4 - Implement Breeding Sterility**
  - Both parents become sterile after breeding
  - Sterile pets cannot breed again (permanent)
  - UI clearly shows sterile status
  - **Acceptance:** Sterility prevents infinite breeding

- [ ] **31.5 - Add Hybrid Breeding**
  - Cross-element breeding creates hybrids
  - Example: Fire + Water = Steam element pet
  - Hybrid rate: 15% for matching rarities
  - **Acceptance:** Hybrids can be bred

- [ ] **31.6 - Implement Egg Hatching**
  - Eggs hatch after completion time
  - Player receives baby pet (Level 1)
  - Baby has inherited IVs
  - **Acceptance:** Eggs hatch correctly

**End of Week 32 Deliverable:** Full breeding system with IV inheritance, sterility, hybrids, egg hatching.

---

### **Week 33: Star Merging System**

**Priority:** HIGH  
**Time Estimate:** 25-35 hours  
**Dependencies:** Week 31-32 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Merge System)

#### **Tasks:**

- [ ] **33.1 - Implement Star System**
  - All pets have stars (1-5 stars)
  - Newly captured pets: 1 star (default)
  - Stars visible in pet UI (★☆☆☆☆)
  - **Acceptance:** Star system visible

- [ ] **33.2 - Implement Merging Mechanic**
  - Merge requires duplicate pets (same species)
  - Merge costs Glow Cash + materials
  - Formula:
    ```
    1★ → 2★: 1 duplicate + 5,000 Glow Cash + 20 Rare Essence
    2★ → 3★: 2 duplicates + 10,000 Glow Cash + 50 Rare Essence
    3★ → 4★: 3 duplicates + 25,000 Glow Cash + 100 Epic Essence
    4★ → 5★: 4 duplicates + 50,000 Glow Cash + 200 Legendary Core
    ```
  - **Acceptance:** Merging works correctly

- [ ] **33.3 - Implement Star Stat Bonuses**
  - 2★: +10% all stats
  - 3★: +25% all stats
  - 4★: +50% all stats
  - 5★: +100% all stats
  - **Acceptance:** Stars boost stats significantly

- [ ] **33.4 - Add Merge Confirmation UI**
  - Show before/after stats
  - Warn that sacrificed pets are lost
  - Require typing "CONFIRM" for 4★/5★ merges
  - **Acceptance:** Merge UI prevents accidents

- [ ] **33.5 - Track Star Achievements**
  - "First 2★ Pet"
  - "First 5★ Pet"
  - "10 pets at 5★"
  - **Acceptance:** Star achievements tracked

**End of Week 33 Deliverable:** Star merging system with stat bonuses, duplicate requirements, confirmation UI.

---

### **Week 34-35: Life Stage System**

**Priority:** HIGH  
**Time Estimate:** 35-45 hours  
**Dependencies:** Week 31-33 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Life Stage & Aging System)

#### **Tasks:**

- [ ] **34.1 - Implement Real-Time Aging**
  - Pets age in real-world time (not playtime)
  - 6 life stages: Baby → Young → Adult → Mature → Elder → Timeless
  - Each stage: Minimum 30 days, 1% chance/day to advance
  - **Acceptance:** Pets age over real time

- [ ] **34.2 - Implement Stage-Based Stats**
  - Each stage grants cumulative stat bonuses:
    ```
    Baby: +0%
    Young: +5%
    Adult: +10% (total +15%)
    Mature: +15% (total +30%)
    Elder: +20% (total +50%)
    Timeless: +30% (total +80%)
    ```
  - **Acceptance:** Stats increase with life stage

- [ ] **34.3 - Add Visual Age Progression**
  - Each stage has different model/size
  - Baby: Small, cute
  - Young: Medium, energetic
  - Adult: Full-sized
  - Mature: Larger, more detailed
  - Elder: Larger, grayed/aged
  - Timeless: Massive, glowing, ethereal
  - **Acceptance:** Pets look different at each stage

- [ ] **34.4 - Implement Age Advancement Notifications**
  - Notify player when pet advances stage
  - Show stat gains and new appearance
  - Celebrate advancement (animation, sound)
  - **Acceptance:** Players notified of advancement

- [ ] **34.5 - Add Age Display in Pet UI**
  - Show current stage and time in stage
  - Show chance to advance (after 30 days)
  - Show estimated time to Timeless (if 1% daily)
  - **Acceptance:** Age info visible

**End of Week 35 Deliverable:** Real-time aging system with 6 life stages, visual progression, stat bonuses.

---

### **Week 36: Friendship System**

**Priority:** MEDIUM  
**Time Estimate:** 20-30 hours  
**Dependencies:** Week 31-35 complete  
**Design Doc:** PET_SYSTEM_DESIGN_DOCUMENT.md (Friendship & Bond System)

#### **Tasks:**

- [ ] **36.1 - Implement Friendship Points**
  - Each pet has friendship value (0-100)
  - Friendship increases through activities:
    - Use in combat: +1 per battle
    - Feed treat: +5
    - Win without pet fainting: +2
  - **Acceptance:** Friendship points tracked

- [ ] **36.2 - Implement Friendship Bonuses**
  - Friendship 25+: +5% stats
  - Friendship 50+: +10% stats
  - Friendship 75+: +15% stats
  - Friendship 100: +20% stats + special title
  - **Acceptance:** Friendship bonuses apply

- [ ] **36.3 - Add Friendship Visual Indicators**
  - Heart icon shows friendship level
  - Hearts fill as friendship increases (5 hearts total)
  - Full hearts = max friendship (100)
  - **Acceptance:** Friendship level visible

- [ ] **36.4 - Implement Treat System**
  - Treats crafted in Workshop
  - Feeding treat increases friendship
  - Treats have cooldown (1 per pet per day)
  - **Acceptance:** Treats boost friendship

- [ ] **36.5 - Add Friendship Achievements**
  - "First Max Friendship Pet"
  - "10 Pets at Max Friendship"
  - "Max Friendship with Legendary Pet"
  - **Acceptance:** Friendship achievements tracked

**End of Week 36 Deliverable:** Friendship system with points, bonuses, treats, visual indicators.

---

## ✅ ALPHA MILESTONE 2 ACCEPTANCE CRITERIA

**Before moving to Milestone 3, verify:**

- [x] Breeding system produces eggs with IV inheritance
- [x] Parents become sterile after breeding
- [x] Hybrid pets can be bred
- [x] Eggs hatch correctly
- [x] Star merging system functional
- [x] Star bonuses significantly boost stats
- [x] Real-time aging works (6 life stages)
- [x] Pets visually change with age
- [x] Life stage bonuses apply correctly
- [x] Friendship system tracks and rewards usage

---

## 📅 ALPHA MILESTONE 3: BASE BUILDING EXPANSION (WEEKS 37-44)

**Goal:** Build all 20 buildings, implement automation, create full crafting ecosystem.

*Note: Due to document length, I'll provide a condensed version of Milestones 3-5 with key tasks. Full details available in design docs.*

### **Week 37-40: Add 15 More Buildings**

**Priority:** HIGH  
**Time Estimate:** 70-90 hours  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (All Buildings)

#### **Key Tasks:**

- [ ] **Implement Phase 2 Buildings (Weeks 37-38)**
  - Laboratory (research system)
  - Sanctuary (pet display)
  - Energy Generator (passive income)
  - Expedition Hub (staging area)
  - **Acceptance:** Phase 2 buildings functional

- [ ] **Implement Phase 3 Buildings (Weeks 39-40)**
  - Market/Trading Post (player trading)
  - Guild Hall (guild system stub)
  - Trophy Hall (achievements display)
  - Pet Daycare (storage)
  - **Acceptance:** Phase 3 buildings functional

### **Week 41-42: Automation Systems**

**Priority:** MEDIUM  
**Time Estimate:** 35-45 hours  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Automation Station)

#### **Key Tasks:**

- [ ] **Implement Automation Station**
- [ ] **Add Mass Training Feature**
- [ ] **Add Auto-Collection Feature**
- [ ] **Add Building Queue System**
- **Acceptance:** Automation reduces tedious tasks

### **Week 43-44: Laboratory Research System**

**Priority:** HIGH  
**Time Estimate:** 35-45 hours  
**Design Doc:** BASE_BUILDING_SYSTEM_DESIGN_DOCUMENT.md (Laboratory)

#### **Key Tasks:**

- [ ] **Implement Research Tree (4 branches)**
- [ ] **Add Permanent Account-Wide Bonuses**
- [ ] **Implement Research Time/Costs**
- **Acceptance:** Research provides meaningful progression

---

## 📅 ALPHA MILESTONE 4: WORLD GENERATION (WEEKS 45-52)

**Goal:** Implement procedural world generation, add 4+ biomes, create dungeons.

### **Week 45-48: Procedural Biome Generation**

**Priority:** HIGH  
**Time Estimate:** 70-90 hours  
**Design Doc:** WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md (Procedural Generation)

#### **Key Tasks:**

- [ ] **Implement Seed-Based World Generation**
- [ ] **Add 4 More Biomes (Tundra, Swamp, Volcanic, Abyss)**
- [ ] **Implement Biome Gradient Transitions**
- [ ] **Add Environmental Hazards per Biome**
- **Acceptance:** Each expedition has unique world layout

### **Week 49-52: Dungeon System**

**Priority:** HIGH  
**Time Estimate:** 70-90 hours  
**Design Doc:** WORLD_MAP_SYSTEM_DESIGN_DOCUMENT.md (Dungeon System)

#### **Key Tasks:**

- [ ] **Create 5 Dungeon Types**
- [ ] **Implement Boss Encounters**
- [ ] **Add Dungeon-Exclusive Loot**
- [ ] **Implement Dungeon Difficulty Scaling**
- **Acceptance:** Dungeons provide challenging group content

---

## 📅 ALPHA MILESTONE 5: MULTIPLAYER FOUNDATION (WEEKS 53-60)

**Goal:** Add Co-op expeditions, implement multiplayer sync, proximity-based engagement.

### **Week 53-56: Co-op Expedition System**

**Priority:** HIGH  
**Time Estimate:** 70-90 hours  
**Design Doc:** MULTIPLAYER_COMBAT_SYSTEM_DESIGN.md (Co-op PvE)

#### **Key Tasks:**

- [ ] **Implement Party System (2-4 players)**
- [ ] **Add Party Formation UI**
- [ ] **Sync Combat for Multiple Players**
- [ ] **Implement Loot Distribution**
- **Acceptance:** Players can explore together in Co-op

### **Week 57-60: Multiplayer Combat & Sync**

**Priority:** HIGH  
**Time Estimate:** 70-90 hours  
**Design Doc:** MULTIPLAYER_COMBAT_SYSTEM_DESIGN.md (Combat Sync)

#### **Key Tasks:**

- [ ] **Implement Turn-Based Sync (Multiple Players)**
- [ ] **Add Proximity-Based Engagement**
- [ ] **Implement Combat Scaling (HP × Players)**
- [ ] **Add Revive System (Co-op)**
- **Acceptance:** Multiplayer combat works smoothly

---

## 🎉 ALPHA PHASE COMPLETE!

**Alpha Deliverables:**
- ✅ Polished combat (3 defense actions, combos, 30+ enemies)
- ✅ Full pet system (breeding, merging, aging, friendship)
- ✅ 20 buildings (crafting, training, automation, research)
- ✅ Procedural world (6 biomes, dungeons, bosses)
- ✅ Co-op multiplayer (2-4 players, shared expeditions)

**Next Steps:**
1. **Closed Alpha Testing** (50-100 players)
2. **Gather Feedback** (surveys, analytics)
3. **Balance Pass** (adjust based on data)
4. **Bug Fixing** (address critical issues)

---

# SECTION 4: PHASE 3 - BETA (MONTHS 13-18)

## 🎯 BETA GOALS

**What is Beta?**

Beta adds retention features, social systems, and polish. The game should be ready for public testing and initial marketing.

**Beta Success Criteria:**
- [ ] Tutorial teaches new players effectively
- [ ] Daily/weekly quests drive retention
- [ ] UI/UX is polished and intuitive
- [ ] Performance hits 60 FPS on mid-range mobile
- [ ] Ready for open beta (500-1,000 players)

---

## 📅 BETA MILESTONE 1: RETENTION FEATURES (WEEKS 61-68)

### **Week 61-64: Tutorial & Onboarding**

**Priority:** CRITICAL  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Design Tutorial Flow (First 15 minutes)**
- [ ] **Implement Guided Combat Tutorial**
- [ ] **Add Progressive Feature Unlocks**
- [ ] **Create Tooltips System**
- **Acceptance:** New players understand game within 15 minutes

### **Week 65-68: Daily/Weekly Quest System**

**Priority:** HIGH  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Implement 50+ Quest Types**
- [ ] **Add Daily Quest Rotation**
- [ ] **Add Weekly Challenges**
- [ ] **Implement Streak Bonuses**
- **Acceptance:** Players have reason to log in daily

---

## 📅 BETA MILESTONE 2: SOCIAL SYSTEMS (WEEKS 69-76)

### **Week 69-72: Guild System**

**Priority:** HIGH  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Implement Guild Creation**
- [ ] **Add Guild Ranks & Permissions**
- [ ] **Implement Guild Chat**
- [ ] **Add Guild Perks/Bonuses**
- **Acceptance:** Guilds provide social engagement

### **Week 73-76: Leaderboards & Seasons**

**Priority:** HIGH  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Implement Multiple Leaderboards**
- [ ] **Add Seasonal Reset System**
- [ ] **Implement Season Rewards**
- [ ] **Add Anti-Cheat for Leaderboards**
- **Acceptance:** Competitive players engaged

---

## 📅 BETA MILESTONE 3: UI/UX POLISH (WEEKS 77-84)

### **Week 77-80: UI Redesign**

**Priority:** HIGH  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Replace Placeholder UI**
- [ ] **Implement Consistent Design Language**
- [ ] **Add Accessibility Features**
- [ ] **Optimize for Mobile Screens**
- **Acceptance:** UI is professional and intuitive

### **Week 81-84: Animation & VFX Polish**

**Priority:** MEDIUM  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Add Juice to All Interactions**
- [ ] **Polish Combat Effects**
- [ ] **Add Ambient Animations**
- [ ] **Implement Screen Shake/Camera Effects**
- **Acceptance:** Game feels polished and satisfying

---

## 📅 BETA MILESTONE 4: PERFORMANCE OPTIMIZATION (WEEKS 85-92)

### **Week 85-88: Mobile Optimization**

**Priority:** CRITICAL  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Profile Performance Bottlenecks**
- [ ] **Optimize Draw Calls**
- [ ] **Implement LOD System**
- [ ] **Reduce Script Load**
- **Acceptance:** 60 FPS on mid-range mobile (iPhone 11, Samsung S10)

### **Week 89-92: Network Optimization**

**Priority:** HIGH  
**Time Estimate:** 60-80 hours  

#### **Key Tasks:**

- [ ] **Reduce Network Traffic**
- [ ] **Implement Client Prediction**
- [ ] **Add Lag Compensation**
- [ ] **Optimize Remote Event Usage**
- **Acceptance:** Multiplayer feels responsive even on poor connections

---

## 🎉 BETA PHASE COMPLETE!

**Beta Deliverables:**
- ✅ Tutorial & onboarding
- ✅ Daily/weekly quests
- ✅ Guild system
- ✅ Leaderboards & seasons
- ✅ Polished UI/UX
- ✅ 60 FPS on mobile

**Next Steps:**
1. **Open Beta Launch** (500-1,000 players)
2. **Marketing Campaign** (trailers, social media)
3. **Community Management** (Discord, forums)
4. **Iterate Based on Feedback**

---

# SECTION 5: PHASE 4 - LAUNCH (MONTHS 19-22)

## 📅 LAUNCH MILESTONE 1: CONTENT COMPLETE (WEEKS 93-96)

### **Week 93-96: Final Content Pass**

**Priority:** HIGH  
**Time Estimate:** 70-90 hours  

#### **Key Tasks:**

- [ ] **Add 200+ Pet Species (Total)**
- [ ] **Create 10+ Biomes**
- [ ] **Design 20+ Dungeons**
- [ ] **Implement 3 Seasonal Events**
- **Acceptance:** Game has enough content for 100+ hours

---

## 📅 LAUNCH MILESTONE 2: LIVE OPERATIONS PREP (WEEKS 97-100)

### **Week 97-100: Launch Preparation**

**Priority:** CRITICAL  
**Time Estimate:** 70-90 hours  

#### **Key Tasks:**

- [ ] **Set Up Server Infrastructure**
- [ ] **Implement Analytics Dashboard**
- [ ] **Create Content Pipeline Tools**
- [ ] **Train Community Moderators**
- [ ] **Prepare Live Ops Schedule**
- **Acceptance:** Ready for full public launch

---

## 🎉 LAUNCH!

**Launch Checklist:**
- [x] Game is feature-complete
- [x] Performance targets hit (60 FPS mobile)
- [x] All critical bugs fixed
- [x] Server infrastructure scaled
- [x] Marketing campaign live
- [x] Community management ready
- [x] Live ops schedule prepared

**Post-Launch:**
- Weekly content updates
- Monthly balance patches
- Seasonal events (every 3 months)
- New features based on player feedback

---

# SECTION 6: TECHNICAL SPECIFICATIONS

## 🗄️ DATABASE SCHEMA

### **Player Data Structure**

```lua
local PlayerData = {
    -- Account Info
    UserID = 12345,
    Username = "Player123",
    AccountLevel = 50,
    AccountXP = 125000,
    CreatedAt = os.time(),
    LastLogin = os.time(),
    
    -- Currency
    GlowCash = 1250000,
    HypeCrystals = 450,
    EncoreTokens = 25,
    StarShards = 1200, -- Premium currency
    
    -- Progression
    PrestigeLevel = 2,
    TotalPetsCaptured = 345,
    TotalBattlesWon = 1280,
    HighestCombo = 87,
    MaxDepthReached = 3500,
    
    -- Pets (Array of Pet Instances)
    Pets = {
        {
            ID = "abc123",
            SpeciesID = "FireWolf",
            Level = 75,
            XP = 125000,
            Stars = 3,
            IVs = {HP = 28, Attack = 31, Defense = 24},
            LifeStage = "Adult",
            AgeInDays = 45,
            Friendship = 85,
            EquippedWeapon = "IronSword_001",
            EquippedArmor = "SteelChestplate_002",
            CaptureTime = os.time() - (86400 * 45), -- 45 days ago
        },
        -- ... more pets
    },
    
    -- Inventory
    Inventory = {
        Items = {
            {ItemID = "HealthPotion", Quantity = 25},
            {ItemID = "GreatBall", Quantity = 50},
            -- ...
        },
        Materials = {
            {MaterialID = "EmberShard", Quantity = 1250},
            {MaterialID = "FireCrystal", Quantity = 350},
            -- ...
        },
        Equipment = {
            {EquipmentID = "IronSword_001", Stats = {Attack = 10}},
            -- ...
        },
    },
    
    -- Base Buildings
    Buildings = {
        {
            BuildingID = "Weaponsmith",
            Level = 7,
            PlotNumber = 1,
            UpgradeStartTime = nil, -- nil if not upgrading
            UpgradeDuration = nil,
        },
        -- ... 20 buildings
    },
    
    -- Research Progress
    ResearchTree = {
        {ResearchID = "CaptureBonus1", Completed = true},
        {ResearchID = "CaptureBonus2", InProgress = true, StartTime = os.time()},
        -- ...
    },
    
    -- Quests
    DailyQuests = {
        {QuestID = "DefeatEnemies", Progress = 15, Goal = 20, Claimed = false},
        -- ...
    },
    WeeklyQuests = {
        {QuestID = "Capture30Pets", Progress = 22, Goal = 30, Claimed = false},
        -- ...
    },
    
    -- Settings
    Settings = {
        SoundVolume = 0.8,
        MusicVolume = 0.6,
        GraphicsQuality = "Medium",
        ShowTutorialTooltips = false,
    },
}
```

### **Data Store Keys**

```lua
-- Main player data
local mainDataStore = DataStoreService:GetDataStore("PlayerData_v1")
local key = "Player_" .. player.UserId

-- Backup data stores
local backupStore1 = DataStoreService:GetDataStore("PlayerData_Backup1")
local backupStore2 = DataStoreService:GetDataStore("PlayerData_Backup2")

-- Ordered data stores (leaderboards)
local depthLeaderboard = DataStoreService:GetOrderedDataStore("Leaderboard_Depth")
local combatLeaderboard = DataStoreService:GetOrderedDataStore("Leaderboard_Combat")
```

---

## 🌐 NETWORK ARCHITECTURE

### **Server-Client Communication**

```lua
-- ReplicatedStorage/Network/Events.lua
local Events = {
    -- Combat Events
    CombatStart = Instance.new("RemoteEvent"),
    CombatAction = Instance.new("RemoteEvent"),
    CombatEnd = Instance.new("RemoteEvent"),
    
    -- Pet Events
    PetCaptureAttempt = Instance.new("RemoteEvent"),
    PetEquip = Instance.new("RemoteEvent"),
    PetTrain = Instance.new("RemoteEvent"),
    
    -- Currency Events
    CurrencyUpdate = Instance.new("RemoteEvent"), -- Server → Client only
    
    -- Inventory Events
    ItemPurchase = Instance.new("RemoteEvent"),
    ItemUse = Instance.new("RemoteEvent"),
    
    -- Building Events
    BuildingUpgrade = Instance.new("RemoteEvent"),
    BuildingCraft = Instance.new("RemoteEvent"),
}

return Events
```

### **Server Authority Rules**

```lua
-- ALWAYS validate on server, NEVER trust client

-- BAD (Client can cheat):
-- Client: "I deal 999,999 damage"
-- Server: "OK, enemy takes 999,999 damage"

-- GOOD (Server validates):
-- Client: "I hit Perfect on timing circle"
-- Server: Check timestamp, validate hit quality, calculate damage
-- Server: "You dealt 150 damage" (sends result to client)
```

---

## 🔒 ANTI-CHEAT IMPLEMENTATION

### **Key Anti-Cheat Measures**

```lua
-- 1. Server-side validation for ALL game state changes
local function ValidateCombatDamage(player, damage)
    local playerStats = GetPlayerStats(player)
    local maxPossibleDamage = playerStats.Attack * 2 -- Even with perfect hit
    
    if damage > maxPossibleDamage then
        -- Flag for cheating
        WarnPlayer(player, "Invalid damage detected")
        KickPlayer(player, "Cheating detected")
        return false
    end
    
    return true
end

-- 2. Rate limiting
local actionTimestamps = {} -- player.UserId → {action → timestamp}

local function RateLimit(player, action, cooldown)
    local lastAction = actionTimestamps[player.UserId] and actionTimestamps[player.UserId][action]
    
    if lastAction and (os.time() - lastAction) < cooldown then
        return false -- Too soon, reject action
    end
    
    if not actionTimestamps[player.UserId] then
        actionTimestamps[player.UserId] = {}
    end
    actionTimestamps[player.UserId][action] = os.time()
    
    return true
end

-- 3. Sanity checks on currency/resources
local function ValidateCurrencyGain(player, amount, source)
    -- Check if source is legitimate
    if source == "Expedition" then
        -- Max possible: 500,000 per hour
        if amount > 500000 then
            FlagPlayer(player, "Impossible currency gain")
            return false
        end
    end
    
    return true
end
```

---

# SECTION 7: TESTING & QA

## ✅ TESTING CHECKLIST

### **Unit Tests (Per System)**

```lua
-- Example: Combat System Tests
describe("Combat System", function()
    it("should calculate damage correctly with Perfect hit", function()
        local damage = CalculatePlayerDamage(100, 50, "Perfect")
        expect(damage).to.equal(75) -- (100 - 50*0.5) * 1.5
    end)
    
    it("should apply combo multiplier correctly", function()
        local damage = CalculateDamageWithCombo(100, 10)
        expect(damage).to.equal(125) -- 100 * 1.25 (10 combo = +25%)
    end)
    
    it("should reset combo on Miss", function()
        ResetCombat()
        PerfectHit()
        PerfectHit()
        MissHit()
        expect(GetCombo()).to.equal(0)
    end)
end)
```

### **Integration Tests (Cross-System)**

- [ ] **Test: Capture pet → Equip as companion → Enter combat**
  - Verify pet stats used in combat
  - Verify pet HP displayed correctly
  - Verify pet faints at 0 HP

- [ ] **Test: Craft weapon → Equip on pet → Test damage increase**
  - Verify weapon stats added to pet
  - Verify damage calculation includes weapon
  - Verify weapon persists after logout

- [ ] **Test: Complete expedition → Extract → Verify rewards**
  - Verify captured pets saved
  - Verify Glow Cash saved
  - Verify materials saved
  - Verify nothing lost on extract

---

## ⚖️ BALANCE TESTING

### **Combat Balance Tests**

- [ ] **Test: Common enemy at Level 10 (100 HP, 20 Attack)**
  - Average player (Level 10, 100 Attack, 50 Defense)
  - Expected: 5-8 attacks to kill
  - Result: ___ attacks (PASS/FAIL)

- [ ] **Test: Legendary enemy at Level 50 (600 HP, 70 Attack)**
  - Average player (Level 50, 300 Attack, 150 Defense)
  - Expected: 12-15 attacks to kill
  - Result: ___ attacks (PASS/FAIL)

### **Economy Balance Tests**

- [ ] **Test: Glow Cash earning rate**
  - 1 hour of expeditions (Level 30 player)
  - Expected: 15,000-25,000 Glow Cash
  - Result: ___ Glow Cash (PASS/FAIL)

- [ ] **Test: Building upgrade costs**
  - Level 1→5 Weaponsmith
  - Expected: 50,000 Glow Cash total
  - Result: ___ Glow Cash (PASS/FAIL)

---

## 🎮 PERFORMANCE BENCHMARKS

### **Target Metrics**

| Platform | FPS Target | Memory Limit | Network Latency |
|----------|-----------|--------------|-----------------|
| iPhone 11+ | 60 FPS | <500 MB | <100ms |
| Samsung S10+ | 60 FPS | <500 MB | <100ms |
| iPad (2020+) | 60 FPS | <700 MB | <100ms |
| PC (Low-End) | 60 FPS | <1 GB | <100ms |

### **Performance Testing Checklist**

- [ ] **Test: Combat with 3 enemies + companion**
  - Measure FPS during combat
  - Target: 60 FPS sustained
  - Result: ___ FPS (PASS/FAIL)

- [ ] **Test: Biome with 20 enemies + 50 assets**
  - Measure FPS while exploring
  - Target: 60 FPS sustained
  - Result: ___ FPS (PASS/FAIL)

- [ ] **Test: Base with 20 buildings + 50 decorations**
  - Measure FPS in base
  - Target: 60 FPS sustained
  - Result: ___ FPS (PASS/FAIL)

---

# 🎊 CONCLUSION

## 📝 DEVELOPMENT ROADMAP SUMMARY

You now have a complete 22-month development roadmap from MVP → Launch:

**✅ Phase 1: MVP (Months 1-6)**
- Core combat prototype
- Pet capture system
- Basic progression (leveling, currency)
- World basics (2 biomes, enemies, extraction)
- Economy foundation (5 buildings, crafting)

**✅ Phase 2: Alpha (Months 7-12)**
- Combat polish (3 defense actions, combos, 30+ enemies)
- Full pet system (breeding, merging, aging, friendship)
- 20 buildings (automation, research)
- Procedural world (6 biomes, dungeons)
- Multiplayer (Co-op expeditions)

**✅ Phase 3: Beta (Months 13-18)**
- Tutorial & onboarding
- Daily/weekly quests
- Social systems (guilds, leaderboards)
- UI/UX polish
- Performance optimization (60 FPS mobile)

**✅ Phase 4: Launch (Months 19-22)**
- Content complete (200+ pets, 10 biomes, 20 dungeons)
- Live operations prep
- Marketing campaign
- Public launch

---

## 🚀 HOW TO USE THIS ROADMAP

### **For Claude Code:**

1. **Start with Week 1, Task 1.1**
2. **Complete each task in order**
3. **Check off tasks as you finish: `[ ]` → `[x]`**
4. **Reference design docs for detailed specs**
5. **Test thoroughly before moving to next milestone**
6. **Update this document with notes/blockers**

### **For Project Management:**

- **Track progress weekly** (how many tasks completed)
- **Adjust estimates** based on actual time spent
- **Identify blockers early** (mark with 🔒)
- **Celebrate milestones** (each phase completion)

### **For Team Collaboration:**

- **Assign tasks** to team members
- **Use GitHub Issues** for bug tracking
- **Use GitHub Projects** for sprint planning
- **Hold weekly reviews** (what's done, what's next)

---

## 📊 SUCCESS METRICS

**Track these metrics throughout development:**

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Development Velocity** | 10-15 tasks/week | Task completion rate |
| **Code Quality** | <5 bugs/week | Bug reports |
| **Performance** | 60 FPS mobile | Profiler data |
| **Player Retention** | 40% Day 1, 20% Day 7 | Analytics |
| **Engagement** | 60+ min/session | Analytics |
| **Monetization** | $8-12 ARPU | Revenue data |

---

## 🎯 FINAL REMINDERS

**Development Best Practices:**

1. ✅ **Test constantly** - Don't accumulate bugs
2. ✅ **Profile regularly** - Don't wait for performance problems
3. ✅ **Commit often** - Small commits are easier to debug
4. ✅ **Document as you go** - Future you will thank you
5. ✅ **Playtest with others** - You're too close to see issues
6. ✅ **Prioritize fun** - If it's not fun, it's not worth building

**When You Get Stuck:**

1. **Check design docs** - Specs are already written
2. **Break it down** - Smaller tasks are easier
3. **Ask for help** - Discord, forums, Reddit
4. **Take breaks** - Fresh eyes solve problems
5. **Ship it anyway** - Iteration beats perfection

---

## 🙏 GOOD LUCK!

You have everything you need:
- ✅ 1.4 million words of design documentation
- ✅ 22-month step-by-step development roadmap
- ✅ Complete technical specifications
- ✅ Testing frameworks and balance guidelines

**Now go build something amazing!** 🚀

---

**Idol Guardians: Eternal Wilds - Development Roadmap**  
**Version 1.0 | Last Updated: January 4, 2026**  
**Total Development Time: 22 months**  
**Target Launch: November 2027**

**Let's make this game a reality!** 💪
