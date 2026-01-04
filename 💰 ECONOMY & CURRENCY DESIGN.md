# 💰 ECONOMY & CURRENCY DESIGN DOCUMENT
**Idol Guardians: Eternal Wilds - Complete Economic System**  
**Version:** 1.0  
**Last Updated:** January 2, 2026

---

## 📋 TABLE OF CONTENTS

### **PART 1: CURRENCY SYSTEM OVERVIEW**
1. Currency Philosophy & Design Pillars
2. Complete Currency Breakdown
3. Currency Flow Architecture
4. Economic Health Metrics

### **PART 2: GLOW CASH (PRIMARY CURRENCY)**
5. Glow Cash Overview
6. Earning Rates by Activity
7. Spending Sinks & Costs
8. Glow Cash Progression Curves

### **PART 3: HYPE CRYSTALS (PREMIUM SOFT CURRENCY)**
9. Hype Crystals Overview
10. Earning System & Drop Rates
11. Exclusive Purchases & Uses
12. Hype Crystal Economy Balance

### **PART 4: ENCORE TOKENS (PRESTIGE CURRENCY)**
13. Prestige System Design
14. Encore Token Earning
15. Prestige Shop & Rewards
16. Prestige Progression

### **PART 5: STAR SHARDS (PREMIUM CURRENCY)**
17. Star Shards Overview (Monetization)
18. Premium Currency Pricing
19. Ethical Monetization Framework
20. Revenue Projections

### **PART 6: MATERIALS SYSTEM**
21. Elemental Materials (Common → Legendary)
22. Universal Resources (Stone, Iron, Crystal)
23. Special Currencies (Essence & Cores)
24. Material Earning & Conversion

### **PART 7: EVENT CURRENCY SYSTEM**
25. Seasonal Event Currency
26. Event Shop & Rewards
27. Event Economy Balance
28. Limited-Time Systems

### **PART 8: TRADING ECONOMY**
29. Player-to-Player Trading
30. Auction House Mechanics
31. Market Fees & Regulations
32. Economic Stability Systems

### **PART 9: ECONOMIC BALANCE & SINKS**
33. Resource Faucets (Income Sources)
34. Resource Sinks (Expense Drains)
35. Inflation Control Systems
36. Long-Term Economic Health

### **PART 10: PROGRESSION & RETENTION**
37. Currency Accumulation Curves
38. Player Progression Milestones
39. Economic Retention Strategies
40. Anti-Exploit Measures

---

# PART 1: CURRENCY SYSTEM OVERVIEW

## 🎯 CURRENCY PHILOSOPHY & DESIGN PILLARS

### **Core Economic Philosophy**

> "A healthy game economy provides clear value for time invested, creates meaningful choices through scarcity, and rewards skill and strategy over pure time investment. Players should always feel progression, never exploitation."

**Design Pillars:**

**1. Multiple Currency Tiers (Complexity with Purpose)**
- Each currency serves a distinct role in progression
- No redundant or confusing currency types
- Clear visual distinction between currency types
- Intuitive earning and spending patterns

**2. Ethical Monetization (Fair Free-to-Play)**
- Premium currency NEVER provides power advantages
- All gameplay content accessible to free players
- Premium purchases save time or add cosmetics only
- Transparent pricing with clear value propositions

**3. Long-Term Sustainability (Avoid Hyperinflation)**
- Strong currency sinks prevent inflation
- Exponential cost scaling for endgame content
- Resource scarcity creates strategic choices
- Regular economic health monitoring

**4. Rewarding Skill Over Time (Skill Expression)**
- Higher skill = higher currency per hour
- Perfect combat chains = bonus multipliers
- PvPvE risks = significantly higher rewards
- Efficiency optimization rewarded

**5. Social Economy (Player Trading)**
- Player-driven market pricing
- Supply and demand dynamics
- Trading creates economic engagement
- Market fees act as currency sinks

---

## 💵 COMPLETE CURRENCY BREAKDOWN

### **The Four Primary Currencies**

| Currency | Type | Source | Primary Use | Can Trade? | Can Convert? |
|----------|------|--------|-------------|------------|--------------|
| **Glow Cash** | Soft (Primary) | Expeditions, quests, activities | Everything (buildings, pets, gear) | ✅ Via items | ❌ No |
| **Hype Crystals** | Soft (Premium) | Rare drops, events, achievements | High-tier upgrades, exclusive items | ✅ Via items | ❌ No |
| **Encore Tokens** | Prestige | Prestige resets, major achievements | Prestige shop, titles, cosmetics | ❌ No | ❌ No |
| **Star Shards** | Premium (Real $) | Purchased with real money | Cosmetics, convenience, NOT power | ❌ No | ❌ No |

### **Currency Hierarchy**

```
┌─────────────────────────────────────────────────────────┐
│                    CURRENCY PYRAMID                     │
├─────────────────────────────────────────────────────────┤
│                                                         │
│              ⭐ STAR SHARDS (Premium)                   │
│           Purchased with real money                     │
│        Used for: Cosmetics, Convenience                 │
│              (No power advantages)                      │
│                                                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│           🎖️ ENCORE TOKENS (Prestige)                  │
│         Earned through prestige resets                  │
│     Used for: Titles, Frames, Status Items              │
│           (Long-term achievement currency)              │
│                                                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│            💎 HYPE CRYSTALS (Rare Soft)                │
│       Earned from rare drops and events                 │
│    Used for: Legendary upgrades, Exclusive items        │
│         (Bridge between common and prestige)            │
│                                                         │
├─────────────────────────────────────────────────────────┤
│                                                         │
│           💰 GLOW CASH (Primary Soft)                  │
│         Earned from all activities                      │
│   Used for: 90% of all progression purchases            │
│     (The backbone of the economy)                       │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 🔄 CURRENCY FLOW ARCHITECTURE

### **Currency Flow Diagram**

```
PLAYER ACTIVITIES
       ↓
┌──────────────────────────────────────────────────────┐
│  EARNING SOURCES (Faucets)                          │
│  ├─ Expeditions (primary)                            │
│  ├─ Daily Quests (routine)                           │
│  ├─ Weekly Quests (significant)                      │
│  ├─ Achievements (one-time)                          │
│  ├─ Market Sales (player-driven)                     │
│  ├─ Passive Income (buildings)                       │
│  └─ Events (seasonal)                                │
└──────────────────────────────────────────────────────┘
       ↓
┌──────────────────────────────────────────────────────┐
│  PLAYER CURRENCY POOL                                │
│  ├─ Glow Cash: 45,000                                │
│  ├─ Hype Crystals: 120                               │
│  ├─ Encore Tokens: 15                                │
│  └─ Star Shards: 500 (premium)                       │
└──────────────────────────────────────────────────────┘
       ↓
┌──────────────────────────────────────────────────────┐
│  SPENDING DECISIONS (Strategic Choices)              │
│  ├─ Upgrade buildings? (Glow Cash)                   │
│  ├─ Buy legendary gear? (Hype Crystals)              │
│  ├─ Unlock prestige frame? (Encore Tokens)           │
│  └─ Purchase cosmetics? (Star Shards)                │
└──────────────────────────────────────────────────────┘
       ↓
┌──────────────────────────────────────────────────────┐
│  CURRENCY SINKS (Permanent Removal)                  │
│  ├─ Building upgrades (40% of Glow Cash)             │
│  ├─ Pet training/breeding (25% of Glow Cash)         │
│  ├─ Crafting costs (20% of Glow Cash)                │
│  ├─ Market fees (5-10% of trade value)               │
│  ├─ Fast travel costs (3% of Glow Cash)              │
│  └─ Consumable purchases (10% of Glow Cash)          │
└──────────────────────────────────────────────────────┘
       ↓
  PROGRESSION
```

---

## 📊 ECONOMIC HEALTH METRICS

### **Key Performance Indicators (KPIs)**

**Currency Velocity:**
- **Target:** Players spend 70-80% of earned Glow Cash within 7 days
- **Why:** High velocity = engaged economy, players always progressing
- **Danger:** >90% spent = too little saving, <50% spent = hoarding/stagnation

**Currency Sink Effectiveness:**
- **Target:** 60% of Glow Cash permanently removed via sinks (not trading)
- **Why:** Prevents inflation, maintains currency value
- **Danger:** <40% removal = inflation, >80% = too expensive

**Average Player Wealth:**
- **Week 1 Player:** 50,000-100,000 Glow Cash net worth
- **Month 1 Player:** 500,000-1,000,000 Glow Cash net worth
- **Month 6+ Player:** 10,000,000-50,000,000 Glow Cash net worth
- **Why:** Exponential wealth growth is expected and healthy

**Premium Conversion Rate:**
- **Target:** 15-25% of players make at least one Star Shard purchase
- **Why:** Sustainable revenue without exploiting players
- **Benchmark:** Industry standard for ethical F2P is 10-30%

**Trading Volume:**
- **Target:** 20-30% of active players use market weekly
- **Why:** Active trading = engaged economy
- **Low volume (<10%):** Market not useful, items too common
- **High volume (>50%):** Possibly market manipulation

---

# PART 2: GLOW CASH (PRIMARY CURRENCY)

## 💰 GLOW CASH OVERVIEW

### **What is Glow Cash?**

Glow Cash is the **primary soft currency** that powers 90% of all progression in Idol Guardians. It's earned through virtually every activity and spent on buildings, pet training, crafting, breeding, and more.

**Visual Identity:**
- Icon: ✨ Glowing gold coin with ethereal trail
- Color: Bright gold (#FFD700) with luminescent glow effect
- Sound: Gentle chime when earned (satisfying audio feedback)
- Animation: Floats upward when collected, sparkles on screen

**Key Properties:**
- **Abundant:** Earned constantly through normal play
- **Essential:** Required for all core progression systems
- **Stable:** Value maintained through strong sinks
- **Tradeable:** Indirectly via selling items for Glow Cash

---

## 📈 EARNING RATES BY ACTIVITY

### **Expedition Rewards (60% of Total Income)**

**Base Expedition Rewards Formula:**

```
Base Glow Cash = 10 × Enemy Level × Rarity Multiplier × Depth Multiplier × Performance Bonus

Rarity Multipliers:
├─ Common: 1.0x
├─ Uncommon: 3.0x
├─ Rare: 10.0x
├─ Epic: 30.0x
├─ Legendary: 100.0x
├─ Mythic: 250.0x
└─ Unique: 1,000.0x

Depth Multipliers (Distance from Base):
├─ 0-500m: 1.0x
├─ 501-1,000m: 1.2x
├─ 1,001-1,500m: 1.5x
├─ 1,501-2,000m: 2.0x
├─ 2,001-2,500m: 2.5x
└─ 2,501m+: 3.0x (maximum)

Performance Bonus:
├─ All Perfect Combat: +50%
├─ No Damage Taken: +25%
├─ Fast Clear (under par time): +15%
└─ All Combined: +100% (doubles rewards)
```

**Example Calculations:**

```
Early Game (Level 5 Common Pet, 200m from base):
10 × 5 × 1.0 × 1.0 × 1.0 = 50 Glow Cash per kill

Mid Game (Level 30 Rare Pet, 1,200m from base, perfect combat):
10 × 30 × 10.0 × 1.5 × 1.5 = 6,750 Glow Cash per kill

Late Game (Level 60 Legendary Pet, 2,600m from base, all bonuses):
10 × 60 × 100.0 × 3.0 × 2.0 = 360,000 Glow Cash per kill
```

**Typical Expedition Income:**

| Player Level | Expedition Duration | Average Kills | Glow Cash/Hour |
|--------------|-------------------|---------------|----------------|
| 1-15 (Early) | 20 minutes | 15-20 Common | 2,000-4,000 |
| 16-30 (Mid) | 30 minutes | 20-30 Uncommon/Rare | 8,000-15,000 |
| 31-50 (Advanced) | 45 minutes | 25-40 Rare/Epic | 25,000-50,000 |
| 51-70 (Endgame) | 60 minutes | 30-50 Epic/Legendary | 75,000-150,000 |
| 71+ (Master) | 60+ minutes | 40+ Legendary/Mythic | 200,000-500,000 |

**Chest Rewards:**

| Chest Rarity | Glow Cash Range | Spawn Rate (per expedition) |
|--------------|----------------|---------------------------|
| Common | 100-500 | 10-15 chests |
| Uncommon | 500-1,500 | 5-8 chests |
| Rare | 2,000-5,000 | 2-4 chests |
| Epic | 10,000-25,000 | 0-2 chests |
| Legendary | 50,000-100,000 | 0-1 chest (5% chance) |

---

### **Daily Quests (15% of Total Income)**

**Daily Quest Structure:**

```
Every day at reset (12:00 AM UTC), players receive 5 daily quests:

Quest Types:
├─ Completion Quests: "Complete 3 expeditions"
├─ Defeat Quests: "Defeat 20 pets"
├─ Capture Quests: "Capture 5 pets"
├─ Training Quests: "Train a pet to Level 10"
└─ Social Quests: "Complete 1 Co-op expedition"
```

**Daily Quest Rewards:**

| Quest Difficulty | Glow Cash Reward | Time Investment |
|-----------------|------------------|-----------------|
| Easy (Quest 1-2) | 1,000-2,000 | 10-15 minutes |
| Medium (Quest 3-4) | 2,500-4,000 | 20-30 minutes |
| Hard (Quest 5) | 5,000-7,500 | 30-45 minutes |
| **Daily Total** | **15,000-25,000** | **1.5-2 hours** |

**Daily Quest Streak Bonus:**

```
Consecutive Days Completed:
├─ Day 1-3: Base rewards
├─ Day 4-6: +10% bonus
├─ Day 7: +50% bonus + 5 Hype Crystals
├─ Day 8-13: +15% bonus
├─ Day 14: +100% bonus + 10 Hype Crystals + Rare Pet Egg
└─ Day 15+: +20% bonus (maintained until streak broken)

Breaking Streak: Resets to Day 1 (but no penalty beyond losing bonus)
```

---

### **Weekly Quests (10% of Total Income)**

**Weekly Quest Structure:**

```
Every Monday at reset, players receive 3 weekly quests:

