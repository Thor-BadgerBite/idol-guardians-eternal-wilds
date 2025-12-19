# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT 
**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 1 of 10 (Core Philosophy & Foundation)  
**Last Updated:** December 18, 2025

---

## 📋 TABLE OF CONTENTS (COMPLETE DOCUMENT)

### **PART 1: CORE PHILOSOPHY & FOUNDATION** *(This Document)*
1. Design Philosophy
2. Base Instance Model
3. Core Engagement Loops
4. Player Progression Journey
5. Base Layout & Plot System

### **PART 2: BUILDING OVERVIEW & PHASES**
6. Complete Building Roster
7. Phase 1 Buildings (MVP)
8. Phase 2 Buildings (Advanced)
9. Phase 3 Buildings (Endgame)
10. Phase 4 Buildings (Utility/Premium)

### **PART 3: CORE PRODUCTION BUILDINGS**
11. Weaponsmith (Detailed)
12. Armorsmith (Detailed)
13. Workshop (Detailed)
14. Refinery (Detailed)

### **PART 4: PET MANAGEMENT BUILDINGS**
15. Training Station (Detailed)
16. Breeding Station (Detailed)
17. Sanctuary (Detailed)
18. Pet Daycare (Detailed)

### **PART 5: PROGRESSION BUILDINGS**
19. Laboratory (Detailed)
20. Expedition Hub (Detailed)
21. Warehouse (Detailed)
22. Mailbox/Notice Board (Detailed)

### **PART 6: SOCIAL & ECONOMY BUILDINGS**
23. Market/Trading Post (Detailed)
24. Guild Hall (Detailed)
25. Trophy Hall (Detailed)
26. Guild Island System

### **PART 7: PREMIUM & UTILITY BUILDINGS**
27. Cosmetic Hub (Detailed)
28. Energy Generator (Detailed)
29. Automation Station (Detailed)
30. Fast Travel Hub (Detailed)
31. Event Billboard (Detailed)

### **PART 8: BUILDING MECHANICS**
32. Upgrade System
33. Construction System
34. Demolition & Rebuilding
35. Building Unlock Gates
36. Multi-Benefit Upgrade Philosophy

### **PART 9: BASE CUSTOMIZATION & AESTHETICS**
37. Plot Customization System
38. Base Theme Evolution
39. Decorative Items
40. Social Features & Visiting
41. Screenshot & Share Features

### **PART 10: MONETIZATION & BALANCE**
42. Ethical Monetization Strategy
43. Premium vs Free Comparison
44. Balance Tables & Formulas
45. Technical Implementation Guidelines
46. Anti-Exploit Measures

---

## 🎯 PART 1: DESIGN PHILOSOPHY

### **The Core Vision**

The Base Building System is the **heart of player retention** in Idol Guardians: Eternal Wilds. While expeditions provide excitement and discovery, the base is where players invest their time, resources, and creativity to build a personalized hub that reflects their journey and achievements.

**The base is NOT:**
- ❌ A simple menu system disguised as buildings
- ❌ A boring waiting room between expeditions
- ❌ A pay-to-win monetization trap
- ❌ A complex city-builder that overwhelms players

**The base IS:**
- ✅ A meaningful progression system with tangible benefits
- ✅ A social showcase of your achievements and pet collection
- ✅ A strategic resource management puzzle
- ✅ A personalized space that evolves with your journey
- ✅ A daily ritual that creates routine and habit

---

## 🏛️ DESIGN PILLARS

### **Pillar 1: Purposeful Progression**

Every building serves a **clear, essential function** in the core gameplay loop:

**Production Buildings** → Enable crafting and upgrades
**Pet Buildings** → Manage your companion roster  
**Progression Buildings** → Unlock new content and research
**Social Buildings** → Connect with other players
**Utility Buildings** → Quality-of-life improvements

There are NO "decoration-only" buildings in the core 20. Every structure matters.

---

### **Pillar 2: Strategic Choices**

Players face **meaningful decisions** at every level:

**Early Game (Levels 1-25):**
- "Do I upgrade my Weaponsmith or unlock Training Station first?"
- "Do I craft armor for defense or weapons for faster clears?"

**Mid Game (Levels 26-50):**
- "Do I invest in Laboratory research or expand my Warehouse?"
- "Do I focus on breeding perfect pets or training my current roster?"

**Late Game (Levels 51+):**
- "Do I build the Energy Generator for passive income or Guild Hall for social features?"
- "Do I buy premium building slots or premium cosmetics?"

**Resource scarcity** and **building slot limits** ensure choices matter.

---

### **Pillar 3: Rewarding Investment**

Time and resources invested in your base should feel **impactful**:

**Immediate Rewards:**
- Finish crafting a weapon → Expedition becomes easier
- Upgrade Training Station → Level pets 20% faster
- Unlock Sanctuary → Display your rare pet collection

**Long-Term Rewards:**
- Level 10 Laboratory → Unlock account-wide 15% capture rate bonus
- Fully upgraded base → 50% faster progression than fresh players
- Aesthetic tier evolution → Visually stunning citadel that impresses visitors

**Social Rewards:**
- Friends visit your base → See your achievements
- Guild Hall upgrades → Entire guild benefits
- Trophy Hall → Permanent record of accomplishments

---

### **Pillar 4: Accessible Complexity**

The base system must be:

**Simple to Understand:**
- New players unlock buildings linearly (one at a time)
- Each building has a clear primary function
- UI tooltips explain every feature

**Deep to Master:**
- Advanced players optimize resource allocation
- Multi-building synergies create efficiency gains
- Research tree unlocks create long-term planning

**Mobile-Friendly:**
- Pre-defined plot system (no complex placement)
- One-tap interactions (upgrade, craft, collect)
- Fast travel between buildings (no tedious walking)

---

### **Pillar 5: Fair Monetization**

Premium features must **respect free players** while offering value to paying players:

**What Premium CANNOT Buy:**
- ❌ Exclusive powerful weapons/armor
- ❌ Better crafting success rates
- ❌ Faster research breakthroughs
- ❌ Access to unique building functions

**What Premium CAN Buy:**
- ✅ Cosmetic building skins (Gothic forge, crystal laboratory)
- ✅ Extra building plots (12 free → 16 max with purchase)
- ✅ Instant completion tokens (skip waiting, not power)
- ✅ Storage expansion (convenience, not necessity)
- ✅ Decorative items (visual flair, zero gameplay impact)

**Free players can achieve 100% gameplay parity.** Premium is cosmetic and convenience only.

---

## 🏠 BASE INSTANCE MODEL

### **How Base Persistence Works**

**Instanced Personal Base with Social Hub Connection**

Your base is a **private, persistent instance** that exists independently of the game world:

```
GAME WORLD STRUCTURE:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🌍 PROCEDURAL EXPEDITION MAPS
   ↓ (Extract/Complete)
   
🏛️ CENTRAL SOCIAL HUB (Shared Instance)
   ├─ 40-60 players visible
   ├─ General chat
   ├─ Event boards
   ├─ Portal to personal bases
   └─ Guild recruitment area
   
   ↓ (Enter Portal)
   
🏠 YOUR PERSONAL BASE (Private Instance)
   ├─ Only you + invited friends can enter
   ├─ Persistent between sessions
   ├─ Buildings remain even when offline
   └─ Safe from griefing/raiding

   ↓ (Invite Friend)
   
👥 FRIEND'S BASE (Read-Only Visit)
   ├─ View their buildings
   ├─ See their pet collection
   ├─ Admire their trophies
   └─ CANNOT steal, damage, or interact
```

---

### **Why Instanced Bases?**

**Advantages:**
- ✅ **100% grief-proof** - No raiding, stealing, or vandalism
- ✅ **No server lag** - Your base doesn't affect others' performance
- ✅ **Total creative freedom** - Customize without worrying about neighbors
- ✅ **Secure progression** - Offline players can't lose buildings/resources
- ✅ **Scalable** - Can support millions of players without world size limits

**Trade-offs:**
- ⚠️ Less "living world" feeling (not persistent like Rust/ARK)
- ⚠️ No spontaneous player encounters at base
- ⚠️ Guild interaction happens in separate Guild Island

**But these trade-offs are worth it for a mobile-first, family-friendly game.**

---

### **Social Hub Integration**

**The Central Hub** serves as the community gathering point:

**What Happens in the Hub:**
- Players socialize between expeditions
- Guild recruitment happens here
- Event announcements are displayed
- Leaderboards are visible (top players/guilds)
- NPC vendors offer basic supplies
- Portal access to personal bases

**What DOESN'T Happen in the Hub:**
- No crafting (that's in your base)
- No pet management (that's in your base)
- No permanent structures (just social space)

**Visual Design:**
- Large open plaza with fantasy architecture
- Portals arranged in a circle (each leads to a player base)
- Event-themed decorations change seasonally
- Guild banners displayed for top-ranked guilds

---

### **Visiting Friends' Bases**

**How It Works:**

1. **Invitation System:**
   - Friend sends base visit invite (via menu or chat)
   - You accept and teleport to their base entrance
   - You appear as a visitor avatar (different visual effect)

2. **Read-Only Mode:**
   - You CAN see all buildings, pets, decorations, trophies
   - You CAN walk around and explore freely
   - You CANNOT open crafting menus, steal items, or damage anything
   - You CANNOT interact with their pets (just observe)

3. **Social Features:**
   - Leave kudos/likes on their base (reputation system)
   - Take screenshots to share on social media
   - Send compliments via quick-chat ("Awesome base!", "Love your Sanctuary!")
   - View their Trophy Hall achievements

4. **Privacy Controls:**
   - Base owner can toggle "Allow Visitors" on/off
   - Can set visit permissions (Friends Only / Guild Only / Anyone)
   - Can kick visitors at any time
   - Can hide specific buildings from visitors (e.g., hide Workshop if you're testing new recipes)

**Why Read-Only?**
- Prevents griefing (can't mess up their layout)
- Prevents exploits (can't steal resources)
- Keeps visits casual and social (not competitive)

---

## 🔄 CORE ENGAGEMENT LOOPS

### **The Base-Expedition Cycle**

The base building system creates a **self-reinforcing feedback loop** with expeditions:

```
CORE LOOP (10-30 Minutes):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. PREPARE AT BASE
   ├─ Collect finished crafts (weapons/armor)
   ├─ Equip best gear on pets
   ├─ Stock consumables (potions/scrolls)
   └─ Select expedition mode (Solo/Co-op/PvPvE)
   
2. DEPLOY TO EXPEDITION
   ├─ Enter procedural world
   ├─ Gather biome-specific resources
   ├─ Capture pets
   └─ Defeat enemies for loot
   
3. EXTRACT WITH CARGO
   ├─ Survive extraction timer
   ├─ Navigate back through dangers
   ├─ Secure cargo at extraction zone
   └─ Return to base
   
4. PROCESS REWARDS
   ├─ Deposit resources in Warehouse
   ├─ Store new pets in Sanctuary
   ├─ Sell duplicates at Market
   └─ Choose next crafting priorities
   
5. INVEST IN BASE
   ├─ Start weapon/armor crafts
   ├─ Queue pet training sessions
   ├─ Research Laboratory upgrades
   └─ Upgrade buildings
   
6. WAIT & PLAN (Offline Period)
   ├─ Crafts complete over hours/days
   ├─ Training finishes
   ├─ Energy Generator accumulates resources
   └─ Research projects progress
   
7. RETURN & REPEAT (STRONGER)
   ├─ Collect finished items
   ├─ Pets are now higher level
   ├─ Research unlocked new bonuses
   └─ Ready for harder expeditions
```

**This loop is addictive because:**
- Each expedition makes your base stronger
- Each base upgrade makes expeditions easier
- Timers create anticipation ("I can't wait to see my finished legendary sword!")
- Progression is constant and visible

---

### **Daily Engagement Loop**

**What Players Do Every Day (5-10 Minutes Minimum):**

```
DAILY RITUAL:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. LOG IN → Spawn in base (not expedition)

2. CHECK MAILBOX
   ├─ Claim daily login reward
   ├─ Accept daily quests
   ├─ Read guild messages
   └─ See friend requests

3. COLLECT FINISHED TASKS
   ├─ Training Station → Pets leveled up
   ├─ Workshop → Potions crafted
   ├─ Breeding Station → New hybrid ready
   ├─ Energy Generator → Passive resources
   └─ Laboratory → Research completed

4. START NEW TASKS
   ├─ Queue overnight training
   ├─ Start 12-hour crafts
   ├─ Begin new research project
   └─ Set breeding pairs

5. QUICK EXPEDITION (Optional)
   ├─ 10-15 minute solo run
   ├─ Gather daily quest materials
   ├─ Extract and return

6. SOCIALIZE (Optional)
   ├─ Visit friend's base
   ├─ Check Market for deals
   ├─ Chat in Guild Hall
   └─ View leaderboards

7. LOG OUT (or continue playing)
```

**Even if players only have 5 minutes, they get:**
- Login reward
- Progress on overnight timers
- New tasks queued for tomorrow
- Feeling of advancement

**This creates daily habit formation.**

---

### **Weekly Engagement Loop**

**What Players Do Weekly (1-2 Hours Total):**

```
WEEKLY GOALS:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. BUILDING UPGRADES (Monday)
   ├─ Upgrade 1-2 buildings
   ├─ Costs accumulated weekly resources
   └─ Unlocks new functionality

2. LABORATORY RESEARCH (Wednesday)
   ├─ Complete 7-day research project
   ├─ Unlock account-wide bonus
   └─ Start next research

3. MARKET ACTIVITY (Friday)
   ├─ Check Market for rare pets
   ├─ List unwanted pets for sale
   ├─ Complete trades with other players
   └─ Invest in limited-time offers

4. GUILD EVENTS (Weekend)
   ├─ Participate in guild dungeon
   ├─ Contribute to guild upgrades
   ├─ Compete on guild leaderboard
   └─ Earn exclusive guild rewards

5. BASE RENOVATION (Sunday)
   ├─ Rearrange decorations
   ├─ Buy new cosmetic items
   ├─ Update Pet Daycare displays
   └─ Screenshot base for social media
```

**Weekly engagement prevents burnout:**
- Not everything requires daily attention
- Long-term projects feel rewarding
- Guild activities provide social motivation

---

### **Monthly Engagement Loop**

**What Players Do Monthly (10+ Hours Total):**

```
MONTHLY MILESTONES:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. UNLOCK NEW BUILDING
   ├─ Reach account level milestone
   ├─ Complete unlock achievement
   ├─ Construct new building
   └─ Access new systems

2. COMPLETE MAJOR RESEARCH
   ├─ Finish 30-day Laboratory project
   ├─ Unlock powerful account bonus
   ├─ Begin next long-term research
   └─ Feel major power spike

3. BASE AESTHETIC EVOLUTION
   ├─ Reach tier upgrade (e.g., Level 25 → Stone Outpost)
   ├─ Entire base visually transforms
   ├─ Screenshot evolution for comparison
   └─ Show off new look to friends

4. SEASONAL RESET
   ├─ New seasonal pets available
   ├─ Event Billboard updates with new content
   ├─ Leaderboard rankings reset
   ├─ Limited-time decorations appear
   └─ Fresh goals and challenges

5. GUILD HALL UPGRADES
   ├─ Guild completes monthly projects
   ├─ Guild Hall unlocks new features
   ├─ All members benefit from upgrades
   └─ Guild prestige increases
```

**Monthly engagement creates long-term commitment:**
- Major milestones feel earned
- Visual transformations are shareable moments
- Seasonal content keeps game fresh

---

## 🎮 PLAYER PROGRESSION JOURNEY

### **The First Hour (Tutorial Phase)**

**New Player Experience:**

```
NEW PLAYER SPAWN SEQUENCE:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. CHARACTER CREATION
   └─ Basic customization (cosmetic only)

2. TUTORIAL EXPEDITION
   ├─ Simple forest biome
   ├─ Capture first pet (guaranteed success)
   ├─ Defeat first enemy (easy win)
   └─ Extract to base

3. BASE ARRIVAL
   ├─ Spawn in empty plot of land
   ├─ NPC guide explains: "This is YOUR base!"
   └─ Only 2 buildings visible:
      • Expedition Hub (always available)
      • Warehouse (storage)

4. FIRST BUILDING UNLOCK
   ├─ Quest: "Build Your Weaponsmith!"
   ├─ Provided free resources
   ├─ Construction is instant (tutorial)
   └─ Quest reward: First weapon blueprint

5. FIRST CRAFT
   ├─ Quest: "Forge Your First Weapon!"
   ├─ Open Weaponsmith menu
   ├─ Craft weapon (instant, tutorial)
   └─ Equip on pet

6. SECOND EXPEDITION (Harder)
   ├─ Return to expedition with new weapon
   ├─ Notice increased damage
   ├─ Quest: "Capture 3 more pets!"
   └─ Extract successfully

7. UNLOCK TRAINING STATION
   ├─ Quest: "Train Your Pet!"
   ├─ Build Training Station (instant)
   ├─ Start first training (1 minute timer)
   └─ Wait and collect (experience waiting mechanic)

8. TUTORIAL COMPLETE
   ├─ Unlock Mailbox (daily rewards)
   ├─ Unlock Social Hub portal
   ├─ Tutorial quest chain ends
   └─ Player is now self-sufficient
```

**Tutorial Goals:**
- Teach expedition → base → upgrade → repeat loop
- Introduce timers gently (1 minute, not hours)
- Give immediate gratification (free resources, instant builds)
- Show progression visually (weapon makes pet stronger)

**Tutorial Duration:** 15-20 minutes

---

### **The First Week (Levels 1-10)**

**What New Players Experience:**

**Day 1-2:**
- Unlock Weaponsmith and Armorsmith
- Complete first few expeditions solo
- Start recognizing biomes and their resources
- First pet reaches Level 5

**Day 3-4:**
- Unlock Workshop (craft first potion)
- Unlock Training Station (queue overnight training)
- Discover Mailbox daily rewards
- Join first co-op expedition with friend

**Day 5-7:**
- Unlock Breeding Station (first pet merge)
- Base has 5 buildings now (feels established)
- First building upgrade (Weaponsmith Level 2)
- Reach account Level 10

**Week 1 Achievements:**
- ✅ Captured 20+ different pets
- ✅ Completed 15+ expeditions
- ✅ Built 5 core buildings
- ✅ Upgraded first building
- ✅ Formed daily login habit

---

### **The First Month (Levels 10-30)**

**Early-Game Progression:**

**Week 2 (Levels 11-15):**
- Unlock Sanctuary (display favorite pets)
- First legendary pet capture (exciting moment)
- Begin understanding elemental weaknesses
- Join first guild (social integration)

**Week 3 (Levels 16-20):**
- Unlock Laboratory (start first research)
- Base aesthetic evolves (Tier 2: Stone Outpost)
- Multiple buildings at Level 3-5
- Participate in first guild event

**Week 4 (Levels 21-30):**
- Unlock Market (start trading)
- Complete first 7-day research project
- First building reaches Level 10
- Attempt first PvPvE expedition

**Month 1 Achievements:**
- ✅ Account Level 30
- ✅ 8-10 buildings constructed
- ✅ First research completed
- ✅ Active guild member
- ✅ Established personal base aesthetic

---

### **The First Three Months (Levels 30-60)**

**Mid-Game Mastery:**

**Month 2:**
- Unlock advanced buildings (Refinery, Trophy Hall)
- Base has 12+ buildings (hitting plot limits)
- Consider purchasing premium plots
- Multiple pets at max level
- Active Market trader

**Month 3:**
- Unlock endgame buildings (Energy Generator, Automation Station)
- Base aesthetic Tier 3 (Advanced Fortress)
- Laboratory unlocked 5+ major researches
- Guild Hall established with active guild
- Consistent PvPvE participant

**Quarter 1 Achievements:**
- ✅ Account Level 60+
- ✅ 12-16 buildings (depending on premium)
- ✅ Base aesthetic Tier 3
- ✅ 50+ pets in Sanctuary
- ✅ Established Market reputation

---

### **Endgame (Levels 60+)**

**Long-Term Engagement:**

**Level 60-75:**
- All buildings unlocked
- Focus shifts to optimization and efficiency
- Trophy Hall filled with achievements
- Guild leadership or top contributor
- Mentoring new players

**Level 75-100:**
- Base aesthetic Tier 4 (Legendary Citadel)
- All buildings max level
- Laboratory research tree completed
- Legendary pet breeding projects
- Content creator or community figure

**Level 100+:**
- Seasonal leaderboard competitor
- Rare pet collector (gotta catch 'em all)
- Market tycoon (wealthy trader)
- Guild leader (manages 50+ members)
- Base showcased in official content

**Endgame Retention:**
- New seasonal content every 3 months
- Prestige system (reset with bonuses)
- Competitive PvPvE tournaments
- Rare cosmetic hunting
- Social community leadership

---

## 🗺️ BASE LAYOUT & PLOT SYSTEM

### **Plot-Based Placement System**

Your base uses a **pre-defined plot grid** where buildings can be placed:

**Plot Grid Structure:**

```
BASE LAYOUT (TOP-DOWN VIEW):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

         [PLOT 9]    [PLOT 10]   [PLOT 11]
              ↑           ↑           ↑
              │           │           │
    [PLOT 7]──┼──[PLOT 8]─┼─[PLOT 12]─┼──[PLOT 13]
              │           │           │
              ↓           ↓           ↓
         [PLOT 5]    [🏠 HUB]   [PLOT 6]
              ↑       (fixed)        ↑
              │           │           │
    [PLOT 3]──┼──[PLOT 4]─┼──[PLOT 14]┼──[PLOT 15]
              │           │           │
              ↓           ↓           ↓
         [PLOT 1]    [PLOT 2]   [PLOT 16*]
         
         
🏠 HUB = Expedition Hub + Mailbox (fixed, cannot move)
[PLOT 1-12] = Free plots (unlock via progression)
[PLOT 13-16*] = Premium plots ($9.99 for all 4)

TOTAL: 16 plots maximum (12 free + 4 premium)
```

---

### **Plot Unlocking Progression**

**How Plots Unlock:**

| Account Level | Plots Available | Cumulative Total |
|---------------|-----------------|------------------|
| Level 1 | Hub + 2 plots | 2 plots |
| Level 5 | +1 plot | 3 plots |
| Level 10 | +1 plot | 4 plots |
| Level 15 | +1 plot | 5 plots |
| Level 20 | +2 plots | 7 plots |
| Level 25 | +1 plot | 8 plots |
| Level 30 | +1 plot | 9 plots |
| Level 40 | +1 plot | 10 plots |
| Level 50 | +1 plot | 11 plots |
| Level 60 | +1 plot | 12 plots (FREE MAX) |
| Premium | +4 plots | 16 plots (PAID MAX) |

**Why Gradual Unlocking?**
- Prevents overwhelming new players with choices
- Creates milestones to celebrate
- Teaches building priorities naturally
- Makes premium plots feel valuable (not mandatory)

---

### **Plot Customization Options**

**Each plot can be customized with:**

**1. Building Selection**
- Choose which building occupies the plot
- Can demolish and rebuild different building (50% resource refund)

**2. Building Orientation**
- Rotate building to face different directions (N/S/E/W)
- Purely cosmetic, no gameplay impact

**3. Ground Decoration**
- Choose path type: Dirt / Stone / Brick / Marble
- Choose ground cover: Grass / Flowers / Snow / Lava Rocks
- Unlocked via achievements or premium currency

**4. Surrounding Decoration**
- Place 1-3 decorative items around building:
  • Trees (various types)
  • Statues (achievement trophies)
  • Fountains (animated)
  • Lights (torches, lanterns, magic crystals)
  • Fences (wood, stone, iron)

**5. Building Skin (Premium)**
- Change building's visual appearance
- Examples:
  • Gothic Weaponsmith (dark stone, red forge)
  • Crystal Laboratory (glowing blue crystals)
  • Nature Workshop (covered in vines)
  • Obsidian Armorsmith (black volcanic rock)

---

### **Plot Sizes & Spacing**

**Technical Specifications:**

- **Plot Size:** 20x20 studs (Roblox units)
- **Building Footprint:** 16x16 studs (leaves 2-stud border for decorations)
- **Path Width:** 4 studs between plots
- **Total Base Size:** ~180x180 studs (easily navigable on mobile)

**Why This Size?**
- ✅ Large enough for impressive buildings
- ✅ Small enough to see multiple buildings on mobile screen
- ✅ Fast travel hub optional (base walkable in <30 seconds)
- ✅ Room for decorations without clutter

---

### **Building Adjacency & Synergies**

**Recommended Layouts (No Mechanical Bonus, Just Aesthetic Logic):**

**Production District:**
```
[Weaponsmith] ←→ [Armorsmith]
       ↓               ↓
  [Workshop] ←→ [Refinery]
```
*Theme: Crafting and manufacturing*

**Pet District:**
```
[Training] ←→ [Breeding]
     ↓            ↓
[Sanctuary] ←→ [Daycare]
```
*Theme: Pet care and management*

**Social District:**
```
[Market] ←→ [Guild Hall]
    ↓            ↓
[Trophy] ←→ [Cosmetic Hub]
```
*Theme: Player interaction*

**Utility District:**
```
[Laboratory] ←→ [Warehouse]
      ↓               ↓
 [Generator] ←→ [Automation]
```
*Theme: Efficiency and progression*

**Players are FREE to ignore these suggestions.** Adjacency provides no gameplay bonuses—only thematic coherence for screenshots and social sharing.

---

### **Base Navigation System**

**Moving Around Your Base:**

**Option 1: Walking (Free)**
- Click/tap ground to walk
- Character moves at normal speed
- Takes ~20-30 seconds to cross entire base
- Good for casually exploring

**Option 2: Fast Travel Hub (Unlockable Building)**
- Build Fast Travel Hub in a plot
- Interact with it to open teleport menu
- Select destination building
- Instantly teleport to that building's entrance
- **Cost:** 10 gold per fast travel (nominal, prevents spam)

**Option 3: Building Quick Menu (Always Available)**
- Press "B" key or tap building icon (mobile)
- Radial menu appears showing all buildings
- Select building from menu
- Opens that building's interface remotely
- **Limitation:** Can't see building visually, just interact with menus

**Why Three Options?**
- Walking → Immersive, good for socializing/screenshots
- Fast Travel Hub → Convenience for frequent upgraders
- Quick Menu → Fastest for quick tasks (collect/queue)

---

### **Camera & Viewing Modes**

**Base Camera Controls:**

**Third-Person Mode (Default):**
- Camera follows player character
- Can rotate 360° around character
- Zoom in/out with pinch gesture (mobile) or scroll wheel (PC)
- Good for walking around and exploring

**Top-Down Mode:**
- Press "V" or UI button to switch
- Camera directly above base, looking down
- See entire base layout at once
- Great for planning and decorating

**Building Focus Mode:**
- Click/tap any building
- Camera zooms to that building
- UI appears with building options
- Press "Esc" to exit

**Screenshot Mode:**
- Press "F" or camera icon
- Removes all UI elements
- Allows perfect screenshots for social sharing
- Enables filters (sepia, black & white, etc.)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 2/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 2 of 10 (Building Overview & Phases)  
**Last Updated:** December 18, 2025

---

## 📋 PART 2 CONTENTS

**This document covers:**
1. Complete Building Roster (All 20 Buildings)
2. Building Categorization System
3. Phase 1: MVP Buildings (Launch Essential)
4. Phase 2: Advanced Buildings (Post-Launch Months 3-6)
5. Phase 3: Endgame Buildings (Post-Launch Months 6-12)
6. Phase 4: Utility & Premium Buildings (Ongoing)
7. Building Unlock Requirements
8. Construction Time & Cost Overview

---

## 🏛️ COMPLETE BUILDING ROSTER

### **All 20 Buildings at a Glance**

| # | Building Name | Category | Phase | Primary Function | Unlock Level |
|---|---------------|----------|-------|------------------|--------------|
| 1 | Expedition Hub | Core | 1 (MVP) | Deploy to expeditions | Level 1 (Default) |
| 2 | Warehouse | Core | 1 (MVP) | Resource storage | Level 1 (Default) |
| 3 | Mailbox/Notice Board | Core | 1 (MVP) | Daily rewards & quests | Level 3 |
| 4 | Weaponsmith | Production | 1 (MVP) | Craft weapons | Level 5 |
| 5 | Armorsmith | Production | 1 (MVP) | Craft armor | Level 10 |
| 6 | Workshop | Production | 1 (MVP) | Craft consumables | Level 15 |
| 7 | Training Station | Pet Management | 1 (MVP) | Train pets with resources | Level 12 |
| 8 | Breeding Station | Pet Management | 1 (MVP) | Merge & breed pets | Level 20 |
| 9 | Refinery | Production | 2 (Advanced) | Process raw materials | Level 25 |
| 10 | Sanctuary | Pet Management | 2 (Advanced) | Display pet collection | Level 30 |
| 11 | Laboratory | Progression | 2 (Advanced) | Research permanent bonuses | Level 35 |
| 12 | Market/Trading Post | Economy | 2 (Advanced) | Buy/sell with players | Level 40 |
| 13 | Trophy Hall | Social | 2 (Advanced) | Display achievements | Level 45 |
| 14 | Pet Daycare | Pet Management | 3 (Endgame) | Interactive pet display | Level 50 |
| 15 | Cosmetic Hub | Premium | 3 (Endgame) | Customize appearance | Level 55 |
| 16 | Energy Generator | Utility | 3 (Endgame) | Passive resource generation | Level 60 |
| 17 | Guild Hall | Social | 3 (Endgame) | Guild management | Level 65 |
| 18 | Automation Station | Utility | 3 (Endgame) | Queue management system | Level 70 |
| 19 | Fast Travel Hub | Utility | 4 (Ongoing) | Teleport between buildings | Level 40 |
| 20 | Event Billboard | Social | 4 (Ongoing) | Seasonal content hub | Level 1 (Seasonal) |

---

## 🗂️ BUILDING CATEGORIZATION SYSTEM

### **By Function Type**

**Core Buildings (3):**
- Essential for basic game loop
- Unlocked very early (Levels 1-3)
- Cannot be demolished once built
- Always visible in UI

**Production Buildings (4):**
- Create weapons, armor, consumables, materials
- Resource → Item conversion
- Time-gated crafting
- Upgradeable for slots/speed

**Pet Management Buildings (4):**
- Train, breed, display, interact with pets
- Core progression for pet-focused players
- Real-time mechanics (age, bonds)
- High engagement frequency

**Progression Buildings (1):**
- Unlock account-wide permanent bonuses
- Long-term investment (days/weeks)
- Creates strategic depth
- Research tree structure

**Economy Buildings (1):**
- Player-to-player trading
- Auction house mechanics
- NPC vendors
- Gold sink systems

**Social Buildings (3):**
- Guild features
- Friend interactions
- Achievement displays
- Community engagement

**Utility Buildings (3):**
- Quality-of-life improvements
- Convenience features
- Time-savers (not power)
- Optional but valuable

**Premium Buildings (1):**
- Cosmetic customization
- Visual personalization
- Monetization hub
- Zero gameplay advantage

---

### **By Unlock Phase**

**Phase 1 Buildings (8) - MVP Launch:**
- Must be in game at launch
- Core gameplay loop depends on them
- Teach fundamental mechanics
- Unlocked in first 20 levels

**Phase 2 Buildings (5) - Advanced Content:**
- Add depth and complexity
- Unlocked Levels 25-45
- Expand strategic options
- Retain mid-game players

**Phase 3 Buildings (5) - Endgame Systems:**
- Long-term engagement features
- Unlocked Levels 50-70
- Guild and social focus
- Prestige and optimization

**Phase 4 Buildings (2) - Ongoing/Seasonal:**
- Added as needed
- May be temporary (Event Billboard)
- Quality-of-life additions
- Community-requested features

---

### **By Player Type Appeal**

**Combat-Focused Players:**
- Weaponsmith ⭐⭐⭐⭐⭐
- Armorsmith ⭐⭐⭐⭐⭐
- Workshop ⭐⭐⭐⭐
- Laboratory (combat research) ⭐⭐⭐

**Pet Collectors:**
- Breeding Station ⭐⭐⭐⭐⭐
- Training Station ⭐⭐⭐⭐⭐
- Sanctuary ⭐⭐⭐⭐⭐
- Pet Daycare ⭐⭐⭐⭐
- Laboratory (pet research) ⭐⭐⭐

**Traders & Economists:**
- Market/Trading Post ⭐⭐⭐⭐⭐
- Warehouse ⭐⭐⭐⭐
- Refinery ⭐⭐⭐⭐
- Energy Generator ⭐⭐⭐

**Social Players:**
- Guild Hall ⭐⭐⭐⭐⭐
- Trophy Hall ⭐⭐⭐⭐
- Pet Daycare ⭐⭐⭐
- Mailbox ⭐⭐⭐

**Casual/Time-Limited Players:**
- Automation Station ⭐⭐⭐⭐⭐
- Energy Generator ⭐⭐⭐⭐
- Fast Travel Hub ⭐⭐⭐⭐
- Mailbox (daily rewards) ⭐⭐⭐⭐

**Completionists:**
- Trophy Hall ⭐⭐⭐⭐⭐
- Sanctuary ⭐⭐⭐⭐
- Laboratory ⭐⭐⭐⭐
- All buildings (collect them all!) ⭐⭐⭐⭐⭐

---

## 🎯 PHASE 1: MVP BUILDINGS (LAUNCH ESSENTIAL)

### **Phase 1 Overview**

**Timeline:** Game Launch (Day 1)  
**Building Count:** 8 buildings  
**Target:** Levels 1-20  
**Purpose:** Establish core gameplay loop

**Phase 1 Buildings:**
1. Expedition Hub *(Level 1 - Default)*
2. Warehouse *(Level 1 - Default)*
3. Mailbox/Notice Board *(Level 3)*
4. Weaponsmith *(Level 5)*
5. Training Station *(Level 12)*
6. Armorsmith *(Level 10)*
7. Workshop *(Level 15)*
8. Breeding Station *(Level 20)*

---

### **1. Expedition Hub** 🗺️

**Unlock:** Level 1 (Default, Always Available)

**Primary Function:**
- Deploy to Solo/Co-op/PvPvE expeditions
- Select biome difficulty
- Choose companion pets (1-3 depending on upgrade)
- Equip crafted weapons/armor
- Stock consumables (potions, scrolls)

**Why MVP Critical:**
- Players cannot play without it
- Core loop entry point
- First building players interact with

**Upgrade Benefits:**
- Level 1: Deploy with 1 companion pet
- Level 3: Deploy with 2 companion pets
- Level 5: Deploy with 3 companion pets
- Level 7: Unlock "Quick Deploy" (repeat last loadout)
- Level 10: Unlock "Squad Presets" (save 3 loadout configurations)

**Construction:**
- Cost: FREE (auto-built at start)
- Time: Instant
- Cannot demolish

**Max Level:** 10

---

### **2. Warehouse** 📦

**Unlock:** Level 1 (Default, Always Available)

**Primary Function:**
- Store resources gathered from expeditions
- Store crafted items
- Store captured pets (basic storage)
- Organize inventory by categories

**Why MVP Critical:**
- Players need resource storage immediately
- Without it, inventory management impossible
- Gates all crafting systems

**Upgrade Benefits:**
- Level 1: 100 storage slots
- Level 3: 200 slots + unlock "Auto-Sort" feature
- Level 5: 350 slots + unlock resource filters
- Level 7: 500 slots + unlock "Quick Stack" (auto-combine stacks)
- Level 10: 750 slots + unlock remote access (from expedition)

**Construction:**
- Cost: FREE (auto-built at start)
- Time: Instant
- Cannot demolish

**Storage Categories:**
- Raw Materials (iron ore, wood, plants)
- Refined Materials (ingots, cloth, gems)
- Consumables (potions, scrolls, food)
- Equipment (weapons, armor)
- Pet-Related (treats, training materials)
- Miscellaneous (quest items, event tokens)

**Max Level:** 10

**Premium Expansion:**
- $4.99 → +500 permanent slots (1,250 total at max level)

---

### **3. Mailbox / Notice Board** 📬

**Unlock:** Level 3

**Primary Function:**
- Claim daily login rewards
- Accept daily/weekly quests
- Read announcements from developers
- Receive friend requests
- Guild invitations and messages

**Why MVP Critical:**
- Daily engagement driver
- Teaches daily login habit
- Quest system foundation

**Upgrade Benefits:**
- Level 1: Daily login rewards only
- Level 2: Unlock daily quests (3 per day)
- Level 3: Unlock weekly quests (3 per week)
- Level 4: Increase daily quest slots (5 per day)
- Level 5: Increase weekly quest slots (5 per week)
- Level 7: Unlock "Quest Auto-Track" (navigate to objectives)
- Level 10: Unlock "Premium Mail" (exclusive offers/rewards)

**Daily Rewards Track:**
| Day | Reward |
|-----|--------|
| 1 | 500 Gold + 10 Common Training Materials |
| 2 | 750 Gold + 1 Rare Pet Egg |
| 3 | 1,000 Gold + 3 Health Potions |
| 4 | 1,500 Gold + 10 Rare Training Materials |
| 5 | 2,000 Gold + 1 Epic Pet Egg |
| 6 | 2,500 Gold + 5 Resurrection Scrolls |
| 7 | 5,000 Gold + 1 Legendary Pet Egg + 100 Premium Currency |

*Resets weekly, streak bonuses for consecutive logins*

**Construction:**
- Cost: 1,000 Gold + 50 Wood + 20 Stone
- Time: Instant (tutorial)
- Cannot demolish

**Max Level:** 10

---

### **4. Weaponsmith** ⚔️

**Unlock:** Level 5

**Primary Function:**
- Craft weapons for companion pets
- Upgrade existing weapons
- Unlock weapon blueprints via research
- Weapons provide offensive buffs (damage, crit chance, elemental damage)

**Why MVP Critical:**
- Core progression system
- Players need damage scaling
- Teaches crafting mechanics

**Upgrade Benefits:**
- Level 1: 1 crafting slot, basic weapons only
- Level 2: 2 crafting slots
- Level 3: Unlock rare weapon recipes
- Level 4: 3 crafting slots + 10% faster crafting
- Level 5: Unlock epic weapon recipes
- Level 7: 4 crafting slots + 20% faster crafting
- Level 10: 5 slots + 30% faster + unlock legendary recipes

**Weapon Types:**
- Swords (balanced damage)
- Axes (high single-target damage)
- Bows (ranged damage)
- Staves (magical/elemental damage)
- Hammers (heavy damage, slow)
- Daggers (fast, critical hits)

**Crafting Time Examples:**
- Common Weapon: 5 minutes
- Rare Weapon: 30 minutes
- Epic Weapon: 2 hours
- Legendary Weapon: 12 hours

**Construction:**
- Cost: 2,500 Gold + 100 Iron Ore + 50 Wood
- Time: 10 minutes
- Can demolish (50% refund)

**Max Level:** 10

---

### **5. Armorsmith** 🛡️

**Unlock:** Level 10

**Primary Function:**
- Craft armor for player character
- Upgrade existing armor
- Unlock armor blueprints via research
- Armor provides defensive buffs (HP, defense, elemental resistance)

**Why MVP Critical:**
- Survival scaling for harder biomes
- Damage absorption mechanics
- Complements weapon system

**Upgrade Benefits:**
- Level 1: 1 crafting slot, basic armor only
- Level 2: 2 crafting slots
- Level 3: Unlock rare armor recipes
- Level 4: 3 crafting slots + 10% faster crafting
- Level 5: Unlock epic armor recipes
- Level 7: 4 crafting slots + 20% faster crafting
- Level 10: 5 slots + 30% faster + unlock legendary recipes

**Armor Pieces:**
- Helmet (head protection)
- Chestplate (torso protection)
- Leggings (leg protection)
- Boots (foot protection + movement speed)
- Gloves (hand protection + attack speed)
- Cloak (elemental resistance)

**Armor Set Bonuses:**
- 2-Piece: +5% HP
- 4-Piece: +10% HP + 5% Defense
- 6-Piece: +15% HP + 10% Defense + Elemental Resistance

**Crafting Time Examples:**
- Common Armor: 5 minutes
- Rare Armor: 30 minutes
- Epic Armor: 2 hours
- Legendary Armor: 12 hours

**Construction:**
- Cost: 3,000 Gold + 150 Iron Ore + 100 Leather
- Time: 15 minutes
- Can demolish (50% refund)

**Max Level:** 10

---

### **6. Training Station** 🎓

**Unlock:** Level 12

**Primary Function:**
- Train pets using biome-specific resources
- Convert resources → pet experience
- Queue multiple pets (slots unlock via upgrades)
- Real-time training (minutes to days)

**Why MVP Critical:**
- Core pet progression system
- Replaces mindless XP grinding
- Teaches resource management

**Upgrade Benefits:**
- Level 1: 1 training slot
- Level 2: 2 training slots
- Level 3: 3 slots + 10% faster training
- Level 4: 4 slots
- Level 5: 5 slots + 20% faster training
- Level 7: 6 slots + 30% faster training
- Level 10: 8 slots + 50% faster training + unlock "Mass Training"

**Training Time by Rarity:**
| Pet Rarity | Level 1→2 | Level 10→11 | Level 50→51 |
|------------|-----------|-------------|-------------|
| Common | 1 minute | 10 minutes | 2 hours |
| Uncommon | 2 minutes | 20 minutes | 4 hours |
| Rare | 5 minutes | 1 hour | 12 hours |
| Epic | 15 minutes | 4 hours | 24 hours |
| Legendary | 1 hour | 12 hours | 3 days |

**Resource Requirements Scale With:**
- Pet level (higher = more resources)
- Pet rarity (legendary = 5x common)
- Training Station level (higher = discount)

**Construction:**
- Cost: 2,000 Gold + 50 Training Materials
- Time: 5 minutes
- Can demolish (50% refund)

**Max Level:** 10

---

### **7. Workshop** 🧪

**Unlock:** Level 15

**Primary Function:**
- Craft consumables (potions, scrolls, food)
- Upgrade existing consumable recipes
- Unlock consumable blueprints
- Consumables used in expeditions for survival

**Why MVP Critical:**
- Survival mechanics for harder content
- Teaches buff/heal systems
- Resource sink (economy balance)

**Upgrade Benefits:**
- Level 1: 1 crafting slot, basic consumables
- Level 2: 2 crafting slots
- Level 3: Unlock rare consumable recipes
- Level 4: 3 crafting slots + 10% crafting discount
- Level 5: Unlock epic consumable recipes
- Level 7: 4 crafting slots + 20% crafting discount
- Level 10: 5 slots + 30% discount + unlock legendary recipes

**Consumable Categories:**

**Health Items:**
- Small Health Potion (restore 25% HP, 30s cooldown)
- Medium Health Potion (restore 50% HP, 60s cooldown)
- Large Health Potion (restore 100% HP, 120s cooldown)

**Buff Items:**
- Strength Elixir (+20% damage, 5 minutes)
- Defense Tonic (+20% defense, 5 minutes)
- Speed Potion (+30% movement speed, 3 minutes)

**Utility Items:**
- Resurrection Scroll (revive fainted pet)
- Teleport Crystal (instant extraction, emergency use)
- Invisibility Cloak (avoid enemy detection, 30 seconds)

**Pet-Specific:**
- Pet Treat (restore pet HP during combat)
- Bond Boost (increase pet friendship, permanent)
- XP Elixir (double training XP gain, 1 use)

**Crafting Time Examples:**
- Common Consumable: 1 minute (x10 batch)
- Rare Consumable: 10 minutes (x5 batch)
- Epic Consumable: 1 hour (x3 batch)
- Legendary Consumable: 4 hours (x1 single)

**Construction:**
- Cost: 2,500 Gold + 100 Plants + 50 Gems
- Time: 10 minutes
- Can demolish (50% refund)

**Max Level:** 10

---

### **8. Breeding Station** 🥚

**Unlock:** Level 20

**Primary Function:**
- Breed two pets to create offspring
- Merge two identical pets to increase star rating
- IV inheritance system
- Hybrid elemental combinations

**Why MVP Critical:**
- Advanced pet progression
- Creates aspirational goals (perfect IV pets)
- Long-term engagement (breeding takes days)

**Upgrade Benefits:**
- Level 1: 1 breeding slot, 7-day breeding time
- Level 2: 2 breeding slots
- Level 3: 5-day breeding time + unlock rare hybrids
- Level 4: 3 breeding slots
- Level 5: 3-day breeding time + unlock epic hybrids
- Level 7: 4 breeding slots + 2-day breeding time
- Level 10: 5 slots + 1-day breeding + unlock legendary hybrids

**Breeding Mechanics:**

**Star Merging:**
- Combine 2 identical pets (same species, same star level)
- Result: 1 pet at +1 star rating
- Example: 2x ⭐⭐ Fire Wolf → 1x ⭐⭐⭐ Fire Wolf

**Breeding (Two Different Pets):**
- Combine 2 different pets (any species, any star)
- Result: Offspring inherits traits from both parents
- IV inheritance (random from parent ranges)
- Possible elemental hybrid (Fire + Water = Steam)

**Breeding Time:**
- Common × Common: 1 day
- Rare × Rare: 3 days
- Epic × Epic: 7 days
- Legendary × Legendary: 14 days

**Construction:**
- Cost: 5,000 Gold + 200 Breeding Materials
- Time: 30 minutes
- Can demolish (50% refund)

**Max Level:** 10

---

## 🚀 PHASE 2: ADVANCED BUILDINGS

### **Phase 2 Overview**

**Timeline:** Months 3-6 Post-Launch  
**Building Count:** 5 buildings  
**Target:** Levels 25-45  
**Purpose:** Add strategic depth and retain mid-game players

**Phase 2 Buildings:**
9. Refinery *(Level 25)*
10. Sanctuary *(Level 30)*
11. Laboratory *(Level 35)*
12. Market/Trading Post *(Level 40)*
13. Trophy Hall *(Level 45)*

---

### **9. Refinery** ⚗️

**Unlock:** Level 25

**Primary Function:**
- Process raw materials → refined materials
- Increase resource value (sell for more gold)
- Unlock advanced crafting recipes requiring refined materials
- Batch processing for efficiency

**Why Phase 2:**
- Early game doesn't need refining (basic recipes only)
- Adds economic depth once players have surplus resources
- Creates market opportunities (sell refined vs raw)

**Upgrade Benefits:**
- Level 1: 1 refining slot, basic recipes
- Level 2: 2 refining slots
- Level 3: 3 slots + 10% faster refining
- Level 4: 4 slots + unlock rare refining recipes
- Level 5: 5 slots + 20% faster refining
- Level 7: 6 slots + 30% faster + unlock epic recipes
- Level 10: 8 slots + 50% faster + unlock legendary recipes

**Refining Recipes:**

**Metals:**
- Iron Ore (x3) → Iron Ingot (x1) - 10 minutes
- Gold Ore (x3) → Gold Ingot (x1) - 30 minutes
- Mithril Ore (x3) → Mithril Ingot (x1) - 2 hours

**Textiles:**
- Plant Fiber (x5) → Cloth (x1) - 5 minutes
- Silk Thread (x5) → Silk Fabric (x1) - 1 hour
- Dragon Scale (x1) → Dragonweave (x1) - 4 hours

**Gems:**
- Rough Gemstone (x2) → Polished Gem (x1) - 15 minutes
- Raw Crystal (x2) → Refined Crystal (x1) - 1 hour
- Chaos Shard (x5) → Chaos Core (x1) - 6 hours

**Value Increase:**
- Raw Iron Ore: 10 gold each
- Iron Ingot: 50 gold each (5x value, but 3:1 ratio = 1.67x profit)

**Construction:**
- Cost: 10,000 Gold + 500 Iron Ore + 200 Gems
- Time: 1 hour
- Can demolish (50% refund)

**Max Level:** 10

---

### **10. Sanctuary** 🏛️

**Unlock:** Level 30

**Primary Function:**
- Display pet collection in trophy cases
- Organize pets by element/rarity/favorites
- View detailed pet stats and history
- Passive bonuses from displayed pets

**Why Phase 2:**
- Players have 50+ pets by Level 30 (need organization)
- Social showcase feature (friends admire collection)
- Creates "gotta catch 'em all" motivation

**Upgrade Benefits:**
- Level 1: Display 20 pets
- Level 2: Display 30 pets + unlock rarity sorting
- Level 3: Display 40 pets + passive bonus (+2% gold from expeditions)
- Level 4: Display 50 pets + unlock element sorting
- Level 5: Display 75 pets + passive bonus (+5% gold)
- Level 7: Display 100 pets + unlock favorites category
- Level 10: Display 150 pets + passive bonus (+10% gold + 5% XP)

**Display Options:**
- Sort by Element (Fire, Water, Earth, etc.)
- Sort by Rarity (Common → Legendary)
- Sort by Star Rating (⭐ → ⭐⭐⭐⭐⭐)
- Sort by Level (1 → 100)
- Sort by Favorites (manually tag favorites)
- Sort by Newest (recently captured)

**Passive Bonuses (Displayed Pets Only):**
- 10 Unique Species Displayed: +2% gold
- 25 Unique Species: +5% gold
- 50 Unique Species: +10% gold + 5% XP
- 100 Unique Species: +15% gold + 10% XP + 5% capture rate

**Social Features:**
- Friends can tour your Sanctuary
- View pet details (stats, moves, history)
- "Like" favorite pets (reputation system)
- Compare collections with friends

**Construction:**
- Cost: 15,000 Gold + 500 Stone + 200 Gems
- Time: 2 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **11. Laboratory** 🔬

**Unlock:** Level 35

**Primary Function:**
- Research permanent account-wide bonuses
- Unlock new systems and features
- Long-term projects (days to weeks)
- Strategic choices (research tree paths)

**Why Phase 2:**
- Players understand core mechanics by Level 35
- Adds strategic depth and long-term planning
- Account progression separate from individual pets

**Upgrade Benefits:**
- Level 1: 1 research slot, basic research tree
- Level 2: 2 research slots
- Level 3: Unlock advanced research tree
- Level 4: 3 research slots + 10% faster research
- Level 5: Unlock expert research tree
- Level 7: 4 research slots + 20% faster research
- Level 10: 5 slots + 30% faster + unlock legendary research

**Research Categories:**

**Combat Research:**
- Improved Critical Hit (+5% crit chance) - 3 days
- Enhanced Damage (+10% all damage) - 7 days
- Perfect Parry (unlock perfect defense timing) - 14 days

**Pet Research:**
- Faster Training (+10% training speed) - 3 days
- Breeding Mastery (+20% IV inheritance chance) - 7 days
- Pet Longevity (pets age 25% slower) - 14 days

**Exploration Research:**
- Increased Carry Capacity (+10 inventory slots) - 2 days
- Better Loot (+10% rare drop chance) - 5 days
- Biome Specialist (choose one biome, +20% rewards) - 10 days

**Economy Research:**
- Merchant's Eye (+10% sell prices) - 3 days
- Resource Efficiency (-10% crafting costs) - 7 days
- Market Mastery (-20% auction house fees) - 14 days

**Capture Research:**
- Improved Capture Rate (+10% capture success) - 5 days
- Quick Capture (capture mechanic 20% faster) - 10 days
- Legendary Luck (+50% legendary spawn rate) - 30 days

**Research Tree Structure:**
- Tier 1 Research: 1-3 days, small bonuses
- Tier 2 Research: 5-7 days, medium bonuses (requires Tier 1)
- Tier 3 Research: 10-14 days, large bonuses (requires Tier 2)
- Tier 4 Research: 21-30 days, game-changing bonuses (requires Tier 3)

**Construction:**
- Cost: 25,000 Gold + 1,000 Mixed Materials
- Time: 4 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **12. Market / Trading Post** 💰

**Unlock:** Level 40

**Primary Function:**
- List pets/items/resources for sale (auction house)
- Browse other players' listings
- Direct player-to-player trades
- NPC vendors for basic supplies

**Why Phase 2:**
- Players have surplus pets/items by Level 40
- Established economy needs by mid-game
- Social trading adds engagement

**Upgrade Benefits:**
- Level 1: List 5 items, 10% auction fee
- Level 2: List 10 items, 8% fee
- Level 3: List 15 items, 6% fee + unlock "Featured Listings"
- Level 5: List 25 items, 5% fee + unlock "Buy Orders"
- Level 7: List 40 items, 3% fee + unlock "Private Trades"
- Level 10: List 50 items, 1% fee + unlock "Market Analytics"

**Auction House Mechanics:**

**Listing Items:**
- Set starting price
- Set buyout price (optional)
- Set duration (1 day / 3 days / 7 days)
- Pay listing fee (non-refundable)

**Bidding:**
- Players bid incrementally
- Highest bid at expiration wins
- Outbid notifications
- Automatic buyout option

**Direct Trades:**
- Send trade offer to specific player
- Both parties confirm items/gold
- No auction house fee (0% for direct)

**NPC Vendors:**
- Basic consumables (overpriced, emergency only)
- Common training materials (convenience)
- Starter equipment (new player assistance)
- Quest items (specific quest requirements)

**Market Filters:**
- Pet Species
- Element Type
- Rarity Level
- Star Rating
- Price Range
- Recently Listed / Ending Soon

**Market Analytics (Level 10 Feature):**
- Price history graphs
- Supply/demand trends
- Popular pet species
- Recommended pricing

**Construction:**
- Cost: 30,000 Gold + 1,000 Mixed Resources
- Time: 6 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **13. Trophy Hall** 🏆

**Unlock:** Level 45

**Primary Function:**
- Display earned achievements as physical trophies
- Track completion progress
- Social prestige showcase
- Unlock achievement-specific rewards

**Why Phase 2:**
- Players have meaningful achievements by Level 45
- Creates completionist goals
- Social showcase for hardcore players

**Upgrade Benefits:**
- Level 1: Display 10 trophies
- Level 2: Display 20 trophies
- Level 3: Display 30 trophies + unlock "Rare Achievements"
- Level 5: Display 50 trophies + passive bonus (+3% rare drop)
- Level 7: Display 75 trophies + unlock "Epic Achievements"
- Level 10: Display 100 trophies + passive bonus (+5% rare drop + title rewards)

**Achievement Categories:**

**Exploration:**
- Discover All Biomes (statue of world map)
- Traverse 1,000 km Total (golden compass)
- Extract 100 Times Successfully (extraction beacon trophy)

**Combat:**
- Defeat 10,000 Enemies (sword monument)
- Perfect Combo 100 Times (golden timing circle)
- Win 50 PvPvE Encounters (champion's crown)

**Pet Collection:**
- Capture 100 Unique Species (master ball statue)
- Breed First Legendary Hybrid (breeding chamber model)
- Raise Pet to Level 100 (pet statue of your choice)

**Crafting:**
- Craft 1,000 Items Total (forgemaster anvil)
- Create First Legendary Weapon (weapon display case)
- Refine 10,000 Materials (refinery model)

**Social:**
- Join a Guild (guild banner trophy)
- Visit 50 Friend Bases (traveler's compass)
- Complete 100 Co-op Expeditions (teamwork medal)

**Economy:**
- Earn 1,000,000 Gold Total (golden vault)
- Complete 100 Market Trades (merchant's scales)
- Sell Legendary Pet (auctioneer's gavel)

**Seasonal:**
- Complete Seasonal Event (seasonal trophy, time-limited)
- Rank Top 100 Leaderboard (leaderboard plaque)
- Win Tournament (championship cup)

**Trophy Rarity:**
- Bronze: Common achievements (50+ available)
- Silver: Rare achievements (25+ available)
- Gold: Epic achievements (10+ available)
- Platinum: Legendary achievements (5+ available)
- Diamond: Unique achievements (1-3 available, extremely rare)

**Social Features:**
- Friends can view your Trophy Hall
- Each trophy has description and unlock date
- Compare achievement progress with friends
- Guild achievement totals visible

**Construction:**
- Cost: 35,000 Gold + 1,500 Mixed Resources
- Time: 8 hours
- Can demolish (50% refund)

**Max Level:** 10

---

## 🎖️ PHASE 3: ENDGAME BUILDINGS

### **Phase 3 Overview**

**Timeline:** Months 6-12 Post-Launch  
**Building Count:** 5 buildings  
**Target:** Levels 50-70  
**Purpose:** Long-term retention and guild/social systems

**Phase 3 Buildings:**
14. Pet Daycare *(Level 50)*
15. Cosmetic Hub *(Level 55)*
16. Energy Generator *(Level 60)*
17. Guild Hall *(Level 65)*
18. Automation Station *(Level 70)*

---

### **14. Pet Daycare** 🐾

**Unlock:** Level 50

**Primary Function:**
- Display pets in "living" interactive environment
- Pets walk around, play, interact with each other
- Click pets to view stats/play minigames
- Emotional bonding feature (see pets happy)

**Why Phase 3:**
- "Alive" feature for dedicated players
- Screenshot/social media content generator
- Aesthetic appeal over gameplay function

**Upgrade Benefits:**
- Level 1: Display 5 pets, small daycare area
- Level 2: Display 10 pets
- Level 3: Display 15 pets + pets interact with each other
- Level 5: Display 25 pets + unlock animations (play, sleep, eat)
- Level 7: Display 40 pets + unlock minigames (fetch, puzzle)
- Level 10: Display 50 pets + unlock "Pet Party" events

**Interactive Features:**
- Click pet to pet them (friendship increase)
- Give treats (purchased from Workshop)
- Play minigames (simple mobile games)
- Watch pets socialize (randomized interactions)

**Social Features:**
- Friends can interact with your pets
- Pets remember visitors (return players greeted excitedly)
- Screenshot pets playing together

**Construction:**
- Cost: 40,000 Gold + 2,000 Mixed Resources
- Time: 12 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **15. Cosmetic Hub / Vanity Station** 💅

**Unlock:** Level 55

**Primary Function:**
- Customize player character appearance
- Apply pet skins and particle effects
- Change building aesthetics
- Monetization hub for cosmetics

**Why Phase 3:**
- Cosmetics marketed to established players
- Monetization without affecting early progression
- Social status symbol

**Upgrade Benefits:**
- Level 1: Basic cosmetic options
- Level 2: Unlock rare cosmetics
- Level 3: Unlock pet particle effects
- Level 5: Unlock building skins
- Level 7: Unlock animated cosmetics
- Level 10: Unlock legendary exclusive cosmetics

**Customization Options:**

**Player Character:**
- Hairstyles (50+ options)
- Hair colors (infinite palette)
- Outfits (shirts, pants, robes, armor skins)
- Accessories (hats, glasses, scarves, badges)
- Emotes (dances, gestures, celebrations)

**Pet Cosmetics:**
- Skin Colors (alternative color palettes)
- Particle Effects (flames, sparkles, auras)
- Accessories (hats, collars, wings)
- Size Modifiers (giant pets, tiny pets - cosmetic only)

**Building Skins:**
- Gothic Weaponsmith (dark stone, red forge)
- Crystal Laboratory (glowing crystals)
- Nature Workshop (covered in vines)
- Obsidian Armorsmith (volcanic aesthetic)

**How to Obtain:**
- Purchase with premium currency
- Earn via achievements
- Seasonal event rewards
- Battle pass rewards
- Limited-time offers

**Construction:**
- Cost: 45,000 Gold + 2,500 Mixed Resources
- Time: 16 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **16. Energy Generator** ⚡

**Unlock:** Level 60

**Primary Function:**
- Generate small amounts of resources while offline
- Passive income for casual players
- NOT a replacement for expeditions (10-20% of active play)

**Why Phase 3:**
- Respects time-limited players
- Prevents feeling "forced" to grind
- Ethical QoL feature

**Upgrade Benefits:**
- Level 1: Generate 10 resources per hour (offline only)
- Level 2: Generate 15 per hour
- Level 3: Generate 20 per hour + choose resource type
- Level 5: Generate 30 per hour + unlock rare resources
- Level 7: Generate 50 per hour + unlock multiple types
- Level 10: Generate 100 per hour + unlock "Premium Generator Mode"

**Resource Generation:**
- Common materials only (iron, wood, plants)
- Random selection from available biomes
- Cap at 24 hours (prevents infinite hoarding)
- Must be collected manually (log in to claim)

**Example Output (24 Hours Offline):**
- Level 1 Generator: 240 common resources
- Level 10 Generator: 2,400 common resources

**Compare to Active Play:**
- 1-hour expedition: 500-1,000 resources
- Generator is 20-50% of active play efficiency

**Premium Generator Mode (Level 10 + Premium):**
- Generate rare materials (15% of output)
- Double generation rate (200 per hour)
- Auto-collect (no need to claim manually)

**Construction:**
- Cost: 50,000 Gold + 3,000 Mixed Resources
- Time: 24 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **17. Guild Hall** 🏰

**Unlock:** Level 65

**Primary Function:**
- Join or create guilds
- Access guild chat
- View guild roster and activities
- Contribute to guild upgrades
- Participate in guild events

**Why Phase 3:**
- Guilds for established, committed players
- Social endgame content
- Competitive guild leaderboards

**Upgrade Benefits:**
- Level 1: Join guild, basic chat
- Level 2: Guild storage (shared resources)
- Level 3: Guild missions (weekly objectives)
- Level 5: Guild buffs (+5% XP for all members)
- Level 7: Guild dungeon access (weekly raid)
- Level 10: Guild wars (compete vs other guilds)

**Guild Features:**

**Guild Creation:**
- Cost: 100,000 Gold
- Name your guild (unique)
- Choose guild emblem
- Set guild motto

**Guild Roles:**
- Guild Leader (1) - full control
- Officers (3) - invite/kick members, manage events
- Veterans (10) - experienced members, no special powers
- Members (unlimited) - standard members

**Guild Storage:**
- Shared resource pool
- Deposit resources (cannot withdraw unless leader permits)
- Used for guild upgrades

**Guild Missions:**
- Weekly objectives (capture 100 rare pets as guild)
- Rewards for all members upon completion
- Increases guild level

**Guild Buffs:**
- Level 1 Guild: +5% XP for members
- Level 5 Guild: +10% XP + 5% gold
- Level 10 Guild: +15% XP + 10% gold + 5% capture rate

**Guild Dungeons:**
- Weekly raid (20+ guild members cooperate)
- Exclusive rewards (legendary pets, cosmetics)
- Guild leaderboard ranking

**Guild Island (Separate Instance):**
- Shared space where guild members gather
- Guild monument (displays achievements)
- Guild shop (exclusive items)
- Social hangout area

**Construction:**
- Cost: 75,000 Gold + 5,000 Mixed Resources
- Time: 48 hours
- Can demolish (50% refund)

**Max Level:** 10

---

### **18. Automation Station** 🤖

**Unlock:** Level 70

**Primary Function:**
- Automate repetitive tasks
- Queue crafting recipes in advance
- Schedule training sessions
- Manage multiple pets simultaneously

**Why Phase 3:**
- QoL for endgame players with 50+ pets
- Reduces micromanagement tedium
- Respects player time

**Upgrade Benefits:**
- Level 1: Auto-queue 3 tasks
- Level 2: Auto-queue 5 tasks
- Level 3: Auto-queue 10 tasks + auto-collect finished crafts
- Level 5: Auto-queue 15 tasks + auto-start next in queue
- Level 7: Auto-queue 25 tasks + auto-optimize (cheapest resources)
- Level 10: Auto-queue 50 tasks + "Smart Queue" (AI suggestions)

**Automation Features:**

**Auto-Craft:**
- Set recipe and quantity
- System auto-crafts when resources available
- Continues until quantity reached or resources depleted

**Auto-Train:**
- Set pet and target level
- System auto-trains until level reached
- Continues across multiple sessions

**Auto-Breed:**
- Set breeding pairs and target offspring
- System auto-breeds when cooldown finished
- Continues until offspring matches criteria

**Auto-Refine:**
- Set raw material and quantity
- System auto-refines until quantity reached
- Continues until resources depleted

**Smart Queue (Level 10):**
- AI analyzes your goals (e.g., "train all fire pets to Level 50")
- Suggests optimal task queue
- One-click accept suggestion

**Construction:**
- Cost: 100,000 Gold + 7,500 Mixed Resources
- Time: 72 hours (3 days)
- Can demolish (50% refund)

**Max Level:** 10

---

## 🛠️ PHASE 4: UTILITY & ONGOING BUILDINGS

### **Phase 4 Overview**

**Timeline:** Ongoing / As-Needed  
**Building Count:** 2+ buildings  
**Target:** Variable levels  
**Purpose:** Quality-of-life and seasonal content

**Phase 4 Buildings:**
19. Fast Travel Hub *(Level 40, can be earlier)*
20. Event Billboard *(Level 1, always visible during events)*

---

### **19. Fast Travel Hub** 🌀

**Unlock:** Level 40 (or earlier via purchase)

**Primary Function:**
- Teleport between buildings instantly
- Fast travel to discovered biomes (from base)
- Convenience feature for large bases

**Why Phase 4:**
- Optional quality-of-life
- Can be added anytime based on player feedback
- Monetization opportunity (early unlock)

**Upgrade Benefits:**
- Level 1: Teleport to buildings only
- Level 3: Teleport to biomes (costs gold per use)
- Level 5: Reduced teleport cost (50% discount)
- Level 7: Unlock "Favorite Locations" (instant free teleport)
- Level 10: Unlimited free teleports

**Teleport Costs:**
- Within Base: 10 gold per teleport
- To Biome: 100 gold per teleport (from base to expedition start)

**Construction:**
- Cost: 20,000 Gold + 1,000 Crystals
- Time: 2 hours
- Can demolish (50% refund)
- **OR:** Purchase with 500 Premium Currency (instant unlock)

**Max Level:** 10

---

### **20. Event Billboard** 🎪

**Unlock:** Level 1 (Always Available During Events)

**Primary Function:**
- Display seasonal/holiday event information
- Accept event quests
- Redeem event currency for rewards
- Show event leaderboards

**Why Phase 4:**
- Seasonal content added regularly
- Temporary structure (appears/disappears with events)
- Keeps game fresh

**Event Types:**

**Seasonal Events:**
- Summer Festival (beach-themed pets, cosmetics)
- Halloween Spooktacular (ghost pets, scary decorations)
- Winter Wonderland (ice pets, snow decorations)
- Spring Bloom (flower pets, nature cosmetics)

**Limited-Time Events:**
- Double XP Weekend
- Legendary Spawn Rate Increase
- Crafting Material Bonanza
- Trading Fair (reduced auction fees)

**Competitive Events:**
- Pet Battle Tournament (PvP)
- Speed Run Challenge (fastest extraction)
- Rarest Capture Contest (who catches rarest pet)

**Event Currency:**
- Event Tokens (earned via event quests)
- Redeemable for exclusive pets, cosmetics, items
- Tokens expire when event ends (creates urgency)

**Construction:**
- Cost: FREE (auto-appears during events)
- Time: Instant
- Auto-demolishes when event ends

**Max Level:** N/A (does not upgrade)

---

## 🔓 BUILDING UNLOCK REQUIREMENTS SUMMARY

### **Quick Reference Table**

| Level Range | Buildings Unlocked | Total Buildings |
|-------------|-------------------|-----------------|
| 1-3 | Hub, Warehouse, Mailbox | 3 |
| 5-20 | Weaponsmith, Armorsmith, Training, Workshop, Breeding | 8 |
| 25-45 | Refinery, Sanctuary, Laboratory, Market, Trophy Hall | 13 |
| 50-70 | Daycare, Cosmetic Hub, Generator, Guild Hall, Automation | 18 |
| 40+ (Variable) | Fast Travel, Event Billboard | 20 |

---

## ⏱️ CONSTRUCTION TIME & COST OVERVIEW

### **Construction Times by Phase**

**Phase 1 Buildings (MVP):**
- Instant: Hub, Warehouse (tutorial)
- 5-10 minutes: Mailbox, Training, Workshop
- 10-15 minutes: Weaponsmith, Armorsmith
- 30 minutes: Breeding Station

**Phase 2 Buildings (Advanced):**
- 1-2 hours: Refinery
- 2-4 hours: Sanctuary
- 4-6 hours: Laboratory
- 6-8 hours: Market, Trophy Hall

**Phase 3 Buildings (Endgame):**
- 12-16 hours: Daycare, Cosmetic Hub
- 24-48 hours: Energy Generator, Guild Hall
- 72 hours (3 days): Automation Station

**Phase 4 Buildings:**
- 2 hours: Fast Travel Hub
- Instant: Event Billboard (auto-built)

**Why Tiered Construction Times?**
- Early buildings: Instant gratification (hook players)
- Mid buildings: Anticipation (creates log-in motivation)
- Late buildings: Commitment (shows dedication)
- Premium can skip (ethical monetization)

---

## 💰 CONSTRUCTION COST SCALING

**Early Buildings (Levels 1-20):**
- 0-3,000 Gold
- 50-200 basic resources
- Affordable for new players

**Mid Buildings (Levels 25-45):**
- 10,000-35,000 Gold
- 500-2,000 mixed resources
- Requires resource management

**Late Buildings (Levels 50-70):**
- 40,000-100,000 Gold
- 2,000-7,500 mixed resources
- Significant investment

**Premium Shortcuts:**
- Instant completion: 50-500 Premium Currency (depends on building)
- Early unlock (ignore level gate): 200-1,000 Premium Currency

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 3/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 3 of 10 (Core Production Buildings - Deep Dive)  
**Last Updated:** December 18, 2025

---

## 📋 PART 3 CONTENTS

**This document covers in-depth mechanics for:**
1. Weaponsmith (Complete System)
2. Armorsmith (Complete System)
3. Workshop (Complete System)
4. Refinery (Complete System)

Each building includes:
- Complete crafting recipe databases
- Resource requirements and scaling
- Crafting time formulas
- Upgrade benefits breakdown
- Balance tables
- Monetization integration
- Player progression curves

---

## ⚔️ WEAPONSMITH - COMPLETE SYSTEM

### **Core Philosophy**

The Weaponsmith is the **primary offensive progression system** for companion pets. Unlike traditional RPGs where weapons drop randomly, players **craft weapons intentionally** using resources gathered from specific biomes, creating a predictable and satisfying progression curve.

**Key Design Principles:**
- Weapons are **account-bound** (cannot trade to prevent pay-to-win)
- Higher-tier weapons require **biome-specific materials** (exploration incentive)
- Crafting is **time-gated** but never RNG-gated (no crafting failure)
- Upgrades are **incremental** (+10% damage per tier, not exponential)
- Elemental weapons provide **situational advantages** (not mandatory)

---

### **Weapon Categories & Stats**

**Six Weapon Types (Each Suited for Different Playstyles):**

| Weapon Type | Base Damage | Attack Speed | Special Property | Best For |
|-------------|-------------|--------------|------------------|----------|
| **Sword** | 100% | Medium | Balanced stats | General use, versatile |
| **Axe** | 130% | Slow | High single-target burst | Boss fights, single targets |
| **Bow** | 90% | Fast | Ranged combat bonus | Keeping distance, mobile |
| **Staff** | 110% | Medium | Elemental damage boost | Elemental pets, magic types |
| **Hammer** | 150% | Very Slow | Stun chance (10%) | Tank pets, crowd control |
| **Dagger** | 80% | Very Fast | Critical hit bonus (+15%) | Crit-focused builds, speed |

**Damage Calculation:**
```
Final Damage = (Pet Base Attack × Weapon Multiplier × Element Modifier) + Weapon Bonus Damage
```

**Example:**
- Pet has 100 base attack
- Equipped with Epic Fire Sword (+50 bonus damage, 100% multiplier)
- Fighting Water enemy (Fire advantage = 1.5x)
- Final Damage: (100 × 1.0 × 1.5) + 50 = **200 damage**

---

### **Weapon Rarity Tiers**

| Rarity | Damage Bonus | Additional Stats | Craft Time | Average Cost |
|--------|--------------|------------------|------------|--------------|
| **Common** | +10 | None | 5 minutes | 100 Gold + 50 materials |
| **Uncommon** | +25 | +5% Crit Chance | 15 minutes | 500 Gold + 150 materials |
| **Rare** | +50 | +10% Crit, +5% Speed | 30 minutes | 2,000 Gold + 500 materials |
| **Epic** | +100 | +15% Crit, +10% Speed, Element | 2 hours | 10,000 Gold + 2,000 materials |
| **Legendary** | +200 | +25% Crit, +15% Speed, Element, Special Effect | 12 hours | 50,000 Gold + 10,000 materials |

**Special Effects (Legendary Only):**
- **Lifesteal:** 10% of damage dealt heals pet
- **Chain Lightning:** Attacks bounce to nearby enemies (Fire/Lightning)
- **Freeze:** 20% chance to slow enemy (Ice)
- **Poison:** Deals damage over time (Nature)
- **Execute:** Bonus damage below 30% HP (Dark)

---

### **Complete Crafting Recipe Database**

#### **COMMON WEAPONS (Level 1 Weaponsmith)**

**Common Iron Sword**
- Materials: Iron Ore (×25), Wood (×10)
- Gold Cost: 100
- Craft Time: 5 minutes
- Stats: +10 Damage
- Requirements: None

**Common Wooden Bow**
- Materials: Wood (×30), String (×5)
- Gold Cost: 100
- Craft Time: 5 minutes
- Stats: +9 Damage, +5% Range
- Requirements: None

**Common Stone Axe**
- Materials: Stone (×20), Wood (×10)
- Gold Cost: 100
- Craft Time: 5 minutes
- Stats: +13 Damage, -10% Speed
- Requirements: None

**Common Staff (Beginner)**
- Materials: Wood (×15), Crystal Shard (×3)
- Gold Cost: 150
- Craft Time: 10 minutes
- Stats: +11 Damage, +5% Magic
- Requirements: None

**Common Hammer**
- Materials: Iron Ore (×30), Wood (×10)
- Gold Cost: 120
- Craft Time: 5 minutes
- Stats: +15 Damage, -15% Speed, 5% Stun
- Requirements: None

**Common Dagger**
- Materials: Iron Ore (×15), Leather (×5)
- Gold Cost: 100
- Craft Time: 5 minutes
- Stats: +8 Damage, +15% Speed, +5% Crit
- Requirements: None

---

#### **UNCOMMON WEAPONS (Level 2 Weaponsmith)**

**Uncommon Steel Sword**
- Materials: Steel Ingot (×10), Leather (×5)
- Gold Cost: 500
- Craft Time: 15 minutes
- Stats: +25 Damage, +5% Crit
- Requirements: Weaponsmith Level 2, Account Level 8

**Uncommon Reinforced Bow**
- Materials: Hardwood (×15), Silk String (×5), Steel (×5)
- Gold Cost: 500
- Craft Time: 15 minutes
- Stats: +23 Damage, +10% Range, +3% Crit
- Requirements: Weaponsmith Level 2, Account Level 8

**Uncommon Battle Axe**
- Materials: Steel Ingot (×15), Hardwood (×10)
- Gold Cost: 600
- Craft Time: 20 minutes
- Stats: +33 Damage, -8% Speed, +5% Crit
- Requirements: Weaponsmith Level 2, Account Level 8

**Uncommon Elemental Staff**
- Materials: Hardwood (×10), Elemental Crystal (×5), Gems (×3)
- Gold Cost: 700
- Craft Time: 25 minutes
- Stats: +28 Damage, +10% Magic, +5% Elemental
- Requirements: Weaponsmith Level 2, Account Level 8

**Uncommon War Hammer**
- Materials: Steel Ingot (×20), Iron Core (×3)
- Gold Cost: 650
- Craft Time: 20 minutes
- Stats: +38 Damage, -12% Speed, 8% Stun
- Requirements: Weaponsmith Level 2, Account Level 8

**Uncommon Twin Daggers**
- Materials: Steel Ingot (×10), Leather (×10), Sharpening Stone (×3)
- Gold Cost: 500
- Craft Time: 15 minutes
- Stats: +20 Damage, +20% Speed, +8% Crit
- Requirements: Weaponsmith Level 2, Account Level 8

---

#### **RARE WEAPONS (Level 3 Weaponsmith)**

**Rare Mithril Sword**
- Materials: Mithril Ingot (×8), Dragon Leather (×5), Enchanted Gem (×2)
- Gold Cost: 2,000
- Craft Time: 30 minutes
- Stats: +50 Damage, +10% Crit, +5% Speed
- Requirements: Weaponsmith Level 3, Account Level 15, Complete "Forge Master" Quest

**Rare Composite Bow**
- Materials: Ancient Wood (×10), Dragon Sinew (×3), Mithril (×5)
- Gold Cost: 2,000
- Craft Time: 30 minutes
- Stats: +45 Damage, +15% Range, +8% Crit, +5% Speed
- Requirements: Weaponsmith Level 3, Account Level 15

**Rare Berserker Axe**
- Materials: Bloodstone (×5), Mithril Ingot (×10), Obsidian (×3)
- Gold Cost: 2,500
- Craft Time: 45 minutes
- Stats: +65 Damage, -5% Speed, +12% Crit, Lifesteal 3%
- Requirements: Weaponsmith Level 3, Account Level 15

**Rare Archmage Staff**
- Materials: Ancient Wood (×8), Arcane Crystal (×5), Mana Essence (×10)
- Gold Cost: 2,200
- Craft Time: 40 minutes
- Stats: +55 Damage, +15% Magic, +10% Elemental, Mana Regen
- Requirements: Weaponsmith Level 3, Account Level 15

**Rare Titan Hammer**
- Materials: Titanium Ore (×15), Earth Core (×3), Giant Bone (×2)
- Gold Cost: 2,800
- Craft Time: 50 minutes
- Stats: +75 Damage, -10% Speed, 12% Stun, +10% Defense
- Requirements: Weaponsmith Level 3, Account Level 15

**Rare Assassin Blades**
- Materials: Shadow Steel (×8), Void Leather (×10), Poison Sac (×5)
- Gold Cost: 2,000
- Craft Time: 30 minutes
- Stats: +40 Damage, +25% Speed, +15% Crit, Poison Proc
- Requirements: Weaponsmith Level 3, Account Level 15

---

#### **EPIC WEAPONS (Level 5 Weaponsmith)**

**Epic Dragonforged Blade (Fire)**
- Materials: Dragon Scale (×10), Lava Core (×5), Mythril Ingot (×15), Phoenix Feather (×3)
- Gold Cost: 10,000
- Craft Time: 2 hours
- Stats: +100 Damage, +15% Crit, +10% Speed, Fire Element (+30% vs Ice)
- Special: Enemies burn for 5 seconds (DoT)
- Requirements: Weaponsmith Level 5, Account Level 30, Volcanic Rift Access

**Epic Frostbite Bow (Ice)**
- Materials: Frozen Wood (×15), Ice Crystal (×10), Mithril String (×5), Yeti Fur (×3)
- Gold Cost: 10,000
- Craft Time: 2 hours
- Stats: +90 Damage, +20% Range, +12% Crit, Ice Element (+30% vs Fire)
- Special: 20% chance to freeze enemy (2 seconds)
- Requirements: Weaponsmith Level 5, Account Level 30, Frosted Peaks Access

**Epic Earthshaker Axe (Earth)**
- Materials: Titan Stone (×20), Earth Essence (×8), Diamond Core (×3)
- Gold Cost: 12,000
- Craft Time: 3 hours
- Stats: +130 Damage, +18% Crit, Earth Element (+30% vs Lightning)
- Special: AOE shockwave on critical hit
- Requirements: Weaponsmith Level 5, Account Level 30, Mountain Depths Access

**Epic Stormcaller Staff (Lightning)**
- Materials: Thunderwood (×10), Storm Crystal (×12), Charged Rune (×5), Cloud Essence (×8)
- Gold Cost: 11,000
- Craft Time: 2.5 hours
- Stats: +110 Damage, +20% Magic, +15% Elemental, Lightning Element
- Special: Chain lightning to 2 nearby enemies
- Requirements: Weaponsmith Level 5, Account Level 30, Sky Citadel Access

**Epic Abyssal Hammer (Dark)**
- Materials: Void Stone (×25), Shadow Core (×5), Cursed Metal (×10)
- Gold Cost: 13,000
- Craft Time: 3 hours
- Stats: +150 Damage, -8% Speed, 15% Stun, Dark Element
- Special: Execute bonus (+50% damage below 30% HP)
- Requirements: Weaponsmith Level 5, Account Level 30, Shadow Realm Access

**Epic Phantom Daggers (Shadow)**
- Materials: Shadow Silk (×20), Void Steel (×12), Ghost Essence (×8)
- Gold Cost: 10,000
- Craft Time: 2 hours
- Stats: +80 Damage, +30% Speed, +25% Crit, Shadow Element
- Special: Invisibility on critical kill (3 seconds)
- Requirements: Weaponsmith Level 5, Account Level 30, Dark Forest Access

---

#### **LEGENDARY WEAPONS (Level 7+ Weaponsmith)**

**Legendary Excalibur (Holy Sword)**
- Materials: Celestial Steel (×20), Star Fragment (×10), Divine Essence (×15), Holy Water (×5)
- Gold Cost: 50,000
- Craft Time: 12 hours
- Stats: +200 Damage, +25% Crit, +15% Speed, Holy Element (all +20%)
- Special: Heal 15% HP on kill, Holy Smite (massive AOE ultimate)
- Requirements: Weaponsmith Level 7, Account Level 50, Complete "Divine Champion" Quest

**Legendary Ragnarok Bow (Apocalypse)**
- Materials: World Tree Wood (×25), Apocalypse Crystal (×15), Eternal String (×8)
- Gold Cost: 50,000
- Craft Time: 12 hours
- Stats: +180 Damage, +30% Range, +20% Crit, Multi-Element
- Special: Piercing shot (hits all enemies in line), explosive arrows
- Requirements: Weaponsmith Level 7, Account Level 50, Complete "Archer Supreme" Quest

**Legendary Godslayer Axe (Chaos)**
- Materials: Chaos Ore (×30), Reality Shard (×10), Primordial Essence (×20)
- Gold Cost: 60,000
- Craft Time: 16 hours
- Stats: +260 Damage, +30% Crit, Chaos Element (random advantage)
- Special: Reality Tear (ignores 50% defense), random elemental proc
- Requirements: Weaponsmith Level 7, Account Level 50, Complete "Chaos Warrior" Quest

**Legendary Infinity Staff (Arcane)**
- Materials: Astral Wood (×20), Infinity Gem (×12), Cosmic Dust (×25), Mana Singularity (×5)
- Gold Cost: 55,000
- Craft Time: 14 hours
- Stats: +220 Damage, +35% Magic, +25% Elemental, All Elements (+15%)
- Special: Infinite Mana (no cooldowns for 10s ultimate), spell echo (cast twice)
- Requirements: Weaponsmith Level 7, Account Level 50, Complete "Archmage" Quest

**Legendary World Breaker (Titan Hammer)**
- Materials: Titan Core (×40), Mountain Heart (×10), Earthquake Rune (×15)
- Gold Cost: 70,000
- Craft Time: 20 hours
- Stats: +300 Damage, -5% Speed, 25% Stun, Earth/Force Element
- Special: Earthquake AOE (stuns all enemies 3s), Ground Slam ultimate
- Requirements: Weaponsmith Level 7, Account Level 50, Complete "Titan Slayer" Quest

**Legendary Oblivion Blades (Void Daggers)**
- Materials: Void Heart (×25), Nothingness Shard (×20), Eternal Shadow (×30)
- Gold Cost: 50,000
- Craft Time: 12 hours
- Stats: +160 Damage, +40% Speed, +35% Crit, Void Element (ignores resistances)
- Special: Blink Strike (teleport behind enemy), Shadow Clone (summon duplicate)
- Requirements: Weaponsmith Level 7, Account Level 50, Complete "Shadow Master" Quest

---

### **Weapon Upgrade System**

**Existing weapons can be upgraded without re-crafting:**

**Upgrade Levels (All Rarities):**
- +1 Upgrade: +10% base stats, 500 Gold + 50% original materials
- +2 Upgrade: +20% base stats, 1,000 Gold + 75% original materials
- +3 Upgrade: +30% base stats, 2,000 Gold + 100% original materials
- +4 Upgrade: +40% base stats, 5,000 Gold + 150% original materials
- +5 Upgrade (MAX): +50% base stats, 10,000 Gold + 200% original materials

**Example:**
- Epic Dragonforged Blade (Base: +100 Damage)
- Upgraded to +5: +150 Damage (+50% increase)
- Total Cost: 18,500 Gold + massive material investment

**Why Upgrades Instead of New Weapons?**
- Respects player investment (keep favorite weapon)
- Reduces inventory bloat
- Creates long-term goals
- Allows for weapon attachment/bonding

---

### **Weaponsmith Building Upgrades (Full Breakdown)**

| Level | Crafting Slots | Speed Bonus | Unlocked Recipes | Cost to Upgrade | Time to Upgrade |
|-------|----------------|-------------|------------------|-----------------|-----------------|
| 1 | 1 slot | 0% | Common weapons | FREE (tutorial) | Instant |
| 2 | 2 slots | 0% | Uncommon weapons | 2,000 Gold + 200 materials | 30 minutes |
| 3 | 3 slots | +10% | Rare weapons | 5,000 Gold + 500 materials | 2 hours |
| 4 | 4 slots | +10% | (None, just efficiency) | 10,000 Gold + 1,000 materials | 6 hours |
| 5 | 5 slots | +20% | Epic weapons | 20,000 Gold + 2,500 materials | 12 hours |
| 6 | 5 slots | +20% | (None) | 35,000 Gold + 5,000 materials | 24 hours |
| 7 | 5 slots | +30% | Legendary weapons | 50,000 Gold + 10,000 materials | 48 hours |
| 8 | 5 slots | +30% | (None) | 75,000 Gold + 20,000 materials | 72 hours |
| 9 | 5 slots | +40% | (None) | 100,000 Gold + 35,000 materials | 5 days |
| 10 | 5 slots | +50% | Mythic weapons (future) | 200,000 Gold + 75,000 materials | 7 days |

**Level 10 Special Bonus:**
- Unlock "Weapon Reforging" (change weapon element without re-crafting)
- Unlock "Stat Rerolling" (reroll bonus stats, costs premium currency)

---

### **Resource Gathering Sources (Biome-Specific)**

**Common Materials (All Biomes):**
- Iron Ore, Wood, Stone, Leather
- Drop Rate: 20-40 per expedition

**Rare Materials (Specific Biomes):**
- Dragon Scale → Volcanic Rift (5% drop from Fire Dragons)
- Frozen Wood → Frosted Peaks (gather from frozen trees)
- Storm Crystal → Sky Citadel (10% drop from Lightning Elementals)
- Shadow Silk → Dark Forest (8% drop from Shadow Spiders)

**Legendary Materials (Endgame Biomes):**
- Celestial Steel → Heaven's Gate (1% drop from Celestial Guardians)
- Chaos Ore → Chaos Wastes (0.5% drop from Chaos Beasts)
- Void Heart → Abyssal Depths (0.3% drop from Void Lords)

**Material Farming Tips:**
- Higher rarity expeditions = better drop rates
- PvPvE mode = +50% material drops (risk vs reward)
- Laboratory research can increase drop rates (+10-20%)

---

### **Balance Philosophy**

**Damage Scaling Curve:**
```
Common Weapon (Level 1):   +10 Damage
Uncommon (Level 8):        +25 Damage (2.5x)
Rare (Level 15):           +50 Damage (5x)
Epic (Level 30):           +100 Damage (10x)
Legendary (Level 50):      +200 Damage (20x)
```

**This scaling is LINEAR, not exponential**, ensuring:
- Early weapons remain viable when upgraded
- New players aren't impossibly far behind veterans
- Skill matters more than gear

**Elemental Damage Philosophy:**
- Elemental advantage = +30% damage (significant but not required)
- Neutral matchups = 0% (no penalty)
- Elemental disadvantage = -15% damage (hurts but not crippling)
- Multi-element weapons = +15% vs all (jack-of-all-trades)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Instant Craft Tokens** (skip 12-hour legendary craft)
  - Cost: 100 Premium Currency per token
  - Does NOT grant better weapon, just saves time
  
- ✅ **Extra Crafting Slots** (beyond Level 10 cap)
  - Cost: 500 Premium Currency for permanent 6th slot
  - Convenience, not power
  
- ✅ **Cosmetic Weapon Skins** (appearance only)
  - Cost: 200-500 Premium Currency
  - Change visual appearance, zero stat changes
  - Examples: Flaming Sword Skin, Ice Crystal Bow Skin

**What CANNOT Be Purchased:**
- ❌ Better crafting success rates (no RNG anyway)
- ❌ Exclusive legendary weapons (all obtainable free)
- ❌ Bonus damage weapons (power = pay-to-win)
- ❌ Materials (must be gathered via gameplay)

---

### **Player Progression Timeline (Weapons)**

**Week 1 (Levels 1-10):**
- Craft first Common Sword (tutorial)
- Unlock Uncommon weapons (Level 8)
- Choose weapon type preference (experiment)

**Week 2-3 (Levels 10-20):**
- Craft first Rare weapon (milestone moment)
- Upgrade weapon to +1 or +2
- Start farming biome-specific materials

**Month 1 (Levels 20-30):**
- Unlock Epic weapons (Level 30)
- Craft first elemental weapon
- Optimize weapon for pet build

**Month 2-3 (Levels 30-50):**
- Farm materials for Legendary weapon
- Complete prerequisite quests
- Finally craft Legendary weapon (huge achievement)

**Endgame (Level 50+):**
- Upgrade Legendary weapon to +5 (months of effort)
- Collect all weapon types (completionist)
- Craft cosmetic variants for social prestige

---

## 🛡️ ARMORSMITH - COMPLETE SYSTEM

### **Core Philosophy**

The Armorsmith provides **defensive scaling** to match the Weaponsmith's offensive scaling. Armor is less about raw HP and more about **damage mitigation, elemental resistances, and utility buffs** (movement speed, stamina, etc.).

**Key Design Principles:**
- Armor is **account-bound** (cannot trade)
- Set bonuses reward **complete armor sets** (2-piece, 4-piece, 6-piece)
- Higher-tier armor requires **biome-specific leather/scales/fabrics**
- Armor does NOT have RNG stats (predictable crafting)
- Elemental resistances create **strategic loadout choices**

---

### **Armor Piece Types (Six Slots)**

| Armor Slot | Primary Stat | Secondary Stat | Special Property |
|------------|--------------|----------------|------------------|
| **Helmet** | +5% HP | +3% Defense | Vision enhancements (night vision, etc.) |
| **Chestplate** | +10% HP | +5% Defense | Core protection, highest defense |
| **Leggings** | +7% HP | +4% Defense | Movement speed bonuses |
| **Boots** | +5% Movement Speed | +2% Defense | Sprint duration, stamina bonuses |
| **Gloves** | +5% Attack Speed | +2% Defense | Faster weapon swings, gathering speed |
| **Cloak/Cape** | +10% Elemental Resist | +2% Defense | Elemental damage reduction |

**Full Set (All 6 Pieces):**
- +32% HP
- +20% Defense
- +10% Elemental Resist
- +5% Movement Speed
- +5% Attack Speed
- + Set Bonuses (explained below)

---

### **Armor Rarity Tiers**

| Rarity | Defense Bonus | Additional Stats | Craft Time | Average Cost |
|--------|---------------|------------------|------------|--------------|
| **Common** | +5 | None | 5 minutes | 100 Gold + 50 materials |
| **Uncommon** | +12 | +3% HP | 15 minutes | 500 Gold + 150 materials |
| **Rare** | +25 | +5% HP, +2% Speed | 30 minutes | 2,000 Gold + 500 materials |
| **Epic** | +50 | +10% HP, +5% Speed, Element Resist | 2 hours | 10,000 Gold + 2,000 materials |
| **Legendary** | +100 | +20% HP, +10% Speed, Element Resist, Special Effect | 12 hours | 50,000 Gold + 10,000 materials |

---

### **Set Bonuses (Matching Armor Pieces)**

**2-Piece Set Bonuses:**
- Common Set: +5% HP
- Uncommon Set: +8% HP
- Rare Set: +10% HP + 5% Defense
- Epic Set: +15% HP + 10% Defense
- Legendary Set: +25% HP + 15% Defense

**4-Piece Set Bonuses:**
- Common Set: +10% HP + 3% Defense
- Uncommon Set: +15% HP + 8% Defense
- Rare Set: +20% HP + 12% Defense + 5% Movement Speed
- Epic Set: +30% HP + 20% Defense + 10% Movement Speed
- Legendary Set: +40% HP + 30% Defense + 15% Movement Speed

**6-Piece Set Bonuses (Full Set):**
- Common Set: +15% HP + 5% Defense + "Iron Will" (reduce CC duration 10%)
- Uncommon Set: +25% HP + 12% Defense + "Stalwart" (reduce CC duration 20%)
- Rare Set: +35% HP + 20% Defense + 10% Movement Speed + "Resilience" (25% CC reduction)
- Epic Set: +50% HP + 35% Defense + 15% Movement Speed + "Elemental Mastery" (+30% chosen element resist)
- Legendary Set: +75% HP + 50% Defense + 25% Movement Speed + "Immortal Fortitude" (cheat death once per expedition)

**Special Set Effects (Legendary):**
- **Immortal Fortitude:** When fatal damage would kill you, survive with 1 HP and gain 5 seconds invincibility (once per expedition)

---

### **Complete Crafting Recipe Database (Armor)**

#### **COMMON ARMOR (Level 1 Armorsmith)**

**Common Leather Set (Full 6 Pieces):**
- Helmet: Leather (×15) + Thread (×5) = +3 Defense, +2% HP
- Chestplate: Leather (×25) + Thread (×10) = +6 Defense, +4% HP
- Leggings: Leather (×20) + Thread (×8) = +5 Defense, +3% HP
- Boots: Leather (×10) + Thread (×5) = +2 Defense, +3% Movement Speed
- Gloves: Leather (×10) + Thread (×5) = +2 Defense, +3% Attack Speed
- Cloak: Leather (×15) + Cloth (×5) = +3 Defense, +5% Elemental Resist

**Total Craft Time (Full Set):** 30 minutes (5 minutes × 6 pieces)  
**Total Cost:** 600 Gold + 95 Leather + 38 Thread + 5 Cloth

---

#### **UNCOMMON ARMOR (Level 2 Armorsmith)**

**Uncommon Steel Plate Set:**
- Helmet: Steel Ingot (×8) + Leather (×10) = +8 Defense, +4% HP
- Chestplate: Steel Ingot (×15) + Leather (×15) = +15 Defense, +8% HP
- Leggings: Steel Ingot (×12) + Leather (×12) = +12 Defense, +6% HP
- Boots: Steel Ingot (×6) + Leather (×8) = +6 Defense, +5% Movement Speed
- Gloves: Steel Ingot (×6) + Leather (×8) = +6 Defense, +5% Attack Speed
- Cloak: Steel Ingot (×5) + Silk (×10) = +8 Defense, +8% Elemental Resist

**Total Craft Time (Full Set):** 90 minutes (15 minutes × 6 pieces)  
**Total Cost:** 3,000 Gold + 52 Steel + 63 Leather + 10 Silk

---

#### **RARE ARMOR (Level 3 Armorsmith)**

**Rare Mithril Armor Set:**
- Helmet: Mithril Ingot (×5) + Dragon Leather (×8) + Enchanted Gem (×1) = +18 Defense, +8% HP, +2% Speed
- Chestplate: Mithril Ingot (×10) + Dragon Leather (×15) + Enchanted Gem (×2) = +30 Defense, +15% HP, +3% Speed
- Leggings: Mithril Ingot (×8) + Dragon Leather (×12) + Enchanted Gem (×1) = +25 Defense, +12% HP, +3% Speed
- Boots: Mithril Ingot (×4) + Dragon Leather (×8) + Speed Rune (×1) = +15 Defense, +8% Movement Speed
- Gloves: Mithril Ingot (×4) + Dragon Leather (×8) + Haste Rune (×1) = +15 Defense, +8% Attack Speed
- Cloak: Mithril Ingot (×3) + Elemental Silk (×15) = +20 Defense, +15% Elemental Resist

**Total Craft Time (Full Set):** 3 hours (30 minutes × 6 pieces)  
**Total Cost:** 12,000 Gold + 34 Mithril + 66 Dragon Leather + 5 Gems + 2 Runes + 15 Silk

---

#### **EPIC ARMOR (Level 5 Armorsmith)**

**Epic Dragonscale Armor Set (Fire Resistance):**
- Helmet: Red Dragon Scale (×8) + Lava Core (×3) + Fire Rune (×1) = +40 Defense, +12% HP, +5% Speed, +25% Fire Resist
- Chestplate: Red Dragon Scale (×15) + Lava Core (×8) + Fire Rune (×2) = +60 Defense, +20% HP, +8% Speed, +35% Fire Resist
- Leggings: Red Dragon Scale (×12) + Lava Core (×6) + Fire Rune (×1) = +50 Defense, +16% HP, +6% Speed, +30% Fire Resist
- Boots: Red Dragon Scale (×8) + Phoenix Feather (×5) = +35 Defense, +12% Movement Speed, +20% Fire Resist
- Gloves: Red Dragon Scale (×8) + Phoenix Feather (×5) = +35 Defense, +10% Attack Speed, +20% Fire Resist
- Cloak: Red Dragon Scale (×10) + Fire Silk (×20) = +45 Defense, +40% Fire Resist

**Total Craft Time (Full Set):** 12 hours (2 hours × 6 pieces)  
**Total Cost:** 60,000 Gold + 61 Dragon Scales + 22 Lava Cores + 4 Fire Runes + 10 Phoenix Feathers + 20 Fire Silk

**Set Bonus (Full Epic Dragonscale):**
- 6-Piece: Immune to Fire DoT effects, Fire attacks heal you for 10% damage

**Other Epic Sets:**
- Ice Armor (Frosted Peaks materials, +Ice Resist)
- Lightning Armor (Sky Citadel materials, +Lightning Resist)
- Nature Armor (Ancient Forest materials, +Nature Resist)
- Shadow Armor (Dark Forest materials, +Shadow Resist)
- Earth Armor (Mountain Depths materials, +Earth Resist)

---

#### **LEGENDARY ARMOR (Level 7+ Armorsmith)**

**Legendary Celestial Plate Set (Holy Armor):**
- Helmet: Celestial Steel (×10) + Star Fragment (×5) + Divine Essence (×8) = +80 Defense, +25% HP, +10% Speed, +30% All Resist
- Chestplate: Celestial Steel (×20) + Star Fragment (×12) + Divine Essence (×15) + Holy Water (×5) = +120 Defense, +40% HP, +15% Speed, +50% All Resist
- Leggings: Celestial Steel (×15) + Star Fragment (×10) + Divine Essence (×12) = +100 Defense, +30% HP, +12% Speed, +40% All Resist
- Boots: Celestial Steel (×10) + Angel Wing (×8) = +70 Defense, +20% Movement Speed, +25% All Resist
- Gloves: Celestial Steel (×10) + Angel Wing (×8) = +70 Defense, +15% Attack Speed, +25% All Resist
- Cloak: Celestial Steel (×12) + Celestial Silk (×30) = +90 Defense, +60% All Resist

**Total Craft Time (Full Set):** 72 hours (12 hours × 6 pieces)  
**Total Cost:** 300,000 Gold + 77 Celestial Steel + 35 Star Fragments + 35 Divine Essence + 5 Holy Water + 16 Angel Wings + 30 Celestial Silk

**Set Bonus (Full Legendary Celestial):**
- 6-Piece: "Immortal Fortitude" (survive fatal damage once per expedition with 1 HP + 5s invincibility), Regenerate 2% HP per second

**Other Legendary Sets:**
- Void Armor (Abyssal materials, teleportation abilities)
- Titan Armor (Mountain Heart materials, unstoppable CC immunity)
- Storm King Armor (Sky Citadel materials, lightning speed)
- Shadow Assassin Armor (Dark Forest materials, stealth bonuses)

---

### **Armor Upgrade System (Same as Weapons)**

- +1 to +5 Upgrade Levels
- Each upgrade: +10% base defense per level
- Full +5 Legendary Set = +50% base defense (massive investment)

---

### **Armorsmith Building Upgrades**

| Level | Crafting Slots | Speed Bonus | Unlocked Recipes | Cost to Upgrade | Time to Upgrade |
|-------|----------------|-------------|------------------|-----------------|-----------------|
| 1 | 1 slot | 0% | Common armor | 3,000 Gold (initial build) | 15 minutes |
| 2 | 2 slots | 0% | Uncommon armor | 2,500 Gold + 250 materials | 45 minutes |
| 3 | 3 slots | +10% | Rare armor | 6,000 Gold + 600 materials | 3 hours |
| 4 | 4 slots | +10% | (Efficiency) | 12,000 Gold + 1,200 materials | 8 hours |
| 5 | 5 slots | +20% | Epic armor | 25,000 Gold + 3,000 materials | 16 hours |
| 6 | 5 slots | +20% | (Efficiency) | 40,000 Gold + 6,000 materials | 30 hours |
| 7 | 5 slots | +30% | Legendary armor | 60,000 Gold + 12,000 materials | 60 hours |
| 8 | 5 slots | +30% | (Efficiency) | 90,000 Gold + 25,000 materials | 4 days |
| 9 | 5 slots | +40% | (Efficiency) | 120,000 Gold + 40,000 materials | 6 days |
| 10 | 5 slots | +50% | Mythic armor (future) | 250,000 Gold + 100,000 materials | 10 days |

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ Instant Craft Tokens (skip 12-hour waits)
- ✅ Extra Crafting Slots (6th permanent slot)
- ✅ Cosmetic Armor Skins (visual only, no stats)

**What CANNOT Be Purchased:**
- ❌ Better defense values
- ❌ Exclusive legendary armor
- ❌ Materials (must be gathered)

---

## 🧪 WORKSHOP - COMPLETE SYSTEM

### **Core Philosophy**

The Workshop produces **consumables** that provide temporary buffs, healing, or utility during expeditions. Unlike weapons/armor (permanent), consumables are **single-use items** that create a continuous resource sink and economy driver.

**Key Design Principles:**
- Consumables are **tradeable** (unlike weapons/armor)
- Batch crafting (e.g., 10 potions at once)
- Tiered potency (Small/Medium/Large/Epic/Legendary)
- Short craft times (1-60 minutes for batches)
- Strategic choices (which consumables to bring on expedition)

---

### **Consumable Categories**

**1. Health Restoration:**
- Small/Medium/Large Health Potions
- Instant Heal vs Heal Over Time (HoT)

**2. Buff Elixirs:**
- Strength (damage boost)
- Defense (damage reduction)
- Speed (movement/attack speed)
- Elemental (fire/ice/lightning damage boost)

**3. Utility Items:**
- Resurrection Scrolls (revive fainted pet)
- Teleport Crystals (emergency extraction)
- Invisibility Cloaks (stealth past enemies)
- Antidotes (remove poison/debuffs)

**4. Pet-Specific:**
- Pet Treats (restore pet HP mid-combat)
- Bond Boost Items (increase friendship faster)
- XP Elixirs (double training XP for 1 use)

**5. Capture Items:**
- Enhanced Capture Orbs (increase capture rate by 10-30%)
- Bait Items (lure rare pets to spawn)

---

### **Complete Crafting Recipe Database (Consumables)**

#### **HEALTH POTIONS**

**Small Health Potion (Batch of 10)**
- Materials: Healing Herbs (×30), Water (×10)
- Gold Cost: 100
- Craft Time: 1 minute
- Effect: Restore 25% HP, 30-second cooldown
- Requirements: Workshop Level 1

**Medium Health Potion (Batch of 10)**
- Materials: Healing Herbs (×50), Pure Water (×20), Honey (×10)
- Gold Cost: 500
- Craft Time: 5 minutes
- Effect: Restore 50% HP, 60-second cooldown
- Requirements: Workshop Level 2

**Large Health Potion (Batch of 5)**
- Materials: Ancient Herbs (×30), Spring Water (×20), Phoenix Ash (×5)
- Gold Cost: 2,000
- Craft Time: 15 minutes
- Effect: Restore 100% HP, 120-second cooldown
- Requirements: Workshop Level 3

**Epic Regeneration Potion (Batch of 3)**
- Materials: Elixir Herb (×20), Blessed Water (×15), Dragon Blood (×3)
- Gold Cost: 10,000
- Craft Time: 1 hour
- Effect: Restore 100% HP + 5% HP per second for 30 seconds
- Requirements: Workshop Level 5

**Legendary Immortality Elixir (Single)**
- Materials: World Tree Sap (×10), Eternal Essence (×5), Phoenix Heart (×1)
- Gold Cost: 50,000
- Craft Time: 4 hours
- Effect: Restore 100% HP, grant invincibility for 10 seconds
- Requirements: Workshop Level 7, Complete "Alchemist Master" Quest

---

#### **BUFF ELIXIRS**

**Strength Elixir (Batch of 5)**
- Materials: Bull Horn (×5), Fireflower (×10), Alcohol (×5)
- Gold Cost: 1,000
- Craft Time: 10 minutes
- Effect: +20% damage for 5 minutes
- Requirements: Workshop Level 2

**Defense Tonic (Batch of 5)**
- Materials: Iron Bark (×10), Stone Moss (×15), Clay (×10)
- Gold Cost: 1,000
- Craft Time: 10 minutes
- Effect: +20% defense for 5 minutes
- Requirements: Workshop Level 2

**Speed Potion (Batch of 5)**
- Materials: Swift Feather (×8), Wind Essence (×10), Sugar (×5)
- Gold Cost: 1,200
- Craft Time: 12 minutes
- Effect: +30% movement speed, +10% attack speed for 3 minutes
- Requirements: Workshop Level 2

**Elemental Infusion (Batch of 3)**
- Materials: Elemental Crystal (×10), Catalyst (×5), Element-Specific Reagent (×8)
- Gold Cost: 5,000
- Craft Time: 30 minutes
- Effect: +40% chosen elemental damage for 10 minutes
- Requirements: Workshop Level 3

**Hero's Might (Single)**
- Materials: Titan Blood (×5), Dragon Heart (×3), Divine Essence (×10)
- Gold Cost: 25,000
- Craft Time: 2 hours
- Effect: +50% damage, +30% defense, +20% speed for 15 minutes
- Requirements: Workshop Level 5

---

#### **UTILITY ITEMS**

**Resurrection Scroll (Batch of 3)**
- Materials: Sacred Parchment (×5), Holy Water (×10), Angel Feather (×3)
- Gold Cost: 3,000
- Craft Time: 20 minutes
- Effect: Revive fainted pet with 50% HP
- Requirements: Workshop Level 3

**Teleport Crystal (Single)**
- Materials: Warp Stone (×10), Mana Crystal (×15), Spatial Essence (×5)
- Gold Cost: 10,000
- Craft Time: 1 hour
- Effect: Instant extraction (emergency escape), cannot be used in PvP combat
- Requirements: Workshop Level 5

**Invisibility Cloak (Single)**
- Materials: Shadow Silk (×20), Void Essence (×10), Ghost Dust (×15)
- Gold Cost: 8,000
- Craft Time: 45 minutes
- Effect: 30 seconds invisibility (enemies can't detect you)
- Requirements: Workshop Level 4

**Antidote (Batch of 10)**
- Materials: Detox Herb (×30), Pure Water (×15)
- Gold Cost: 500
- Craft Time: 5 minutes
- Effect: Remove poison, burn, freeze, and other DoT effects
- Requirements: Workshop Level 2

---

#### **PET-SPECIFIC ITEMS**

**Pet Treat (Batch of 20)**
- Materials: Meat (×20), Honey (×10), Healing Herbs (×10)
- Gold Cost: 200
- Craft Time: 3 minutes
- Effect: Restore 30% pet HP (usable mid-combat)
- Requirements: Workshop Level 1

**Bond Boost Candy (Batch of 5)**
- Materials: Sugar (×10), Rainbow Essence (×5), Love Petals (×8)
- Gold Cost: 2,500
- Craft Time: 15 minutes
- Effect: Increase pet friendship by 10 points (permanent)
- Requirements: Workshop Level 3

**XP Elixir (Single)**
- Materials: Knowledge Essence (×10), Sage Herb (×15), Mana Potion (×5)
- Gold Cost: 5,000
- Craft Time: 30 minutes
- Effect: Double training XP for next training session (single use)
- Requirements: Workshop Level 4

---

#### **CAPTURE ITEMS**

**Enhanced Capture Orb (Batch of 5)**
- Materials: Capture Crystal (×10), Binding Essence (×8), Luck Charm (×5)
- Gold Cost: 3,000
- Craft Time: 20 minutes
- Effect: +10% capture rate for one pet
- Requirements: Workshop Level 3

**Master Capture Orb (Batch of 3)**
- Materials: Master Crystal (×15), Binding Rune (×10), Fortune Gem (×5)
- Gold Cost: 10,000
- Craft Time: 1 hour
- Effect: +30% capture rate for one pet (legendary viable)
- Requirements: Workshop Level 5

**Rare Pet Bait (Single)**
- Materials: Exotic Meat (×20), Rare Pheromone (×10), Lure Crystal (×5)
- Gold Cost: 15,000
- Craft Time: 2 hours
- Effect: Increase rare pet spawn chance by 50% for 30 minutes
- Requirements: Workshop Level 6

---

### **Workshop Building Upgrades**

| Level | Crafting Slots | Cost Discount | Unlocked Recipes | Cost to Upgrade | Time to Upgrade |
|-------|----------------|---------------|------------------|-----------------|-----------------|
| 1 | 1 slot | 0% | Basic consumables | 2,500 Gold (initial build) | 10 minutes |
| 2 | 2 slots | 0% | Medium potions, buffs | 2,000 Gold + 200 materials | 30 minutes |
| 3 | 3 slots | +10% | Rare consumables, utility | 5,000 Gold + 500 materials | 2 hours |
| 4 | 4 slots | +10% | Pet items, enhanced orbs | 10,000 Gold + 1,000 materials | 5 hours |
| 5 | 5 slots | +20% | Epic consumables, teleport crystals | 20,000 Gold + 2,500 materials | 10 hours |
| 6 | 5 slots | +20% | (Efficiency) | 35,000 Gold + 5,000 materials | 20 hours |
| 7 | 5 slots | +30% | Legendary consumables | 50,000 Gold + 10,000 materials | 40 hours |
| 8 | 5 slots | +30% | (Efficiency) | 75,000 Gold + 20,000 materials | 60 hours |
| 9 | 5 slots | +40% | (Efficiency) | 100,000 Gold + 35,000 materials | 4 days |
| 10 | 5 slots | +50% | Mythic consumables (future) | 150,000 Gold + 75,000 materials | 7 days |

**Level 10 Special Bonus:**
- Unlock "Batch Size Increase" (craft 2x quantity per batch)
- Unlock "No-Fail Crafting" (every craft produces +1 bonus item)

---

### **Consumable Economy & Trading**

**Why Consumables Are Tradeable:**
- Creates player-driven economy
- Allows specialization (dedicated alchemists)
- High-volume trading (unlike rare pets)
- Continuous demand (single-use items)

**Market Pricing Examples:**
- Small Health Potion: 15-20 Gold each
- Resurrection Scroll: 1,500-2,000 Gold each
- Teleport Crystal: 12,000-15,000 Gold each
- XP Elixir: 6,000-8,000 Gold each

**Profit Margins:**
- Crafting Cost: Materials + Gold + Time
- Market Sale Price: Usually 1.5x-2x crafting cost
- Profit: 50-100% ROI for dedicated crafters

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ Instant Craft Tokens (skip crafting time)
- ✅ Extra Crafting Slots (beyond Level 10)
- ✅ Recipe Book Bundles (unlock all recipes at once, no level gate)

**What CANNOT Be Purchased:**
- ❌ Consumables directly (must craft or trade with players)
- ❌ Better consumable effects (everyone's potions are equal)
- ❌ Materials (must gather)

---

## ⚗️ REFINERY - COMPLETE SYSTEM

### **Core Philosophy**

The Refinery transforms **raw materials → refined materials**, which are required for advanced crafting recipes. This creates a **two-tier resource economy**:
1. Raw materials (gathered from expeditions)
2. Refined materials (processed via Refinery)

**Key Design Principles:**
- Refining takes time (minutes to hours)
- Refining increases material VALUE (sell for more)
- Advanced recipes REQUIRE refined materials
- Batch processing for efficiency
- Economic choice: sell raw or refine first?

---

### **Refining Categories**

**1. Metals:**
- Raw Ore → Refined Ingots

**2. Textiles:**
- Plant Fibers → Cloth/Silk

**3. Gems:**
- Rough Stones → Polished Gems

**4. Leathers:**
- Raw Hide → Cured Leather

**5. Magical Materials:**
- Raw Essence → Purified Essence

---

### **Complete Refining Recipe Database**

#### **METAL REFINING**

**Iron Ingot (Batch of 5)**
- Input: Iron Ore (×15)
- Output: Iron Ingot (×5)
- Refine Time: 10 minutes
- Requirements: Refinery Level 1
- Value Increase: 10g per ore → 40g per ingot (2.67x profit)

**Steel Ingot (Batch of 3)**
- Input: Iron Ore (×15), Coal (×5)
- Output: Steel Ingot (×3)
- Refine Time: 30 minutes
- Requirements: Refinery Level 2
- Value Increase: 15g input → 80g per steel (5.33x profit)

**Mithril Ingot (Batch of 2)**
- Input: Mithril Ore (×10), Catalyst (×3)
- Output: Mithril Ingot (×2)
- Refine Time: 2 hours
- Requirements: Refinery Level 3
- Value Increase: 100g input → 400g per mithril (4x profit)

**Celestial Steel (Single)**
- Input: Mithril Ingot (×5), Star Fragment (×3), Divine Essence (×10)
- Output: Celestial Steel (×1)
- Refine Time: 6 hours
- Requirements: Refinery Level 7
- Value Increase: 2,500g input → 15,000g output (6x profit)

---

#### **TEXTILE REFINING**

**Cloth (Batch of 10)**
- Input: Plant Fiber (×50)
- Output: Cloth (×10)
- Refine Time: 5 minutes
- Requirements: Refinery Level 1
- Value Increase: 5g per fiber → 30g per cloth (6x profit)

**Silk (Batch of 5)**
- Input: Silk Thread (×25), Water (×10)
- Output: Silk (×5)
- Refine Time: 30 minutes
- Requirements: Refinery Level 2
- Value Increase: 20g per thread → 150g per silk (7.5x profit)

**Dragon Weave (Single)**
- Input: Dragon Scale (×5), Silk (×10), Fire Essence (×5)
- Output: Dragon Weave (×1)
- Refine Time: 3 hours
- Requirements: Refinery Level 5
- Value Increase: 1,500g input → 10,000g output (6.67x profit)

---

#### **GEM REFINING**

**Polished Gem (Batch of 5)**
- Input: Rough Gemstone (×10)
- Output: Polished Gem (×5)
- Refine Time: 15 minutes
- Requirements: Refinery Level 1
- Value Increase: 20g per rough → 60g per polished (3x profit)

**Refined Crystal (Batch of 3)**
- Input: Raw Crystal (×10), Polish Powder (×5)
- Output: Refined Crystal (×3)
- Refine Time: 1 hour
- Requirements: Refinery Level 3
- Value Increase: 100g per raw → 450g per refined (4.5x profit)

**Chaos Core (Single)**
- Input: Chaos Shard (×20), Stabilizer (×10)
- Output: Chaos Core (×1)
- Refine Time: 8 hours
- Requirements: Refinery Level 7
- Value Increase: 5,000g input → 50,000g output (10x profit)

---

#### **LEATHER REFINING**

**Cured Leather (Batch of 10)**
- Input: Raw Hide (×30), Salt (×10)
- Output: Cured Leather (×10)
- Refine Time: 10 minutes
- Requirements: Refinery Level 1
- Value Increase: 8g per hide → 35g per leather (4.38x profit)

**Dragon Leather (Batch of 3)**
- Input: Dragon Hide (×10), Tanning Oil (×5), Fire Essence (×3)
- Output: Dragon Leather (×3)
- Refine Time: 2 hours
- Requirements: Refinery Level 4
- Value Increase: 500g input → 2,500g per leather (5x profit)

---

#### **ESSENCE REFINING**

**Purified Essence (Batch of 5)**
- Input: Raw Essence (×20), Distilled Water (×10)
- Output: Purified Essence (×5)
- Refine Time: 30 minutes
- Requirements: Refinery Level 2
- Value Increase: 30g per raw → 180g per purified (6x profit)

**Divine Essence (Single)**
- Input: Purified Essence (×20), Holy Water (×10), Star Fragment (×3)
- Output: Divine Essence (×1)
- Refine Time: 6 hours
- Requirements: Refinery Level 6
- Value Increase: 5,000g input → 25,000g output (5x profit)

---

### **Refinery Building Upgrades**

| Level | Refining Slots | Speed Bonus | Unlocked Recipes | Cost to Upgrade | Time to Upgrade |
|-------|----------------|-------------|------------------|-----------------|-----------------|
| 1 | 1 slot | 0% | Basic refining (iron, cloth, gems) | 10,000 Gold (initial build) | 1 hour |
| 2 | 2 slots | 0% | Steel, silk, purified essence | 5,000 Gold + 500 materials | 2 hours |
| 3 | 3 slots | +10% | Mithril, refined crystals | 10,000 Gold + 1,000 materials | 4 hours |
| 4 | 4 slots | +10% | Dragon leather, advanced textiles | 20,000 Gold + 2,000 materials | 8 hours |
| 5 | 5 slots | +20% | Dragon weave, epic materials | 35,000 Gold + 5,000 materials | 16 hours |
| 6 | 5 slots | +20% | Divine essence, legendary components | 50,000 Gold + 10,000 materials | 32 hours |
| 7 | 5 slots | +30% | Celestial steel, chaos cores | 75,000 Gold + 20,000 materials | 48 hours |
| 8 | 5 slots | +30% | (Efficiency) | 100,000 Gold + 35,000 materials | 4 days |
| 9 | 5 slots | +40% | (Efficiency) | 150,000 Gold + 50,000 materials | 6 days |
| 10 | 5 slots | +50% | Mythic materials (future) | 250,000 Gold + 100,000 materials | 10 days |

**Level 10 Special Bonus:**
- Unlock "Perfect Refining" (10% chance of bonus output)
- Unlock "Mass Production" (craft 2x batch sizes)

---

### **Economic Strategy**

**When to Refine vs Sell Raw:**

**Sell Raw When:**
- You need immediate gold
- Market demand for raw materials is high
- You don't have time to wait for refining

**Refine When:**
- You need refined materials for crafting
- You want maximum profit (refining = 2-10x value)
- You're a dedicated crafter/trader

**Example Economic Scenario:**
- Gather 100 Iron Ore (worth 1,000 Gold raw)
- Refine to 33 Iron Ingots (worth 1,320 Gold refined)
- Further refine 15 ingots to 5 Steel Ingots (worth 400 Gold)
- **Total Value:** 1,200 Gold (ingots) + 400 Gold (steel) = 1,600 Gold (60% profit increase)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ Instant Refine Tokens (skip 8-hour legendary refines)
- ✅ Extra Refining Slots (6th permanent slot)
- ✅ Recipe Book Bundle (unlock all recipes)

**What CANNOT Be Purchased:**
- ❌ Refined materials directly (must refine or trade)
- ❌ Better refining ratios (everyone gets same output)
- ❌ Raw materials (must gather)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 4/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 4 of 10 (Pet Management Buildings - Deep Dive)  
**Last Updated:** December 18, 2025

---

## 📋 PART 4 CONTENTS

**This document covers in-depth mechanics for:**
1. Training Station (Complete System)
2. Breeding Station (Complete System)
3. Sanctuary (Complete System)
4. Pet Daycare (Complete System)

Each building includes:
- Complete mechanical systems
- Resource requirements and formulas
- Time calculations and scaling
- Upgrade benefits breakdown
- Balance tables
- Player progression curves
- Social integration features

---

## 🎓 TRAINING STATION - COMPLETE SYSTEM

### **Core Philosophy**

The Training Station is the **primary pet leveling system**, replacing traditional combat XP grinding with **intentional resource investment**. This design respects player time while maintaining engagement through strategic resource management.

**Key Design Principles:**
- Training is **100% predictable** (no RNG, guaranteed results)
- Resources are **biome-specific** (exploration incentive)
- Time investment is **real-world time** (creates daily engagement)
- Multiple pets can train **simultaneously** (scales with upgrades)
- Training is **offline-persistent** (respects casual players)

**Why This System Works:**
- ✅ No mindless grinding required
- ✅ Progress continues while offline
- ✅ Strategic resource allocation
- ✅ Multiple progression paths (combat vs pets)
- ✅ Mobile-friendly (set and forget)

---

### **Training Mechanics (Step-by-Step)**

#### **How Training Works:**

```
TRAINING FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. SELECT PET
   └─ Choose pet from roster (not currently deployed)

2. CHOOSE TRAINING TYPE
   ├─ Basic Training (Common materials, slow)
   ├─ Advanced Training (Rare materials, medium)
   └─ Elite Training (Epic materials, fast)

3. SET TARGET LEVEL
   ├─ Train to next level (1 level)
   ├─ Train multiple levels (up to +5)
   └─ Train to max (auto-calculate resources)

4. VIEW COSTS
   ├─ See required materials
   ├─ See gold cost
   └─ See time estimate

5. CONFIRM & START
   └─ Pet enters training (unavailable for expeditions)

6. WAIT (Offline or Online)
   └─ Timer counts down in real-time

7. COLLECT RESULTS
   ├─ Pet gains levels
   ├─ Stats increase
   └─ Return to roster
```

---

### **Training Types & Efficiency**

| Training Type | Material Rarity | Time Efficiency | Cost Efficiency | Best Use Case |
|---------------|-----------------|-----------------|-----------------|---------------|
| **Basic** | Common | Slow (100% base) | Cheap (100% base) | Early game, bulk training |
| **Advanced** | Rare | Medium (60% time) | Moderate (150% cost) | Mid-game optimization |
| **Elite** | Epic/Legendary | Fast (40% time) | Expensive (250% cost) | Endgame, rushing important pets |

**Example Comparison (Level 10 → 11 Rare Pet):**
- Basic Training: 60 minutes, 50 Common Materials, 100 Gold
- Advanced Training: 36 minutes, 30 Rare Materials, 150 Gold
- Elite Training: 24 minutes, 15 Epic Materials, 250 Gold

**Strategic Choice:**
- Use Basic for bulk training (20+ pets)
- Use Advanced for important pets
- Use Elite for urgent leveling (PvP tournament tomorrow)

---

### **Training Time Formula**

```
Base Training Time = (Pet Level × Rarity Multiplier × 2 minutes)

Rarity Multipliers:
- Common: 1.0x
- Uncommon: 1.5x
- Rare: 2.0x
- Epic: 3.0x
- Legendary: 5.0x

Modified by:
- Training Type (Basic 1.0x, Advanced 0.6x, Elite 0.4x)
- Training Station Level (up to -50% at Level 10)
- Laboratory Research (up to -20% with research)
```

**Examples:**

**Common Pet, Level 1 → 2:**
- Base: 1 × 1.0 × 2 = 2 minutes
- With Advanced Training: 2 × 0.6 = 1.2 minutes
- With Level 5 Station (-20%): 1.2 × 0.8 = ~1 minute

**Legendary Pet, Level 50 → 51:**
- Base: 50 × 5.0 × 2 = 500 minutes (8.3 hours)
- With Elite Training: 500 × 0.4 = 200 minutes (3.3 hours)
- With Level 10 Station (-50%): 200 × 0.5 = 100 minutes (1.7 hours)
- With Research (-20%): 100 × 0.8 = 80 minutes (1.3 hours)

**This scaling ensures:**
- Early levels are quick (minutes)
- Mid levels require planning (hours)
- Late levels are significant investment (days)
- But never feels punishing (always reducible with resources/upgrades)

---

### **Resource Requirements Formula**

```
Base Materials = (Pet Level × Rarity Multiplier × 5)

Rarity Multipliers:
- Common: 1.0x
- Uncommon: 2.0x
- Rare: 4.0x
- Epic: 8.0x
- Legendary: 15.0x

Gold Cost = Base Materials × 10

Modified by:
- Training Type (Basic 1.0x, Advanced 1.5x, Elite 2.5x)
- Training Station Level (up to -30% at Level 10)
- Laboratory Research (up to -15% with research)
```

**Examples:**

**Rare Pet, Level 20 → 21:**
- Base Materials: 20 × 4.0 × 5 = 400 materials
- Gold Cost: 400 × 10 = 4,000 Gold
- With Basic Training: 400 materials, 4,000 Gold
- With Advanced (1.5x cost but 40% faster): 600 rare materials, 6,000 Gold
- With Level 10 Station (-30%): 280 materials, 2,800 Gold

**Legendary Pet, Level 75 → 76:**
- Base Materials: 75 × 15.0 × 5 = 5,625 materials
- Gold Cost: 56,250 Gold
- With Elite Training (2.5x cost but 60% faster): 14,063 materials, 140,625 Gold
- With Max Upgrades (-45% total): 7,734 materials, 77,344 Gold

**Resource Balancing:**
- Early training is accessible (hundreds of materials)
- Late training requires preparation (thousands of materials)
- Creates natural "check-in" moments (can't train forever without expeditions)

---

### **Biome-Specific Training Materials**

Different pets benefit from **biome-specific materials** that reduce training costs:

| Pet Element | Preferred Biome | Material Name | Bonus Effect |
|-------------|-----------------|---------------|--------------|
| Fire | Volcanic Rift | Lava Essence | -25% training time & cost |
| Ice | Frosted Peaks | Frost Crystal | -25% training time & cost |
| Lightning | Sky Citadel | Storm Charge | -25% training time & cost |
| Nature | Ancient Forest | Life Bloom | -25% training time & cost |
| Earth | Mountain Depths | Stone Core | -25% training time & cost |
| Water | Coral Abyss | Tidal Pearl | -25% training time & cost |
| Shadow | Dark Forest | Void Essence | -25% training time & cost |
| Light | Heaven's Gate | Holy Radiance | -25% training time & cost |

**Example:**
- Training Fire Pet with Lava Essence: 100 minutes → 75 minutes, 1,000 materials → 750 materials
- Training Fire Pet with generic materials: 100 minutes, 1,000 materials (no bonus)

**Strategic Implication:**
- Players farm biomes matching their pet roster
- Encourages diverse pet collection
- Creates trading opportunities (excess materials)

---

### **Mass Training Feature (Level 10 Unlock)**

**At Training Station Level 10, unlock "Mass Training":**

**How It Works:**
1. Select multiple pets (up to 20)
2. Set target level for all
3. System calculates total resources
4. All pets train simultaneously (using all slots)
5. Complete in waves (if more than slot count)

**Example:**
- Player has 15 Common Pets at Level 10
- Wants to train all to Level 15
- Mass Training calculates: 22,500 materials, 225,000 Gold, 75 minutes each
- With 8 slots: Wave 1 (8 pets), Wave 2 (7 pets)
- Total time: 150 minutes (two waves)

**Why This Matters:**
- Endgame players have 50-100+ pets
- Manual training each one = tedious
- Mass Training = quality-of-life feature

---

### **Training Station Building Upgrades**

| Level | Training Slots | Time Reduction | Cost Reduction | Special Feature | Upgrade Cost | Upgrade Time |
|-------|----------------|----------------|----------------|-----------------|--------------|--------------|
| 1 | 1 slot | 0% | 0% | Basic Training only | 2,000 Gold (initial) | 5 minutes |
| 2 | 2 slots | -5% | -5% | Unlock Advanced Training | 3,000 Gold + 500 materials | 30 minutes |
| 3 | 3 slots | -10% | -10% | Unlock biome bonuses | 5,000 Gold + 1,000 materials | 2 hours |
| 4 | 4 slots | -15% | -15% | Unlock Elite Training | 10,000 Gold + 2,500 materials | 6 hours |
| 5 | 5 slots | -20% | -20% | Unlock "Training Queue" | 20,000 Gold + 5,000 materials | 12 hours |
| 6 | 6 slots | -25% | -25% | (Efficiency boost) | 35,000 Gold + 10,000 materials | 24 hours |
| 7 | 7 slots | -30% | -30% | Unlock "Auto-Train" | 50,000 Gold + 20,000 materials | 48 hours |
| 8 | 8 slots | -40% | -30% | (Efficiency boost) | 75,000 Gold + 35,000 materials | 72 hours |
| 9 | 8 slots | -45% | -30% | (Efficiency boost) | 100,000 Gold + 50,000 materials | 5 days |
| 10 | 8 slots | -50% | -30% | Unlock "Mass Training" | 150,000 Gold + 100,000 materials | 7 days |

**Special Features Explained:**

**Training Queue (Level 5):**
- Queue multiple training sessions per pet
- Example: Train Pet A 1→10, then 10→20, then 20→30
- Automatically starts next session when current finishes

**Auto-Train (Level 7):**
- Set target level for pet
- System automatically trains until target reached
- Deducts resources incrementally
- Continues even if you log off

**Mass Training (Level 10):**
- Train up to 20 pets simultaneously
- Bulk resource calculation
- One-click training for entire roster

---

### **Training Station Automation Integration**

**When paired with Automation Station (Level 70 unlock):**
- Auto-Train engages when resources available
- Smart resource allocation (prioritize important pets)
- Notifications when training completes
- One-click "Collect All" button

---

### **Player Progression Curve (Training)**

**Week 1 (Levels 1-10):**
- Train 3-5 companion pets to Level 10
- Training times: 1-5 minutes per level
- Learn training mechanics
- Discover biome material bonuses

**Month 1 (Levels 10-30):**
- Train main roster (10-15 pets) to Level 20-30
- Training times: 10-60 minutes per level
- Upgrade Training Station to Level 5 (5 slots)
- Begin using Advanced Training

**Month 2-3 (Levels 30-50):**
- Train core team (5-8 pets) to Level 50
- Training times: 1-4 hours per level
- Upgrade Training Station to Level 7 (Auto-Train)
- Begin using Elite Training for favorites

**Endgame (Levels 50-100):**
- Train legendary pets to Level 100
- Training times: 4-12 hours per level
- Training Station Level 10 (Mass Training)
- Optimize resource farming routes

---

### **Social Features (Training Station)**

**Leaderboards:**
- "Highest Level Pet" (global ranking)
- "Most Pets Trained" (volume ranking)
- Guild training competitions (weekly totals)

**Achievements:**
- "First Level 50 Pet" (rare achievement)
- "Train 100 Pets to Level 20+" (completionist)
- "Max Level Legendary" (prestige achievement)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Instant Training Tokens** (skip any training time)
  - Cost: 10-100 Premium Currency (scales with training time)
  - Does NOT grant better stats, just saves time
  
- ✅ **Extra Training Slots** (beyond Level 10 cap)
  - Cost: 500 Premium Currency for permanent 9th slot
  - Convenience, not power
  
- ✅ **Resource Bundle** (training materials only, not rare/legendary)
  - Cost: 200 Premium Currency for 1,000 common materials
  - Still requires expeditions for rare materials

**What CANNOT Be Purchased:**
- ❌ Bonus pet stats/IVs
- ❌ Faster training rates permanently
- ❌ Exclusive training recipes
- ❌ Rare/Legendary materials directly

---

## 🥚 BREEDING STATION - COMPLETE SYSTEM

### **Core Philosophy**

The Breeding Station enables **pet combination mechanics** through two primary systems:
1. **Star Merging** - Combine identical pets to increase star rating
2. **Breeding** - Combine different pets to create offspring with inherited traits

**Key Design Principles:**
- Breeding is **long-term investment** (days to weeks)
- IV inheritance creates **perfect pet hunting** (aspirational goals)
- Elemental hybrids add **strategic depth**
- Star merging provides **alternative progression** (beyond leveling)
- Breeding slots scale with upgrades (patience vs investment)

---

### **System 1: Star Merging**

#### **How Star Merging Works:**

```
STAR MERGING FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. SELECT TWO IDENTICAL PETS
   ├─ Same species (e.g., Fire Wolf + Fire Wolf)
   ├─ Same star rating (e.g., both ⭐⭐)
   └─ Any level (level doesn't matter)

2. CHOOSE MERGE OPTIONS
   ├─ Standard Merge (free, 24 hours)
   ├─ Rapid Merge (premium, instant)
   └─ Guaranteed IV Merge (premium, keep best IVs)

3. CONFIRM MERGE
   └─ Both pets consumed (cannot undo)

4. WAIT FOR TIMER
   └─ 24 hours real-time (offline-persistent)

5. RECEIVE RESULT
   ├─ One pet at +1 star rating (⭐⭐⭐)
   ├─ Level 1 (must re-train)
   ├─ Random IV selection from parents
   └─ Can immediately deploy or train
```

**Star Rating Progression:**
- ⭐ + ⭐ = ⭐⭐ (2-star)
- ⭐⭐ + ⭐⭐ = ⭐⭐⭐ (3-star)
- ⭐⭐⭐ + ⭐⭐⭐ = ⭐⭐⭐⭐ (4-star)
- ⭐⭐⭐⭐ + ⭐⭐⭐⭐ = ⭐⭐⭐⭐⭐ (5-star MAX)

**Why Star Merging Matters:**
- Higher star rating = **+10% base stats per star**
- 5-star pet at Level 50 = same power as 3-star pet at Level ~80
- Creates alternative progression (merge vs level)
- Gives purpose to duplicate pet captures

---

#### **Star Merging Time & Cost**

| Merge | Time (Standard) | Gold Cost | Result Star Rating | Stat Bonus |
|-------|-----------------|-----------|-------------------|------------|
| ⭐ → ⭐⭐ | 24 hours | 5,000 Gold | ⭐⭐ | +10% base stats |
| ⭐⭐ → ⭐⭐⭐ | 48 hours | 15,000 Gold | ⭐⭐⭐ | +20% base stats |
| ⭐⭐⭐ → ⭐⭐⭐⭐ | 72 hours | 50,000 Gold | ⭐⭐⭐⭐ | +30% base stats |
| ⭐⭐⭐⭐ → ⭐⭐⭐⭐⭐ | 7 days | 150,000 Gold | ⭐⭐⭐⭐⭐ | +40% base stats |

**Time Reduction (Breeding Station Upgrades):**
- Level 1: 100% time (default)
- Level 3: 80% time (5 days → 4 days for 5-star)
- Level 5: 60% time (5 days → 3 days)
- Level 7: 40% time (5 days → 2 days)
- Level 10: 25% time (5 days → 1.25 days = 30 hours)

**Economic Investment (5-Star Pet from Scratch):**
- Capture 32 identical 1-star pets
- Merge 16 pairs → 16 two-star pets (24h each = 16 days)
- Merge 8 pairs → 8 three-star pets (48h each = 16 days)
- Merge 4 pairs → 4 four-star pets (72h each = 12 days)
- Merge 2 pairs → 2 five-star pets (7d each = 14 days)
- **Total Time:** ~58 days (with Level 1 Breeding Station)
- **Total Time:** ~14 days (with Level 10 Breeding Station)
- **Total Cost:** 1,360,000 Gold

**This massive investment ensures:**
- 5-star pets feel incredibly valuable
- Creates long-term goals
- Respects player effort (not RNG gambling)

---

### **System 2: Breeding (Cross-Species)**

#### **How Breeding Works:**

```
BREEDING FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. SELECT TWO DIFFERENT PETS (Parents)
   ├─ Can be different species (Wolf + Dragon)
   ├─ Can be different elements (Fire + Ice)
   └─ Any star rating/level

2. VIEW BREEDING PREVIEW
   ├─ Possible offspring species (genetic pool)
   ├─ Possible elements (parent elements + hybrids)
   ├─ IV inheritance probability
   └─ Breeding time & cost

3. CONFIRM BREEDING
   ├─ Both parents stay in roster (not consumed)
   ├─ Cannot breed same parents again for 7 days (cooldown)
   └─ Pay gold cost

4. WAIT FOR GESTATION
   └─ 1-14 days (depends on parent rarity)

5. HATCH EGG
   ├─ Receive offspring pet
   ├─ Random species from parent pool
   ├─ IV inherited from parents
   └─ Element determined by parents

6. RAISE OFFSPRING
   ├─ Starts at Level 1
   ├─ Train normally
   └─ Can breed again after maturity
```

---

#### **Breeding Time Formula**

```
Base Breeding Time = (Parent 1 Rarity + Parent 2 Rarity) × 1 day

Rarity Values:
- Common: 1 day
- Uncommon: 2 days
- Rare: 3 days
- Epic: 5 days
- Legendary: 7 days

Examples:
- Common + Common = 2 days
- Rare + Rare = 6 days
- Legendary + Legendary = 14 days
- Common + Legendary = 8 days (mixed)

Modified by:
- Breeding Station Level (up to -75% at Level 10)
- Laboratory Research (up to -20%)
```

**Examples with Max Upgrades:**
- Common + Common: 2 days → 0.4 days (10 hours)
- Rare + Rare: 6 days → 1.2 days (29 hours)
- Legendary + Legendary: 14 days → 2.8 days (67 hours)

---

#### **IV Inheritance System**

**Each pet has 6 IVs (Individual Values):**
- HP IV (0-31)
- Attack IV (0-31)
- Defense IV (0-31)
- Speed IV (0-31)
- Special Attack IV (0-31)
- Special Defense IV (0-31)

**Inheritance Mechanics:**
- Each IV has **50% chance** to come from Parent 1, 50% from Parent 2
- **5% chance** of "Perfect Roll" (automatic 31 IV regardless of parents)
- **Destiny Knot Item** (rare drop): Guarantees offspring inherits 5 IVs from parents (not random)

**Example:**
- Parent 1: HP 25, ATK 31, DEF 20, SPD 15, SP.ATK 28, SP.DEF 22
- Parent 2: HP 18, ATK 22, DEF 31, SPD 28, SP.ATK 15, SP.DEF 30
- Offspring: 
  - HP: 50% → Parent 2 (18)
  - ATK: 50% → Parent 1 (31) ✓
  - DEF: 50% → Parent 2 (31) ✓
  - SPD: 50% → Parent 1 (15)
  - SP.ATK: 5% Perfect Roll → (31) ✓
  - SP.DEF: 50% → Parent 2 (30)

**Perfect Pet Hunting:**
- Breeding two 6×31 IV pets still only gives ~50% chance of 6×31 offspring
- Requires multiple breeding attempts (RNG chase)
- Creates aspirational endgame goal
- Trading market for high IV pets

---

#### **Elemental Hybrid System**

**When breeding different elements, offspring can be:**

**Pure Element (50% chance each parent):**
- Fire Parent + Water Parent = Fire Offspring OR Water Offspring

**Hybrid Element (20% chance if parents differ):**
- Fire + Water = **Steam** (hybrid element)
- Fire + Earth = **Magma** (hybrid element)
- Water + Ice = **Frost** (hybrid element)
- Lightning + Wind = **Storm** (hybrid element)

**Neutral Element (5% chance):**
- Any Parent + Any Parent = **Arcane** (neutral, no weakness)

**Hybrid Element Advantages:**
- Dual type advantages (Steam beats Fire AND Earth)
- Unique visual aesthetics (cool factor)
- Rarer than pure elements (prestige)
- Stronger in PvP (versatility)

**Complete Hybrid Chart:**

| Parent 1 | Parent 2 | Hybrid Result | Type Advantages |
|----------|----------|---------------|-----------------|
| Fire | Water | Steam | Fire, Earth |
| Fire | Earth | Magma | Ice, Nature |
| Fire | Lightning | Plasma | Water, Metal |
| Water | Ice | Frost | Fire, Ground |
| Water | Nature | Swamp | Fire, Rock |
| Earth | Lightning | Crystal | Flying, Fire |
| Ice | Wind | Blizzard | Nature, Ground |
| Shadow | Light | Twilight | Shadow, Light (self) |
| Any | Any | Arcane (5%) | None (neutral) |

---

#### **Breeding Cost & Cooldowns**

| Parent Rarity Combo | Gold Cost | Breeding Time | Cooldown (Same Pair) |
|---------------------|-----------|---------------|----------------------|
| Common + Common | 2,000 Gold | 2 days | 3 days |
| Uncommon + Uncommon | 5,000 Gold | 4 days | 5 days |
| Rare + Rare | 15,000 Gold | 6 days | 7 days |
| Epic + Epic | 50,000 Gold | 10 days | 10 days |
| Legendary + Legendary | 150,000 Gold | 14 days | 14 days |

**Cooldown Explanation:**
- Same two parents cannot breed again for X days
- Prevents breeding exploits (spam same pair)
- Encourages diverse breeding experiments
- Can breed different pairs simultaneously

---

### **Breeding Station Building Upgrades**

| Level | Breeding Slots | Time Reduction | Unlocked Features | Upgrade Cost | Upgrade Time |
|-------|----------------|----------------|-------------------|--------------|--------------|
| 1 | 1 slot | 0% | Basic merging/breeding | 5,000 Gold (initial) | 30 minutes |
| 2 | 2 slots | -10% | Unlock rare hybrids | 5,000 Gold + 1,000 materials | 2 hours |
| 3 | 3 slots | -20% | Unlock IV preview | 10,000 Gold + 2,500 materials | 6 hours |
| 4 | 3 slots | -30% | (Efficiency boost) | 20,000 Gold + 5,000 materials | 12 hours |
| 5 | 4 slots | -40% | Unlock epic hybrids | 40,000 Gold + 10,000 materials | 24 hours |
| 6 | 4 slots | -50% | (Efficiency boost) | 60,000 Gold + 20,000 materials | 48 hours |
| 7 | 5 slots | -60% | Unlock legendary hybrids | 90,000 Gold + 35,000 materials | 72 hours |
| 8 | 5 slots | -65% | Unlock "Breed Queue" | 120,000 Gold + 50,000 materials | 5 days |
| 9 | 5 slots | -70% | (Efficiency boost) | 180,000 Gold + 75,000 materials | 7 days |
| 10 | 5 slots | -75% | Unlock "Guaranteed IV" | 250,000 Gold + 150,000 materials | 10 days |

**Special Features:**

**IV Preview (Level 3):**
- Before confirming breed, see IV ranges
- Shows "Best Case" and "Worst Case" outcomes
- Helps decide if breeding pair is worth it

**Breed Queue (Level 8):**
- Queue multiple breeding pairs
- Automatically starts next when slot opens
- Example: Queue 5 pairs, they breed sequentially

**Guaranteed IV (Level 10):**
- Choose one IV to guarantee as 31
- Costs 50,000 Gold extra per breed
- Reduces RNG for perfect pets

---

### **Breeding Achievements & Goals**

**Completionist Goals:**
- "Elemental Master" - Breed all 8 pure elements
- "Hybrid Collector" - Breed all 15 hybrid elements
- "Perfect Breeder" - Breed a 6×31 IV pet
- "5-Star Legend" - Create a 5-star Legendary pet
- "Genetic Savant" - Breed 100 offspring total

**These achievements unlock:**
- Exclusive pet skins
- Breeding Station cosmetics
- Title badges
- Trophy Hall displays

---

### **Social Features (Breeding)**

**Breeding Leaderboards:**
- "Highest IV Pet" (sum of all IVs)
- "Most Hybrids Bred"
- "Fastest 5-Star Creation"

**Trading Market:**
- High IV pets are VERY valuable
- Perfect IV pets sell for 500,000+ Gold
- 5-star pets are premium items
- Hybrid elements are sought after

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Instant Hatch Tokens** (skip breeding timer)
  - Cost: 50-500 Premium Currency (scales with time)
  - Does NOT improve IVs, just saves time
  
- ✅ **Destiny Knot Item** (guaranteed 5 IV inheritance)
  - Cost: 200 Premium Currency OR rare drop
  - Consumable, one-time use
  
- ✅ **Extra Breeding Slot** (6th permanent slot)
  - Cost: 1,000 Premium Currency
  - Convenience, not power

**What CANNOT Be Purchased:**
- ❌ Perfect IV pets directly
- ❌ Guaranteed hybrid outcomes
- ❌ Exclusive legendary species
- ❌ Bypass cooldown timers

---

## 🏛️ SANCTUARY - COMPLETE SYSTEM

### **Core Philosophy**

The Sanctuary is a **pet collection showcase** where players display their favorite pets, organize their roster, and earn passive bonuses. It serves both functional (organization) and social (prestige) purposes.

**Key Design Principles:**
- Display is **curated by player** (choose which pets to showcase)
- Displayed pets provide **passive bonuses** (reward collection)
- Social feature (friends can tour Sanctuary)
- Organizational tool (sort/filter large rosters)
- Achievement tracker (collection progress)

---

### **Sanctuary Core Features**

#### **Display System**

**How Display Works:**
1. Player selects pets from roster
2. Pets appear in trophy cases/pedestals
3. Can view detailed stats by clicking pet
4. Can rearrange display order
5. Can filter by element/rarity/favorites

**Display Capacity:**
- Level 1: 20 pets displayed
- Level 5: 75 pets displayed
- Level 10: 150 pets displayed
- Premium Expansion: +50 slots (200 total)

**Visual Presentation:**
- Pets appear in 3D on pedestals
- Animated idle animations
- Elemental effects (fire pets glow, ice pets shimmer)
- Name plates with stats
- Star rating displayed

---

#### **Organizational Tools**

**Sorting Options:**
- By Element (Fire, Water, Earth, etc.)
- By Rarity (Common → Legendary)
- By Star Rating (⭐ → ⭐⭐⭐⭐⭐)
- By Level (1 → 100)
- By Capture Date (Newest/Oldest)
- By IV Total (Perfect → Worst)
- By Favorites (manually tagged)

**Filter Options:**
- Show only specific element
- Show only specific rarity
- Show only 5-star pets
- Show only Level 50+ pets
- Show only hybrids
- Show only shinies/cosmetics

**Search Function:**
- Search by species name
- Search by element
- Search by minimum IV
- Search by level range

**Why This Matters:**
- Endgame players have 200+ pets
- Finding specific pet takes minutes
- Sanctuary = instant access
- Quality-of-life feature

---

### **Passive Bonus System**

**Displayed pets grant account-wide bonuses:**

| Unique Species Displayed | Gold Bonus | XP Bonus | Capture Rate Bonus | Other Bonuses |
|-------------------------|------------|----------|-------------------|---------------|
| 10 species | +2% | 0% | 0% | None |
| 25 species | +5% | +2% | 0% | None |
| 50 species | +10% | +5% | +2% | Unlock "Collector" title |
| 75 species | +12% | +8% | +4% | +5% material drop rate |
| 100 species | +15% | +10% | +5% | +10% material drop rate |
| 125 species | +18% | +12% | +7% | Unlock rare cosmetics |
| 150 species | +20% | +15% | +10% | Unlock "Master Collector" title |

**Important Notes:**
- Bonuses require **unique species** (not just total count)
- 10 Fire Wolves = 1 unique species
- 10 different species = 10 unique species
- Encourages diverse collection (gotta catch 'em all)

**Bonus Stacking:**
- Sanctuary bonuses stack with Laboratory research
- Example: 15% Sanctuary + 10% Lab = 25% gold bonus
- Creates multiplicative power curve

---

### **Collection Progress Tracker**

**Built-in Pokédex-style tracker:**

**Species Checklist:**
- Shows all 200+ species in game
- Marks captured (✓) vs uncaptured (—)
- Shows capture locations (biome hints)
- Tracks variants (shiny, hybrid, etc.)

**Completion Rewards:**
- 25% Species: Rare Cosmetic Unlock
- 50% Species: Epic Pet Egg
- 75% Species: Legendary Pet Egg
- 100% Species: Mythic Title + Exclusive Mount

**Rarity Progress:**
- X/50 Common Species
- X/40 Uncommon Species
- X/30 Rare Species
- X/20 Epic Species
- X/10 Legendary Species

---

### **Social Features (Sanctuary)**

**Friend Visits:**
- Friends can tour your Sanctuary (read-only)
- See your displayed pets
- View pet stats (if you allow)
- Leave "kudos" (likes/reactions)
- Compare collections ("I have X species, you have Y")

**Public Leaderboards:**
- "Most Unique Species"
- "Most 5-Star Pets"
- "Most Perfect IV Pets"
- "Most Legendary Pets"

**Guild Sanctuary:**
- Guild can have shared Sanctuary
- Top members' pets displayed
- Guild collection progress tracker

---

### **Sanctuary Building Upgrades**

| Level | Display Capacity | Passive Bonus Multiplier | Special Features | Upgrade Cost | Upgrade Time |
|-------|------------------|--------------------------|------------------|--------------|--------------|
| 1 | 20 pets | 1.0x | Basic display | 15,000 Gold (initial) | 2 hours |
| 2 | 30 pets | 1.0x | Unlock sorting | 10,000 Gold + 2,000 materials | 4 hours |
| 3 | 40 pets | 1.1x | Unlock filters | 20,000 Gold + 5,000 materials | 8 hours |
| 4 | 50 pets | 1.1x | Unlock search | 35,000 Gold + 10,000 materials | 16 hours |
| 5 | 75 pets | 1.2x | Unlock Pokédex tracker | 50,000 Gold + 20,000 materials | 32 hours |
| 6 | 85 pets | 1.2x | (Efficiency boost) | 75,000 Gold + 35,000 materials | 48 hours |
| 7 | 100 pets | 1.3x | Unlock "Favorites" category | 100,000 Gold + 50,000 materials | 72 hours |
| 8 | 120 pets | 1.3x | (Efficiency boost) | 150,000 Gold + 75,000 materials | 5 days |
| 9 | 135 pets | 1.4x | (Efficiency boost) | 200,000 Gold + 100,000 materials | 7 days |
| 10 | 150 pets | 1.5x | Unlock "Pet Statues" (decorative) | 300,000 Gold + 200,000 materials | 10 days |

**Passive Bonus Multiplier Explanation:**
- Level 1: Bonuses as listed (e.g., 50 species = +10% gold)
- Level 10: Bonuses × 1.5 (e.g., 50 species = +15% gold)
- Encourages upgrading Sanctuary (not just unlocking it)

---

### **Pet Statues Feature (Level 10)**

**Commemorative Statues:**
- Create permanent statue of favorite pet
- Place in base as decoration
- Shows pet's best achievement (first legendary, highest level, etc.)
- Friends can interact with statue (read inscription)

**Statue Types:**
- Bronze: Uncommon pets
- Silver: Rare pets
- Gold: Epic pets
- Platinum: Legendary pets
- Diamond: Perfect IV pets

**Statue Costs:**
- 10,000 Gold + 5,000 materials per statue
- Unlimited statues (limited by plot decorations)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Extra Display Slots** (+50 permanent slots)
  - Cost: 500 Premium Currency
  - Convenience for collectors
  
- ✅ **Sanctuary Themes** (visual customization)
  - Cost: 200-400 Premium Currency
  - Examples: Crystal Cave, Fire Temple, Ice Palace
  - Zero gameplay impact
  
- ✅ **Pet Statue Packs** (decorative only)
  - Cost: 300 Premium Currency for 5 statues
  - Saves gold, not power

**What CANNOT Be Purchased:**
- ❌ Passive bonus increases
- ❌ Exclusive species unlocks
- ❌ Automatic collection completion

---

## 🐾 PET DAYCARE - COMPLETE SYSTEM

### **Core Philosophy**

The Pet Daycare is a **"living museum"** where pets roam freely, interact with each other, and can be directly engaged with through minigames and petting. This is primarily an **aesthetic and social feature** rather than a functional progression system.

**Key Design Principles:**
- Pets are **visibly alive** (walking, playing, sleeping)
- Players can **interact directly** (pet, feed, play)
- Social showcase (friends see your pets happy)
- Screenshot opportunities (social media content)
- Emotional bonding (see pets as companions, not tools)

---

### **Daycare Core Features**

#### **Living Environment System**

**How Daycare Works:**
1. Select up to 50 pets to display in Daycare
2. Pets appear in open playground area
3. Pets autonomously walk, play, interact
4. Click any pet to interact (pet, feed, play minigame)
5. Pets remember players (return visitors get excited greeting)

**Pet Behaviors (Autonomous AI):**
- **Wandering:** Pets walk around randomly
- **Playing:** Two pets chase each other
- **Sleeping:** Pets curl up and rest
- **Eating:** Pets approach food bowls
- **Socializing:** Pets nuzzle/interact with others
- **Exploring:** Pets investigate toys/obstacles

**Environmental Features:**
- Grass terrain with trees
- Toy balls and obstacles
- Food/water bowls
- Benches for players to sit
- Weather effects (rain, snow, sunshine)

---

#### **Interactive Features**

**Player-Pet Interactions:**

**1. Petting:**
- Click pet to pet them
- Pet animation plays (player hand petting pet)
- Pet reacts happily (wag tail, purr, glow)
- Increases friendship by 1 point

**2. Feeding Treats:**
- Use treats from Workshop
- Pet eats treat (eating animation)
- Restores pet's "happiness" meter
- Increases friendship by 2 points

**3. Playing Minigames:**
- **Fetch:** Throw ball, pet retrieves (timing minigame)
- **Hide & Seek:** Find hidden pet (exploration minigame)
- **Race:** Race pet around track (button-mashing minigame)
- **Puzzle:** Complete puzzle with pet (logic minigame)
- Rewards: Friendship +5, small gold reward

**4. Taking Photos:**
- Screenshot mode (remove UI)
- Pose pets (click to make sit/stand/action)
- Filters (sepia, black & white, brightness)
- Share to social media directly

---

#### **Friendship & Bonding System**

**Each pet has "Friendship" stat (0-100):**

**Friendship Benefits:**
- 25 Friendship: Pet learns "Happy Emote" (visual effect in combat)
- 50 Friendship: Pet gains +5% stats in combat
- 75 Friendship: Pet learns unique "Bond Move" (special ability)
- 100 Friendship (MAX): Pet evolves appearance (shiny/cosmetic variant)

**Increasing Friendship:**
- Petting: +1 per interaction (cooldown: 1 hour)
- Feeding Treats: +2 per treat
- Playing Minigames: +5 per game (cooldown: 30 minutes)
- Winning Battles Together: +1 per victory
- Time in Daycare: +1 per 24 hours

**Friendship Decay:**
- Friendship does NOT decay (permanent progress)
- But benefits only apply to pets in active roster or Daycare

---

### **Social Features (Daycare)**

**Friend Visits:**
- Friends can visit your Daycare (read-only)
- See your pets playing together
- Can pet your pets (with permission)
- Leave "kudos" on favorite pets
- Take screenshots of your Daycare

**Daycare Competitions:**
- Weekly "Happiest Pet" contest (highest friendship)
- Monthly "Best Daycare" (most kudos from visitors)
- Prizes: Cosmetics, pet treats, gold

---

### **Pet Daycare Building Upgrades**

| Level | Display Capacity | Environment Size | Special Features | Upgrade Cost | Upgrade Time |
|-------|------------------|------------------|------------------|--------------|--------------|
| 1 | 5 pets | Small (20×20) | Basic animations | 40,000 Gold (initial) | 12 hours |
| 2 | 10 pets | Small | Unlock petting | 20,000 Gold + 5,000 materials | 16 hours |
| 3 | 15 pets | Medium (30×30) | Pets interact with each other | 40,000 Gold + 10,000 materials | 24 hours |
| 4 | 20 pets | Medium | Unlock feeding treats | 60,000 Gold + 20,000 materials | 36 hours |
| 5 | 25 pets | Large (40×40) | Unlock animations (play, sleep, eat) | 90,000 Gold + 35,000 materials | 48 hours |
| 6 | 30 pets | Large | (Capacity boost) | 120,000 Gold + 50,000 materials | 72 hours |
| 7 | 40 pets | Very Large (50×50) | Unlock minigames (fetch, puzzle) | 180,000 Gold + 75,000 materials | 5 days |
| 8 | 45 pets | Very Large | (Capacity boost) | 240,000 Gold + 100,000 materials | 7 days |
| 9 | 50 pets | Very Large | (Capacity boost) | 320,000 Gold + 150,000 materials | 10 days |
| 10 | 50 pets | Massive (60×60) | Unlock "Pet Party" events | 500,000 Gold + 300,000 materials | 14 days |

**Pet Party Events (Level 10):**
- Weekly themed parties in Daycare
- All pets wear party hats (cosmetic)
- Bonus friendship gains (+50% for 24 hours)
- Exclusive party decorations
- Friends can join party (social event)

---

### **Customization Options**

**Daycare Themes (Visual Customization):**
- **Meadow** (default, grassy with flowers)
- **Beach** (sand, ocean waves)
- **Forest** (trees, mushrooms)
- **Winter** (snow, ice)
- **Volcanic** (lava rocks, ember effects)
- **Crystal Cave** (glowing crystals)
- **Sky Garden** (floating islands)

**Decorative Items:**
- Toy balls (various colors)
- Obstacle courses (tunnels, ramps)
- Furniture (benches, tables)
- Plants (trees, bushes, flowers)
- Water features (fountains, ponds)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Daycare Themes** (visual customization)
  - Cost: 300-500 Premium Currency
  - Zero gameplay impact, pure aesthetics
  
- ✅ **Decorative Items Pack**
  - Cost: 200 Premium Currency for 10 items
  - Makes Daycare prettier, no bonuses
  
- ✅ **Pet Costume Pack** (cosmetic wearables)
  - Cost: 400 Premium Currency for 5 costumes
  - Pets wear hats, scarves, accessories
  
- ✅ **Extra Capacity** (+10 permanent pet slots)
  - Cost: 600 Premium Currency
  - Convenience for large collections

**What CANNOT Be Purchased:**
- ❌ Friendship boosts (must be earned)
- ❌ Exclusive minigames
- ❌ Stat bonuses from Daycare
- ❌ Auto-play minigames

---

### **Why Pet Daycare Matters (Design Justification)**

**Functional Benefits:**
- Increases friendship (combat stat bonuses)
- Provides minigame rewards (small gold)
- Social showcase (prestige)

**Emotional Benefits:**
- Makes pets feel alive (not just numbers)
- Creates emotional attachment (bonding)
- Screenshot opportunities (social media marketing)
- "Cute factor" appeals to younger players

**Retention Benefits:**
- Daily check-in ritual (pet your favorites)
- Long-term goal (max friendship for all pets)
- Social engagement (visit friends' Daycares)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 5/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 5 of 10 (Progression Buildings - Deep Dive)  
**Last Updated:** December 18, 2025

---

## 📋 PART 5 CONTENTS

**This document covers in-depth mechanics for:**
1. Laboratory (Complete System)
2. Expedition Hub (Complete System)
3. Warehouse (Complete System)
4. Mailbox/Notice Board (Complete System)

Each building includes:
- Complete functional systems
- Research trees and deployment mechanics
- Resource management strategies
- Daily engagement features
- Upgrade progression
- Balance considerations
- Monetization integration

---

## 🔬 LABORATORY - COMPLETE SYSTEM

### **Core Philosophy**

The Laboratory provides **permanent account-wide upgrades** through a research tree system. Unlike pet training (pet-specific) or crafting (temporary items), Laboratory research creates **lasting improvements** that benefit all future gameplay.

**Key Design Principles:**
- Research is **permanent** (never lost, even on death/reset)
- Research is **expensive** (gold + materials + time)
- Research is **strategic** (choose upgrade paths wisely)
- Research is **account-wide** (all pets/expeditions benefit)
- Research is **long-term** (days to weeks per project)

**Why This System Works:**
- ✅ Creates aspirational long-term goals
- ✅ Rewards veteran players (cumulative power)
- ✅ Never feels "wasted" (permanent gains)
- ✅ Adds strategic depth (which research first?)
- ✅ Respects casual players (offline progression)

---

### **Research Tree Structure**

**Five Research Categories:**
1. **Combat Research** (damage, defense, timing)
2. **Pet Research** (training, breeding, capture)
3. **Exploration Research** (inventory, loot, stamina)
4. **Economy Research** (gold, trading, crafting)
5. **Mastery Research** (endgame, prestige, unique)

**Four Research Tiers per Category:**
- **Tier 1:** Foundational bonuses (1-3 days, small bonuses)
- **Tier 2:** Significant improvements (5-7 days, medium bonuses)
- **Tier 3:** Major upgrades (10-14 days, large bonuses)
- **Tier 4:** Game-changing abilities (21-30 days, massive bonuses)

**Total Research Projects:** 5 categories × 4 tiers × ~5 projects per tier = **100+ research projects**

---

### **Complete Research Tree Database**

#### **COMBAT RESEARCH TREE**

**Tier 1: Foundations (1-3 Days)**

**Critical Strike Training**
- Duration: 2 days
- Cost: 10,000 Gold + 2,000 Combat Materials
- Effect: +5% critical hit chance (account-wide)
- Requirements: Laboratory Level 1

**Damage Enhancement I**
- Duration: 3 days
- Cost: 15,000 Gold + 3,000 Combat Materials
- Effect: +5% all damage dealt
- Requirements: Laboratory Level 1

**Defense Basics**
- Duration: 2 days
- Cost: 10,000 Gold + 2,000 Defense Materials
- Effect: +5% damage reduction
- Requirements: Laboratory Level 1

**Stamina Efficiency**
- Duration: 1 day
- Cost: 8,000 Gold + 1,500 Combat Materials
- Effect: -10% stamina consumption in combat
- Requirements: Laboratory Level 1

**Timing Mastery I**
- Duration: 3 days
- Cost: 12,000 Gold + 2,500 Combat Materials
- Effect: Timing windows +10% larger (easier perfect blocks)
- Requirements: Laboratory Level 1

---

**Tier 2: Advancements (5-7 Days)**

**Critical Strike Mastery**
- Duration: 5 days
- Cost: 30,000 Gold + 8,000 Combat Materials
- Effect: +10% critical hit chance (+15% total with Tier 1)
- Requirements: Critical Strike Training (Tier 1), Laboratory Level 3

**Damage Enhancement II**
- Duration: 7 days
- Cost: 40,000 Gold + 10,000 Combat Materials
- Effect: +10% all damage (+15% total)
- Requirements: Damage Enhancement I (Tier 1), Laboratory Level 3

**Fortified Defense**
- Duration: 5 days
- Cost: 35,000 Gold + 9,000 Defense Materials
- Effect: +10% damage reduction (+15% total)
- Requirements: Defense Basics (Tier 1), Laboratory Level 3

**Elemental Proficiency**
- Duration: 7 days
- Cost: 45,000 Gold + 12,000 Elemental Materials
- Effect: +5% damage with all elements
- Requirements: Damage Enhancement I, Laboratory Level 3

**Combo Mastery**
- Duration: 6 days
- Cost: 38,000 Gold + 10,000 Combat Materials
- Effect: Perfect combos grant +15% bonus damage
- Requirements: Timing Mastery I, Laboratory Level 3

---

**Tier 3: Expertise (10-14 Days)**

**Deadly Precision**
- Duration: 10 days
- Cost: 75,000 Gold + 25,000 Combat Materials
- Effect: +20% critical hit chance (+35% total), crits deal +25% damage
- Requirements: Critical Strike Mastery (Tier 2), Laboratory Level 5

**Overwhelming Power**
- Duration: 14 days
- Cost: 100,000 Gold + 35,000 Combat Materials
- Effect: +20% all damage (+35% total)
- Requirements: Damage Enhancement II (Tier 2), Laboratory Level 5

**Impenetrable Armor**
- Duration: 12 days
- Cost: 90,000 Gold + 30,000 Defense Materials
- Effect: +20% damage reduction (+35% total), immune to CC below 30% HP
- Requirements: Fortified Defense (Tier 2), Laboratory Level 5

**Elemental Ascendancy**
- Duration: 14 days
- Cost: 110,000 Gold + 40,000 Elemental Materials
- Effect: +15% elemental damage (+20% total), elemental attacks ignore 25% resistance
- Requirements: Elemental Proficiency (Tier 2), Laboratory Level 5

**Perfect Execution**
- Duration: 10 days
- Cost: 80,000 Gold + 28,000 Combat Materials
- Effect: Perfect timing windows +20% larger, perfect blocks reflect 25% damage
- Requirements: Combo Mastery (Tier 2), Laboratory Level 5

---

**Tier 4: Mastery (21-30 Days)**

**Godlike Reflexes**
- Duration: 30 days
- Cost: 250,000 Gold + 100,000 Combat Materials
- Effect: +30% crit chance (+65% total), crits deal +50% damage, 10% chance to insta-kill non-boss enemies
- Requirements: Deadly Precision (Tier 3), Laboratory Level 7

**Titan's Strength**
- Duration: 28 days
- Cost: 300,000 Gold + 120,000 Combat Materials
- Effect: +30% all damage (+65% total), attacks have 15% chance to stun
- Requirements: Overwhelming Power (Tier 3), Laboratory Level 7

**Immortal Fortitude**
- Duration: 25 days
- Cost: 275,000 Gold + 110,000 Defense Materials
- Effect: +30% damage reduction (+65% total), survive fatal damage once per expedition with 1 HP
- Requirements: Impenetrable Armor (Tier 3), Laboratory Level 7

**Elemental Supremacy**
- Duration: 30 days
- Cost: 320,000 Gold + 130,000 Elemental Materials
- Effect: +30% elemental damage (+50% total), attacks automatically apply strongest elemental advantage
- Requirements: Elemental Ascendancy (Tier 3), Laboratory Level 7

**Time Manipulation**
- Duration: 30 days
- Cost: 350,000 Gold + 150,000 Rare Materials
- Effect: Slow time during combat (30% slower enemy attacks), perfect timing windows +50%
- Requirements: Perfect Execution (Tier 3), Laboratory Level 7

---

#### **PET RESEARCH TREE**

**Tier 1: Foundations (1-3 Days)**

**Training Efficiency I**
- Duration: 2 days
- Cost: 10,000 Gold + 2,000 Training Materials
- Effect: -10% training time for all pets
- Requirements: Laboratory Level 1

**Breeding Basics**
- Duration: 3 days
- Cost: 12,000 Gold + 2,500 Breeding Materials
- Effect: -10% breeding time
- Requirements: Laboratory Level 1

**Capture Enhancement I**
- Duration: 2 days
- Cost: 15,000 Gold + 3,000 Capture Materials
- Effect: +5% capture rate for all pets
- Requirements: Laboratory Level 1

**IV Stability I**
- Duration: 3 days
- Cost: 20,000 Gold + 4,000 Genetic Materials
- Effect: +5% chance of perfect IV roll during breeding
- Requirements: Laboratory Level 1

**Pet Longevity I**
- Duration: 2 days
- Cost: 18,000 Gold + 3,500 Age Materials
- Effect: Pets age 10% slower (real-time)
- Requirements: Laboratory Level 1

---

**Tier 2: Advancements (5-7 Days)**

**Training Efficiency II**
- Duration: 5 days
- Cost: 35,000 Gold + 9,000 Training Materials
- Effect: -20% training time (-30% total)
- Requirements: Training Efficiency I (Tier 1), Laboratory Level 3

**Advanced Breeding**
- Duration: 7 days
- Cost: 40,000 Gold + 10,000 Breeding Materials
- Effect: -20% breeding time (-30% total), +10% hybrid chance
- Requirements: Breeding Basics (Tier 1), Laboratory Level 3

**Capture Enhancement II**
- Duration: 6 days
- Cost: 45,000 Gold + 12,000 Capture Materials
- Effect: +10% capture rate (+15% total)
- Requirements: Capture Enhancement I (Tier 1), Laboratory Level 3

**IV Stability II**
- Duration: 7 days
- Cost: 50,000 Gold + 15,000 Genetic Materials
- Effect: +10% perfect IV roll chance (+15% total)
- Requirements: IV Stability I (Tier 1), Laboratory Level 3

**Pet Longevity II**
- Duration: 5 days
- Cost: 42,000 Gold + 11,000 Age Materials
- Effect: Pets age 20% slower (-30% total)
- Requirements: Pet Longevity I (Tier 1), Laboratory Level 3

---

**Tier 3: Expertise (10-14 Days)**

**Training Mastery**
- Duration: 12 days
- Cost: 90,000 Gold + 30,000 Training Materials
- Effect: -30% training time (-60% total), -15% training cost
- Requirements: Training Efficiency II (Tier 2), Laboratory Level 5

**Genetic Manipulation**
- Duration: 14 days
- Cost: 110,000 Gold + 40,000 Breeding Materials
- Effect: -40% breeding time (-70% total), +25% hybrid chance, guarantee 3 IVs from parents
- Requirements: Advanced Breeding (Tier 2), Laboratory Level 5

**Master Capture**
- Duration: 10 days
- Cost: 95,000 Gold + 32,000 Capture Materials
- Effect: +20% capture rate (+35% total), legendary pets +10% bonus
- Requirements: Capture Enhancement II (Tier 2), Laboratory Level 5

**Perfect Genetics**
- Duration: 14 days
- Cost: 120,000 Gold + 50,000 Genetic Materials
- Effect: +20% perfect IV roll (+35% total), breeding always passes down 4 IVs
- Requirements: IV Stability II (Tier 2), Laboratory Level 5

**Eternal Youth**
- Duration: 12 days
- Cost: 100,000 Gold + 35,000 Age Materials
- Effect: Pets age 40% slower (-70% total), pets live 50% longer
- Requirements: Pet Longevity II (Tier 2), Laboratory Level 5

---

**Tier 4: Mastery (21-30 Days)**

**Instantaneous Training**
- Duration: 28 days
- Cost: 300,000 Gold + 120,000 Training Materials
- Effect: -50% training time (-80% total), -30% training cost, unlock "Instant Train" for common pets
- Requirements: Training Mastery (Tier 3), Laboratory Level 7

**Divine Breeding**
- Duration: 30 days
- Cost: 350,000 Gold + 150,000 Breeding Materials
- Effect: -60% breeding time (-90% total), +50% hybrid chance, guarantee 5 IVs, unlock mythic hybrids
- Requirements: Genetic Manipulation (Tier 3), Laboratory Level 7

**Guaranteed Capture**
- Duration: 25 days
- Cost: 280,000 Gold + 110,000 Capture Materials
- Effect: +35% capture rate (+70% total), legendary pets +30% bonus, epic+ pets never flee
- Requirements: Master Capture (Tier 3), Laboratory Level 7

**Flawless Genetics**
- Duration: 30 days
- Cost: 400,000 Gold + 180,000 Genetic Materials
- Effect: +30% perfect IV roll (+65% total), breeding ALWAYS passes 5 IVs, choose which stat is perfect
- Requirements: Perfect Genetics (Tier 3), Laboratory Level 7

**Age Reversal**
- Duration: 30 days
- Cost: 380,000 Gold + 160,000 Age Materials
- Effect: Pets age 70% slower (-95% total), pets live 2x longer, unlock "Youth Potion" (reset age to baby)
- Requirements: Eternal Youth (Tier 3), Laboratory Level 7

---

#### **EXPLORATION RESEARCH TREE**

**Tier 1: Foundations (1-3 Days)**

**Inventory Expansion I**
- Duration: 1 day
- Cost: 8,000 Gold + 1,500 Materials
- Effect: +10 base inventory slots
- Requirements: Laboratory Level 1

**Resource Detection I**
- Duration: 2 days
- Cost: 10,000 Gold + 2,000 Materials
- Effect: +10% material drop rate
- Requirements: Laboratory Level 1

**Stamina Reserves I**
- Duration: 2 days
- Cost: 12,000 Gold + 2,500 Materials
- Effect: +20% max stamina
- Requirements: Laboratory Level 1

**Sprint Training I**
- Duration: 3 days
- Cost: 15,000 Gold + 3,000 Materials
- Effect: +10% movement speed
- Requirements: Laboratory Level 1

**Biome Adaptation I**
- Duration: 3 days
- Cost: 18,000 Gold + 3,500 Materials
- Effect: -10% environmental damage (fire, ice, poison zones)
- Requirements: Laboratory Level 1

---

**Tier 2: Advancements (5-7 Days)**

**Inventory Expansion II**
- Duration: 5 days
- Cost: 30,000 Gold + 8,000 Materials
- Effect: +20 slots (+30 total)
- Requirements: Inventory Expansion I, Laboratory Level 3

**Resource Detection II**
- Duration: 7 days
- Cost: 40,000 Gold + 10,000 Materials
- Effect: +20% material drop rate (+30% total), rare materials +10%
- Requirements: Resource Detection I, Laboratory Level 3

**Stamina Reserves II**
- Duration: 6 days
- Cost: 35,000 Gold + 9,000 Materials
- Effect: +30% max stamina (+50% total), -15% stamina consumption
- Requirements: Stamina Reserves I, Laboratory Level 3

**Sprint Training II**
- Duration: 7 days
- Cost: 42,000 Gold + 11,000 Materials
- Effect: +15% movement speed (+25% total), sprint 20% longer
- Requirements: Sprint Training I, Laboratory Level 3

**Biome Mastery**
- Duration: 7 days
- Cost: 48,000 Gold + 12,000 Materials
- Effect: -25% environmental damage (-35% total), unlock biome-specific buffs
- Requirements: Biome Adaptation I, Laboratory Level 3

---

**Tier 3: Expertise (10-14 Days)**

**Vast Inventory**
- Duration: 10 days
- Cost: 80,000 Gold + 28,000 Materials
- Effect: +40 slots (+70 total), unlock "Auto-Stack" (materials combine automatically)
- Requirements: Inventory Expansion II, Laboratory Level 5

**Treasure Hunter**
- Duration: 14 days
- Cost: 100,000 Gold + 35,000 Materials
- Effect: +40% material drop (+70% total), rare +20%, epic +5%
- Requirements: Resource Detection II, Laboratory Level 5

**Endless Stamina**
- Duration: 12 days
- Cost: 90,000 Gold + 30,000 Materials
- Effect: +50% max stamina (+100% total), -30% consumption, stamina regens 50% faster
- Requirements: Stamina Reserves II, Laboratory Level 5

**Lightning Speed**
- Duration: 10 days
- Cost: 85,000 Gold + 29,000 Materials
- Effect: +25% movement speed (+50% total), sprint 50% longer, sprint drains 50% less stamina
- Requirements: Sprint Training II, Laboratory Level 5

**Environmental Immunity**
- Duration: 14 days
- Cost: 110,000 Gold + 38,000 Materials
- Effect: -50% environmental damage (-85% total), immune to slows in hazard zones
- Requirements: Biome Mastery, Laboratory Level 5

---

**Tier 4: Mastery (21-30 Days)**

**Infinite Pockets**
- Duration: 25 days
- Cost: 280,000 Gold + 110,000 Materials
- Effect: +100 slots (+170 total), unlock "Remote Access" (access warehouse from expedition)
- Requirements: Vast Inventory, Laboratory Level 7

**Legendary Luck**
- Duration: 30 days
- Cost: 350,000 Gold + 150,000 Materials
- Effect: +70% material drop (+140% total), rare +40%, epic +15%, legendary +5%
- Requirements: Treasure Hunter, Laboratory Level 7

**Inexhaustible**
- Duration: 28 days
- Cost: 320,000 Gold + 130,000 Materials
- Effect: +100% max stamina (+200% total), -50% consumption, stamina regens 100% faster
- Requirements: Endless Stamina, Laboratory Level 7

**Supersonic**
- Duration: 25 days
- Cost: 300,000 Gold + 120,000 Materials
- Effect: +40% movement speed (+90% total), infinite sprint, dash cooldown -75%
- Requirements: Lightning Speed, Laboratory Level 7

**Biome Transcendence**
- Duration: 30 days
- Cost: 380,000 Gold + 160,000 Materials
- Effect: Immune to environmental damage, hazard zones grant buffs instead of debuffs
- Requirements: Environmental Immunity, Laboratory Level 7

---

#### **ECONOMY RESEARCH TREE**

**Tier 1: Foundations (1-3 Days)**

**Merchant Training I**
- Duration: 2 days
- Cost: 10,000 Gold + 2,000 Materials
- Effect: +10% gold from all sources
- Requirements: Laboratory Level 1

**Crafting Efficiency I**
- Duration: 3 days
- Cost: 12,000 Gold + 2,500 Materials
- Effect: -10% crafting material costs
- Requirements: Laboratory Level 1

**Market Savvy I**
- Duration: 2 days
- Cost: 15,000 Gold + 3,000 Materials
- Effect: -10% Market auction fees
- Requirements: Laboratory Level 1

**Salvage Expert I**
- Duration: 2 days
- Cost: 11,000 Gold + 2,200 Materials
- Effect: +20% materials from salvaging items
- Requirements: Laboratory Level 1

**Appraisal Knowledge I**
- Duration: 3 days
- Cost: 13,000 Gold + 2,700 Materials
- Effect: See true value of items before selling
- Requirements: Laboratory Level 1

---

**Tier 2: Advancements (5-7 Days)**

**Merchant Training II**
- Duration: 5 days
- Cost: 35,000 Gold + 9,000 Materials
- Effect: +20% gold (+30% total), sell prices +5%
- Requirements: Merchant Training I, Laboratory Level 3

**Crafting Efficiency II**
- Duration: 7 days
- Cost: 40,000 Gold + 10,000 Materials
- Effect: -20% crafting costs (-30% total), 10% chance to not consume materials
- Requirements: Crafting Efficiency I, Laboratory Level 3

**Market Savvy II**
- Duration: 6 days
- Cost: 38,000 Gold + 9,500 Materials
- Effect: -20% auction fees (-30% total), listings last +3 days
- Requirements: Market Savvy I, Laboratory Level 3

**Salvage Expert II**
- Duration: 5 days
- Cost: 33,000 Gold + 8,500 Materials
- Effect: +40% materials from salvage (+60% total), 5% chance to recover rare components
- Requirements: Salvage Expert I, Laboratory Level 3

**Appraisal Mastery**
- Duration: 7 days
- Cost: 42,000 Gold + 11,000 Materials
- Effect: See item IVs before buying, predict market trends
- Requirements: Appraisal Knowledge I, Laboratory Level 3

---

**Tier 3: Expertise (10-14 Days)**

**Golden Touch**
- Duration: 12 days
- Cost: 90,000 Gold + 30,000 Materials
- Effect: +40% gold (+70% total), sell prices +15%, 5% chance for double gold drops
- Requirements: Merchant Training II, Laboratory Level 5

**Master Crafter**
- Duration: 14 days
- Cost: 100,000 Gold + 35,000 Materials
- Effect: -30% crafting costs (-60% total), 20% chance to not consume materials
- Requirements: Crafting Efficiency II, Laboratory Level 5

**Market Mogul**
- Duration: 10 days
- Cost: 85,000 Gold + 29,000 Materials
- Effect: -30% auction fees (-60% total), listings permanent until sold, priority placement
- Requirements: Market Savvy II, Laboratory Level 5

**Recycling Genius**
- Duration: 12 days
- Cost: 95,000 Gold + 32,000 Materials
- Effect: +70% materials from salvage (+130% total), 15% rare component recovery
- Requirements: Salvage Expert II, Laboratory Level 5

**Market Prophet**
- Duration: 14 days
- Cost: 110,000 Gold + 38,000 Materials
- Effect: See future price trends (7 days ahead), unlock "Buy Orders" system
- Requirements: Appraisal Mastery, Laboratory Level 5

---

**Tier 4: Mastery (21-30 Days)**

**Midas Blessing**
- Duration: 28 days
- Cost: 320,000 Gold + 130,000 Materials
- Effect: +70% gold (+140% total), sell prices +30%, 15% double gold drops, enemies drop 2x gold
- Requirements: Golden Touch, Laboratory Level 7

**Divine Artisan**
- Duration: 30 days
- Cost: 350,000 Gold + 150,000 Materials
- Effect: -50% crafting costs (-80% total), 40% chance to not consume materials, crafts have +20% stats
- Requirements: Master Crafter, Laboratory Level 7

**Trade Empire**
- Duration: 25 days
- Cost: 300,000 Gold + 120,000 Materials
- Effect: -50% auction fees (-80% total), free listings forever, unlock "Bulk Trading"
- Requirements: Market Mogul, Laboratory Level 7

**Alchemy Transmutation**
- Duration: 30 days
- Cost: 380,000 Gold + 160,000 Materials
- Effect: +150% salvage materials (+280% total), 30% rare recovery, convert materials to any other type
- Requirements: Recycling Genius, Laboratory Level 7

**Omniscient Trader**
- Duration: 30 days
- Cost: 400,000 Gold + 180,000 Materials
- Effect: Perfect market predictions (30 days ahead), instant price alerts, unlock "Automated Trading Bot"
- Requirements: Market Prophet, Laboratory Level 7

---

#### **MASTERY RESEARCH TREE (Endgame)**

**Tier 1-3: Mixed Prerequisites**

**Prestige Training**
- Duration: 21 days
- Cost: 500,000 Gold + 250,000 Materials
- Effect: Unlock "Prestige Mode" (reset progress for permanent bonuses)
- Requirements: All Combat Tier 3 + All Pet Tier 3, Laboratory Level 8

**Account Ascension**
- Duration: 30 days
- Cost: 1,000,000 Gold + 500,000 Materials
- Effect: +100 account level cap, unlock "Ascension Perks"
- Requirements: All Exploration Tier 3 + All Economy Tier 3, Laboratory Level 9

**Legendary Researcher**
- Duration: 45 days
- Cost: 2,000,000 Gold + 1,000,000 Materials
- Effect: All research -50% time, -30% cost, +2 Laboratory slots
- Requirements: All categories Tier 3, Laboratory Level 10

**Mythic Awakening**
- Duration: 60 days
- Cost: 5,000,000 Gold + 3,000,000 Materials
- Effect: Unlock Mythic rarity pets, Mythic crafting recipes, Mythic biomes
- Requirements: All categories Tier 4 completed (100%), Laboratory Level 10

---

### **Laboratory Building Upgrades**

| Level | Research Slots | Speed Bonus | Unlocked Tiers | Special Feature | Upgrade Cost | Upgrade Time |
|-------|----------------|-------------|----------------|-----------------|--------------|--------------|
| 1 | 1 slot | 0% | Tier 1 research | Basic research | 25,000 Gold (initial) | 4 hours |
| 2 | 2 slots | 0% | (Efficiency) | (None) | 15,000 Gold + 5,000 materials | 8 hours |
| 3 | 3 slots | -5% | Tier 2 research | Unlock Tier 2 | 30,000 Gold + 10,000 materials | 16 hours |
| 4 | 3 slots | -10% | (Efficiency) | (None) | 50,000 Gold + 20,000 materials | 32 hours |
| 5 | 4 slots | -15% | Tier 3 research | Unlock Tier 3 | 80,000 Gold + 35,000 materials | 48 hours |
| 6 | 4 slots | -20% | (Efficiency) | Research Queue | 120,000 Gold + 50,000 materials | 72 hours |
| 7 | 5 slots | -25% | Tier 4 research | Unlock Tier 4 | 180,000 Gold + 80,000 materials | 5 days |
| 8 | 5 slots | -30% | (Efficiency) | Research Preview | 250,000 Gold + 120,000 materials | 7 days |
| 9 | 5 slots | -35% | Mastery research | (Efficiency) | 350,000 Gold + 180,000 materials | 10 days |
| 10 | 5 slots | -40% | All research | "Research Boost" (premium) | 500,000 Gold + 300,000 materials | 14 days |

**Special Features:**

**Research Queue (Level 6):**
- Queue up to 10 research projects
- Automatically starts next when current finishes
- Plan months of research ahead

**Research Preview (Level 8):**
- See all future research options
- Plan optimal research path
- Avoid dead-end researches

**Research Boost (Level 10 + Premium):**
- Premium currency can accelerate research by 50%
- Ethical monetization (time-saver, not exclusive content)

---

### **Research Strategy Guide**

**Early Game Priority (Levels 1-30):**
1. Capture Enhancement I (easier pet collection)
2. Training Efficiency I (faster leveling)
3. Inventory Expansion I (carry more loot)
4. Resource Detection I (more materials)
5. Merchant Training I (more gold)

**Mid Game Priority (Levels 30-60):**
1. Damage Enhancement II (combat power)
2. Training Efficiency II (keep pets leveled)
3. Capture Enhancement II (rare pets)
4. Treasure Hunter (farm efficiency)
5. Golden Touch (economy scaling)

**Late Game Priority (Levels 60-90):**
1. All Tier 3 Combat Research (maximize damage)
2. Genetic Manipulation (perfect pet breeding)
3. Master Capture (legendary hunting)
4. Lightning Speed (expedition efficiency)
5. Market Mogul (trade dominance)

**Endgame Priority (Level 90+):**
1. Complete all Tier 4 research
2. Unlock Mastery research
3. Prestige Training (infinite scaling)
4. Mythic Awakening (endgame content)

---

### **Research Cost Balancing**

**Total Investment for 100% Completion:**
- Gold: ~15,000,000+ Gold
- Materials: ~8,000,000+ Materials
- Time: ~1,200+ days (with Level 1 Laboratory)
- Time: ~480 days (with Level 10 Laboratory + max bonuses)

**This ensures:**
- Research is truly "endgame" (years of content)
- Veteran players have permanent advantage (earned)
- New players aren't impossibly behind (can catch up with focus)
- Creates aspirational goals (something to always work toward)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Research Acceleration Tokens** (reduce research time by 25-50%)
  - Cost: 100-500 Premium Currency per token
  - Does NOT unlock exclusive research, just speeds up
  
- ✅ **Extra Research Slots** (6th permanent slot)
  - Cost: 1,000 Premium Currency
  - Convenience, not power
  
- ✅ **Research Reset Token** (refund research, reallocate)
  - Cost: 500 Premium Currency
  - Allows experimentation without penalty

**What CANNOT Be Purchased:**
- ❌ Exclusive research projects
- ❌ Instant research completion (must wait minimum time)
- ❌ Better research bonuses (everyone gets same stats)
- ❌ Skip research prerequisites

---

## 🗺️ EXPEDITION HUB - COMPLETE SYSTEM

### **Core Philosophy**

The Expedition Hub is the **deployment center** where players prepare for expeditions, select game modes, choose companions, and equip loadouts before entering the procedural world.

**Key Design Principles:**
- Hub is **ritual before adventure** (creates anticipation)
- Clear **mode selection** (Solo/Co-op/PvPvE)
- Strategic **loadout choices** (weapons, armor, pets, consumables)
- **Squad presets** for quick deployment
- **Statistics tracking** (lifetime stats, recent performance)

---

### **Expedition Hub Features**

#### **1. Mode Selection Screen**

```
EXPEDITION MODE SELECTION:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🧍 SOLO EXPEDITION
   └─ Play alone, standard difficulty
   └─ Standard rewards (100% base)
   └─ No risk of player interference
   └─ Best for: Learning, farming, casual play

👥 CO-OP PvE EXPEDITION
   └─ Team up with 2-6 players
   └─ Shared encounters, friendly fire OFF
   └─ Cooperative rewards (110% base, shared loot)
   └─ Best for: Socializing, harder content, efficiency

⚔️ PvPvE HIGH STAKES
   └─ Player combat enabled (20-40 players per server)
   └─ High risk, high reward (150% loot multiplier)
   └─ Can lose cargo to other players
   └─ Best for: Competitive, high-skill, prestige
```

**Mode Selection Details:**
- Click desired mode
- Confirm choice (cannot change once deployed)
- Enter matchmaking (for Co-op/PvPvE) or instant deploy (Solo)
- Loading screen with tips/lore

---

#### **2. Companion Pet Selection**

**Choose Active Companions:**
- Unlock slots via Expedition Hub upgrades:
  - Level 1: 1 companion slot
  - Level 3: 2 companion slots
  - Level 5: 3 companion slots (MAX)

**Pet Selection UI:**
- View all pets in roster
- Filter by element, rarity, level
- See pet stats (HP, Attack, Defense, Speed)
- See pet abilities (active + passive)
- Drag pets into companion slots

**Strategic Considerations:**
- Elemental coverage (bring Fire + Ice for versatility)
- Role diversity (tank + DPS + support)
- Level appropriate (don't bring Level 5 to endgame biome)

---

#### **3. Loadout Equipment**

**Equip Crafted Gear:**

**Weapon Slot:**
- Choose from crafted weapons (Weaponsmith)
- See weapon stats (damage, element, special effects)
- Recent weapons shown first

**Armor Slots (6 pieces):**
- Helmet, Chestplate, Leggings, Boots, Gloves, Cloak
- See total defense, HP bonus, resistances
- Set bonuses displayed prominently

**Consumable Hotbar (5 slots):**
- Drag consumables from Workshop inventory
- Assign to hotkeys (1-5)
- See quantity (e.g., 15 Health Potions)

**Loadout Preview:**
- Total Stats Summary:
  - HP: X (+Y from armor)
  - Attack: X (+Y from weapon)
  - Defense: X (+Y from armor/research)
  - Speed: X (+Y from boots/research)
- Elemental Resistances (pie chart)
- Set Bonus Active (visual indicator)

---

#### **4. Squad Presets (Level 5 Unlock)**

**Save/Load Loadouts:**
- Save up to 10 presets
- Name presets ("Fire Biome Farm", "PvP Build", "Boss Rush")
- One-click load entire loadout (pets + gear + consumables)
- Share presets with friends (export code)

**Preset Categories:**
- Combat Focus (high damage, offensive gear)
- Survival Focus (high defense, healing consumables)
- Farming Focus (loot bonuses, speed gear)
- PvP Focus (balanced stats, anti-player strategies)

**Why Presets Matter:**
- Endgame players have 10+ viable loadouts
- Switching manually takes 5+ minutes
- Presets = 5 seconds (quality-of-life)

---

#### **5. Quick Deploy Feature (Level 7 Unlock)**

**Repeat Last Expedition:**
- Button: "Quick Deploy - [Last Mode]"
- Instantly deploy with same loadout/mode
- No need to reconfigure
- Perfect for grinding same biome repeatedly

**Auto-Restock Consumables:**
- Automatically refills consumables from storage
- Example: Used 10 Health Potions → automatically restocks before next expedition
- Saves time (no manual inventory management)

---

#### **6. Statistics Dashboard**

**Lifetime Statistics:**
- Total Expeditions: X
- Solo / Co-op / PvPvE breakdown
- Total Pets Captured: X
- Total Enemies Defeated: X
- Total Distance Traveled: X km
- Total Gold Earned: X
- Total Materials Gathered: X
- Successful Extractions: X (Y% success rate)

**Recent Performance (Last 10 Expeditions):**
- Mode, Duration, Loot Value, Outcome (Success/Failed)
- Biomes Visited
- Pets Captured
- Enemies Defeated

**Personal Bests:**
- Fastest Extraction Time
- Most Gold in Single Expedition
- Most Pets Captured in Single Expedition
- Longest Survival (minutes)

**Leaderboards Integration:**
- View global/guild rankings
- Filter by timeframe (daily, weekly, all-time)
- Compare stats with friends

---

### **Expedition Hub Building Upgrades**

| Level | Companion Slots | Special Features | Upgrade Cost | Upgrade Time |
|-------|-----------------|------------------|--------------|--------------|
| 1 | 1 slot | Basic deployment | FREE (always available) | Instant |
| 2 | 1 slot | Unlock Statistics Dashboard | 5,000 Gold + 1,000 materials | 1 hour |
| 3 | 2 slots | Second companion slot | 10,000 Gold + 3,000 materials | 3 hours |
| 4 | 2 slots | Unlock Loadout Preview | 20,000 Gold + 6,000 materials | 6 hours |
| 5 | 3 slots | Third slot + Squad Presets (10 presets) | 40,000 Gold + 12,000 materials | 12 hours |
| 6 | 3 slots | (Efficiency boost) | 60,000 Gold + 20,000 materials | 24 hours |
| 7 | 3 slots | Quick Deploy + Auto-Restock | 90,000 Gold + 35,000 materials | 48 hours |
| 8 | 3 slots | (Efficiency boost) | 130,000 Gold + 50,000 materials | 72 hours |
| 9 | 3 slots | Unlock "Expedition Goals" (bonus objectives) | 180,000 Gold + 80,000 materials | 5 days |
| 10 | 3 slots | Unlock "Hardcore Mode" (permadeath, 3x rewards) | 250,000 Gold + 120,000 materials | 7 days |

**Special Features:**

**Expedition Goals (Level 9):**
- Optional objectives for each expedition
- Examples: "Capture 5 Fire Pets", "Defeat 20 Enemies", "Extract in 15 Minutes"
- Bonus rewards for completion (+10-30% loot)

**Hardcore Mode (Level 10):**
- Permadeath (lose all cargo if you die, not just extraction failure)
- 3x loot multiplier (high risk, high reward)
- Exclusive cosmetics for Hardcore achievements
- Separate leaderboards

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Extra Preset Slots** (20 presets instead of 10)
  - Cost: 300 Premium Currency
  - Convenience for loadout hoarders
  
- ✅ **Cosmetic Deployment Animations**
  - Cost: 200-500 Premium Currency
  - Fancy portal effects, pet summon animations
  - Zero gameplay impact

**What CANNOT Be Purchased:**
- ❌ Extra companion slots (3 is max for everyone)
- ❌ Better loot multipliers
- ❌ Skip expedition requirements
- ❌ Exclusive game modes

---

## 📦 WAREHOUSE - COMPLETE SYSTEM

### **Core Philosophy**

The Warehouse is the **central storage hub** for all resources, materials, crafted items, and pets. It must be **organized, accessible, and scalable** as players accumulate thousands of items.

**Key Design Principles:**
- Storage is **finite** (creates strategic choices)
- Upgrades **expand capacity** (progression reward)
- **Auto-sorting** available (quality-of-life)
- **Remote access** unlockable (Laboratory research)
- **Categories** separate item types (organization)

---

### **Warehouse Storage Categories**

**1. Raw Materials:**
- Iron Ore, Wood, Stone, Leather, Plants
- Biome-specific materials (Lava Essence, Frost Crystal, etc.)
- Stack size: 999 per slot

**2. Refined Materials:**
- Iron Ingots, Steel, Mithril, Celestial Steel
- Cloth, Silk, Dragon Weave
- Polished Gems, Refined Crystals
- Stack size: 999 per slot

**3. Consumables:**
- Health Potions (Small/Medium/Large)
- Buff Elixirs
- Utility Items (Teleport Crystals, Resurrection Scrolls)
- Stack size: 99 per slot

**4. Equipment:**
- Weapons (Swords, Bows, Axes, Staves, Hammers, Daggers)
- Armor (Helmets, Chestplates, Leggings, Boots, Gloves, Cloaks)
- Stack size: 1 per slot (unique items)

**5. Pet Storage:**
- Captured pets (not in active roster)
- Stack size: 1 per slot
- Note: Sanctuary also displays pets, but Warehouse is bulk storage

**6. Miscellaneous:**
- Quest items
- Event tokens
- Crafting blueprints
- Cosmetic items
- Stack size: Variable (1-99)

---

### **Storage Capacity Progression**

| Warehouse Level | Total Slots | Raw Materials | Refined | Consumables | Equipment | Pets | Misc |
|----------------|-------------|---------------|---------|-------------|-----------|------|------|
| 1 | 100 | 30 | 20 | 15 | 10 | 15 | 10 |
| 2 | 150 | 45 | 30 | 20 | 15 | 25 | 15 |
| 3 | 200 | 60 | 40 | 30 | 20 | 30 | 20 |
| 4 | 275 | 80 | 55 | 40 | 30 | 40 | 30 |
| 5 | 350 | 100 | 70 | 50 | 40 | 55 | 35 |
| 6 | 450 | 130 | 90 | 65 | 50 | 70 | 45 |
| 7 | 550 | 160 | 110 | 80 | 65 | 85 | 50 |
| 8 | 700 | 200 | 140 | 100 | 80 | 110 | 70 |
| 9 | 850 | 250 | 170 | 120 | 100 | 135 | 75 |
| 10 | 1,000 | 300 | 200 | 140 | 120 | 160 | 80 |

**Premium Expansion:**
- +500 permanent slots (1,500 total at Level 10)
- Cost: $4.99 or 500 Premium Currency
- Distributed proportionally across categories

---

### **Warehouse Organization Tools**

**Auto-Sort (Level 3 Unlock):**
- Button: "Auto-Sort All"
- Automatically organizes items by:
  1. Category (materials, consumables, etc.)
  2. Rarity (Common → Legendary)
  3. Alphabetically
- Takes 1 second (instant gratification)

**Quick Stack (Level 5 Unlock):**
- Button: "Quick Stack"
- Combines all stackable items automatically
- Example: 10 slots of "Iron Ore ×50" → 1 slot of "Iron Ore ×500"
- Frees up slots instantly

**Search Function (Level 2 Unlock):**
- Search bar at top
- Search by name ("Iron"), category ("Materials"), rarity ("Legendary")
- Instant filtering (no scrolling through 1,000 items)

**Filters (Level 4 Unlock):**
- Filter by category, rarity, level requirement
- Hide/show specific item types
- Example: "Show only Epic+ Equipment"

**Favorites (Level 6 Unlock):**
- Star items to mark as favorites
- Favorites appear at top of list
- Prevents accidental selling/salvaging

---

### **Remote Access Feature (Laboratory Research)**

**Laboratory Research: "Remote Access"**
- Unlocks ability to access Warehouse from anywhere
- Cost: Tier 4 Exploration Research
- Use Case: Mid-expedition, realize you need different consumables → access Warehouse remotely

**Limitations:**
- Cannot deposit items remotely (must return to base)
- Can only withdraw to inventory (limited by inventory capacity)
- 5-minute cooldown between uses (prevents exploitation)

---

### **Warehouse Building Upgrades**

| Level | Total Slots | Special Features | Upgrade Cost | Upgrade Time |
|-------|-------------|------------------|--------------|--------------|
| 1 | 100 | Basic storage | FREE (always available) | Instant |
| 2 | 150 | Unlock Search | 3,000 Gold + 500 materials | 30 minutes |
| 3 | 200 | Auto-Sort | 8,000 Gold + 2,000 materials | 2 hours |
| 4 | 275 | Filters | 15,000 Gold + 5,000 materials | 6 hours |
| 5 | 350 | Quick Stack | 30,000 Gold + 10,000 materials | 12 hours |
| 6 | 450 | Favorites | 50,000 Gold + 20,000 materials | 24 hours |
| 7 | 550 | (Capacity boost) | 80,000 Gold + 35,000 materials | 48 hours |
| 8 | 700 | (Capacity boost) | 120,000 Gold + 50,000 materials | 72 hours |
| 9 | 850 | (Capacity boost) | 180,000 Gold + 80,000 materials | 5 days |
| 10 | 1,000 | Unlock "Vault" (secure storage) | 250,000 Gold + 120,000 materials | 7 days |

**Vault Feature (Level 10):**
- Separate 50-slot storage for most valuable items
- Items in Vault cannot be accidentally sold/salvaged
- Requires password to access (security)
- Use for: Legendary pets, perfect IV pets, rare cosmetics

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Storage Expansion** (+500 permanent slots)
  - Cost: $4.99 or 500 Premium Currency
  - One-time purchase (permanent benefit)
  
- ✅ **Extra Vault Slots** (+50 secure slots)
  - Cost: 300 Premium Currency
  - Protects more valuable items

**What CANNOT Be Purchased:**
- ❌ Infinite storage (must have limit for game economy)
- ❌ Better organization tools (everyone gets same features)
- ❌ Exclusive storage categories

---

## 📬 MAILBOX / NOTICE BOARD - COMPLETE SYSTEM

### **Core Philosophy**

The Mailbox is the **daily engagement hub** where players claim login rewards, accept quests, receive notifications, and check announcements. It's designed to create **daily habits** and **retention**.

**Key Design Principles:**
- **Daily login rewards** (motivates returning)
- **Quest system** (gives short-term goals)
- **Notifications** (friend requests, guild invites, market sales)
- **Announcements** (developer news, events, patches)
- **Streak tracking** (rewards consecutive logins)

---

### **Mailbox Core Features**

#### **1. Daily Login Rewards**

**7-Day Reward Cycle:**

| Day | Reward |
|-----|--------|
| Day 1 | 500 Gold + 10 Common Training Materials |
| Day 2 | 750 Gold + 1 Rare Pet Egg |
| Day 3 | 1,000 Gold + 3 Health Potions |
| Day 4 | 1,500 Gold + 10 Rare Training Materials |
| Day 5 | 2,000 Gold + 1 Epic Pet Egg |
| Day 6 | 2,500 Gold + 5 Resurrection Scrolls |
| Day 7 | 5,000 Gold + 1 Legendary Pet Egg + 100 Premium Currency |

**Monthly Login Rewards (Consecutive):**
- 7 days straight: Exclusive cosmetic pet skin
- 14 days straight: Rare mount
- 21 days straight: Epic mount + title
- 30 days straight: Legendary mount + exclusive badge

**Login Streak Tracker:**
- Visual calendar showing login history
- Current streak highlighted
- Next reward preview
- Missed days shown (but streak doesn't break with 1 missed day)

**Streak Protection:**
- 1 "Free Pass" per month (miss 1 day without losing streak)
- Premium players get 3 "Free Passes" per month

---

#### **2. Quest System**

**Daily Quests (3 per day, refresh at midnight):**

**Combat Quests:**
- "Defeat 20 Enemies" → 1,000 Gold, 200 Combat Materials
- "Win 3 Perfect Timing Blocks" → 1,500 Gold, 300 Combat Materials
- "Defeat 1 Elite Enemy" → 2,000 Gold, 500 Combat Materials

**Capture Quests:**
- "Capture 5 Fire Pets" → 1,000 Gold, 5 Capture Orbs
- "Capture 1 Rare+ Pet" → 2,000 Gold, 10 Enhanced Capture Orbs
- "Capture Different Species (3)" → 1,500 Gold, 1 Rare Pet Egg

**Gathering Quests:**
- "Gather 100 Materials" → 800 Gold, 50 Mixed Materials
- "Explore Volcanic Rift" → 1,500 Gold, 20 Lava Essence
- "Extract Successfully" → 1,200 Gold, 100 Gold Bonus

**Social Quests:**
- "Complete 1 Co-op Expedition" → 1,500 Gold, 1 Rare Cosmetic
- "Visit Friend's Base" → 500 Gold, 50 Social Points
- "Trade 1 Item on Market" → 1,000 Gold, -10% Auction Fees (1 day buff)

**Weekly Quests (3 per week, refresh Monday):**

**Epic Quests:**
- "Capture 15 Rare+ Pets" → 10,000 Gold, 1 Epic Pet Egg, 500 Mixed Materials
- "Complete 10 Expeditions" → 8,000 Gold, 1,000 Mixed Materials
- "Defeat 100 Enemies" → 12,000 Gold, 1,500 Combat Materials

**Special Quests:**
- "Participate in Guild Event" → 15,000 Gold, 2,000 Guild Points, Exclusive Cosmetic
- "Win 3 PvPvE Matches" → 20,000 Gold, 1 Legendary Pet Egg, PvP Title

---

#### **3. Notifications Tab**

**Friend Requests:**
- "PlayerX sent you a friend request"
- Accept / Decline buttons
- See player level, guild, playtime

**Guild Invites:**
- "GuildY invited you to join"
- View guild stats (members, level, perks)
- Accept / Decline

**Market Sales:**
- "Your listing 'Fire Wolf ⭐⭐⭐' sold for 50,000 Gold!"
- Claim gold button
- Relist option

**Achievement Unlocks:**
- "You unlocked 'Master Collector' achievement!"
- Claim reward button

**System Announcements:**
- Server maintenance notices
- Event start/end notifications
- Patch notes highlights

---

#### **4. Developer Announcements**

**Announcement Categories:**

**Game Updates:**
- Patch notes (new features, balance changes)
- Bug fixes
- Known issues

**Events:**
- Seasonal events starting/ending
- Limited-time offers
- Double XP weekends

**Community Spotlights:**
- Featured player bases (social showcase)
- Top guild of the month
- Content creator highlights

---

### **Mailbox Building Upgrades**

| Level | Daily Quests | Weekly Quests | Special Features | Upgrade Cost | Upgrade Time |
|-------|--------------|---------------|------------------|--------------|--------------|
| 1 | 3 | 0 | Daily login rewards only | FREE (tutorial) | Instant |
| 2 | 3 | 1 | Unlock daily quests | 2,000 Gold + 500 materials | 1 hour |
| 3 | 5 | 1 | Increase daily quest slots | 5,000 Gold + 1,500 materials | 3 hours |
| 4 | 5 | 2 | Unlock weekly quests | 10,000 Gold + 3,000 materials | 6 hours |
| 5 | 5 | 3 | Increase weekly quest slots | 20,000 Gold + 6,000 materials | 12 hours |
| 6 | 7 | 3 | Increase daily slots again | 35,000 Gold + 12,000 materials | 24 hours |
| 7 | 7 | 3 | Unlock "Quest Auto-Track" | 50,000 Gold + 20,000 materials | 48 hours |
| 8 | 7 | 5 | Increase weekly slots | 80,000 Gold + 35,000 materials | 72 hours |
| 9 | 10 | 5 | Max daily slots | 120,000 Gold + 50,000 materials | 5 days |
| 10 | 10 | 5 | Unlock "Premium Mail" tab | 180,000 Gold + 80,000 materials | 7 days |

**Special Features:**

**Quest Auto-Track (Level 7):**
- Accepted quests automatically tracked on HUD
- Example: "Defeat Enemies: 15/20" appears on screen during expedition
- Waypoint markers for gathering quests

**Premium Mail (Level 10):**
- Exclusive offers for premium players
- Early access to new features
- Bonus rewards (extra gold, rare items)
- NOT pay-to-win (cosmetics and convenience only)

---

### **Quest Reward Scaling**

**Daily Quest Rewards (by Account Level):**
- Level 1-20: 500-1,000 Gold, basic materials
- Level 21-40: 1,000-2,000 Gold, rare materials
- Level 41-60: 2,000-4,000 Gold, epic materials
- Level 61-80: 4,000-8,000 Gold, legendary materials
- Level 81-100: 8,000-15,000 Gold, endgame materials

**Weekly Quest Rewards:**
- 5x daily quest rewards (scaled to level)
- Guaranteed Rare+ Pet Egg
- Exclusive cosmetics (rotating weekly)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Extra Quest Slots** (+3 daily, +2 weekly)
  - Cost: 300 Premium Currency (permanent)
  - More objectives = more rewards
  
- ✅ **Instant Quest Completion Tokens** (skip quest, claim reward)
  - Cost: 50-100 Premium Currency per token
  - Use Case: Don't feel like doing "Defeat 20 Enemies" today
  
- ✅ **Streak Protection Tokens** (extra "Free Passes")
  - Cost: 50 Premium Currency per token
  - Prevents losing monthly streak

**What CANNOT Be Purchased:**
- ❌ Better quest rewards (everyone gets same rewards)
- ❌ Exclusive quests (all quests available to free players)
- ❌ Automatic daily logins (must actually log in)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 6/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 6 of 10 (Social & Economy Buildings - Deep Dive)  
**Last Updated:** December 18, 2025

---

## 📋 PART 6 CONTENTS

**This document covers in-depth mechanics for:**
1. Market/Trading Post (Complete System)
2. Guild Hall (Complete System)
3. Trophy Hall (Complete System)
4. Guild Island System (Complete Design)

Each building includes:
- Complete trading and auction mechanics
- Guild management systems
- Achievement tracking
- Social features and integration
- Anti-exploit measures
- Economic balancing
- Monetization strategies

---

## 💰 MARKET / TRADING POST - COMPLETE SYSTEM

### **Core Philosophy**

The Market is the **player-driven economy hub** where items, pets, and resources are bought and sold through auction house mechanics and direct trades. It creates a **dynamic economy** where supply and demand determine prices.

**Key Design Principles:**
- **Player-driven pricing** (no fixed NPC prices for most items)
- **Auction house** for public listings (competitive bidding)
- **Direct trades** for friend-to-friend exchanges
- **Anti-exploit systems** (prevents duping, price manipulation)
- **NPC vendors** for baseline items (price floor)
- **Market analytics** for informed trading decisions

**Why This System Works:**
- ✅ Creates emergent economy (player agency)
- ✅ Rewards market-savvy players (skill expression)
- ✅ Prevents monopolies (anti-exploit measures)
- ✅ Provides gold sink (auction fees)
- ✅ Encourages specialization (dedicated traders/crafters)

---

### **Market Building Features**

#### **1. Auction House System**

**How Auction House Works:**

```
AUCTION HOUSE FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SELLING:
1. Select item/pet to list
2. Set starting bid price
3. Set buyout price (optional, instant purchase)
4. Set duration (1 day / 3 days / 7 days)
5. Pay listing fee (5-10% of starting price)
6. Item listed publicly

BIDDING:
1. Browse auction house
2. Filter by category/rarity/price
3. Place bid (must beat current bid by 5%)
4. Receive notification if outbid
5. Highest bidder at expiration wins

BUYOUT:
1. See buyout price on listing
2. Click "Buy Now"
3. Pay full buyout price
4. Receive item instantly
5. Auction ends immediately
```

---

#### **Auction House Categories**

**Item Categories:**
- **Pets** (by species, element, rarity, star rating, IV)
- **Weapons** (by type, element, rarity, level requirement)
- **Armor** (by slot, element, rarity, level requirement)
- **Consumables** (by type, potency)
- **Materials** (raw, refined, by biome)
- **Cosmetics** (skins, mounts, emotes, decorations)
- **Blueprints** (crafting recipes)
- **Miscellaneous** (quest items, event tokens)

**Advanced Filters:**
- **Price Range:** Min/Max gold
- **Rarity:** Common, Uncommon, Rare, Epic, Legendary
- **Level Requirement:** 1-100
- **Star Rating:** ⭐ to ⭐⭐⭐⭐⭐
- **IV Range:** Total IV 0-186 (6 stats × 31 max)
- **Element Type:** Fire, Water, Earth, etc.
- **Special Properties:** Set bonus, elemental resistance, special effects
- **Seller Type:** Friends only, Guild only, Anyone
- **Time Remaining:** Ending soon (<1 hour), Newly listed

**Search Function:**
- Search by name ("Fire Wolf", "Dragonforged Blade")
- Search by seller name ("PlayerX")
- Search by minimum stats (e.g., "Attack > 150")

---

#### **Listing Fees & Duration**

**Auction House Fees:**

| Market Level | Listing Fee | Duration Options | Featured Listing Cost |
|-------------|-------------|------------------|----------------------|
| 1 | 10% of starting price | 1 day, 3 days | Not available |
| 2 | 8% | 1 day, 3 days | 1,000 Gold |
| 3 | 6% | 1 day, 3 days, 7 days | 800 Gold |
| 5 | 5% | All + 14 days | 500 Gold |
| 7 | 3% | All + 30 days | 300 Gold |
| 10 | 1% | All + Permanent | 100 Gold |

**Fee Refund Policy:**
- If item sells: Fee is kept (gold sink)
- If auction expires with no bids: 50% fee refunded
- If seller cancels auction: No refund (prevents abuse)

**Featured Listings (Level 3+):**
- Pay extra to highlight listing (appears at top)
- Lasts 24 hours
- 3x more views on average
- Use for high-value items (legendary pets, perfect IV)

---

#### **Auction Duration & Timing**

**Duration Options:**

**1-Day Auction:**
- Fast turnover (quick gold)
- Lower final price (less bidding time)
- Best for: Common items, consumables, bulk materials

**3-Day Auction:**
- Balanced (standard choice)
- Moderate final price
- Best for: Rare/Epic items, general trading

**7-Day Auction:**
- Maximum exposure (more bidders)
- Higher final price (more competition)
- Best for: Legendary pets, perfect IV, rare cosmetics

**14-Day Auction (Level 5+):**
- Very long exposure
- Best for: Extremely rare items (5-star legendaries)

**30-Day Auction (Level 7+):**
- Patient sellers
- Best for: Collectors' items, discontinued cosmetics

**Permanent Listing (Level 10):**
- Never expires until sold
- Best for: Overpriced vanity items, trophy pets
- Can be cancelled anytime (no fee refund)

---

#### **Buyout System**

**How Buyout Works:**
- Seller sets optional "Buy Now" price
- Anyone can instantly purchase at buyout price
- Auction ends immediately when bought out
- Seller receives gold minus auction fee

**Strategic Buyout Pricing:**
- Set buyout 20-30% above starting bid (encourages bidding)
- Set buyout at market value (fast sale)
- No buyout (forces bidding war)

**Example:**
- Legendary Pet, Starting Bid: 100,000 Gold, Buyout: 150,000 Gold
- Bidding: 100k → 110k → 120k → 130k
- Impatient buyer clicks buyout at 150,000 Gold
- Seller receives 148,500 Gold (150k - 1% fee)
- Auction ends

---

#### **Bid Increment Rules**

**Minimum Bid Increments:**

| Current Bid | Minimum Increment |
|-------------|-------------------|
| 0-1,000 Gold | +50 Gold (5%) |
| 1,001-10,000 Gold | +500 Gold (5%) |
| 10,001-100,000 Gold | +5,000 Gold (5%) |
| 100,001-1,000,000 Gold | +50,000 Gold (5%) |
| 1,000,001+ Gold | +100,000 Gold (5%) |

**Why 5% Increments:**
- Prevents sniping (tiny bid increases)
- Encourages meaningful bids
- Speeds up auction resolution

**Autobid System (Level 5+):**
- Set maximum bid (e.g., 50,000 Gold)
- System automatically bids minimum increment when outbid
- Stops bidding when max reached
- Saves time (no manual monitoring)

**Example:**
- PlayerA sets autobid max: 50,000 Gold
- PlayerB bids 30,000 Gold
- System auto-bids 31,500 for PlayerA
- PlayerB bids 35,000 Gold
- System auto-bids 36,750 for PlayerA
- Continues until PlayerA's max reached

---

#### **Direct Trading System**

**How Direct Trading Works:**

```
DIRECT TRADE FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Send trade request to player (friends/guild/nearby)
2. Trade window opens for both players
3. Each player adds items/gold to their side
4. Both players review offer
5. Both players click "Accept"
6. Trade completes instantly
7. No auction fees (0% fee)
```

**Trade Window Features:**
- **Your Offer Side:** Drag items/pets + enter gold amount
- **Their Offer Side:** See their items/pets + gold
- **Fairness Indicator:** Shows approximate value ratio (your value / their value)
  - Green: Fair trade (0.8-1.2 ratio)
  - Yellow: Slightly unfair (0.5-0.8 or 1.2-2.0 ratio)
  - Red: Very unfair (below 0.5 or above 2.0 ratio)
- **Trade History:** See last 10 trades with this player
- **Report Button:** Report suspicious trades (scam attempts)

**Direct Trade Advantages:**
- Zero fees (no auction house cut)
- Instant completion (no waiting)
- Barter system (item for item, no gold needed)
- Privacy (not public listing)

**Direct Trade Limitations:**
- Must be online simultaneously
- Must be friends, guildmates, or physically nearby in hub
- Cannot trade to alts (anti-exploit: must be different IPs)

---

#### **NPC Vendors**

**NPC Vendor Purposes:**
- Provide baseline prices (price floor)
- Sell emergency supplies (overpriced)
- Buy junk items (gold sink)

**NPC Vendor Types:**

**General Goods Vendor:**
- Sells: Common consumables (health potions, basic materials)
- Prices: 2x crafting cost (expensive, but convenient)
- Use Case: Emergency potion when you forgot to craft

**Salvage Vendor:**
- Buys: Any item player wants to sell
- Prices: 10% of market value (very low)
- Use Case: Quick gold for junk items

**Blueprint Vendor:**
- Sells: Common crafting blueprints
- Prices: 5,000-50,000 Gold depending on rarity
- Use Case: Buy blueprint instead of finding via exploration

**Cosmetic Vendor (Premium):**
- Sells: Exclusive cosmetics for premium currency
- Prices: 200-1,000 Premium Currency
- Use Case: Cosmetic shop (monetization)

---

#### **Market Analytics (Level 10 Feature)**

**Analytics Dashboard:**

**Price History Graphs:**
- Line graph showing price trends (7 days, 30 days, all-time)
- Example: "Legendary Fire Wolf average price over 30 days"
- Helps determine fair market value

**Supply & Demand Tracker:**
- Shows active listings vs searches
- High demand + low supply = rising prices
- Low demand + high supply = falling prices

**Popular Items Ranking:**
- Top 10 most searched items (what players want)
- Top 10 most listed items (what players sell)
- Identify profitable niches

**Recommended Pricing Tool:**
- Enter item to list
- System suggests starting bid + buyout based on recent sales
- Example: "Suggested starting bid: 45,000 Gold (based on 10 recent sales avg: 52,000 Gold)"

**Market Alerts:**
- Set alerts for specific items
- Notify when item listed below target price
- Example: "Alert me when Legendary Fire Wolf listed below 80,000 Gold"

---

### **Anti-Exploit & Security Measures**

#### **Anti-Duping Systems**

**Item Tracking:**
- Every item has unique ID (invisible to players)
- System tracks item creation source (crafted, dropped, traded)
- Duplicate IDs flagged instantly
- Automatic ban for duping attempts

**Trade Logs:**
- All trades recorded (timestamp, items, gold, players)
- Suspicious patterns flagged (e.g., 100 trades in 1 hour)
- Manual review by developers

---

#### **Anti-Price Manipulation**

**Listing Limits:**
- Max 50 active listings per player (Level 10 Market)
- Prevents flooding market with overpriced items

**Bid Collusion Detection:**
- System tracks if two accounts bid on each other's auctions repeatedly
- Flags potential shill bidding (fake bids to inflate prices)

**Bulk Purchase Limits:**
- Cannot buy more than 100 of same item per day
- Prevents cornering market (buying all supply to control prices)

---

#### **Anti-Scam Protections**

**Trade Confirmation:**
- 5-second countdown before trade finalizes
- Both players see exactly what they're receiving
- "Are you sure?" popup for high-value trades (>100,000 Gold)

**Phishing Protection:**
- Cannot link external websites in trade chat
- Trade window cannot be spoofed (secure UI)

**Banned Item Trading:**
- Exploited items cannot be traded
- Example: If exploit creates 9999 Legendary Pets, those pets become untradeable

---

### **Market Building Upgrades**

| Level | Max Listings | Auction Fee | Duration Options | Special Features | Upgrade Cost | Upgrade Time |
|-------|-------------|-------------|------------------|------------------|--------------|--------------|
| 1 | 5 | 10% | 1 day, 3 days | Basic auction house | 30,000 Gold (initial) | 6 hours |
| 2 | 10 | 8% | 1 day, 3 days | Search filters | 15,000 Gold + 5,000 materials | 8 hours |
| 3 | 15 | 6% | +7 days | Featured listings | 30,000 Gold + 10,000 materials | 16 hours |
| 4 | 20 | 5% | (None) | Advanced filters | 50,000 Gold + 20,000 materials | 24 hours |
| 5 | 25 | 5% | +14 days | Autobid system | 80,000 Gold + 35,000 materials | 48 hours |
| 6 | 30 | 4% | (None) | Direct trade window | 120,000 Gold + 50,000 materials | 72 hours |
| 7 | 40 | 3% | +30 days | Price history (7 days) | 180,000 Gold + 80,000 materials | 5 days |
| 8 | 45 | 2% | (None) | Buy orders system | 250,000 Gold + 120,000 materials | 7 days |
| 9 | 50 | 1.5% | (None) | Price history (30 days) | 350,000 Gold + 180,000 materials | 10 days |
| 10 | 50 | 1% | +Permanent | Full analytics dashboard | 500,000 Gold + 300,000 materials | 14 days |

**Special Features Explained:**

**Buy Orders System (Level 8):**
- Create "wanted" listings
- Example: "Buying Legendary Fire Wolf, offering 100,000 Gold"
- Sellers can fulfill buy orders instantly
- Reverses traditional auction (buyers compete on price they offer)

---

### **Market Economy Balancing**

**Gold Sinks (Remove Gold from Economy):**
- Auction house fees (1-10% of sales)
- NPC vendor purchases (expensive)
- Crafting costs
- Building upgrades
- Training/breeding costs

**Gold Sources (Add Gold to Economy):**
- Expedition rewards
- Quest completion
- Selling to NPCs (very low returns)
- Daily login rewards

**Inflation Control:**
- Gold sinks must exceed gold sources (deflationary pressure)
- Prevents runaway inflation (100k items become 10M items)
- Keeps economy stable for new players

**Material Sinks:**
- Crafting consumes materials permanently
- Refining converts materials (3:1 ratio = net sink)
- Training/breeding consumes materials

**Material Sources:**
- Expeditions (primary source)
- Salvaging items
- Daily rewards
- Energy Generator (small passive income)

---

### **Typical Market Prices (Examples)**

**Common Items:**
- Iron Ore (×100): 1,000 Gold
- Health Potion (×10): 150 Gold
- Common Pet (⭐): 500 Gold

**Rare Items:**
- Rare Pet (⭐⭐⭐): 20,000 Gold
- Epic Weapon: 50,000 Gold
- Rare Training Materials (×100): 10,000 Gold

**Epic Items:**
- Epic Pet (⭐⭐⭐⭐): 200,000 Gold
- Epic Armor Set (6 pieces): 300,000 Gold
- Epic Training Materials (×100): 50,000 Gold

**Legendary Items:**
- Legendary Pet (⭐⭐⭐⭐⭐): 1,000,000+ Gold
- Perfect IV Pet (6×31): 5,000,000+ Gold
- 5-Star Legendary Pet: 10,000,000+ Gold
- Legendary Weapon: 500,000 Gold

**Cosmetics:**
- Rare Skin: 50,000 Gold
- Epic Mount: 200,000 Gold
- Legendary Mount: 1,000,000 Gold
- Limited Edition Seasonal: 5,000,000+ Gold

---

### **Trading Strategies for Players**

**For Sellers:**
- **Crafters:** Craft consumables in bulk, list at 1.5-2x cost
- **Breeders:** Breed high IV pets, sell for premium
- **Farmers:** Farm rare materials, sell during demand spikes
- **Flippers:** Buy underpriced items, relist at market value

**For Buyers:**
- **Snipers:** Watch for ending auctions with low bids
- **Negotiators:** Use direct trades to barter without fees
- **Bulk Buyers:** Buy materials in bulk (100+) for discount
- **Patient Buyers:** Set low buy orders and wait

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Extra Listing Slots** (+10 permanent slots)
  - Cost: 500 Premium Currency
  - Convenience for heavy traders
  
- ✅ **Featured Listing Bundle** (10 featured listings)
  - Cost: 200 Premium Currency
  - Saves 1,000 Gold (100 per listing)
  
- ✅ **Market Analytics Subscription** (early access to Level 10 analytics)
  - Cost: 300 Premium Currency/month
  - Get analytics before Level 10

**What CANNOT Be Purchased:**
- ❌ Lower auction fees (everyone pays same %)
- ❌ Exclusive trading items (no premium-only market items)
- ❌ Bypass listing limits (50 max for everyone)
- ❌ Gold directly (no "buy gold" option)

---

## 🏰 GUILD HALL - COMPLETE SYSTEM

### **Core Philosophy**

The Guild Hall enables **organized group play** through guild management, shared progression, and cooperative events. Guilds provide **social structure** and **long-term engagement** beyond solo play.

**Key Design Principles:**
- Guilds are **optional** (solo play is fully viable)
- Guild benefits are **meaningful** (not just cosmetic)
- Guild progression is **cooperative** (everyone contributes)
- Guild leadership is **hierarchical** (roles with permissions)
- Guilds create **community** (social bonds, retention)

**Why Guilds Matter:**
- ✅ Long-term player retention (social bonds)
- ✅ Organized group content (raids, wars)
- ✅ Shared goals (cooperative progression)
- ✅ Competitive rankings (guild leaderboards)
- ✅ Mentorship system (veterans help newbies)

---

### **Guild System Features**

#### **1. Guild Creation & Management**

**Creating a Guild:**
- Cost: 100,000 Gold
- Requirements: Account Level 40+
- Choose guild name (unique, 3-20 characters)
- Choose guild emblem (from preset list or upload custom)
- Write guild motto (50 characters max)
- Set guild tags (e.g., [TAG])

**Guild Ranks & Permissions:**

| Rank | Count | Permissions |
|------|-------|-------------|
| **Guild Leader** | 1 | Full control (promote, kick, disband, edit settings) |
| **Officer** | Up to 5 | Invite, kick members (not officers), manage events, guild bank withdraw (limited) |
| **Veteran** | Up to 20 | No special permissions, status/prestige rank |
| **Member** | Unlimited | Standard member, guild chat, guild events |
| **Recruit** | Unlimited | Trial period (7 days), limited guild bank access |

**Guild Settings:**
- **Recruitment Status:** Open (anyone can join), Invite-Only, Closed (not recruiting)
- **Minimum Level:** Set minimum account level to join (e.g., Level 30+)
- **Activity Requirements:** "Must log in at least once per week" or removed
- **Guild Bank Permissions:** Who can deposit/withdraw
- **Guild Event Scheduling:** Officers can create events

---

#### **2. Guild Leveling System**

**How Guilds Level Up:**
- Guild XP earned by member activities:
  - Complete expedition: +10 Guild XP per member
  - Capture rare pet: +25 Guild XP
  - Win PvPvE match: +50 Guild XP
  - Complete guild event: +500 Guild XP
  - Donate to guild bank: +1 Guild XP per 1,000 Gold donated

**Guild Level Progression:**

| Guild Level | XP Required | Max Members | Perks Unlocked |
|-------------|-------------|-------------|----------------|
| 1 | 0 | 20 | Basic guild functions |
| 2 | 10,000 | 25 | +2% XP for all members |
| 3 | 25,000 | 30 | Guild bank unlocked |
| 4 | 50,000 | 35 | +5% XP for all members |
| 5 | 100,000 | 40 | Guild emblem on pets |
| 6 | 200,000 | 45 | +5% gold for all members |
| 7 | 400,000 | 50 | Guild dungeon unlocked |
| 8 | 800,000 | 60 | +10% XP, +5% gold |
| 9 | 1,500,000 | 70 | Guild wars enabled |
| 10 | 3,000,000 | 100 | +15% XP, +10% gold, guild island upgrades |

**Guild Perks:**
- Permanent bonuses for ALL guild members
- Stacks with Laboratory research
- Example: Level 10 Guild + Laboratory research = +30% XP total

---

#### **3. Guild Bank System**

**How Guild Bank Works:**
- Shared storage for guild resources
- Members deposit gold/materials (voluntary)
- Officers can withdraw for guild upgrades
- Leader has full control

**Guild Bank Capacity:**

| Guild Level | Gold Capacity | Material Capacity |
|-------------|---------------|-------------------|
| 3 | 500,000 Gold | 10,000 Materials |
| 5 | 1,000,000 Gold | 25,000 Materials |
| 7 | 2,500,000 Gold | 50,000 Materials |
| 10 | 10,000,000 Gold | 200,000 Materials |

**Guild Bank Uses:**
- Fund guild upgrades (Guild Hall building, Guild Island features)
- Pay for guild events (dungeon entry fees, war costs)
- Help new members (officers can distribute starter packs)
- Guild projects (cooperative goals)

**Guild Bank Permissions:**
- **Leader:** Unlimited withdraw
- **Officer:** Withdraw up to 10% per day
- **Veteran:** Withdraw up to 1% per day (emergency)
- **Member:** Deposit only
- **Recruit:** Deposit only, cannot withdraw

---

#### **4. Guild Chat & Communication**

**Guild Chat Channels:**
- **#general:** All members, casual chat
- **#officers:** Officers only, private strategy
- **#events:** Event announcements, reminders
- **#trading:** Internal guild trading (no fees)

**Chat Features:**
- **@mentions:** Tag specific members
- **Announcements:** Leader/Officers can pin messages
- **Voice Chat:** Optional (third-party integration)
- **Emojis/Stickers:** Custom guild emojis

---

#### **5. Guild Events**

**Weekly Guild Dungeon (Raid):**
- Unlocked at Guild Level 7
- 10-20 guild members cooperate
- Defeat series of bosses (scales to member count)
- Exclusive rewards:
  - Legendary pet eggs
  - Guild-only cosmetics
  - Huge Guild XP (5,000+ per completion)
- Resets every Monday

**Guild Missions (Daily/Weekly):**
- Cooperative objectives:
  - "Guild captures 100 Fire Pets this week"
  - "Guild completes 50 expeditions today"
  - "Guild donates 100,000 Gold to bank"
- Rewards for all members upon completion
- Increases guild level

**Guild Wars (Level 9+):**
- Guild vs Guild competitions
- Weekly tournaments
- Ranked brackets (Bronze, Silver, Gold, Platinum, Diamond)
- Prizes:
  - Top guild: Exclusive legendary mount
  - Top 10 guilds: Epic cosmetics
  - All participants: Guild war tokens (shop currency)

**Guild War Format:**
- 20v20 PvPvE battles
- Capture objectives (flags, bases)
- Team with most points after 30 minutes wins
- Best of 3 rounds

---

#### **6. Guild Leaderboards**

**Global Guild Rankings:**
- By Guild Level (highest XP)
- By Total Members (largest guilds)
- By Guild War Rating (competitive ranking)
- By Weekly Activity (most active)
- By Net Worth (total gold + materials)

**Rewards for Top Guilds:**
- Top 10 Guilds: Featured on main menu screen
- Top 3 Guilds: Exclusive guild cosmetics
- #1 Guild: Server-wide announcement, permanent trophy

---

#### **7. Guild Recruitment**

**Recruitment Tools:**
- **Guild Recruitment Board:** Public board in Social Hub
  - Guilds post recruitment ads
  - Players browse guilds
  - Click to apply or request invite
  
- **In-Game Guild Search:**
  - Filter by level, member count, activity
  - See guild motto, emblem, perks
  - Apply with one click

- **Guild Advertisements:**
  - Officers can pay 10,000 Gold for featured listing (24 hours)
  - Appears at top of recruitment board

---

### **Guild Hall Building Upgrades**

| Level | Special Features | Upgrade Cost | Upgrade Time |
|-------|------------------|--------------|--------------|
| 1 | Basic guild functions (create/join) | 75,000 Gold (initial) | 48 hours |
| 2 | Guild chat, roster view | 30,000 Gold + 10,000 materials | 2 days |
| 3 | Guild bank unlocked | 60,000 Gold + 25,000 materials | 3 days |
| 4 | Guild missions (weekly) | 100,000 Gold + 50,000 materials | 4 days |
| 5 | Guild emblem customization | 150,000 Gold + 80,000 materials | 5 days |
| 6 | Guild events calendar | 220,000 Gold + 120,000 materials | 6 days |
| 7 | Guild dungeon access | 300,000 Gold + 180,000 materials | 7 days |
| 8 | Guild war registration | 450,000 Gold + 250,000 materials | 10 days |
| 9 | Advanced guild analytics | 600,000 Gold + 350,000 materials | 14 days |
| 10 | Guild island full access | 1,000,000 Gold + 600,000 materials | 21 days |

---

### **Guild Island System (Separate Instance)**

**What is Guild Island:**
- Shared space where all guild members can gather
- Separate from personal bases
- Customizable by guild officers
- Social hub for guild activities

**Guild Island Features:**

**1. Guild Monument:**
- Central statue displaying guild emblem
- Shows guild level, member count, achievements
- Upgradeable with guild bank funds
- Higher tiers = more impressive visuals

**2. Guild Meeting Hall:**
- Indoor space for guild gatherings
- Voice chat enabled
- Can host guild meetings, events
- Decorations purchasable with guild funds

**3. Guild Training Grounds:**
- PvP practice arena
- Guild members can duel for fun (no rewards)
- Test builds, practice combat
- Spectator stands for watching matches

**4. Guild Shop:**
- Exclusive items for guild members
- Purchase with guild tokens (earned from events)
- Items:
  - Guild cosmetics (emblem capes, banners)
  - Consumables at discount (10% cheaper than market)
  - Rare pets (rotating weekly)

**5. Guild Garden:**
- Decorative area with plants/fountains
- Members can contribute decorations
- Social hangout spot
- Screenshot-friendly location

**6. Guild Notice Board:**
- Physical board displaying guild announcements
- Event calendar
- Member birthdays (real-world, if shared)
- Guild achievements

**Guild Island Customization:**
- Officers can place decorations (purchased with guild bank)
- Change terrain theme (meadow, beach, volcanic, ice)
- Add buildings (cosmetic structures)
- Rearrange layout

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased (Guild Leader/Officers):**
- ✅ **Premium Guild Emblems** (animated, exclusive designs)
  - Cost: 500 Premium Currency
  - Cosmetic only, zero gameplay impact
  
- ✅ **Guild Island Decorations Bundle**
  - Cost: 300 Premium Currency
  - Cosmetic decorations for island
  
- ✅ **Guild Boost Tokens** (temporary XP boost for all members)
  - Cost: 200 Premium Currency for +50% XP (24 hours)
  - Convenience, not permanent advantage

**What CANNOT Be Purchased:**
- ❌ Guild levels directly (must earn XP)
- ❌ Guild war wins
- ❌ Exclusive powerful items
- ❌ Bypass member limits

---

## 🏆 TROPHY HALL - COMPLETE SYSTEM

### **Core Philosophy**

The Trophy Hall is a **permanent achievement showcase** where players display earned trophies, track completion progress, and earn achievement-specific rewards. It's designed for **completionists** and **prestige hunters**.

**Key Design Principles:**
- Achievements are **permanent** (never lost)
- Trophies are **physical displays** (visible 3D models)
- Achievements are **challenging** (not trivial)
- Achievements grant **rewards** (titles, cosmetics, stats)
- Achievements are **diverse** (combat, social, collection, etc.)

---

### **Achievement Categories**

**1. Exploration Achievements:**
- "World Traveler" - Discover all biomes (statue: world map)
- "Marathon Runner" - Travel 1,000 km total (golden compass)
- "Master Extractor" - Extract 100 times successfully (extraction beacon)
- "Speed Demon" - Complete expedition in under 10 minutes (stopwatch)

**2. Combat Achievements:**
- "Slayer" - Defeat 10,000 enemies (sword monument)
- "Perfect Warrior" - 100 perfect timing combos (golden circle)
- "Duel Master" - Win 50 PvPvE encounters (champion crown)
- "Boss Hunter" - Defeat 50 elite bosses (boss trophy)

**3. Pet Collection Achievements:**
- "Collector" - Capture 100 unique species (master ball)
- "Breeder" - Breed 50 offspring (breeding chamber)
- "Perfect Trainer" - Raise pet to Level 100 (pet statue)
- "Shiny Hunter" - Capture 10 shiny variants (rainbow crystal)

**4. Crafting Achievements:**
- "Forgemaster" - Craft 1,000 items total (anvil)
- "Legendary Smith" - Craft first legendary weapon (weapon case)
- "Master Refiner" - Refine 10,000 materials (refinery model)
- "Alchemist" - Craft 500 consumables (potion rack)

**5. Social Achievements:**
- "Guild Founder" - Create a guild (guild banner)
- "Social Butterfly" - Visit 50 friend bases (compass)
- "Teamwork" - Complete 100 co-op expeditions (handshake medal)
- "Trader" - Complete 100 market trades (merchant scales)

**6. Economy Achievements:**
- "Millionaire" - Earn 1,000,000 Gold total (golden vault)
- "Tycoon" - Net worth exceeds 10,000,000 Gold (diamond vault)
- "Philanthropist" - Donate 100,000 Gold to guild (charity ribbon)
- "Market Mogul" - Sell 1,000 items on market (auctioneer gavel)

**7. Seasonal Achievements (Time-Limited):**
- "Halloween Hunter" - Complete Halloween event (pumpkin trophy)
- "Winter Champion" - Win winter tournament (snowflake crown)
- "Spring Collector" - Capture all spring pets (flower wreath)
- "Summer Legend" - Reach #1 summer leaderboard (sun medal)

---

### **Trophy Rarity & Rewards**

| Trophy Rarity | Count Available | Unlock Difficulty | Rewards |
|---------------|-----------------|-------------------|---------|
| **Bronze** | 50+ | Common (most players achieve) | Title, small gold reward |
| **Silver** | 25+ | Uncommon (requires effort) | Title, rare cosmetic |
| **Gold** | 10+ | Rare (skilled/dedicated players) | Title, epic cosmetic, +1% stat |
| **Platinum** | 5+ | Very Rare (top 10% players) | Title, legendary cosmetic, +2% stat |
| **Diamond** | 1-3 | Legendary (top 1% players) | Title, mythic cosmetic, +5% stat |

**Stat Bonuses (Cumulative):**
- Collect 10 Bronze: +1% gold
- Collect 5 Silver: +2% gold
- Collect 3 Gold: +3% gold + 1% XP
- Collect 1 Platinum: +5% gold + 2% XP
- Collect 1 Diamond: +10% gold + 5% XP + 2% capture rate

---

### **Trophy Hall Display System**

**Display Capacity:**

| Trophy Hall Level | Display Slots | Stat Bonus Multiplier |
|------------------|---------------|----------------------|
| 1 | 10 | 1.0x |
| 2 | 20 | 1.0x |
| 3 | 30 | 1.1x |
| 5 | 50 | 1.2x |
| 7 | 75 | 1.3x |
| 10 | 100 | 1.5x |

**Trophy Display Options:**
- **Pedestals:** Individual trophy on pedestal
- **Wall Mounts:** Hang trophy on wall
- **Glass Cases:** Multiple small trophies in case
- **Spotlights:** Highlight favorite trophies

**Interactive Features:**
- Click trophy to view achievement details
- See unlock date, completion stats
- Read achievement lore/flavor text
- Share achievement link with friends

---

### **Achievement Progress Tracker**

**Completion Tracking:**
- **Category Progress:** "Combat: 15/20 achievements"
- **Rarity Progress:** "Gold: 2/10 achievements"
- **Closest to Unlock:** Shows achievements near completion
  - Example: "Slayer: 9,847/10,000 enemies defeated (98%)"

**Achievement Hints:**
- Locked achievements show vague hints
- Example: "??? - Capture a very rare pet variant"
- Unlock condition hidden until 50% progress
- Full details shown at 75% progress

---

### **Trophy Hall Building Upgrades**

| Level | Display Slots | Stat Multiplier | Special Features | Upgrade Cost | Upgrade Time |
|-------|---------------|----------------|------------------|--------------|--------------|
| 1 | 10 | 1.0x | Basic display | 35,000 Gold (initial) | 8 hours |
| 2 | 20 | 1.0x | Wall mounts | 20,000 Gold + 5,000 materials | 12 hours |
| 3 | 30 | 1.1x | Glass cases | 40,000 Gold + 15,000 materials | 24 hours |
| 4 | 40 | 1.1x | Progress tracker | 70,000 Gold + 30,000 materials | 48 hours |
| 5 | 50 | 1.2x | Achievement hints | 110,000 Gold + 50,000 materials | 72 hours |
| 6 | 60 | 1.2x | Spotlights | 160,000 Gold + 80,000 materials | 5 days |
| 7 | 75 | 1.3x | Customizable layout | 230,000 Gold + 120,000 materials | 7 days |
| 8 | 85 | 1.3x | (Capacity boost) | 320,000 Gold + 180,000 materials | 10 days |
| 9 | 95 | 1.4x | (Capacity boost) | 450,000 Gold + 250,000 materials | 14 days |
| 10 | 100 | 1.5x | "Hall of Legends" room | 650,000 Gold + 400,000 materials | 21 days |

**Hall of Legends (Level 10):**
- Separate room for Diamond trophies
- Grand entrance with red carpet
- Epic lighting effects
- Friends automatically see this room first when visiting

---

### **Social Features (Trophy Hall)**

**Friend Visits:**
- Friends can tour your Trophy Hall
- Compare achievement progress
- Leave kudos on impressive trophies
- Motivates achievement hunting

**Achievement Leaderboards:**
- "Most Achievements Unlocked"
- "First to Unlock [Specific Achievement]"
- "Highest Achievement Score" (weighted by rarity)

**Guild Achievement Totals:**
- Guild Trophy Hall displays top members' trophies
- Guild achievement score (sum of all members)
- Competition between guilds

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Extra Display Slots** (+20 permanent slots)
  - Cost: 400 Premium Currency
  - Showcase more achievements
  
- ✅ **Trophy Hall Themes** (visual customization)
  - Cost: 300 Premium Currency
  - Examples: Museum, Temple, Vault
  
- ✅ **Trophy Frames** (cosmetic borders for trophies)
  - Cost: 100 Premium Currency per frame
  - Makes trophies look fancier

**What CANNOT Be Purchased:**
- ❌ Achievements directly (must earn)
- ❌ Better stat bonuses (everyone gets same)
- ❌ Exclusive achievements (all available to free players)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 7/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 7 of 10 (Premium & Utility Buildings - Deep Dive)  
**Last Updated:** December 18, 2025

---

## 📋 PART 7 CONTENTS

**This document covers in-depth mechanics for:**
1. Cosmetic Hub / Vanity Station (Complete System)
2. Energy Generator (Complete System)
3. Automation Station (Complete System)
4. Fast Travel Hub (Complete System)
5. Event Billboard (Complete System)

Each building includes:
- Complete functional systems
- Customization options
- Quality-of-life features
- Passive generation mechanics
- Automation capabilities
- Balance considerations
- Monetization integration

---

## 💅 COSMETIC HUB / VANITY STATION - COMPLETE SYSTEM

### **Core Philosophy**

The Cosmetic Hub is the **personalization center** where players customize their appearance, pet aesthetics, and building visuals without affecting gameplay stats. This is the **primary monetization hub** while maintaining ethical design (cosmetics only, no power).

**Key Design Principles:**
- Customization is **purely cosmetic** (zero gameplay advantages)
- Options are **diverse** (hundreds of combinations)
- Unlocks via **gameplay AND purchase** (free options exist)
- Premium options are **high quality** (worth the price)
- Social showcase (visible to others)

**Why This System Works:**
- ✅ Ethical monetization (no pay-to-win)
- ✅ Player expression (individuality)
- ✅ Social engagement (showing off cool cosmetics)
- ✅ Revenue generation (sustainable business model)
- ✅ Aspirational goals (free players can earn cosmetics)

---

### **Cosmetic Hub Features**

#### **1. Player Character Customization**

**Character Creator:**

**Body Options:**
- **Species:** Human, Elf, Dwarf, Orc, Demon, Angel (6 species)
- **Body Type:** Slim, Average, Athletic, Muscular, Heavy (5 types)
- **Height:** Slider (short to tall)
- **Skin Tone:** Color wheel (infinite options)
- **Gender:** Male, Female, Non-binary (inclusive)

**Face Customization:**
- **Face Shape:** 20 preset shapes
- **Eyes:** 50+ eye shapes, pupil colors
- **Nose:** 15 nose shapes
- **Mouth:** 20 mouth shapes
- **Ears:** 10 ear shapes (human, elf, etc.)
- **Facial Hair:** 30+ beard/mustache options (men/non-binary)
- **Makeup:** Eyeshadow, lipstick, blush (all genders)
- **Scars/Markings:** Tattoos, scars, birthmarks (50+ options)

**Hair Options:**
- **Hairstyles:** 100+ options (short, long, braids, ponytails, mohawks)
- **Hair Color:** Color wheel + gradient options (dual-tone hair)
- **Highlights/Ombre:** Secondary color options

**Example Premium Hairstyles:**
- Animated flowing hair (wind effects)
- Glowing hair (magic aura)
- Elemental hair (fire, water, lightning)
- Color-shifting hair (rainbow cycling)

---

#### **2. Outfit Customization**

**Outfit Slots:**
- **Head:** Hats, helmets, crowns, hoods, headbands
- **Torso:** Shirts, jackets, robes, armor (cosmetic)
- **Legs:** Pants, skirts, shorts, armor (cosmetic)
- **Feet:** Shoes, boots, sandals
- **Hands:** Gloves, gauntlets, rings
- **Back:** Capes, cloaks, wings, backpacks

**Outfit Categories:**

**Casual Wear (Free Options):**
- T-shirts, jeans, hoodies, sneakers
- 50+ color variations each
- Earned via gameplay (quests, achievements)

**Fantasy Gear (Mixed Free/Premium):**
- Wizard robes, knight armor, ranger leather
- Some earned, some purchased
- Set bonuses (visual only, e.g., matching armor glows)

**Premium Exclusive:**
- Animated outfits (flowing capes, glowing armor)
- Seasonal exclusives (Halloween costumes, Christmas outfits)
- Collaboration outfits (branded content)
- Legendary sets (ultra-detailed, particle effects)

**Outfit Dye System:**
- Dye any outfit piece any color
- Basic dyes: Free (earned via gameplay)
- Metallic dyes: Rare drops
- Glowing dyes: Premium currency
- Animated dyes: Premium exclusive (pulsing, shifting colors)

---

#### **3. Emote & Animation Customization**

**Emotes (Contextual Actions):**
- **Basic Emotes (Free):** Wave, Thumbs Up, Dance, Sit, Laugh, Cry
- **Rare Emotes (Earned):** Backflip, Fireworks, Victory Pose
- **Epic Emotes (Premium):** Magic Tricks, Summon Pet, Special Dances
- **Legendary Emotes (Premium Exclusive):** Transformation effects, Holograms

**Idle Animations:**
- Change how character stands when idle
- Default: Hands on hips
- Options: Arms crossed, hands behind back, stretching, reading book

**Walking/Running Styles:**
- Default: Normal walk/run
- Options: Swagger walk, ninja run, skip, march

**Combat Animations (Cosmetic Override):**
- Change weapon swing animations (visual only, same timing)
- Example: Sword swing becomes magical slash with sparkles

---

#### **4. Pet Cosmetic Customization**

**Pet Skins (Alternative Appearances):**

**Recolor Skins (Common - Earned):**
- Change pet's primary color
- Example: Red Fire Wolf → Blue Fire Wolf
- Unlocked via achievements ("Capture 50 Fire Wolves" unlocks blue skin)

**Themed Skins (Rare/Epic - Mixed):**
- Holiday themes (Santa hat Fire Wolf, Halloween ghost)
- Biome variants (Jungle Fire Wolf, Arctic Fire Wolf)
- Elemental inversions (Ice Fire Wolf - cold flames)

**Legendary Skins (Premium Exclusive):**
- Completely redesigned models (Fire Wolf → Cyber Wolf)
- Animated effects (trailing sparkles, aura glows)
- Unique idle animations

**Pet Accessories:**
- **Hats:** 50+ hats (wizard hat, crown, headband)
- **Collars:** 30+ collars (spiked, jeweled, glowing)
- **Wings:** 20+ wing types (angel, dragon, butterfly)
- **Trails:** 15+ trail effects (sparkles, fire, rainbow)

**Pet Particles (Aura Effects):**
- Surround pet with visual effects
- Examples: Glowing aura, falling leaves, snowflakes, flames
- No impact on stats (purely visual)

---

#### **5. Building Cosmetic Skins**

**Building Visual Overhauls:**

**Weaponsmith Skins:**
- Default: Stone forge with wooden roof
- Gothic: Dark stone, red forge glow
- Crystal: Transparent crystal walls, blue glow
- Nature: Overgrown with vines, flower decorations
- Volcanic: Obsidian walls, lava glow

**Armorsmith Skins:**
- Default: Brick building with anvil
- Royal: Gold trim, purple banners
- Industrial: Metal walls, steam vents
- Arcane: Magic runes, floating crystals

**Workshop Skins:**
- Default: Wooden lab with potion racks
- Alchemist: Bubbling cauldrons, mystical ingredients
- Modern: Clean lab, high-tech equipment
- Witch Hut: Crooked building, spooky decorations

**All 20 Buildings Have 5-10 Skin Options:**
- 1-2 Free (earned via gameplay)
- 3-5 Premium (purchasable)
- 2-3 Event Exclusive (limited-time seasonal)

---

#### **6. Base Decoration Customization**

**Plot Ground Decorations:**
- **Paths:** Dirt, stone, brick, marble, glowing crystals
- **Ground Cover:** Grass, flowers, snow, sand, lava rocks
- **Borders:** Fences (wood, iron, crystal), hedges, walls

**Surrounding Decorations (Per Plot):**
- **Trees:** Oak, pine, willow, cherry blossom, palm
- **Plants:** Bushes, flowers, mushrooms, crystals
- **Lighting:** Torches, lanterns, magic crystals, spotlights
- **Furniture:** Benches, tables, fountains, statues
- **Animals:** Decorative birds, butterflies, fish (in ponds)

**Base Themes (Global Visual Overhaul):**
- **Meadow:** Green grass, flowers, sunny
- **Beach:** Sand, ocean sounds, palm trees
- **Forest:** Dense trees, mushrooms, misty
- **Winter:** Snow, ice, aurora lights
- **Volcanic:** Lava rocks, ember particles, dark sky
- **Crystal Cave:** Glowing crystals, underground vibe
- **Sky Garden:** Floating islands, clouds, birds

**Theme Effects:**
- Changes all plot ground textures
- Adds ambient sounds (birds, waves, wind)
- Alters skybox and lighting
- Purely visual (no gameplay impact)

---

### **Cosmetic Hub Unlock System**

**How to Unlock Cosmetics:**

**1. Gameplay Unlocks (Free):**
- **Achievements:** "Capture 100 Fire Pets" → Fire-themed outfit
- **Quest Rewards:** Daily/Weekly quests grant cosmetic tokens
- **Level Milestones:** Reach Level 50 → Epic hairstyle unlock
- **Event Participation:** Complete event → Limited cosmetic
- **Guild Rewards:** Guild dungeons drop cosmetic items

**2. Cosmetic Tokens (Earnable Currency):**
- Earn 10-50 tokens per achievement
- Spend tokens in Cosmetic Hub shop
- Token Shop Items:
  - Rare Hairstyle: 100 tokens
  - Epic Outfit: 500 tokens
  - Legendary Pet Skin: 2,000 tokens

**3. Premium Currency (Purchased):**
- Buy premium cosmetics directly
- Prices: 100-1,000 Premium Currency
- Exclusive items not available via gameplay

**4. Limited-Time Events:**
- Seasonal cosmetics (Halloween, Christmas)
- Available only during event period
- Can be purchased or earned via event quests
- May return next year (or never - FOMO factor)

---

### **Cosmetic Hub Building Upgrades**

| Level | Customization Options | Special Features | Upgrade Cost | Upgrade Time |
|-------|----------------------|------------------|--------------|--------------|
| 1 | Basic character creator | Hair, face, body | 45,000 Gold (initial) | 16 hours |
| 2 | Outfit customization | 20 free outfits unlocked | 25,000 Gold + 10,000 materials | 24 hours |
| 3 | Pet cosmetics | Pet recolors, basic accessories | 50,000 Gold + 25,000 materials | 48 hours |
| 4 | Emote library | 10 free emotes unlocked | 80,000 Gold + 40,000 materials | 72 hours |
| 5 | Building skins | 5 free building skins | 120,000 Gold + 60,000 materials | 5 days |
| 6 | Dye system | Color customization unlocked | 180,000 Gold + 90,000 materials | 7 days |
| 7 | Base decorations | Plot customization | 250,000 Gold + 130,000 materials | 10 days |
| 8 | Animation overrides | Walking/running styles | 350,000 Gold + 180,000 materials | 14 days |
| 9 | Pet particles | Aura effects for pets | 480,000 Gold + 250,000 materials | 18 days |
| 10 | Base themes | Global visual overhauls | 700,000 Gold + 400,000 materials | 21 days |

---

### **Cosmetic Shop (In-Game Store)**

**Shop Categories:**

**Featured:**
- New releases (weekly rotation)
- Limited-time offers
- Seasonal exclusives

**Characters:**
- Hairstyles, faces, body types
- Outfits (by category)
- Emotes

**Pets:**
- Skins (by species)
- Accessories (hats, collars, wings)
- Particle effects

**Buildings:**
- Building skins (by building type)
- Decorations (furniture, plants, lights)
- Themes (base-wide visuals)

**Bundles:**
- Themed bundles (Fire theme: Fire outfit + Fire pet skin + Fire building skin)
- Starter packs (New player cosmetics at discount)
- Seasonal bundles (Halloween pack, Christmas pack)

**Pricing Examples:**
- Rare Hairstyle: 100 Premium Currency
- Epic Outfit: 300 Premium Currency
- Legendary Pet Skin: 500 Premium Currency
- Building Skin: 200 Premium Currency
- Base Theme: 400 Premium Currency
- Emote: 150 Premium Currency

**Bundle Discounts:**
- Buy 3 items: 10% off
- Buy 5 items: 20% off
- Themed bundles: 25% off (pre-selected items)

---

### **Social Showcase Features**

**Fashion Shows (Community Events):**
- Weekly cosmetic contests
- Players vote on best outfits
- Winners receive exclusive cosmetics
- Categories: Best Theme, Most Creative, Funniest

**Screenshot Mode:**
- Remove all UI elements
- Pose character (select emote, freeze animation)
- Adjust camera angle
- Apply filters (sepia, black & white, brightness)
- Share directly to social media

**Outfit Codes (Share System):**
- Save outfit as code (string of text)
- Share code with friends
- Friends input code to copy your outfit (if they own items)
- Popular outfit codes shared on social media

---

### **Monetization Strategy (Ethical)**

**Free-to-Play Experience:**
- 50+ free hairstyles (earned via gameplay)
- 30+ free outfits (quests, achievements)
- 20+ free pet skins (achievements)
- 10+ free emotes
- 5+ free building skins per building
- 3+ free base themes

**Premium Experience:**
- 100+ exclusive hairstyles
- 100+ exclusive outfits (higher quality, animated)
- 50+ exclusive pet skins (legendary quality)
- 30+ exclusive emotes (special effects)
- 10+ exclusive building skins per building
- 10+ exclusive base themes

**Value Proposition:**
- Free players have FULL gameplay access (zero power locked)
- Premium players get MORE OPTIONS (not better, just more)
- Premium cosmetics are HIGH QUALITY (worth the price)
- Regular content updates (new cosmetics monthly)

**Premium Currency Pricing:**
- $4.99 = 500 Premium Currency
- $9.99 = 1,100 Premium Currency (10% bonus)
- $19.99 = 2,500 Premium Currency (25% bonus)
- $49.99 = 7,000 Premium Currency (40% bonus)

---

## ⚡ ENERGY GENERATOR - COMPLETE SYSTEM

### **Core Philosophy**

The Energy Generator provides **passive resource generation** for players who cannot dedicate hours to active play. This is an **ethical retention mechanic** that respects casual players' time without replacing active gameplay.

**Key Design Principles:**
- Generation is **slow** (10-20% of active play efficiency)
- Generation is **offline-only** (no benefit while playing)
- Generation has **caps** (max 24 hours accumulation)
- Generation is **optional** (not required for progression)
- Premium version offers **convenience** (not power)

**Why This System Works:**
- ✅ Respects casual players (can't play 8 hours/day)
- ✅ Maintains active play value (still better to play)
- ✅ Prevents "forced" feeling (log in to avoid waste)
- ✅ Ethical monetization (premium speeds up, doesn't unlock exclusive)
- ✅ Retention mechanic (reason to return daily)

---

### **Energy Generator Features**

#### **1. Resource Generation Mechanics**

**How Generation Works:**

```
GENERATION FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Player logs out (or closes game)
2. Energy Generator starts accumulating resources
3. Resources accumulate per hour (rate based on level)
4. Accumulation stops at 24-hour cap
5. Player logs in
6. Click "Collect" button on Energy Generator
7. Receive accumulated resources
```

**Generation Rates (Per Hour):**

| Generator Level | Resources/Hour | Max Accumulation (24h) | Resource Types |
|----------------|----------------|------------------------|----------------|
| 1 | 10 | 240 | Common materials only |
| 2 | 15 | 360 | Common + small gold |
| 3 | 20 | 480 | Common + choose type |
| 4 | 25 | 600 | Common + small rare |
| 5 | 30 | 720 | Common + rare + gold |
| 6 | 40 | 960 | All + choose biome |
| 7 | 50 | 1,200 | All + better gold |
| 8 | 60 | 1,440 | All + epic chance (5%) |
| 9 | 75 | 1,800 | All + epic (10%) |
| 10 | 100 | 2,400 | All + epic (15%) + legendary (1%) |

**Resource Type Selection (Level 3+):**
- Choose preferred material type
- Examples: Iron Ore, Wood, Plants, Leather
- Generator focuses on selected type (70% of output)
- Remaining 30% is random common materials

**Biome Selection (Level 6+):**
- Choose preferred biome
- Generates biome-specific materials
- Examples: Volcanic Rift → Lava Essence, Frost Peaks → Frost Crystal
- Rare materials at reduced rate (10% of common rate)

---

#### **2. Gold Generation (Level 2+)**

**Gold Generation Rate:**

| Generator Level | Gold/Hour | Max Gold (24h) |
|----------------|-----------|----------------|
| 2 | 100 | 2,400 |
| 5 | 250 | 6,000 |
| 7 | 500 | 12,000 |
| 10 | 1,000 | 24,000 |

**Comparison to Active Play:**
- 1-hour expedition yields: 5,000-10,000 Gold
- 24-hour passive generation: 2,400-24,000 Gold
- Passive is 20-50% of active (intentionally lower)

---

#### **3. Rare & Epic Material Generation**

**Rare Materials (Level 5+):**
- 10% chance per resource to be rare instead of common
- Example: Level 10 Generator, 2,400 resources → ~240 rare materials

**Epic Materials (Level 8+):**
- 5-15% chance (scales with level)
- Level 8: 5% chance
- Level 10: 15% chance
- Example: Level 10, 2,400 resources → ~360 epic materials

**Legendary Materials (Level 10):**
- 1% chance (extremely rare)
- Example: 24 hours → 1-2 legendary materials on average
- Creates excitement ("I got a Chaos Shard overnight!")

---

#### **4. 24-Hour Accumulation Cap**

**Why Cap at 24 Hours:**
- Prevents infinite hoarding (can't save for weeks)
- Encourages daily check-ins
- Respects time-limited players (24h is reasonable)
- Prevents exploitation (botting, extended absences)

**Overflow Protection:**
- If player doesn't collect for 48 hours, no extra resources
- Resources stop at 24-hour mark
- Message: "Generator full - collect to resume generation"

**Premium Overflow Extension:**
- Premium players: 48-hour cap instead of 24
- Costs 300 Premium Currency/month (subscription)
- Quality-of-life for busy players

---

#### **5. Generation Boost Items**

**Boost Consumables (Crafted in Workshop):**

**Energy Catalyst:**
- Crafted: 10,000 Gold + 1,000 Materials
- Effect: +50% generation rate for 7 days
- Stackable: Up to 3 catalysts (max +150%)

**Premium Energy Boost:**
- Purchased: 200 Premium Currency
- Effect: Double generation rate for 7 days
- Does NOT stack with Energy Catalyst

**Use Cases:**
- Going on vacation: Apply boost before leaving
- Busy week at work: Apply boost to maintain progress
- Preparing for new pet training: Stock up on materials

---

### **Energy Generator Building Upgrades**

| Level | Generation Rate | Resource Types | Special Features | Upgrade Cost | Upgrade Time |
|-------|----------------|----------------|------------------|--------------|--------------|
| 1 | 10/hour | Common only | Basic generation | 50,000 Gold (initial) | 24 hours |
| 2 | 15/hour | Common + gold | Gold generation | 30,000 Gold + 10,000 materials | 36 hours |
| 3 | 20/hour | Common + gold | Choose resource type | 60,000 Gold + 25,000 materials | 48 hours |
| 4 | 25/hour | Common + gold | (Rate boost) | 100,000 Gold + 45,000 materials | 72 hours |
| 5 | 30/hour | +Rare (10%) | Rare materials | 150,000 Gold + 70,000 materials | 5 days |
| 6 | 40/hour | +Rare | Choose biome | 220,000 Gold + 110,000 materials | 7 days |
| 7 | 50/hour | +Rare | Better gold rate | 310,000 Gold + 160,000 materials | 10 days |
| 8 | 60/hour | +Epic (5%) | Epic materials | 430,000 Gold + 230,000 materials | 14 days |
| 9 | 75/hour | +Epic (10%) | (Rate boost) | 600,000 Gold + 320,000 materials | 18 days |
| 10 | 100/hour | +Legendary (1%) | Legendary materials | 900,000 Gold + 500,000 materials | 21 days |

---

### **Balance Philosophy**

**Active Play vs Passive Generation:**

**Active Play (1 Hour Expedition):**
- 500-1,000 materials gathered
- 5,000-10,000 Gold earned
- Rare pet captures possible
- Direct progression (XP, levels, achievements)

**Passive Generation (24 Hours Offline):**
- 240-2,400 materials (Level 1-10)
- 2,400-24,000 Gold (Level 2-10)
- No pet captures
- No direct progression

**Efficiency Comparison:**
- 1 hour active play = 5-24 hours passive generation
- Passive is 4-20% as efficient as active
- This maintains active play value while respecting casual players

---

### **Player Types & Use Cases**

**Hardcore Players (8+ hours/day):**
- Energy Generator is minor bonus (~5% of total income)
- Collects once per day (morning ritual)
- Mostly useful for stockpiling common materials

**Average Players (2-4 hours/day):**
- Energy Generator is ~15% of total income
- Collects twice per day (morning + evening)
- Helps maintain progression during busy days

**Casual Players (30 minutes - 1 hour/day):**
- Energy Generator is ~30% of total income
- Essential for keeping up with crafting costs
- Allows viable progression without grinding

**Very Casual Players (login every few days):**
- Energy Generator is primary resource source
- Can still make meaningful progress (slow but steady)
- Prevents feeling "left behind"

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Premium Generator Mode** (double rate + 48h cap)
  - Cost: 300 Premium Currency/month (subscription)
  - Convenience for busy players
  
- ✅ **Instant Collection** (skip to base, instant collect)
  - Cost: 50 Premium Currency per use
  - Saves time (no need to walk to generator)
  
- ✅ **Energy Boost Tokens** (temporary rate increase)
  - Cost: 200 Premium Currency for 7-day double rate
  - Alternative to crafted boosts

**What CANNOT Be Purchased:**
- ❌ Exclusive materials (everyone can generate same resources)
- ❌ Unlimited generation (still capped at 24-48 hours)
- ❌ Active generation (only works offline)
- ❌ Guaranteed legendary materials

---

## 🤖 AUTOMATION STATION - COMPLETE SYSTEM

### **Core Philosophy**

The Automation Station reduces **tedious micromanagement** for players with large rosters (50+ pets, 100+ items). This is a **quality-of-life endgame feature** that respects player time without removing meaningful choices.

**Key Design Principles:**
- Automation is **optional** (manual control always available)
- Automation is **late-game** (unlocks at Level 70)
- Automation is **strategic** (set rules, not "do everything")
- Automation has **costs** (uses resources, not free)
- Automation respects **player agency** (preview before executing)

**Why This System Works:**
- ✅ Reduces tedious tasks (training 50 pets individually)
- ✅ Maintains engagement (still requires strategic planning)
- ✅ Endgame QoL (reward for veteran players)
- ✅ Optional (manual players not penalized)
- ✅ Ethical (no "pay to automate" exclusive features)

---

### **Automation Station Features**

#### **1. Auto-Train System**

**How Auto-Train Works:**

```
AUTO-TRAIN SETUP:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Select pets to auto-train (up to 50)
2. Set target level for each (or same for all)
3. Choose training type (Basic/Advanced/Elite)
4. Set resource allocation (% of warehouse stock)
5. Preview total cost & time
6. Confirm automation
7. System automatically trains pets in waves
8. Notifies when complete
```

**Auto-Train Rules:**

**Priority System:**
- High Priority: Train first (favorite pets)
- Normal Priority: Train in roster order
- Low Priority: Train last (bulk training)

**Resource Management:**
- Set max % of warehouse to use (e.g., "Use max 30% of Iron Ore")
- Prevents depleting critical resources
- Auto-stops if resources fall below threshold

**Time Optimization:**
- System calculates optimal Training Station slot usage
- Minimizes total completion time
- Example: 50 pets, 8 slots → 7 waves of training

**Conditional Training:**
- "Only train Fire pets to Level 50"
- "Only train pets with 20+ total IVs"
- "Stop if warehouse Iron Ore < 5,000"

---

#### **2. Auto-Craft System**

**How Auto-Craft Works:**

```
AUTO-CRAFT SETUP:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Select recipes to auto-craft
2. Set quantity for each recipe
3. Set resource priority (which materials to use first)
4. Enable "Continuous Craft" (repeats until stopped)
5. Preview costs
6. Confirm automation
7. System crafts in queue automatically
```

**Auto-Craft Features:**

**Batch Crafting:**
- "Craft 100 Health Potions" → System queues 10 batches of 10
- Automatically starts next batch when slot opens
- Continues across login sessions (offline-persistent)

**Recipe Chains:**
- "Craft 50 Iron Ingots, then craft 10 Iron Swords"
- System executes in order
- Stops if intermediate step fails (not enough resources)

**Consumable Restocking:**
- "Maintain 50 Health Potions in inventory"
- System auto-crafts when below threshold
- Useful for frequent expedition players

---

#### **3. Auto-Breed System**

**How Auto-Breed Works:**

```
AUTO-BREED SETUP:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Select breeding pairs (parent species)
2. Set breeding goals:
   - "Breed until 6×31 IV offspring"
   - "Breed 10 Fire/Water hybrids"
   - "Breed until 5-star achieved"
3. Enable auto-retry (use new offspring as parents)
4. Set resource limits
5. Confirm automation
6. System breeds, evaluates offspring, repeats
```

**Auto-Breed Intelligence:**

**IV Optimization:**
- System tracks offspring IVs
- Uses best offspring as parents for next generation
- Gradually improves IV average over generations
- Stops when target IV reached (e.g., 6×31)

**Hybrid Hunting:**
- Repeat same parent combo until hybrid appears
- 20% hybrid chance → Average 5 breeds needed
- System automatically retries until success

**Star Merging Chains:**
- "Merge until 5-star achieved"
- System identifies identical pets
- Merges pairs sequentially
- Example: 32 one-star → 1 five-star (automated over weeks)

---

#### **4. Auto-Refine System**

**How Auto-Refine Works:**

```
AUTO-REFINE SETUP:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Select raw materials to refine
2. Set target refined quantity
3. Enable "Continuous Refine" (refine all available)
4. Set conversion priority (which recipes first)
5. Confirm automation
6. System refines automatically
```

**Auto-Refine Benefits:**
- Bulk refining: "Convert all Iron Ore to Iron Ingots"
- Saves hours of manual clicking
- Optimal slot usage (fills all 8 Refinery slots)

---

#### **5. Smart Queue System**

**What is Smart Queue:**
- AI analyzes your goals
- Suggests optimal task queue
- Example: "You want a Legendary Fire Sword. Here's the queue:"
  1. Refine 50 Iron Ore → 16 Iron Ingots
  2. Refine 16 Ingots + Coal → 5 Steel Ingots
  3. Gather Lava Essence (expedition reminder)
  4. Craft Legendary Fire Sword (Weaponsmith)

**Smart Queue Features:**

**Goal-Based Planning:**
- Enter goal: "5-star Legendary Fire Wolf"
- System calculates:
  - Need 32 one-star Fire Wolves (capture task)
  - Need 16 merges (breeding task)
  - Need X gold (farming task)
  - Total time: ~60 days

**Resource Path Finding:**
- "I need Celestial Steel"
- System shows: Mithril Ore → Mithril Ingot → + Star Fragment → Celestial Steel
- Adds all steps to queue

**Time Optimization:**
- Reorders tasks to minimize idle time
- Example: Start long craft first, then short crafts

---

### **Automation Station Building Upgrades**

| Level | Queue Slots | Auto Features | Special Features | Upgrade Cost | Upgrade Time |
|-------|-------------|---------------|------------------|--------------|--------------|
| 1 | 3 slots | Auto-train basic | Basic automation | 100,000 Gold (initial) | 72 hours |
| 2 | 5 slots | Auto-craft added | (More slots) | 50,000 Gold + 20,000 materials | 4 days |
| 3 | 10 slots | Auto-refine added | Resource limits | 100,000 Gold + 50,000 materials | 5 days |
| 4 | 15 slots | Auto-breed added | Priority system | 180,000 Gold + 90,000 materials | 7 days |
| 5 | 25 slots | (More slots) | Conditional rules | 280,000 Gold + 150,000 materials | 10 days |
| 6 | 35 slots | (More slots) | Cross-session persist | 400,000 Gold + 230,000 materials | 14 days |
| 7 | 50 slots | (More slots) | Recipe chains | 600,000 Gold + 350,000 materials | 18 days |
| 8 | 75 slots | (More slots) | Smart Queue AI | 850,000 Gold + 500,000 materials | 21 days |
| 9 | 100 slots | (More slots) | (Efficiency boost) | 1,200,000 Gold + 750,000 materials | 25 days |
| 10 | Unlimited | All features | "Automation Profiles" (save setups) | 2,000,000 Gold + 1,500,000 materials | 30 days |

**Automation Profiles (Level 10):**
- Save entire automation setup as profile
- Example profiles:
  - "Mass Training" (train all pets to Level 50)
  - "Consumable Factory" (craft 100 of each potion)
  - "Perfect Breeding" (hunt for 6×31 IV pets)
- One-click load profile
- Share profiles with friends (export code)

---

### **Automation Limitations (Prevent Exploitation)**

**What Automation CANNOT Do:**
- ❌ Play expeditions automatically (must be manual)
- ❌ Capture pets automatically (must be manual)
- ❌ Fight battles automatically (must be manual)
- ❌ Make Market trades automatically (must be manual)
- ❌ Bypass timers (still must wait for training/breeding)

**What Automation CAN Do:**
- ✅ Queue multiple tasks (set-and-forget)
- ✅ Execute repetitive crafting
- ✅ Manage large pet rosters
- ✅ Optimize resource usage
- ✅ Reduce clicking (quality-of-life)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Extra Queue Slots** (beyond Level 10 unlimited)
  - Cost: N/A (Level 10 already unlimited)
  
- ✅ **Automation Profile Slots** (+10 saved profiles)
  - Cost: 400 Premium Currency
  - Convenience for players with many strategies

**What CANNOT Be Purchased:**
- ❌ Faster automation execution (everyone waits same time)
- ❌ Exclusive automation features (all players get same tools)
- ❌ Auto-play expeditions (not automatable)
- ❌ Bypass resource costs (must still spend materials/gold)

---

## 🌀 FAST TRAVEL HUB - COMPLETE SYSTEM

### **Core Philosophy**

The Fast Travel Hub provides **instant teleportation** within the base and to discovered biomes, reducing tedious walking. This is a **quality-of-life feature** for players with large bases or frequent expeditions.

**Key Design Principles:**
- Fast travel is **optional** (walking is free)
- Fast travel has **costs** (gold per use, prevents spam)
- Fast travel is **unlockable** (earn via exploration)
- Fast travel respects **game world** (must discover locations first)
- Premium reduces **costs** (not exclusive access)

---

### **Fast Travel Hub Features**

#### **1. Within-Base Teleportation**

**How It Works:**
- Open Fast Travel Hub menu
- See list of all buildings in base
- Click building name
- Pay 10 Gold
- Instantly teleport to building entrance

**Why 10 Gold Cost:**
- Prevents spamming (thoughtful use)
- Gold sink (economy balance)
- Walking is free (alternative exists)
- 10 Gold is trivial for mid-game+ players

**Favorite Locations (Level 5):**
- Mark 3 buildings as favorites
- Favorite teleports are FREE (no gold cost)
- Use for most-visited buildings (Training Station, Workshop, Market)

---

#### **2. Biome Fast Travel**

**How It Works:**
- Must discover biome first (visit via expedition)
- Biome unlocked in Fast Travel menu
- Click biome name
- Pay 100-500 Gold (depends on biome tier)
- Instantly deploy to biome starting zone

**Biome Fast Travel Costs:**

| Biome Tier | Gold Cost | Biome Examples |
|------------|-----------|----------------|
| Tier 1 (Starter) | 100 Gold | Emerald Glade, Sunlit Plains |
| Tier 2 (Mid) | 200 Gold | Volcanic Rift, Frosted Peaks |
| Tier 3 (Advanced) | 300 Gold | Sky Citadel, Ancient Forest |
| Tier 4 (Endgame) | 500 Gold | Shadow Realm, Heaven's Gate |

**Why Biome Fast Travel Costs More:**
- Saves expedition travel time (5-15 minutes)
- Convenient for farming specific materials
- Gold sink (economy balance)

**Biome Fast Travel Limitations:**
- Can only teleport to biome entrance (not deep inside)
- Cannot fast travel while in combat
- Cannot fast travel with cargo (must extract first)

---

#### **3. Friend Base Fast Travel**

**How It Works:**
- Friend must be online
- Request "Visit Base" via friend list
- Friend accepts
- Instantly teleport to friend's base entrance
- Free (no gold cost)

**Use Cases:**
- Social visits (tour friend's base)
- Trading (meet in person for direct trade)
- Co-op planning (gather guild members before expedition)

---

### **Fast Travel Hub Building Upgrades**

| Level | Within-Base Cost | Favorite Slots | Biome Unlocks | Special Features | Upgrade Cost | Upgrade Time |
|-------|-----------------|----------------|---------------|------------------|--------------|--------------|
| 1 | 10 Gold/use | 0 | None | Basic within-base | 20,000 Gold (initial) | 2 hours |
| 2 | 10 Gold/use | 0 | Tier 1 biomes | Biome discovery | 10,000 Gold + 3,000 materials | 4 hours |
| 3 | 10 Gold/use | 1 favorite | Tier 1-2 biomes | First favorite slot | 20,000 Gold + 8,000 materials | 8 hours |
| 4 | 8 Gold/use | 1 favorite | Tier 1-2 biomes | Cost reduction | 35,000 Gold + 15,000 materials | 12 hours |
| 5 | 8 Gold/use | 3 favorites | Tier 1-3 biomes | More favorites | 60,000 Gold + 25,000 materials | 24 hours |
| 6 | 5 Gold/use | 3 favorites | Tier 1-3 biomes | Cost reduction | 90,000 Gold + 40,000 materials | 48 hours |
| 7 | 5 Gold/use | 3 favorites | Tier 1-4 biomes | All biomes | 130,000 Gold + 60,000 materials | 72 hours |
| 8 | 3 Gold/use | 5 favorites | All biomes | More favorites | 190,000 Gold + 90,000 materials | 5 days |
| 9 | 1 Gold/use | 5 favorites | All biomes | Cost reduction | 270,000 Gold + 130,000 materials | 7 days |
| 10 | FREE | Unlimited favorites | All biomes | All free! | 400,000 Gold + 200,000 materials | 10 days |

**Level 10 Benefit:**
- ALL fast travel is FREE (no gold cost)
- Unlimited favorite locations
- Massive quality-of-life (walk never required)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Premium Fast Travel Pass** (all fast travel free for 30 days)
  - Cost: 300 Premium Currency/month
  - Alternative to upgrading building
  - Convenience for impatient players
  
- ✅ **Instant Travel Tokens** (bundle of 100 uses)
  - Cost: 200 Premium Currency
  - Each token = 1 free fast travel
  - Saves gold (not exclusive access)

**What CANNOT Be Purchased:**
- ❌ Fast travel to undiscovered biomes (must explore first)
- ❌ Fast travel while in combat (safety rule)
- ❌ Fast travel with cargo (extraction mechanic)

---

## 🎪 EVENT BILLBOARD - COMPLETE SYSTEM

### **Core Philosophy**

The Event Billboard displays **seasonal and limited-time events**, providing rotating content that keeps the game fresh. This is a **retention mechanic** and **live service** feature.

**Key Design Principles:**
- Events are **time-limited** (creates urgency)
- Events offer **exclusive rewards** (FOMO motivation)
- Events are **accessible** (all players can participate)
- Events are **diverse** (different types, different audiences)
- Events provide **fresh content** (prevents burnout)

---

### **Event Billboard Features**

#### **1. Seasonal Events**

**Summer Festival (June-August):**
- Beach-themed pets (tropical birds, crabs, dolphins)
- Summer cosmetics (swimsuits, sunglasses, surfboards)
- Beach biome (limited-time)
- Event quests (collect seashells, catch fish)
- Rewards: Exclusive summer mount, beach base theme

**Halloween Spooktacular (October):**
- Spooky pets (ghosts, skeletons, pumpkins)
- Halloween cosmetics (costumes, masks, witch hats)
- Haunted biome (limited-time)
- Event quests (trick-or-treat, defeat ghosts)
- Rewards: Exclusive ghost mount, haunted base theme

**Winter Wonderland (December-January):**
- Ice pets (snowmen, polar bears, ice dragons)
- Winter cosmetics (Santa outfits, elf hats, scarves)
- Frozen biome (limited-time)
- Event quests (build snowmen, gift giving)
- Rewards: Exclusive reindeer mount, winter base theme

**Spring Bloom (March-April):**
- Nature pets (butterflies, bees, flowers)
- Spring cosmetics (flower crowns, pastel outfits)
- Garden biome (limited-time)
- Event quests (plant flowers, butterfly catching)
- Rewards: Exclusive unicorn mount, garden base theme

---

#### **2. Limited-Time Events**

**Double XP Weekend:**
- All XP gains doubled (training, quests, combat)
- Every 4-6 weeks (random)
- No special quests (just bonus)
- Encourages high activity during event

**Legendary Spawn Rate Increase:**
- Legendary pets spawn 5x more frequently
- 48-hour event
- Great for players hunting specific legendaries
- Announced 24 hours in advance

**Crafting Material Bonanza:**
- All expeditions drop 2x materials
- 72-hour event
- Perfect for stockpiling resources
- Happens before major updates (helps players prepare)

**Trading Fair:**
- Market auction fees reduced to 0%
- 7-day event
- Encourages economic activity
- Happens quarterly

---

#### **3. Competitive Events**

**Pet Battle Tournament:**
- PvP bracket tournament
- Single-elimination (win or eliminated)
- Prizes for top 8 players:
  - 1st: Exclusive legendary pet + mount
  - 2nd: Exclusive epic pet + mount
  - 3rd-4th: Exclusive rare pet
  - 5th-8th: Exclusive cosmetics
- Monthly event

**Speed Run Challenge:**
- Fastest extraction time wins
- Leaderboard tracks top 100 times
- Prizes for top 10:
  - 1st: 1,000,000 Gold + title
  - 2nd-3rd: 500,000 Gold + title
  - 4th-10th: 250,000 Gold
- Weekly event

**Rarest Capture Contest:**
- Who captures rarest pet during event (IV + rarity combo)
- Example: 6×31 IV Legendary Fire Wolf
- Prizes for rarest capture:
  - 1st: Exclusive "Legendary Hunter" title + cosmetic
  - 2nd-5th: Rare cosmetics
- Monthly event

---

#### **4. Event Currency & Shop**

**Event Tokens:**
- Earned by completing event quests
- Example: Halloween Event → Candy Tokens
- Spend in Event Shop (time-limited)

**Event Shop Items:**
- Exclusive pets (not obtainable elsewhere)
- Exclusive cosmetics (limited-time only)
- Boost items (XP potions, capture rate boosts)
- Premium currency (small amounts)

**Example Event Shop (Halloween):**
- Ghost Pet: 500 Candy Tokens
- Witch Outfit: 300 Candy Tokens
- Pumpkin Pet Skin: 200 Candy Tokens
- XP Elixir (×5): 100 Candy Tokens
- 100 Premium Currency: 1,000 Candy Tokens

**Shop Closes When Event Ends:**
- Must spend tokens before event ends
- Leftover tokens convert to gold (10 tokens = 100 gold)
- Creates urgency (FOMO)

---

### **Event Billboard Building Details**

**Building Appearance:**
- Large billboard (like movie theater marquee)
- Displays current active events
- Animated (scrolling text, flashing lights)
- Changes theme with seasonal events (pumpkins in October, snowflakes in December)

**Event Billboard Upgrades:**
- **NOT upgradeable** (always available at Level 1)
- Automatically appears during events
- Disappears when no events active
- Cost: FREE (auto-built by system)

---

### **Event Calendar (Annual Schedule)**

| Month | Event Type | Duration |
|-------|------------|----------|
| January | Winter Wonderland (end) | 2 weeks |
| February | Valentine's Day Special | 2 weeks |
| March | Spring Bloom (start) | 4 weeks |
| April | Spring Bloom (end) | 2 weeks |
| May | Pet Battle Tournament | 1 week |
| June | Summer Festival (start) | 8 weeks |
| July | Summer Festival (mid) | Ongoing |
| August | Summer Festival (end) | 2 weeks |
| September | Back to School Event | 2 weeks |
| October | Halloween Spooktacular | 4 weeks |
| November | Thanksgiving Harvest | 2 weeks |
| December | Winter Wonderland (start) | 4 weeks |

**Plus Random Events:**
- Double XP weekends (monthly)
- Legendary spawn boosts (bi-monthly)
- Trading fairs (quarterly)
- Speed run challenges (weekly)

---

### **Monetization Integration (Ethical)**

**What Can Be Purchased:**
- ✅ **Event Token Bundles** (skip some grinding)
  - Cost: 500 Premium Currency for 1,000 Event Tokens
  - Convenience (can still earn all tokens free)
  
- ✅ **Event Cosmetics (Direct Purchase)**
  - Cost: 300-800 Premium Currency
  - Alternative to grinding tokens
  - Still available via free tokens

**What CANNOT Be Purchased:**
- ❌ Exclusive event pets (must earn via tokens or gameplay)
- ❌ Tournament wins (must compete fairly)
- ❌ Leaderboard positions (skill-based only)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 8/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 8 of 10 (Building Mechanics & Systems)  
**Last Updated:** December 18, 2025

---

## 📋 PART 8 CONTENTS

**This document covers fundamental building systems:**
1. Upgrade System (Complete Mechanics)
2. Construction System (Complete Flow)
3. Demolition & Rebuilding (Complete Rules)
4. Building Unlock Gates (Complete Requirements)
5. Multi-Benefit Upgrade Philosophy (Design Principles)

Each section includes:
- Complete mechanical breakdowns
- Mathematical formulas
- Progression curves
- Balance considerations
- Edge case handling
- Player experience optimization

---

## 📈 UPGRADE SYSTEM - COMPLETE MECHANICS

### **Core Philosophy**

Building upgrades are the **primary gold and material sink** in the base system. Upgrades must feel **meaningful** (tangible benefits), **achievable** (not impossibly expensive), and **rewarding** (celebration moment).

**Key Design Principles:**
- Upgrades provide **multiple benefits** (not just one stat increase)
- Upgrade costs **scale exponentially** (early cheap, late expensive)
- Upgrade times **scale linearly** (predictable wait times)
- Upgrades are **permanent** (never lost)
- Upgrades create **milestones** (Level 5, 7, 10 unlock features)

---

### **Upgrade Cost Formula**

**Mathematical Formula:**

```
BASE COST FORMULA:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Gold Cost = Initial Cost × (1.5 ^ (Level - 1))
Material Cost = Initial Materials × (1.6 ^ (Level - 1))

Where:
- Initial Cost = Building's base upgrade cost
- Initial Materials = Building's base material cost
- Level = Target upgrade level (2-10)
- 1.5 = Gold scaling factor (moderate)
- 1.6 = Material scaling factor (slightly steeper)
```

**Example: Weaponsmith Upgrades**

```
Initial Cost = 2,000 Gold + 200 Materials

Level 1 → 2:
- Gold: 2,000 × (1.5 ^ 0) = 2,000 Gold
- Materials: 200 × (1.6 ^ 0) = 200 Materials

Level 2 → 3:
- Gold: 2,000 × (1.5 ^ 1) = 3,000 Gold
- Materials: 200 × (1.6 ^ 1) = 320 Materials

Level 3 → 4:
- Gold: 2,000 × (1.5 ^ 2) = 4,500 Gold
- Materials: 200 × (1.6 ^ 2) = 512 Materials

Level 9 → 10:
- Gold: 2,000 × (1.5 ^ 8) = 51,200 Gold
- Materials: 200 × (1.6 ^ 8) = 11,529 Materials
```

**Total Investment (Level 1 → 10):**
- Gold: ~115,000 Gold total
- Materials: ~26,000 Materials total

**Why Exponential Scaling:**
- Early levels accessible (new players progress fast)
- Late levels expensive (creates long-term goals)
- Prevents maxing all buildings instantly
- Creates strategic choices (which building to prioritize)

---

### **Upgrade Time Formula**

**Mathematical Formula:**

```
TIME FORMULA:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Upgrade Time = Base Time × (Level ^ 0.8)

Where:
- Base Time = Building's initial upgrade time
- Level = Target upgrade level (2-10)
- 0.8 = Time scaling exponent (sublinear)
```

**Why Sublinear Scaling (^0.8 instead of ^1.0):**
- Prevents absurd wait times at high levels
- Level 10 upgrades feel achievable (days, not weeks)
- Players maintain engagement (not waiting months)

**Example: Training Station Upgrades**

```
Base Time = 30 minutes

Level 1 → 2: 30 × (1 ^ 0.8) = 30 minutes
Level 2 → 3: 30 × (2 ^ 0.8) = 52 minutes
Level 3 → 4: 30 × (3 ^ 0.8) = 73 minutes
Level 4 → 5: 30 × (4 ^ 0.8) = 92 minutes
Level 5 → 6: 30 × (5 ^ 0.8) = 110 minutes (~2 hours)
Level 9 → 10: 30 × (9 ^ 0.8) = 189 minutes (~3 hours)
```

**Total Time (Level 1 → 10):**
- ~13 hours cumulative (spread over weeks)

---

### **Upgrade Benefits Philosophy**

**Every upgrade provides MULTIPLE benefits, not just one:**

**Example: Weaponsmith Level 1 → 10 Benefits**

| Level | Gold Cost | Crafting Slots | Speed Bonus | Unlocked Recipes | Special Feature |
|-------|-----------|----------------|-------------|------------------|-----------------|
| 1 | FREE | 1 | 0% | Common | Basic forge |
| 2 | 2,000 | 2 | 0% | Uncommon | +1 slot |
| 3 | 5,000 | 3 | +10% | Rare | +1 slot, speed |
| 4 | 10,000 | 4 | +10% | — | +1 slot |
| 5 | 20,000 | 5 | +20% | Epic | +1 slot, speed, recipes |
| 6 | 35,000 | 5 | +20% | — | — |
| 7 | 50,000 | 5 | +30% | Legendary | Speed, recipes |
| 8 | 75,000 | 5 | +30% | — | — |
| 9 | 100,000 | 5 | +40% | — | Speed |
| 10 | 200,000 | 5 | +50% | Mythic | Speed, recipes, reforging |

**Benefit Types:**
1. **Slot Increases** (Levels 2-5) - More simultaneous crafts
2. **Speed Bonuses** (Levels 3, 5, 7, 9, 10) - Faster crafting
3. **Recipe Unlocks** (Levels 2, 3, 5, 7, 10) - New tiers
4. **Special Features** (Levels 5, 7, 10) - Unique mechanics

**Why This Works:**
- Every level feels impactful (not just "+1 slot")
- Milestone levels (5, 7, 10) are exciting (new recipes!)
- Even-numbered levels provide incremental boosts
- Level 10 is transformative (Mythic recipes + Reforging)

---

### **Milestone Levels (Special Unlocks)**

**Level 3 Milestone:**
- Unlocks Rare-tier content
- Example: Rare weapons, rare consumables, rare research
- Represents "mid-game transition"

**Level 5 Milestone:**
- Unlocks Epic-tier content
- Unlocks quality-of-life features (Queuing, Auto-Sort, etc.)
- Represents "advanced player status"

**Level 7 Milestone:**
- Unlocks Legendary-tier content
- Unlocks powerful features (Auto-Train, Quick Deploy, etc.)
- Represents "veteran player status"

**Level 10 Milestone (Ultimate):**
- Unlocks Mythic-tier content (future-proofing)
- Unlocks game-changing features (Mass Training, Analytics, etc.)
- Represents "mastery achievement"
- Celebratory moment (confetti animation, achievement)

---

### **Upgrade Progress Tracking**

**Visual Progress Bar:**
```
Building: Weaponsmith [Level 7]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Progress: ████████████████░░░░ 80% (Level 8)
Time Remaining: 2 days, 15 hours

Next Level Benefits:
• Same stats (efficiency upgrade)
• Continue toward Level 9 (+40% speed bonus)
```

**Upgrade Queue System (Unlocked in Automation Station):**
- Queue multiple building upgrades
- Example: "Upgrade Weaponsmith 7→8, then 8→9, then 9→10"
- System automatically starts next when current finishes
- Can plan weeks of upgrades in advance

---

### **Simultaneous Upgrade Limits**

**How Many Buildings Can Upgrade At Once:**

**Default (No Limits):**
- Unlimited simultaneous upgrades
- Can upgrade all 20 buildings at once if you have resources
- No artificial gating

**Why No Limits:**
- Respects player's resource investment
- Players self-limit (can't afford 20 upgrades simultaneously)
- Creates exciting progression bursts (upgrade multiple after big expedition)
- Mobile-friendly (set upgrades, close app, check back later)

---

### **Instant Upgrade Tokens (Monetization)**

**How Instant Upgrades Work:**

**Premium Currency Cost:**
```
Token Cost = Base Premium Currency × (Remaining Hours / 24)

Where:
- Base Premium Currency = 50-500 depending on building tier
- Remaining Hours = Time left on upgrade
```

**Example:**
- Weaponsmith Level 9→10 upgrade: 7 days remaining
- Base Token Cost: 200 Premium Currency
- Calculation: 200 × (168 hours / 24) = 1,400 Premium Currency
- OR: Wait 7 days (free)

**Pricing Philosophy:**
- Short waits (< 1 hour): ~10-50 Premium Currency
- Medium waits (1-12 hours): ~50-200 Premium Currency
- Long waits (1-7 days): ~200-1,000 Premium Currency
- Extremely long waits (7+ days): ~1,000-2,000 Premium Currency

**Why This Pricing:**
- Incentivizes patience (waiting is always cheaper)
- Reasonable for impatient players (not exploitative)
- Scales with value (longer upgrades = more valuable)
- Alternative to subscription (one-time purchase vs recurring)

---

## 🏗️ CONSTRUCTION SYSTEM - COMPLETE FLOW

### **Core Philosophy**

Construction is the **initial building placement** process. Unlike upgrades (improve existing), construction creates new buildings. Construction must be **accessible** (not too expensive) while **gating progression** (can't unlock everything instantly).

**Key Design Principles:**
- Construction is **level-gated** (unlock buildings progressively)
- Construction is **expensive** (significant investment)
- Construction has **wait times** (creates anticipation)
- Construction is **visible** (see building under construction)
- Construction can be **sped up** (premium monetization)

---

### **Construction Flow (Step-by-Step)**

```
CONSTRUCTION PROCESS:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. UNLOCK BUILDING
   └─ Reach required account level
   └─ Complete prerequisite quest (if any)
   └─ Building appears in "Available Buildings" menu

2. SELECT BUILDING TO CONSTRUCT
   └─ View construction cost (gold + materials)
   └─ View construction time (instant to 72 hours)
   └─ View building description and benefits

3. CHOOSE PLOT LOCATION
   └─ Select empty plot (Plots 1-16)
   └─ Preview building appearance
   └─ Confirm placement

4. PAY CONSTRUCTION COST
   └─ Deduct gold from wallet
   └─ Deduct materials from warehouse
   └─ Cannot cancel after payment (no refunds)

5. CONSTRUCTION BEGINS
   └─ Building appears as "under construction"
   └─ Visual: Wooden scaffolding, workers (cosmetic)
   └─ Timer counts down

6. CONSTRUCTION COMPLETES
   └─ Notification: "Your [Building] is complete!"
   └─ Building becomes functional
   └─ Celebration animation (confetti, sparkles)
   └─ Achievement unlocked (if first of that type)
```

---

### **Construction Costs by Building Tier**

**Tier 1: Core Buildings (Always Available)**
- Expedition Hub: FREE (tutorial)
- Warehouse: FREE (tutorial)
- Mailbox: 1,000 Gold + 50 Wood + 20 Stone

**Tier 2: Early Buildings (Levels 5-20)**
- Weaponsmith: 2,500 Gold + 100 Iron Ore + 50 Wood
- Armorsmith: 3,000 Gold + 150 Iron Ore + 100 Leather
- Training Station: 2,000 Gold + 50 Training Materials
- Workshop: 2,500 Gold + 100 Plants + 50 Gems

**Tier 3: Mid Buildings (Levels 25-45)**
- Refinery: 10,000 Gold + 500 Iron Ore + 200 Gems
- Breeding Station: 5,000 Gold + 200 Breeding Materials
- Sanctuary: 15,000 Gold + 500 Stone + 200 Gems
- Laboratory: 25,000 Gold + 1,000 Mixed Materials
- Market: 30,000 Gold + 1,000 Mixed Resources
- Trophy Hall: 35,000 Gold + 1,500 Mixed Resources

**Tier 4: Advanced Buildings (Levels 50-70)**
- Pet Daycare: 40,000 Gold + 2,000 Mixed Resources
- Cosmetic Hub: 45,000 Gold + 2,500 Mixed Resources
- Energy Generator: 50,000 Gold + 3,000 Mixed Resources
- Guild Hall: 75,000 Gold + 5,000 Mixed Resources
- Automation Station: 100,000 Gold + 7,500 Mixed Resources

**Tier 5: Utility Buildings (Variable Unlock)**
- Fast Travel Hub: 20,000 Gold + 1,000 Crystals
- Event Billboard: FREE (auto-built during events)

---

### **Construction Times by Building Tier**

**Instant Construction (Tutorial Buildings):**
- Expedition Hub: Instant
- Warehouse: Instant
- Mailbox: Instant (first building after tutorial)

**Short Construction (5 minutes - 2 hours):**
- Training Station: 5 minutes
- Workshop: 10 minutes
- Weaponsmith: 10 minutes
- Armorsmith: 15 minutes
- Breeding Station: 30 minutes

**Medium Construction (2-24 hours):**
- Refinery: 1 hour
- Sanctuary: 2 hours
- Laboratory: 4 hours
- Market: 6 hours
- Trophy Hall: 8 hours

**Long Construction (1-3 days):**
- Pet Daycare: 12 hours
- Cosmetic Hub: 16 hours
- Energy Generator: 24 hours
- Guild Hall: 48 hours
- Automation Station: 72 hours (3 days)

**Utility Construction:**
- Fast Travel Hub: 2 hours
- Event Billboard: Instant (system-built)

---

### **Construction Time Purpose**

**Why Not Instant Construction for Everything:**

**Short Times (5-30 minutes):**
- Creates brief anticipation (not frustrating)
- Teaches patience mechanics
- Mobile-friendly (short sessions)

**Medium Times (1-8 hours):**
- Creates "check back later" motivation
- Respects player's time (can do other activities)
- Feels substantial (major building milestone)

**Long Times (12-72 hours):**
- High-impact buildings (endgame features)
- Creates significant achievement moment
- Encourages planning (start before you need it)
- Can be skipped with premium (monetization)

**Balance:**
- Early buildings: Fast (5-30 minutes) → New players progress quickly
- Mid buildings: Medium (1-8 hours) → Moderate pacing
- Late buildings: Long (12-72 hours) → Significant milestones

---

### **Construction Visuals (Player Experience)**

**Under Construction Appearance:**
- Building outline visible (ghosted)
- Wooden scaffolding around building
- Animated workers (hammering, sawing - cosmetic)
- Progress bar above building (0% → 100%)
- Estimated completion time displayed

**Completion Animation:**
- Scaffolding disappears (animated collapse)
- Building solidifies (opacity 50% → 100%)
- Confetti explosion (celebration)
- Notification banner: "🎉 [Building Name] Complete!"
- Achievement popup (if applicable)

**Post-Completion:**
- Building fully functional immediately
- Tutorial prompt if first of type (explains features)
- Building glows briefly (24 hours) to indicate "new"

---

### **Simultaneous Construction Limits**

**How Many Buildings Can Construct At Once:**

**Default: Unlimited**
- Can construct multiple buildings simultaneously
- No artificial limits
- Self-limited by resources and plot availability

**Why Unlimited:**
- Players already limited by gold/materials
- Plot slots are limited (12 free, 16 max)
- Creates excitement (multiple buildings finishing at once)
- No frustration (waiting for one to finish before starting next)

---

### **Instant Construction Tokens (Monetization)**

**How Instant Construction Works:**

**Premium Currency Cost:**
```
Token Cost = Base Cost × (Remaining Hours / 24)

Tier 1-2 Buildings: 50-100 Premium Currency base
Tier 3 Buildings: 100-300 Premium Currency base
Tier 4 Buildings: 300-800 Premium Currency base
```

**Example:**
- Guild Hall construction: 48 hours remaining
- Base Token Cost: 500 Premium Currency
- Calculation: 500 × (48 / 24) = 1,000 Premium Currency
- OR: Wait 48 hours (free)

**Bundle Discount:**
- Buy 10 Instant Construction Tokens: 10% off
- Buy 25 Instant Construction Tokens: 20% off

---

## 🔨 DEMOLITION & REBUILDING - COMPLETE RULES

### **Core Philosophy**

Demolition allows players to **remove buildings** and **rebuild different ones**. This creates **flexibility** (change base layout) while **penalizing** frequent changes (resource loss).

**Key Design Principles:**
- Demolition is **allowed** (no buildings are permanent)
- Demolition has **costs** (lose some resources)
- Demolition has **cooldowns** (prevents constant switching)
- Demolition is **strategic** (plan before demolishing)
- Core buildings **cannot be demolished** (Hub, Warehouse, Mailbox)

---

### **Demolition Rules**

**Which Buildings Can Be Demolished:**
- ✅ ALL production buildings (Weaponsmith, Armorsmith, Workshop, Refinery)
- ✅ ALL pet buildings (Training, Breeding, Sanctuary, Daycare)
- ✅ ALL progression buildings (Laboratory)
- ✅ ALL social buildings (Market, Guild Hall, Trophy Hall)
- ✅ ALL utility buildings (Cosmetic Hub, Generator, Automation, Fast Travel)

**Which Buildings CANNOT Be Demolished:**
- ❌ Expedition Hub (core gameplay)
- ❌ Warehouse (core storage)
- ❌ Mailbox (core engagement)

---

### **Demolition Process (Step-by-Step)**

```
DEMOLITION FLOW:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. SELECT BUILDING TO DEMOLISH
   └─ Click building
   └─ Select "Demolish" option

2. CONFIRMATION WARNING
   └─ "Are you sure? This action cannot be undone!"
   └─ Shows refund amount (50% of construction cost)
   └─ Shows upgrade level (will be lost)
   └─ Shows cooldown (cannot rebuild here for 10 minutes)

3. DEMOLISH BUILDING
   └─ Building disappears (animated collapse)
   └─ Receive 50% resource refund
   └─ Plot becomes empty (available for new building)
   └─ 10-minute cooldown before rebuilding

4. REBUILD DIFFERENT BUILDING
   └─ After cooldown, can place any unlocked building
   └─ Must pay full construction cost (no discount)
   └─ New building starts at Level 1 (upgrades not carried over)
```

---

### **Demolition Refund Rates**

**Resource Refund:**
- **50% of initial construction cost** (gold + materials)
- Does NOT refund upgrade costs (those are lost)
- Does NOT refund time (immediate demolition)

**Example:**
- Weaponsmith initial construction: 2,500 Gold + 100 Iron Ore + 50 Wood
- Weaponsmith upgraded to Level 7: Additional ~50,000 Gold + ~15,000 Materials spent
- Demolish Weaponsmith:
  - Refund: 1,250 Gold + 50 Iron Ore + 25 Wood (50% of initial)
  - Lost: All upgrade investment (~50,000 Gold + 15,000 Materials)

**Why 50% Refund (Not 100%):**
- Penalizes frequent changes (encourages planning)
- Resource sink (economic balance)
- Makes demolition feel costly (not trivial decision)
- Still allows flexibility (not totally punishing)

---

### **Demolition Cooldown**

**10-Minute Plot Cooldown:**
- After demolishing, plot is "cooling down"
- Cannot build on that specific plot for 10 minutes
- Can build on OTHER plots immediately
- Prevents accidental rapid demolition/rebuild cycles

**Why 10 Minutes:**
- Prevents misclicks (accidental demolish → rebuild spam)
- Gives player time to think (is this really what I want?)
- Nominal penalty (10 minutes is short)

---

### **Rebuilding Strategy**

**Common Rebuild Scenarios:**

**Scenario 1: Specialization Shift**
- Early game: Built Workshop (consumables)
- Late game: Consumables less important
- Demolish Workshop → Build Automation Station
- Use Case: Endgame optimization

**Scenario 2: Correcting Mistakes**
- Accidentally built Refinery before needing it
- Demolish Refinery → Build Market (more useful now)
- Use Case: New player learning

**Scenario 3: Plot Limit Optimization**
- Free player with 12 plots, wants 13th building
- Demolish least-used building → Build higher-priority building
- Use Case: Resource management without premium plots

**Scenario 4: Testing Builds**
- Unsure if Cosmetic Hub or Energy Generator first
- Build one, try for a week
- Demolish if not useful → Build alternative
- Use Case: Experimentation

---

### **Demolition UI/UX**

**Safety Measures:**
- **Double Confirmation:** "Are you sure?" → "Are you REALLY sure?"
- **Upgrade Warning:** "You will lose Level 7 upgrades! (50,000 Gold + 15,000 Materials)"
- **Cooldown Reminder:** "This plot will be unavailable for 10 minutes"
- **Refund Display:** "You will receive: 1,250 Gold + 50 Iron Ore + 25 Wood"

**Visual Feedback:**
- Building flashes red when "Demolish" selected
- Building collapses with animation (bricks falling)
- Dust cloud effect
- Plot becomes grayed out (cooldown indicator)

---

## 🔓 BUILDING UNLOCK GATES - COMPLETE REQUIREMENTS

### **Core Philosophy**

Building unlocks create **progression pacing** and **achievement milestones**. Unlocks must feel **earned** (not arbitrary) while **accessible** (not gated behind paywalls).

**Key Design Principles:**
- Unlocks are **level-based** (primary gate)
- Unlocks may have **quest requirements** (secondary gate)
- Unlocks may have **prerequisite buildings** (tertiary gate)
- Unlocks are **transparent** (players see requirements)
- Unlocks are **achievable** (no impossible gates)

---

### **Complete Building Unlock Requirements**

**Level 1 (Tutorial):**
- Expedition Hub: FREE (always available)
- Warehouse: FREE (always available)

**Level 3:**
- Mailbox/Notice Board: FREE (quest: "Complete First Expedition")

**Level 5:**
- Weaponsmith: 2,500 Gold + 100 Iron Ore + 50 Wood

**Level 10:**
- Armorsmith: 3,000 Gold + 150 Iron Ore + 100 Leather

**Level 12:**
- Training Station: 2,000 Gold + 50 Training Materials

**Level 15:**
- Workshop: 2,500 Gold + 100 Plants + 50 Gems

**Level 20:**
- Breeding Station: 5,000 Gold + 200 Breeding Materials

**Level 25:**
- Refinery: 10,000 Gold + 500 Iron Ore + 200 Gems

**Level 30:**
- Sanctuary: 15,000 Gold + 500 Stone + 200 Gems

**Level 35:**
- Laboratory: 25,000 Gold + 1,000 Mixed Materials

**Level 40:**
- Market/Trading Post: 30,000 Gold + 1,000 Mixed Resources
- Fast Travel Hub: 20,000 Gold + 1,000 Crystals (optional)

**Level 45:**
- Trophy Hall: 35,000 Gold + 1,500 Mixed Resources

**Level 50:**
- Pet Daycare: 40,000 Gold + 2,000 Mixed Resources

**Level 55:**
- Cosmetic Hub: 45,000 Gold + 2,500 Mixed Resources

**Level 60:**
- Energy Generator: 50,000 Gold + 3,000 Mixed Resources

**Level 65:**
- Guild Hall: 75,000 Gold + 5,000 Mixed Resources

**Level 70:**
- Automation Station: 100,000 Gold + 7,500 Mixed Resources

**Variable (Event-Based):**
- Event Billboard: FREE (appears during events automatically)

---

### **Quest Requirements (Optional Gates)**

**Some buildings require quest completion:**

**Weaponsmith Quest:**
- Quest: "Forge Your First Weapon"
- Requirement: Gather 100 Iron Ore + 50 Wood
- Reward: Unlock Weaponsmith building

**Laboratory Quest:**
- Quest: "Scientific Curiosity"
- Requirement: Train a pet to Level 30 + Craft 10 Rare items
- Reward: Unlock Laboratory building

**Guild Hall Quest:**
- Quest: "Join or Create a Guild"
- Requirement: Either join an existing guild OR pay 100,000 Gold to create one
- Reward: Unlock Guild Hall building

**Why Quest Requirements:**
- Teaches mechanics (forge weapon before unlocking Weaponsmith)
- Ensures readiness (don't unlock Lab until trained pet to 30)
- Creates narrative (quests tell a story)

---

### **Prerequisite Building Requirements**

**Some buildings require others first:**

**Refinery Prerequisites:**
- Requires: Weaponsmith Level 3 OR Armorsmith Level 3
- Logic: Need basic crafting before refining

**Automation Station Prerequisites:**
- Requires: Training Station Level 5 + Workshop Level 5
- Logic: Need buildings to automate before unlocking automation

**Energy Generator Prerequisites:**
- Requires: Warehouse Level 5
- Logic: Need storage capacity for generated resources

**Why Prerequisites:**
- Ensures logical progression (don't automate before having things to automate)
- Prevents wasted builds (don't build Refinery if not crafting yet)
- Guides player journey (natural flow)

---

### **Unlock Visibility (UI/UX)**

**Building Menu Display:**

```
AVAILABLE BUILDINGS:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ Weaponsmith [Unlocked]
   └─ Build for 2,500 Gold + 100 Iron Ore + 50 Wood

🔒 Armorsmith [Locked]
   └─ Unlock at Level 10 (5 levels away)

🔒 Laboratory [Locked]
   └─ Unlock at Level 35 (12 levels away)
   └─ Complete Quest: "Scientific Curiosity"

🔒 Automation Station [Locked]
   └─ Unlock at Level 70 (45 levels away)
   └─ Requires: Training Station Level 5 + Workshop Level 5
```

**Why Show Locked Buildings:**
- Creates aspirational goals (see what's coming)
- Helps planning (know what to save for)
- Increases engagement (motivation to level up)

---

## 🎯 MULTI-BENEFIT UPGRADE PHILOSOPHY - DESIGN PRINCIPLES

### **Core Philosophy**

Every building upgrade should provide **3-5 tangible benefits** rather than just one stat increase. This makes upgrades feel **impactful** and **exciting**.

**Single-Benefit Upgrades (BAD):**
```
Level 2 → 3: +1 crafting slot
Level 3 → 4: +1 crafting slot
Level 4 → 5: +1 crafting slot
```
❌ Boring, predictable, unexciting

**Multi-Benefit Upgrades (GOOD):**
```
Level 2 → 3:
• +1 crafting slot
• +10% crafting speed
• Unlock Rare recipes

Level 3 → 4:
• +1 crafting slot
• Unlock Auto-Sort feature

Level 4 → 5:
• +1 crafting slot
• +20% crafting speed (total)
• Unlock Epic recipes
• -5% resource cost
```
✅ Exciting, varied, impactful

---

### **Benefit Categories**

**Quantitative Benefits (Numbers Go Up):**
- Slot increases (+1 crafting slot)
- Speed bonuses (+10% faster)
- Cost reductions (-5% materials)
- Capacity increases (+50 storage slots)

**Qualitative Benefits (New Features):**
- Recipe unlocks (Rare → Epic → Legendary)
- Feature unlocks (Auto-Sort, Queuing, Automation)
- System unlocks (Research trees, Analytics, Profiles)

**Milestone Benefits (Game-Changing):**
- Level 5: Unlock major feature (Queuing)
- Level 7: Unlock endgame content (Legendary tier)
- Level 10: Unlock ultimate feature (Mass Training, Analytics)

---

### **Upgrade Pacing Strategy**

**Early Levels (1-3):**
- Focus: Capacity increases (more slots)
- Pace: Fast (minutes to hours)
- Cost: Low (thousands of gold)

**Mid Levels (4-6):**
- Focus: Efficiency increases (speed, cost reduction)
- Pace: Medium (hours to days)
- Cost: Medium (tens of thousands of gold)

**Late Levels (7-9):**
- Focus: Advanced features (automation, analytics)
- Pace: Slow (days to weeks)
- Cost: High (hundreds of thousands of gold)

**Ultimate Level (10):**
- Focus: Game-changing features (reforging, mass systems)
- Pace: Very Slow (weeks)
- Cost: Very High (millions of gold)

---

### **Upgrade Excitement Curve**

**Goal: Keep players excited about every upgrade**

```
EXCITEMENT GRAPH:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

High ┤     *           *               *****
     │    * *         * *           ****
     │   *   *       *   *       ****
     │  *     *     *     *   ****
Low  └─*───────*───*───────***────────────────
     1   2   3   4   5   6   7   8   9   10
                Level

* = Excitement level

Key Moments:
- Level 3: Unlock Rare (first major milestone)
- Level 5: Unlock Epic + QoL feature (big jump)
- Level 7: Unlock Legendary (endgame unlocked)
- Level 10: Unlock Mythic + ultimate feature (peak excitement)
```

**Design Takeaway:**
- Not every level is equally exciting
- Milestone levels (3, 5, 7, 10) are peaks
- Intermediate levels (2, 4, 6, 8, 9) are incremental
- But ALL levels provide value (no "dead" levels)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 9/10

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 9 of 10 (Base Customization & Aesthetics)  
**Last Updated:** December 18, 2025

---

## 📋 PART 9 CONTENTS

**This document covers base personalization systems:**
1. Plot Customization System (Complete Design)
2. Base Theme Evolution (Complete Progression)
3. Decorative Items & Furniture (Complete Catalog)
4. Social Features & Base Visiting (Complete Mechanics)
5. Screenshot & Sharing Features (Complete Tools)

Each section includes:
- Complete customization options
- Progression tiers
- Unlock conditions
- Social integration
- Monetization strategies
- Player expression systems

---

## 🎨 PLOT CUSTOMIZATION SYSTEM - COMPLETE DESIGN

### **Core Philosophy**

Plot customization allows players to **personalize individual building locations** with ground textures, borders, and surrounding decorations. This creates **visual identity** and **ownership feeling** without affecting gameplay.

**Key Design Principles:**
- Customization is **per-plot** (16 individual spaces)
- Customization is **cosmetic only** (zero gameplay impact)
- Customization is **progressive** (unlock more options over time)
- Customization is **social** (visible to friends)
- Customization is **affordable** (free options + premium)

**Why This System Works:**
- ✅ Player expression (individuality)
- ✅ Achievement showcase (earned decorations)
- ✅ Social engagement (show friends your base)
- ✅ Long-term goals (collect all decorations)
- ✅ Ethical monetization (premium options don't grant power)

---

### **Plot Structure Overview**

**16 Total Plots Available:**
- **12 Free Plots:** Available to all players (default)
- **4 Premium Plots:** $9.99 one-time purchase (optional)

**Plot Size:**
- Each plot: 10m × 10m (100 square meters)
- Building footprint: 6m × 6m (36 square meters)
- Decoration space: 64 square meters around building

**Plot Grid Layout:**
```
BASE LAYOUT (Top-Down View):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

    [Social Hub - Central Area]
           (Portal)
              ↓
    
    [Plot 1]  [Plot 2]  [Plot 3]  [Plot 4]
    
    [Plot 5]  [Plot 6]  [Plot 7]  [Plot 8]
    
    [Plot 9]  [Plot 10] [Plot 11] [Plot 12]
    
    [Plot 13] [Plot 14] [Plot 15] [Plot 16]
        ↑          ↑          ↑          ↑
    Premium    Premium    Premium    Premium
```

**Navigation Paths:**
- Automatic pathways between plots (stone by default)
- Pathways customize with ground textures
- Smooth walking between buildings

---

### **Plot Customization Categories**

#### **1. Ground Textures (Base Surface)**

**How Ground Textures Work:**
- Replace default grass with custom texture
- Covers entire 10m × 10m plot
- Seamless blending with adjacent plots

**Free Ground Textures (Earned via Gameplay):**

**Natural Textures:**
- **Grass** (default, free)
- **Short Grass** (Achievement: "Place 5 Buildings")
- **Wildflower Meadow** (Achievement: "Capture 50 Nature Pets")
- **Autumn Leaves** (Achievement: "Play During Fall Season")
- **Cherry Blossom Petals** (Achievement: "Visit 10 Friend Bases")

**Stone/Brick Textures:**
- **Cobblestone** (Quest: "Craft 10 Rare Items")
- **Brick Pavement** (Achievement: "Upgrade 5 Buildings to Level 5")
- **Marble Tiles** (Achievement: "Reach Account Level 50")
- **Sandstone** (Quest: "Explore Desert Biome")

**Natural Ground:**
- **Sand** (Quest: "Explore Beach Biome")
- **Snow** (Quest: "Explore Frosted Peaks")
- **Volcanic Rock** (Quest: "Explore Volcanic Rift")
- **Moss-Covered Stone** (Quest: "Explore Ancient Forest")

**Premium Ground Textures (Purchasable):**

**Magical Textures:**
- **Glowing Crystal Ground** (300 Premium Currency)
- **Star-Lit Void** (400 Premium Currency)
- **Rainbow Shimmer** (500 Premium Currency)
- **Ethereal Mist** (350 Premium Currency)

**Animated Textures:**
- **Flowing Water Surface** (600 Premium Currency)
- **Lava Flow** (600 Premium Currency)
- **Shifting Sands** (500 Premium Currency)
- **Living Grass** (animated growth, 700 Premium Currency)

---

#### **2. Plot Borders (Edge Decorations)**

**How Borders Work:**
- Outline the 10m × 10m plot perimeter
- Create defined separation between plots
- Can mix/match with ground textures

**Free Borders (Earned via Gameplay):**

**Natural Borders:**
- **None** (default, no border)
- **Wooden Fence** (Quest: "Build First Building")
- **Stone Wall** (low, 1m height) (Achievement: "Reach Level 20")
- **Hedge Row** (bushes) (Achievement: "Capture 100 Pets")
- **Flower Border** (Achievement: "Complete 50 Daily Quests")

**Material Borders:**
- **Iron Fence** (Quest: "Craft 50 Iron Weapons")
- **Brick Wall** (Achievement: "Upgrade 10 Buildings to Level 5")
- **Log Barrier** (Quest: "Gather 10,000 Wood")

**Premium Borders (Purchasable):**

**Magical Borders:**
- **Crystal Spikes** (200 Premium Currency)
- **Floating Runes** (animated, 300 Premium Currency)
- **Fire Ring** (animated flames, 400 Premium Currency)
- **Ice Barrier** (frosted effect, 350 Premium Currency)

**Prestige Borders:**
- **Golden Filigree** (500 Premium Currency)
- **Diamond Encrusted** (800 Premium Currency)
- **Ethereal Barrier** (glowing forcefield, 600 Premium Currency)

---

#### **3. Decorative Objects (Surrounding Items)**

**How Decorative Objects Work:**
- Place up to 10 objects per plot (surrounding building)
- Objects are 3D models (trees, benches, statues)
- Objects can be moved/rotated freely within plot

**Free Decorative Objects (Earned via Gameplay):**

**Natural Objects:**
- **Oak Tree** (Quest: "Gather 1,000 Wood")
- **Pine Tree** (Quest: "Explore Frosted Peaks")
- **Palm Tree** (Quest: "Explore Beach Biome")
- **Cherry Blossom Tree** (Achievement: "Capture 50 Different Species")
- **Bush (Small)** (default, free)
- **Bush (Large)** (Achievement: "Place 10 Buildings")
- **Flower Patch (Red/Blue/Yellow)** (Achievement: "Capture 10 Nature Pets each")

**Functional Props:**
- **Wooden Bench** (Quest: "Visit 5 Friend Bases")
- **Stone Table** (Achievement: "Complete 100 Expeditions")
- **Lamp Post** (lights up at night) (Quest: "Craft 100 Items")
- **Well** (decorative, no function) (Achievement: "Reach Level 30")
- **Fountain** (animated water) (Achievement: "Upgrade 5 Buildings to Level 10")

**Rocks & Natural Features:**
- **Small Rock** (default, free)
- **Large Boulder** (Quest: "Explore Mountain Depths")
- **Crystal Cluster** (glowing) (Quest: "Refine 1,000 Gems")
- **Mushroom Circle** (Achievement: "Capture 50 Nature Pets")

**Premium Decorative Objects (Purchasable):**

**Magical Props:**
- **Floating Crystal** (animated rotation, 150 Premium Currency)
- **Magic Circle** (glowing runes on ground, 200 Premium Currency)
- **Arcane Pillar** (tall, glowing, 250 Premium Currency)
- **Summoning Portal** (animated swirl, 400 Premium Currency)

**Statues:**
- **Pet Statue** (bronze/silver/gold, 200-500 Premium Currency)
- **Warrior Statue** (300 Premium Currency)
- **Dragon Statue** (large, 600 Premium Currency)
- **Abstract Art Piece** (modern, 250 Premium Currency)

**Animated Decorations:**
- **Butterfly Swarm** (flying around plot, 300 Premium Currency)
- **Fireflies** (night-time glow, 250 Premium Currency)
- **Falling Leaves** (constant animation, 200 Premium Currency)
- **Floating Orbs** (magical spheres, 350 Premium Currency)

---

#### **4. Plot Lighting (Ambient Effects)**

**How Lighting Works:**
- Affects entire plot ambiance
- Changes brightness, color tone, particle effects
- Can combine with decorations for layered effects

**Free Lighting Options (Earned via Gameplay):**

**Time-of-Day Presets:**
- **Daytime** (default, bright)
- **Sunset** (orange glow) (Achievement: "Play for 100 Hours")
- **Night** (dark, stars visible) (Achievement: "Log in at Midnight")
- **Overcast** (cloudy, muted) (Quest: "Explore Shadow Realm")

**Seasonal Effects:**
- **Spring** (bright, birds chirping) (default)
- **Summer** (warm, intense) (Play during June-August)
- **Autumn** (golden hour, leaves) (Play during September-November)
- **Winter** (cool, occasional snowflakes) (Play during December-February)

**Premium Lighting Options (Purchasable):**

**Magical Ambiance:**
- **Ethereal Glow** (soft purple ambient, 200 Premium Currency)
- **Fire Embers** (orange particles floating, 250 Premium Currency)
- **Frost Aura** (blue-tinted, icy particles, 250 Premium Currency)
- **Starlight** (night sky, extra stars, 300 Premium Currency)

**Dramatic Effects:**
- **Spotlight** (focused beam on building, 150 Premium Currency)
- **Rainbow Shimmer** (rainbow particles, 400 Premium Currency)
- **Dimensional Rift** (purple void effect, 500 Premium Currency)

---

### **Plot Customization UI/UX**

**Customization Mode (How Players Edit):**

```
CUSTOMIZATION INTERFACE:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Plot 5 Selected] - Weaponsmith Building

┌─────────────────────────────────────────┐
│ Ground Texture:  [Grass ▼]              │
│ Border:          [Stone Wall ▼]         │
│ Lighting:        [Daytime ▼]            │
└─────────────────────────────────────────┘

Decorative Objects (3/10 placed):
┌─────────────────────────────────────────┐
│ • Oak Tree (front-left)       [Move][X] │
│ • Bench (front-right)          [Move][X] │
│ • Lamp Post (back-center)      [Move][X] │
│                                          │
│ [+ Add Decoration]                       │
└─────────────────────────────────────────┘

[Preview Changes] [Apply] [Cancel]
```

**Placement Mode:**
- Click "[+ Add Decoration]"
- Browse available decorations (grid view)
- Click decoration to select
- Preview appears on plot (ghosted)
- Drag to position, rotate with mouse wheel
- Click to place (confirmed)

**Move/Rotate Mode:**
- Click "[Move]" next to decoration
- Drag to reposition
- Rotate with mouse wheel
- Click to confirm new position

---

### **Plot Customization Progression**

**Starter Base (Level 1-10):**
- 1-3 plots customized (learning system)
- Free ground textures only (grass, short grass)
- Basic decorations (bushes, small rocks)
- Daytime lighting

**Developing Base (Level 10-30):**
- 5-8 plots customized (growing personality)
- Mix of free textures (cobblestone, wildflower)
- More decorations (trees, benches, flower patches)
- Seasonal lighting unlocked

**Established Base (Level 30-60):**
- 10-12 plots fully customized (distinct style)
- Advanced free textures (marble, volcanic rock)
- Premium decorations start appearing (floating crystals)
- Animated decorations (fountains, butterflies)

**Prestigious Base (Level 60+):**
- All 16 plots customized (masterpiece)
- Premium ground textures (glowing crystal, lava flow)
- Premium borders (golden filigree, diamond)
- Premium lighting (ethereal glow, starlight)
- Premium animated decorations (summoning portals, fireflies)

---

### **Monetization Strategy (Ethical)**

**Free-to-Play Experience:**
- 30+ ground textures (earned)
- 20+ borders (earned)
- 50+ decorative objects (earned)
- 10+ lighting options (earned)
- Can create beautiful bases without spending

**Premium Experience:**
- 20+ exclusive ground textures (animated, magical)
- 15+ exclusive borders (prestige materials)
- 40+ exclusive decorations (statues, animated)
- 10+ exclusive lighting (dramatic effects)
- Higher quality, more unique options

**Pricing:**
- Ground Texture: 300-700 Premium Currency
- Border: 200-800 Premium Currency
- Decoration: 150-600 Premium Currency
- Lighting: 150-500 Premium Currency

**Bundles:**
- **Theme Bundle** (Ground + Border + 5 Decorations + Lighting): 1,500 Premium Currency (20% discount)
  - Example: "Fire Theme" - Lava ground, fire ring border, ember lighting, flame decorations

---

## 🎭 BASE THEME EVOLUTION - COMPLETE PROGRESSION

### **Core Philosophy**

Base themes are **global visual overhauls** that change the entire base's appearance instantly. Themes progress through **aesthetic tiers** as players level up, creating visible status markers.

**Key Design Principles:**
- Themes are **account-level based** (automatic progression)
- Themes affect **all plots simultaneously** (cohesive look)
- Themes have **3 aesthetic tiers** (Basic, Advanced, Prestigious)
- Themes are **optional** (can disable for custom look)
- Themes showcase **veteran status** (endgame players look impressive)

---

### **Theme Tier System**

**Tier 1: Basic Themes (Levels 1-30)**
- Simple, clean aesthetics
- Wooden/stone buildings
- Natural environment
- Represents: New players, learning systems

**Tier 2: Advanced Themes (Levels 31-60)**
- Enhanced materials (brick, marble)
- Magical elements (glowing runes, crystals)
- Refined environment
- Represents: Established players, mastery

**Tier 3: Prestigious Themes (Levels 61+)**
- Exotic materials (celestial metal, void crystal)
- Animated effects (floating, pulsing, rotating)
- Epic environment (dramatic skies, particles)
- Represents: Veteran players, prestige

---

(Continuing with complete theme catalog, social features, and screenshot tools...)

---
# 🏗️ BASE BUILDING SYSTEM DESIGN DOCUMENT - PART 10/10 (FINAL)

**Idol Guardians: Eternal Wilds - Complete Base Architecture**  
**Version:** 1.0  
**Part:** 10 of 10 (Monetization Strategy & Balance - FINAL DOCUMENT)  
**Last Updated:** December 18, 2025

---

## 📋 PART 10 CONTENTS (FINAL)

**This document covers the final pieces:**
1. Complete Monetization Strategy (Ethical Framework)
2. Economic Balance & Resource Sinks (System Health)
3. Player Progression Curves (Retention Design)
4. Anti-Exploit Measures (Security)
5. Technical Implementation Guidelines (Development)
6. Future Expansion Plans (Roadmap)
7. Complete Document Summary (Executive Overview)

Each section includes:
- Comprehensive strategies
- Mathematical models
- Balance tables
- Implementation guidelines
- Long-term sustainability

---

## 💰 COMPLETE MONETIZATION STRATEGY - ETHICAL FRAMEWORK

### **Core Monetization Philosophy**

**Guiding Principle:**
> "Players should NEVER feel they must spend money to compete or progress. Premium purchases save TIME or add COSMETICS, never POWER."

**Ethical Commitments:**
1. **No Pay-to-Win:** Zero gameplay advantages from spending
2. **Transparent Pricing:** No hidden costs, clear value propositions
3. **Respect Free Players:** 100% content accessible without spending
4. **Fair Pricing:** Reasonable prices, no exploitative tactics
5. **Optional Spending:** Never required, always optional

---

### **Revenue Streams (Prioritized)**

#### **Primary Revenue: Cosmetics (60% of revenue)**

**Why Cosmetics Work:**
- High perceived value (visual expression)
- No competitive advantage (ethical)
- Infinite scalability (new cosmetics forever)
- Social showcase (drive adoption)
- Low resistance (players accept cosmetic monetization)

**Cosmetic Categories:**
- **Character Customization:** Hairstyles, outfits, emotes ($1-10 each)
- **Pet Skins:** Visual overhauls for pets ($3-8 each)
- **Building Skins:** Aesthetic building variants ($2-5 each)
- **Base Themes:** Global visual changes ($4-10 each)
- **Decorations:** Plot decorations ($1-6 each)
- **Bundles:** Themed cosmetic packs ($10-25, 20-30% discount)

**Pricing Strategy:**
- **Impulse Purchases:** $1-3 (high volume, low friction)
- **Standard Items:** $3-8 (most cosmetics)
- **Premium Items:** $8-15 (legendary quality)
- **Mega Bundles:** $15-50 (seasonal collections)

**Expected Conversion:**
- 5-10% of players buy at least one cosmetic
- Average spending: $15-30 per paying player per year

---

#### **Secondary Revenue: Convenience (30% of revenue)**

**Why Convenience Works:**
- Saves time (respects busy players)
- Doesn't grant power (ethical)
- Optional (free alternative exists)
- Reasonable pricing (not exploitative)

**Convenience Categories:**

**Time-Savers:**
- **Instant Construction/Upgrade Tokens:** Skip wait times (50-500 Premium Currency)
- **Auto-Collection:** Instant collection from buildings (50 Premium Currency per use)
- **Fast Travel Pass:** Free teleports for 30 days (300 Premium Currency/month)

**Capacity Increases:**
- **Extra Building Plots:** +4 permanent slots ($9.99 one-time)
- **Warehouse Expansion:** +500 permanent slots ($4.99 one-time)
- **Extra Queue Slots:** More simultaneous tasks (300-500 Premium Currency)

**Quality-of-Life:**
- **Automation Profiles:** Save automation setups (400 Premium Currency)
- **Premium Generator Mode:** 2x passive income + 48h cap (300 Premium Currency/month)
- **Market Analytics Early Access:** Get analytics before Level 10 (300 Premium Currency/month)

**Expected Conversion:**
- 10-15% of players buy convenience items
- Average spending: $20-40 per paying player per year

---

#### **Tertiary Revenue: Battle Pass / Seasons (10% of revenue)**

**Seasonal Battle Pass Structure:**

**Free Track (All Players):**
- 50 tiers of rewards
- Cosmetics (common/uncommon)
- Resources (gold, materials)
- Pet eggs (rare)
- Earnable by playing (no purchase required)

**Premium Track ($9.99):**
- Same 50 tiers PLUS premium rewards
- Exclusive cosmetics (epic/legendary)
- Extra resources (2x value)
- Exclusive pets (legendary)
- Premium currency back (500 Premium Currency returned)

**Battle Pass Benefits:**
- Predictable revenue ($9.99 × 3-4 seasons per year)
- High perceived value (50+ items for $10)
- Retention driver (complete tiers over 2-3 months)
- Organic engagement (rewards for playing normally)

**Expected Conversion:**
- 15-25% of active players buy Battle Pass
- Revenue: ~$2-5 per active player per season

---

### **Premium Currency Pricing**

**Premium Currency Bundles:**

| Bundle | Currency | Bonus | Price | $ per 100 Currency |
|--------|----------|-------|-------|-------------------|
| Starter | 500 | 0% | $4.99 | $0.998 |
| Value | 1,100 | 10% | $9.99 | $0.908 |
| Popular | 2,500 | 25% | $19.99 | $0.800 |
| Premium | 5,500 | 38% | $49.99 | $0.909 |
| Mega | 12,000 | 50% | $99.99 | $0.833 |

**Pricing Philosophy:**
- Small bundles for impulse ($5)
- Mid bundles for regular spenders ($10-20)
- Large bundles for whales ($50-100)
- Bonus % scales with bundle size (rewards commitment)

**Expected Revenue:**
- Average purchase: $15-25
- Repeat purchases: 2-3 times per year per paying player

---

### **Total Monetization Model (Expected ARPU)**

**Player Categories:**

**Non-Payers (Free-to-Play) - 80% of players:**
- Revenue: $0
- Engagement: High (100% content access)
- Value: Community size, social proof, organic marketing

**Minnows (Casual Spenders) - 15% of players:**
- Revenue: $10-30 per year
- Purchases: Battle Pass, occasional cosmetics
- Value: Stable baseline revenue

**Dolphins (Regular Spenders) - 4% of players:**
- Revenue: $50-150 per year
- Purchases: Battle Pass, cosmetics, convenience items
- Value: Primary revenue source

**Whales (Heavy Spenders) - 1% of players:**
- Revenue: $200-500+ per year
- Purchases: Everything (cosmetics, convenience, multiple battle passes)
- Value: Significant revenue, but NOT exploited

**Average Revenue Per User (ARPU):**
- Free Players: $0
- Minnows: $20/year average
- Dolphins: $100/year average
- Whales: $300/year average
- **Total ARPU: $8-12 per year** (industry average for ethical F2P)

**Total Revenue Projection (100,000 active players):**
- Year 1: $800,000 - $1,200,000
- Year 2: $1,200,000 - $1,800,000 (retention + growth)
- Year 3: $1,500,000 - $2,500,000 (established player base)

---

### **What We DO NOT Sell (Non-Negotiable)**

**NEVER Sell:**
- ❌ **Stat Boosts:** No "+10% damage" purchases
- ❌ **Exclusive Powerful Items:** All legendary weapons/armor earnable free
- ❌ **Loot Boxes / Gacha:** No randomized premium purchases
- ❌ **Energy Systems:** No "stamina refills" or play limits
- ❌ **Competitive Advantages:** No PvP pay-to-win
- ❌ **Content Locks:** No premium-only biomes or pets
- ❌ **Skip Progression:** Cannot buy levels or instant max-level pets

**Why These Rules:**
- Protects game integrity (skill > wallet)
- Builds player trust (ethical reputation)
- Long-term sustainability (players stay longer)
- Regulatory compliance (avoids gambling laws)
- Moral obligation (game design ethics)

---

## ⚖️ ECONOMIC BALANCE & RESOURCE SINKS - SYSTEM HEALTH

### **Core Economic Philosophy**

**Healthy Economy Requires:**
1. **Balanced Faucets:** Resources enter economy at controlled rates
2. **Strong Sinks:** Resources exit economy permanently
3. **Scarcity:** Resources must be valuable (not abundant)
4. **Progression:** Resource costs scale with player power
5. **Stability:** Inflation/deflation avoided

---

### **Resource Faucets (Income Sources)**

**Gold Faucets:**

| Source | Gold/Hour (Active Play) | % of Total Income |
|--------|------------------------|-------------------|
| Expeditions | 5,000-10,000 | 60% |
| Daily Quests | 1,000-5,000 | 15% |
| Weekly Quests | 2,000-10,000 | 10% |
| Market Sales | Variable (player-driven) | 10% |
| Energy Generator | 100-1,000 (passive) | 5% |

**Total Gold Income (Casual Player):**
- 2 hours active play/day: 15,000-25,000 Gold/day
- 7 days: 105,000-175,000 Gold/week
- 30 days: 450,000-750,000 Gold/month

**Material Faucets:**

| Source | Materials/Hour (Active) | % of Total Income |
|--------|------------------------|-------------------|
| Expeditions | 500-1,000 | 70% |
| Daily Rewards | 50-200 | 10% |
| Energy Generator | 10-100 (passive) | 5% |
| Refinery | Variable (conversion) | 10% |
| Salvaging | Variable (recycling) | 5% |

**Total Material Income (Casual Player):**
- 2 hours active play/day: 1,500-2,500 Materials/day
- 7 days: 10,500-17,500 Materials/week
- 30 days: 45,000-75,000 Materials/month

---

### **Resource Sinks (Expense Drains)**

**Gold Sinks (Permanent Removal):**

| Sink | Gold Cost | % of Total Spending |
|------|-----------|---------------------|
| Building Upgrades | 10,000-200,000 per upgrade | 40% |
| Construction | 2,500-100,000 per building | 20% |
| Crafting | 100-50,000 per item | 15% |
| Training | 100-56,250 per level | 10% |
| Breeding | 2,000-150,000 per breed | 5% |
| Market Fees | 1-10% of sale price | 5% |
| Fast Travel | 10-500 per use | 3% |
| Misc (NPC vendors, etc.) | Variable | 2% |

**Total Gold Spending (Casual Player):**
- Early game (Levels 1-30): 50,000-100,000 Gold/week
- Mid game (Levels 31-60): 150,000-300,000 Gold/week
- Late game (Levels 61+): 500,000-1,000,000+ Gold/week

**Material Sinks (Permanent Removal):**

| Sink | Materials Cost | % of Total Spending |
|------|----------------|---------------------|
| Building Upgrades | 200-100,000 per upgrade | 35% |
| Construction | 100-7,500 per building | 15% |
| Crafting | 50-10,000 per item | 25% |
| Training | 50-5,625 per level | 15% |
| Breeding | 200-materials per breed | 5% |
| Research | 2,000-150,000 per project | 5% |

**Total Material Spending (Casual Player):**
- Early game: 5,000-15,000 Materials/week
- Mid game: 20,000-50,000 Materials/week
- Late game: 100,000-200,000+ Materials/week

---

### **Economic Balance Formula**

**Healthy Economy:**
```
Resource Faucets = Resource Sinks + 10-20% Buffer

Where:
- Faucets = Income from all sources
- Sinks = Expenses for progression
- Buffer = 10-20% surplus (player savings, hoarding)
```

**Example (Casual Player, Mid-Game):**
- Gold Income: 175,000/week
- Gold Spending: 150,000/week
- Buffer: 25,000/week (14% surplus) ✅ Healthy

**If Buffer Too High (>30%):**
- Resources too abundant (no scarcity)
- Progression too easy (no challenge)
- Fix: Increase sink costs OR decrease faucet rates

**If Buffer Too Low (<5%):**
- Resources too scarce (frustration)
- Progression blocked (pay-to-progress temptation)
- Fix: Decrease sink costs OR increase faucet rates

---

### **Inflation Prevention**

**Causes of Inflation:**
- Faucets > Sinks (too much income)
- Permanent resource accumulation (veterans hoard)
- No high-level sinks (endgame players stockpile)

**Prevention Strategies:**

**1. Exponential Upgrade Costs:**
- Level 1→2: 2,000 Gold
- Level 9→10: 200,000 Gold
- Veterans spend massively on final upgrades

**2. Endgame Sinks:**
- Laboratory research (300,000+ Gold per project)
- Automation Station (100,000+ Gold)
- Level 10 upgrades (1,000,000+ Gold cumulative)

**3. Prestige Systems (Future):**
- Reset progress for permanent bonuses
- Spend accumulated resources on prestige
- Creates infinite sink

**4. Seasonal Content:**
- New cosmetics (gold + premium currency)
- Event shops (gold for limited items)
- Guild competitions (gold entry fees)

---

### **Player Economy Progression Curve**

**Weeks 1-4 (Levels 1-20):**
- Net worth: 10,000-50,000 Gold + 2,000-10,000 Materials
- Status: Resource-poor (always spending everything)
- Feeling: Progression rapid, resources scarce

**Months 2-3 (Levels 21-40):**
- Net worth: 100,000-300,000 Gold + 20,000-50,000 Materials
- Status: Resource-stable (income meets expenses)
- Feeling: Comfortable progression, strategic choices

**Months 4-6 (Levels 41-60):**
- Net worth: 500,000-1,500,000 Gold + 100,000-200,000 Materials
- Status: Resource-comfortable (can save surplus)
- Feeling: Planning big upgrades, optimization phase

**Months 7+ (Levels 61+):**
- Net worth: 2,000,000-10,000,000+ Gold + 500,000+ Materials
- Status: Resource-wealthy (endgame sinks required)
- Feeling: Maxing everything, collecting cosmetics

**This curve ensures:**
- Early game: Struggle (engagement through challenge)
- Mid game: Balance (strategic resource management)
- Late game: Abundance (reward for commitment)

---

## 📊 PLAYER PROGRESSION CURVES - RETENTION DESIGN

### **Core Retention Philosophy**

**Retention Requires:**
1. **Early Hook:** First 15 minutes are exciting
2. **Daily Habit:** Reason to log in every day
3. **Weekly Milestones:** Tangible progress each week
4. **Monthly Goals:** Long-term aspirations
5. **Social Bonds:** Friends keep you playing

---

### **Retention Metrics (Target KPIs)**

**Day 1 Retention: 40-50%**
- Players who return after first session
- Driven by: Tutorial quality, early rewards, hook moments

**Day 7 Retention: 20-30%**
- Players who play for a full week
- Driven by: Daily quests, first major upgrades, social features

**Day 30 Retention: 10-15%**
- Players who become regular users
- Driven by: Guild integration, endgame content preview, progression satisfaction

**Day 90 Retention: 5-8%**
- Core player base (long-term retention)
- Driven by: Social bonds, mastery goals, prestige systems

---

### **Progression Pacing (Detailed Timeline)**

#### **Week 1: Tutorial & Hook (Levels 1-10)**

**Day 1 (First Session - 30-60 minutes):**
- Complete tutorial expedition
- Build first buildings (Expedition Hub, Warehouse, Mailbox)
- Unlock Weaponsmith (Level 5)
- Craft first weapon
- Capture first 5 pets
- Complete first daily quest
- **Key Feeling:** "This is fun! I want to play more."

**Days 2-3:**
- Unlock Training Station (Level 12)
- Train first pet to Level 10
- Craft first armor piece
- Upgrade Weaponsmith to Level 2
- Join first Co-op expedition
- **Key Feeling:** "I'm making progress every session."

**Days 4-7:**
- Unlock Workshop (Level 15)
- Craft first consumables
- Upgrade 3 buildings to Level 3
- Reach Account Level 20
- Unlock Breeding Station
- **Key Feeling:** "So much to do! I'm hooked."

**Week 1 Retention Drivers:**
- New unlocks every session (constant novelty)
- Rapid leveling (1-20 levels in a week)
- Clear progression path (guided)
- Social integration (Co-op unlocked Day 2)

---

#### **Weeks 2-4: Establishing Habits (Levels 11-30)**

**Week 2:**
- Unlock Refinery (Level 25)
- Start refining materials (economic strategy)
- Upgrade 5 buildings to Level 5
- Join or create guild
- Capture 50 unique species
- **Key Feeling:** "I'm getting good at this."

**Week 3:**
- Unlock Sanctuary (Level 30)
- Display favorite pets
- Start Laboratory research (Level 35)
- Unlock Market (Level 40) - early access via quest
- First legendary item crafted
- **Key Feeling:** "I'm becoming powerful."

**Week 4:**
- Unlock Trophy Hall (Level 45)
- Earn first Gold achievement
- Upgrade 3 buildings to Level 7
- Participate in first guild dungeon
- Reach Account Level 50
- **Key Feeling:** "I'm committed to this game."

**Month 1 Retention Drivers:**
- Daily quests (habit formation)
- Guild integration (social bonds)
- First legendary items (power spike)
- Mid-game unlocks (content depth)

---

#### **Months 2-3: Deepening Engagement (Levels 31-60)**

**Month 2:**
- Unlock Pet Daycare (Level 50)
- Unlock Cosmetic Hub (Level 55)
- Start customizing base appearance
- Upgrade 10 buildings to Level 5
- Complete 50+ expeditions
- **Key Feeling:** "This is MY game now."

**Month 3:**
- Unlock Energy Generator (Level 60)
- Unlock Guild Hall (Level 65)
- Participate in guild wars
- Upgrade 5 buildings to Level 10
- Capture 100 unique species
- **Key Feeling:** "I'm a veteran player."

**Months 2-3 Retention Drivers:**
- Personalization (base customization)
- Social prestige (guild leadership, high-level player)
- Endgame content preview (guild wars)
- Long-term goals (Level 10 upgrades)

---

#### **Months 4-6: Endgame Mastery (Levels 61-80)**

**Month 4:**
- Unlock Automation Station (Level 70)
- Quality-of-life improvements (mass training)
- Upgrade 10 buildings to Level 10
- Complete 50% of Laboratory research
- **Key Feeling:** "I'm optimizing everything."

**Month 5:**
- Reach Account Level 80
- Unlock all buildings (20/20)
- Upgrade 15 buildings to Level 10
- Complete 75% of achievements
- **Key Feeling:** "I'm nearly maxed out."

**Month 6:**
- Upgrade all 20 buildings to Level 10
- Complete all Laboratory research
- Capture all 200+ species
- Reach top 1% leaderboard
- **Key Feeling:** "I've mastered this game."

**Months 4-6 Retention Drivers:**
- Mastery goals (100% completion)
- Competitive rankings (leaderboards)
- Social prestige (veteran status)
- Collecting cosmetics (ongoing goal)

---

#### **Month 7+: Retention Endgame**

**Retention Strategies for Veterans:**

**1. Seasonal Content:**
- New events every month (fresh content)
- Seasonal battle pass (3-4 per year)
- Limited-time cosmetics (FOMO)

**2. Competitive Content:**
- Guild wars (weekly)
- Speed run challenges (weekly)
- Pet battle tournaments (monthly)

**3. Social Leadership:**
- Guild leadership roles (responsibility)
- Mentoring new players (community)
- Content creation (screenshots, guides)

**4. Collection Completion:**
- Cosmetics (200+ items)
- Achievements (100+ achievements)
- Perfect IV pets (aspirational)

**5. Prestige Systems (Future):**
- Reset for permanent bonuses
- Prestige-exclusive content
- Infinite progression

---

### **Session Length Optimization**

**Target Session Lengths:**

**New Players (Week 1):**
- Session length: 30-60 minutes
- Frequency: 2-3 sessions per day
- Content: High novelty, rapid progression

**Established Players (Months 2-6):**
- Session length: 60-120 minutes
- Frequency: 1-2 sessions per day
- Content: Strategic optimization, social play

**Veterans (Month 7+):**
- Session length: 30-90 minutes
- Frequency: 1 session per day
- Content: Daily quests, guild events, competitive

**Casual Players (All Stages):**
- Session length: 15-30 minutes
- Frequency: 1 session per day
- Content: Daily quests, passive collection, social

---

## 🛡️ ANTI-EXPLOIT MEASURES - SECURITY

### **Core Security Philosophy**

**Security Requires:**
1. **Prevention:** Make exploits difficult
2. **Detection:** Identify exploits quickly
3. **Response:** Ban exploiters, fix vulnerabilities
4. **Recovery:** Rollback economy damage

---

### **Critical Exploit Vectors**

#### **1. Duplication Exploits (Item/Resource Duping)**

**Prevention:**
- **Server-side validation:** All item creation server-authoritative
- **Unique IDs:** Every item has unique ID (duplicates impossible)
- **Transaction logs:** All item movements logged (audit trail)
- **Checksums:** Inventory checksums validated on login

**Detection:**
- **Duplicate ID alerts:** Automatic flagging of impossible duplicates
- **Suspicious patterns:** 1,000 legendary pets in 1 hour = flag
- **Inventory snapshots:** Compare login/logout inventory

**Response:**
- **Immediate ban:** Zero tolerance (permanent ban)
- **Rollback:** Remove all duped items from economy
- **Economy adjustment:** If widespread, adjust prices

---

#### **2. Currency Exploits (Gold/Premium Currency)**

**Prevention:**
- **Server-side economy:** All transactions validated server-side
- **Rate limits:** Cannot earn 1,000,000 Gold in 1 second
- **Transaction verification:** Gold sources must be legitimate
- **Purchase validation:** Premium currency purchases verified with payment processor

**Detection:**
- **Anomaly detection:** Sudden 10,000,000 Gold = flag
- **Source tracking:** Where did gold come from? (expedition, market, exploit?)
- **Premium currency audits:** Match purchases to payment records

**Response:**
- **Account freeze:** Investigate before banning
- **Refund policy:** If exploit, remove fraudulent currency
- **Permanent ban:** If intentional exploitation

---

#### **3. Market Manipulation (Price Fixing, Cornering)**

**Prevention:**
- **Listing limits:** Max 50 active listings per player
- **Purchase limits:** Max 100 of same item per day
- **Bid collusion detection:** Flag repeated shill bidding
- **Market analytics:** Track price anomalies

**Detection:**
- **Price spikes:** Sudden 1,000% price increase on common item
- **Volume anomalies:** One player buys 100% of supply
- **Coordinated behavior:** Multiple accounts working together

**Response:**
- **Market suspension:** Temporarily disable problematic listings
- **Account suspension:** Ban coordinating accounts
- **Price rollback:** Reset manipulated items to fair price

---

#### **4. Botting & Automation (Third-Party Scripts)**

**Prevention:**
- **Captchas:** Occasional human verification during gameplay
- **Input patterns:** Detect inhuman click patterns (1,000 clicks/second)
- **Session monitoring:** Flag 24-hour continuous play
- **Client validation:** Detect modified game clients

**Detection:**
- **Behavioral analysis:** Perfect timing, repetitive patterns
- **Impossible speeds:** Completing expedition in 10 seconds
- **Third-party software detection:** Scan for known botting tools

**Response:**
- **Soft ban:** Temporary suspension (investigate)
- **Permanent ban:** If proven botting
- **Hardware ban:** Repeat offenders banned by device ID

---

#### **5. Account Sharing (Guild Boosting, Power Leveling)**

**Prevention:**
- **IP tracking:** Flag if account logs in from 10 countries in 1 day
- **Device fingerprinting:** Track device changes
- **Behavioral consistency:** Detect sudden playstyle changes

**Detection:**
- **Impossible geography:** Login in USA then China 1 hour later
- **Skill discrepancy:** Newbie player suddenly plays like pro
- **Suspicious trades:** Account transfers expensive items to new account

**Response:**
- **Account verification:** Require email/phone verification
- **Temporary lock:** Investigate suspicious logins
- **Rollback trades:** Reverse suspicious item transfers

---

### **Fair Play Enforcement**

**Ban Policy:**

**Temporary Bans (3-30 days):**
- First-time minor offense (unintentional exploit use)
- Suspicious but unproven behavior (investigation period)
- Warning for potential violations

**Permanent Bans:**
- Proven intentional exploitation (duping, botting)
- Repeated offenses (3+ temporary bans)
- RMT (Real Money Trading for in-game gold)
- Harassment, hate speech, or severe TOS violations

**Appeal Process:**
- Players can appeal bans (support ticket)
- Manual review by community team
- Evidence-based decisions (logs, screenshots)
- Transparent reasoning (why ban was applied)

---

## 💻 TECHNICAL IMPLEMENTATION GUIDELINES - DEVELOPMENT

### **Core Architecture Principles**

**System Requirements:**
1. **Scalability:** Support 100,000+ concurrent users
2. **Performance:** 60 FPS on mobile devices
3. **Security:** Server-authoritative design
4. **Reliability:** 99.9% uptime (3 nines)
5. **Maintainability:** Clean code, modular systems

---

### **Server-Client Architecture**

**Client Responsibilities (Local):**
- Rendering graphics (buildings, pets, decorations)
- Input handling (clicks, touches, keyboard)
- UI presentation (menus, dialogs, HUD)
- Audio playback (music, sound effects)
- Animation playback (pet movements, building construction)

**Server Responsibilities (Authoritative):**
- Player data storage (inventory, pets, progress)
- Economy validation (gold, materials, transactions)
- Building state management (upgrade timers, construction)
- Research progress (Laboratory timers)
- Breeding/Training calculations (pet progression)
- Market transactions (auction house, trades)
- Anti-cheat verification (input validation, rate limits)

**Why Server-Authoritative:**
- Prevents client-side exploits (memory hacking, modified APKs)
- Ensures fair play (all players experience same rules)
- Enables cross-platform play (mobile, PC, web)
- Allows rollback if exploits discovered

---

### **Database Schema (Simplified)**

**Core Tables:**

**players:**
- player_id (primary key)
- account_level
- gold_balance
- premium_currency
- created_at, last_login

**buildings:**
- building_id (primary key)
- player_id (foreign key)
- building_type (Weaponsmith, Armorsmith, etc.)
- level (1-10)
- plot_number (1-16)
- upgrade_timer (nullable, timestamp when upgrade completes)

**pets:**
- pet_id (primary key)
- player_id (foreign key)
- species
- rarity (Common, Legendary, etc.)
- star_rating (1-5)
- level (1-100)
- iv_hp, iv_attack, iv_defense, iv_speed, iv_sp_attack, iv_sp_defense
- friendship (0-100)

**inventory:**
- item_id (primary key)
- player_id (foreign key)
- item_type (weapon, armor, material, consumable)
- quantity (stackable items)

**market_listings:**
- listing_id (primary key)
- seller_id (foreign key)
- item_id (foreign key)
- starting_bid
- buyout_price (nullable)
- duration (timestamp when expires)
- current_bid, current_bidder_id

**guild:**
- guild_id (primary key)
- guild_name
- guild_level (1-10)
- guild_xp
- max_members

**guild_members:**
- guild_id, player_id (composite key)
- rank (Leader, Officer, Member, Recruit)
- contribution_xp

---

### **API Endpoints (RESTful)**

**Player Management:**
- `GET /player/{id}` - Get player data
- `POST /player/create` - Create new player
- `PUT /player/{id}/gold` - Update gold balance (server-only)

**Building Management:**
- `GET /player/{id}/buildings` - Get all buildings
- `POST /player/{id}/building/construct` - Start construction
- `POST /player/{id}/building/upgrade` - Start upgrade
- `POST /player/{id}/building/demolish` - Demolish building

**Pet Management:**
- `GET /player/{id}/pets` - Get all pets
- `POST /player/{id}/pet/train` - Start training
- `POST /player/{id}/pet/breed` - Start breeding
- `GET /player/{id}/pet/{pet_id}` - Get specific pet

**Market:**
- `GET /market/listings` - Browse market
- `POST /market/listing/create` - Create listing
- `POST /market/listing/bid` - Place bid
- `POST /market/listing/buyout` - Instant purchase

**Guild:**
- `GET /guild/{id}` - Get guild info
- `POST /guild/create` - Create guild
- `POST /guild/{id}/join` - Join guild
- `POST /guild/{id}/leave` - Leave guild

---

### **Performance Optimization**

**Mobile Optimization (Target: 60 FPS on mid-range devices):**

**Graphics:**
- LOD system (Level of Detail) - distant buildings use simplified models
- Occlusion culling - don't render buildings behind camera
- Texture compression - reduce memory usage
- Baked lighting - pre-calculate shadows (not real-time)

**Memory:**
- Asset streaming - load buildings/decorations on-demand
- Unload unused assets - remove from memory when not visible
- Texture atlases - combine multiple textures into one (reduce draw calls)

**Network:**
- Delta updates - only send changed data (not full state)
- Compression - gzip API responses
- Caching - cache static data locally (building descriptions)
- Batch requests - combine multiple API calls into one

**Loading Times:**
- Initial load: <10 seconds (first time)
- Return load: <3 seconds (cached assets)
- Building placement: Instant (no loading)
- Expedition deploy: <5 seconds (world generation)

---

## 🚀 FUTURE EXPANSION PLANS - ROADMAP

### **Year 1: Foundation & Core Loop**

**Q1 (Months 1-3):**
- Launch with 15 buildings (Phase 1-2)
- Core gameplay loop (expeditions, base building)
- Basic social features (friends, guilds)
- First seasonal event (Spring Bloom)

**Q2 (Months 4-6):**
- Add 3 buildings (Phase 3 partial)
- First major balance patch
- Guild wars feature
- Second seasonal event (Summer Festival)

**Q3 (Months 7-9):**
- Add 2 buildings (Phase 3 completion)
- First battle pass season
- Market analytics feature
- Third seasonal event (Halloween)

**Q4 (Months 10-12):**
- Add 2 buildings (Phase 4)
- Automation Station launch
- Prestige system (Tier 1)
- Fourth seasonal event (Winter Wonderland)

---

### **Year 2: Depth & Retention**

**Q1:**
- Mythic rarity tier (Tier 5 content)
- Advanced guild features (Guild Island expansions)
- New biome (Celestial Realm)
- Cosmetic Hub expansion (50+ new cosmetics)

**Q2:**
- Pet evolution system (pets evolve at max level)
- Advanced breeding (triple-element hybrids)
- New competitive mode (Ranked PvPvE)
- Second battle pass season

**Q3:**
- New building type (Alchemy Lab - transmutation)
- Advanced research tree (Tier 5 Laboratory)
- New biome (Abyssal Depths)
- Third battle pass season

**Q4:**
- Prestige system expansion (Tier 2-3)
- Cross-server guild wars
- New weapon types (Whips, Scythes)
- Fourth battle pass season

---

### **Year 3: Endgame & Innovation**

**Major Features:**
- Housing 2.0 (Indoor decorating, multi-floor bases)
- Pet raids (20-player cooperative boss fights)
- Seasonal ladders (competitive rankings)
- Player-created content (custom decorations, mod support)
- Esports integration (official tournaments)

---

## 📄 COMPLETE DOCUMENT SUMMARY - EXECUTIVE OVERVIEW

### **Project Scope: Idol Guardians: Eternal Wilds - Base Building System**

**Total Documentation:**
- **10 comprehensive parts** (95,000+ words)
- **20 buildings** detailed across 4 phases
- **100+ systems** fully designed
- **22-month development timeline**
- **$2-4 million budget** (estimated)

---

### **Core Design Pillars (Recap)**

1. **No Pay-to-Win:** 100% content accessible free
2. **Respectful Monetization:** Cosmetics + convenience only
3. **Long-Term Engagement:** Years of content, not months
4. **Social Integration:** Guilds, friends, community
5. **Player Agency:** Strategic choices, not forced paths
6. **Quality-of-Life:** Automation, fast travel, QoL features
7. **Accessibility:** Mobile-first, casual-friendly, no FOMO mechanics
8. **Progression Balance:** Early fast, mid strategic, late aspirational

---

### **Building Roster Summary (20 Buildings)**

**Phase 1 (MVP) - 8 Buildings:**
1. Expedition Hub - Deployment center
2. Warehouse - Storage management
3. Mailbox - Daily engagement hub
4. Weaponsmith - Offensive progression
5. Armorsmith - Defensive progression
6. Training Station - Pet leveling
7. Workshop - Consumable crafting
8. Breeding Station - Pet breeding & merging

**Phase 2 (Advanced) - 5 Buildings:**
9. Refinery - Material processing
10. Sanctuary - Collection showcase
11. Laboratory - Research tree
12. Market - Player economy
13. Trophy Hall - Achievement display

**Phase 3 (Endgame) - 5 Buildings:**
14. Pet Daycare - Living pet display
15. Cosmetic Hub - Personalization center
16. Energy Generator - Passive income
17. Guild Hall - Social hub
18. Automation Station - QoL endgame

**Phase 4 (Utility) - 2 Buildings:**
19. Fast Travel Hub - Teleportation
20. Event Billboard - Seasonal content

---

### **Key Systems Summary**

**Progression Systems:**
- Building upgrades (Level 1-10, exponential costs)
- Laboratory research (100+ projects, 1-30 day timers)
- Pet training (resource-based, 6-9 month real-time aging)
- Breeding (star merging, IV inheritance, elemental hybrids)

**Economic Systems:**
- Auction house (1-10% fees, buyout system, analytics)
- Direct trading (0% fees, friend/guild trades)
- Resource sinks (upgrades, crafting, training, breeding)
- Gold/material faucets (expeditions, quests, passive generation)

**Social Systems:**
- Guild system (100 members, levels 1-10, guild wars)
- Base visiting (read-only, kudos system, guided tours)
- Leaderboards (kudos, achievements, net worth)
- Screenshot sharing (4K, filters, direct social media)

**Customization Systems:**
- Plot customization (ground textures, borders, decorations, lighting)
- Base themes (15+ themes, 3 tiers, level-based)
- Character customization (100+ hairstyles, outfits, emotes)
- Pet skins (50+ skins, accessories, particles)

---

### **Monetization Summary (Ethical)**

**Revenue Streams:**
- Cosmetics (60%): $1-10 items, $10-25 bundles
- Convenience (30%): Time-savers, capacity increases, QoL
- Battle Pass (10%): $9.99/season, 50 tiers of rewards

**Expected ARPU:**
- Free players: $0 (80% of players)
- Minnows: $20/year (15% of players)
- Dolphins: $100/year (4% of players)
- Whales: $300/year (1% of players)
- **Total: $8-12 per player per year**

**What We Don't Sell:**
- ❌ Stat boosts, exclusive powerful items, loot boxes, energy systems, content locks, skip progression

---

### **Technical Requirements**

**Platform:** Roblox (mobile-first optimization)
**Performance:** 60 FPS on mid-range devices
**Architecture:** Server-authoritative (anti-cheat)
**Scalability:** 100,000+ concurrent users
**Uptime:** 99.9% (3 nines)

**Development Timeline:**
- Phase 1 (MVP): Months 1-6
- Phase 2 (Advanced): Months 7-12
- Phase 3 (Endgame): Months 13-18
- Phase 4 (Polish): Months 19-22
- **Total: 22 months**

---

### **Success Metrics (Target KPIs)**

**Retention:**
- Day 1: 40-50%
- Day 7: 20-30%
- Day 30: 10-15%
- Day 90: 5-8%

**Monetization:**
- Conversion rate: 15-20% (industry average: 2-5%)
- ARPU: $8-12/year
- LTV (Lifetime Value): $50-100 per player

**Engagement:**
- Daily active users: 20-30% of registered players
- Average session: 45-90 minutes
- Sessions per day: 1-2

**Revenue (Year 1):**
- 100,000 active players
- $800,000 - $1,200,000 total revenue
- Sustainable growth trajectory

---

## 🎉 FINAL THOUGHTS & CONCLUSION

### **What Makes This Design Special**

**1. Ethical Monetization:**
- Industry-leading ethical standards
- No pay-to-win (rare in free-to-play)
- Transparent pricing (no dark patterns)
- Respects player time and money

**2. Long-Term Vision:**
- 22-month development cycle (not rushed)
- Years of content planned (not months)
- Sustainable business model (not exploitative)
- Player-first design decisions

**3. Comprehensive Documentation:**
- 95,000+ words (publication-ready)
- Every system fully designed (no ambiguity)
- Balance tables and formulas (implementable)
- GitHub-ready markdown (version control)

**4. Mobile-First Design:**
- Touch-optimized UI (not PC port)
- Short session support (15-30 minutes viable)
- Offline progression (passive generation)
- Performance optimized (60 FPS target)

**5. Social Integration:**
- Guilds (100 members, cooperative content)
- Base visiting (social showcase)
- Screenshot sharing (organic marketing)
- Community-driven features (leaderboards, contests)

---

### **Development Priorities**

**Phase 1 (Months 1-6) - MVP:**
- Focus: Core loop (expeditions → base → progression)
- Buildings: 8 essential buildings
- Goal: Prove concept, establish retention

**Phase 2 (Months 7-12) - Depth:**
- Focus: Endgame content (Laboratory, Market, Trophy Hall)
- Buildings: 5 advanced buildings
- Goal: Long-term retention, monetization launch

**Phase 3 (Months 13-18) - Polish:**
- Focus: Quality-of-life (Automation, Daycare, Cosmetic Hub)
- Buildings: 5 endgame buildings
- Goal: Veteran player retention, prestige systems

**Phase 4 (Months 19-22) - Launch:**
- Focus: Final polish, balance tuning, marketing
- Buildings: 2 utility buildings
- Goal: Successful public launch, sustainable growth

---

### **Risk Mitigation**

**Technical Risks:**
- **Risk:** Performance issues on mobile
- **Mitigation:** Roblox platform (optimized), aggressive LOD system, mobile-first testing

**Economic Risks:**
- **Risk:** Inflation spiral (economy breaks)
- **Mitigation:** Exponential cost scaling, endgame gold sinks, monitoring tools

**Monetization Risks:**
- **Risk:** Low conversion (players don't spend)
- **Mitigation:** High-quality cosmetics, fair pricing, battle pass value

**Retention Risks:**
- **Risk:** Players quit after Month 1
- **Mitigation:** Guild integration (social bonds), daily quests (habits), long-term goals

**Competition Risks:**
- **Risk:** Similar games launch first
- **Mitigation:** Unique combination (extraction + pets + base building), ethical monetization USP

---

### **Success Criteria (Launch +12 Months)**

**Baseline Success:**
- 50,000 active players
- $500,000 revenue
- Day 30 retention: 10%+
- Conversion rate: 10%+

**Target Success:**
- 100,000 active players
- $1,000,000 revenue
- Day 30 retention: 15%+
- Conversion rate: 15%+

**Exceptional Success:**
- 200,000+ active players
- $2,000,000+ revenue
- Day 30 retention: 20%+
- Conversion rate: 20%+

---

