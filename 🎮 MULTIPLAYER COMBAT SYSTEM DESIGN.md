# 🎮 MULTIPLAYER COMBAT SYSTEM DESIGN
**Idol Guardians: Eternal Wilds**

Version: 1.0  
Last Updated: December 2025

---

## 📋 TABLE OF CONTENTS

1. [Core Philosophy](#core-philosophy)
2. [Three-Mode System Overview](#three-mode-system-overview)
3. [Mode 1: Solo Expeditions](#mode-1-solo-expeditions)
4. [Mode 2: Co-op PvE Expeditions](#mode-2-co-op-pve-expeditions)
5. [Mode 3: PvPvE Expeditions](#mode-3-pvpve-expeditions)
6. [Hybrid Proximity Join System](#hybrid-proximity-join-system)
7. [Anti-Griefing Systems](#anti-griefing-systems)
8. [Matchmaking & Server Architecture](#matchmaking--server-architecture)
9. [Reward Distribution](#reward-distribution)
10. [Technical Implementation](#technical-implementation)

---

## 🎯 CORE PHILOSOPHY

### Design Pillars

**1. Player Choice First**
- Players choose their experience before deployment
- No forced PvP encounters
- Clear risk/reward communication

**2. Fair Competition**
- Skill-based combat, not gear-check gatekeeping
- Anti-griefing built into core systems
- Power bracket matchmaking

**3. Social Play Encouraged**
- Co-op is rewarding and fun
- Proximity-based organic grouping
- Fair loot distribution systems

**4. High-Stakes Optional**
- PvPvE offers significantly better rewards
- But never required for progression
- Balanced risk vs reward curve

---

## 🌍 THREE-MODE SYSTEM OVERVIEW

### Mode Selection (Pre-Deployment)

Players choose ONE mode before entering expedition:

```
┌─────────────────────────────────────────┐
│     🎮 SELECT EXPEDITION MODE           │
├─────────────────────────────────────────┤
│                                         │
│  🧍 SOLO                                │
│  ├─ Play alone                          │
│  ├─ Standard rewards                    │
│  └─ No player interaction               │
│                                         │
│  👥 CO-OP PvE                           │
│  ├─ Team up (2-6 players)               │
│  ├─ Shared encounters                   │
│  └─ Cooperative rewards                 │
│                                         │
│  ⚔️ PvPvE HIGH STAKES                   │
│  ├─ Player combat enabled               │
│  ├─ 150% loot multiplier                │
│  ├─ Higher rare spawn rates             │
│  └─ Risk of losing cargo to players     │
│                                         │
└─────────────────────────────────────────┘
```

### Why Three Modes?

| Mode | Target Audience | Core Appeal |
|------|----------------|-------------|
| **Solo** | Casual players, introverts, learners | Safe exploration, no pressure |
| **Co-op PvE** | Social players, friends, grinders | Teamwork, shared victories |
| **PvPvE** | Competitive players, high-risk seekers | Adrenaline, massive rewards |

---

## 🧍 MODE 1: SOLO EXPEDITIONS

### Overview
Pure single-player experience with no multiplayer interactions.

### Core Features

**✅ What You Get**
- Complete solo instance
- Standard pet spawn rates
- Standard extraction timers
- Full control over pacing
- No cargo theft risk

**⚙️ Technical Details**
- Dedicated server instance (1 player max)
- Full world generation
- All biomes accessible
- Normal difficulty scaling

**📊 Reward Structure**
- Base reward rates (100%)
- Standard pet rarity pools
- Normal currency drops
- Solo leaderboards available

### Use Cases
- Learning game mechanics
- Casual play sessions
- Testing builds
- Peaceful farming
- Story/exploration focus

---

## 👥 MODE 2: CO-OP PvE EXPEDITIONS

### Overview
Cooperative multiplayer with **NO player combat**. Players work together against PvE threats.

### Core Features

**✅ What You Get**
- Team size: 2-6 players
- Shared encounters
- Combined firepower
- Strategic teamwork
- Social experience

**🚫 What You DON'T Get**
- No player damage
- No cargo theft
- No forced competition
- No griefing possible

### Squad Formation

**Pre-Made Squads**
```lua
-- Friends form squad before deployment
Squad = {
    Leader = Player1,
    Members = {Player2, Player3, Player4},
    LootMode = "RollSystem", -- or "Assigned"
}
```

**Proximity Join System (Hybrid)**
```lua
-- Players can join nearby allies during expedition
if ProximityDetected and BothPlayersConsent then
    FormTemporarySquad()
end
```

See [Hybrid Proximity Join System](#hybrid-proximity-join-system) for details.

### Shared Encounter Mechanics

**Boss Fights**
- All squad members can damage boss
- Aggro distributed across team
- Shared capture opportunity
- Loot distribution at end

**Capture Protocol**
```
1. Squad defeats pet → Pet enters weakened state
2. Squad collectively decides who captures
3. Options:
   - Designated capturer (agreed beforehand)
   - Roll system (RNG decides)
   - Pass/Need (like MMO loot)
4. Success → Pet goes to winner
5. Failure → Chest spawns, squad splits loot
```

### Reward Distribution Systems

See [Reward Distribution](#reward-distribution) section for full details.

**Quick Summary:**
- **Roll System**: Fair RNG for equal chance
- **Assigned System**: Leader designates rewards
- **Pass/Need**: Players bid on items they want

### Difficulty Scaling

Co-op encounters scale with squad size:

| Squad Size | Pet HP | Pet Damage | Spawn Rate |
|-----------|--------|------------|------------|
| 2 players | 150% | 110% | 120% |
| 3 players | 200% | 120% | 140% |
| 4 players | 250% | 130% | 160% |
| 5-6 players | 300% | 140% | 180% |

**Why Scale?**
- Prevents trivializing content
- Maintains challenge
- Rewards coordination

### Communication Tools

**Built-In Systems**
- Ping markers (points of interest)
- Quick chat commands
- Minimap shared visibility
- Squad health bars

---

## ⚔️ MODE 3: PvPvE EXPEDITIONS

### Overview
High-stakes mode where **player combat is enabled**. Risk losing cargo to other players, but gain significantly better rewards.

### Risk vs Reward

**🎁 Rewards (Why Play PvPvE)**
- **150% base loot multiplier**
- **2x legendary spawn rate**
- **Exclusive unique pet variants**
- **PvPvE-only cosmetics**
- **Seasonal ranking rewards**
- **Special crafting materials**

**⚠️ Risks**
- Players can attack you for cargo
- Death = lose ALL carried cargo
- Extraction becomes tactical choice
- Higher pressure gameplay

### The Pet Duel System (Core PvP Mechanic)

**Why Pet Duels Instead of Direct PvP?**

Traditional PvP problems we're avoiding:
- Instant kills with no counterplay
- Gear-check victories (rich players auto-win)
- Spawn camping
- Griefing low-level players

**How Pet Duels Work**

```
┌──────────────────────────────────────────────┐
│         PET DUEL INITIATION                  │
├──────────────────────────────────────────────┤
│                                              │
│  Player A wants to attack Player B           │
│                                              │
│  ✅ Validation Checks:                       │
│     - Is Player B carrying cargo?            │
│     - Is Player A in same bracket?           │
│     - Is area a safe zone? (No)              │
│     - Does Player A have stake?              │
│                                              │
│  If all pass → DUEL BEGINS                   │
│                                              │
│  ⚔️ DUEL PHASE:                              │
│                                              │
│  Both players' ACTIVE COMPANION PET          │
│  becomes a "Boss Proxy"                      │
│                                              │
│  ┌─────────────┐        ┌─────────────┐     │
│  │ Player A    │  VS    │ Player B    │     │
│  │ must defeat │        │ must defeat │     │
│  │ Pet B       │        │ Pet A       │     │
│  └─────────────┘        └─────────────┘     │
│                                              │
│  First to defeat opponent's pet WINS         │
│                                              │
│  🏆 WINNER GETS:                             │
│     - Opponent's cargo (or %)                │
│     - Bonus PvP tokens                       │
│     - Ranking points                         │
│                                              │
│  💀 LOSER:                                   │
│     - Loses cargo                            │
│     - Returns to base                        │
│     - Keeps base inventory                   │
│                                              │
└──────────────────────────────────────────────┘
```

### Pet Duel Mechanics Deep Dive

**Companion Pet Selection**
- Each player designates 1 "Active Companion" before deployment
- This companion:
  - Follows player in world
  - Provides passive buffs
  - Becomes "Boss Proxy" in PvP

**Duel Arena Mechanics**
```lua
-- When duel starts:
1. Both players frozen in place (can't run)
2. 3-second countdown
3. Pet Boss Proxies spawn
4. Players fight opponent's pet (not each other directly)
5. Pets use their skill trees, elements, and stats
6. First pet defeated = owner loses duel
```

**Why This Works**
- ✅ Skill-based: Pet builds, timing, strategy matter
- ✅ Fair: Both players fight "bosses" of similar power
- ✅ Engaging: Pet customization becomes PvP meta
- ✅ No instant kills: Duels take 30-90 seconds
- ✅ Counterplay exists: Dodging, pet abilities, items

### Staked PvP System

**The Stake Requirement**

To initiate a duel, attacker must stake:
- PvP Tokens (earned from PvPvE mode)
- OR equivalent currency value
- OR rare materials

**Stake Outcomes**
```
Attacker Wins → Keeps stake + gets defender's cargo
Attacker Loses → Defender claims the stake
Defender Escapes → Stake consumed (burned)
```

**Why Stakes Matter**
- Prevents random griefing
- Makes attacks meaningful decisions
- Punishes failed ganks
- Creates risk for attackers too

### Target Selection Rules

**Who Can Be Attacked?**

✅ **Valid Targets:**
- Players carrying cargo (captured pets)
- Players in same power bracket
- Players outside safe zones
- Players not in extraction animation

❌ **Invalid Targets:**
- Players with no cargo (optional rule variant)
- Players in safe zones
- Players in extraction countdown (final 10s)
- Players in different brackets

**Power Bracket System**

Players matched by approximate power:

| Bracket | Criteria | Example |
|---------|----------|---------|
| Novice | Base level 1-25 | New players |
| Veteran | Base level 26-75 | Mid-tier |
| Elite | Base level 76-150 | Advanced |
| Master | Base level 151+ | Endgame |

**Cross-bracket attacks disabled** to prevent seal-clubbing.

### Cargo Loss Rules

**On Death in PvPvE:**

**Full Loss (Harsh Variant)**
```lua
-- Player loses everything in cargo
Cargo = {} -- All captured pets lost
Items = {} -- All consumables lost
```

**Partial Loss (Balanced Variant)**
```lua
-- Player loses 50-75% of cargo
LossPercentage = 0.75
LostPets = Cargo * LossPercentage
RemainingPets = Cargo * (1 - LossPercentage)
```

**Insured Cargo (Premium Option)**
```lua
-- Players can "insure" pets before deployment
InsuredPets = {Pet1, Pet2} -- Protected from loss
Cost = InsuranceFee * PetRarity
```

**Design Choice:** We recommend **partial loss (75%)** as it:
- Stings enough to matter
- Doesn't fully punish players
- Keeps them engaged

---

## 🤝 HYBRID PROXIMITY JOIN SYSTEM

### The Problem with Pure Random Matchmaking

**Issues:**
- Players paired with randoms (no communication)
- Loot drama guaranteed
- No social bonds form
- Feels impersonal

**Issues with Pure Solo:**
- Isolating experience
- Misses social potential
- Can't organically help others

### The Solution: Hybrid System

**Pre-Deployment Options**

```
┌────────────────────────────────────┐
│   CO-OP DEPLOYMENT OPTIONS         │
├────────────────────────────────────┤
│                                    │
│  🎯 SQUAD WITH FRIENDS             │
│  └─ Invite 1-5 friends directly    │
│                                    │
│  🌍 ALLOW PROXIMITY JOINS          │
│  ├─ Deploy solo initially          │
│  ├─ Can join/be joined by others   │
│  └─ Both players must consent      │
│                                    │
│  🚫 PURE SOLO (No Joins)           │
│  └─ Completely alone, no grouping  │
│                                    │
└────────────────────────────────────┘
```

### Proximity Join Mechanics

**Trigger Conditions**
```lua
-- Two players in Co-op PvE mode
-- Within ~50 studs of each other
-- Both have "Allow Proximity Joins" enabled

if Distance(Player1, Player2) < ProximityRadius then
    if Player1.AllowProximityJoins and Player2.AllowProximityJoins then
        ShowJoinPrompt()
    end
end
```

**Join Prompt UI**
```
┌────────────────────────────────────┐
│  🤝 PLAYER NEARBY                  │
├────────────────────────────────────┤
│                                    │
│  "FireMage42" is nearby!           │
│                                    │
│  Form temporary squad?             │
│                                    │
│  [✓ Accept]    [✗ Decline]         │
│                                    │
│  Note: Loot will use Roll System   │
│                                    │
└────────────────────────────────────┘
```

**Both players must accept** to form squad.

### Temporary Squad Rules

**Duration**
- Squad persists until:
  - Either player extracts
  - Either player dies
  - Either player manually leaves
  - Extraction timer expires

**Loot Distribution**
- Default: **Roll System** (fair RNG)
- Can change to Assigned if both agree

**Leaving Squad**
```lua
-- Either player can leave at any time
Player:LeaveSquad() -- No penalty
```

### Why Hybrid Works

**✅ Flexibility**
- Players can choose social level
- Organic friendships form
- Not forced into randoms

**✅ Discovery**
- Meet players in the wild
- Natural conversation starters
- Build community

**✅ Safety**
- Consent-based system
- Can decline joins
- Can leave anytime

---

## 🛡️ ANTI-GRIEFING SYSTEMS

### Core Principle
**High-stakes PvPvE should reward skill and risk-taking, NOT griefing and toxicity.**

---

### 1. Power Bracket Matchmaking

**The Problem:** Level 200 players hunting level 10 newbies.

**The Solution:**

```lua
-- Players only matchmade with similar brackets
Brackets = {
    Novice = {MinLevel = 1, MaxLevel = 25},
    Veteran = {MinLevel = 26, MaxLevel = 75},
    Elite = {MinLevel = 76, MaxLevel = 150},
    Master = {MinLevel = 151, MaxLevel = 999},
}

-- Cross-bracket attacks impossible
if Attacker.Bracket ~= Defender.Bracket then
    DuelInitiation = false
    ShowMessage("Target in different power bracket")
end
```

**Bracket Progression**
- Players graduate brackets naturally
- No way to "smurf" (alt accounts face detection)
- Seasonal bracket resets possible

---

### 2. Cargo-Based Targeting

**The Problem:** Players attacking for fun, not loot.

**The Solution: "Loot or Leave" Rule**

```lua
-- Option A: Only cargo carriers can be attacked
if Player.CargoCount == 0 then
    CanBeAttacked = false
end

-- Option B: Attackers get NOTHING if target has no cargo
if Player.CargoCount == 0 then
    DuelReward = 0 -- No stake returned, no loot
    -- Makes attacking pointless
end
```

**Design Choice:** We recommend **Option B** because:
- Allows all PvP attempts
- But makes cargo-less attacks worthless
- Naturally discourages griefing

---

### 3. Staked PvP (Anti-Spam)

**The Problem:** Players spam-attacking everyone they see.

**The Solution:**

```lua
-- Attacker must pay upfront stake
AttackCost = {
    PvPTokens = 5, -- Earned only in PvPvE mode
    OR
    Currency = 1000, -- Significant amount
}

-- If attacker loses duel:
Defender:GiveReward(AttackCost) -- Defender gets the stake

-- If attacker wins:
Attacker:KeepStake() -- Gets stake back + loot
```

**Why This Works:**
- Attackers risk something EVERY time
- Failed ganks = loss
- Defenders rewarded for winning
- Spam attacks become expensive

---

### 4. Safe Zones

**The Problem:** Spawn camping and extraction camping.

**The Solution:**

```lua
-- Safe Zone Radius around base
SafeZoneRadius = 200 -- studs

if Distance(Player, BaseCenter) < SafeZoneRadius then
    PvPEnabled = false
    ShowMessage("Safe Zone: PvP Disabled")
end
```

**Safe Zone Rules:**
- No PvP initiation possible
- Small radius (not entire map)
- Only near spawn/extraction points

**Visual Indicator:**
- Blue dome/circle on ground
- UI icon when inside
- Audio cue on entry

---

### 5. Extraction Protection

**The Problem:** Camping extraction points to gank loaded players.

**The Solution: Tiered Protection**

```lua
-- Phase 1: Extraction Warning (30s before)
OnExtractionStart:
    Player.ExtractionStatus = "Warning"
    ShowCountdown(30)
    -- PvP still active

-- Phase 2: Extraction Countdown (10s)
OnExtractionFinal:
    Player.ExtractionStatus = "Extracting"
    ShowCountdown(10)
    -- PvP still active BUT...

-- Phase 3: Invulnerability (Final 5s)
if ExtractionTimer < 5 then
    Player.Invulnerable = true
    CanBeAttacked = false
end
```

**Why 5-Second Buffer?**
- Prevents last-second ganks
- Gives player guaranteed escape
- Still allows interception if player spotted early

---

### 6. Anti-Camping Detection

**The Problem:** Players lurking near extraction indefinitely.

**The Solution:**

```lua
-- Track time spent near extraction points
if Distance(Player, ExtractionPoint) < CampRadius then
    CampTime = CampTime + dt
end

-- After camping too long:
if CampTime > MaxCampTime then
    -- Reveal on map
    Player.Revealed = true
    ShowMapMarker(Player)
    
    -- Apply debuff
    Player.MovementSpeed = Player.MovementSpeed * 0.7
    
    -- Spawn PvE hunters
    SpawnHostilePets(Player.Position, "High Aggression")
end
```

**Camp Thresholds:**
- **60 seconds:** Warning message
- **90 seconds:** Map revealed
- **120 seconds:** Debuff applied
- **180 seconds:** PvE hunters spawn

**Why This Works:**
- Camping becomes dangerous
- Forces movement
- Gives advantage to extractors

---

### 7. Duel Cooldowns

**The Problem:** Players losing, respawning, immediately re-attacking.

**The Solution:**

```lua
-- After losing a duel
OnDuelLoss:
    Player.DuelCooldown = 300 -- 5 minutes
    
-- Cannot initiate duels during cooldown
if Player.DuelCooldown > 0 then
    CanInitiateDuel = false
    ShowMessage("Duel cooldown: " .. CooldownRemaining)
end
```

**Cooldown Rules:**
- Applies only to LOSING duels
- Winning has no cooldown
- Prevents revenge spam
- Allows strategic re-attacks after cooldown

---

### 8. Reputation System (Advanced)

**The Problem:** Serial griefers, even with stakes.

**The Solution: Hidden Reputation Score**

```lua
-- Track player behavior
ReputationFactors = {
    DuelsWon = +5,
    DuelsLost = 0,
    AttacksOnCargolessPlayers = -10,
    ReceivedReports = -20,
    FairExtractions = +2,
}

-- Low reputation = harsher matchmaking
if Player.Reputation < -50 then
    -- Matched only with other low-rep players
    Matchmaking.PreferLowRep = true
end
```

**Reputation Effects:**
- Purely for matchmaking
- Not shown to player (prevents gaming)
- Isolates griefers from normal players

---

### 9. Report System + Moderation

**Quick Report UI:**

```
┌────────────────────────────────────┐
│  Report Player                     │
├────────────────────────────────────┤
│                                    │
│  Reason:                           │
│  ○ Griefing / Harassment           │
│  ○ Exploiting                      │
│  ○ Offensive Name/Behavior         │
│                                    │
│  [Submit Report]                   │
│                                    │
└────────────────────────────────────┘
```

**Automated Actions:**
- 3+ reports → temporary matchmaking restriction
- 10+ reports → manual review
- Confirmed griefing → PvPvE mode ban

---

### 10. Extraction Point Variety

**The Problem:** One extraction = easy camping spot.

**The Solution: Multiple Random Exits**

```lua
-- Generate 3-5 extraction points per map
ExtractionPoints = {}
for i = 1, RandomRange(3, 5) do
    local Point = GenerateRandomExtractionPoint()
    ExtractionPoints[i] = Point
end

-- Each closes at different times
ExtractionPoints[1].CloseTime = 600 -- 10 min
ExtractionPoints[2].CloseTime = 900 -- 15 min
ExtractionPoints[3].CloseTime = 1200 -- 20 min
```

**Strategic Depth:**
- Players choose exit based on proximity and time
- Campers must split attention
- Creates dynamic routing

---

## 🎮 MATCHMAKING & SERVER ARCHITECTURE

### Server Types

**Instance-Based Servers**

Each expedition = new server instance:

```
┌─────────────────────────────────────┐
│      SERVER INSTANCE TYPES          │
├─────────────────────────────────────┤
│                                     │
│  Solo Instance                      │
│  ├─ Max 1 player                    │
│  └─ Full world generated            │
│                                     │
│  Co-op PvE Instance                 │
│  ├─ Max 6-12 players                │
│  ├─ Squad-based or proximity        │
│  └─ No PvP enabled                  │
│                                     │
│  PvPvE Instance                     │
│  ├─ Max 12-20 players               │
│  ├─ Power bracket segregated        │
│  └─ Full PvP enabled                │
│                                     │
└─────────────────────────────────────┘
```

### Matchmaking Flow

**Solo:**
```lua
OnSoloDeployment:
    CreateNewServerInstance()
    Player:JoinServer()
    -- Done
```

**Co-op PvE:**
```lua
OnCoopDeployment:
    if PlayerHasSquad then
        CreateSquadServer()
        InviteSquadMembers()
    else
        if AllowProximityJoins then
            JoinPublicCoopServer() -- Others can join
        else
            CreateSoloCoopServer() -- Private instance
        end
    end
```

**PvPvE:**
```lua
OnPvPvEDeployment:
    GetPlayerBracket()
    FindMatchingBracketServer()
    
    if ServerFound then
        JoinServer()
    else
        CreateNewBracketServer()
        WaitForPlayers()
    end
```

### Server Population

**Co-op PvE:**
- Target: 6-12 players per server
- Allows organic proximity encounters
- Not overcrowded

**PvPvE:**
- Target: 12-20 players per server
- Enough for dynamic PvP
- Not a chaos fest

---

## 💎 REWARD DISTRIBUTION

### Solo Mode Rewards

**Simple:**
- Player gets 100% of their loot
- No sharing mechanics needed

---

### Co-op PvE Reward Systems

**System 1: Roll System (Default for Proximity Joins)**

```lua
-- When capture succeeds or chest spawns
OnRewardDrop:
    EligiblePlayers = GetSquadMembers()
    RollResults = {}
    
    for Player in EligiblePlayers do
        RollResults[Player] = RandomRange(1, 100)
    end
    
    Winner = GetHighestRoll(RollResults)
    AwardLoot(Winner)
    
    -- Show results to all
    BroadcastRollResults(RollResults)
```

**UI Display:**
```
┌─────────────────────────────────┐
│  🎲 LOOT ROLL                   │
├─────────────────────────────────┤
│                                 │
│  FireMage42:    [87] 🏆 Winner  │
│  StormKing11:   [64]            │
│  PetLover99:    [53]            │
│  You:           [42]            │
│                                 │
│  FireMage42 receives:           │
│  ⭐ Legendary Lava Hound         │
│                                 │
└─────────────────────────────────┘
```

**System 2: Pass/Need System**

```lua
-- Players bid on loot
OnRewardDrop:
    ShowLootToSquad(Item)
    
    -- Players choose
    Options = {
        "Need", -- Want this item
        "Greed", -- Want only if nobody needs
        "Pass", -- Don't want
    }
    
    -- Resolve
    if AnyPlayerNeeds then
        NeedPlayers = GetNeedPlayers()
        Winner = RandomChoice(NeedPlayers)
    elseif AnyPlayerGreeds then
        GreedPlayers = GetGreedPlayers()
        Winner = RandomChoice(GreedPlayers)
    else
        -- Nobody wants it, random
        Winner = RandomSquadMember()
    end
```

**System 3: Assigned/Leader System**

```lua
-- Squad leader assigns loot
OnRewardDrop:
    if Player == SquadLeader then
        ShowAssignmentUI(Item, SquadMembers)
    end
    
    Leader:ChooseRecipient() -- Manual selection
```

**Which System to Use?**

| System | Best For | Fairness | Speed |
|--------|----------|----------|-------|
| Roll | Randoms, quick groups | High | Fast |
| Pass/Need | Fair distribution by preference | Very High | Medium |
| Assigned | Pre-made squads, friends | Depends on leader | Slow |

**Recommendation:**
- Proximity joins → **Roll System** (fair, fast)
- Friend squads → **Pass/Need** OR **Assigned** (player choice)

---

### PvPvE Rewards

**Duel Winner:**
```lua
OnDuelWin:
    LooterGains = {
        -- Cargo from loser
        Cargo = Loser.Cargo * LossPercentage,
        
        -- Bonus PvP rewards
        PvPTokens = BasePvPReward * LoserCargoValue,
        Currency = BonusCurrency,
        
        -- Ranking points
        RankingPoints = +15,
    }
    
    AwardLoot(Winner, LooterGains)
```

**Duel Loser:**
```lua
OnDuelLoss:
    -- Loses cargo
    Cargo = Cargo * (1 - LossPercentage)
    
    -- Keeps base inventory
    BaseInventory = Unchanged
    
    -- Respawn at base
    Teleport(BaseSpawn)
```

---

## 🛠️ TECHNICAL IMPLEMENTATION

### Server-Side Authority

**CRITICAL RULE: Client NEVER decides outcomes**

```lua
-- ❌ WRONG (Client-side)
local function AttemptCapture()
    if math.random() < CaptureChance then
        AddPetToInventory(Pet) -- EXPLOITABLE
    end
end

-- ✅ CORRECT (Server-side)
-- Client
RemoteEvent:FireServer("AttemptCapture", PetID)

-- Server
RemoteEvent.OnServerEvent:Connect(function(Player, PetID)
    local CaptureChance = CalculateCaptureChance(Player, PetID)
    if math.random() < CaptureChance then
        AddPetToInventory(Player, PetID)
    end
end)
```

**Server Authority Checklist:**
- ✅ Capture success/failure
- ✅ Duel outcomes
- ✅ Damage calculation
- ✅ Loot drops
- ✅ Cargo management
- ✅ Extraction success

---

### Anti-Exploit Measures

**1. Sanity Checks**

```lua
-- Validate all client requests
function ValidateCaptureAttempt(Player, PetID)
    -- Pet exists?
    if not ActivePets[PetID] then return false end
    
    -- Player in range?
    if Distance(Player, Pet) > MaxCaptureRange then return false end
    
    -- Pet weakened?
    if Pet.State ~= "Weakened" then return false end
    
    -- Player has cargo space?
    if Player.CargoCount >= Player.MaxCargo then return false end
    
    return true
end
```

**2. Rate Limiting**

```lua
-- Prevent spam exploits
local Cooldowns = {}

function RateLimitAction(Player, Action, Cooldown)
    local LastAction = Cooldowns[Player.UserId][Action]
    if LastAction and tick() - LastAction < Cooldown then
        return false -- Too soon
    end
    
    Cooldowns[Player.UserId][Action] = tick()
    return true
end
```

**3. Data Validation**

```lua
-- Check data integrity on DataStore save
function ValidatePlayerData(Data)
    -- Check for impossible values
    if Data.Currency < 0 then return false end
    if Data.Level > MaxLevel + 100 then return false end
    if #Data.Pets > MaxPossiblePets then return false end
    
    return true
end
```

---

### Performance Considerations

**Proximity Join Optimization**

```lua
-- Don't check every frame
local ProximityCheckInterval = 2 -- seconds

while true do
    wait(ProximityCheckInterval)
    CheckNearbyPlayers()
end
```

**Duel System Optimization**

```lua
-- Limit active duels per server
local MaxSimultaneousDuels = 5

if ActiveDuels >= MaxSimultaneousDuels then
    -- Queue duel
    DuelQueue[#DuelQueue + 1] = {Attacker, Defender}
end
```

---

## 📊 BALANCING RECOMMENDATIONS

### PvPvE Risk/Reward Tuning

**Current Proposal:**
- PvPvE Loot Multiplier: **150%**
- Legendary Spawn Rate: **2x**
- Cargo Loss on Death: **75%**

**Testing Metrics to Watch:**
- PvPvE adoption rate (target: 20-30% of players)
- Average loot secured vs lost
- Player complaints about unfairness
- Duel duration (target: 30-90 seconds)

**Adjustment Levers:**
- Increase rewards if too few players
- Decrease loss percentage if too punishing
- Buff stakes if too much griefing
- Nerf rewards if economy inflation

---

### Co-op Scaling Balance

**Current Proposal:**
| Squad Size | HP Multiplier | Difficulty |
|-----------|---------------|------------|
| Solo | 100% | Base |
| 2 players | 150% | +50% |
| 3 players | 200% | +100% |
| 4 players | 250% | +150% |

**Test For:**
- Is 4-player squad easier than solo?
- Do players avoid squads because too hard?
- Is loot distribution satisfying?

---

## 🎯 FINAL DESIGN CHECKLIST

### Must-Haves (MVP)

- [x] Three distinct mode selection
- [x] Solo mode (private instance)
- [x] Co-op PvE mode (no PvP)
- [x] PvPvE mode (full PvP)
- [x] Pet Duel system
- [x] Power bracket matchmaking
- [x] Staked PvP
- [x] Safe zones
- [x] Extraction protection (final 5s)
- [x] Cargo loss on death
- [x] Roll-based loot system
- [x] Server authority on all outcomes

### Nice-to-Haves (Post-MVP)

- [ ] Proximity join system (hybrid)
- [ ] Pass/Need loot system
- [ ] Reputation system
- [ ] Anti-camping detection
- [ ] Multiple extraction points
- [ ] Seasonal PvPvE rankings
- [ ] Duel spectator mode
- [ ] Replay system for epic duels

---

## 📝 CONCLUSION

This multiplayer combat system is designed to:

✅ **Respect player choice** (three modes)  
✅ **Encourage cooperation** (Co-op PvE rewarding)  
✅ **Reward risk-taking** (PvPvE high stakes)  
✅ **Prevent griefing** (built-in protections)  
✅ **Create fair competition** (bracket system, pet duels)  
✅ **Scale infinitely** (works at any player count)

The key innovation is the **Pet Duel system**, which turns PvP into a skill-based, strategy-rich encounter rather than a gear-check instakill fest.

Combined with **optional high-stakes PvPvE** and **safe Co-op PvE**, players can choose their preferred experience while always having progression paths.

---

**Next Implementation Steps:**
1. Build mode selection UI
2. Implement server instance separation
3. Code Pet Duel mechanics
4. Test bracket matchmaking
5. Add safe zones and extraction protection
6. Tune reward multipliers based on playtesting

**End of Document**