Quest Types:
├─ Progression Quests: "Reach Depth 2,000m"
├─ Collection Quests: "Capture 30 unique species"
├─ Building Quests: "Upgrade 5 buildings"
├─ Combat Quests: "Defeat 10 Legendary+ pets"
└─ Social Quests: "Complete 5 Co-op expeditions"
```

**Weekly Quest Rewards:**

| Quest Number | Glow Cash Reward | Additional Rewards | Time Investment |
|--------------|------------------|--------------------|-----------------|
| Quest 1 | 10,000-15,000 | 50 Materials | 3-4 hours |
| Quest 2 | 15,000-25,000 | 100 Materials + 5 Hype Crystals | 5-6 hours |
| Quest 3 | 30,000-50,000 | 200 Materials + 10 Hype Crystals + Rare Pet Egg | 8-10 hours |
| **Weekly Total** | **55,000-90,000** | **350 Materials + 15 Hype Crystals** | **16-20 hours** |

---

### **Achievement Rewards (One-Time Bonuses)**

**Achievement Categories & Rewards:**

| Category | Achievements | Glow Cash per Achievement | Total Possible |
|----------|--------------|--------------------------|----------------|
| Combat Mastery | 20 achievements | 5,000-50,000 | 500,000 |
| Collection | 25 achievements | 10,000-100,000 | 1,250,000 |
| Exploration | 15 achievements | 15,000-75,000 | 750,000 |
| Building | 20 achievements | 10,000-200,000 | 2,000,000 |
| Social | 10 achievements | 5,000-25,000 | 150,000 |
| **Total** | **90 achievements** | **Variable** | **~4,650,000** |

**Example Achievements:**

```
Combat Achievements:
├─ "First Blood": Defeat your first pet (500 Glow Cash)
├─ "Perfect Warrior": Chain 50 Perfect hits (5,000 Glow Cash)
├─ "Legendary Hunter": Defeat 100 Legendary pets (50,000 Glow Cash)
└─ "Mythic Slayer": Defeat your first Mythic pet (100,000 Glow Cash)

Collection Achievements:
├─ "Novice Collector": Capture 10 unique species (1,000 Glow Cash)
├─ "Rare Collector": Capture 50 unique species (10,000 Glow Cash)
├─ "Master Collector": Capture 150 unique species (75,000 Glow Cash)
└─ "Completionist": Capture all 200+ species (250,000 Glow Cash + Mythic Egg)
```

---

### **Market Sales (10% of Total Income)**

**Player-Driven Economy:**

Players can sell items, materials, and pets to other players via the Market/Auction House system.

**Common Market Transactions:**

| Item Type | Average Sale Price | Market Fee (10%) | Net Glow Cash |
|-----------|-------------------|------------------|---------------|
| Common Materials | 50-200 | 5-20 | 45-180 |
| Rare Materials | 500-2,000 | 50-200 | 450-1,800 |
| Epic Materials | 5,000-15,000 | 500-1,500 | 4,500-13,500 |
| Legendary Materials | 50,000-200,000 | 5,000-20,000 | 45,000-180,000 |
| Rare Pets (2-3 star) | 10,000-50,000 | 1,000-5,000 | 9,000-45,000 |
| Epic Pets (4-5 star) | 100,000-500,000 | 10,000-50,000 | 90,000-450,000 |
| Legendary Gear | 200,000-1,000,000 | 20,000-100,000 | 180,000-900,000 |

**Average Player Market Income:**
- **Casual Players:** 5,000-15,000 Glow Cash/week
- **Active Traders:** 50,000-150,000 Glow Cash/week
- **Market Specialists:** 200,000-500,000+ Glow Cash/week

---

### **Passive Income (5% of Total Income)**

**Energy Generator Building:**

Players can assign pets to the Energy Generator to earn passive Glow Cash while offline.

**Passive Income Formula:**

```
Passive Glow Cash/Hour = Pet Rarity Value × Generator Level Multiplier × Worker Slots

Pet Rarity Values:
├─ Common: 10/hour
├─ Uncommon: 30/hour
├─ Rare: 100/hour
├─ Epic: 300/hour
├─ Legendary: 1,000/hour
├─ Mythic: 3,000/hour
└─ Unique: 10,000/hour

Generator Level Multipliers:
├─ Level 1: 1.0x (1 slot)
├─ Level 3: 1.25x (2 slots)
├─ Level 5: 1.5x (3 slots)
├─ Level 7: 1.75x (5 slots)
└─ Level 10: 2.5x (10 slots, max)
```

**Example Passive Income Setups:**

```
Early Game (Level 3 Generator, 2 Rare pets):
2 × 100 × 1.25 = 250 Glow Cash/hour
= 6,000 Glow Cash/day (24 hours)

Mid Game (Level 7 Generator, 5 Epic pets):
5 × 300 × 1.75 = 2,625 Glow Cash/hour
= 63,000 Glow Cash/day

Late Game (Level 10 Generator, 10 Legendary pets):
10 × 1,000 × 2.5 = 25,000 Glow Cash/hour
= 600,000 Glow Cash/day

Endgame (Level 10 Generator, 10 Mythic pets):
10 × 3,000 × 2.5 = 75,000 Glow Cash/hour
= 1,800,000 Glow Cash/day
```

**Passive Income Caps:**
- **Free Players:** 24-hour collection cap
- **Premium Players:** 48-hour collection cap (via Generator Mode subscription)
- **Why:** Prevents infinite accumulation, encourages daily logins

---

### **Event Rewards (Seasonal - Variable)**

**Seasonal Event Structure:**

```
Events occur every 6-8 weeks, lasting 2-3 weeks each.

Event Types:
├─ Summer Festival (June-July)
├─ Halloween Spooktacular (October)
├─ Winter Wonderland (December)
├─ Spring Bloom (March-April)
└─ Special Collaborations (varies)
```

**Event Glow Cash Rewards:**

| Event Activity | Glow Cash Reward | Frequency |
|----------------|------------------|-----------|
| Daily Event Quest | 5,000-10,000 | Daily (14-21 days) |
| Weekly Event Challenge | 25,000-50,000 | Weekly (2-3 times) |
| Event Leaderboard (Top 100) | 100,000-500,000 | Once per event |
| Event Shop Purchases | Variable | Throughout event |

**Total Event Glow Cash (Average Player):**
- **Per Event:** 150,000-300,000 Glow Cash
- **Per Year (6-8 events):** 900,000-2,400,000 Glow Cash

---

## 💸 SPENDING SINKS & COSTS

### **Building Upgrades (40% of Total Spending)**

**Building Upgrade Cost Formula:**

```
Upgrade Cost = Base Cost × (1.5^Level) × Building Tier Multiplier

Building Tier Multipliers:
├─ Phase 1 Buildings (MVP): 1.0x
├─ Phase 2 Buildings (Advanced): 1.5x
├─ Phase 3 Buildings (Endgame): 2.0x
└─ Phase 4 Buildings (Utility): 1.25x
```

**Example Building Upgrade Costs:**

| Building | Level | Glow Cash Cost | Materials Cost | Construction Time |
|----------|-------|----------------|----------------|-------------------|
| Weaponsmith | 1→2 | 5,000 | 50 Stone | 5 minutes |
| Weaponsmith | 2→3 | 7,500 | 75 Stone | 15 minutes |
| Weaponsmith | 5→6 | 28,000 | 100 Iron | 2 hours |
| Weaponsmith | 9→10 | 180,000 | 500 Crystal + 200 Legendary Core | 24 hours |
| Laboratory (Tier 2) | 5→6 | 42,000 | 150 Iron | 3 hours |
| Laboratory | 9→10 | 270,000 | 750 Crystal + 300 Legendary Core | 36 hours |
| Guild Hall (Tier 3) | 5→6 | 56,000 | 200 Iron | 4 hours |
| Guild Hall | 9→10 | 360,000 | 1,000 Crystal + 400 Legendary Core | 48 hours |

**Total Building Upgrade Costs (All 20 Buildings to Level 10):**
- **Glow Cash:** ~9,435,000
- **Materials:** ~500,000 total (Stone, Iron, Crystal)
- **Special Currencies:** ~12,000 Legendary Core
- **Time Investment:** ~300 hours construction time (can be accelerated)

---

### **Pet Training & Breeding (25% of Total Spending)**

**Training Costs:**

```
Training Cost Per Level = Base Cost + (Level × 100)

Base Cost by Rarity:
├─ Common: 1,000 Glow Cash
├─ Uncommon: 2,000 Glow Cash
├─ Rare: 5,000 Glow Cash
├─ Epic: 10,000 Glow Cash
├─ Legendary: 25,000 Glow Cash
├─ Mythic: 50,000 Glow Cash
└─ Unique: 100,000 Glow Cash
```

**Example Training Costs:**

```
Common Pet (Level 1→50):
Total = 50,000 + (1+2+3+...+50) × 100
     = 50,000 + 127,500
     = 177,500 Glow Cash

Legendary Pet (Level 1→100):
Total = 2,500,000 + (1+2+3+...+100) × 100
     = 2,500,000 + 505,000
     = 3,005,000 Glow Cash
```

**Breeding Costs:**

```
Breeding Cost = (Parent 1 Rarity Value + Parent 2 Rarity Value) × 5,000

Rarity Values:
├─ Common: 1
├─ Uncommon: 3
├─ Rare: 5
├─ Epic: 7
└─ Legendary: 10

Examples:
├─ Common + Common: (1+1) × 5,000 = 10,000 Glow Cash
├─ Rare + Rare: (5+5) × 5,000 = 50,000 Glow Cash
└─ Legendary + Legendary: (10+10) × 5,000 = 100,000 Glow Cash
```

**Life Stage Advancement Costs:**

```
Baby → Young: 1,000 Glow Cash
Young → Adult: 10,000 Glow Cash
Adult → Mature: 25,000 Glow Cash
Mature → Elder: 50,000 Glow Cash
Elder → Timeless: 100,000 Glow Cash

Total (Baby → Timeless): 186,000 Glow Cash per pet
```

---

### **Crafting Costs (20% of Total Spending)**

**Weapon & Armor Crafting:**

| Item Tier | Glow Cash Cost | Material Requirements | Crafting Time |
|-----------|----------------|----------------------|---------------|
| Common | 500 | 10 Common Materials | Instant |
| Uncommon | 2,000 | 25 Common + 5 Uncommon | 5 minutes |
| Rare | 10,000 | 50 Uncommon + 10 Rare | 30 minutes |
| Epic | 50,000 | 100 Rare + 25 Epic | 2 hours |
| Legendary | 250,000 | 250 Epic + 50 Legendary | 8 hours |
| Mythic | 1,000,000 | 500 Legendary + 100 Mythic | 24 hours |

**Consumable Crafting:**

| Consumable | Glow Cash Cost | Materials | Effect |
|------------|----------------|-----------|--------|
| Health Potion | 100 | 5 Common | Restore 25% HP |
| Stamina Potion | 150 | 8 Common | Restore 50% Stamina |
| Capture Boost | 500 | 15 Uncommon | +10% Capture Rate (1 hour) |
| Experience Boost | 1,000 | 25 Rare | +25% XP (1 hour) |
| Loot Boost | 2,500 | 50 Epic | +50% Loot Quality (1 hour) |

**Average Crafting Spending:**
- **Early Game:** 5,000-10,000 Glow Cash/week
- **Mid Game:** 25,000-50,000 Glow Cash/week
- **Late Game:** 100,000-250,000 Glow Cash/week

---

### **Star Merging Costs (5% of Total Spending)**

**Pet Star Merging:**

| Current Stars | Target Stars | Glow Cash Cost | Sacrifice Pets Required | Material Cost |
|---------------|--------------|----------------|------------------------|---------------|
| ★☆☆☆☆ | ★★☆☆☆ | 5,000 | 1 duplicate | 20 Rare Essence |
| ★★☆☆☆ | ★★★☆☆ | 10,000 | 2 duplicates | 50 Rare Essence |
| ★★★☆☆ | ★★★★☆ | 25,000 | 3 duplicates | 100 Epic Essence |
| ★★★★☆ | ★★★★★ | 50,000 | 4 duplicates | 200 Legendary Core |

**Total Cost (★☆☆☆☆ → ★★★★★):** 90,000 Glow Cash + 10 pets + materials

---

### **Market Fees (5-10% of Trade Value)**

**Trading Fees:**

```
Market Transaction Fee: 10% of sale price

Examples:
├─ Sell item for 10,000 Glow Cash → Pay 1,000 fee → Net 9,000
├─ Sell item for 100,000 Glow Cash → Pay 10,000 fee → Net 90,000
└─ Sell item for 1,000,000 Glow Cash → Pay 100,000 fee → Net 900,000

Why 10% Fee:
├─ Currency sink (removes Glow Cash from economy)
├─ Prevents market manipulation (cost to flip items)
├─ Encourages direct trades (lower fees)
└─ Funds NPC vendor stock (lore justification)
```

**Auction House Fees:**

```
Listing Fee: 1% of listing price (paid upfront, non-refundable)
Sale Fee: 5% of final sale price (deducted from payout)

Total Fee: 6% if item sells, 1% if doesn't sell

Example:
├─ List item for 100,000 Glow Cash
├─ Pay 1,000 listing fee
├─ Item sells for 100,000
├─ Additional 5,000 sale fee deducted
└─ Net received: 94,000 Glow Cash (6% total fees)
```

---

### **Fast Travel Costs (3% of Total Spending)**

**Fast Travel System:**

```
Fast Travel Cost = Base Cost + (Distance/100) × 10

Base Cost: 50 Glow Cash (minimum)
Distance: Measured in studs

Examples:
├─ Base → Social Hub (500 studs): 50 + (500/100) × 10 = 100 Glow Cash
├─ Base → Distant Biome (2,000 studs): 50 + (2,000/100) × 10 = 250 Glow Cash
└─ Base → Extraction Zone (5,000 studs): 50 + (5,000/100) × 10 = 550 Glow Cash

