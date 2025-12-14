# 🎮 COMBAT SYSTEM DESIGN DOCUMENT
## Idol Guardians: Eternal Wilds - Complete Combat Architecture

**Version:** 1.0  
**Last Updated:** December 14, 2025  
**Status:** Ready for Implementation

---

## 📋 TABLE OF CONTENTS

1. [Core Combat Philosophy](#core-combat-philosophy)
2. [Combat Flow Overview](#combat-flow-overview)
3. [HP System Architecture](#hp-system-architecture)
4. [Timing & Defense Mechanics](#timing-defense-mechanics)
5. [Damage Calculation System](#damage-calculation-system)
6. [Enemy Pet Stats & Scaling](#enemy-pet-stats-scaling)
7. [Companion Pet System](#companion-pet-system)
8. [Visual UI System](#visual-ui-system)
9. [Combo System](#combo-system)
10. [Special Attack Types](#special-attack-types)
11. [Healing & Revival Mechanics](#healing-revival-mechanics)
12. [Technical Implementation](#technical-implementation)
13. [Balance Tables](#balance-tables)

---

## 🎯 CORE COMBAT PHILOSOPHY

### **Design Pillars:**

1. **Skill-Based, Not Stat-Only**
   - Perfect timing beats higher stats
   - Accessible to new players, mastery for veterans
   - Mobile-friendly (single input at a time)

2. **Strategic Loadout Choices**
   - Tank pets for safe runs
   - DPS pets for fast clears
   - Hybrid pets for balanced play

3. **Risk vs Reward**
   - Companion HP management matters
   - Extraction pressure increases with fainted companion
   - Healing resources are limited

4. **Endless Scalability**
   - Enemy HP scales infinitely by rarity
   - Companion stats scale infinitely
   - Always room to improve

---

## ⚔️ COMBAT FLOW OVERVIEW

### **Complete Combat Loop:**

```
┌─────────────────────────────────────────────────┐
│ PHASE 1: ENCOUNTER INITIATION                   │
├─────────────────────────────────────────────────┤
│ • Player approaches wild pet                    │
│ • Pet aggros based on behavior type             │
│ • Combat UI opens                               │
│ • World continues (no freeze)                   │
└─────────────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────────────┐
│ PHASE 2: COMBAT ROUNDS (Repeat Until Winner)   │
├─────────────────────────────────────────────────┤
│ ROUND STRUCTURE:                                │
│                                                 │
│ 1. Enemy Pet Attacks                            │
│    └─ Selects attack from pattern pool          │
│    └─ Telegraphs attack type                    │
│                                                 │
│ 2. Defense Circle Appears                       │
│    └─ Random position (1 of 8 zones)            │
│    └─ Correct button highlights                 │
│    └─ Circle begins shrinking                   │
│                                                 │
│ 3. Player Responds                              │
│    └─ Taps highlighted button                   │
│    └─ Server validates timing                   │
│    └─ Result: Perfect / Good / Miss             │
│                                                 │
│ 4. Damage Calculation                           │
│    └─ Enemy → Player/Companion (based on timing)│
│    └─ Companion → Enemy (counterattack)         │
│                                                 │
│ 5. HP Updates                                   │
│    └─ Check for deaths/weakened states          │
│    └─ Update UI                                 │
│                                                 │
│ 6. Next Round OR End Combat                     │
└─────────────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────────────┐
│ PHASE 3: COMBAT RESOLUTION                     │
├─────────────────────────────────────────────────┤
│ VICTORY (Enemy HP = 0):                         │
│ • Enemy enters WEAKENED state                   │
│ • Capture attempt phase begins                  │
│ • Timing quality affects capture bonus          │
│                                                 │
│ DEFEAT (Player HP = 0):                         │
│ • Player defeated                               │
│ • Cargo lost                                    │
│ • Respawn at base                               │
│                                                 │
│ COMPANION FAINT (Companion HP = 0):             │
│ • Companion removed from combat                 │
│ • Player continues alone (vulnerable)           │
│ • No counterattacks, full damage taken          │
└─────────────────────────────────────────────────┘
```

---

## ❤️ HP SYSTEM ARCHITECTURE

### **Three HP Pools:**

```
┌─────────────────────────────────────┐
│ PLAYER HP                           │
│ ████████████ 100/100                │
│                                     │
│ • Core survival pool                │
│ • Reaches 0 = defeat                │
│ • Takes bleed-through damage        │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ COMPANION PET HP                    │
│ ██████████░░ 75/100                 │
│                                     │
│ • Guardian/protector pool           │
│ • Reaches 0 = fainted (not dead)    │
│ • Absorbs damage first              │
│ • Deals counterattack damage        │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ ENEMY PET HP                        │
│ ████████████████ 250/250            │
│                                     │
│ • Must be depleted to win           │
│ • Scales by rarity                  │
│ • Reaches 0 = weakened state        │
└─────────────────────────────────────┘
```

### **Damage Flow (Hybrid Distribution System):**

#### **When Companion is ALIVE:**

```
Enemy Pet deals 30 damage
        ↓
Companion absorbs portion (e.g., 80% = 24 damage)
        ↓
Player takes overflow (20% = 6 damage)
        ↓
RESULT:
Companion HP: 75 → 51
Player HP: 100 → 94
```

#### **When Companion is FAINTED:**

```
Enemy Pet deals 30 damage
        ↓
No companion to absorb
        ↓
Player takes FULL damage (100% = 30 damage)
        ↓
RESULT:
Companion HP: 0 (fainted)
Player HP: 94 → 64
```

### **Why This System Works:**

✅ **Companion feels like a guardian** (actively protecting player)  
✅ **Losing companion is scary** (vulnerability increases dramatically)  
✅ **Strategic resource management** (heal companion vs heal self)  
✅ **Supports multiple playstyles** (tank/DPS/balanced companions)

---

## 🎯 TIMING & DEFENSE MECHANICS

### **Visual System: Shrinking Circle**

```
┌─────────────────────────────────────┐
│                                     │
│         ◯◯◯◯◯                       │
│         ◯   ◯  ← Outer ring         │
│         ◯ ● ◯  ← Center dot         │
│         ◯   ◯                       │
│         ◯◯◯◯◯                       │
│                                     │
│    Circle shrinks toward center     │
│    Player taps when overlapping     │
└─────────────────────────────────────┘
```

### **Timing Zones:**

```
Perfect Zone:  ●   (tiny, center)
Good Zone:    (●)  (medium ring)
Miss Zone:   ( ● ) (outside zones)
```

### **Random Position System (8 Zones):**

```
┌─────────────────────────────────┐
│  [1]      [2]      [3]          │
│                                 │
│  [4]   Pet Image   [5]          │
│                                 │
│  [6]      [7]      [8]          │
└─────────────────────────────────┘
```

**Position Rules:**
- **Common pets:** Use 4 positions (2, 4, 5, 7)
- **Rare pets:** Use 6 positions (1, 2, 3, 5, 7, 8)
- **Legendary pets:** Use all 8 positions
- **Combos:** Circle jumps between positions rapidly

### **Three Defense Actions:**

#### **1. DODGE (Blue)**
```
Used for: Physical attacks, melee strikes
Effect: Evade completely if perfect
Visual: Character sidestep animation
```

#### **2. BLOCK (Green)**
```
Used for: Elemental attacks, projectiles
Effect: Absorb/reduce damage if perfect
Visual: Shield/barrier animation
```

#### **3. COUNTER (Red)**
```
Used for: Punishing enemy openings
Effect: Deal bonus damage on perfect
Visual: Aggressive retaliation animation
```

### **Button Highlighting System:**

```
Enemy telegraphs: 🔥 FLAME BURST!
        ↓
UI highlights: [BLOCK] button glows GREEN
        ↓
Circle appears at random position
        ↓
Player taps BLOCK at perfect timing
        ↓
Result: ✅ Perfect block, counterattack!
```

---

## 🧮 DAMAGE CALCULATION SYSTEM

### **Complete Damage Formula:**

```lua
-- STEP 1: Enemy attacks player
local baseDamage = enemyPet.AttackStat

-- STEP 2: Player defends (timing result)
local timingResult = ValidateTiming() -- "Perfect" | "Good" | "Miss"

-- STEP 3: Apply timing multiplier to incoming damage
local damageMultiplier = {
    Perfect = 0,    -- No damage taken
    Good = 0.5,     -- Half damage
    Miss = 1.0,     -- Full damage
}

local incomingDamage = baseDamage * damageMultiplier[timingResult]

-- STEP 4: Distribute damage between companion and player
if companion.IsFainted then
    -- No companion protection
    player.HP = player.HP - incomingDamage
else
    -- Companion absorbs portion based on defense stat
    local companionAbsorption = companion.DefensePercent -- 0.4 to 0.8
    local companionDamage = incomingDamage * companionAbsorption
    local playerDamage = incomingDamage * (1 - companionAbsorption)
    
    companion.HP = companion.HP - companionDamage
    player.HP = player.HP - playerDamage
    
    -- Check if companion fainted
    if companion.HP <= 0 then
        companion.HP = 0
        companion.IsFainted = true
    end
end

-- STEP 5: Companion counterattacks (if not Miss and not fainted)
if timingResult ~= "Miss" and not companion.IsFainted then
    local counterMultiplier = {
        Perfect = 1.0,  -- Full counterattack damage
        Good = 0.5,     -- Half counterattack damage
    }
    
    local counterDamage = companion.AttackStat * counterMultiplier[timingResult]
    
    -- Apply companion ability modifiers
    if companion.HasAbility("CriticalStrike") and timingResult == "Perfect" then
        counterDamage = counterDamage * 1.5
    end
    
    enemyPet.HP = enemyPet.HP - counterDamage
end

-- STEP 6: Check combat end conditions
if enemyPet.HP <= 0 then
    enemyPet.State = "Weakened"
    TriggerCapturePhase()
elseif player.HP <= 0 then
    TriggerPlayerDefeat()
end
```

### **Damage Calculation Examples:**

#### **Example 1: Perfect Timing with Tank Companion**

```
SETUP:
Player HP: 100
Companion: StoneGuard (75 HP, 30 Attack, 80% absorption)
Enemy: BranchStalker (250 HP, 35 Attack)

ATTACK:
Enemy deals 35 damage
Player hits DODGE - PERFECT ✅

CALCULATION:
incomingDamage = 35 * 0 = 0 damage
companionDamage = 0 * 0.8 = 0
playerDamage = 0 * 0.2 = 0
counterDamage = 30 * 1.0 = 30

RESULT:
Player HP: 100 → 100 (no change)
Companion HP: 75 → 75 (no change)
Enemy HP: 250 → 220 (-30)
```

#### **Example 2: Good Timing with DPS Companion**

```
SETUP:
Player HP: 85
Companion: FlameRaptor (50 HP, 60 Attack, 40% absorption)
Enemy: StormDrake (400 HP, 50 Attack)

ATTACK:
Enemy deals 50 damage
Player hits BLOCK - GOOD ⚠️

CALCULATION:
incomingDamage = 50 * 0.5 = 25 damage
companionDamage = 25 * 0.4 = 10
playerDamage = 25 * 0.6 = 15
counterDamage = 60 * 0.5 = 30

RESULT:
Player HP: 85 → 70 (-15)
Companion HP: 50 → 40 (-10)
Enemy HP: 400 → 370 (-30)
```

#### **Example 3: Miss with Fainted Companion**

```
SETUP:
Player HP: 65
Companion: FAINTED (0 HP)
Enemy: VoidStalker (600 HP, 70 Attack)

ATTACK:
Enemy deals 70 damage
Player MISSES ❌

CALCULATION:
incomingDamage = 70 * 1.0 = 70 damage
No companion to absorb
playerDamage = 70
No counterattack

RESULT:
Player HP: 65 → 0 (DEFEATED)
Companion HP: 0 (fainted)
Enemy HP: 600 (unchanged)
```

---

## 🐾 ENEMY PET STATS & SCALING

### **Base Stats by Rarity:**

| Rarity | Base HP | Attack Damage | Attacks Per Fight | Shrink Speed | Perfect Zone |
|--------|---------|---------------|-------------------|--------------|--------------|
| **Common** | 100 | 20 | 3-4 | 2.0s | 30% |
| **Uncommon** | 150 | 25 | 4-5 | 1.5s | 25% |
| **Rare** | 250 | 35 | 5-6 | 1.0s | 15% |
| **Epic** | 400 | 50 | 6-8 | 0.7s | 10% |
| **Legendary** | 600 | 70 | 8-10 | 0.4s | 5% |
| **Unique** | 800+ | 90+ | 10-15 | 0.3s | 3% |

### **Attack Patterns by Rarity:**

#### **Common Pets (Simple, Predictable):**
```
Pattern: Single attack type repeated
Example: ForestSprite
  └─ Claw Swipe x4 (all DODGE)
  └─ Slow, telegraphed
  └─ Large timing windows
```

#### **Uncommon Pets (Two Attack Types):**
```
Pattern: Alternating attacks
Example: MossBear
  └─ Swipe (DODGE) → Roar (BLOCK) → repeat
  └─ Medium speed
  └─ Medium timing windows
```

#### **Rare Pets (Three Attack Types + Combos):**
```
Pattern: Mixed attacks with 2-hit combos
Example: BranchStalker
  └─ Claw (DODGE) → Root Trap (BLOCK) → Fury (COUNTER)
  └─ Occasional 2-hit combo: Claw → Claw
  └─ Faster speed
```

#### **Epic Pets (Complex Patterns + 3-Hit Combos):**
```
Pattern: Pattern recognition required
Example: CrystalGolem
  └─ Rock Slam (BLOCK) → Shard Burst (DODGE) → 
      Ground Pound (BLOCK) → Counter Window (COUNTER)
  └─ 3-hit combos common
  └─ Fast speed, small windows
```

#### **Legendary Pets (Advanced Patterns + Multi-Phase):**
```
Pattern: Phase-based combat
Example: StormDrake
  
  PHASE 1 (100%-50% HP):
  └─ Lightning (DODGE) → Thunder (BLOCK) → Volt (DODGE)
  └─ 3-hit combos
  
  PHASE 2 (50%-0% HP):
  └─ ENRAGED: Attacks faster
  └─ 5-hit combo finale
  └─ Smaller perfect zones
```

#### **Unique/Boss Pets (Rhythm Game Sequences):**
```
Pattern: Choreographed burst sequences
Example: VoidLord (Dungeon Boss)
  
  PHASE 1: Standard attacks
  PHASE 2: Void Barrage
    └─ [DODGE][DODGE][BLOCK][COUNTER][DODGE]
    └─ 0.3s per input
    └─ Must hit all 5 perfectly for no damage
  
  PHASE 3: Chaos Mode
    └─ Random positions, all 3 button types
    └─ 10+ hit sequence
    └─ Ultimate test of skill
```

### **Enemy Stat Scaling Formula:**

```lua
-- Base stats
local baseHP = RarityStats[rarity].BaseHP
local baseAttack = RarityStats[rarity].BaseAttack

-- Distance from base scaling
local distanceMultiplier = 1 + (distanceFromBase * 0.1)

-- Final stats
enemyPet.MaxHP = baseHP * distanceMultiplier
enemyPet.AttackStat = baseAttack * distanceMultiplier

-- Example: Rare pet at distance 10
-- HP: 250 * (1 + 10*0.1) = 250 * 2 = 500 HP
-- Attack: 35 * 2 = 70 damage
```

---

## 🛡️ COMPANION PET SYSTEM

### **Companion Stats (Three Archetypes):**

#### **TANK ARCHETYPE (Stone/Nature):**
```
┌─────────────────────────────────┐
│ StoneGuard (Epic Stone Pet)    │
├─────────────────────────────────┤
│ HP: 100                         │
│ Attack: 30                      │
│ Defense: 80% absorption         │
│                                 │
│ Passive: Fortress Shield        │
│ └─ Absorbs 80% of damage        │
│                                 │
│ Active: Last Stand              │
│ └─ When HP < 30%, next attack   │
│    is fully blocked             │
└─────────────────────────────────┘

PLAYSTYLE:
• Slow, safe progression
• Minimal healing items needed
• Long fights but low risk
• Best for: New players, exploration
```

#### **DPS ARCHETYPE (Fire/Lightning):**
```
┌─────────────────────────────────┐
│ FlameRaptor (Legendary Fire)   │
├─────────────────────────────────┤
│ HP: 50                          │
│ Attack: 60                      │
│ Defense: 40% absorption         │
│                                 │
│ Passive: Glass Cannon           │
│ └─ +100% attack damage          │
│ └─ Only 40% damage absorption   │
│                                 │
│ Active: Inferno Burst           │
│ └─ Next perfect timing oneshots│
│    Common pets, double damage   │
│    on Rare+                     │
└─────────────────────────────────┘

PLAYSTYLE:
• Fast, risky combat
• High skill requirement
• Quick clears if perfect timing
• Best for: Skilled players, speedruns
```

#### **BALANCED ARCHETYPE (Water/Air):**
```
┌─────────────────────────────────┐
│ TideRunner (Rare Water Pet)    │
├─────────────────────────────────┤
│ HP: 75                          │
│ Attack: 40                      │
│ Defense: 60% absorption         │
│                                 │
│ Passive: Adaptive Flow          │
│ └─ Balanced stats for all       │
│    situations                   │
│                                 │
│ Active: Cleansing Wave          │
│ └─ Remove status effects +      │
│    heal 20 HP                   │
└─────────────────────────────────┘

PLAYSTYLE:
• Versatile, adaptable
• Medium risk, medium reward
• Good for all content
• Best for: General gameplay
```

### **Companion Ability System:**

#### **Passive Abilities (Always Active):**

```lua
-- Example abilities and their effects

FortressShield = {
    Type = "Passive",
    Effect = function(companion)
        companion.DefensePercent = 0.80 -- 80% absorption
    end
}

GlassCannon = {
    Type = "Passive",
    Effect = function(companion)
        companion.AttackStat = companion.AttackStat * 2
        companion.DefensePercent = 0.40 -- Only 40% absorption
    end
}

Regeneration = {
    Type = "Passive",
    Effect = function(companion, deltaTime)
        if not InCombat then
            companion.HP = math.min(companion.HP + 5 * deltaTime, companion.MaxHP)
        end
    end
}

CriticalStrike = {
    Type = "Passive",
    Effect = function(damage, timingResult)
        if timingResult == "Perfect" then
            return damage * 1.5 -- +50% damage on perfect
        end
        return damage
    end
}
```

#### **Active Abilities (Triggered Automatically):**

```lua
-- Auto-trigger conditions

LastStand = {
    Type = "Active",
    Trigger = "HP < 30%",
    Effect = function(companion)
        -- Next incoming attack is fully blocked
        companion.NextAttackBlocked = true
    end,
    Cooldown = 60, -- seconds
}

InfernoBurst = {
    Type = "Active",
    Trigger = "Perfect timing achieved",
    Effect = function(damage, enemyRarity)
        if enemyRarity == "Common" then
            return 999999 -- Instant kill
        else
            return damage * 2
        end
    end,
    Cooldown = 30,
}

ShieldBubble = {
    Type = "Active",
    Trigger = "Combat start",
    Effect = function()
        -- One free perfect defense
        return "AutoPerfect"
    end,
    UsesPerCombat = 1,
}
```

### **Companion Stat Progression:**

```lua
-- Companion levels up through use
CompanionProgression = {
    XP_Per_Perfect = 10,
    XP_Per_Good = 5,
    XP_Per_Combat_Won = 50,
    
    StatGains_Per_Level = {
        HP = 5,
        Attack = 2,
        -- Defense % stays constant
    }
}

-- Example: Level 1 → Level 50
-- StoneGuard starts: 100 HP, 30 Attack, 80% defense
-- StoneGuard at 50: 345 HP, 128 Attack, 80% defense
```

---

## 🎨 VISUAL UI SYSTEM

### **Combat UI Layout (Mobile):**

```
┌─────────────────────────────────┐
│ ┌─────────────────────────────┐ │
│ │ BranchStalker (Rare)        │ │
│ │ HP: ████████████░░ 205/250  │ │
│ └─────────────────────────────┘ │
├─────────────────────────────────┤
│                                 │
│      [3D Pet Model Here]        │
│                                 │
│         ◯                       │
│          ●  ← Circle            │
│         Position [7]            │
│                                 │
├─────────────────────────────────┤
│ ┌─────────────────────────────┐ │
│ │ Player HP: ████░░ 89/100    │ │
│ │ Companion: ██░░░ 33/75      │ │
│ └─────────────────────────────┘ │
├─────────────────────────────────┤
│  [DODGE]  [BLOCK]  [COUNTER]    │
│   BLUE     GREEN     RED        │
│ (40% screen height tap zones)   │
└─────────────────────────────────┘
```

### **Circle Animation States:**

#### **State 1: Spawn**
```
Frame 1: Circle appears instantly at random position
Size: 200% of center dot
Color: White/neutral
Duration: 0.1s (flash)
```

#### **State 2: Shrink**
```
Frame 2-N: Circle shrinks toward center
Speed: Based on enemy rarity (0.3s to 2.0s total)
Color: Transitions white → yellow → orange → red
Zones visible:
  • Outer ring (miss zone) = red
  • Middle ring (good zone) = yellow
  • Inner dot (perfect zone) = green
```

#### **State 3: Resolution**
```
PERFECT HIT:
• Bright green flash
• Circle explodes outward
• "PERFECT!" text
• Vibration (mobile)
• Sound: satisfying chime

GOOD HIT:
• Yellow flash
• "GOOD" text
• Smaller vibration
• Sound: normal hit

MISS:
• Red flash
• Circle disappears
• "MISS!" text
• Harsh vibration
• Sound: error/damage tone
```

### **Button Highlighting System:**

```lua
-- When enemy telegraphs attack
function HighlightButton(attackType)
    local buttonMap = {
        Physical = "DODGE",  -- Blue glow
        Elemental = "BLOCK", -- Green glow
        Counter = "COUNTER", -- Red glow
    }
    
    local button = buttonMap[attackType]
    
    -- Visual effects
    button.Glow = true
    button.Scale = 1.2 -- Slightly bigger
    button.Pulse = true -- Pulsing animation
    
    -- Other buttons dim
    for _, otherButton in pairs(AllButtons) do
        if otherButton ~= button then
            otherButton.Transparency = 0.5
        end
    end
end
```

### **Damage Feedback Effects:**

```lua
-- Visual feedback for damage taken/dealt

function ShowDamageNumber(amount, position, type)
    local color = {
        PlayerDamage = Color3.fromRGB(255, 0, 0),    -- Red
        CompanionDamage = Color3.fromRGB(255, 165, 0), -- Orange
        EnemyDamage = Color3.fromRGB(0, 255, 0),     -- Green
    }
    
    -- Create floating number
    local label = CreateFloatingLabel(amount, position)
    label.TextColor3 = color[type]
    label.TextSize = 24 + (amount / 10) -- Bigger for more damage
    
    -- Animate upward and fade
    TweenService:Create(label, TweenInfo.new(1), {
        Position = position + Vector3.new(0, 3, 0),
        TextTransparency = 1
    }):Play()
end
```

### **Combo Chain Visual:**

```lua
-- For multi-hit combos, show chain counter

function ShowComboChain(hitNumber, totalHits)
    -- Display: "CHAIN 3/5"
    local comboUI = GetComboUI()
    comboUI.Text = "CHAIN " .. hitNumber .. "/" .. totalHits
    comboUI.Visible = true
    
    -- Pulse on each hit
    comboUI.Scale = 1.3
    TweenService:Create(comboUI, TweenInfo.new(0.2), {
        Scale = 1.0
    }):Play()
    
    -- If perfect chain completed
    if hitNumber == totalHits and allPerfect then
        comboUI.Text = "PERFECT CHAIN!"
        comboUI.TextColor3 = Color3.fromRGB(255, 215, 0) -- Gold
        -- Flash effect
        FlashScreen(Color3.fromRGB(255, 215, 0), 0.3)
    end
end
```

---

## 🔥 COMBO SYSTEM

### **Combo Attack Structure:**

```lua
-- Enemy attacks in rapid succession
-- Player must hit multiple defenses in sequence

ComboAttack = {
    Name = "Triple Thunder Strike",
    Hits = 3,
    Sequence = {
        {
            Type = "DODGE",
            Position = 2,
            ShrinkTime = 0.5,
        },
        {
            Type = "BLOCK",
            Position = 6,
            ShrinkTime = 0.4,
        },
        {
            Type = "COUNTER",
            Position = 4,
            ShrinkTime = 0.3,
        }
    },
    
    -- Combo bonus if all hits are perfect
    PerfectBonus = {
        FinalHitDamageMultiplier = 1.5,
        PlayerDamageReduction = 0.5,
    }
}
```

### **Combo Execution Example:**

```
StormDrake uses: TRIPLE THUNDER STRIKE!

HIT 1:
  └─ Circle at position [2]
  └─ [DODGE] button highlights
  └─ 0.5s to respond
  └─ Player: PERFECT ✅
  └─ Companion counterattacks: 30 damage

HIT 2:
  └─ Circle at position [6]
  └─ [BLOCK] button highlights
  └─ 0.4s to respond
  └─ Player: PERFECT ✅
  └─ Companion counterattacks: 30 damage

HIT 3:
  └─ Circle at position [4]
  └─ [COUNTER] button highlights
  └─ 0.3s to respond (FASTER!)
  └─ Player: PERFECT ✅
  └─ Companion counterattacks: 45 damage (1.5x bonus!)

COMBO COMPLETE!
Total damage dealt: 30 + 30 + 45 = 105
Total damage taken: 0 (all perfect)
UI shows: "PERFECT CHAIN!" (gold text + flash)
```

### **Combo Difficulty Scaling:**

| Enemy Rarity | Combo Length | Time Per Hit | Perfect Bonus |
|--------------|--------------|--------------|---------------|
| Common | None | N/A | N/A |
| Uncommon | 2 hits | 1.0s | +25% final hit |
| Rare | 2-3 hits | 0.8s | +50% final hit |
| Epic | 3-4 hits | 0.5s | +100% final hit |
| Legendary | 4-5 hits | 0.4s | +150% final hit |
| Unique/Boss | 5-10 hits | 0.3s | +200% final hit |

### **Combo Failure Consequences:**

```lua
-- If player misses ANY hit in combo
function ComboFailure(comboAttack, missedHit)
    -- Player takes damage from missed hit
    ApplyDamage(comboAttack.BaseDamage)
    
    -- Combo breaks
    comboAttack.Active = false
    
    -- No bonus damage on remaining hits
    comboAttack.PerfectBonus = nil
    
    -- Visual feedback
    ShowText("COMBO BROKEN!", Color3.fromRGB(255, 0, 0))
end
```

---

## ⚡ SPECIAL ATTACK TYPES

### **Attack Type Taxonomy:**

#### **1. HEAVY STRIKE**
```
Description: Slow, powerful attack
Used by: Tank-type enemies (Stone, Nature)

Mechanics:
• Deals 2x normal damage
• Circle shrinks SLOWLY (easy to perfect)
• BUT if player MISSES → devastating damage
• Good risk/reward for player

Example:
RockGolem uses BOULDER SLAM
  └─ Damage: 100 (2x normal 50)
  └─ Shrink time: 2.5s (very slow)
  └─ Perfect zone: 40% (generous)
  └─ Miss = player takes 100 damage
  └─ Perfect = player takes 0, counters for 60
```

#### **2. RAPID ASSAULT**
```
Description: Multiple weak hits rapidly
Used by: Speed-type enemies (Air, Lightning)

Mechanics:
• 3-5 hits in quick succession
• Each hit deals 0.5x damage
• Circle shrinks FAST (hard to perfect)
• Miss one = chip damage adds up

Example:
WindRaptor uses TALON FLURRY
  └─ 4 hits x 15 damage = 60 total
  └─ Shrink time: 0.4s per hit
  └─ Perfect zone: 10%
  └─ Perfect all 4 = 0 damage taken, 80 damage dealt
  └─ Miss 2 = 30 damage taken, 40 damage dealt
```

#### **3. ELEMENTAL BURST**
```
Description: Magical attack with status effect
Used by: Elemental enemies (Fire, Water, Lightning)

Mechanics:
• Deals normal damage + status effect
• Status persists for 10 seconds
• Can stack multiple effects
• Specific buttons counter specific elements

Status Effects:
BURN (Fire): -5 HP per second for 10s
  └─ Counter: BLOCK with water companion
  
STUN (Lightning): Next counter deals 0 damage
  └─ Counter: DODGE perfectly
  
FREEZE (Ice): Next circle shrinks 50% faster
  └─ Counter: BLOCK with fire companion
  
POISON (Nature): -3 HP per second for 15s
  └─ Counter: Use healing item

Example:
FlameDrake uses INFERNO WAVE
  └─ Damage: 40
  └─ Status: BURN (-5 HP/s for 10s)
  └─ Total potential: 40 + 50 = 90 damage
  └─ Perfect BLOCK = 0 immediate damage, burn negated
  └─ Miss = 40 immediate + 50 over time = 90 total
```

#### **4. COUNTER WINDOW**
```
Description: Enemy exposes weakness briefly
Used by: Boss-type enemies

Mechanics:
• Enemy telegraphs special attack
• Button is COUNTER (red)
• Perfect timing = massive bonus damage
• Miss = enemy gains buff

Example:
VoidLord uses DARK ARMOR CHARGE
  └─ Telegraphs for 1.5s
  └─ [COUNTER] window appears (0.3s)
  └─ Perfect counter = 200 damage + armor broken
  └─ Miss = VoidLord gains +50% defense for 30s
```

### **Attack Selection AI:**

```lua
-- Enemy chooses attacks based on HP phase and RNG

function SelectAttack(enemy)
    local hpPercent = enemy.HP / enemy.MaxHP
    local attacks = {}
    
    if hpPercent > 0.5 then
        -- Phase 1: Normal attacks
        attacks = {
            {Type = "Normal", Weight = 70},
            {Type = "HeavyStrike", Weight = 20},
            {Type = "ElementalBurst", Weight = 10},
        }
    elseif hpPercent > 0.25 then
        -- Phase 2: More aggressive
        attacks = {
            {Type = "Normal", Weight = 40},
            {Type = "RapidAssault", Weight = 30},
            {Type = "ElementalBurst", Weight = 20},
            {Type = "ComboAttack", Weight = 10},
        }
    else
        -- Phase 3: Desperate/Enraged
        attacks = {
            {Type = "RapidAssault", Weight = 30},
            {Type = "HeavyStrike", Weight = 20},
            {Type = "ComboAttack", Weight = 30},
            {Type = "CounterWindow", Weight = 20},
        }
    end
    
    return WeightedRandom(attacks)
end
```

---

## 💊 HEALING & REVIVAL MECHANICS

### **Consumable Items:**

#### **During Combat (Emergency Use):**

```lua
EmergencyHeal = {
    Name = "Health Potion",
    Effect = function(player)
        player.HP = math.min(player.HP + 50, player.MaxHP)
    end,
    Cooldown = 10, -- seconds, prevent spam
    UsesPerExpedition = 3, -- Limited quantity
    Cost = 50, -- Currency to buy
}

AdrenalineShot = {
    Name = "Adrenaline Injection",
    Effect = function(player, companion)
        player.HP = math.min(player.HP + 30, player.MaxHP)
        if not companion.IsFainted then
            companion.HP = math.min(companion.HP + 30, companion.MaxHP)
        end
    end,
    UsesPerExpedition = 1, -- Rare item
    Cost = 200,
}

RevivalScroll = {
    Name = "Pet Revival Scroll",
    Effect = function(companion)
        if companion.IsFainted then
            companion.IsFainted = false
            companion.HP = companion.MaxHP * 0.5 -- Revive at 50%
        end
    end,
    UsesPerExpedition = 1,
    Cost = 500, -- Expensive!
}
```

#### **Outside Combat (Passive Healing):**

```lua
Bandages = {
    Name = "Bandages",
    Effect = function(player)
        -- Heal over time, can't move during
        local healAmount = 100
        local duration = 10
        
        player.IsHealing = true
        player.CanMove = false
        
        for i = 1, duration do
            task.wait(1)
            player.HP = math.min(player.HP + (healAmount/duration), player.MaxHP)
        end
        
        player.IsHealing = false
        player.CanMove = true
    end,
    Cost = 20, -- Cheap but slow
}

PetFood = {
    Name = "Pet Nutrition Bar",
    Effect = function(companion)
        if not companion.IsFainted then
            companion.HP = math.min(companion.HP + 50, companion.MaxHP)
        end
    end,
    Instant = true,
    Cost = 30,
}
```

### **Companion Healing Abilities:**

```lua
-- Some companions have built-in healing

LifeBloom = { -- Nature pet passive
    Name = "Natural Regeneration",
    Effect = function(companion, deltaTime)
        if not InCombat then
            companion.HP = math.min(
                companion.HP + (5 * deltaTime),
                companion.MaxHP
            )
        end
    end,
}

Lifesteal = { -- Nature pet active
    Name = "Vampiric Strike",
    Effect = function(damageDealt, companion)
        local healAmount = damageDealt * 0.5
        companion.HP = math.min(
            companion.HP + healAmount,
            companion.MaxHP
        )
    end,
    TriggerOn = "Perfect timing",
}
```

### **Life Transfer System (Advanced):**

```lua
-- Player can sacrifice own HP to heal companion
-- Unlock via skill tree

LifeTransfer = {
    Name = "Life Link",
    Unlocked = false, -- Requires skill point
    
    Effect = function(player, companion, amount)
        if player.HP > amount then
            player.HP = player.HP - amount
            companion.HP = math.min(
                companion.HP + (amount * 2), -- 1:2 ratio (efficient)
                companion.MaxHP
            )
            return true
        else
            return false -- Not enough HP
        end
    end,
    
    UsageExample = function()
        -- Player has 80 HP, Companion has 20/100 HP
        -- Player transfers 30 HP
        -- Result: Player 50 HP, Companion 80 HP
    end
}
```

### **Base Healing (Free but Requires Extraction):**

```lua
-- At base, full restore for free
function BaseHealing(player, companion)
    player.HP = player.MaxHP
    
    if companion.IsFainted then
        companion.IsFainted = false
    end
    companion.HP = companion.MaxHP
    
    -- Remove all status effects
    player.StatusEffects = {}
    
    -- This encourages extraction gameplay
end
```

---

## 🔧 TECHNICAL IMPLEMENTATION

### **File Structure:**

```
src/
├── Server/
│   ├── Services/
│   │   ├── CombatService.lua          # Main combat orchestrator
│   │   ├── DamageCalculationService.lua # Damage formulas
│   │   ├── TimingValidationService.lua  # Server-side timing checks
│   │   ├── CompanionService.lua        # Companion stats/abilities
│   │   └── EnemyAIService.lua          # Enemy attack patterns
│   └── ServerMain.server.lua
│
├── Client/
│   ├── Controllers/
│   │   ├── CombatUIController.lua      # UI rendering
│   │   ├── InputController.lua         # Button tap handling
│   │   └── AnimationController.lua     # Visual effects
│   └── ClientMain.client.lua
│
├── Shared/
│   ├── CombatConstants.lua             # Shared combat config
│   ├── PetDefinitions.lua              # All pet stats
│   ├── AttackPatterns.lua              # Enemy attack data
│   └── AbilityDefinitions.lua          # Companion abilities
│
└── ReplicatedStorage/
    └── RemoteEvents/
        ├── CombatStart.lua
        ├── DefenseInput.lua
        ├── CombatUpdate.lua
        └── CombatEnd.lua
```

### **Server-Side Combat Flow:**

```lua
-- CombatService.lua (Server)

local CombatService = {}

function CombatService:InitiateCombat(player, enemyPet)
    -- Create combat session
    local session = {
        Player = player,
        Companion = player.ActiveCompanion,
        Enemy = enemyPet,
        Round = 0,
        CombatActive = true,
    }
    
    -- Store session
    self.ActiveSessions[player] = session
    
    -- Notify client to open UI
    RemoteEvents.CombatStart:FireClient(player, {
        EnemyName = enemyPet.Name,
        EnemyHP = enemyPet.HP,
        EnemyRarity = enemyPet.Rarity,
    })
    
    -- Start first round
    self:StartRound(session)
end

function CombatService:StartRound(session)
    session.Round = session.Round + 1
    
    -- Enemy selects attack
    local attack = EnemyAIService:SelectAttack(session.Enemy)
    
    -- Determine defense type and position
    local defenseType = attack.DefenseType -- DODGE/BLOCK/COUNTER
    local position = math.random(1, 8) -- Random position
    
    -- Calculate timing window
    local rarityConfig = CombatConstants.RarityConfig[session.Enemy.Rarity]
    local shrinkTime = rarityConfig.ShrinkSpeed
    local perfectZone = rarityConfig.PerfectZone
    
    -- Send to client
    RemoteEvents.CombatUpdate:FireClient(session.Player, {
        AttackName = attack.Name,
        DefenseType = defenseType,
        Position = position,
        ShrinkTime = shrinkTime,
        PerfectZone = perfectZone,
    })
    
    -- Start timing window
    session.StartTime = tick()
    session.ShrinkTime = shrinkTime
    session.CurrentAttack = attack
end

function CombatService:ProcessDefenseInput(player, inputTime, buttonPressed)
    local session = self.ActiveSessions[player]
    if not session or not session.CombatActive then return end
    
    -- Validate timing
    local timingResult = TimingValidationService:ValidateTiming(
        session.StartTime,
        session.ShrinkTime,
        inputTime
    )
    
    -- Validate button
    local correctButton = session.CurrentAttack.DefenseType == buttonPressed
    if not correctButton then
        timingResult = "Miss" -- Wrong button = miss
    end
    
    -- Calculate damage
    local damageResults = DamageCalculationService:Calculate(
        session.Enemy,
        session.Companion,
        session.Player,
        timingResult
    )
    
    -- Apply damage
    session.Enemy.HP = session.Enemy.HP - damageResults.EnemyDamage
    session.Companion.HP = session.Companion.HP - damageResults.CompanionDamage
    session.Player.HP = session.Player.HP - damageResults.PlayerDamage
    
    -- Check fainted
    if session.Companion.HP <= 0 then
        session.Companion.HP = 0
        session.Companion.IsFainted = true
    end
    
    -- Send results to client for visual feedback
    RemoteEvents.CombatUpdate:FireClient(player, {
        TimingResult = timingResult,
        EnemyHP = session.Enemy.HP,
        CompanionHP = session.Companion.HP,
        PlayerHP = session.Player.HP,
        EnemyDamage = damageResults.EnemyDamage,
        PlayerDamage = damageResults.PlayerDamage + damageResults.CompanionDamage,
    })
    
    -- Check end conditions
    if session.Enemy.HP <= 0 then
        self:EndCombat(session, "Victory")
    elseif session.Player.HP <= 0 then
        self:EndCombat(session, "Defeat")
    else
        -- Next round
        task.wait(1.5) -- Brief pause between rounds
        self:StartRound(session)
    end
end

function CombatService:EndCombat(session, result)
    session.CombatActive = false
    
    if result == "Victory" then
        -- Trigger weakened state
        session.Enemy.State = "Weakened"
        
        -- Notify client for capture phase
        RemoteEvents.CombatEnd:FireClient(session.Player, {
            Result = "Victory",
            CaptureBonus = CalculateCaptureBonus(session),
        })
    else
        -- Player defeated
        RemoteEvents.CombatEnd:FireClient(session.Player, {
            Result = "Defeat",
        })
        
        -- Handle defeat consequences (cargo loss, etc.)
        PlayerDefeatService:HandleDefeat(session.Player)
    end
    
    -- Clean up session
    self.ActiveSessions[session.Player] = nil
end

return CombatService
```

### **Client-Side UI Controller:**

```lua
-- CombatUIController.lua (Client)

local CombatUIController = {}

function CombatUIController:ShowCombatUI(enemyData)
    -- Create/show UI
    local ui = self.CombatUI
    ui.Visible = true
    
    -- Update enemy info
    ui.EnemyName.Text = enemyData.EnemyName
    ui.EnemyHP.Text = enemyData.EnemyHP .. " HP"
    ui.RarityLabel.Text = enemyData.EnemyRarity
end

function CombatUIController:StartDefensePhase(roundData)
    -- Highlight correct button
    self:HighlightButton(roundData.DefenseType)
    
    -- Spawn circle at position
    local circle = self:CreateCircle(roundData.Position)
    
    -- Animate shrinking
    local shrinkTween = TweenService:Create(circle, 
        TweenInfo.new(roundData.ShrinkTime, Enum.EasingStyle.Linear),
        {Size = UDim2.new(0.05, 0, 0.05, 0)} -- Shrink to dot size
    )
    shrinkTween:Play()
    
    -- Track perfect zone
    self.CurrentCircle = circle
    self.PerfectZoneSize = roundData.PerfectZone
    self.StartTime = tick()
end

function CombatUIController:OnButtonPressed(buttonType)
    if not self.CurrentCircle then return end
    
    -- Calculate timing
    local inputTime = tick()
    local elapsed = inputTime - self.StartTime
    
    -- Send to server
    RemoteEvents.DefenseInput:FireServer(inputTime, buttonType)
    
    -- Immediately show visual feedback (optimistic)
    -- Server will validate and correct if needed
    self:ShowPreliminaryFeedback(elapsed)
end

function CombatUIController:ShowResult(resultData)
    -- Show timing result
    local resultText = resultData.TimingResult -- "Perfect"/"Good"/"Miss"
    
    if resultText == "Perfect" then
        self:ShowPerfectEffect()
    elseif resultText == "Good" then
        self:ShowGoodEffect()
    else
        self:ShowMissEffect()
    end
    
    -- Show damage numbers
    if resultData.EnemyDamage > 0 then
        self:ShowDamageNumber(resultData.EnemyDamage, "Enemy", "Green")
    end
    
    if resultData.PlayerDamage > 0 then
        self:ShowDamageNumber(resultData.PlayerDamage, "Player", "Red")
    end
    
    -- Update HP bars
    self:UpdateHPBars(resultData)
    
    -- Clean up circle
    self.CurrentCircle:Destroy()
    self.CurrentCircle = nil
end

return CombatUIController
```

### **Timing Validation (Server):**

```lua
-- TimingValidationService.lua (Server)

local TimingValidationService = {}

function TimingValidationService:ValidateTiming(startTime, shrinkTime, inputTime)
    local elapsed = inputTime - startTime
    
    -- Timing windows
    local perfectWindow = shrinkTime * 0.95 -- Last 5% of shrink
    local goodWindowStart = shrinkTime * 0.85 -- 85%-95%
    local goodWindowEnd = shrinkTime * 1.05 -- Up to 5% after
    
    if elapsed >= perfectWindow and elapsed <= shrinkTime then
        return "Perfect"
    elseif elapsed >= goodWindowStart and elapsed <= goodWindowEnd then
        return "Good"
    else
        return "Miss"
    end
end

-- Anti-cheat: Prevent timing manipulation
function TimingValidationService:ValidateInputTiming(player, inputTime)
    local now = tick()
    local ping = player:GetNetworkPing()
    local maxValidTime = now + ping + 0.1 -- Allow small variance
    
    if inputTime > maxValidTime then
        -- Suspicious timing, likely cheating
        warn("Suspicious timing from player:", player.Name)
        return false
    end
    
    return true
end

return TimingValidationService
```

---

## 📊 BALANCE TABLES

### **Complete Stat Tables:**

#### **Enemy Pet Stats:**

```lua
EnemyStats = {
    Common = {
        BaseHP = 100,
        AttackDamage = 20,
        ShrinkSpeed = 2.0,
        PerfectZone = 0.30,
        AttacksPerFight = {3, 4},
        ComboChance = 0,
        SpecialAttackChance = 0.1,
    },
    Uncommon = {
        BaseHP = 150,
        AttackDamage = 25,
        ShrinkSpeed = 1.5,
        PerfectZone = 0.25,
        AttacksPerFight = {4, 5},
        ComboChance = 0.2,
        SpecialAttackChance = 0.15,
    },
    Rare = {
        BaseHP = 250,
        AttackDamage = 35,
        ShrinkSpeed = 1.0,
        PerfectZone = 0.15,
        AttacksPerFight = {5, 6},
        ComboChance = 0.4,
        SpecialAttackChance = 0.25,
    },
    Epic = {
        BaseHP = 400,
        AttackDamage = 50,
        ShrinkSpeed = 0.7,
        PerfectZone = 0.10,
        AttacksPerFight = {6, 8},
        ComboChance = 0.6,
        SpecialAttackChance = 0.35,
    },
    Legendary = {
        BaseHP = 600,
        AttackDamage = 70,
        ShrinkSpeed = 0.4,
        PerfectZone = 0.05,
        AttacksPerFight = {8, 10},
        ComboChance = 0.8,
        SpecialAttackChance = 0.5,
    },
    Unique = {
        BaseHP = 800,
        AttackDamage = 90,
        ShrinkSpeed = 0.3,
        PerfectZone = 0.03,
        AttacksPerFight = {10, 15},
        ComboChance = 1.0,
        SpecialAttackChance = 0.7,
    },
}
```

#### **Companion Pet Archetypes:**

```lua
CompanionArchetypes = {
    Tank = {
        BaseHP = 100,
        BaseAttack = 30,
        DefensePercent = 0.80,
        HPGrowthPerLevel = 5,
        AttackGrowthPerLevel = 2,
        Examples = {"StoneGuard", "IronTurtle", "MossBeast"},
    },
    DPS = {
        BaseHP = 50,
        BaseAttack = 60,
        DefensePercent = 0.40,
        HPGrowthPerLevel = 2,
        AttackGrowthPerLevel = 4,
        Examples = {"FlameRaptor", "StormHawk", "VoidReaper"},
    },
    Balanced = {
        BaseHP = 75,
        BaseAttack = 40,
        DefensePercent = 0.60,
        HPGrowthPerLevel = 3,
        AttackGrowthPerLevel = 3,
        Examples = {"TideRunner", "WindDancer", "CrystalFox"},
    },
    Support = {
        BaseHP = 60,
        BaseAttack = 35,
        DefensePercent = 0.70,
        HPGrowthPerLevel = 3,
        AttackGrowthPerLevel = 2,
        SpecialAbility = "Healing/Buff focused",
        Examples = {"LifeBloom", "LightBearer", "HarmonySprite"},
    },
}
```

#### **Consumable Items:**

```lua
Consumables = {
    HealthPotion = {
        HealAmount = 50,
        Target = "Player",
        Cooldown = 10,
        MaxPerExpedition = 3,
        Cost = 50,
    },
    AdrenalineShot = {
        HealAmount = 30,
        Target = "Both",
        Cooldown = 30,
        MaxPerExpedition = 1,
        Cost = 200,
    },
    RevivalScroll = {
        Effect = "Revive companion at 50% HP",
        Target = "Companion",
        Cooldown = 0,
        MaxPerExpedition = 1,
        Cost = 500,
    },
    Bandages = {
        HealAmount = 100,
        Target = "Player",
        Duration = 10,
        RequiresStanding = true,
        Cost = 20,
    },
    PetFood = {
        HealAmount = 50,
        Target = "Companion",
        Instant = true,
        Cost = 30,
    },
}
```

#### **Damage Multipliers:**

```lua
DamageMultipliers = {
    Timing = {
        Perfect = 0,    -- No damage taken
        Good = 0.5,     -- 50% damage taken
        Miss = 1.0,     -- 100% damage taken
    },
    
    Counterattack = {
        Perfect = 1.0,  -- 100% companion attack
        Good = 0.5,     -- 50% companion attack
        Miss = 0,       -- No counterattack
    },
    
    ComboBonus = {
        TwoHitPerfect = 1.25,   -- +25% final hit
        ThreeHitPerfect = 1.5,  -- +50% final hit
        FourHitPerfect = 2.0,   -- +100% final hit
        FiveHitPerfect = 2.5,   -- +150% final hit
    },
    
    SpecialAttacks = {
        HeavyStrike = 2.0,      -- 2x damage
        RapidAssault = 0.5,     -- 0.5x per hit
        ElementalBurst = 1.0,   -- Normal + status
    },
}
```

---

## 🎯 IMPLEMENTATION CHECKLIST

### **Phase 1: Core Combat (Week 1)**
- [ ] Create CombatService.lua (server)
- [ ] Create DamageCalculationService.lua (server)
- [ ] Create TimingValidationService.lua (server)
- [ ] Create CombatUIController.lua (client)
- [ ] Create InputController.lua (client)
- [ ] Implement basic combat loop (single attack)
- [ ] Implement HP tracking (player, companion, enemy)
- [ ] Implement damage distribution (hybrid system)
- [ ] Test with Common pets only

### **Phase 2: Timing System (Week 2)**
- [ ] Implement shrinking circle animation
- [ ] Implement 8-position random spawn
- [ ] Implement timing validation (Perfect/Good/Miss)
- [ ] Implement button highlighting
- [ ] Add visual feedback (colors, flashes)
- [ ] Add damage number displays
- [ ] Test timing accuracy and responsiveness

### **Phase 3: Companion System (Week 3)**
- [ ] Create CompanionService.lua
- [ ] Implement companion stats (HP, Attack, Defense%)
- [ ] Implement companion abilities (passive/active)
- [ ] Implement companion leveling/progression
- [ ] Implement fainted state mechanics
- [ ] Test all three archetypes (Tank/DPS/Balanced)

### **Phase 4: Enemy Variety (Week 4)**
- [ ] Create EnemyAIService.lua
- [ ] Implement attack patterns by rarity
- [ ] Implement combo attacks
- [ ] Implement special attack types
- [ ] Implement HP-based phases
- [ ] Test all rarity tiers

### **Phase 5: Polish & Balance (Week 5)**
- [ ] Implement healing/revival system
- [ ] Implement status effects
- [ ] Add sound effects and music
- [ ] Add particle effects
- [ ] Balance damage numbers
- [ ] Playtest and iterate

---

## 📝 CONCLUSION

This combat system provides:

✅ **Skill-based gameplay** (timing over stats)  
✅ **Strategic depth** (companion loadouts, ability choices)  
✅ **Mobile optimization** (single-input, clear visuals)  
✅ **Endless scalability** (rarity tiers, infinite progression)  
✅ **Spectator appeal** (combo chains, perfect plays)  
✅ **Fair challenge** (no pay-to-win, skill matters)

**Total Development Time: ~5 weeks for full implementation**

---

**Document Status:** ✅ Ready for Development  
**Next Step:** Begin Phase 1 implementation  
**Questions?** Refer to specific sections above for detailed mechanics
