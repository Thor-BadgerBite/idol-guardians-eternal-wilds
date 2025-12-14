# ⚔️ Combat System - Implementation Guide

**Idol Guardians: Eternal Wilds**

A skill-based, timing-driven combat system designed for mobile-first gameplay with endless progression.

---

## 🎯 Quick Overview

### **What Makes This Combat System Unique**

- **Skill > Stats**: Perfect timing beats higher-level opponents
- **Mobile-First**: Single-tap defense mechanics, optimized for touch controls  
- **Strategic Depth**: Companion pet loadouts dramatically change playstyle
- **No World Freeze**: Combat happens in real-time, extraction pressure maintained
- **Endless Scaling**: Enemy HP and companion stats scale infinitely

### **Core Mechanics**

```
Enemy attacks → Circle appears at random position → 
Player taps correct button at perfect timing → 
Companion counterattacks → Repeat until victory or defeat
```

---

## 📁 Project Structure

```
src/
├── Server/
│   ├── Services/
│   │   ├── CombatService.lua               # Main combat orchestrator
│   │   ├── DamageCalculationService.lua    # Handles all damage math
│   │   ├── TimingValidationService.lua     # Server-side anti-cheat timing
│   │   ├── CompanionService.lua            # Companion stats & abilities
│   │   └── EnemyAIService.lua              # Enemy attack patterns
│   └── ServerMain.server.lua
│
├── Client/
│   ├── Controllers/
│   │   ├── CombatUIController.lua          # UI rendering & animations
│   │   ├── InputController.lua             # Button tap handling
│   │   └── AnimationController.lua         # Visual effects
│   └── ClientMain.client.lua
│
├── Shared/
│   ├── CombatConstants.lua                 # Balance tables & config
│   ├── PetDefinitions.lua                  # Enemy & companion stats
│   ├── AttackPatterns.lua                  # Enemy attack sequences
│   └── AbilityDefinitions.lua              # Companion ability effects
│
└── ReplicatedStorage/
    └── RemoteEvents/
        ├── CombatStart                     # Initiate combat session
        ├── DefenseInput                    # Player defense input
        ├── CombatUpdate                    # Round updates
        └── CombatEnd                       # Victory/defeat resolution
```

---

## 🚀 Quick Start

### **1. Read the Full Design Document**

Before coding, read [`COMBAT_SYSTEM_DESIGN.md`](./COMBAT_SYSTEM_DESIGN.md) for:
- Complete mechanics breakdown
- Damage formulas
- Balance tables
- UI mockups

### **2. Implementation Order**

Follow this exact sequence to avoid refactoring:

#### **Phase 1: Core Combat Loop** (Week 1)
```
✅ Basic combat session management
✅ HP tracking (player, companion, enemy)
✅ Simple damage calculation
✅ Victory/defeat conditions
```

#### **Phase 2: Timing System** (Week 2)
```
✅ Shrinking circle animation
✅ 8-position random spawn
✅ Timing validation (Perfect/Good/Miss)
✅ Visual feedback
```

#### **Phase 3: Companion System** (Week 3)
```
✅ Companion stats & archetypes
✅ Damage distribution (hybrid system)
✅ Abilities (passive/active)
✅ Fainted state mechanics
```

#### **Phase 4: Enemy Variety** (Week 4)
```
✅ Attack patterns by rarity
✅ Combo attacks
✅ Special attack types
✅ Boss mechanics
```

#### **Phase 5: Polish** (Week 5)
```
✅ Healing/revival system
✅ Sound & particle effects
✅ Balance tuning
✅ Mobile optimization
```

### **3. Copy Template Files**

Start with the provided template files:

```bash
# From the project root
cp templates/CombatService.lua src/Server/Services/
cp templates/CombatUIController.lua src/Client/Controllers/
cp templates/CombatConstants.lua src/Shared/
```

---

## 🎮 Core Systems Explained

### **HP System (Hybrid Distribution)**

Three separate HP pools:

```lua
Player HP:    100  -- Core survival pool
Companion HP: 75   -- Guardian/protector pool  
Enemy HP:     250  -- Must deplete to win
```

**Damage Flow:**

When companion is **alive**:
```
Enemy deals 30 damage
  → Companion absorbs 80% (24 damage)
  → Player takes 20% (6 damage)
```

When companion is **fainted**:
```
Enemy deals 30 damage
  → Player takes 100% (30 damage)
```

**Why this works:**
- Companion feels like a guardian (actively protecting)
- Losing companion creates urgency (massive vulnerability spike)
- Strategic healing decisions (companion vs self)

---

### **Timing System (Shrinking Circle)**

**Visual:**
```
      ◯◯◯◯◯
      ◯   ◯  ← Outer ring (shrinks)
      ◯ ● ◯  ← Center dot (target)
      ◯   ◯
      ◯◯◯◯◯
```