Premium Fast Travel Pass:
├─ Cost: 300 Star Shards/month (premium currency)
├─ Effect: Unlimited free fast travel for 30 days
└─ Value: Saves 10,000-30,000 Glow Cash/month for active players
```

---

### **Miscellaneous Sinks (2% of Total Spending)**

**Other Currency Sinks:**

| Sink Type | Glow Cash Cost | Purpose |
|-----------|----------------|---------|
| Pet Renaming | 1,000 (first), 5,000 (subsequent) | Cosmetic personalization |
| Resource Conversion | 1,000 per conversion | Convert materials |
| Pet Respec (IV Reroll) | 50,000 per reroll | Change pet stats |
| Building Relocation | 5,000-25,000 | Move building plots |
| Storage Expansion | 10,000-100,000 | Increase storage capacity |

---

## 📊 GLOW CASH PROGRESSION CURVES

### **Expected Glow Cash Accumulation**

**Player Net Worth by Time Played:**

| Time Period | Active Play Hours | Expected Net Worth | Daily Active Income | Daily Spending |
|-------------|------------------|-------------------|---------------------|----------------|
| Week 1 | 10-15 hours | 50,000-100,000 | 8,000-15,000 | 5,000-10,000 |
| Month 1 | 40-60 hours | 500,000-1,000,000 | 20,000-35,000 | 15,000-25,000 |
| Month 3 | 120-180 hours | 2,000,000-5,000,000 | 50,000-80,000 | 40,000-70,000 |
| Month 6 | 240-360 hours | 10,000,000-25,000,000 | 100,000-200,000 | 80,000-150,000 |
| Month 12+ | 500+ hours | 50,000,000-200,000,000+ | 200,000-500,000+ | 150,000-400,000 |

**Progression Curve Graph:**

```
NET WORTH OVER TIME (Logarithmic Scale)

100M ┤                                      ****
     │                                  ****
     │                              ****
 10M ┤                          ****
     │                      ****
     │                  ****
  1M ┤              ****
     │          ****
     │      ****
100K ┤  ****
     └─────────────────────────────────────────
     Week1  Month1  Month3  Month6   Month12

Key Observations:
├─ Exponential growth is intentional (feels rewarding)
├─ Early game is tight (strategic choices matter)
├─ Late game is abundant (can afford experimentation)
└─ Never plateaus (always growing)
```

**Wealth Distribution (Expected):**

```
After 6 Months of Active Play:

Top 1% (Whales/No-Lifers):   100M+ Glow Cash
Top 10% (Hardcore):            25M-100M Glow Cash
Middle 40% (Regular):          5M-25M Glow Cash
Bottom 40% (Casual):           1M-5M Glow Cash
Bottom 10% (New/Inactive):     <1M Glow Cash

Why This is Healthy:
├─ Wealth gap is expected (time investment rewarded)
├─ Bottom players still progressing (not stuck)
├─ Top players need sinks (endgame purchases)
└─ Middle players are majority (balanced economy)
```

---

# PART 3: HYPE CRYSTALS (PREMIUM SOFT CURRENCY)

## 💎 HYPE CRYSTALS OVERVIEW

### **What are Hype Crystals?**

Hype Crystals are a **rare premium soft currency** that bridges the gap between common Glow Cash and prestige Encore Tokens. They're earned through challenging content, rare drops, and significant achievements—rewarding dedicated players with access to exclusive high-tier items.

**Visual Identity:**
- Icon: 💎 Crystalline gem with prismatic rainbow shimmer
- Color: Iridescent cyan-purple gradient (#00FFFF → #9370DB)
- Sound: Crystal chime (higher pitch than Glow Cash, more "special")
- Animation: Sparkles and refracts light, rotates slowly

**Design Philosophy:**
- **Rare but attainable:** Feel special without being impossible to earn
- **Reward dedication:** Given for hard content, not just time
- **Bridge currency:** More valuable than Glow Cash, less exclusive than Encore Tokens
- **Cannot purchase:** Never sold for real money (preserves value)

---

## 🎯 EARNING SYSTEM & DROP RATES

### **Primary Earning Methods**

**1. Legendary+ Enemy Defeats (30% of Hype Crystals)**

```
Drop Rates by Enemy Rarity:

Legendary Pet Defeat:
├─ Drop Chance: 10%
├─ Amount: 1-3 Hype Crystals
└─ Expected: 0.2 Hype Crystals per kill (10% × 2 average)

Mythic Pet Defeat:
├─ Drop Chance: 30%
├─ Amount: 3-8 Hype Crystals
└─ Expected: 1.65 Hype Crystals per kill

Unique/Boss Pet Defeat:
├─ Drop Chance: 100% (guaranteed)
├─ Amount: 10-20 Hype Crystals
└─ Expected: 15 Hype Crystals per kill
```

**Expected Legendary+ Defeats:**

| Player Level | Legendary Kills/Week | Mythic Kills/Week | Unique Kills/Week | Total Hype Crystals/Week |
|--------------|---------------------|------------------|------------------|-------------------------|
| 51-60 | 10-15 | 0-2 | 0 | 2-6 |
| 61-70 | 20-30 | 3-6 | 0-1 | 8-15 |
| 71-80 | 40-60 | 8-12 | 1-2 | 25-40 |
| 81+ | 60-100 | 15-25 | 2-4 | 50-80 |

---

**2. Dungeon Completion Rewards (25% of Hype Crystals)**

```
Dungeon Hype Crystal Rewards:

Common Dungeon:
└─ 0-1 Hype Crystals (20% chance)

Rare Dungeon:
└─ 1-3 Hype Crystals (50% chance)

Epic Dungeon:
└─ 3-5 Hype Crystals (100% guaranteed)

Legendary Dungeon:
└─ 8-12 Hype Crystals (100% guaranteed)

Weekly Boss Dungeon:
└─ 20-30 Hype Crystals (100% guaranteed)

Hard Mode Bonus:
└─ +50% Hype Crystals if completed on Hard Mode
```

**Expected Dungeon Runs:**

| Player Type | Dungeons/Week | Average Hype Crystals/Week |
|-------------|--------------|---------------------------|
| Casual | 2-4 (mostly Common/Rare) | 2-5 |
| Regular | 5-10 (mix of all types) | 10-20 |
| Hardcore | 15-25 (farming Legendary) | 40-60 |

---

**3. Daily/Weekly Quest Rewards (20% of Hype Crystals)**

```
Daily Quest Hype Crystal Rewards:

Daily Streak Bonuses:
├─ Day 7: 5 Hype Crystals
├─ Day 14: 10 Hype Crystals
└─ Day 30: 25 Hype Crystals + Rare Pet Egg

Weekly Quest Rewards:
├─ Quest 2: 5 Hype Crystals
├─ Quest 3: 10 Hype Crystals
└─ Weekly Total: 15 Hype Crystals
```

**Expected from Quests:**

- **Daily Players:** 5-10 Hype Crystals/week (from streaks)
- **Weekly Completionists:** 15-25 Hype Crystals/week (all quests)

---

**4. Achievement Rewards (15% of Hype Crystals)**

```
Achievement Hype Crystal Rewards:

Tier 1 Achievements (Bronze):
└─ 1-5 Hype Crystals each

Tier 2 Achievements (Silver):
└─ 5-15 Hype Crystals each

Tier 3 Achievements (Gold):
└─ 15-50 Hype Crystals each

Tier 4 Achievements (Platinum):
└─ 50-200 Hype Crystals each

Example Achievements:
├─ "Legendary Hunter": Defeat 100 Legendary pets (25 Hype Crystals)
├─ "Dungeon Master": Complete 50 dungeons (50 Hype Crystals)
├─ "Perfect Collector": Capture all 200+ species (200 Hype Crystals)
└─ "Endgame Conqueror": Reach Level 100 (100 Hype Crystals)

Total Available from Achievements: ~3,500 Hype Crystals (one-time)
```

---

**5. Event Participation (10% of Hype Crystals)**

```
Seasonal Event Hype Crystal Rewards:

Event Daily Quest: 1-3 Hype Crystals/day
Event Weekly Challenge: 10-20 Hype Crystals
Event Leaderboard:
├─ Top 10: 200-500 Hype Crystals
├─ Top 100: 50-200 Hype Crystals
└─ Top 1,000: 10-50 Hype Crystals

Average Event Participation: 30-80 Hype Crystals per 2-3 week event
```

---

### **Total Hype Crystal Income (Weekly Estimates)**

| Player Type | Active Hours/Week | Hype Crystals/Week |
|-------------|------------------|-------------------|
| Casual | 5-10 hours | 10-20 |
| Regular | 15-25 hours | 30-60 |
| Hardcore | 30-50 hours | 80-150 |
| Elite | 50+ hours | 150-250+ |

**Monthly Accumulation:**
- Casual: 40-80 Hype Crystals/month
- Regular: 120-240 Hype Crystals/month
- Hardcore: 320-600 Hype Crystals/month
- Elite: 600-1,000+ Hype Crystals/month

---

## 🛒 EXCLUSIVE PURCHASES & USES

### **Hype Crystal Shop (Permanent)**

**High-Tier Equipment:**

| Item | Hype Crystal Cost | Equivalent Glow Cash Value | Benefits |
|------|------------------|---------------------------|----------|
| Legendary Weapon Blueprint | 100 Hype Crystals | 500,000 Glow Cash | Craft Legendary weapons |
| Mythic Armor Blueprint | 250 Hype Crystals | 2,000,000 Glow Cash | Craft Mythic armor |
| Exclusive Pet Egg (Legendary) | 150 Hype Crystals | Cannot buy with Glow Cash | Guaranteed 3-4 star Legendary |
| IV Reroll Token | 50 Hype Crystals | 100,000 Glow Cash | Reroll pet IVs |
| Building Upgrade Accelerator (24h) | 75 Hype Crystals | 200,000 Glow Cash | Instant complete 24h upgrade |

**Convenience Items:**

| Item | Hype Crystal Cost | Effect |
|------|------------------|--------|
| Warehouse Expansion +500 Slots | 200 Hype Crystals | Permanent storage increase |
| Training Queue +1 Slot | 150 Hype Crystals | Train one more pet simultaneously |
| Breeding Hall +1 Slot | 200 Hype Crystals | Breed one more pair simultaneously |
| Fast Travel Waypoint Unlock | 100 Hype Crystals | Unlock permanent fast travel point |

**Exclusive Cosmetics:**

| Item | Hype Crystal Cost | Rarity |
|------|------------------|--------|
| Hype Crystal Weapon Skin | 300 Hype Crystals | Exclusive (cannot get elsewhere) |
| Legendary Pet Skin | 400 Hype Crystals | Animated, particle effects |
| Mythic Emote | 250 Hype Crystals | Special animations |
| Building Skin (Hype Crystal Theme) | 500 Hype Crystals | Glowing crystalline aesthetic |

---

### **Limited Rotation Shop (Weekly)**

```
Every Monday, 3-5 exclusive items rotate in:

Week 1 Example:
├─ Rare Pet Egg (Fire Element): 80 Hype Crystals
├─ Epic Material Bundle: 50 Hype Crystals
└─ Exclusive Emote: 150 Hype Crystals

Why Rotation:
├─ Creates urgency (FOMO)
├─ Prevents hoarding (spend or miss out)
├─ Keeps economy flowing
└─ Adds variety to Hype Crystal shop
```

---

## ⚖️ HYPE CRYSTAL ECONOMY BALANCE

### **Earning vs Spending Balance**

**Target Accumulation:**

```
Goal: Players should earn 50-150 Hype Crystals/month (casual to regular)

With this earning rate:
├─ Major purchase (500+ Hype Crystals): 3-10 months saving
├─ Medium purchase (100-200 Hype Crystals): 2-4 months saving
├─ Small purchase (50-100 Hype Crystals): 1-2 months saving
└─ Weekly rotation items: Can buy 1-2 items/month

Why This Balance:
├─ Prevents instant gratification (value maintained)
├─ Rewards long-term planning (saving matters)
├─ Enables small impulse buys (weekly rotation)
└─ Respects time investment (feels worth it)
```

**Hype Crystal Sinks (Where They Go):**

| Sink Category | % of Spending | Purpose |
|--------------|---------------|---------|
| Exclusive Cosmetics | 40% | Personalization, status symbols |
| High-Tier Equipment | 30% | Power progression (alternatives exist) |
| Convenience Items | 20% | Quality of life (optional) |
| Limited Rotation | 10% | Impulse purchases, variety |

---

### **Preventing Hype Crystal Inflation**

**Design Safeguards:**

1. **Earning Caps:**
   - Legendary+ enemies have diminishing returns (10 kills/hour max yield)
   - Dungeons have weekly lockouts (prevents infinite farming)
   - Daily/weekly quests are capped by nature

2. **High-Value Sinks:**
   - Most valuable items cost 200-500+ Hype Crystals
   - Encourages long-term saving, not instant spending
   - New exclusive items added regularly

3. **No Trading:**
   - Hype Crystals cannot be traded between players
   - Prevents market manipulation
   - Maintains rarity and prestige

4. **No Premium Conversion:**
   - Cannot buy Hype Crystals with Star Shards (premium currency)
   - Must be earned through gameplay only
   - Preserves sense of accomplishment

---

# PART 4: ENCORE TOKENS (PRESTIGE CURRENCY)

## 🎖️ PRESTIGE SYSTEM DESIGN

### **What is the Prestige System?**

The Prestige System is a **long-term achievement and status framework** that rewards players for reaching major milestones. By completing prestigious achievements and hitting level caps, players earn **Encore Tokens**—an exclusive currency used to purchase cosmetic titles, profile frames, and status symbols that showcase their dedication.

**Design Philosophy:**
- **Pure prestige:** No power advantages, only cosmetic/social rewards
- **Long-term goals:** Takes months to accumulate significant tokens
- **Achievement-driven:** Rewards skill and completion, not just time
- **Social status:** Visible to other players (titles, frames, badges)

**Visual Identity:**
- Icon: 🎖️ Medallion with laurel wreath, gold and royal purple
- Color: Gold (#FFD700) with royal purple accents (#9370DB)
- Sound: Fanfare/trumpet (rare, special sound)
- Animation: Radiates prestige aura, sparkles with authority

---

## 🏆 ENCORE TOKEN EARNING

### **Primary Earning Method: Prestige Milestones**

**Level-Based Prestige Resets:**

```
Prestige becomes available every 20 levels starting at Level 100:

Prestige 1 (Level 100):
├─ Reward: 10 Encore Tokens + Title "The Ascending"
├─ Reset: Return to Level 1, keep all pets/buildings/items
└─ Bonus: +1% permanent XP gain (stacks with future prestiges)

Prestige 2 (Level 100 again):
├─ Reward: 15 Encore Tokens + Title "Twice Ascended"
├─ Bonus: +2% permanent XP gain (total: +3%)
└─ Profile Frame: Bronze Prestige Frame

Prestige 3 (Level 100 third time):
├─ Reward: 20 Encore Tokens + Title "Thrice Ascended"
├─ Bonus: +3% permanent XP gain (total: +6%)
└─ Profile Frame: Silver Prestige Frame

Prestige 5:
├─ Reward: 30 Encore Tokens + Title "Master of Renewal"
├─ Bonus: +5% permanent XP gain (total: +20%)
└─ Profile Frame: Gold Prestige Frame

Prestige 10:
├─ Reward: 100 Encore Tokens + Title "Eternal Champion"
├─ Bonus: +10% permanent XP gain (total: +65%)
└─ Profile Frame: Platinum Prestige Frame + Exclusive Badge
```

**What You Keep:**
- ✅ All pets and their levels
- ✅ All base buildings and upgrades
- ✅ All items and gear
- ✅ All currency (Glow Cash, Hype Crystals, Star Shards)
- ✅ All achievements and titles
- ✅ All cosmetics

**What Resets:**
- ❌ Player Account Level (back to Level 1)
- ❌ Expedition depth progress (restart from base)
- ❌ Some repeatable quest progress

**Why Prestige Works:**
- Provides infinite progression (never "done")
- Rewards dedicated players with status symbols
- Adds long-term goals (months to achieve multiple prestiges)
- Creates social hierarchy (high prestige = veteran)

---

### **Secondary Earning: Major Achievements**

**Platinum-Tier Achievements (Extremely Rare):**

| Achievement | Requirement | Encore Token Reward |
|-------------|-------------|-------------------|
| "Master Collector" | Capture all 200+ species | 25 Encore Tokens |
| "Dungeon Conqueror" | Complete all dungeons on Hard Mode | 30 Encore Tokens |
| "PvPvE Legend" | Win 100 PvPvE duels | 20 Encore Tokens |
| "Pet Master" | Own 10 pets at Max Level + 5-star | 40 Encore Tokens |
| "Billionaire" | Accumulate 100,000,000 Glow Cash net worth | 50 Encore Tokens |
| "Speedrunner" | Complete expedition in under 5 minutes | 15 Encore Tokens |
| "Perfect Warrior" | Chain 1,000 Perfect hits | 20 Encore Tokens |
| "Guild Leader" | Lead a top 10 guild for 3 months | 35 Encore Tokens |

**Total Encore Tokens from Achievements:** ~300 Encore Tokens (lifetime)

---

### **Tertiary Earning: Seasonal Leaderboards**

```
At the end of each 3-month season, top players receive Encore Tokens:

Leaderboard Category: Expedition Depth
├─ Rank 1-10: 50 Encore Tokens
├─ Rank 11-50: 25 Encore Tokens
├─ Rank 51-100: 10 Encore Tokens
└─ Rank 101-500: 5 Encore Tokens

Leaderboard Category: PvPvE Wins
├─ Rank 1-10: 50 Encore Tokens
├─ Rank 11-50: 25 Encore Tokens
└─ Rank 51-100: 10 Encore Tokens

Leaderboard Category: Collection Completeness
├─ Rank 1-10: 30 Encore Tokens
└─ Rank 11-50: 15 Encore Tokens

Per Season (Top 10 all categories): 130 Encore Tokens max
Per Year (4 seasons): 520 Encore Tokens max (for top players)
```

---

### **Expected Encore Token Accumulation**

| Player Type | Months Played | Encore Tokens Earned | Primary Source |
|-------------|--------------|---------------------|----------------|
| Casual | 6 months | 10-30 | Achievements only |
| Regular | 6 months | 40-80 | 1-2 prestiges + achievements |
| Hardcore | 6 months | 100-200 | 3-5 prestiges + achievements + leaderboards |
| Elite | 6 months | 250-400 | 5-10 prestiges + all achievements + top leaderboard |

**Prestige Token Rarity:**
- Most valuable currency in the game
- Takes months to accumulate significant amounts
- Highly prestigious to own (visible status)

---

## 🏪 PRESTIGE SHOP & REWARDS

### **Exclusive Titles (Social Status)**

**Title Tiers:**

| Title | Encore Token Cost | Visual Effect | Rarity |
|-------|------------------|---------------|--------|
| "The Ascending" | Free (Prestige 1 reward) | Standard text | Common |
| "Veteran" | 25 Encore Tokens | Bronze glow | Uncommon |
| "Elite Guardian" | 50 Encore Tokens | Silver glow | Rare |
| "Legendary Master" | 100 Encore Tokens | Gold glow + sparkles | Epic |
| "Mythic Champion" | 200 Encore Tokens | Iridescent glow + aura | Legendary |
| "Eternal Sovereign" | 500 Encore Tokens | Rainbow shimmer + crown icon | Mythic |

**Title Categories:**

```
Combat Titles:
├─ "Duelist" (50 Encore Tokens): Win 50 PvPvE duels
├─ "Gladiator" (100 Encore Tokens): Win 100 PvPvE duels
└─ "Arena Champion" (200 Encore Tokens): Top 10 PvPvE leaderboard

Collection Titles:
├─ "Naturalist" (30 Encore Tokens): Capture 100 species
├─ "Zoologist" (75 Encore Tokens): Capture 150 species
└─ "Pokédex Complete" (150 Encore Tokens): Capture all species

Wealth Titles:
├─ "Millionaire" (50 Encore Tokens): 10M+ Glow Cash
├─ "Tycoon" (100 Encore Tokens): 50M+ Glow Cash
└─ "Economic Overlord" (200 Encore Tokens): 100M+ Glow Cash
```

---

### **Profile Frames (Visual Prestige)**

**Frame Rarity Tiers:**

| Frame | Encore Token Cost | Visual Design | Animation |
|-------|------------------|---------------|-----------|
| Bronze Frame | 40 Encore Tokens | Bronze border, simple | Static |
| Silver Frame | 80 Encore Tokens | Silver border, elegant | Gentle pulse |
| Gold Frame | 150 Encore Tokens | Gold border, ornate | Shimmer effect |
| Platinum Frame | 300 Encore Tokens | Platinum + gems | Rotating particles |
| Mythic Frame | 500 Encore Tokens | Animated rainbow | Full animation loop |

**Exclusive Seasonal Frames:**

```
Limited-time frames available only during specific seasons:

Summer Festival Frame: 200 Encore Tokens (June-July only)
Halloween Spooky Frame: 200 Encore Tokens (October only)
Winter Wonderland Frame: 200 Encore Tokens (December only)

Why Limited:
├─ Creates urgency (FOMO)
├─ Rewards active seasonal players
├─ Becomes rare/prestigious after season ends
└─ Shows "I was there" status
```

---

### **Profile Badges (Achievement Showcases)**

**Badge System:**

```
Players can display up to 6 badges on their profile:

Badge Categories:
├─ Prestige Badges: Show prestige level (Prestige 1-10+)
├─ Achievement Badges: Show rare achievement completion
├─ Seasonal Badges: Show seasonal event participation
├─ Guild Badges: Show guild rank/leadership
└─ Special Badges: Exclusive one-time events

Badge Costs:
├─ Common Badges: 10-25 Encore Tokens
├─ Rare Badges: 30-60 Encore Tokens
├─ Epic Badges: 75-150 Encore Tokens
└─ Legendary Badges: 200-400 Encore Tokens
```

**Example Badges:**

| Badge Name | Encore Token Cost | Requirement | Visual |
|------------|------------------|-------------|--------|
| "Prestige Master" | 100 Encore Tokens | Reach Prestige 5 | Gold medallion |
| "Dungeon Delver" | 75 Encore Tokens | Complete 100 dungeons | Dungeon icon |
| "Perfect Chain" | 50 Encore Tokens | 500 Perfect hits in a row | Chain icon |
| "First Blood" | 200 Encore Tokens | Be first to defeat new boss | Crown icon |
| "Beta Tester" | Free (Special) | Play during beta | Exclusive beta badge |

---

### **Exclusive Cosmetics (Premium Prestige Items)**

**Prestige-Exclusive Cosmetics:**

These cosmetics CANNOT be obtained any other way—not with Glow Cash, Hype Crystals, or Star Shards. Only Encore Tokens.

| Cosmetic Type | Encore Token Cost | Description |
|--------------|------------------|-------------|
| Prestige Pet Skin | 300 Encore Tokens | Golden ethereal glow, particle trail |
| Prestige Weapon Skin | 250 Encore Tokens | Mythic-tier visual effects |
| Prestige Emote | 200 Encore Tokens | Unique animation (victory pose) |
| Prestige Base Theme | 500 Encore Tokens | Gold + purple aesthetic for entire base |

**Why Prestige Cosmetics Matter:**
- Instant recognition of dedication
- Cannot be bought with real money (earned only)
- Social status symbol
- Shows commitment to the game

---

## 📈 PRESTIGE PROGRESSION

### **Prestige Leveling Speed**

**Time to Reach Level 100 (Per Prestige):**

| Prestige Level | XP Required | Expected Time | XP Bonus from Past Prestiges |
|----------------|-------------|---------------|----------------------------|
| Prestige 1 (First time) | 5,000,000 XP | 60-80 hours | 0% |
| Prestige 2 | 5,000,000 XP | 55-70 hours | +1% (+50k XP saved) |
| Prestige 3 | 5,000,000 XP | 50-65 hours | +3% (+150k XP saved) |
| Prestige 5 | 5,000,000 XP | 40-55 hours | +20% (+1M XP saved) |
| Prestige 10 | 5,000,000 XP | 30-45 hours | +65% (+3.25M XP saved) |

**Diminishing Time Investment:**
- First prestige: ~70 hours
- Tenth prestige: ~38 hours (46% faster)
- Result: Players can prestige multiple times without feeling punished

---

### **Long-Term Prestige Goals**

**Year 1 Hardcore Player:**
- Prestige 5-7 (300-400 hours of play)
- Encore Tokens: 150-250
- Can afford: 2-3 major cosmetics + several titles/frames

**Year 2 Veteran Player:**
- Prestige 10-15
- Encore Tokens: 500-800
- Can afford: Most prestige shop items, working on limited seasonal

**Year 3+ Elite Player:**
- Prestige 20-30+
- Encore Tokens: 1,500-3,000+
- Can afford: Everything + collecting limited seasonal items

---

# PART 5: STAR SHARDS (PREMIUM CURRENCY)

## ⭐ STAR SHARDS OVERVIEW

**Note:** This section summarizes premium currency monetization, which is already extensively documented in the Base Building System Design Document. See that document for full details on ethical monetization strategy.

### **What are Star Shards?**

Star Shards are the **premium currency** purchased with real money. They are used EXCLUSIVELY for cosmetic items and convenience features—NEVER for power advantages.

**Visual Identity:**
- Icon: ⭐ Shimmering star fragment
- Color: Bright white with rainbow refraction (#FFFFFF + rainbow)
- Sound: Magical twinkle
- Animation: Rotates and glows

**Ethical Design Principles:**
1. **No Pay-to-Win:** Zero gameplay advantages
2. **Cosmetic Focus:** 60% of purchases are cosmetics
3. **Convenience Options:** 30% are time-savers (optional)
4. **Fair Pricing:** Industry-standard prices
5. **Respect Free Players:** 100% content accessible without spending

---

## 💳 PREMIUM CURRENCY PRICING

**Star Shard Bundles:**

| Bundle | Star Shards | Bonus | Price (USD) | $/100 Shards |
|--------|------------|-------|-------------|--------------|
| Starter | 500 | 0% | $4.99 | $0.998 |
| Value | 1,100 | 10% | $9.99 | $0.908 |
| Popular | 2,500 | 25% | $19.99 | $0.800 |
| Premium | 5,500 | 38% | $49.99 | $0.909 |
| Mega | 12,000 | 50% | $99.99 | $0.833 |

**Pricing Philosophy:**
- Small impulse purchases ($5)
- Standard value ($10-20)
- Whale options ($50-100)
- Bonus incentivizes larger purchases

---

## 🛡️ ETHICAL MONETIZATION FRAMEWORK

**What Star Shards CAN Buy:**

✅ **Cosmetics (60% of revenue):**
- Character customization (hairstyles, outfits, emotes)
- Pet skins (visual overhauls)
- Building skins (aesthetic variants)
- Base themes (global visual changes)

✅ **Convenience (30% of revenue):**
- Instant upgrade tokens (skip wait times)
- Extra building plots (+4 permanent slots)
- Warehouse expansion (+500 slots)
- Premium Generator Mode (2x passive income)
- Fast Travel Pass (30-day unlimited)

✅ **Battle Pass (10% of revenue):**
- $9.99 seasonal battle pass (3-4 per year)
- Exclusive cosmetics + resources + premium currency back

**What Star Shards CANNOT Buy:**

❌ **NEVER:**
- Stat boosts (+damage, +defense, etc.)
- Exclusive powerful items (all gear earnable free)
- Loot boxes/gacha (no randomized premium purchases)
- Energy systems (no "stamina refills")
- Competitive advantages (no PvP pay-to-win)
- Content locks (no premium-only biomes/pets)
- Level skips (cannot buy instant max level)

---

## 📊 REVENUE PROJECTIONS

**Expected Average Revenue Per User (ARPU):**

| Player Type | % of Players | Spending/Year | Purchases |
|-------------|--------------|---------------|-----------|
| Free Players | 80% | $0 | None |
| Minnows | 15% | $10-30 | Battle Pass + occasional cosmetic |
| Dolphins | 4% | $50-150 | Battle Pass + cosmetics + convenience |
| Whales | 1% | $200-500+ | Everything available |

**Total ARPU:** $8-12/year (industry standard for ethical F2P)

**Revenue Projection (100,000 active players):**
- Year 1: $800,000-$1,200,000
- Year 2: $1,200,000-$1,800,000
- Year 3: $1,500,000-$2,500,000

**Revenue Streams:**
- Cosmetics: 60% ($7.2M over 3 years)
- Convenience: 30% ($3.6M over 3 years)
- Battle Pass: 10% ($1.2M over 3 years)

---

# PART 6: MATERIALS SYSTEM

## 🔥 ELEMENTAL MATERIALS (COMMON → LEGENDARY)

### **Material Hierarchy**

Each of the 8 elements has a 5-tier material system:

```
FIRE MATERIALS:
├─ Tier 1 (Common): Ember Shard
├─ Tier 2 (Uncommon): Fire Crystal
├─ Tier 3 (Rare): Magma Core
├─ Tier 4 (Epic): Inferno Essence
└─ Tier 5 (Legendary): Eternal Flame