**Timing Zones:**
- **Perfect**: Center dot (0% damage taken, 100% counterattack)
- **Good**: Medium ring (50% damage taken, 50% counterattack)
- **Miss**: Outside zones (100% damage taken, no counterattack)

**Random Position System:**
```
┌─────────────────────┐
│ [1]   [2]   [3]     │
│ [4] PetImg  [5]     │
│ [6]   [7]   [8]     │
└─────────────────────┘
```

Circle spawns at 1 of 8 positions, creating spatial awareness challenge.

---

### **Defense Actions (Three Buttons)**

| Button | Color | Used For | Effect |
|--------|-------|----------|--------|
| **DODGE** | Blue | Physical attacks | Evade completely if perfect |
| **BLOCK** | Green | Elemental attacks | Absorb/reduce damage if perfect |
| **COUNTER** | Red | Enemy openings | Deal bonus damage on perfect |

**How it works:**
```
Enemy telegraphs: 🔥 FLAME BURST!
  ↓
[BLOCK] button glows GREEN
  ↓
Circle appears at position [3]
  ↓
Player taps BLOCK at perfect timing
  ↓
✅ Perfect! 0 damage taken, counterattack deals 40 damage
```

---

### **Companion Archetypes**

#### **Tank** (Stone/Nature)
```
HP:      100
Attack:  30
Defense: 80% absorption

Best for: Safe exploration, new players
```

#### **DPS** (Fire/Lightning)
```
HP:      50
Attack:  60  
Defense: 40% absorption

Best for: Fast clears, skilled players
```

#### **Balanced** (Water/Air)
```
HP:      75
Attack:  40
Defense: 60% absorption

Best for: General gameplay, versatility
```

---

## 📊 Balance Tables

### **Enemy Stats by Rarity**

| Rarity | HP | Attack | Shrink Time | Perfect Zone | Combos |
|--------|----|----|-------------|--------------|--------|
| Common | 100 | 20 | 2.0s | 30% | None |
| Uncommon | 150 | 25 | 1.5s | 25% | Rare |
| Rare | 250 | 35 | 1.0s | 15% | Common |
| Epic | 400 | 50 | 0.7s | 10% | Frequent |
| Legendary | 600 | 70 | 0.4s | 5% | Very Common |
| Unique | 800+ | 90+ | 0.3s | 3% | Always |

### **Damage Multipliers**

```lua
-- Timing-based damage reduction
Perfect: 0%    damage taken (full dodge/block)
Good:    50%   damage taken
Miss:    100%  damage taken

-- Counterattack damage
Perfect: 100%  companion attack
Good:    50%   companion attack  
Miss:    0%    no counterattack
```

---

## 🔧 Code Examples

### **Basic Combat Initiation (Server)**

```lua
-- CombatService.lua
function CombatService:InitiateCombat(player, enemyPet)
    local session = {
        Player = player,
        Companion = player.ActiveCompanion,
        Enemy = enemyPet,
        Round = 0,
        CombatActive = true,
    }
    
    self.ActiveSessions[player] = session
    
    RemoteEvents.CombatStart:FireClient(player, {
        EnemyName = enemyPet.Name,
        EnemyHP = enemyPet.HP,
        EnemyRarity = enemyPet.Rarity,
    })
    
    self:StartRound(session)
end
```

### **Damage Calculation (Server)**

```lua
-- DamageCalculationService.lua
function DamageCalculationService:Calculate(enemy, companion, player, timingResult)
    local baseDamage = enemy.AttackStat
    
    -- Apply timing multiplier
    local multipliers = {Perfect = 0, Good = 0.5, Miss = 1.0}
    local incomingDamage = baseDamage * multipliers[timingResult]
    
    -- Distribute damage
    local companionDamage = 0
    local playerDamage = 0
    
    if companion.IsFainted then
        playerDamage = incomingDamage
    else
        companionDamage = incomingDamage * companion.DefensePercent
        playerDamage = incomingDamage * (1 - companion.DefensePercent)
    end
    
    -- Counterattack
    local counterDamage = 0
    if timingResult ~= "Miss" and not companion.IsFainted then
        local counterMultipliers = {Perfect = 1.0, Good = 0.5}
        counterDamage = companion.AttackStat * counterMultipliers[timingResult]
    end
    
    return {
        CompanionDamage = companionDamage,
        PlayerDamage = playerDamage,
        EnemyDamage = counterDamage,
    }
end
```

### **Circle Animation (Client)**