WATER MATERIALS:
├─ Tier 1 (Common): Water Drop
├─ Tier 2 (Uncommon): Aqua Pearl
├─ Tier 3 (Rare): Tidal Stone
├─ Tier 4 (Epic): Ocean Heart
└─ Tier 5 (Legendary): Primordial Tide

EARTH MATERIALS:
├─ Tier 1 (Common): Pebble Shard
├─ Tier 2 (Uncommon): Earth Crystal
├─ Tier 3 (Rare): Boulder Core
├─ Tier 4 (Epic): Terra Essence
└─ Tier 5 (Legendary): World Stone

WIND MATERIALS:
├─ Tier 1 (Common): Breeze Wisp
├─ Tier 2 (Uncommon): Wind Crystal
├─ Tier 3 (Rare): Gale Core
├─ Tier 4 (Epic): Tempest Essence
└─ Tier 5 (Legendary): Sky Shard

LIGHTNING MATERIALS:
├─ Tier 1 (Common): Spark Fragment
├─ Tier 2 (Uncommon): Bolt Crystal
├─ Tier 3 (Rare): Thunder Core
├─ Tier 4 (Epic): Storm Essence
└─ Tier 5 (Legendary): Eternal Charge

NATURE MATERIALS:
├─ Tier 1 (Common): Leaf Essence
├─ Tier 2 (Uncommon): Vine Crystal
├─ Tier 3 (Rare): Root Core
├─ Tier 4 (Epic): Life Essence
└─ Tier 5 (Legendary): World Tree Seed

DARK MATERIALS:
├─ Tier 1 (Common): Shadow Wisp
├─ Tier 2 (Uncommon): Void Crystal
├─ Tier 3 (Rare): Abyss Core
├─ Tier 4 (Epic): Darkness Essence
└─ Tier 5 (Legendary): Primordial Dark

LIGHT MATERIALS:
├─ Tier 1 (Common): Gleam Shard
├─ Tier 2 (Uncommon): Radiance Crystal
├─ Tier 3 (Rare): Lumen Core
├─ Tier 4 (Epic): Celestial Essence
└─ Tier 5 (Legendary): Divine Light
```

---

### **Material Drop Rates**

**Enemy Defeat Drops:**

| Enemy Rarity | Material Tier | Drop Chance | Amount |
|--------------|--------------|-------------|--------|
| Common | Common (Tier 1) | 100% | 2-5 |
| Uncommon | Uncommon (Tier 2) | 80% | 1-3 |
| Rare | Rare (Tier 3) | 60% | 1-2 |
| Epic | Epic (Tier 4) | 40% | 1-2 |
| Legendary | Legendary (Tier 5) | 20% | 1 |
| Mythic | Legendary (Tier 5) | 60% | 2-3 |
| Unique | Legendary (Tier 5) | 100% | 5-10 |

**Chest Loot:**

| Chest Rarity | Material Tier | Guaranteed Amount |
|--------------|--------------|-------------------|
| Common | Common | 5-10 |
| Uncommon | Uncommon | 3-6 |
| Rare | Rare | 2-4 |
| Epic | Epic | 1-3 |
| Legendary | Legendary | 1-2 |

---

### **Material Storage Limits**

```
Base Storage Capacity (Warehouse Level 1):

├─ Common Materials: 10,000 per element
├─ Uncommon Materials: 5,000 per element
├─ Rare Materials: 1,000 per element
├─ Epic Materials: 500 per element
└─ Legendary Materials: 100 per element

Total Base Storage: 132,800 material units (8 elements × 16,600)

Warehouse Upgrades:
├─ Level 3: +25% capacity (166,000 total)
├─ Level 5: +50% capacity (199,200 total)
├─ Level 7: +75% capacity (232,400 total)
└─ Level 10: +100% capacity (265,600 total)

Premium Expansion (+$4.99 one-time):
└─ +50% permanent capacity (398,400 max total)
```

---

### **Material Conversion System**

**Upconversion (Low → High):**

```
Conversion Ratio: 10:1
Conversion Fee: 1,000 Glow Cash per conversion

Examples:
├─ 10 Ember Shard → 1 Fire Crystal (+ 1,000 Glow Cash)
├─ 10 Fire Crystal → 1 Magma Core (+ 1,000 Glow Cash)
├─ 10 Magma Core → 1 Inferno Essence (+ 1,000 Glow Cash)
└─ 10 Inferno Essence → 1 Eternal Flame (+ 1,000 Glow Cash)

Total Cost (Common → Legendary):
├─ 10,000 Common materials
├─ 4,000 Glow Cash (4 conversion steps)
└─ Result: 1 Legendary material
```

**Downconversion (High → Low):**

```
Conversion Ratio: 1:5
Conversion Fee: 5,000 Glow Cash per downconversion

Examples:
├─ 1 Eternal Flame → 5 Inferno Essence (+ 5,000 Glow Cash)
├─ 1 Inferno Essence → 5 Magma Core (+ 5,000 Glow Cash)
└─ 1 Magma Core → 5 Fire Crystal (+ 5,000 Glow Cash)

Warning: Very inefficient, emergency use only
```

---

## 🏗️ UNIVERSAL RESOURCES (STONE, IRON, CRYSTAL)

### **Universal Resource Overview**

These materials are NOT tied to any specific element and are used exclusively for base building upgrades.

**Three Universal Tiers:**

| Tier | Resource | Used For | Source |
|------|----------|----------|--------|
| Basic | Stone | Building Levels 1-4 | Mining nodes (90% spawn rate) |
| Advanced | Iron | Building Levels 5-7 | Mining nodes (8% spawn rate) |
| Premium | Crystal | Building Levels 8-10 | Mining nodes (2% spawn rate) |

---

### **Universal Resource Earning**

**Mining Nodes (Found in ALL Biomes):**

```
Stone Deposit:
├─ Spawn Rate: 90% of mining nodes
├─ Yield: 5-10 Stone per harvest
├─ Respawn Time: 10 minutes
└─ Optimal Farming: Stone Wastes biome (highest node density)

Iron Vein:
├─ Spawn Rate: 8% of mining nodes
├─ Yield: 3-5 Iron per harvest
├─ Respawn Time: 10 minutes
└─ Optimal Farming: Mountain biomes

Crystal Formation:
├─ Spawn Rate: 2% of mining nodes
├─ Yield: 1-2 Crystal per harvest
├─ Respawn Time: 10 minutes
└─ Optimal Farming: Volcanic/Abyss biomes (deeper = better)
```

**Vendor Purchase (Emergency Fallback):**

| Resource | Glow Cash Cost | Availability |
|----------|---------------|--------------|
| Stone | 5 each | Unlimited stock |
| Iron | 50 each | Unlimited stock |
| Crystal | 500 each | Limited stock (50/day) |

**Expedition Rewards:**

- **Common Expeditions:** 50-100 Stone per run
- **Advanced Expeditions:** 25-50 Iron per run
- **Endgame Expeditions:** 5-15 Crystal per run

---

### **Universal Resource Requirements**

**Total Universal Resources Needed (All 20 Buildings to Level 10):**

| Resource | Total Required | Cost if Bought | Time to Farm |
|----------|---------------|----------------|--------------|
| Stone | ~50,000 | 250,000 Glow Cash | 20-30 hours |
| Iron | ~100,000 | 5,000,000 Glow Cash | 40-60 hours |
| Crystal | ~30,000 | 15,000,000 Glow Cash | 60-80 hours |

**Recommended Strategy:**
- ✅ Farm Stone (abundant, easy)
- ✅ Farm Iron (moderate, worthwhile)
- ❌ Don't buy Crystal (extremely expensive)
- ✅ Mine Crystal yourself (time investment but much cheaper)

---

## 💎 SPECIAL CURRENCIES (ESSENCE & CORES)

### **Rare Essence, Epic Essence, Legendary Core**

These are **high-tier crafting materials** used for endgame building upgrades and pet breeding. They bridge the gap between common materials and currency.

**Three Special Currency Tiers:**

| Currency | Rarity | Used For | Source |
|----------|--------|----------|--------|
| Rare Essence | Rare | Building Levels 4-6, breeding | Decompose Rare+ pets, dungeons |
| Epic Essence | Epic | Building Levels 7-8, high breeding | Decompose Epic+ pets, elite dungeons |
| Legendary Core | Legendary | Building Levels 9-10, fusion | Decompose Legendary+ pets, boss dungeons |

---

### **Special Currency Earning**

**Method 1: Pet Decomposition (Primary Source)**

```
Decompose Feature:
└─ Permanently destroy unwanted pet → receive resources

Decomposition Yields:
├─ Common Pet: 5-10 Rare Essence
├─ Uncommon Pet: 10-20 Rare Essence
├─ Rare Pet: 20-30 Rare Essence + 1-3 Epic Essence
├─ Epic Pet: 50 Rare Essence + 10-20 Epic Essence
├─ Legendary Pet: 100 Rare Essence + 50 Epic Essence + 10-20 Legendary Core
├─ Mythic Pet: 200 Rare Essence + 100 Epic Essence + 50-100 Legendary Core
└─ Unique Pet: 500 Rare Essence + 250 Epic Essence + 200-300 Legendary Core

Strategic Use:
├─ Decompose duplicate low-IV pets (keep high-IV for merging)
├─ Decompose Common/Uncommon pets (abundant)
└─ NEVER decompose Legendary+ unless truly worthless
```

**Method 2: Dungeon Rewards**

```
Common Dungeon: 10-20 Rare Essence (guaranteed)
Rare Dungeon: 30-50 Rare Essence + 5-10 Epic Essence
Epic Dungeon: 100 Rare Essence + 30-50 Epic Essence + 5-10 Legendary Core
Legendary Dungeon: 250 Rare Essence + 100 Epic Essence + 30-50 Legendary Core
Boss Dungeon (Weekly): 500 Rare Essence + 250 Epic Essence + 100 Legendary Core
```

**Method 3: Event Rewards**

```
Seasonal Events:
├─ Daily Login: 10 Rare Essence per day
├─ Weekly Challenge: 50 Rare Essence + 10 Epic Essence
├─ Monthly Achievement: 200 Rare Essence + 50 Epic Essence + 10 Legendary Core
└─ Leaderboard Rewards (Top 100): 1,000+ Legendary Core
```

**Method 4: Trading (Player Economy)**

```
Market Prices (Approximate):
├─ Rare Essence: 100-200 Glow Cash each
├─ Epic Essence: 1,000-2,000 Glow Cash each
└─ Legendary Core: 10,000-25,000 Glow Cash each

Trading Strategy:
├─ Buy Rare Essence with excess Glow Cash (relatively cheap)
├─ Farm Epic Essence yourself (expensive to buy)
└─ Never buy Legendary Core unless emergency (extremely expensive)
```

---

### **Special Currency Requirements**

**Total Special Currencies Needed (All 20 Buildings to Level 10):**

| Currency | Total Required | Equivalent Glow Cash (if bought) |
|----------|---------------|--------------------------------|
| Rare Essence | ~50,000 | 5,000,000-10,000,000 Glow Cash |
| Epic Essence | ~20,000 | 20,000,000-40,000,000 Glow Cash |
| Legendary Core | ~12,000 | 120,000,000-300,000,000 Glow Cash |

**Key Takeaway:** Special currencies are FAR too expensive to buy—they MUST be farmed through dungeons and pet decomposition. This creates a natural progression gate.

---

# PART 7: EVENT CURRENCY SYSTEM

## 🎪 SEASONAL EVENT CURRENCY

### **Event Currency Design**

Each seasonal event introduces a **temporary event currency** that can be earned during the event and spent in the Event Shop. Leftover currency converts to Glow Cash at the end of the event.

**Event Currency Examples:**

| Season | Event Currency | Icon | Duration |
|--------|---------------|------|----------|
| Summer Festival | Beach Tokens | 🏖️ | June-July (3 weeks) |
| Halloween | Candy Tokens | 🍬 | October (3 weeks) |
| Winter Wonderland | Snowflake Tokens | ❄️ | December (3 weeks) |
| Spring Bloom | Flower Petals | 🌸 | March-April (3 weeks) |

---

### **Event Currency Earning**

**Daily Event Quests:**

```
Each day during the event, players receive 3 event quests:

Example (Halloween Event):
├─ "Defeat 10 Spooky Pets": 50 Candy Tokens
├─ "Complete Haunted Dungeon": 100 Candy Tokens
└─ "Capture 5 Ghost Pets": 75 Candy Tokens

Daily Total: 225 Candy Tokens
Weekly Total: 1,575 Candy Tokens
Event Total (3 weeks): 4,725 Candy Tokens
```

**Weekly Event Challenge:**

```
Each week, one major challenge:

Week 1: "Defeat Headless Horseman Boss": 500 Candy Tokens
Week 2: "Complete 10 Haunted Dungeons": 500 Candy Tokens
Week 3: "Capture 20 Unique Halloween Pets": 500 Candy Tokens

Total from Weekly Challenges: 1,500 Candy Tokens
```

**Event Leaderboard:**

```
At the end of the event, top players receive bonus event currency:

Rank 1-10: 2,000 Candy Tokens
Rank 11-50: 1,000 Candy Tokens
Rank 51-100: 500 Candy Tokens
Rank 101-500: 250 Candy Tokens
```

**Random Event Drops:**

```
During the event, enemies have a chance to drop event currency:

Common Pet: 1-3 Candy Tokens (10% chance)
Rare Pet: 5-10 Candy Tokens (25% chance)
Epic Pet: 15-30 Candy Tokens (50% chance)
Legendary Pet: 50-100 Candy Tokens (100% chance)

Average Farming Rate: 100-200 Candy Tokens/hour (active play)
```

**Premium Currency Conversion (Pay-to-Catch-Up):**

```
Players can convert Star Shards (premium currency) to event currency:

100 Star Shards → 1,000 Event Tokens

Why Allow This:
├─ Lets late-joiners catch up (joined event late)
├─ Optional for players with limited time (busy week)
├─ Ethical because it's just time-saver (not exclusive content)
└─ Revenue opportunity (optional, not required)
```

---

### **Total Event Currency (Average Player)**

| Player Type | Active Play | Event Currency Earned |
|-------------|-------------|----------------------|
| Casual | 1-2 hours/day | 6,000-8,000 |
| Regular | 2-4 hours/day | 10,000-15,000 |
| Hardcore | 4-6 hours/day | 18,000-25,000 |
| Elite (+ Leaderboard) | 6+ hours/day | 30,000-40,000+ |

---

## 🏪 EVENT SHOP & REWARDS

### **Event Shop Structure**

```
Event Shop has 4 tiers of rewards:

Tier 1: Budget Items (50-200 Event Tokens)
├─ Consumables (potions, boosts)
├─ Common materials
└─ Small Glow Cash bundles

Tier 2: Mid-Range Items (200-800 Event Tokens)
├─ Event-themed cosmetics (common)
├─ Rare materials
└─ Event-exclusive pet eggs

Tier 3: Premium Items (800-2,000 Event Tokens)
├─ Exclusive event cosmetics (rare/epic)
├─ Epic materials
└─ Exclusive event titles

Tier 4: Grand Prize (3,000-5,000 Event Tokens)
├─ Legendary event cosmetic (unobtainable elsewhere)
├─ Event-exclusive Mythic pet
└─ Exclusive profile frame
```

---

### **Example Event Shop (Halloween)**

| Item | Candy Token Cost | Description |
|------|-----------------|-------------|
| **TIER 1** |
| Health Potion ×10 | 100 | Restore 25% HP |
| Capture Boost ×5 | 150 | +10% Capture Rate |
| 5,000 Glow Cash | 200 | Currency bundle |
| **TIER 2** |
| Pumpkin Hat | 500 | Cosmetic headgear |
| Ghost Pet Egg | 800 | Event-exclusive pet |
| 50 Rare Essence | 600 | Crafting materials |
| **TIER 3** |
| Spooky Emote | 1,200 | Exclusive animation |
| Witch Outfit | 1,500 | Full cosmetic set |
| "Spooky" Title | 1,000 | Event-exclusive title |
| **TIER 4** |
| Headless Horseman Pet Skin | 3,500 | Legendary cosmetic |
| Haunted Mansion Base Theme | 4,000 | Event-exclusive theme |
| Halloween Profile Frame | 5,000 | Ultra-rare frame |

**Total Cost for Everything:** ~20,000 Candy Tokens
**Average Casual Player Earnings:** 6,000-8,000 Candy Tokens

**Key Design:**
- Casual players can afford Tier 1 + 2 items
- Regular players can afford Tier 1 + 2 + some Tier 3
- Hardcore players can afford everything except 1-2 Grand Prizes
- Elite players can afford everything (or use premium conversion)

---

## ⚖️ EVENT ECONOMY BALANCE

### **Event Currency Conversion (Leftover Currency)**

```
At the end of the event, leftover event currency converts to Glow Cash:

Conversion Rate: 1 Event Token → 50 Glow Cash

Examples:
├─ 500 leftover Candy Tokens → 25,000 Glow Cash
├─ 2,000 leftover Candy Tokens → 100,000 Glow Cash
└─ 5,000 leftover Candy Tokens → 250,000 Glow Cash

Why Conversion Matters:
├─ No wasted effort (currency has value even after event)
├─ Encourages farming (leftovers still useful)
├─ Prevents hoarding for next year (currency expires)
└─ Rewards event participation (bonus Glow Cash)
```

---

### **Event Balance Philosophy**

**Design Goals:**

1. **Casual players get something:** Even 1 hour/day = Tier 1-2 rewards
2. **Hardcore players get most things:** 3-4 hours/day = Tier 1-3 + some Tier 4
3. **Grand Prize is aspirational:** Requires dedication or premium conversion
4. **Premium conversion is optional:** Never required, just catch-up

**Why This Works:**
- No one feels excluded (everyone gets rewards)
- Hardcore players feel rewarded (exclusive Grand Prize)
- Premium conversion is ethical (just time-saver)
- Event currency converts (no waste)

---

# PART 8: TRADING ECONOMY

## 🤝 PLAYER-TO-PLAYER TRADING

### **Direct Trading System**

**How Direct Trading Works:**

```
Two players can initiate a direct trade:

Step 1: Player A sends trade request to Player B
Step 2: Both players open trade window
Step 3: Each player adds items/currency to trade window
Step 4: Both players review and confirm
Step 5: Trade executes (no take-backs)

Trade Window UI:
┌─────────────────────────────────────────────────────────┐
│ DIRECT TRADE: Player A ↔ Player B                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ PLAYER A OFFERS:                PLAYER B OFFERS:        │
│ ├─ 10,000 Glow Cash            ├─ Rare Pet (3-star)    │
│ ├─ 50 Rare Essence             ├─ Epic Weapon          │
│ └─ Uncommon Materials ×100     └─ 5 Hype Crystals      │
│                                                         │
│ [CONFIRM TRADE]                 [CONFIRM TRADE]         │
│                                                         │
│ Both players must confirm to complete trade             │
└─────────────────────────────────────────────────────────┘
```

---

### **What Can Be Traded**

✅ **TRADEABLE:**
- Glow Cash (soft currency)
- Elemental materials (all tiers)
- Universal resources (Stone, Iron, Crystal)
- Special currencies (Rare Essence, Epic Essence, Legendary Core)
- Unequipped weapons and armor
- Consumables (potions, boosts)
- Crafting blueprints

❌ **NON-TRADEABLE:**
- Pets (cannot trade to prevent pay-to-win)
- Hype Crystals (rare currency must be earned)
- Encore Tokens (prestige currency must be earned)
- Star Shards (premium currency)
- Equipped gear (must unequip first)
- Event currency (temporary, expires)
- Bound items (soulbound exclusives)

---

### **Direct Trade Fees**

```
Direct Trade Fee: 5% of Glow Cash value

Examples:
├─ Trade 10,000 Glow Cash → 500 fee (9,500 received)
├─ Trade items worth 50,000 Glow Cash → 2,500 fee
└─ Trade items worth 1,000,000 Glow Cash → 50,000 fee

Why Fee Exists:
├─ Currency sink (removes Glow Cash from economy)
├─ Prevents infinite item flipping (cost to trade)
├─ Encourages auction house (lower fees)
└─ Reduces scam attempts (cost barrier)
```

---

## 🏛️ AUCTION HOUSE MECHANICS

### **Auction House Overview**

The Auction House allows players to list items for sale to the entire player base. It's the primary player-driven market.

**Auction House Features:**
- Search & filter by item type, rarity, price
- Bid system OR instant buyout
- 24-48 hour listing duration
- Automatic highest bidder wins
- Notifications when outbid or auction won

---

### **Listing an Item**

```
Step 1: Open Market/Trading Post building
Step 2: Select "Auction House" tab
Step 3: Choose item to list
Step 4: Set starting bid and buyout price
Step 5: Choose duration (24h, 48h, 72h)
Step 6: Pay listing fee (1% of buyout price)
Step 7: Item is listed for other players to see

Listing Fee Example:
├─ List item with 100,000 Glow Cash buyout
├─ Pay 1,000 Glow Cash listing fee (upfront, non-refundable)
└─ If item doesn't sell, lose 1,000 Glow Cash
```

---

### **Bidding on an Item**

```
Step 1: Browse Auction House
Step 2: Find item you want
Step 3: Place bid (must be higher than current bid + minimum increment)
Step 4: If outbid, Glow Cash refunded automatically
Step 5: If you win, pay final bid + 5% sale fee
Step 6: Item delivered to your mailbox

Bidding Example:
├─ Item listed with 50,000 Glow Cash starting bid
├─ You bid 60,000 Glow Cash
├─ Someone bids 70,000 Glow Cash → You're refunded 60,000
├─ No more bids, auction ends
├─ Winner pays 70,000 + 3,500 (5% fee) = 73,500 total
└─ Seller receives 69,300 (70,000 - 700 listing fee)
```

---

### **Buyout System**

```
Instant Buyout Option:

Instead of bidding, players can instantly buy the item at the buyout price:

Example:
├─ Item listed: Starting bid 10,000, Buyout 50,000
├─ Player A bids 15,000
├─ Player B clicks "Buyout" for 50,000
├─ Player B wins immediately (auction ends early)
├─ Player A refunded 15,000
├─ Player B pays 50,000 + 2,500 (5% fee) = 52,500 total
└─ Seller receives 49,500 (50,000 - 500 listing fee)

Why Buyout Matters:
├─ Convenience (instant purchase)
├─ Avoids bidding wars
├─ Guarantees item acquisition
└─ Premium pricing (usually 2-5x starting bid)
```

---

## 📜 MARKET FEES & REGULATIONS

### **Complete Fee Structure**

| Transaction Type | Fee Structure | Purpose |
|-----------------|---------------|---------|
| Direct Trade | 5% of Glow Cash value | Currency sink, reduces flipping |
| Auction House Listing | 1% of buyout price (upfront) | Prevents spam listings |
| Auction House Sale | 5% of final sale price | Currency sink |
| **Total Auction Fee** | **6% total** | (1% listing + 5% sale) |

**Fee Comparison:**

```
Selling a 100,000 Glow Cash item:

Direct Trade:
├─ Buyer pays: 100,000
├─ Fee: 5,000 (5%)
├─ Seller receives: 95,000
└─ Total cost to buyer: 100,000

Auction House:
├─ Listing fee (paid by seller): 1,000 (1%)
├─ Buyer pays: 100,000
├─ Sale fee (paid by seller): 5,000 (5%)
├─ Seller receives: 94,000 (100,000 - 1,000 - 5,000)
└─ Total cost to buyer: 100,000

Key Difference:
├─ Direct Trade: Seller gets 95,000 (5% fee)
├─ Auction House: Seller gets 94,000 (6% fee)
└─ Auction House has higher reach (worth extra 1% fee)
```

---

### **Anti-Manipulation Regulations**

**Listing Limits:**

```
Per Player Limits:

├─ Max 50 active auction listings at once
├─ Max 100 successful sales per week
├─ Max 200 total listings per week
└─ Max 20 listings of same item type

Why Limits:
├─ Prevents market flooding
├─ Stops bots from dominating
├─ Encourages strategic listing
└─ Reduces server load
```

**Purchase Limits:**

```
Per Player Limits:

├─ Max 100 purchases of same item per day
├─ Max 1,000 total purchases per week
└─ Max 10,000,000 Glow Cash spent per day (anti-RMT)

Why Limits:
├─ Prevents cornering markets (buying all supply)
├─ Reduces price manipulation
├─ Detects suspicious activity (bots, RMT)
└─ Protects economy stability
```

**Price Floor/Ceiling Warnings:**

```
Extreme Price Detection:

If an item is listed at:
├─ 90% below market average → Warning: "This price is unusually low"
├─ 300% above market average → Warning: "This price is unusually high"
└─ Player can still list, but receives warning

Why Warnings:
├─ Prevents accidental low listings (typo protection)
├─ Alerts buyers to suspicious prices (scam prevention)
├─ Doesn't force prices (free market maintained)
└─ Educates players about market value
```

---

## 🛡️ ECONOMIC STABILITY SYSTEMS

### **Dynamic Supply & Demand**

**Market Analytics (Available to Players):**

```
Auction House Analytics Tab:

Shows for each item:
├─ Average sale price (last 7 days)
├─ Total listings currently active
├─ Total sales (last 7 days)
├─ Price trend graph (14-day history)
└─ Supply vs demand indicator

Example Analytics:
"Rare Essence"
├─ Average Price: 150 Glow Cash
├─ Active Listings: 342
├─ Sales (7 days): 1,248
├─ Trend: Decreasing (-12%)
└─ Supply > Demand (Price falling)

Why Analytics Matter:
├─ Informed trading decisions
├─ Identify market opportunities
├─ Predict price changes
└─ Educates players about economics
```

---

### **NPC Vendor Price Anchoring**

**NPC Vendor Prices (Safety Net):**

```
NPC vendors buy and sell common items at fixed prices:

NPC Sell Prices (Players buy from NPCs):
├─ Common Materials: 10 Glow Cash each
├─ Uncommon Materials: 100 Glow Cash each
├─ Rare Essence: 500 Glow Cash each

NPC Buy Prices (Players sell to NPCs):
├─ Common Materials: 5 Glow Cash each
├─ Uncommon Materials: 50 Glow Cash each
├─ Rare Essence: 250 Glow Cash each