```lua
-- CombatUIController.lua
function CombatUIController:StartDefensePhase(roundData)
    -- Highlight correct button
    self:HighlightButton(roundData.DefenseType)
    
    -- Create circle at random position
    local circle = self:CreateCircle(roundData.Position)
    
    -- Animate shrinking
    local shrinkTween = TweenService:Create(
        circle,
        TweenInfo.new(roundData.ShrinkTime, Enum.EasingStyle.Linear),
        {Size = UDim2.new(0.05, 0, 0.05, 0)} -- Shrink to dot
    )
    shrinkTween:Play()
    
    self.CurrentCircle = circle
    self.StartTime = tick()
end
```

---

## 🎯 Special Features

### **Combo Attacks**

For Rare+ enemies, attacks come in sequences:

```
Enemy: TRIPLE THUNDER STRIKE!

Hit 1: [DODGE] at position [2] (0.5s)
  → Player: PERFECT ✅ (30 damage)

Hit 2: [BLOCK] at position [6] (0.4s)
  → Player: PERFECT ✅ (30 damage)

Hit 3: [COUNTER] at position [4] (0.3s)  
  → Player: PERFECT ✅ (45 damage, 1.5x bonus!)

Total: 105 damage if all perfect
       0 damage taken
       "PERFECT CHAIN!" displayed
```

### **Companion Abilities**

**Passive (Always Active):**
```lua
FortressShield = {
    Effect = "80% damage absorption instead of 60%"
}

CriticalStrike = {
    Effect = "Perfect timing deals +50% damage"
}
```

**Active (Auto-Trigger):**
```lua
LastStand = {
    Trigger = "HP < 30%",
    Effect = "Next attack fully blocked",
    Cooldown = 60,
}

InfernoBurst = {
    Trigger = "Perfect timing",
    Effect = "Oneshot Common pets, 2x damage on Rare+",
    Cooldown = 30,
}
```

### **Special Attack Types**

**Heavy Strike:**
- 2x damage
- Slow circle (easy to perfect)
- Devastating if missed

**Rapid Assault:**
- 3-5 hits × 0.5 damage
- Fast circles (hard to perfect)
- Chip damage adds up

**Elemental Burst:**
- Normal damage + status effect
- Burn: -5 HP/s for 10s
- Stun: Next counter deals 0
- Freeze: Next circle shrinks faster

---

## 🧪 Testing Guide

### **Test Checklist**

#### **Phase 1: Basic Combat**
```
[ ] Player can engage enemy
[ ] HP bars display correctly
[ ] Damage calculation works
[ ] Victory condition triggers
[ ] Defeat condition triggers
```

#### **Phase 2: Timing**
```
[ ] Circle spawns at all 8 positions randomly
[ ] Circle shrinks smoothly
[ ] Perfect timing detected accurately
[ ] Good timing detected accurately
[ ] Miss timing detected accurately
[ ] Correct button required for success
```

#### **Phase 3: Companions**
```
[ ] Tank archetype absorbs 80% damage
[ ] DPS archetype deals 2x damage
[ ] Balanced archetype works as expected
[ ] Fainted state triggers at 0 HP
[ ] Damage distribution correct when fainted
[ ] Abilities trigger appropriately
```

#### **Phase 4: Enemy Variety**
```
[ ] Common pets use simple patterns
[ ] Legendary pets use complex combos
[ ] Special attacks work (Heavy/Rapid/Elemental)
[ ] Boss phases transition correctly
```

### **Balance Testing**

Test these scenarios:

```
1. Level 1 player with Common companion vs Common enemy
   → Should win in 4-5 perfect hits
   → Should survive 2-3 misses

2. Level 10 player with Rare companion vs Rare enemy
   → Should win in 6-8 perfect hits
   → Should survive 1 miss if companion healthy

3. Level 20 player with Epic companion vs Legendary enemy
   → Should win in 10-12 perfect hits
   → Cannot afford any misses
```

---

## 📱 Mobile Optimization

### **Touch Controls**

```lua
-- Buttons must be LARGE (40% screen height)
-- Tap zones should not overlap
-- Visual feedback instant (<50ms)

ButtonSizing = {
    Width = "90% of screen width / 3",
    Height = "40% of screen height",
    Padding = "5% between buttons",
}
```

### **Performance**

```lua
-- Keep UI elements minimal during combat
-- Limit particle effects to <20 concurrent
-- Use object pooling for damage numbers
-- Tween animations instead of RunService
```

### **Network Handling**

```lua
-- Account for mobile latency
function TimingValidationService:ValidateTiming(startTime, shrinkTime, inputTime)
    local elapsed = inputTime - startTime
    local ping = player:GetNetworkPing()
    
    -- Add latency compensation
    local compensatedElapsed = elapsed - (ping / 2)
    
    -- Then validate as normal
    ...
end
```

---

## 🔒 Anti-Cheat Measures

### **Server-Side Validation**

```lua
-- NEVER trust client for:
1. Timing results (server calculates)
2. Damage amounts (server owns HP)
3. Attack selection (server chooses)
4. Combat outcomes (server validates)
```