Why NPC Anchoring:
├─ Price ceiling (players won't pay more than NPC)
├─ Price floor (players won't sell for less than NPC)
├─ Market stability (prevents extreme swings)
└─ Fallback option (always can buy/sell)
```

**Market vs NPC Price Dynamics:**

```
Typical Market Prices vs NPC Prices:

Item: Rare Essence
├─ NPC Sell Price: 500 Glow Cash (ceiling)
├─ Market Price: 100-200 Glow Cash (player-driven)
├─ NPC Buy Price: 250 Glow Cash (floor)

If Market Price > 500: Players buy from NPCs instead
If Market Price < 250: Players sell to NPCs instead
Result: Market naturally stabilizes between 250-500
```

---

### **Currency Sink Effectiveness Monitoring**

**Economic Health Dashboard (Dev-Side):**

```
Real-time monitoring of economy health:

Currency Velocity:
├─ Glow Cash spent per day: 150M
├─ Glow Cash earned per day: 180M
├─ Net inflation: +30M/day (+20% weekly)
└─ Status: âš ï¸ Warning (approaching inflation threshold)

Currency Sinks (Last 7 Days):
├─ Building upgrades: 420M (35% of total spending)
├─ Pet training: 300M (25%)
├─ Market fees: 180M (15%)
├─ Crafting: 240M (20%)
└─ Other: 60M (5%)

If Inflation Detected:
├─ Increase sink costs (building upgrades +10%)
├─ Add limited-time sinks (event shop with high prices)
├─ Reduce faucet yields (expedition rewards -5%)
└─ Monitor for 2 weeks, adjust as needed
```

---

# PART 9: ECONOMIC BALANCE & SINKS

## 💧 RESOURCE FAUCETS (INCOME SOURCES)

### **Glow Cash Faucets (Total Weekly Income)**

| Source | % of Income | Casual Player/Week | Regular Player/Week | Hardcore Player/Week |
|--------|-------------|-------------------|-------------------|---------------------|
| Expeditions | 60% | 60,000-100,000 | 150,000-300,000 | 400,000-800,000 |
| Daily Quests | 15% | 15,000-25,000 | 15,000-25,000 | 15,000-25,000 |
| Weekly Quests | 10% | 55,000-90,000 | 55,000-90,000 | 55,000-90,000 |
| Market Sales | 10% | 5,000-15,000 | 50,000-150,000 | 200,000-500,000 |
| Passive Income | 5% | 10,000-30,000 | 50,000-100,000 | 200,000-400,000 |
| **Total/Week** | **100%** | **145,000-260,000** | **320,000-665,000** | **870,000-1,815,000** |

**Monthly Income:**
- Casual: 580,000-1,040,000 Glow Cash/month
- Regular: 1,280,000-2,660,000 Glow Cash/month
- Hardcore: 3,480,000-7,260,000 Glow Cash/month

---

### **Material Faucets (Total Weekly Income)**

| Source | Common Mats/Week | Rare Mats/Week | Epic Mats/Week | Legendary Mats/Week |
|--------|-----------------|----------------|----------------|-------------------|
| Expeditions (Active) | 1,500-3,000 | 200-500 | 30-80 | 5-15 |
| Mining Nodes | 500-1,000 | 50-150 | 10-30 | 2-5 |
| Dungeons | 200-500 | 100-300 | 50-150 | 20-60 |
| Pet Decomposition | 1,000-2,000 | 300-600 | 100-250 | 30-80 |
| **Total/Week** | **3,200-6,500** | **650-1,550** | **190-510** | **57-160** |

---

### **Special Currency Faucets (Total Weekly Income)**

| Source | Rare Essence/Week | Epic Essence/Week | Legendary Core/Week |
|--------|------------------|------------------|-------------------|
| Dungeons | 200-500 | 50-150 | 10-30 |
| Pet Decomposition | 500-1,500 | 100-400 | 20-80 |
| Events | 50-200 | 10-50 | 2-10 |
| **Total/Week** | **750-2,200** | **160-600** | **32-120** |

---

## 🚰 RESOURCE SINKS (EXPENSE DRAINS)

### **Glow Cash Sinks (Total Weekly Spending)**

| Sink Category | % of Spending | Casual Player/Week | Regular Player/Week | Hardcore Player/Week |
|--------------|---------------|-------------------|-------------------|---------------------|
| Building Upgrades | 40% | 50,000-100,000 | 150,000-300,000 | 400,000-800,000 |
| Pet Training/Breeding | 25% | 30,000-60,000 | 90,000-180,000 | 250,000-500,000 |
| Crafting | 20% | 25,000-50,000 | 75,000-150,000 | 200,000-400,000 |
| Market Fees | 5% | 5,000-10,000 | 20,000-40,000 | 50,000-100,000 |
| Fast Travel | 3% | 3,000-6,000 | 10,000-20,000 | 30,000-60,000 |
| Miscellaneous | 7% | 7,000-14,000 | 25,000-50,000 | 70,000-140,000 |
| **Total/Week** | **100%** | **120,000-240,000** | **370,000-740,000** | **1,000,000-2,000,000** |

**Net Glow Cash Accumulation:**

```
Casual Player:
Income: 145,000-260,000/week
Spending: 120,000-240,000/week
Net: +25,000 to +20,000/week (positive accumulation)

Regular Player:
Income: 320,000-665,000/week
Spending: 370,000-740,000/week
Net: -50,000 to -75,000/week (slight deficit during heavy building)

Hardcore Player:
Income: 870,000-1,815,000/week
Spending: 1,000,000-2,000,000/week
Net: -130,000 to -185,000/week (deficit during max progression)

Why Deficits Are OK:
├─ Players periodically enter "building phases" (heavy spending)
├─ Followed by "farming phases" (heavy income, low spending)
├─ Net zero over time (balanced economy)
└─ Encourages strategic resource management
```

---

### **Material Sinks (Total Weekly Consumption)**

| Sink Category | Common Mats/Week | Rare Mats/Week | Epic Mats/Week | Legendary Mats/Week |
|--------------|-----------------|----------------|----------------|-------------------|
| Building Upgrades | 1,000-3,000 | 200-600 | 50-150 | 10-30 |
| Gear Crafting | 500-1,500 | 100-300 | 20-60 | 5-15 |
| Consumable Crafting | 200-600 | 50-150 | 10-30 | 2-8 |
| Pet Breeding | 100-300 | 50-150 | 20-60 | 5-15 |
| **Total/Week** | **1,800-5,400** | **400-1,200** | **100-300** | **22-68** |

**Net Material Balance:**

```
Common Materials:
Faucets: 3,200-6,500/week
Sinks: 1,800-5,400/week
Net: +1,400 to +1,100/week (surplus accumulation)

Rare Materials:
Faucets: 650-1,550/week
Sinks: 400-1,200/week
Net: +250 to +350/week (moderate surplus)

Epic Materials:
Faucets: 190-510/week
Sinks: 100-300/week
Net: +90 to +210/week (tight balance)

Legendary Materials:
Faucets: 57-160/week
Sinks: 22-68/week
Net: +35 to +92/week (always bottleneck)

Why This Balance:
├─ Common materials abundant (always available)
├─ Rare materials moderate (some farming needed)
├─ Epic materials tight (strategic farming required)
└─ Legendary materials scarce (major progression gate)
```

---

## 🛡️ INFLATION CONTROL SYSTEMS

### **Primary Inflation Controls**

**1. Exponential Cost Scaling**

```
Building upgrade costs increase exponentially:

Weaponsmith:
├─ Level 1→2: 5,000 Glow Cash
├─ Level 2→3: 7,500 Glow Cash
├─ Level 5→6: 28,000 Glow Cash
└─ Level 9→10: 180,000 Glow Cash

Why Exponential:
├─ Early game: Affordable (engagement)
├─ Mid game: Moderate (strategic choices)
├─ Late game: Expensive (major sink)
└─ Prevents runaway wealth accumulation
```

**2. Permanent Currency Removal Sinks**

```
Currency Removed Per Week (Average Player):

Market Fees: 20,000-40,000 Glow Cash (5-10% of sales)
Building Upgrades: 150,000-300,000 Glow Cash (construction costs)
Crafting Costs: 75,000-150,000 Glow Cash (material conversion)
Pet Training: 90,000-180,000 Glow Cash (leveling costs)
Fast Travel: 10,000-20,000 Glow Cash (convenience)

Total Removed: 345,000-690,000 Glow Cash/week

Why Permanent Removal:
├─ Reduces total Glow Cash in economy
├─ Maintains currency value over time
├─ Prevents hyperinflation
└─ Balances faucets (income) vs sinks (removal)
```

**3. Limited-Time High-Value Sinks**

```
Seasonal/Event Currency Sinks:

Event Shop Exclusive:
├─ Legendary Cosmetic: 3,500 Event Tokens (≈175,000 Glow Cash equivalent)
├─ Mythic Pet: 5,000 Event Tokens (≈250,000 Glow Cash equivalent)
└─ Profile Frame: 4,000 Event Tokens (≈200,000 Glow Cash equivalent)

Why Limited-Time:
├─ Creates urgency (spend now or miss out)
├─ Drains hoarded currency
├─ Prevents infinite accumulation
└─ Adds variety to economy
```

---

### **Inflation Monitoring & Response**

**Economic Health Indicators:**

```
Daily Monitoring Metrics:

Currency Velocity:
├─ Target: 70-80% of earned Glow Cash spent within 7 days
├─ Current: 75% (healthy)
└─ Action: None needed

Glow Cash Supply Growth:
├─ Target: +15% per month (exponential growth is expected)
├─ Current: +22% per month (slightly high)
└─ Action: Increase sink costs by 5% next patch

Average Player Wealth:
├─ Target: 500k-1M Glow Cash at Month 1
├─ Current: 1.2M Glow Cash at Month 1 (high)
└─ Action: Reduce expedition rewards by 5%

Market Price Inflation:
├─ Target: +10% per quarter (gradual increase)
├─ Current: +15% per quarter (moderate inflation)
└─ Action: Monitor for another month, adjust if continues
```

**Response Actions (If Inflation Detected):**

```
If Inflation > Target:

Immediate Actions (Hot Fix):
├─ Increase building upgrade costs +10%
├─ Increase market fees 5% → 6%
├─ Add limited-time high-value sinks (event shop)

Short-Term Actions (Next Patch):
├─ Reduce expedition Glow Cash rewards -5 to -10%
├─ Increase crafting costs +15%
├─ Add new endgame building (massive sink)

Long-Term Actions (Next Season):
├─ Prestige system (resets player levels, adds sinks)
├─ Guild wars (currency sinks for competitive guilds)
├─ New endgame content (new progression sinks)
```

---

## 📊 LONG-TERM ECONOMIC HEALTH

### **Economic Lifecycle (Year 1)**

```
MONTH 1: RAPID GROWTH
├─ New players joining daily
├─ High currency velocity (spending to progress)
├─ Low inflation (limited wealth accumulation)
└─ Status: Healthy

MONTH 3: STABILIZATION
├─ Player base stabilizes
├─ Mid-game players accumulating wealth
├─ Moderate inflation (5-10% per month)
└─ Status: Healthy

MONTH 6: WEALTH CONCENTRATION
├─ Veteran players very wealthy
├─ Endgame sinks needed
├─ Higher inflation (10-15% per month)
└─ Status: Requires monitoring

MONTH 12: MATURE ECONOMY
├─ Established trading economy
├─ Market self-regulating
├─ Controlled inflation (10% per quarter)
└─ Status: Stable with active management
```

---

### **Long-Term Sustainability Strategies**

**1. Prestige Systems (Currency Resets)**
- Players can prestige (reset level) for exclusive rewards
- Encourages spending accumulated wealth before reset
- Creates cyclical economy (boom-bust cycles)

**2. Seasonal Resets (Leaderboards)**
- Every 3 months, leaderboards reset
- Encourages competitive spending (push for top rank)
- Drains hoarded currency

**3. Guild Wars (Group Currency Sinks)**
- Guilds compete in wars, requiring massive resource investment
- Entry fees, equipment costs, consumable usage
- High-level currency sink for established players

**4. New Content Patches (Expansion Sinks)**
- New buildings, pets, biomes require new investments
- Opens new progression paths (more sinks)
- Prevents economic stagnation

---

# PART 10: PROGRESSION & RETENTION

## 📈 CURRENCY ACCUMULATION CURVES

### **Expected Glow Cash Net Worth Over Time**

```
GLOW CASH NET WORTH PROGRESSION (Logarithmic Scale):

1B   ┤
     │
     │
100M ┤                                              ****
     │                                          ****
     │                                      ****
 10M ┤                                  ****
     │                              ****
     │                          ****
  1M ┤                      ****
     │                  ****
     │              ****
100K ┤          ****
     │      ****
     │  ****
 10K ┤**
     └─────────────────────────────────────────────────────
     Week1  Month1  Month3  Month6  Month12  Month24

Data Points:
├─ Week 1: 50K-100K Glow Cash
├─ Month 1: 500K-1M Glow Cash
├─ Month 3: 2M-5M Glow Cash
├─ Month 6: 10M-25M Glow Cash
├─ Month 12: 50M-200M Glow Cash
└─ Month 24: 200M-1B+ Glow Cash (top players)
```

**Key Observations:**
- Exponential growth is intentional and healthy
- Early game is tight (strategic choices)
- Late game is abundant (experimentation enabled)
- Never plateaus (infinite progression)

---

### **Hype Crystal Accumulation Curve**

```
HYPE CRYSTAL ACCUMULATION OVER TIME:

5,000 ┤
      │                                              ****
      │                                          ****
2,500 ┤                                      ****
      │                                  ****
      │                              ****
1,000 ┤                          ****
      │                      ****
      │                  ****
  500 ┤              ****
      │          ****
      │      ****
  100 ┤  ****
      └─────────────────────────────────────────────────────
      Week1  Month1  Month3  Month6  Month12  Month24

Data Points:
├─ Week 1: 5-15 Hype Crystals
├─ Month 1: 40-80 Hype Crystals
├─ Month 3: 150-300 Hype Crystals
├─ Month 6: 500-1,000 Hype Crystals
├─ Month 12: 1,500-3,000 Hype Crystals
└─ Month 24: 4,000-8,000 Hype Crystals
```

**Key Observations:**
- Much slower accumulation than Glow Cash
- Rare drops maintain prestige value
- Major purchases take months of saving
- Never becomes trivial to earn

---

### **Encore Token Accumulation Curve**

```
ENCORE TOKEN ACCUMULATION OVER TIME:

1,500 ┤
      │                                              ****
      │                                          ****
  750 ┤                                      ****
      │                                  ****
      │                              ****
  400 ┤                          ****
      │                      ****
      │                  ****
  150 ┤              ****
      │          ****
      │      **
   50 ┤  ***
      └─────────────────────────────────────────────────────
      Month1  Month3  Month6  Month12  Month18  Month24

Data Points:
├─ Month 1: 0-30 Encore Tokens (achievements only)
├─ Month 3: 40-80 Encore Tokens (1-2 prestiges)
├─ Month 6: 100-200 Encore Tokens (3-5 prestiges)
├─ Month 12: 300-600 Encore Tokens (8-12 prestiges)
├─ Month 18: 500-1,000 Encore Tokens (15-20 prestiges)
└─ Month 24: 800-1,500 Encore Tokens (25-35 prestiges)
```

**Key Observations:**
- Extremely rare currency (slowest accumulation)
- Prestige system gates earning (requires Level 100)
- Major purchases take 6-12 months of saving
- True long-term achievement currency

---

## 🎯 PLAYER PROGRESSION MILESTONES

### **Economic Milestones by Time Played**

**Week 1 Milestones:**
```
Economic Status: Struggling (Resource-Starved)

Currency:
├─ 50,000-100,000 Glow Cash net worth
├─ 5-15 Hype Crystals
└─ 0 Encore Tokens

Spending Power:
├─ Can upgrade 3-5 buildings to Level 3
├─ Can train 2-3 pets to Level 20
├─ Can craft Common/Uncommon gear
└─ Cannot afford: Epic+ items, building Level 5+

Player Feeling:
├─ "I need to make strategic choices"
├─ "Every purchase matters"
└─ "Excited about first major upgrades"
```

**Month 1 Milestones:**
```
Economic Status: Emerging (Strategic Management)

Currency:
├─ 500,000-1,000,000 Glow Cash net worth
├─ 40-80 Hype Crystals
└─ 0-30 Encore Tokens (first achievements)

Spending Power:
├─ Can upgrade all buildings to Level 5
├─ Can train 5-10 pets to Level 50
├─ Can craft Rare gear
└─ Cannot afford: Legendary gear, building Level 10

Player Feeling:
├─ "I'm making meaningful progress"
├─ "I can afford some experimentation"
└─ "Working toward first major goals"
```

**Month 3 Milestones:**
```
Economic Status: Comfortable (Resource-Stable)

Currency:
├─ 2,000,000-5,000,000 Glow Cash net worth
├─ 150-300 Hype Crystals
└─ 40-80 Encore Tokens (1-2 prestiges)

Spending Power:
├─ Can upgrade 10-15 buildings to Level 7
├─ Can train 20+ pets to Level 75
├─ Can craft Epic gear
├─ Can afford: First Hype Crystal exclusive items
└─ Cannot afford: All buildings Level 10, Mythic gear

Player Feeling:
├─ "I have financial security now"
├─ "I can pursue multiple goals simultaneously"
└─ "Working toward endgame content"
```

**Month 6 Milestones:**
```
Economic Status: Wealthy (Resource-Abundant)

Currency:
├─ 10,000,000-25,000,000 Glow Cash net worth
├─ 500-1,000 Hype Crystals
└─ 100-200 Encore Tokens (3-5 prestiges)

Spending Power:
├─ Can upgrade all buildings to Level 10
├─ Can train unlimited pets to Level 100
├─ Can craft Legendary gear
├─ Can afford: Most Hype Crystal items
├─ Can afford: Some Prestige shop items
└─ Cannot afford: Everything in Prestige shop

Player Feeling:
├─ "I'm a veteran player"
├─ "I can experiment freely"
├─ "Working toward completion and prestige"
└─ "Need new endgame sinks"
```

**Month 12 Milestones:**
```
Economic Status: Elite (Resource-Saturated)

Currency:
├─ 50,000,000-200,000,000+ Glow Cash net worth
├─ 1,500-3,000 Hype Crystals
└─ 300-600 Encore Tokens (8-12 prestiges)

Spending Power:
├─ All buildings Level 10 (multiple times via prestige)
├─ 50+ pets at max level with perfect IVs
├─ Full Legendary/Mythic gear collection
├─ Most Hype Crystal exclusives owned
├─ Half of Prestige shop purchased
└─ Cannot afford: Limited seasonal exclusives (need more time)

Player Feeling:
├─ "I'm an endgame whale"
├─ "I need new content and goals"
├─ "Collecting seasonal/limited items"
└─ "Competing on leaderboards"
```

---

## 🎮 ECONOMIC RETENTION STRATEGIES

### **Daily Engagement Hooks**

**Daily Currency Opportunities:**
```
Every Day, Players Can Earn:

Daily Quests:
├─ 5 quests × 3,000 average = 15,000 Glow Cash
├─ Time: 1-2 hours
└─ Retention Hook: "Log in daily for rewards"

Daily Dungeon Bonus:
├─ First dungeon: +50% rewards
├─ Additional: 3-5 Hype Crystals
└─ Retention Hook: "Don't miss first dungeon bonus"

Passive Income Collection:
├─ Energy Generator: 10,000-50,000 Glow Cash (24h cap)
├─ Time: 2 minutes
└─ Retention Hook: "Collect passive income daily"

Daily Login Streak:
├─ Day 7: 5 Hype Crystals
├─ Day 14: 10 Hype Crystals + Rare Egg
└─ Retention Hook: "Don't break your streak!"

Total Daily Value: 30,000-75,000 Glow Cash + bonuses
Time Investment: 1.5-2.5 hours
```

---

### **Weekly Engagement Hooks**

**Weekly Currency Opportunities:**
```
Every Week, Players Can Earn:

Weekly Quests:
├─ 3 quests × 25,000 average = 75,000 Glow Cash
├─ Additional: 15 Hype Crystals
└─ Retention Hook: "Complete all 3 for best rewards"

Weekly Boss Dungeon:
├─ Guaranteed: 20-30 Hype Crystals + 100 Legendary Core
├─ Time: 1-2 hours (finding group + completion)
└─ Retention Hook: "Don't miss weekly boss!"

Market Flipping:
├─ Buy low, sell high: 50,000-200,000 Glow Cash profit/week
├─ Time: 30 minutes browsing/trading
└─ Retention Hook: "Check market for deals"

Total Weekly Value: 150,000-300,000 Glow Cash + 30-45 Hype Crystals
Time Investment: 15-25 hours/week
```

---

### **Monthly Engagement Hooks**

**Monthly Currency Opportunities:**
```
Every Month, Players Can Earn:

Monthly Achievement:
├─ Complete 30 expeditions: 50,000 Glow Cash + 25 Hype Crystals
└─ Retention Hook: "Work toward monthly goal"

Seasonal Event (if active):
├─ Event currency: 6,000-15,000 Event Tokens
├─ Converted to: 300,000-750,000 Glow Cash equivalent
└─ Retention Hook: "Limited-time exclusive rewards"

Leaderboard Reset:
├─ Top 100: 10-50 Encore Tokens
├─ Top 500: 5 Encore Tokens
└─ Retention Hook: "Push for leaderboard before reset"

Total Monthly Value: 500,000-1,000,000+ Glow Cash equivalent
```

---

## 🔒 ANTI-EXPLOIT MEASURES

### **Currency Exploit Prevention**

**Server-Side Validation:**
```
All currency transactions validated server-side:

Exploit Example:
├─ Client: "I earned 10,000,000 Glow Cash from one Common pet"
├─ Server Check: Common pets drop 10-50 Glow Cash maximum
├─ Server Response: REJECT, flag account, investigate
└─ Result: Exploit prevented, cheater flagged

All Currency Changes Logged:
├─ Source: What granted currency? (expedition, quest, market, etc.)
├─ Amount: How much? (validated against possible ranges)
├─ Timestamp: When? (rate limit checks)
└─ Player ID: Who? (track suspicious patterns)
```

**Rate Limits:**
```
Currency Earning Rate Limits:

Glow Cash:
├─ Max per hour: 500,000 (even for top players)
├─ If exceeded: Flag account, investigate
└─ Prevents: Speed hacks, automated farming

Hype Crystals:
├─ Max per hour: 100 (extremely generous)
├─ If exceeded: Instant flag, possible ban
└─ Prevents: Drop rate manipulation

Trading:
├─ Max Glow Cash transferred per day: 10,000,000
├─ If exceeded: Account locked, RMT investigation
└─ Prevents: Real-money trading (RMT)
```

---

### **Market Manipulation Prevention**

**Price Fixing Detection:**
```
Market Monitoring Systems:

Suspicious Pattern #1: Wash Trading
├─ Player A lists item for 1,000,000 Glow Cash
├─ Player B (alt account) buys it immediately
├─ Player A lists again, Player B buys again (repeat 10x)
├─ Detection: Same two accounts trading same item type repeatedly
└─ Response: Both accounts flagged, investigated

Suspicious Pattern #2: Market Cornering
├─ Player A buys all 500 listings of "Rare Essence"
├─ Player A lists all 500 at 10x normal price
├─ Detection: Single player owns >80% of market supply
└─ Response: Account flagged, purchase limits enforced

Suspicious Pattern #3: Price Collusion
├─ 10 players simultaneously list same item at 5x normal price
├─ Detection: Coordinated price change (guild conspiracy)
└─ Response: Guild investigated, potential ban
```

---

### **Duplication Exploit Prevention**

**Unique Item IDs:**
```
Every item has a unique ID:

Item Creation:
├─ Server generates: ItemID = UUID4 (unique identifier)
├─ Example: "RareEssence_ab12cd34-ef56-gh78-ij90-kl12mn34op56"
└─ Duplicate IDs are impossible (UUID collision rate: 1 in 10^36)

Item Duplication Attempt:
├─ Hacker: "Clone item with ID ab12cd34..."
├─ Server Check: Item ID already exists in database
├─ Server Response: REJECT, cannot create duplicate ID
└─ Result: Duplication exploit prevented

Item Transfer Logs:
├─ Every item movement logged:
├─ "2026-01-02 14:35:22 - ItemID ab12cd34 transferred from Player A to Player B"
├─ Audit trail for investigating exploits
└─ Can rollback economy if needed
```

---

### **Real-Money Trading (RMT) Prevention**

**Transaction Monitoring:**
```
RMT Detection Patterns:

Pattern #1: Lopsided Trade
├─ Player A trades 100,000,000 Glow Cash for 1 Common Material
├─ Detection: Trade value ratio >1,000:1
├─ Response: Trade flagged, investigate both accounts
└─ Likely RMT (selling Glow Cash for real money)

Pattern #2: New Account Wealth Transfer
├─ Level 5 player receives 50,000,000 Glow Cash from Level 100 player
├─ Detection: New account (<7 days) receiving massive wealth
├─ Response: Both accounts flagged, likely RMT
└─ Action: Freeze transferred currency, investigate

Pattern #3: Repeated Large Transfers
├─ Player A sends 10,000,000 Glow Cash to 10 different players (100M total)
├─ Detection: Single player sending massive amounts to many recipients
├─ Response: Account locked, RMT investigation
└─ Action: If confirmed RMT, permanent ban + currency rollback
```

**Purchase Limit Enforcement:**
```
Daily Purchase Limits:

Glow Cash Trading:
├─ Max receive: 10,000,000 Glow Cash/day
├─ Max send: 10,000,000 Glow Cash/day
└─ Prevents: Large-scale RMT operations

Market Purchases:
├─ Max spend: 50,000,000 Glow Cash/day
├─ Max buy of same item: 100 units/day
└─ Prevents: Money laundering via market
```

---

# 🎊 CONCLUSION

## 📝 ECONOMY DESIGN SUMMARY

**This document has covered:**

✅ **4 Currency Types:**
- Glow Cash (primary soft currency)
- Hype Crystals (rare soft currency)
- Encore Tokens (prestige currency)
- Star Shards (premium currency)

✅ **Complete Earning & Spending Systems:**
- Detailed earning rates for all activities
- Comprehensive spending sinks
- Progression curves and accumulation

✅ **Materials System:**
- 8 elemental material tiers (Common → Legendary)
- Universal resources (Stone, Iron, Crystal)
- Special currencies (Essence & Cores)

✅ **Event Currency:**
- Seasonal event tokens
- Event shop rewards
- Limited-time systems

✅ **Trading Economy:**
- Player-to-player trading
- Auction house mechanics
- Market fees and regulations

✅ **Economic Balance:**
- Faucets (income sources)
- Sinks (expense drains)
- Inflation controls
- Long-term sustainability

✅ **Progression & Retention:**
- Currency accumulation curves
- Player milestones
- Engagement hooks
- Anti-exploit measures

---

## 🎯 DESIGN GOALS ACHIEVED

**1. Multiple Currency Tiers:** ✅
- Each currency serves distinct purpose
- Clear visual/mechanical distinction
- No redundancy or confusion

**2. Ethical Monetization:** ✅
- Premium currency (Star Shards) = cosmetics + convenience only
- 100% content accessible to free players
- No pay-to-win mechanics
- Transparent pricing

**3. Long-Term Sustainability:** ✅
- Strong currency sinks prevent inflation
- Exponential cost scaling for endgame
- Prestige system creates cyclical economy
- Regular economic health monitoring

**4. Rewarding Skill:** ✅
- Perfect combat = bonus multipliers
- PvPvE risk = higher rewards
- Leaderboards reward competitive play
- Efficiency optimization rewarded

**5. Social Economy:** ✅
- Player-driven market pricing
- Auction house with anti-manipulation
- Trading creates engagement
- Market fees act as sinks

---

## 🚀 IMPLEMENTATION PRIORITIES

### **Phase 1: Core Economy (MVP)**
1. Glow Cash system (earning, spending, UI)
2. Basic material drops (Common → Epic)
3. NPC vendors (buy/sell fallback)
4. Building upgrade costs
5. Pet training/breeding costs

### **Phase 2: Advanced Systems**
6. Hype Crystal drops and shop
7. Market/Auction House
8. Special currencies (Essence/Cores)
9. Event currency framework
10. Economic monitoring dashboard

### **Phase 3: Prestige & Endgame**
11. Prestige system and Encore Tokens
12. Prestige shop (titles, frames, badges)
13. Seasonal leaderboards
14. Guild wars (group sinks)

### **Phase 4: Polish & Balance**
15. Anti-exploit systems
16. Market analytics for players
17. Dynamic economic adjustments
18. Long-term sustainability systems

---

## 📊 SUCCESS METRICS

**Economic Health KPIs:**

| Metric | Target | Purpose |
|--------|--------|---------|
| Currency Velocity | 70-80% spent/week | Engaged economy |
| Sink Effectiveness | 60% permanently removed | Inflation control |
| Premium Conversion | 15-25% make purchase | Revenue sustainability |
| Trading Volume | 20-30% use market weekly | Active economy |
| ARPU | $8-12/year | Ethical monetization |

---

## 💬 FINAL NOTES

**This economy is designed to:**
- Reward time investment without exploitation
- Create meaningful choices through scarcity
- Maintain long-term value through strong sinks
- Enable player-driven markets with safeguards
- Provide infinite progression without pay-to-win

**The economy is a living system** that requires:
- Regular monitoring and adjustment
- Community feedback integration
- Seasonal content updates
- Anti-exploit vigilance
- Ethical monetization standards

**May your economy be prosperous, balanced, and exploiter-free!** 🎉

---

**End of Economy & Currency Design Document**
**Version 1.0 | Last Updated: January 2, 2026**