### **Timing Validation**

```lua
-- Check for impossible timing
function ValidateInputTiming(player, inputTime)
    local now = tick()
    local ping = player:GetNetworkPing()
    local maxValidTime = now + ping + 0.1
    
    if inputTime > maxValidTime then
        warn("Suspicious timing:", player.Name)
        return false
    end
    
    return true
end
```

### **Rate Limiting**

```lua
-- Prevent input spam
local lastInputTime = {}

function OnDefenseInput(player, inputTime)
    local now = tick()
    if lastInputTime[player] and (now - lastInputTime[player]) < 0.1 then
        -- Too fast, ignore
        return
    end
    
    lastInputTime[player] = now
    -- Process normally
end
```

---

## 📈 Progression & Scaling

### **Companion Leveling**

```lua
CompanionProgression = {
    XP_Per_Perfect = 10,
    XP_Per_Good = 5,
    XP_Per_Combat_Won = 50,
    XP_Per_Level = 100 + (level * 50), -- Exponential
    
    StatGains_Per_Level = {
        HP = 5,
        Attack = 2,
    }
}
```

**Example:**
```
StoneGuard Level 1:   100 HP, 30 Attack
StoneGuard Level 10:  145 HP, 48 Attack  
StoneGuard Level 50:  345 HP, 128 Attack
StoneGuard Level 100: 595 HP, 228 Attack
```

### **Enemy Scaling**

```lua
-- Scale with distance from base
local distanceMultiplier = 1 + (distanceFromBase * 0.1)
enemyPet.HP = baseHP * distanceMultiplier
enemyPet.Attack = baseAttack * distanceMultiplier

-- Example at distance 20:
-- Rare pet: 250 HP → 750 HP
-- Attack: 35 → 105 damage
```

---

## 🎨 Visual Polish Checklist

### **Must-Have Effects**

```
✅ Circle color transitions (white → yellow → orange → red)
✅ Perfect hit: Bright flash + screen shake
✅ Good hit: Subtle flash
✅ Miss: Red flash + damage shake
✅ Damage numbers float upward and fade
✅ HP bars drain smoothly (tween)
✅ Companion faint: Particle burst + dim model
✅ Victory: Confetti + fanfare
✅ Defeat: Screen desaturate + dramatic music
```

### **Sound Design**

```
Perfect hit:    Satisfying chime (high pitch)
Good hit:       Normal impact (medium pitch)
Miss:           Error buzz (low pitch)
Counterattack:  Whoosh + impact combo
Combo chain:    Escalating tones
Perfect chain:  Victory fanfare
```

---

## 📝 Common Issues & Solutions

### **Issue: Circle doesn't appear on mobile**

```lua
-- Solution: Check ScreenGui ZIndex
CombatUI.DisplayOrder = 100 -- Higher than other UIs
Circle.ZIndex = 10
```

### **Issue: Timing feels off**

```lua
-- Solution: Add latency compensation
local ping = player:GetNetworkPing()
local compensatedTime = inputTime - (ping / 2)
```

### **Issue: Buttons not responding**

```lua
-- Solution: Increase tap zone size
Button.Size = UDim2.new(0.3, 0, 0.4, 0) -- 30% width, 40% height
Button.Active = true
Button.AutoButtonColor = false -- Manual control
```

### **Issue: Damage feels random**

```lua
-- Solution: Add debug logging
print("Enemy Attack:", enemy.AttackStat)
print("Timing Result:", timingResult)
print("Companion Defense:", companion.DefensePercent)
print("Final Player Damage:", playerDamage)
```

---

## 🎓 Learning Resources

### **Required Reading**

1. [`COMBAT_SYSTEM_DESIGN.md`](./COMBAT_SYSTEM_DESIGN.md) - Full mechanics
2. Roblox Tween Documentation - For animations
3. RemoteEvent Best Practices - For client-server communication

### **Recommended Study**

- **Undertale** - Timing-based combat inspiration
- **Guitar Hero** - Rhythm mechanics
- **Dark Souls** - Parry timing systems
- **Monster Hunter** - Attack telegraphing

---

## 🚀 Ready to Build?

### **Next Steps:**

1. ✅ Read full design document
2. ✅ Set up file structure
3. ✅ Start with Phase 1 (Core Combat Loop)
4. ✅ Test incrementally (don't skip testing!)
5. ✅ Iterate based on playtesting

### **Questions?**

Refer back to:
- [`COMBAT_SYSTEM_DESIGN.md`](./COMBAT_SYSTEM_DESIGN.md) for detailed mechanics
- This README for implementation guidance
- Balance tables for tuning values

---

**Happy Coding! ⚔️**

*Last Updated: December 14, 2025*  
*Version: 1.0*
