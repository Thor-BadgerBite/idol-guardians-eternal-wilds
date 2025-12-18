# ETERNAL WILDS - WORLD & MAP SYSTEM DESIGN DOCUMENT

---

## 1. WORLD SYSTEM OVERVIEW

### 1.1 Core Concept
Eternal Wilds features a **procedurally generated world** that creates unique map layouts for each expedition while maintaining consistent gameplay balance and progression structure. The world uses **template-based biome placement** with randomized internal content, combining the replayability of procedural generation with the quality control of handcrafted design.

### 1.2 Key Design Pillars

**Exploration & Discovery**
- Each expedition presents a unique world layout via random seed generation
- Fog of war reveals territory as players explore, resetting each expedition
- Players cannot memorize optimal routes or resource locations
- Legendary pet spawns create dynamic hunt objectives across varying terrain

**Risk vs Reward Progression**
- Starter biomes near central base with safe, low-tier content
- Progressive difficulty radiating outward from spawn point
- Furthest biomes contain highest rewards with maximum danger
- Player choice drives how deep to venture before extracting

**Extraction Game Loop**
- 30-45 minute timed expeditions with closing extraction zones
- Permadeath for carried loot and loadout gear (except secure pet slots)
- Wildlife extinction mechanic creates organic time pressure
- Strategic decisions between safe early extraction vs risky deep runs

**Mobile-First Performance**
- Template-based generation ensures consistent performance
- Pre-optimized biome modules prevent runtime lag spikes
- Fixed map dimensions maintain predictable server load
- Fog of war reduces render distance requirements

### 1.3 World Dimensions & Scale

**Total Map Size**
- **10,000 x 10,000 studs** (Roblox units)
- Edge-to-edge travel time: ~10 minutes at sprint speed
- Base-to-edge travel time: ~5 minutes at sprint speed
- Actual travel time longer due to terrain obstacles, pet encounters, and stamina management

**Traversal Mechanics**
- Base movement speed: 16 studs/second (standard Roblox walk)
- Sprint speed: 24 studs/second (50% faster)
- Stamina system limits sustained sprinting (covered in Movement section)
- Natural barriers (rivers, mountains, cliffs) extend travel time

**Performance Optimization Zones**
- Map divided into 25 sectors (5x5 grid) for spatial partitioning
- Each sector: 2,000 x 2,000 studs
- Dynamic loading/unloading based on player proximity
- Prevents full map rendering on mobile devices

---

## 2. PROCEDURAL GENERATION SYSTEM

### 2.1 Seed-Based Generation

**Seed Structure**
```
Format: EW-[4-digit-number][1-letter]
Example: EW-2847A
Components:
- EW prefix (Eternal Wilds identifier)
- 4-digit number (1000-9999) for primary variation
- Single letter (A-Z) for micro-variation within number seed
Total possible seeds: 234,000 unique combinations
```

**Seed Display & Sharing**
- Seed code displayed in expedition lobby before deployment
- Visible on minimap UI during expedition
- Players can share seeds with community
- Future feature: Input custom seed for specific map recreation
- Creates social metagame: "EW-3921C has Volcanic Rift near base!"

**Seed Generation Algorithm**
```
Phase 1: Server generates random seed on expedition creation
Phase 2: Seed passed to world generation algorithm
Phase 3: Deterministic generation ensures consistency
Phase 4: All clients receive identical map from same seed
Phase 5: Seed logged for debugging and recreation purposes
```

### 2.2 Generation Phase Architecture

**Phase 1: Biome Placement (Large-Scale Structure)**

**Objective**: Position major biome zones according to difficulty progression rules while maintaining variety between seeds.

**Central Base Zone (Always Fixed)**
- Position: Exact center of 10,000 x 10,000 map (5000, 5000)
- Radius: 500 studs circular safe zone
- Contains: Base Hub structures, starting NPCs, crafting stations
- Never varies between seeds (orientation landmark)

**Starter Biome Ring (Guaranteed Safety)**
- Position: Circular ring around base hub
- Inner radius: 500 studs (edge of base)
- Outer radius: 1,500 studs
- Total area: ~7.07 million square studs
- Biome type: Whispering Forest (always starter biome)
- Purpose: Safe farming zone for new players, predictable early resources

**Mid-Tier Biome Placement (Randomized Positions)**
- Position: Between 1,500-4,500 stud radius from center
- Count: 3-4 biomes per seed (algorithm selects from pool)
- Available biome types:
  - Scorched Badlands (Fire/Rock pets)
  - Frozen Tundra (Ice/Wind pets)
  - Toxic Swamp (Poison/Water pets)
  - Crystal Caverns (Gem/Earth pets)
- Placement rules:
  - Minimum 1,000 studs separation between biome centers
  - No biome can fully surround another
  - Must have at least 2 access paths from starter ring
  - Cannot block direct routes to high-tier zones

**High-Tier Biome Placement (Edge Zones)**
- Position: Between 4,500-5,000 stud radius (map edges)
- Count: 2-3 biomes per seed
- Available biome types:
  - Volcanic Rift (Legendary Fire/Dragon pets)
  - Void Chasm (Legendary Dark/Psychic pets)
  - Storm Peaks (Legendary Electric/Flying pets)
  - Abyssal Depths (Legendary Water/Ghost pets)
- Placement rules:
  - Always at maximum distance from base
  - Minimum 2,000 studs separation from each other
  - Direction from base randomized (North/South/East/West/NE/NW/SE/SW)
  - One legendary biome always furthest point (5,000 studs from base)

**Biome Size Variation**
- Starter biome: Fixed size (1,000 stud radius ring)
- Mid-tier biomes: 800-1,200 stud radius (varies per seed)
- High-tier biomes: 600-1,000 stud radius (smaller, concentrated danger)
- Size inversely proportional to reward quality (smaller = denser loot)

**Phase 2: Transition Zone Generation**

**Objective**: Create natural blending between biomes to prevent jarring visual/gameplay boundaries.

**Gradient Transition System**
- Each biome has 200-stud transition border overlapping adjacent zones
- Terrain gradually morphs between biome types
- Example: Forest → Scorched transition
  - 0-50 studs: Full forest density, green vegetation
  - 50-100 studs: Thinning trees, browning grass, smoke particles
  - 100-150 studs: Sparse dead trees, cracked earth, ember particles
  - 150-200 studs: No trees, scorched ground, heat distortion
- Asset density tapers off naturally (no hard cut-offs)

**Natural Barriers**
- Rivers: 50-100 stud wide water barriers between some biomes
  - Crossable via bridges (random placement, 2-3 per river)
  - Swimming possible but slow (50% movement speed)
  - Adds 30-60 seconds to crossing time
- Mountain Ridges: Elevation barriers between difficulty tiers
  - Passable through mountain passes (1-2 per ridge)
  - Forces players into predictable paths (PvP choke points)
  - Climbing steep slopes: 25% movement speed penalty
- Cliffs: Vertical drops preventing direct access
  - Requires finding ramps or going around (adds 1-2 minutes)
  - Fall damage prevents jumping down (50% HP loss)
  - Creates one-way travel paths (retreat routes)

**Transition Zone Gameplay**
- Pet spawns in transitions: Mix of both adjacent biome types
  - 40% pets from biome A
  - 40% pets from biome B
  - 20% unique "hybrid" pets exclusive to that transition
- Chest spawns: Average rarity between both biomes
- Dungeons never spawn in transition zones (prevents confusion)

**Phase 3: Point of Interest (POI) Population**

**Objective**: Place interactive elements within biomes for exploration and resource gathering.

**Chest Spawn Algorithm**

**Common Chests (Abundant)**
- Count per biome: 15-25 (varies by biome size)
- Placement rules:
  - Minimum 100 studs from biome edge
  - Minimum 50 studs from other chests
  - Never inside dungeon radius (200 studs from entrance)
  - Avoid steep slopes or unreachable locations
- Visual identity: Wooden, weathered appearance
- Loot quality: Common/Uncommon materials (80/20 split)

**Uncommon Chests (Moderate)**
- Count per biome: 8-12
- Placement rules:
  - Minimum 200 studs from biome edge (deeper exploration)
  - Minimum 100 studs from other uncommon chests
  - 50% chance to be trapped (spawns guardian pet on open)
- Visual identity: Iron-banded, reinforced
- Loot quality: Uncommon/Rare materials (60/40 split)

**Rare Chests (Scarce)**
- Count per biome: 3-5
- Placement rules:
  - Only spawn in high-traffic paths or near landmarks
  - Minimum 300 studs from biome edge
  - 80% chance to be trapped
  - Never clustered with other rare chests (minimum 400 studs)
- Visual identity: Gold trim, glowing runes
- Loot quality: Rare/Epic materials (70/30 split)

**Legendary Chests (Extremely Rare)**
- Count per biome: 0-1 (high-tier biomes only)
- Placement rules:
  - Always trapped (guaranteed boss-tier guardian)
  - Requires solving environmental puzzle to access
  - Located at furthest point within biome from all entrances
- Visual identity: Ornate, magical aura, particle effects
- Loot quality: Epic/Legendary materials (50/50 split) + guaranteed blueprint

**Trapped Chest Mechanics**
- When opened, spawns guardian pet 10 studs from chest
- Guardian difficulty scales to chest rarity:
  - Common trapped: Basic-tier pet (1 star)
  - Uncommon trapped: Elite-tier pet (2 star)
  - Rare trapped: Boss-tier pet (3 star)
  - Legendary trapped: Mini-boss pet (4 star)
- Guardian must be defeated before chest loot can be collected
- Guardian drops additional materials on defeat (bonus reward)
- 10-second animation before guardian spawns (player can run, but loses chest)

**Dungeon Entrance Placement**

**Dungeon Count per Biome**
- Starter biome: 2 dungeons (low difficulty)
- Mid-tier biomes: 2-3 dungeons (medium difficulty)
- High-tier biomes: 1-2 dungeons (high difficulty, better rewards)

**Placement Rules**
- Minimum 800 studs from biome edge (requires commitment to reach)
- Minimum 500 studs from other dungeon entrances
- Never placed in transition zones or near natural barriers
- Positioned away from direct paths (encourages exploration)
- Always in relatively flat terrain (no cliff-edge dungeons)

**Dungeon Entrance Types per Biome**
- Forest: Cave entrance (stone archway, moss-covered)
- Scorched: Lava tube entrance (glowing fissure, heat waves)
- Frozen: Ice cavern (crystalline opening, frost particles)
- Toxic: Sinkhole entrance (murky water, poison fog)
- Volcanic: Magma chamber (obsidian gates, fire effects)
- Void: Reality tear (distorted space, dark energy)

**Landmark Structures (Navigation Aids)**

**Purpose**: Help players orient themselves without relying on minimap, especially important on mobile.

**Landmark Types per Biome**
- Forest: Ancient tree (300 studs tall, visible from distance)
- Scorched: Rock spire (towering sandstone formation)
- Frozen: Ice pillar (crystalline obelisk, glowing blue)
- Toxic: Dead titan (massive skeletal remains)
- Volcanic: Lava geyser (erupts periodically, visible plume)
- Void: Floating ruins (anti-gravity stone fragments)

**Landmark Placement**
- 1-2 landmarks per biome (larger biomes get 2)
- Always near biome center for maximum visibility
- Minimum 400 studs from dungeons (prevents confusion)
- Visible from biome edges (line-of-sight checks)

**Gameplay Function**
- Players can use landmarks for callouts ("Meet at the Ancient Tree")
- Landmarks appear on minimap once discovered
- No gameplay bonuses (purely navigational)

---

## 3. BIOME SYSTEM ARCHITECTURE

### 3.1 Biome Definition Framework

Each biome is a **self-contained module** with the following components:

**Terrain Template**
- Heightmap data (elevation profile)
- Ground texture sets (4-6 textures for variation)
- Vegetation density maps
- Ambient particle systems
- Lighting configuration (color, intensity, fog density)

**Asset Pools**
- Trees/plants (10-15 unique models)
- Rocks/debris (8-12 models)
- Environmental props (6-10 interactive objects)
- All assets pre-optimized for mobile (LOD models included)

**Spawn Data**
- Pet spawn points (density map)
- Chest spawn zones (probability map)
- Dungeon entrance locations (fixed positions within template)
- Landmark positions (fixed)

**Audio Configuration**
- Ambient soundscape (looping background)
- Environmental sounds (wind, water, etc.)
- Music track (biome-specific theme)

### 3.2 Starter Biome: Whispering Forest

**Theme**: Lush temperate forest, safe haven, tutorial zone

**Visual Identity**
- Terrain: Rolling hills, gentle slopes (max 30° incline)
- Ground: Grass, dirt paths, moss-covered rocks
- Vegetation: Dense deciduous trees (oak, birch), ferns, flowers
- Lighting: Soft green-tinted, dappled sunlight through canopy
- Weather: Clear with occasional light rain
- Particles: Fireflies (night), falling leaves, pollen

**Gameplay Characteristics**
- Difficulty: Very Low (starter zone)
- Pet level range: 1-10
- Pet rarities: Common (70%), Uncommon (25%), Rare (5%)
- Pet types: Nature, Normal, Bug, Flying (basic elements)
- Resource quality: Common materials (90%), Uncommon (10%)

**Unique Features**
- Tutorial NPCs scattered throughout (explain mechanics)
- Higher chest density than other biomes (learning opportunity)
- No trapped chests in outer ring (100 studs from base)
- Pet aggro range reduced by 50% (safer exploration)

**Dungeon Type**: Mossy Cavern
- Rooms: 5-7 connected chambers
- Enemies: Low-level Nature/Bug pets
- Boss: Ancient Tree Spirit (Level 10, 2-star)
- Loot: Uncommon materials, basic blueprints

### 3.3 Mid-Tier Biome: Scorched Badlands

**Theme**: Desert wasteland, oppressive heat, rugged survival

**Visual Identity**
- Terrain: Flat expanses with jagged rock formations, canyons
- Ground: Cracked earth, sand dunes, volcanic rock
- Vegetation: Sparse cacti, dead bushes, tumbleweeds
- Lighting: Harsh orange/yellow, heat distortion effect
- Weather: Clear (daytime), dust storms (periodic)
- Particles: Embers, dust devils, heat waves

**Gameplay Characteristics**
- Difficulty: Medium
- Pet level range: 15-30
- Pet rarities: Common (40%), Uncommon (35%), Rare (20%), Epic (5%)
- Pet types: Fire, Rock, Ground
- Resource quality: Uncommon (60%), Rare (35%), Epic (5%)

**Environmental Hazards**
- Heat zones: Standing still causes 1% HP drain per second (forces movement)
- Sandstorms: Periodic visibility reduction to 50 studs, lasts 90 seconds
- Quicksand patches: Reduces movement speed by 75%, drains stamina faster

**Dungeon Type**: Lava Tubes
- Rooms: 8-10 winding tunnels with lava rivers
- Enemies: Mid-level Fire/Rock pets
- Boss: Magma Drake (Level 25, 3-star)
- Loot: Rare materials, fire-element blueprints

---

## 3. BIOME SYSTEM ARCHITECTURE (CONTINUED)

### 3.4 Mid-Tier Biome: Frozen Tundra

**Theme**: Arctic wasteland, bitter cold, crystalline beauty

**Visual Identity**
- Terrain: Flat snowfields interrupted by ice formations, frozen lakes
- Ground: Deep snow (footprint trails), ice sheets, permafrost
- Vegetation: Dead trees encased in ice, frozen shrubs, ice crystals
- Lighting: Cool blue-white, aurora borealis effects (night)
- Weather: Blizzards (periodic), light snowfall (constant)
- Particles: Snowflakes, ice shards, frozen mist, aurora streaks

**Gameplay Characteristics**
- Difficulty: Medium
- Pet level range: 15-30
- Pet rarities: Common (35%), Uncommon (40%), Rare (20%), Epic (5%)
- Pet types: Ice, Wind, Water
- Resource quality: Uncommon (55%), Rare (40%), Epic (5%)

**Environmental Hazards**
- Frostbite zones: Standing still causes 1.5% HP drain per second
- Slippery ice: Movement becomes sliding-based (reduced control, 30% faster speed)
- Frozen lakes: Thin ice cracks under prolonged standing (3 seconds), plunges into water
  - Water slows movement to 30% and drains stamina 3x faster
  - Must reach shore within 15 seconds or HP drain begins (5% per second)
- Blizzards: Periodic whiteout conditions, visibility reduced to 30 studs, lasts 2 minutes

**Unique Mechanics**
- Ice walls: Can be broken with Fire-type pet attacks (creates shortcuts)
- Frozen chests: Require fire damage to thaw before opening (adds tactical layer)
- Snowdrifts: Hiding spots that break line-of-sight for stealth

**Dungeon Type**: Glacial Cavern
- Rooms: 7-9 ice-carved chambers with frozen waterfalls
- Environmental puzzle: Light refraction through ice crystals to unlock doors
- Enemies: Mid-level Ice/Wind pets
- Boss: Frost Wyrm (Level 28, 3-star)
- Loot: Rare ice materials, cold-resistance blueprints

### 3.5 Mid-Tier Biome: Toxic Swamp

**Theme**: Murky wetland, disease-ridden, treacherous ground

**Visual Identity**
- Terrain: Shallow water pools, mud flats, twisted root systems
- Ground: Murky water (semi-transparent), sludge, rotting vegetation
- Vegetation: Gnarled trees with hanging moss, giant mushrooms, toxic flowers
- Lighting: Sickly green tint, bioluminescent fungi glow (night)
- Weather: Heavy fog (constant), acid rain (periodic)
- Particles: Toxic gas clouds, spores, bubbling sludge, glowing insects

**Gameplay Characteristics**
- Difficulty: Medium-High
- Pet level range: 20-35
- Pet rarities: Common (30%), Uncommon (35%), Rare (25%), Epic (10%)
- Pet types: Poison, Water, Bug, Dark
- Resource quality: Uncommon (45%), Rare (45%), Epic (10%)

**Environmental Hazards**
- Poison pools: Walking through deals 2% HP per second, stacks with DoT effect
  - DoT: 0.5% HP per second for 10 seconds after leaving pool
- Quickmud: Reduces movement speed by 80%, escape requires stamina sprint
- Toxic gas vents: Erupts every 30 seconds, 50-stud radius, 3% HP per tick (5 ticks)
- Acid rain: Periodic weather, open-area exposure deals 1% HP per 2 seconds

**Unique Mechanics**
- Safe islands: Elevated wooden platforms above water (rest spots, no hazards)
- Vine bridges: Unstable crossings that break after 5 seconds of standing
- Mushroom bounces: Giant mushrooms launch players upward for shortcut access

**Dungeon Type**: Fungal Grotto
- Rooms: 6-8 organic caverns with pulsating walls
- Environmental hazard: Spore clouds reduce visibility and drain stamina
- Enemies: Mid-high level Poison/Bug pets
- Boss: Plague Spore Lord (Level 32, 3-star)
- Loot: Rare poison materials, antidote blueprints, mutation components

### 3.6 Mid-Tier Biome: Crystal Caverns

**Theme**: Underground geode network, magical luminescence, mineral wealth

**Visual Identity**
- Terrain: Subterranean caves with massive crystal formations
- Ground: Smooth stone, crystal clusters, glowing mineral veins
- Vegetation: Minimal - bioluminescent moss, crystal flowers
- Lighting: Multi-colored crystal glow (purple, blue, green), no natural light
- Weather: None (underground), occasional crystal rain (shard particles)
- Particles: Floating crystal dust, magical sparkles, light beams

**Gameplay Characteristics**
- Difficulty: Medium-High
- Pet level range: 20-35
- Pet rarities: Common (25%), Uncommon (35%), Rare (30%), Epic (10%)
- Pet types: Rock, Gem, Psychic, Fairy
- Resource quality: Uncommon (40%), Rare (50%), Epic (10%)

**Environmental Hazards**
- Crystal resonance: Large crystals emit shockwaves periodically (knockback + 2% HP)
- Narrow passages: Tight corridors between crystal walls (no room to dodge)
- Falling crystals: Stalactites drop randomly (3-second warning glow, 10% HP damage)
- Light dependency: Darkness zones require light source (carried torch item or pet ability)

**Unique Mechanics**
- Mining nodes: Rare crystal deposits can be harvested (one-time use per expedition)
- Light puzzles: Reflect crystal beams to unlock sealed areas
- Teleport crystals: Step on glowing platform to warp to paired crystal (random locations)

**Dungeon Type**: Geode Chamber
- Rooms: 5-7 crystalline halls with reflective surfaces
- Environmental puzzle: Activate crystal sequence to progress
- Enemies: Mid-high level Rock/Gem/Psychic pets
- Boss: Gemstone Colossus (Level 30, 3-star)
- Loot: Rare gem materials, crystal weapon blueprints, enchantment components

---

## 3.7 High-Tier Biomes (Legendary Zones)

### 3.7.1 High-Tier Biome: Volcanic Rift

**Theme**: Active volcano interior, extreme heat, dragon domain

**Visual Identity**
- Terrain: Obsidian cliffs, lava rivers, floating platforms above magma
- Ground: Blackened rock, glowing fissures, solidified lava flows
- Vegetation: None - ash-covered dead trees, fire-resistant fungi
- Lighting: Intense red-orange glow, lava illumination, smoke obscures sky
- Weather: Ash fall (constant), lava eruptions (periodic)
- Particles: Embers, ash clouds, lava splashes, fire tornadoes

**Gameplay Characteristics**
- Difficulty: Very High
- Pet level range: 40-60
- Pet rarities: Rare (30%), Epic (40%), Legendary (25%), Mythic (5%)
- Pet types: Fire, Dragon, Rock (legendary variants)
- Resource quality: Rare (30%), Epic (50%), Legendary (20%)

**Environmental Hazards**
- Lava rivers: Instant death on contact (no swimming)
- Pyroclastic clouds: Fast-moving gas walls that insta-kill (20-second warning rumble)
- Eruption zones: Ground glows red 5 seconds before lava geyser (15% HP damage)
- Ambient heat: Constant 2% HP drain per second in open areas (must use cover)

**Cover System**
- Obsidian rocks: Reduce heat damage by 75% when behind them
- Caves: Complete heat protection, but contain ambush pets
- Time limit in open: 50 seconds before heat overwhelms (forces movement strategy)

**Unique Mechanics**
- Lava platforms: Obsidian chunks float on lava, used as stepping stones (sink after 3 seconds)
- Dragon nests: High-value loot but guaranteed 4-star guardian pet
- Forging stations: Use volcanic heat to craft fire-element gear (unique to this biome)

**Dungeon Type**: Magma Core
- Rooms: 4-6 chambers deep inside volcano
- Environmental hazard: Rising lava floods room every 2 minutes (must reach high ground)
- Enemies: High-level Fire/Dragon pets (3-4 star minimum)
- Boss: Inferno Dragon King (Level 55, 5-star, Legendary)
- Loot: Epic/Legendary fire materials, dragon scales, ultimate fire blueprints

### 3.7.2 High-Tier Biome: Void Chasm

**Theme**: Reality-torn dimension, cosmic horror, psychic nightmares

**Visual Identity**
- Terrain: Floating islands in endless void, gravity-defying architecture
- Ground: Obsidian platforms, reality fragments, distorted surfaces
- Vegetation: Impossible geometry plants, eyes that follow players, tentacle growths
- Lighting: No natural light - purple/black void, glowing runes, star-field backdrop
- Weather: Reality storms (space-time distortions)
- Particles: Void energy, floating debris, cosmic dust, reality cracks

**Gameplay Characteristics**
- Difficulty: Very High
- Pet level range: 40-60
- Pet rarities: Rare (25%), Epic (40%), Legendary (30%), Mythic (5%)
- Pet types: Dark, Psychic, Ghost, Void (exclusive type)
- Resource quality: Rare (25%), Epic (50%), Legendary (25%)

**Environmental Hazards**
- Void falls: Falling off platforms = instant death (no respawn)
- Gravity shifts: Periodic direction changes (up becomes down, disorienting)
- Madness zones: Proximity causes screen distortion, inverted controls (temporary)
- Reality tears: Teleport players randomly within biome (5% chance per 30 seconds)

**Sanity Mechanic (Unique to Void Chasm)**
- Sanity bar: Drains slowly while in biome (1% per 10 seconds)
- Low sanity effects:
  - 50% sanity: Hallucination pets appear (fake, waste time)
  - 25% sanity: Audio distortions, fake player callouts
  - 0% sanity: Screen goes dark, controls reversed, constant HP drain
- Restore sanity: Defeat pets (+5%), consume sanity potions (+25%), leave biome (full restore)

**Unique Mechanics**
- Phase platforms: Toggle between visible/invisible with switches
- Mirror realms: Step through portals to inverted dimension (different loot/enemies)
- Cosmic altars: Sacrifice materials for guaranteed legendary pet spawn (risky choice)

**Dungeon Type**: Abyssal Rift
- Rooms: 3-5 non-euclidean chambers (rooms connect impossibly)
- Environmental puzzle: Navigate paradox geometry to reach center
- Enemies: High-level Dark/Psychic/Ghost pets (3-4 star minimum)
- Boss: Void Leviathan (Level 58, 5-star, Legendary)
- Loot: Epic/Legendary void materials, reality shards, cosmic blueprints

### 3.7.3 High-Tier Biome: Storm Peaks

**Theme**: Floating sky islands, perpetual thunderstorm, wind-swept heights

**Visual Identity**
- Terrain: Floating rock islands connected by rope bridges and wind currents
- Ground: Stone platforms, cloud surfaces (semi-solid), ancient ruins
- Vegetation: Wind-bent trees, sky flowers, lightning-struck remnants
- Lighting: Dark storm clouds, constant lightning flashes, blue-white illumination
- Weather: Perpetual thunderstorm, torrential rain, hurricane winds
- Particles: Rain sheets, lightning bolts, swirling clouds, electric arcs

**Gameplay Characteristics**
- Difficulty: Very High
- Pet level range: 40-60
- Pet rarities: Rare (28%), Epic (40%), Legendary (27%), Mythic (5%)
- Pet types: Electric, Flying, Wind, Storm (exclusive type)
- Resource quality: Rare (28%), Epic (50%), Legendary (22%)

**Environmental Hazards**
- Lightning strikes: Random 100-stud radius bolts (5-second warning glow on ground, 20% HP)
- Hurricane winds: Push players toward edges (must lean into wind to walk straight)
- Updrafts: Launch players upward uncontrollably (can overshoot platforms)
- Rain slickness: Reduces traction, easier to slide off edges

**Unique Mechanics**
- Wind currents: Glide between islands using special glider item (required for exploration)
- Lightning rods: Attract strikes away from players (craftable, single-use)
- Storm vortexes: Teleport to random island when entered (risk/reward shortcut)

**Dungeon Type**: Thunderspire Temple
- Rooms: 5-7 sky temple chambers with exposed platforms
- Environmental hazard: Chain lightning jumps between players and enemies
- Enemies: High-level Electric/Flying pets (3-4 star minimum)
- Boss: Thunder God Phoenix (Level 60, 5-star, Legendary)
- Loot: Epic/Legendary storm materials, wing fragments, lightning weapon blueprints

### 3.7.4 High-Tier Biome: Abyssal Depths

**Theme**: Deep ocean trench, crushing pressure, bioluminescent horrors

**Visual Identity**
- Terrain: Underwater caves, coral formations, sunken ruins
- Ground: Sandy seabed, kelp forests, rocky outcrops
- Vegetation: Giant kelp, glowing anemones, coral trees, deep-sea plants
- Lighting: Minimal natural light, bioluminescence (blue/green), darkness at depth
- Weather: Underwater currents (visual flow), pressure zones
- Particles: Bubbles, floating plankton, light rays from surface (shallow), darkness (deep)

**Gameplay Characteristics**
- Difficulty: Very High
- Pet level range: 40-60
- Pet rarities: Rare (26%), Epic (40%), Legendary (29%), Mythic (5%)
- Pet types: Water, Ice, Ghost, Abyss (exclusive type)
- Resource quality: Rare (26%), Epic (52%), Legendary (22%)

**Environmental Hazards**
- Pressure zones: Deep areas deal increasing HP damage (5% per second at maximum depth)
- Oxygen system: Limited air supply, must return to air pockets every 60 seconds
- Strong currents: Push players in specific directions (must swim against to progress)
- Darkness: Light sources required at depth (visibility reduced to 20 studs)

**Oxygen Mechanic (Unique to Abyssal Depths)**
- Oxygen bar: 60 seconds of air
- Air pockets: Found in caves, bubbles from vents (instant refill)
- Oxygen tanks: Craftable item (+30 seconds air, consumable)
- Low oxygen warning: 15 seconds remaining triggers screen vignette + warning sound
- Zero oxygen: 5% HP drain per second until air found or death

**Unique Mechanics**
- Underwater caves: Safe zones with air, but contain ambush predators
- Bioluminescent trails: Follow glowing fish to hidden loot
- Pressure suits: Craftable gear reduces pressure damage by 50%

**Dungeon Type**: Sunken Citadel
- Rooms: 6-8 flooded chambers with air-locked sections
- Environmental puzzle: Activate pressure valves to drain rooms
- Enemies: High-level Water/Ghost/Abyss pets (3-4 star minimum)
- Boss: Leviathan of the Deep (Level 57, 5-star, Legendary)
- Loot: Epic/Legendary abyssal materials, pressure-proof blueprints, legendary water pets

---

## 3.8 Biome Comparison Table

| Biome | Difficulty | Pet Level | Common% | Uncommon% | Rare% | Epic% | Legendary% | Mythic% | Resource Quality |
|-------|------------|-----------|---------|-----------|-------|-------|------------|---------|------------------|
| Whispering Forest | Very Low | 1-10 | 70% | 25% | 5% | 0% | 0% | 0% | Common 90%, Uncommon 10% |
| Scorched Badlands | Medium | 15-30 | 40% | 35% | 20% | 5% | 0% | 0% | Uncommon 60%, Rare 35%, Epic 5% |
| Frozen Tundra | Medium | 15-30 | 35% | 40% | 20% | 5% | 0% | 0% | Uncommon 55%, Rare 40%, Epic 5% |
| Toxic Swamp | Medium-High | 20-35 | 30% | 35% | 25% | 10% | 0% | 0% | Uncommon 45%, Rare 45%, Epic 10% |
| Crystal Caverns | Medium-High | 20-35 | 25% | 35% | 30% | 10% | 0% | 0% | Uncommon 40%, Rare 50%, Epic 10% |
| Volcanic Rift | Very High | 40-60 | 0% | 0% | 30% | 40% | 25% | 5% | Rare 30%, Epic 50%, Legendary 20% |
| Void Chasm | Very High | 40-60 | 0% | 0% | 25% | 40% | 30% | 5% | Rare 25%, Epic 50%, Legendary 25% |
| Storm Peaks | Very High | 40-60 | 0% | 0% | 28% | 40% | 27% | 5% | Rare 28%, Epic 50%, Legendary 22% |
| Abyssal Depths | Very High | 40-60 | 0% | 0% | 26% | 40% | 29% | 5% | Rare 26%, Epic 52%, Legendary 22% |

---

## 3.9 Transition Zone Mechanics (Detailed)

### 3.9.1 Gradient Transition System

**Visual Blending**
- Each biome has **200-stud transition border** overlapping adjacent zones
- Assets from both biomes appear with decreasing/increasing density
- Ground textures blend using alpha transparency (smooth color shift)
- Lighting transitions gradually over 100-stud span

**Example: Forest → Badlands Transition**
```
Distance from Forest Edge:
0-50 studs:
  - Tree density: 100% → 60%
  - Grass color: Green → Yellow-brown
  - Temperature: Normal → Warm (visual heat shimmer begins)
  - Ambient sound: Birds 100% → 50%, wind increases

50-100 studs:
  - Tree density: 60% → 20% (trees show fire damage)
  - Ground: Grass patches with cracked earth between
  - Particles: Leaves → Mix of leaves and embers
  - Lighting: Green tint fades, orange tint increases

100-150 studs:
  - Tree density: 20% → 0% (only dead stumps remain)
  - Ground: Mostly cracked earth, scattered grass tufts
  - Particles: Primarily embers and dust
  - Ambient sound: Birds 0%, wind 100%, distant rumbles

150-200 studs:
  - Tree density: 0% (full desert)
  - Ground: Pure cracked earth and sand
  - Temperature: Hot (heat distortion visible)
  - Full Badlands biome reached
```

### 3.9.2 Natural Barrier Details

**Rivers**
- Width: 50-100 studs (varies along length)
- Depth: 20 studs (too deep to wade)
- Current strength: Pushes players 10 studs downstream per second
- Crossing options:
  - Bridges: 2-3 per river, wooden/stone depending on nearby biome
  - Swimming: Reduces movement to 8 studs/second (50% normal)
  - Stamina drain: 2x faster while swimming
- Strategic value: Natural PvP choke points at bridges

**Mountain Ridges**
- Height: 200-300 studs elevation gain
- Slope angle: 45-60° (difficult to climb)
- Mountain passes: 1-2 openings per ridge, 50-stud width
- Climbing penalties:
  - Movement speed: 4 studs/second (75% reduction)
  - Stamina drain: 3x normal rate
  - Vulnerable to attacks (can't dodge while climbing)
- Strategic value: Defensible positions, long-range visibility

**Cliffs**
- Height: 100-200 studs vertical drop
- Fall damage: 50% HP if falling from full height
- Descent options:
  - Find ramps/switchbacks (adds 2-3 minutes travel)
  - Use glider item in Storm Peaks (requires special gear)
  - Risk fall damage (strategic choice when fleeing)
- Strategic value: One-way retreat routes, high ground advantage

### 3.9.3 Transition Zone Spawns

**Hybrid Pet Spawns**
- 40% from biome A (lower-tier biome in most cases)
- 40% from biome B (higher-tier biome)
- 20% unique "hybrid" pets exclusive to that transition

**Example: Forest/Badlands Transition Hybrids**
- Scorched Vine Beast (Nature/Fire fusion)
- Desert Fox Spirit (Normal/Fire hybrid)
- Ash Butterfly (Bug/Fire combination)

**Hybrid Pet Characteristics**
- Level: Average of both biomes (Forest 1-10 + Badlands 15-30 = Transition 10-20)
- Rarity: Weighted toward uncommon/rare (transition exclusivity)
- Loot: Drops materials from both biomes (useful for cross-element crafting)

**Chest Distribution in Transitions**
- Spawn rate: 50% of normal biome density
- Rarity: Average between both biomes
- Trapped chance: Average between both biomes

---

## 4. EXTRACTION ZONE SYSTEM

### 4.1 Extraction Zone Overview

**Core Concept**
Extraction zones are temporary safe exit points that appear throughout the map, allowing players to leave the expedition with their collected loot and pets. Zones spawn on timers, remain active for limited durations, and close permanently, forcing players to find alternative exits or venture to the final extraction point near base.

**Strategic Purpose**
- Creates tension: "Do I extract now with guaranteed loot, or push deeper for better rewards?"
- Prevents infinite camping: Players can't stay in one safe area forever
- Encourages map traversal: Must explore to find active extraction zones
- Supports varied playstyles: Cautious players extract early, aggressive players stay late

### 4.2 Extraction Zone Types & Placement

**Type 1: Early Extraction Zones (Starter Tier)**

**Location**
- Spawn within starter biome ring (500-1,500 studs from base)
- Count: 3-4 zones per expedition
- Placement: Evenly distributed around base (North, East, South, West quadrants)
- Proximity to base: 800-1,200 studs average

**Timing**
- Spawn time: 0:00 (available at expedition start)
- Active duration: 20 minutes
- Close time: 20:00 mark
- Warning: 5-minute countdown notification ("Early extractions closing in 5 minutes")

**Visual Identity**
- Structure: Wooden watchtower with rope ladder
- Particles: Green smoke signal visible from 300 studs
- Minimap icon: Green evacuation symbol
- Audio: Distant horn sound when nearby (100-stud radius)

**Gameplay Characteristics**
- Safety level: High (within starter biome, low-level pet spawns)
- Extraction time: 10 seconds (stand in 20-stud radius zone)
- Interruption: Any damage cancels extraction, must restart timer
- Capacity: Unlimited (all players can use simultaneously)
- Risk: Low - primarily for cautious players or early loot banking

**Type 2: Mid Extraction Zones (Mid-Tier)**

**Location**
- Spawn within mid-tier biomes (1,500-4,000 studs from base)
- Count: 4-5 zones per expedition
- Placement: One per mid-tier biome, near biome edges
- Proximity to base: 2,500-3,500 studs average

**Timing**
- Spawn time: 10:00 (appear 10 minutes into expedition)
- Active duration: 20 minutes
- Close time: 30:00 mark
- Warning: 5-minute countdown notification

**Visual Identity**
- Structure: Stone pillar with magical runes
- Particles: Blue energy beam shooting skyward
- Minimap icon: Blue evacuation symbol
- Audio: Mystical hum when nearby (100-stud radius)

**Gameplay Characteristics**
- Safety level: Medium (within dangerous biomes, pet aggro possible)
- Extraction time: 15 seconds
- Interruption: Damage cancels extraction
- Capacity: Unlimited
- Risk: Medium - must navigate dangerous biome to reach, potential PvP ambush points

**Type 3: Late Extraction Zones (High-Tier)**

**Location**
- Spawn at edges of high-tier biomes (4,000-5,000 studs from base)
- Count: 2-3 zones per expedition
- Placement: Randomized at legendary biome borders
- Proximity to base: 4,500-5,000 studs (maximum distance)

**Timing**
- Spawn time: 20:00 (appear 20 minutes into expedition)
- Active duration: 15 minutes
- Close time: 35:00 mark
- Warning: 3-minute countdown notification

**Visual Identity**
- Structure: Ancient portal gate with glowing archway
- Particles: Purple reality distortion effect
- Minimap icon: Purple evacuation symbol
- Audio: Deep resonance when nearby (150-stud radius)

**Gameplay Characteristics**
- Safety level: Very Low (surrounded by legendary pets and hazards)
- Extraction time: 20 seconds
- Interruption: Damage cancels extraction
- Capacity: Limited (10 players maximum before portal destabilizes)
- Risk: Very High - deepest zones, guaranteed PvP in PvPvE, environmental hazards

**Type 4: Final Extraction (Base Hub Emergency)**

**Location**
- Base hub center (0, 0 coordinates)
- Count: 1 zone (permanent fixture)
- Always active, never closes

**Timing**
- Spawn time: 0:00 (always available)
- Active duration: Entire expedition
- Close time: Never (fallback extraction)
- Warning: None (always accessible)

**Visual Identity**
- Structure: Massive stone gateway with defensive walls
- Particles: White light column (visible from any point on map)
- Minimap icon: White home symbol
- Audio: Sanctuary bell tolling (audible from 500 studs)

**Gameplay Characteristics**
- Safety level: Medium-Low (see Pet Alert Mechanic below)
- Extraction time: 5 seconds (fastest extraction)
- Interruption: Damage cancels extraction
- Capacity: Unlimited
- Risk: Triggers Pet Alert Mechanic (see Section 4.3)

### 4.3 Base Hub Pet Alert Mechanic

**Core Concept**
When a player initiates extraction at the base hub, all nearby pets (within 500 studs) become alerted and converge on the base, attempting to prevent the player's escape. This creates dramatic tension during final extractions.

**Alert Trigger**
- Activation: Player enters base extraction zone (20-stud radius)
- Alert radius: 500 studs from base center
- Affected pets: All wild pets within radius, regardless of type/level
- Alert duration: Until player completes extraction or dies

**Pet Behavior During Alert**
- Aggro: All alerted pets immediately aggro to extracting player
- Movement: Pets sprint toward base at 2x normal speed
- Priority targeting: Ignore other players, focus on extractor
- Arrival time: Varies by distance (50-500 studs = 10-100 seconds)
- Combat: Pets attack normally once in range

**Wave Structure**
```
0-15 seconds: Nearest pets arrive (0-100 studs away)
  - 2-5 pets typically
  - Starter biome pets (low level)
  
15-30 seconds: Mid-range pets arrive (100-300 studs away)
  - 5-10 pets typically
  - Mix of starter and mid-tier pets
  
30-60 seconds: Distant pets arrive (300-500 studs away)
  - 10-20 pets potentially
  - Includes any mid/high-tier pets that were nearby
```

**Strategic Implications**
- Early expedition base extraction: Few pets nearby, relatively safe
- Late expedition base extraction: Potentially surrounded by strong pets from recent hunting
- Player decisions:
  - Clear area before extraction (proactive)
  - Sprint to base and extract quickly (risky)
  - Use pet companions to defend during extraction (tactical)

**Visual/Audio Feedback**
- Alert trigger: Screen rumble, ominous music sting
- Pet alerts: Red exclamation marks above pet heads
- Minimap: Red dots converging on base
- Audio: Roars, howls, and creature sounds intensifying
- Warning message: "Pets are alerted to your presence!"

**Companion Pet Interaction**
- Player's companion pet automatically engages alerted pets
- Companion prioritizes strongest threats first
- Creates 5-10 second buffer for player to complete extraction
- Companion returns to player after successful extraction

### 4.4 Extraction Process Mechanics

**Initiation**
1. Player enters extraction zone (20-stud radius circle)
2. UI prompt appears: "Hold [E] to Extract"
3. Extraction timer begins (duration varies by zone type)
4. Circular progress bar fills around screen center
5. Player character performs extraction animation (hands raised, glowing effect)

**During Extraction**
- Movement: Player locked in place (cannot move)
- Rotation: Player can look around (camera control only)
- Actions disabled: Cannot attack, use items, or interact
- Vulnerability: Fully exposed to attacks
- Party members: Can defend extracting player

**Interruption Conditions**
- Taking any damage: Resets extraction timer to 0
- Leaving extraction zone: Cancels extraction
- Player death: Extraction fails, loot lost
- Zone closure: If timer expires mid-extraction, player has 10 seconds to finish or zone vanishes

**Successful Extraction**
1. Timer completes, bright flash of light
2. Player character vanishes with teleport effect
3. Loading screen: "Returning to Laboratory..."
4. All carried loot/pets transferred to permanent storage
5. Expedition summary screen shows stats, loot acquired, XP earned

**Failed Extraction**
- Death during extraction: Standard permadeath rules apply (lose everything except secure pet slot)
- Zone closes: Must find alternative extraction or return to base
- Party wipe: All players die, everyone loses loot

### 4.5 Extraction Zone Discovery & Navigation

**Fog of War Integration**
- Extraction zones only appear on minimap once discovered (within 100-stud range)
- Undiscovered zones show no indication (encourages exploration)
- Once discovered, zone remains on minimap even if player leaves area
- Discovered zones shared with party members (squad communication)

**Minimap Indicators**
- Active zone: Solid colored icon (green/blue/purple based on tier)
- Closing soon: Flashing icon with countdown timer (5 minutes remaining)
- Closed zone: Grayed out icon with X overlay (no longer accessible)
- Base hub: Always visible white home icon

**Distance Indicators**
- Compass shows direction to nearest active extraction
- Distance readout: "Nearest Extraction: 450 studs NW"
- Updates in real-time as player moves
- Prioritizes closest open zone

**Audio Cues**
- Proximity alerts: Distinctive sound when within 200 studs of extraction
- Closing warnings: Urgent audio sting at 5-minute mark
- Direction indicators: Stereo audio guides player toward zone (louder in correct direction)

### 4.6 PvPvE Extraction Dynamics

**Contested Extractions**
- Multiple squads can use same extraction zone simultaneously
- No limit on concurrent extractions (except late zones: 10 player cap)
- PvP is enabled in extraction zones (no safe zones)
- Creates high-tension standoffs: "Do we fight or cooperate?"

**Ambush Tactics**
- Experienced players camp popular extraction zones
- Late-game zones become PvP hotspots (everyone converges)
- Squads must scout extraction zones before committing
- Smoke grenades/decoys (craftable items) can create distractions

**Counter-Ambush Strategies**
- Use unpopular extraction zones (longer travel but safer)
- Extract during closing window (last 2 minutes, ambushers already left)
- Coordinate squad covering fire while one member extracts
- Sacrifice low-value player as distraction (controversial tactic)

**Extraction Denial**
- Killing player mid-extraction drops their loot at zone
- Attackers can steal loot from killed extractors
- Creates risk: "Do we extract safely or kill others for more loot?"
- Rewards aggressive PvP playstyle in late-game

---

## 5. BASE HUB ARCHITECTURE

### 5.1 Base Hub Overview

**Dual Base Concept**
Eternal Wilds features two distinct "base" locations that serve different purposes:

1. **Expedition Base Hub** (In-World Safe Zone)
   - Located in center of procedurally generated expedition map
   - Temporary structure that exists only during current expedition
   - Provides basic safety, crafting, and extraction functions
   - Accessible during active expedition only

2. **Laboratory Base** (Persistent Player Instance)
   - Personal instanced space outside expedition loop
   - Permanent home for pet collection, advanced crafting, customization
   - Accessible between expeditions (main menu hub)
   - Social space where other players can visit
   - **Note**: Laboratory Base covered in separate documentation (Part 8)

**This section focuses on Expedition Base Hub only.**

### 5.2 Expedition Base Hub Layout

**Size & Structure**
- Total area: 500-stud radius circle (785,000 square studs)
- Outer wall: 15-stud tall wooden palisade with watchtowers
- Interior zones: 4 distinct functional areas
- Elevation: Ground level (flat terrain)

**Zone 1: Extraction Plaza (Center)**
- Location: Dead center of base (coordinates 0, 0)
- Size: 100-stud radius circular platform
- Features:
  - Massive stone gateway (final extraction point)
  - White light column effect (visible from anywhere)
  - Bench seating for resting (HP/stamina regen +50%)
  - Ambient peaceful music (no combat sounds)
- Function: Primary extraction zone, social gathering point

**Zone 2: Crafting Quarter (North Quadrant)**
- Location: 200 studs north of center
- Size: 150-stud radius semicircle
- Structures:
  - Basic crafting table (wood structure, anvil, tools)
  - Campfire (cooking/consumable crafting)
  - Material storage chest (deposit excess materials)
  - Blueprint board (view unlocked recipes)
- NPCs:
  - Crafting Vendor (sells basic recipes for currency)
  - Repair Technician (repairs durability for cost)

**Zone 3: Supply Storage (East Quadrant)**
- Location: 200 studs east of center
- Size: 100-stud radius area
- Structures:
  - Warehouse building (open-sided barn design)
  - Storage crates (visual props, no interaction)
  - Item deposit boxes (transfer items to Laboratory Base)
- NPCs:
  - Quartermaster (explains storage system)
  - Merchant (sells basic consumables: bandages, torches, food)

**Zone 4: Pet Sanctuary (West Quadrant)**
- Location: 200 studs west of center
- Size: 150-stud radius open field
- Features:
  - Grass field with flower patches
  - Small pond (decorative, pets drink from it)
  - Trees for shade (visual only)
  - Pet interaction zone (players can view companion pets)
- NPCs:
  - Pet Caretaker (provides pet tips, lore)
  - Veterinarian (heals pet HP for free)

**Zone 5: Tutorial Area (South Quadrant)**
- Location: 200 studs south of center
- Size: 100-stud radius training ground
- Features:
  - Training dummies (practice combat timing)
  - Target range (test pet abilities)
  - Tutorial signs (explain game mechanics)
- NPCs:
  - Instructor (provides tutorial quests)
  - Lore Keeper (explains world backstory)

### 5.3 Base Hub Safety Mechanics

**Safe Zone Rules**
- Combat disabled: Players cannot attack each other or pets
- Pet spawns: No wild pets spawn inside base walls
- Environmental hazards: None (no damage sources)
- Regeneration: HP regenerates at 5% per second while inside base
- Stamina: Full stamina regeneration in 3 seconds (faster than outside)

**Entry/Exit Points**
- Gates: 4 main gates (North, East, South, West)
- Gate size: 30 studs wide (accommodate multiple players)
- Gate state: Always open (no doors, free passage)
- Transition: Stepping through gate exits safe zone (combat re-enabled immediately)

**Pet Alert Exception**
- Safe zone protection disabled when player initiates extraction at plaza
- Pet Alert Mechanic overrides safe zone (pets can enter during extraction)
- Warning message: "You are no longer protected - pets are incoming!"
- Other players in base remain safe (only extractor is vulnerable)

### 5.4 Basic Crafting System (Base Hub Only)

**Crafting Table Capabilities**
The base hub crafting table provides access to **basic consumables only**. Advanced gear crafting requires Laboratory Base.

**Available Recipes:**

**Bandages** (Healing Consumable)
- Materials: 3x Plant Fiber (common material)
- Effect: Restore 25% HP over 5 seconds
- Cooldown: 30 seconds between uses
- Weight: 1 inventory slot

**Torch** (Light Source)
- Materials: 2x Wood, 1x Plant Fiber
- Effect: Provides 50-stud radius light for 10 minutes
- Durability: Consumed after 10 minutes
- Weight: 1 inventory slot

**Stamina Potion** (Energy Consumable)
- Materials: 5x Berry (foraged from bushes), 1x Water
- Effect: Restore 50% stamina instantly
- Cooldown: 60 seconds between uses
- Weight: 1 inventory slot

**Antidote** (Status Cure)
- Materials: 3x Herb (foraged from toxic swamp), 2x Water
- Effect: Remove poison/burn/freeze status effects
- Cooldown: None (can spam if needed)
- Weight: 1 inventory slot

**Smoke Bomb** (Tactical Item)
- Materials: 5x Ash (from scorched badlands), 3x Explosive Powder (rare drop)
- Effect: Create 30-stud smoke cloud lasting 15 seconds (blocks vision)
- Cooldown: None (limited by materials)
- Weight: 1 inventory slot

**Repair Kit** (Gear Maintenance)
- Materials: 10x Metal Scrap (common drop), 5x Leather (uncommon drop)
- Effect: Restore 25% durability to one equipped item
- Cooldown: None
- Weight: 1 inventory slot

**Crafting Interface**
- UI: Grid showing available recipes with material requirements
- Highlighting: Recipes with sufficient materials glow green
- Locked recipes: Grayed out with padlock icon (unlock via blueprints)
- Batch crafting: Hold button to craft multiple (5 per batch maximum)
- Crafting time: Instant (no waiting animation)

**Material Storage Chest**
- Capacity: 50 slots (separate from player inventory)
- Purpose: Store excess materials to free inventory space
- Persistence: Materials remain in chest for duration of expedition
- Shared: Not shared with other players (personal storage)
- Extraction: Materials in chest are NOT extracted (must be in inventory)
  - Strategic choice: Deposit low-value materials, keep high-value in inventory

### 5.5 NPC Vendors & Services

**Crafting Vendor**
- Function: Sells basic crafting recipes (blueprints)
- Currency: Expedition Currency (earned from pet defeats, chest loots)
- Available recipes:
  - Bandage Recipe: 50 currency
  - Torch Recipe: 30 currency
  - Stamina Potion Recipe: 75 currency
  - Antidote Recipe: 100 currency
  - Smoke Bomb Recipe: 200 currency
- Inventory: Refreshes each expedition (random selection of 3-5 recipes)

**Repair Technician**
- Function: Repairs equipped gear durability
- Cost: 10 currency per 1% durability restored
  - Example: Restore 50% durability = 500 currency
- Speed: Instant repair (no waiting)
- Limitations: Cannot repair broken gear (0% durability = permanently lost)

**Merchant**
- Function: Sells basic consumables
- Currency: Expedition Currency
- Inventory:
  - Bandage: 20 currency
  - Torch: 15 currency
  - Stamina Potion: 30 currency
  - Antidote: 40 currency
  - Water (consumable): 5 currency
  - Bread (restores 10% HP): 10 currency
- Stock: Unlimited (can buy as many as affordable)

**Quartermaster**
- Function: Explains storage and extraction systems (tutorial NPC)
- Services: None (dialogue only)
- Lore: Provides tips on inventory management

**Pet Caretaker**
- Function: Explains pet companion mechanics (tutorial NPC)
- Services: Free pet HP healing (instant, unlimited uses)
- Interaction: Players can view their companion pets here (cosmetic)

**Veterinarian**
- Function: Heals companion pet HP to full
- Cost: Free (unlimited uses)
- Speed: Instant
- Availability: Always present

**Instructor**
- Function: Provides tutorial quests for new players
- Quests:
  - "Capture Your First Pet" (Reward: 100 currency)
  - "Defeat 5 Common Pets" (Reward: 150 currency)
  - "Open 3 Chests" (Reward: 100 currency)
  - "Extract Successfully" (Reward: 200 currency)
- One-time rewards: Cannot repeat quests

**Lore Keeper**
- Function: Provides world backstory through dialogue
- Services: None (lore/dialogue only)
- Unlock: Additional lore entries by discovering landmarks

### 5.6 Base Hub Ambience & Atmosphere

**Visual Design**
- Architecture: Rustic wooden structures with stone foundations
- Color palette: Warm browns, greens, natural tones (inviting, safe)
- Lighting: Torches, lanterns, campfires (cozy illumination)
- NPCs: 10-15 total (vendors + background characters for immersion)
- Animals: Passive creatures (birds, rabbits) roaming freely (aesthetic only)

**Audio Design**
- Music: Calm orchestral theme with acoustic instruments
- Ambient sounds: Crackling fire, distant birdsong, wind chimes
- NPC chatter: Background dialogue (muffled conversation sounds)
- No combat sounds: Emphasizes safety and peace

**Player Interaction**
- Emotes: Players can use social emotes (/wave, /sit, /dance)
- Chat: Text chat enabled (no voice chat in base for now)
- Pet display: Companion pets visible to other players (show off rare catches)
- Resting: Sitting on benches provides HP regen buff

---

## 6. WILDLIFE EXTINCTION MECHANIC

### 6.1 Extinction System Overview

**Core Concept**
The Wildlife Extinction system creates organic time pressure by gradually reducing pet spawn populations throughout the expedition. Instead of artificial closing zones or storms, the world's ecosystem naturally depletes as players hunt, forcing strategic decisions about when to extract versus continuing the hunt for increasingly rare spawns.

**Design Philosophy**
- **Thematic coherence**: Players witness ecosystem collapse from overhunting
- **Natural pacing**: Early abundance → mid-game scarcity → late-game desperation
- **Strategic depth**: Common pets extinct first, legendary pets appear later
- **Anti-camping**: Valuable content literally disappears, forcing movement
- **Memorable moments**: Dramatic extinction events create emotional beats

**Extinction Stages**
The system operates through 4 distinct waves over a 45-minute expedition, each with different spawn behavior, despawn rates, and rarity availability.

### 6.2 Wave 1: Abundance (0-15 Minutes)

**Timing**
- Start: 0:00 (expedition begins)
- Duration: 15 minutes
- End: 15:00 mark
- Phase name: "The Wilds are Thriving"

**Spawn Behavior**

**Common Pets**
- Spawn rate: 100% normal (1 pet per 200 studs in appropriate biomes)
- Respawn: 3 minutes after defeat/capture
- Lifespan: 10 minutes after spawn (then despawn naturally)
- Total population: ~200-300 common pets active on map simultaneously

**Uncommon Pets**
- Spawn rate: 100% normal (1 pet per 500 studs)
- Respawn: 5 minutes after defeat/capture
- Lifespan: 15 minutes after spawn
- Total population: ~80-120 uncommon pets active

**Rare Pets**
- Spawn rate: 100% normal (1 pet per 1,000 studs)
- Respawn: 8 minutes after defeat/capture
- Lifespan: 20 minutes after spawn
- Total population: ~40-60 rare pets active

**Epic Pets**
- Spawn rate: Limited (1 pet per 2,000 studs, only in mid-tier biomes)
- Respawn: None (one-time spawns)
- Lifespan: 30 minutes after spawn
- Total population: ~15-20 epic pets active

**Legendary Pets**
- Spawn rate: None (do not spawn during Wave 1)
- Availability: Wave 2 onwards only

**Player Experience**
- Overwhelming abundance of targets
- Easy to find common/uncommon pets for basic materials
- Players spread across map farming efficiently
- Low competition for spawns (plenty for everyone)
- Sense of safety and control

**Strategic Implications**
- Optimal time for new players to farm basic resources
- Experienced players focus on uncommon/rare for better materials
- PvP less common (players focused on PvE farming)
- No urgency to extract (plenty of time remaining)

### 6.3 Wave 2: Thinning (15-30 Minutes)

**Timing**
- Start: 15:00 mark
- Duration: 15 minutes
- End: 30:00 mark
- Phase name: "The Wilds are Thinning"

**Extinction Event Trigger (15:00 Mark)**

**Visual/Audio Spectacle**
1. Screen rumble (2-second earthquake effect)
2. All common pets emit panicked behavior:
   - Pets stop attacking, flee toward biome edges
   - Movement speed increased by 50%
   - Emit distress calls (high-pitched cries)
3. Environmental response:
   - Ambient wildlife sounds fade by 50%
   - Sky darkens slightly (cloud coverage increases)
   - Wind sound increases in intensity
4. UI notification: "Common creatures are fleeing the Wilds..."
5. Audio sting: Melancholic orchestral chord (emotional impact)
6. Duration: 10-second spectacle, then mass despawn

**Spawn Behavior Changes**

**Common Pets**
- Mass despawn: 70% of all common pets vanish instantly at 15:00
- Remaining population: 30% stay alive (60-90 pets total)
- New spawns: Disabled (no more common pets spawn)
- Lifespan: Remaining pets despawn over next 5 minutes (gradual extinction)
- By 20:00 mark: Common pets completely extinct

**Uncommon Pets**
- Partial despawn: 40% despawn at 15:00
- Remaining population: 60% stay alive (48-72 pets)
- Respawn rate: Reduced to 50% normal (10 minutes instead of 5)
- Lifespan: 12 minutes (reduced from 15)
- Total population decline: ~50-60 uncommon pets active

**Rare Pets**
- No despawn: All rare pets remain alive
- Spawn rate: 100% normal (unchanged)
- Respawn: Still 8 minutes
- Lifespan: 20 minutes (unchanged)
- Total population stable: ~40-60 rare pets active

**Epic Pets**
- No despawn: All epic pets remain
- Spawn rate: Slightly increased (1 per 1,500 studs, was 1 per 2,000)
- Respawn: None (still one-time spawns)
- Lifespan: 30 minutes (unchanged)
- Total population increase: ~20-30 epic pets active

**Legendary Pets** (FIRST APPEARANCE)
- Spawn rate: Enabled (1 per 3,000 studs, high-tier biomes only)
- Respawn: None (one-time spawns)
- Lifespan: 30 minutes after spawn
- Spawn locations: Volcanic Rift, Void Chasm, Storm Peaks, Abyssal Depths
- Total population: ~8-12 legendary pets active
- Spawn announcement: Global message to all players

**Legendary Spawn Announcement System**
When a legendary pet spawns, ALL players receive:
```
UI Notification (center screen):
"⚠️ LEGENDARY SIGHTING ⚠️"
"[Inferno Salamander] has appeared in the Volcanic Rift"

Audio: Epic horn fanfare (2 seconds)
Minimap: Golden pulse effect in biome direction
Compass: Golden arrow pointing toward biome
```

**Player Experience**
- Sudden realization: "The world is changing"
- Common pet extinction creates scarcity
- Focus shifts to uncommon/rare pets
- Legendary spawns create "event moments"
- Competition increases (fewer targets, more players)
- First extraction wave: Cautious players leave with guaranteed loot

**Strategic Implications**
- Players must decide: Extract now or hunt legendaries?
- Common materials no longer farmable (use wisely)
- Legendary spawns create PvP hotspots in high-tier biomes
- Time pressure begins (20 minutes remaining)

### 6.4 Wave 3: Scarcity (30-45 Minutes)

**Timing**
- Start: 30:00 mark
- Duration: 15 minutes
- End: 45:00 mark (final wave transition)
- Phase name: "The Wilds are Silent"

**Extinction Event Trigger (30:00 Mark)**

**Visual/Audio Spectacle**
1. Stronger screen rumble (3-second earthquake)
2. All uncommon pets emit panic behavior and flee
3. Environmental response:
   - Ambient wildlife sounds fade to 25% volume
   - Sky significantly darker (overcast, ominous)
   - Fog density increases by 50%
   - Music shifts to eerie, empty tones
4. UI notification: "Uncommon creatures have abandoned the Wilds..."
5. Audio sting: Haunting choir vocals (emotional weight)
6. Duration: 15-second spectacle

**Spawn Behavior Changes**

**Common Pets**
- Status: Extinct (already extinct since 20:00)
- Population: 0

**Uncommon Pets**
- Mass despawn: 90% despawn at 30:00 mark
- Remaining population: 10% stay alive (5-7 pets total)
- New spawns: Disabled completely
- Lifespan: Remaining pets despawn over next 2 minutes
- By 32:00 mark: Uncommon pets completely extinct

**Rare Pets**
- Partial despawn: 60% despawn at 30:00
- Remaining population: 40% stay alive (16-24 pets)
- Respawn rate: Disabled (no new rare spawns)
- Lifespan: 10 minutes (reduced from 20)
- By 40:00 mark: Rare pets nearly extinct

**Epic Pets**
- Partial despawn: 40% despawn at 30:00
- Remaining population: 60% stay alive (12-18 pets)
- Respawn: None (still one-time spawns)
- Lifespan: 15 minutes (reduced from 30)
- Total population: ~12-18 epic pets active

**Legendary Pets**
- No despawn: All legendary pets remain
- Spawn rate: Increased (1 per 2,000 studs, was 1 per 3,000)
- Respawn: None
- Lifespan: 30 minutes (unchanged)
- New legendary spawns possible (replaces extinct spawns)
- Total population increase: ~12-18 legendary pets active

**Mythic Pets** (FIRST APPEARANCE)
- Spawn rate: Enabled (1-2 pets total across entire map)
- Respawn: None (unique one-time spawn)
- Lifespan: Until expedition ends or captured
- Spawn locations: Only in furthest legendary biome (5,000 studs from base)
- Global announcement with special effects

**Mythic Spawn Announcement**
```
UI Notification (full screen takeover):
"🔥 MYTHIC ENTITY AWAKENED 🔥"
"[Eternal Phoenix] has manifested in the Storm Peaks"

Audio: Epic orchestral crescendo (5 seconds)
Screen effect: Golden flash, reality distortion
Minimap: Entire map pulses gold
Compass: Glowing golden arrow (visible through terrain)
All players' screens shake for 1 second
```

**Player Experience**
- World feels empty and haunted
- Scarcity forces deeper exploration
- Legendary pets are primary targets
- Mythic spawn creates server-wide event
- PvP intensifies (everyone hunting same rare spawns)
- Second extraction wave: Mid-tier players extract to secure loot

**Strategic Implications**
- Only legendary/mythic hunting remains viable
- Players concentrated in high-tier biomes (PvP inevitable)
- Risk vs reward at peak: "Do I hunt mythic or extract safely?"
- Time pressure critical (15 minutes remaining)

### 6.5 Wave 4: Collapse (45+ Minutes)

**Timing**
- Start: 45:00 mark
- Duration: Until server closes (typically 60:00 maximum)
- Phase name: "The Wilds are Dying"

**Extinction Event Trigger (45:00 Mark)**

**Visual/Audio Spectacle**
1. Intense screen rumble (5-second earthquake)
2. All rare and epic pets flee simultaneously
3. Environmental response:
   - Ambient sounds completely silent (no birds, wind, etc.)
   - Sky blood-red or dark purple (apocalyptic)
   - Heavy fog reduces visibility to 100 studs
   - Music stops entirely (only silence and wind)
4. UI notification: "The Wilds are collapsing - Extract immediately!"
5. Audio: Silence, then single mournful horn note
6. Duration: 30-second spectacle (dramatic finale)

**Spawn Behavior Changes**

**Common/Uncommon Pets**
- Status: Extinct (long extinct)
- Population: 0

**Rare/Epic Pets**
- Mass despawn: 100% despawn at 45:00
- Population: 0 (completely extinct)
- Message: "Rare and Epic creatures have perished..."

**Legendary Pets**
- Rapid despawn: Begin despawning at accelerated rate
- Lifespan: 5 minutes after 45:00 mark (reduced from 30)
- No new spawns: All legendary spawn points disabled
- Despawn cascade: 1-2 legendary pets despawn per minute
- By 50:00 mark: Most legendaries extinct

**Mythic Pets**
- Status: Remain alive (final targets)
- Lifespan: Until captured or 60:00 mark
- Population: 1-2 mythic pets total (only targets left)
- Despawn warning: At 55:00, notification warns mythic will despawn in 5 minutes

**Server Closure Sequence**

**50:00 Mark**
- Warning: "Extraction zones closing in 10 minutes"
- Late extraction zones begin closing (one every 2 minutes)
- Audio: Urgent warning bells

**55:00 Mark**
- Warning: "Final extraction in 5 minutes - Return to Base Hub!"
- All extraction zones except base hub close
- Mythic pets emit distress call (last chance to capture)
- Music: Intense countdown theme

**58:00 Mark**
- Warning: "Server closing in 2 minutes - EXTRACT NOW!"
- Screen borders pulse red
- Compass locked to base hub direction
- NPCs at base shout warnings

**60:00 Mark**
- Server force-closes
- All remaining players auto-extracted (successful, keep loot)
- Expedition summary screen
- If player died before 60:00: Standard permadeath rules apply

**Player Experience**
- Apocalyptic atmosphere (world is dying)
- Only mythic hunting or immediate extraction viable
- Extreme time pressure
- PvP at maximum intensity (final loot grab)
- Dramatic conclusion to expedition

**Strategic Implications**
- Only the most aggressive players remain
- Mythic pets worth enormous risk
- Base hub becomes final battleground (PvPvE chaos)
- Players must extract or lose everything

### 6.6 Extinction Feedback Systems

**UI Indicators**

**Wildlife Population Meter**
- Location: Top-right of screen below minimap
- Visual: Horizontal bar with color gradient
  - Green (100-75%): Abundant
  - Yellow (75-50%): Thinning
  - Orange (50-25%): Scarce
  - Red (25-0%): Critical
- Text readout: "Wildlife: 87% Remaining"
- Updates every 30 seconds

**Biome Spawn Density Overlay**
- Minimap shows heatmap of active spawns
  - Bright colors: High spawn density
  - Dim colors: Low spawn density
  - Black: Extinct (no spawns)
- Updates every 60 seconds
- Example: "Forest: 12 pets | Badlands: 5 pets | Volcanic: 3 pets"

**Rarity Countdown Timers**
```
Common: EXTINCT (0 remaining)
Uncommon: EXTINCT (0 remaining)
Rare: 8 remaining (Despawning in 12 minutes)
Epic: 4 remaining (Despawning in 8 minutes)
Legendary: 6 remaining (Despawning in 15 minutes)
Mythic: 1 remaining (Eternal Phoenix - Storm Peaks)
```

**Environmental Feedback**

**Ambient Audio Changes**
- Wave 1 (0-15 min): Full wildlife soundscape
  - Birds chirping, insects buzzing, distant animal calls
  - Volume: 100%
- Wave 2 (15-30 min): Reduced wildlife sounds
  - Occasional bird calls, mostly wind
  - Volume: 50%
- Wave 3 (30-45 min): Sparse sounds
  - Rare animal sounds, heavy wind
  - Volume: 25%
- Wave 4 (45+ min): Complete silence
  - Only wind, player footsteps, combat sounds
  - Volume: 0% (ambient wildlife extinct)

**Visual Atmosphere Changes**
- Wave 1: Vibrant, lively world (animals visible in background)
- Wave 2: Slightly muted colors, clouds increase
- Wave 3: Desaturated colors, heavy fog, dark sky
- Wave 4: Near-monochrome, blood-red sky, apocalyptic

**Music Progression**
- Wave 1: Adventurous orchestral theme (hopeful, energetic)
- Wave 2: Tension builds (minor key elements introduced)
- Wave 3: Eerie, haunting (sparse instrumentation)
- Wave 4: Silent or intense countdown track (dramatic finale)

**Notification System**

**Major Extinction Milestones**
```
15:00 - "Common creatures are fleeing the Wilds..."
20:00 - "Common creatures have gone extinct."
30:00 - "Uncommon creatures have abandoned the Wilds..."
32:00 - "Uncommon creatures have gone extinct."
40:00 - "Rare creatures are nearly extinct."
45:00 - "The Wilds are collapsing - Extract immediately!"
50:00 - "Legendary creatures are perishing rapidly."
55:00 - "Only mythic entities remain - Final chance!"
60:00 - "The expedition has ended."
```

**Countdown Warnings (Audio + Visual)**
- 5 minutes before wave transition: Subtle warning chime
- 1 minute before wave transition: Urgent warning tone
- Wave transition: Dramatic audio sting + screen effect

### 6.7 Super Elusive Pets (Special Spawn Type)

**Definition**
Super Elusive Pets are ultra-rare variants of legendary/mythic pets with extremely short lifespans and high capture difficulty. They represent the pinnacle of challenge and reward.

**Spawn Mechanics**
- Spawn rate: 1-3 per entire expedition (random, not guaranteed)
- Spawn timing: Only during Wave 2 or 3 (never Wave 1 or 4)
- Spawn locations: Completely random (any biome, no proximity rules)
- Lifespan: 3-5 minutes (significantly shorter than regular legendaries)
- Despawn warning: 1-minute warning notification

**Global Announcement**
```
UI Notification (urgent style):
"⚡ ELUSIVE CREATURE SPOTTED ⚡"
"[Shadow Wraith Dragon] has appeared somewhere in the Wilds!"
"Estimated time remaining: 5 minutes"

Audio: Mysterious ethereal sound (creates urgency)
Minimap: NO location indicator (must search)
Compass: NO direction arrow (true hunt)
```

**Discovery Mechanics**
- No map indicators: Players must physically explore to find
- Visual cue when nearby (50-stud range):
  - Unique particle trail leading toward pet
  - Faint glowing aura visible through terrain
  - Distinct audio hum (directional, gets louder when close)
- Upon discovery:
  - Screen flash effect
  - Personal notification: "You've discovered [Shadow Wraith Dragon]!"
  - Location NOT shared with other players (competitive advantage)

**Capture Difficulty**
- Combat: 6-star difficulty (hardest in game)
- HP: 5x normal legendary HP
- Capture rate: 1% base (requires perfect weakening + best capture items)
- Special mechanics: Unique attack patterns, teleportation, invulnerability phases
- Time pressure: Must defeat AND capture within 3-5 minute window

**Strategic Implications**
- High-risk, high-reward: Spend time hunting or focus on guaranteed targets?
- Information advantage: First discoverer has head start
- PvP trigger: Other players may track you to find the pet
- Time cost: 5+ minutes to hunt/capture could be spent farming other legendaries

**Rewards**
- Guaranteed mythic-tier materials (5-10x legendary value)
- Unique pet variant (different coloration, special ability)
- Achievement unlock: "Elusive Hunter" title
- Bragging rights: Rare pet collection showcase

### 6.8 Extinction System Balance Considerations

**Pet Count Formulas**

**Wave 1 Totals**
```
Common: 250 pets (70% of population)
Uncommon: 100 pets (25%)
Rare: 50 pets (4%)
Epic: 20 pets (1%)
Legendary: 0 pets
Mythic: 0 pets
Total: 420 pets active
```

**Wave 2 Totals**
```
Common: 75 → 0 (extinct by 20:00)
Uncommon: 60 pets (gradual decline)
Rare: 50 pets (stable)
Epic: 25 pets (increase)
Legendary: 10 pets (first appearance)
Mythic: 0 pets
Total: 145-220 pets active (declining)
```

**Wave 3 Totals**
```
Common: 0 (extinct)
Uncommon: 0 (extinct by 32:00)
Rare: 20 pets (declining)
Epic: 15 pets (declining)
Legendary: 15 pets (increase)
Mythic: 1-2 pets (first appearance)
Total: 50-52 pets active
```

**Wave 4 Totals**
```
Common: 0 (extinct)
Uncommon: 0 (extinct)
Rare: 0 (extinct at 45:00)
Epic: 0 (extinct at 45:00)
Legendary: 5-10 pets (rapid despawn)
Mythic: 1-2 pets (final targets)
Total: 6-12 pets active (collapsing)
```

**Player Density Considerations**
- Solo/Co-op PvE: Spawn counts unchanged (balanced for 1-4 players)
- PvPvE (20-40 players): Spawn counts increased by 50% (more competition)
  - Example: Wave 1 common pets = 375 instead of 250
  - Prevents instant depletion from large player count

**Anti-Exploit Measures**
- Spawn locations randomized each expedition (can't memorize)
- Despawn timers server-authoritative (no client manipulation)
- Pet capture logs (track if players exploiting spawn mechanics)
- Legendary/Mythic spawns have anti-camp radius (won't spawn if players nearby)

---

## 7. DAY/NIGHT CYCLE SYSTEM

### 7.1 Day/Night Overview

**Cycle Duration**
- Full cycle: 45 minutes (matches expedition length)
- Day phase: 30 minutes (0:00 - 30:00)
- Dusk phase: 5 minutes (30:00 - 35:00)
- Night phase: 10 minutes (35:00 - 45:00)
- No dawn phase: Expedition ends before dawn

**Synchronization**
- Day/night tied to expedition timer (not real-world time)
- All players in expedition experience same time of day
- Consistent across seeds (same progression every expedition)

### 7.2 Day Phase (0:00 - 30:00)

**Lighting**
- Sun position: Overhead (zenith) at 15:00, gradual descent
- Brightness: 100% (full visibility)
- Shadows: Dynamic, medium-length
- Sky color: Blue with white clouds
- Ambient light: Warm yellow-white

**Gameplay Effects**
- Visibility: Maximum (200-stud view distance)
- Pet behavior: Normal aggro ranges
- Environmental hazards: Standard (no night-specific dangers)
- Navigation: Easy (landmarks clearly visible)

**Biome Lighting Variations**
- Forest: Dappled sunlight through canopy
- Badlands: Harsh, bright (heat shimmer intensifies)
- Tundra: Bright reflection off snow/ice (glare effect)
- Swamp: Filtered green light through fog
- Volcanic: Sun obscured by ash clouds (dim even during day)

### 7.3 Dusk Phase (30:00 - 35:00)

**Lighting Transition**
- Sun position: Descending toward horizon (western sky)
- Brightness: 100% → 40% (gradual dimming)
- Shadows: Lengthening dramatically
- Sky color: Orange, pink, purple gradient
- Ambient light: Warm orange fading to cool blue

**Visual Spectacle**
- Sunset colors reflect off water, ice, crystals
- Long dramatic shadows create atmosphere
- Bioluminescent elements begin glowing (preparation for night)
- First stars appear in darkening sky

**Gameplay Effects**
- Visibility: 200 → 120 studs (gradual reduction)
- Pet behavior: Nocturnal pets begin spawning
- Navigation: Landmarks still visible but harder to see
- Warning: "Night is falling - visibility will decrease"

### 7.4 Night Phase (35:00 - 45:00)

**Lighting**
- Sun position: Below horizon (full darkness)
- Brightness: 30% (significant visibility reduction)
- Shadows: Very dark (contrast with light sources)
- Sky color: Deep blue-black with stars/moon
- Ambient light: Cool blue moonlight

**Moon System**
- Moon position: Overhead at 40:00
- Moon phase: Always full (maximum light)
- Moonlight: Provides 30% base illumination
- Moon rays: Volumetric light beams through clouds

**Gameplay Effects**

**Visibility Reduction**
- Standard view distance: 120 studs (down from 200)
- Without light source: 60 studs (severe reduction)
- With torch: 50-stud radius bright, 120 total
- Pet glow: Some pets emit bioluminescence (visible from 150 studs)

**Pet Behavior Changes**
- Nocturnal variants: Exclusive night spawns (different loot tables)
- Daytime pets: 50% despawn at dusk (replaced by nocturnal)
- Aggro ranges: Increased by 25% (predators more aggressive)
- Ambush mechanics: Pets hide in darkness (surprise attacks)

**Bioluminescent Environment**
- Glowing plants: Mushrooms, flowers, algae emit light (navigation aids)
- Glowing insects: Fireflies, phosphorescent bugs (atmospheric)
- Bioluminescent trails: Some pets leave glowing footprints (tracking mechanic)
- Crystal glow: Crystal Caverns become brighter at night (safe haven)

**Night-Exclusive Spawns**

**Nocturnal Pet Types**
- Shadow creatures: Dark/Ghost types (only spawn at night)
- Lunar variants: Special moon-powered pets (enhanced stats)
- Predators: Aggressive hunters with stealth mechanics
- Bioluminescent pets: Glowing variants (beautiful, rare)

**Spawn Distribution**
- 50% of daytime pets replaced with nocturnal equivalents
- Nocturnal pets have 20% higher rarity drop rates (incentive to stay)
- Super Elusive pets 2x more likely to spawn at night (risk/reward)

**Strategic Implications**
- Light sources required: Torches, pet abilities, or suffer severe disadvantage
- Navigation harder: Easy to get lost, landmarks obscured
- PvP advantage: Stealth-focused players thrive (harder to spot)
- Higher rewards: Nocturnal pets drop better loot (incentive to risk)

### 7.5 Light Source Mechanics

**Torch Item**
- Radius: 50-stud bright zone, 120-stud visible zone
- Duration: 10 minutes per torch
- Crafting: 2x Wood, 1x Plant Fiber (cheap, renewable)
- Inventory: 1 slot per torch
- Drawback: Occupies hand slot (can't use weapon simultaneously)
- PvP risk: Makes player visible from 150 studs (beacon for enemies)

**Pet Luminescence Abilities**
- Certain pets emit passive light when summoned as companion
- Fire pets: Warm orange glow (40-stud radius)
- Electric pets: Blue-white flash (60-stud radius, pulsing)
- Fairy pets: Soft rainbow aura (50-stud radius, most aesthetic)
- Advantage: Hands-free lighting (can still fight)

**Environmental Light Sources**
- Campfires: Found near POIs, 60-stud radius (safe zones)
- Glowing crystals: In Crystal Caverns, 30-stud radius
- Lava: In Volcanic Rift, 100-stud radius (hazard + light)
- Bioluminescent pools: In Toxic Swamp, 40-stud radius

**Strategic Light Management**
- Trade-off: Visibility vs detection (PvP consideration)
- Resource cost: Torches consume inventory slots
- Pet choice: Glowing pets valuable at night (meta shift)
- Darkness ambush: Skilled players can navigate without light (stealth advantage)

### 7.6 Atmospheric Effects by Time

**Audio Changes**

**Day (0-30 min)**
- Birds chirping (high activity)
- Wind rustling leaves
- Distant animal calls
- Upbeat ambient music

**Dusk (30-35 min)**
- Birds quieting (settling for night)
- Crickets beginning (transition sound)
- Wind increasing
- Music shifts to minor key

**Night (35-45 min)**
- Owls hooting
- Wolves howling (distant)
- Cricket symphony
- Mysterious ambient music (tense, atmospheric)

**Visual Atmosphere**

**Day**
- Vibrant colors (full saturation)
- Clear skies (minimal fog)
- Active particle effects (butterflies, pollen)
- Bright, inviting

**Dusk**
- Warm color grading (orange/purple)
- Moderate fog (atmospheric depth)
- Transition particles (bats emerging, fireflies)
- Beautiful, cinematic

**Night**
- Desaturated colors (blue tint)
- Heavy fog (mystery, danger)
- Glowing particles (fireflies, spores, sparks)
- Dark, ominous

---

## 8. DYNAMIC WEATHER SYSTEM

### 8.1 Weather System Overview

**Core Concept**
Dynamic weather creates additional layer of environmental challenge and visual variety. Weather conditions affect visibility, movement, combat effectiveness, and strategic decisions. Each biome has unique weather patterns that reinforce its thematic identity and gameplay characteristics.

**Weather Architecture**
- **Biome-specific**: Each biome has its own weather pool (no snow in desert)
- **Periodic cycling**: Weather changes every 5-10 minutes (random intervals)
- **Gradual transitions**: 30-second fade between weather states (no instant changes)
- **Gameplay impact**: Weather affects mechanics, not just cosmetic
- **Player agency**: Weather can be mitigated with gear/items/pet abilities

**Weather Intensity Levels**
- **Clear**: No weather (baseline)
- **Light**: Minimal impact (mostly visual)
- **Moderate**: Noticeable gameplay effects
- **Heavy**: Significant challenge (forces adaptation)
- **Extreme**: Rare, dangerous conditions (survival challenge)

### 8.2 Universal Weather Effects (All Biomes)

**Clear Weather**
- Visibility: 200 studs (maximum)
- Movement: 100% normal speed
- Stamina drain: 100% normal rate
- Combat: No modifiers
- Duration: 40% of expedition time (most common)
- Audio: Biome ambient sounds only

**Light Rain**
- Visibility: 180 studs (minimal reduction)
- Movement: 100% speed (no penalty)
- Stamina drain: 100% normal
- Combat: No modifiers
- Visual: Light rain particles, wet ground textures
- Audio: Gentle patter sound
- Duration: 25% of expedition time
- Biomes: Forest, Swamp, Crystal Caverns

**Moderate Rain**
- Visibility: 150 studs (noticeable reduction)
- Movement: 95% speed (slight mud/slip)
- Stamina drain: 110% (rain fatigue)
- Combat: Fire-element damage reduced 15%
- Visual: Heavy rain sheets, puddles forming, dripping effects
- Audio: Loud rainfall, thunder distant
- Duration: 15% of expedition time
- Biomes: Forest, Swamp

**Heavy Thunderstorm**
- Visibility: 100 studs (significant reduction)
- Movement: 90% speed (slippery surfaces)
- Stamina drain: 125% (difficult conditions)
- Combat: Fire damage reduced 25%, Electric damage increased 25%
- Lightning strikes: Random 100-stud radius bolts (5% HP damage, 10-second warning)
- Visual: Torrential rain, lightning flashes, dark sky
- Audio: Thunder crashes, heavy downpour
- Duration: 10% of expedition time
- Biomes: Forest, Storm Peaks

**Fog**
- Visibility: 80 studs (severe reduction)
- Movement: 100% speed (no penalty)
- Stamina drain: 100% normal
- Combat: Ranged attacks -30% accuracy (hard to aim)
- Pet detection: Pet aggro range reduced by 50% (can sneak past)
- Visual: Thick fog banks, muted colors
- Audio: Muffled sounds, eerie atmosphere
- Duration: 10% of expedition time
- Biomes: Forest, Swamp, Tundra, Void Chasm

### 8.3 Biome-Specific Weather

**Whispering Forest Weather Pool**

**Sunny (Clear)**
- Occurrence: 50%
- Effects: Standard clear weather
- Visual: Blue sky, dappled sunlight through trees
- Strategic value: Optimal exploration conditions

**Light Rain**
- Occurrence: 25%
- Effects: As universal light rain
- Visual: Rain dripping through canopy, moss glistening
- Strategic value: Neutral (no real penalty)

**Heavy Rain**
- Occurrence: 15%
- Effects: As universal moderate rain
- Visual: Waterlogged forest floor, streams forming
- Strategic value: Fire pets less effective

**Thunderstorm**
- Occurrence: 8%
- Effects: As universal heavy thunderstorm
- Visual: Lightning striking tall trees, crashing branches
- Strategic value: High danger (lightning + tree falls)

**Dense Fog**
- Occurrence: 2%
- Effects: As universal fog
- Visual: Mysterious mist between trees, limited visibility
- Strategic value: Stealth advantage, easy to get lost

---

**Scorched Badlands Weather Pool**

**Clear Skies (Harsh Sun)**
- Occurrence: 60%
- Effects: Standard clear + heat shimmer
- Heat damage: 1% HP per second in open (existing mechanic)
- Visual: Wavering air, intense glare
- Strategic value: Baseline difficulty

**Dust Storm (Light)**
- Occurrence: 20%
- Visibility: 120 studs
- Movement: 95% speed (dust in face)
- Stamina drain: 115%
- Visual: Swirling dust clouds, orange tint
- Audio: Howling wind
- Strategic value: Navigation harder

**Dust Storm (Heavy)**
- Occurrence: 15%
- Visibility: 60 studs (severe)
- Movement: 85% speed (strong wind resistance)
- Stamina drain: 140%
- Heat damage: Paused during storm (dust blocks sun)
- Visual: Massive dust walls, near-blindness
- Audio: Roaring wind, sand impacts
- Strategic value: Can't navigate, must wait out or find shelter

**Scorching Heat Wave**
- Occurrence: 5%
- Visibility: 100 studs (shimmer distortion)
- Movement: 90% speed (exhaustion)
- Stamina drain: 150% (oppressive heat)
- Heat damage: 2% HP per second (doubled)
- Fire-element pets: +20% damage bonus
- Visual: Extreme heat distortion, mirage effects
- Audio: Crackling air
- Strategic value: Extreme danger, must use cover

**Sandstorm (Extreme)**
- Occurrence: Rare event (triggered at 40:00 mark once per expedition)
- Duration: 5 minutes
- Visibility: 30 studs (near-zero)
- Movement: 70% speed (barely able to move)
- Stamina drain: 200%
- Damage: 0.5% HP per second (sand abrasion)
- Minimap: Disabled (navigation impossible)
- Visual: Complete whiteout, violent sand
- Audio: Deafening roar
- Strategic value: Survival mode (find shelter or die)

---

**Frozen Tundra Weather Pool**

**Clear Skies (Bitter Cold)**
- Occurrence: 40%
- Effects: Standard clear + frostbite mechanic
- Frostbite: 1.5% HP per second standing still (existing mechanic)
- Visual: Crystal-clear sky, aurora at night
- Strategic value: Baseline difficulty

**Light Snow**
- Occurrence: 30%
- Visibility: 150 studs
- Movement: 95% speed (snow accumulation)
- Stamina drain: 110%
- Frostbite: 1.5% (unchanged)
- Visual: Gentle snowfall, accumulating on ground
- Audio: Soft wind, snow crunching
- Strategic value: Minimal impact

**Heavy Snow**
- Occurrence: 20%
- Visibility: 100 studs
- Movement: 85% speed (deep snow)
- Stamina drain: 130%
- Frostbite: 2% HP per second (increased cold)
- Footprints: Leave visible trails (tracking/PvP disadvantage)
- Visual: Heavy snowfall, drifts forming
- Audio: Howling wind
- Strategic value: Slower movement, easier tracking

**Blizzard**
- Occurrence: 8%
- Duration: 2 minutes per occurrence
- Visibility: 40 studs (whiteout conditions)
- Movement: 70% speed (barely able to walk)
- Stamina drain: 180%
- Frostbite: 3% HP per second (extreme cold)
- Ice pets: +25% damage bonus
- Visual: Complete whiteout, horizontal snow
- Audio: Screaming wind
- Strategic value: Must find shelter or die

**Aurora Storm (Rare)**
- Occurrence: 2% (mostly at night)
- Visibility: 120 studs (aurora light provides illumination)
- Movement: 100% speed
- Stamina drain: 90% (energizing effect)
- Frostbite: Paused (aurora warmth)
- Psychic/Fairy pets: +30% damage bonus
- Visual: Brilliant aurora curtains, shifting colors
- Audio: Ethereal humming
- Strategic value: Beautiful, beneficial weather (players seek it out)

---

**Toxic Swamp Weather Pool**

**Heavy Fog (Baseline)**
- Occurrence: 50%
- Effects: As universal fog
- Poison gas visibility: Gas clouds harder to see in fog
- Visual: Thick green-tinted mist
- Strategic value: Hazard concealment (more dangerous)

**Light Rain**
- Occurrence: 25%
- Visibility: 150 studs
- Movement: 95% speed (muddy ground)
- Stamina drain: 120%
- Poison pools: Diluted (1.5% damage instead of 2%)
- Visual: Rain hitting murky water, ripples
- Strategic value: Slight poison reduction (beneficial)

**Acid Rain**
- Occurrence: 20%
- Visibility: 120 studs
- Movement: 100% speed
- Stamina drain: 110%
- Acid damage: 1% HP per second in open areas
- Cover required: Must use trees, caves, platforms
- Poison damage: Stacks with acid (extremely dangerous)
- Visual: Green-tinted rain, sizzling surfaces
- Audio: Hissing, sizzling sounds
- Strategic value: Must constantly seek shelter

**Toxic Gas Surge**
- Occurrence: 5%
- Duration: 3 minutes
- Visibility: 60 studs (thick gas)
- Movement: 90% speed (choking)
- Stamina drain: 150%
- Poison damage: 2% HP per second (constant, no pools needed)
- Gas mask item: Negates damage (craftable, consumable)
- Visual: Dense green/purple gas clouds
- Audio: Choking, coughing (character sounds)
- Strategic value: Extremely dangerous, must have gas mask or extract

**Spore Bloom (Rare)**
- Occurrence: Rare event (30:00 mark, once per expedition)
- Duration: 5 minutes
- Visibility: 100 studs (glowing spores provide light)
- Movement: 80% speed (spores slow movement)
- Stamina drain: 200% (heavy breathing)
- Hallucinations: 25% chance per minute to see fake pets/players
- Vision distortion: Screen warps, color shifts
- Mushroom spawns: Temporary bounce mushrooms appear (traversal aid)
- Visual: Massive glowing spore clouds, bioluminescence
- Audio: Pulsing organic sounds
- Strategic value: Disorenting but creates shortcuts via mushrooms

---

**Crystal Caverns Weather (Underground)**

**Stable Conditions (Baseline)**
- Occurrence: 70%
- Effects: No weather (underground isolation)
- Visual: Steady crystal glow
- Strategic value: Predictable, safe from surface weather

**Crystal Resonance Storm**
- Occurrence: 20%
- Duration: 3 minutes
- Visibility: 150 studs (enhanced by crystal flashing)
- Movement: 100% speed
- Stamina drain: 100%
- Shockwaves: Every 15 seconds, 50-stud radius pulses from large crystals (2% HP + knockback)
- Crystal shattering: Random small crystals explode (sharp fragments deal 5% HP)
- Visual: Crystals pulsing rapidly, light beams crossing
- Audio: High-pitched ringing, shattering sounds
- Strategic value: Dodge shockwaves, use timing between pulses

**Earthquake**
- Occurrence: 8%
- Duration: 90 seconds
- Visibility: 100 studs (dust clouds)
- Movement: 80% speed (shaking ground)
- Stamina drain: 140%
- Falling crystals: Random stalactites drop (3-second warning, 10% HP)
- Cave-ins: Random passages temporarily blocked (alt routes needed)
- Visual: Shaking screen, falling debris
- Audio: Rumbling, crashing rocks
- Strategic value: High danger, must stay mobile

**Magical Flux (Rare)**
- Occurrence: 2%
- Duration: 5 minutes
- Visibility: 200 studs (crystals emit intense light)
- Movement: 110% speed (levitation effect)
- Stamina drain: 50% (magical energy)
- Gem/Psychic pets: +40% damage bonus
- Teleport crystals: Activate more frequently (30-second cooldown instead of 5 minutes)
- Visual: Rainbow crystal light, floating particles, gravity anomalies
- Audio: Magical chimes, ethereal tones
- Strategic value: Highly beneficial, enhanced mobility and damage

---

**Volcanic Rift Weather Pool**

**Ash Fall (Baseline)**
- Occurrence: 50%
- Effects: As described in biome section
- Visibility: 120 studs
- Heat damage: 2% HP per second (baseline)
- Visual: Constant ash particles, grey atmosphere
- Strategic value: Standard difficulty

**Lava Rain**
- Occurrence: 25%
- Duration: 2 minutes
- Visibility: 100 studs (smoky)
- Movement: 100% speed
- Heat damage: 3% HP per second (increased)
- Lava droplets: Random small lava drops from sky (5% HP if hit, 1-second warning glow)
- Cover required: Must use obsidian outcrops or caves
- Visual: Glowing orange drops falling, sizzling impacts
- Audio: Splattering, hissing
- Strategic value: Must constantly dodge or use cover

**Pyroclastic Surge**
- Occurrence: 15%
- Duration: 90 seconds
- Visibility: 40 studs (ash cloud)
- Movement: 60% speed (heavy ash)
- Heat damage: 5% HP per second (extreme)
- Fast-moving cloud: Rolls across biome in one direction (must outrun or find shelter)
- Shelter: Caves provide complete protection
- Visual: Massive rolling ash cloud, orange glow
- Audio: Roaring, approaching doom sound
- Strategic value: Life-threatening, must reach shelter or die

**Magma Eruption**
- Occurrence: 8%
- Duration: 3 minutes
- Visibility: 80 studs (smoke)
- Movement: 90% speed
- Heat damage: 2% (baseline)
- Lava geysers: 10+ geysers erupt across biome (5-second warning rumble, 20% HP + knockback)
- Lava rivers: Temporary lava flows create new hazards (block paths)
- Visual: Multiple eruption columns, flowing lava
- Audio: Explosive eruptions, rumbling
- Strategic value: Extreme navigation challenge, paths change

**Inferno (Rare - Extreme)**
- Occurrence: 2% (triggered manually by mythic pet spawn)
- Duration: Until mythic pet defeated or despawns
- Visibility: 60 studs (fire haze)
- Movement: 80% speed (oppressive heat)
- Heat damage: 10% HP per second (instant death without fire resistance gear)
- Fire tornadoes: 3-5 tornadoes roam biome (instant death on contact)
- Sky: Blood-red, black smoke, lightning
- Fire pets: +50% damage bonus
- Visual: Apocalyptic hellscape, everything on fire
- Audio: Roaring flames, explosions
- Strategic value: Only end-game players with max fire resistance can survive

---

**Void Chasm Weather (Reality-Warped)**

**Stable Void (Baseline)**
- Occurrence: 60%
- Effects: As biome baseline (sanity drain, reality tears)
- Visual: Purple-black void, star field
- Strategic value: Standard void difficulty

**Reality Storm**
- Occurrence: 25%
- Duration: 3 minutes
- Visibility: Variable (80-150 studs, shifts randomly)
- Movement: Variable (50-150% speed, reality warps)
- Sanity drain: 2% per 10 seconds (doubled)
- Gravity shifts: Random direction changes every 30 seconds
- Teleportation: 15% chance per minute to random location in biome
- Visual: Reality fractures, distorted geometry, color inversions
- Audio: Reversed sounds, echoing voices
- Strategic value: Disorienting, unpredictable

**Void Collapse**
- Occurrence: 10%
- Duration: 90 seconds
- Visibility: 30 studs (darkness encroaching)
- Movement: 70% speed (reality dragging)
- Sanity drain: 5% per 10 seconds (rapid)
- Platform disappearance: Islands vanish temporarily (20% chance per platform every 15 seconds)
- Must keep moving: Standing still causes void fall (instant death)
- Visual: Darkness consuming world, platforms fading
- Audio: Void whispers, reality tearing
- Strategic value: Survival mode, must keep moving

**Cosmic Awakening (Rare)**
- Occurrence: 5% (mostly triggers with mythic spawn)
- Duration: 5 minutes
- Visibility: 200 studs (cosmic light)
- Movement: 120% speed (floating)
- Sanity: No drain (cosmic enlightenment)
- Void pets: +60% damage bonus
- Cosmic altars: All activate (free legendary spawns)
- Visual: Brilliant cosmic nebula, stars, dimensional rifts
- Audio: Celestial choir, harmonious tones
- Strategic value: Extremely beneficial, exploit cosmic power

---

**Storm Peaks Weather Pool**

**Thunderstorm (Baseline)**
- Occurrence: 60%
- Effects: As biome baseline (constant storm)
- Visual: Dark clouds, rain, lightning
- Strategic value: Standard difficulty

**Hurricane Winds**
- Occurrence: 20%
- Duration: 5 minutes
- Visibility: 80 studs (rain sheets)
- Movement: Variable (wind pushes 50-150% speed depending on direction)
- Stamina drain: 180%
- Wind direction: Changes every 60 seconds (must adapt)
- Platform edges: Easier to get blown off (danger)
- Visual: Horizontal rain, bending trees, debris flying
- Audio: Screaming wind
- Strategic value: Navigation extremely difficult

**Lightning Storm (Intense)**
- Occurrence: 15%
- Duration: 2 minutes
- Visibility: 100 studs
- Movement: 100% speed
- Lightning frequency: 3x normal (strikes every 10 seconds instead of 30)
- Chain lightning: Strikes jump to nearby players/pets (30-stud radius)
- Electric pets: +40% damage bonus
- Visual: Constant lightning flashes, sky lit up
- Audio: Continuous thunder
- Strategic value: Must use lightning rods or constantly dodge

**Tornado**
- Occurrence: 4%
- Duration: 3 minutes
- Tornado count: 1-2 tornadoes roam biome
- Tornado movement: 20 studs/second (faster than sprint)
- Tornado effect: Sucks players in from 50-stud radius, launches into air (fall damage 50% HP)
- Visibility: 120 studs (except inside tornado: 0 studs)
- Visual: Massive funnel cloud, debris swirling
- Audio: Roaring vortex
- Strategic value: Must track tornado position, extreme danger

**Eye of the Storm (Rare)**
- Occurrence: 1%
- Duration: 10 minutes
- Visibility: 250 studs (crystal clear)
- Movement: 100% speed
- Stamina drain: 50% (calm air)
- Weather: Complete calm (no rain, lightning, wind)
- Storm pets: +50% spawn rate (attracted to calm)
- Visual: Blue sky in circular area, storm wall surrounding
- Audio: Peaceful silence, distant thunder
- Strategic value: Perfect hunting conditions, highly sought after

---

**Abyssal Depths Weather (Underwater)**

**Calm Waters (Baseline)**
- Occurrence: 60%
- Effects: As biome baseline (oxygen system, pressure)
- Visual: Clear water, gentle currents
- Strategic value: Standard difficulty

**Strong Currents**
- Occurrence: 25%
- Duration: 3 minutes
- Visibility: 120 studs (churning water)
- Movement: Variable (50-150% speed with/against current)
- Oxygen drain: 1.5x faster (harder breathing)
- Current direction: One direction across biome, changes every minute
- Visual: Fast-flowing water, debris carried by current
- Audio: Rushing water
- Strategic value: Use current for speed or fight against it

**Deep Pressure Zone**
- Occurrence: 10%
- Duration: 90 seconds
- Visibility: 80 studs (murky)
- Movement: 70% speed (pressure resistance)
- Pressure damage: 10% HP per second (doubled from baseline)
- Oxygen drain: 2x faster
- Pressure suits: Essential for survival
- Visual: Darkness, heavy water distortion
- Audio: Creaking, groaning (pressure sounds)
- Strategic value: Extremely dangerous, must have gear

**Bioluminescent Bloom**
- Occurrence: 4%
- Duration: 5 minutes
- Visibility: 200 studs (glowing plankton)
- Movement: 100% speed
- Oxygen: No drain (plankton produces oxygen)
- Pressure: No damage (bloom cushions pressure)
- Water pets: +50% spawn rate
- Visual: Glowing blue-green plankton clouds, ethereal beauty
- Audio: Soft humming
- Strategic value: Incredibly beneficial, temporary safe zone

**Leviathan Call (Rare - Extreme)**
- Occurrence: 1% (triggered by mythic pet presence)
- Duration: Until mythic defeated
- Visibility: 40 studs (churning darkness)
- Movement: 60% speed (turbulence)
- Oxygen drain: 3x faster (panic)
- Shockwaves: Periodic pressure waves (10% HP, stun 2 seconds)
- Visual: Dark water, massive shadow passing, tremors
- Audio: Deep whale-like calls, ominous drones
- Strategic value: Boss-encounter weather, extreme threat

### 8.4 Weather Mitigation Systems

**Gear-Based Protection**

**Weather-Resistant Armor Sets**
- **Raincoat**: Reduces rain stamina drain by 50%, crafted from plant fiber + leather
- **Insulated Parka**: Reduces frostbite damage by 50%, crafted from fur + thick fabric
- **Heat-Resistant Suit**: Reduces heat damage by 50%, crafted from asbestos materials + fire essence
- **Gas Mask**: Negates poison/acid gas damage, crafted from leather + charcoal filters (consumable: 10-minute duration)
- **Pressure Suit**: Reduces underwater pressure damage by 75%, crafted from reinforced plates + rubber seals

**Cost-Benefit Trade-off**
- Weather gear occupies armor slot (lose combat stats)
- Must pre-craft before expedition (inventory management)
- Durability system applies (gear degrades)
- Strategic choice: Combat power vs environmental protection

**Pet Abilities (Weather Adaptation)**

**Fire Pets**
- Ability: "Warming Aura" - Reduces frostbite/cold damage by 75% in 20-stud radius
- Use case: Tundra exploration without heavy gear

**Ice Pets**
- Ability: "Cooling Aura" - Reduces heat damage by 75% in 20-stud radius
- Use case: Volcanic/Badlands exploration

**Electric Pets**
- Ability: "Lightning Rod" - Attracts lightning strikes to pet (absorbs damage harmlessly)
- Use case: Storm Peaks protection

**Water Pets**
- Ability: "Oxygen Bubble" - Provides breathable air underwater (negates oxygen system)
- Use case: Abyssal Depths extended dives

**Rock/Ground Pets**
- Ability: "Earthquake Resistance" - Immune to knockback/falling crystals
- Use case: Crystal Caverns/earthquake events

**Consumable Items**

**Weather-Specific Consumables**
- **Warming Potion**: +50% frostbite resistance for 5 minutes (3x Herbs + Fire essence)
- **Cooling Elixir**: +50% heat resistance for 5 minutes (3x Ice shards + Water)
- **Clarity Tonic**: Negates fog/visibility reduction for 3 minutes (5x Crystal dust)
- **Grounding Stone**: Attracts lightning away from player for 2 minutes (1x Copper ore + Electric essence)
- **Oxygen Tank**: +30 seconds air underwater, stackable (2x Metal + Compressed air)

**Cost-Benefit**
- Consumables expensive to craft (rare materials)
- Limited duration (must time usage)
- Inventory slots consumed
- Trade-off: Spend resources on weather protection vs combat items

**Shelter System**

**Natural Shelters**
- Caves: Complete protection from all weather (rain, heat, cold, lightning)
- Overhangs: 75% protection (blocks rain/ash/lava but not wind/cold)
- Dense foliage: 50% protection (blocks light rain/snow only)
- Underwater caves: Air pockets + pressure protection

**Craftable Shelters**
- **Temporary Tent**: Player can deploy portable shelter (blocks rain/wind for 5 minutes, then despawns)
  - Crafting: 10x Fabric + 5x Wood poles
  - Weight: 3 inventory slots
  - Use case: Emergency weather protection

**Strategic Shelter Use**
- Extreme weather forces shelter-seeking (gameplay rhythm)
- Shelters become PvP choke points (ambush locations)
- Risk: Trapped in shelter while loot opportunities outside
- Balance: Safety vs opportunity cost

### 8.5 Weather Forecasting & Warnings

**Weather Prediction UI**

**Minimap Weather Overlay**
- Current weather icon displayed (rain cloud, snowflake, lightning bolt, etc.)
- Next weather forecast: "Heavy Rain in 3 minutes" (countdown timer)
- Weather severity color-coded:
  - Green: Clear/Light (safe)
  - Yellow: Moderate (caution)
  - Orange: Heavy (danger)
  - Red: Extreme (life-threatening)

**Audio Warnings**

**Pre-Weather Cues** (60 seconds before change)
- Thunder rumbling (before storms)
- Wind picking up (before dust storms/blizzards)
- Temperature drop sound (before cold snap)
- Seismic rumble (before earthquake)
- Character dialogue: "Something's changing..." (generic warning)

**Extreme Weather Sirens** (30 seconds before extreme events)
- Loud warning siren (emergency tone)
- Screen border pulses red
- UI message: "EXTREME WEATHER INCOMING - SEEK SHELTER"
- NPC shouts (if near base hub)

**Environmental Indicators**

**Visual Cues**
- Sky color changes (darkening clouds before storm)
- Wind direction shifts (leaves/debris blowing)
- Animal behavior (birds fleeing before danger)
- Horizon effects (dust wall visible approaching)

**Audio Cues**
- Distant thunder (storms approaching)
- Wind howling (blizzard/dust storm coming)
- Ground rumbling (earthquake warning)
- Silence (eerie calm before extreme weather)

### 8.6 Weather Strategy & Metagame

**Optimal Weather Windows**

**Best Hunting Conditions**
- Clear weather: Maximum visibility, standard combat
- Light weather: Minimal penalties, still productive
- Aurora Storm (Tundra): Beneficial buffs, increased spawns
- Magical Flux (Crystal Caverns): Enhanced mobility and damage
- Bioluminescent Bloom (Abyssal): Safe exploration

**Players actively seek these conditions for efficient farming**

**Worst Conditions (Extract or Shelter)**
- Extreme Sandstorm (Badlands): Near-zero visibility
- Pyroclastic Surge (Volcanic): High lethality
- Void Collapse (Void Chasm): Platform disappearance
- Inferno (Volcanic): Apocalyptic fire
- Leviathan Call (Abyssal): Boss-tier threat

**Players extract or hide during these events**

**Weather-Based Tactics**

**PvP Strategies**
- **Fog ambush**: Use low visibility to surprise enemies
- **Storm cover**: Lightning/weather chaos provides distraction
- **Weather endurance**: Outlast opponents who lack protection gear
- **Shelter camping**: Guard shelter entrances during extreme weather

**PvE Strategies**
- **Weather rotation farming**: Move between biomes based on favorable weather
- **Buff exploitation**: Hunt during beneficial weather for enhanced rewards
- **Resource efficiency**: Extract before extreme weather to avoid consumable waste
- **Pet synergy**: Use weather-adapted pets for specific biome clears

**Seasonal Meta Shifts**
(Future feature: Real-world seasons could influence in-game weather patterns)
- Summer: More heat-based weather (Volcanic/Badlands more active)
- Winter: More cold-based weather (Tundra harsher)
- Spring: More rain-based weather (Forest/Swamp wetter)
- Fall: More fog-based weather (All biomes mistier)

---

## 9. STAMINA & TRAVERSAL MECHANICS

### 9.1 Stamina System Overview

**Core Concept**
Stamina governs sprinting, dodging, climbing, and swimming. Players must strategically manage stamina to escape danger, chase targets, and navigate terrain. Stamina depletion creates vulnerability and forces tactical positioning.

**Stamina Bar**
- **Maximum capacity**: 100 stamina points
- **Regeneration rate**: 10 stamina per second (when not sprinting)
- **Regeneration delay**: 2 seconds after stamina-consuming action
- **Visual**: Blue bar below HP bar
- **Audio**: Heavy breathing when below 25 stamina

### 9.2 Stamina Consumption Actions

**Sprinting**
- **Movement speed**: 24 studs/second (150% of walk speed)
- **Stamina cost**: 5 stamina per second
- **Duration at full stamina**: 20 seconds continuous sprint
- **Depletion effect**: Sprint automatically stops, forced to walk
- **Recovery time**: 10 seconds to full stamina (if standing still)
- **Strategic use**: Escaping combat, chasing fleeing pets, rushing to extraction

**Dodging** (Combat Mechanic)
- **Stamina cost**: 15 stamina per dodge roll
- **Cooldown**: 1 second between dodges
- **Max consecutive dodges**: 6 dodges (90 stamina) before depletion
- **Dodge distance**: 10 studs forward/backward/side
- **Invincibility frames**: 0.3 seconds (brief immunity during roll)
- **Depletion effect**: Cannot dodge, must rely on positioning
- **Strategic use**: Avoiding pet attacks, PvP evasion

**Climbing Steep Terrain**
- **Stamina cost**: 3 stamina per second while climbing
- **Climb speed**: 4 studs/second (25% of walk speed)
- **Duration**: 33 seconds max climb at full stamina
- **Depletion effect**: Player slides down slope, must rest before retry
- **Fall risk**: If stamina reaches 0 mid-climb, player falls (fall damage possible)
- **Strategic use**: Shortcut routes, accessing high-ground vantage points

**Swimming**
- **Stamina cost**: 2 stamina per second while swimming
- **Swim speed**: 8 studs/second (50% of walk speed)
- **Duration**: 50 seconds max swim at full stamina
- **Depletion effect**: Movement speed reduced to 4 studs/second (drowning risk increases)
- **Drowning**: If stamina depleted underwater for 10 seconds, 5% HP per second until death or shore
- **Strategic use**: Crossing rivers, escaping land-based threats

**Power Attacks** (Advanced Combat)
- **Stamina cost**: 20 stamina per heavy attack
- **Damage**: 2x normal attack damage
- **Cooldown**: 3 seconds between power attacks
- **Max consecutive**: 5 power attacks before depletion
- **Depletion effect**: Cannot use power attacks, only light attacks
- **Strategic use**: Burst damage on tough pets, finishing weakened targets

### 9.3 Stamina Recovery Modifiers

**Standing Still**
- Regeneration: 10 stamina/second (baseline)
- Best for: Full recovery during safe moments

**Walking (Not Sprinting)**
- Regeneration: 5 stamina/second (50% rate)
- Best for: Slow recovery while staying mobile

**Crouching**
- Regeneration: 15 stamina/second (150% rate)
- Movement: 8 studs/second (50% walk speed)
- Best for: Stealth + fast recovery

**Sitting (Benches/Campfires)**
- Regeneration: 25 stamina/second (250% rate)
- Movement: Immobile
- Best for: Rapid recovery in safe zones (base hub)

**Consumable: Stamina Potion**
- Effect: Instant +50 stamina
- Cooldown: 60 seconds
- Best for: Emergency escape/combat continuation

**Pet Aura: Energize** (Certain pets provide passive buff)
- Effect: +5 stamina regen per second (150% total)
- Pets: Wind/Flying type pets with "Energize" ability
- Best for: Extended exploration

### 9.4 Environmental Stamina Modifiers

**Terrain Effects**

**Flat Ground**
- Stamina cost: 100% normal (baseline)

**Uphill (Gentle Slope <20°)**
- Stamina cost: 125% (sprint costs 6.25/second instead of 5)

**Uphill (Steep Slope 20-40°)**
- Stamina cost: 150% (sprint costs 7.5/second)

**Downhill**
- Stamina cost: 75% (sprint costs 3.75/second)
- Movement speed: 110% (gravity assist)

**Deep Snow/Mud/Sand**
- Stamina cost: 150% (difficult terrain)
- Movement speed: 80%

**Water (Shallow/Wading)**
- Stamina cost: 130%
- Movement speed: 70%

**Ice (Slippery)**
- Stamina cost: 90% (less friction, easier to move)
- Movement speed: 130% (sliding)
- Control: Reduced turning (overslide mechanic)

**Weather Effects on Stamina**

**Rain**
- Stamina regen: -10% (wet, tired)
- Sprint cost: +10% (slippery)

**Snow**
- Stamina regen: -20% (cold exhaustion)
- Sprint cost: +20% (deep snow)

**Heat (Badlands/Volcanic)**
- Stamina regen: -30% (dehydration)
- Sprint cost: +30% (oppressive heat)

**Cold (Tundra)**
- Stamina regen: -20% (hypothermia)
- Sprint cost: +10% (shivering)

**Poison/Toxic Gas**
- Stamina regen: -50% (labored breathing)
- Sprint cost: +50% (choking)

**Bioluminescent Bloom (Abyssal)**
- Stamina regen: +25% (oxygen-rich)
- Sprint cost: -25% (energizing)

### 9.5 Advanced Movement Mechanics

**Slide (Downhill Mechanic)**
- **Activation**: Sprint downhill on 30°+ slope
- **Speed**: 30 studs/second (200% sprint speed)
- **Stamina**: No cost (momentum-based)
- **Control**: Limited steering (momentum carries forward)
- **Duration**: Until slope ends or player jumps to cancel
- **Risk**: Cannot stop quickly, may overshoot into danger
- **Strategic use**: Fast biome traversal, escape chases, PvP surprise

**Wall Run (Advanced Mobility)**
- **Activation**: Sprint toward wall at 45° angle, jump at wall contact
- **Duration**: 2 seconds or 20 studs horizontal distance
- **Stamina cost**: 20 stamina (one-time cost)
- **Speed**: 20 studs/second (maintains sprint momentum)
- **Requirement**: Vertical surface at least 15 studs tall
- **Strategic use**: Bypass obstacles, reach elevated areas, stylish movement

**Gliding (Storm Peaks Only)**
- **Item required**: Glider (craftable: 10x Fabric + 5x Lightweight frame)
- **Activation**: Jump from height, hold glide button
- **Descent rate**: 2 studs/second downward, 12 studs/second forward
- **Stamina cost**: 1 stamina per second (minimal)
- **Wind interaction**: Updrafts lift player, winds push horizontally
- **Max distance**: ~500 studs from high peak (massive travel distance)
- **Strategic use**: Island-to-island traversal in Storm Peaks, escape tool

**Grappling Hook (Craftable Tool)**
- **Activation**: Aim at grapple point (ledges, branches), fire hook
- **Range**: 50 studs maximum
- **Speed**: 15 studs/second pull
- **Stamina cost**: 15 stamina per grapple
- **Cooldown**: 5 seconds between grapples
- **Strategic use**: Vertical mobility, cliff climbing, chase/escape

**Vine Swinging (Swamp Only)**
- **Activation**: Jump to grab hanging vine
- **Swing arc**: 30-stud arc (pendulum motion)
- **Stamina cost**: 5 stamina per swing
- **Chaining**: Can chain multiple vine swings (Tarzan-style)
- **Release timing**: Must release at apex for maximum distance
- **Strategic use**: Cross poison pools, bypass muddy ground

### 9.6 Stamina Management Strategy

**Optimal Stamina Usage Patterns**

**Exploration Phase (Early Expedition)**
- Walk normally (conserve stamina for emergencies)
- Sprint only when crossing dangerous open areas
- Save 50+ stamina reserve for unexpected combat/escape

**Combat Phase**
- Enter combat with full stamina (rest before engaging)
- Use 2-3 dodges per enemy attack pattern
- Reserve 30 stamina for escape if fight goes wrong

**Escape Phase (Low HP, Fleeing)**
- Sprint continuously until safe distance (burn all stamina if needed)
- Use terrain advantage (downhill slides, vines, grapples)
- Pop stamina potion mid-sprint to extend distance

**Extraction Phase (Final Rush)**
- Sprint entire distance to extraction zone (time-critical)
- Use all stamina, drink potion if necessary
- Accept vulnerability (extraction timer = priority)

**High-Level Play: Stamina Faking**
- Pretend to be out of stamina (bait enemy approach)
- Suddenly sprint/dodge when enemy commits to attack
- PvP mind-game tactic

---

## 10. NAVIGATION & MAP SYSTEMS

### 10.1 Fog of War System

**Core Concept**
The map is initially completely hidden, revealing only as players physically explore. Fog of war resets each expedition, ensuring every run requires fresh exploration and preventing route memorization.

**Fog of War Mechanics**

**Initial State**
- 100% map covered in black fog
- Only base hub visible (500-stud radius circle of revealed terrain)
- Minimap shows player position and immediate surroundings (50-stud radius)
- No biome indicators visible (must discover biomes physically)

**Reveal Radius**
- **Walking/Standing**: 100-stud radius reveals around player
- **Elevated position**: 150-stud radius (high ground advantage)
- **Using telescope item**: 300-stud radius (temporary peek, 30-second cooldown)
- **Pet scouting ability**: Certain Flying pets scout 200 studs ahead for 10 seconds

**Reveal Permanence (Per Expedition)**
- Revealed areas stay uncovered for duration of current expedition
- Minimap fills in with terrain data as explored
- Biome names appear on minimap once discovered
- POIs (chests, dungeons, landmarks) marked once within 50 studs

**Fog of War Reset**
- Completely resets at start of each new expedition
- Previous expedition's map data erased
- Prevents route memorization across multiple runs
- Ensures exploration remains meaningful

**Shared Fog of War (Squad Play)**
- Party members share revealed map data in real-time
- If squadmate explores north, all players' maps update
- Encourages splitting up to cover more ground
- Communication: "I found extraction zone west!"

### 10.2 Minimap System

**Minimap UI**
- **Location**: Top-right corner of screen
- **Size**: 200x200 pixel square
- **Zoom levels**: 3 levels (50/100/200-stud radius toggle)
- **Rotation**: North-locked (does not rotate with player)
- **Transparency**: 80% opaque (can see through to world)

**Minimap Icons**

**Player Indicators**
- **Self**: Blue arrow (points forward direction)
- **Squad members**: Green arrows
- **Other players (PvPvE)**: Red dots (only visible within 100 studs)

**POI Icons**
- **Extraction zones**: Green/Blue/Purple evacuation symbols (tier-coded)
- **Base hub**: White home symbol (always visible)
- **Chests**: Yellow treasure icon (only after discovery)
- **Dungeons**: Purple cave icon (only after discovery)
- **Landmarks**: Orange pillar icon (only after discovery)

**Pet Indicators**
- **Companion pet**: Light blue paw icon (follows player)
- **Legendary spawn**: Golden star icon (appears globally when legendary spawns)
- **Mythic spawn**: Red diamond icon (appears globally when mythic spawns)
- **Regular pets**: Not shown (minimap would be cluttered)

**Biome Color-Coding**
- **Whispering Forest**: Green
- **Scorched Badlands**: Orange
- **Frozen Tundra**: Light blue
- **Toxic Swamp**: Dark green
- **Crystal Caverns**: Purple
- **Volcanic Rift**: Red
- **Void Chasm**: Black-purple gradient
- **Storm Peaks**: Dark blue
- **Abyssal Depths**: Navy blue

**Elevation Indicators**
- **Higher elevation**: Lighter shade of biome color
- **Lower elevation**: Darker shade
- **Cliffs**: Black lines indicating drop-offs
- **Water**: Blue overlay on map

### 10.3 Compass System

**Compass UI**
- **Location**: Top-center of screen
- **Display**: Horizontal bar showing cardinal directions (N, E, S, W)
- **Player facing**: Yellow indicator shows current heading
- **Degree readout**: Optional numerical heading (0-360°)

**Compass Markers**

**Objective Markers**
- **Nearest extraction**: Green arrow with distance ("Extraction 450m NW")
- **Base hub**: White arrow (always present, distance shown)
- **Waypoints**: Player-placed custom markers (up to 3 active)

**Dynamic Markers**
- **Legendary spawn**: Golden arrow ("Inferno Drake 1,200m N")
- **Mythic spawn**: Red arrow ("Eternal Phoenix 2,500m NE")
- **Party member**: Green arrow (shows direction to squadmates beyond minimap range)

**Weather Indicators**
- **Storm approaching**: Yellow hazard icon with direction
- **Extreme weather**: Red hazard icon with countdown timer

### 10.4 Waypoint & Ping System

**Player Waypoints**
- **Placement**: Open map, click location, place custom waypoint
- **Limit**: 3 waypoints maximum active simultaneously
- **Duration**: Permanent until manually removed or expedition ends
- **Icon**: Custom colors (red, blue, yellow) for categorization
- **Use cases**:
  - Mark chest locations for later return
  - Mark dangerous areas to avoid
  - Mark extraction zones discovered
  - Coordinate with squad: "Meet at red waypoint"

**Contextual Pings (Squad Communication)**
- **Activation**: Aim at location/object, press ping button
- **Ping types**:
  - **Enemy ping**: "Enemy spotted here!" (red exclamation mark)
  - **Loot ping**: "Loot here!" (yellow treasure)
  - **Danger ping**: "Danger here!" (orange hazard)
  - **Go ping**: "Go here!" (green arrow)
- **Visibility**: All squad members see ping on screen + minimap
- **Duration**: 10 seconds, then fades
- **Cooldown**: 3 seconds between pings (prevents spam)
- **Audio**: Distinct sound for each ping type

**Verbal Callouts (Auto-Generated)**
When pinging certain objects, character automatically shouts:
- Chest ping: "Chest over here!"
- Enemy ping: "Contact! Enemy spotted!"
- Extraction ping: "Extraction zone here!"
- Danger ping: "Watch out! Danger!"

### 10.5 Full Map View

**Map Screen Access**
- **Button**: Hold M key (PC) or map button (mobile)
- **Screen takeover**: Full-screen map overlay (pauses gameplay in solo, not in multiplayer)
- **Return**: Release button to return to game

**Full Map Features**

**Zoom & Pan**
- **Zoom levels**: 5 levels (from entire map to 50-stud radius detail)
- **Pan**: Click-drag or WASD to move view
- **Center on player**: Button to instantly recenter
- **Quick-travel**: Click biome name to jump view to that biome

**Map Filters (Toggle Layers)**
- **Topography**: Show elevation lines, cliffs, water bodies
- **POIs**: Toggle chest/dungeon/landmark visibility
- **Biomes**: Toggle biome boundary overlays
- **Spawns**: Show approximate pet density heatmap (updated every minute)
- **Weather**: Show current weather per biome
- **Extraction**: Highlight active extraction zones with timers

**Map Legend**
- Sidebar showing all icon meanings
- Color key for biome coding
- Elevation key for height interpretation

**Measurement Tool**
- Click two points to measure distance between them
- Useful for planning routes: "350 studs to extraction"
- Calculates approximate travel time: "~2 minutes at sprint"

### 10.6 Navigation Tools & Items

**Telescope (Craftable)**
- **Crafting**: 5x Glass + 3x Metal tube
- **Function**: Extended fog of war reveal (300-stud radius, 5-second duration)
- **Cooldown**: 30 seconds
- **Use case**: Scout ahead before committing to dangerous area

**Compass Rose (Craftable)**
- **Crafting**: 10x Crystal + 5x Magnetic ore
- **Function**: Shows direction to nearest uncollected rare+ chest
- **Range**: 1,000 studs
- **Cooldown**: 60 seconds
- **Use case**: Loot hunting optimization

**Map Fragment (Rare Drop)**
- **Source**: Random drop from elite/boss pets
- **Function**: Reveals random 500x500-stud map section permanently
- **Tradeable**: Can share with squadmates
- **Use case**: Instant exploration boost

**Flare Gun (Craftable)**
- **Crafting**: 5x Gunpowder + 3x Signal flare
- **Function**: Shoots flare into sky (visible from entire map for 30 seconds)
- **Use cases**:
  - Mark your position for squadmates
  - Request help (universal distress signal)
  - Coordinate extraction meetup point
- **Cooldown**: 5 minutes
- **PvP risk**: Reveals your position to enemies

**Scout Drone (Premium/Rare Item)**
- **Function**: Deploy drone that flies 200 studs in aimed direction
- **Reveals**: Everything along path (instant fog of war removal)
- **Duration**: 10-second flight time
- **Cooldown**: 3 minutes
- **Consumable**: 5 uses per item, then depleted
- **Use case**: Safe scouting of extremely dangerous areas

---

## 11. DUNGEON SYSTEM ARCHITECTURE

### 11.1 Dungeon Overview

**Core Concept**
Dungeons are procedurally generated instanced caves within biomes that offer high-risk, high-reward challenges. Each dungeon features randomized layouts, escalating encounters, environmental puzzles, and guaranteed boss fights. Dungeons provide concentrated pet hunting, exclusive materials, and blueprint drops unavailable in the open world.

**Design Philosophy**
- **High commitment**: 10-15 minute clear time (significant investment)
- **Escalating difficulty**: Rooms progressively harder toward boss
- **Guaranteed rewards**: Boss always drops quality loot
- **Instance isolation**: Solo/squad only (no other players can enter your dungeon)
- **No respawn**: Death in dungeon = standard permadeath rules
- **Strategic choice**: "Do I risk dungeon dive or keep surface farming?"

**Dungeon Count per Expedition**
- Starter biome (Forest): 2 dungeons
- Mid-tier biomes: 2-3 dungeons each (8-12 total)
- High-tier biomes: 1-2 dungeons each (4-8 total)
- Total dungeons per map: 14-22 dungeons

### 11.2 Dungeon Generation System

**Generation Phase (Part of Map Generation)**

**Phase 1: Entrance Placement**
- Algorithm places dungeon entrances during POI population phase
- Placement rules (from Part 2):
  - Minimum 800 studs from biome edge
  - Minimum 500 studs from other dungeon entrances
  - Never in transition zones
  - Positioned away from direct paths (requires exploration)
  - Flat terrain requirement

**Phase 2: Template Selection**
- Each biome has 3-5 pre-built dungeon templates (room layouts)
- Algorithm randomly selects one template per dungeon entrance
- Templates vary in:
  - Room count (5-10 rooms)
  - Path complexity (linear, branching, looping)
  - Environmental hazard density
  - Boss arena design

**Example Templates:**

**Linear Dungeon (Simplest)**
```
[Entrance] → [Room 1] → [Room 2] → [Room 3] → [Boss Arena]
- 5 rooms total
- Straightforward progression
- No backtracking required
- Best for new players
```

**Branching Dungeon (Medium)**
```
                    → [Room 3A] →
[Entrance] → [Room 1] → [Room 2]              → [Room 5] → [Boss Arena]
                    → [Room 3B] →
- 7 rooms total
- Two parallel paths converge
- Optional exploration (side rooms have extra loot)
- Requires decision-making
```

**Looping Dungeon (Complex)**
```
[Entrance] → [Room 1] → [Room 2] → [Room 3]
                ↓                      ↑
            [Room 5] ← [Room 4] ←─────┘
                ↓
          [Boss Arena]
- 6 rooms total + boss
- Can loop back to earlier rooms
- Multiple paths to same destination
- Easy to get lost (navigation challenge)
```

**Phase 3: Room Randomization**
Within each template room, procedural generation randomizes:
- **Enemy spawn positions**: 8-12 spawn points per room, randomized selection
- **Chest locations**: 0-2 chests per room, random positions
- **Trap placements**: Pressure plates, spike walls, etc. (position varies)
- **Environmental hazards**: Lava pools, poison vents, falling stalactites (density varies)
- **Puzzle elements**: Lever positions, crystal sequences, etc.

**Phase 4: Difficulty Scaling**
- Room 1: Easy (1-2 common pets, level = biome minimum)
- Room 2-3: Medium (2-3 uncommon pets, level = biome average)
- Room 4-5: Hard (3-4 rare pets, level = biome maximum)
- Boss Arena: Very Hard (1 boss pet, 2-3 adds, level = biome max +5)

**Difficulty modifiers based on biome tier:**
- Starter biome: -10 levels from formula
- Mid-tier biome: Formula as-is
- High-tier biome: +10 levels to formula

### 11.3 Biome-Specific Dungeon Types

**Whispering Forest: Mossy Cavern**

**Theme**: Ancient underground grotto overgrown with vegetation

**Visual Identity**
- Walls: Moss-covered stone, tree roots hanging from ceiling
- Ground: Dirt floor, mushroom patches, shallow water puddles
- Lighting: Soft green glow from bioluminescent moss
- Atmosphere: Humid, earthy smell (implied), dripping water sounds

**Room Count**: 5-7 rooms

**Environmental Hazards**
- **Poison spores**: Mushroom patches release spores (1% HP/sec in cloud)
- **Root snares**: Hidden roots trip players (2-second stun, 5% HP)
- **Collapsing ceiling**: Weak ceiling sections drop dirt (3-second warning, 8% HP)
- Hazard density: Low (beginner-friendly)

**Enemy Composition**
- Common: Forest Wolves, Vine Serpents, Giant Beetles (Nature/Bug types)
- Uncommon: Treant Guardians, Moss Elementals
- Rare: Ancient Stag (optional mini-boss in side room)

**Puzzle Mechanic**: Sunlight Redirection
- Some rooms have mirrors and light beams
- Redirect light beam to moss-covered door to open
- Simple 1-2 mirror puzzles (tutorial difficulty)

**Boss: Ancient Tree Spirit**
- Level: 10 (starter dungeon)
- Stars: 2-star
- Type: Nature
- HP: 2,000
- Mechanics:
  - Summons Vine Snare roots (ground AoE, 2-second windup)
  - Healing Pulse (restores 10% HP every 30 seconds, can be interrupted)
  - Thorn Barrage (ranged attack, fires 5 thorns in spread pattern)
- Arena: Circular room with large tree in center, roots provide cover
- Drops: Uncommon materials (80%), Rare materials (20%), Forest Pet Egg (15% chance)

---

**Scorched Badlands: Lava Tubes**

**Theme**: Volcanic cave system with flowing lava rivers

**Visual Identity**
- Walls: Blackened rock, glowing fissures
- Ground: Obsidian, lava rivers cutting through rooms
- Lighting: Orange-red glow from lava, heat distortion
- Atmosphere: Oppressive heat, rumbling sounds

**Room Count**: 8-10 rooms

**Environmental Hazards**
- **Lava rivers**: Instant death if player falls in (no swimming)
- **Lava geysers**: Erupt from floor (5-second warning glow, 15% HP + knockback)
- **Heat zones**: Areas near lava deal 2% HP/sec (must use rocks for cover)
- **Collapsing bridges**: Lava-stone bridges crack after 5 seconds standing (fall to death)
- Hazard density: High (dangerous environment)

**Enemy Composition**
- Common: Magma Slugs, Fire Imps, Lava Hounds (Fire/Rock types)
- Uncommon: Obsidian Golems, Ember Drakes
- Rare: Lava Titan (optional elite in hidden room)

**Puzzle Mechanic**: Pressure Plate Bridges
- Lava rivers block progress
- Pressure plates raise obsidian platforms from lava (temporary bridges)
- Must weigh down plates with rocks while crossing
- Platforming challenge (requires timing)

**Boss: Magma Drake**
- Level: 25 (mid-tier dungeon)
- Stars: 3-star
- Type: Fire/Dragon
- HP: 5,000
- Mechanics:
  - Fire Breath (cone AoE, 20% HP + burn DoT 2%/sec for 5 seconds)
  - Lava Pool Summon (creates 50-stud lava pool, lasts 30 seconds)
  - Enrage at 30% HP (attack speed +50%, movement speed +25%)
  - Wing Buffet (knockback attack, throws players toward lava)
- Arena: Large circular room with lava river around perimeter, obsidian islands
- Drops: Rare materials (60%), Epic materials (30%), Legendary fire essence (10%), Fire Pet Egg (20% chance)

---

**Frozen Tundra: Glacial Cavern**

**Theme**: Ice-carved cave system with frozen waterfalls

**Visual Identity**
- Walls: Crystalline ice, frozen rock
- Ground: Slippery ice sheets, snow drifts
- Lighting: Blue-white from glowing ice crystals
- Atmosphere: Bitter cold, echoing ice cracks

**Room Count**: 7-9 rooms

**Environmental Hazards**
- **Slippery ice**: Movement becomes sliding (reduced control, 130% speed)
- **Falling icicles**: Stalactite icicles drop (3-second warning, 12% HP + slow debuff)
- **Frozen floors**: Thin ice cracks under weight (10 seconds standing, plunge into freezing water)
- **Freezing water**: If player falls through ice, takes 10% HP/sec until exit (5 seconds max survival)
- **Frostbite zones**: Areas without ice crystals deal 3% HP/sec (existing tundra mechanic amplified)
- Hazard density: Medium-High

**Enemy Composition**
- Common: Ice Wolves, Frost Sprites, Frozen Zombies (Ice/Undead types)
- Uncommon: Yeti Guardians, Crystal Elementals
- Rare: Permafrost Colossus (optional elite)

**Puzzle Mechanic**: Light Refraction Through Ice
- Ice crystals refract light beams
- Must position crystals to redirect beam to frozen door (melts ice lock)
- 3-4 crystal puzzles of increasing complexity
- Requires spatial reasoning

**Boss: Frost Wyrm**
- Level: 28 (mid-tier dungeon)
- Stars: 3-star
- Type: Ice/Dragon
- HP: 5,500
- Mechanics:
  - Ice Breath (cone AoE, 18% HP + freeze debuff 3 seconds)
  - Blizzard Summon (arena-wide snowstorm, 80-stud visibility, lasts 20 seconds)
  - Ice Shard Rain (random falling shards across arena, 8% HP per hit)
  - Frozen Armor (at 50% HP, gains shield absorbing 1,000 damage, must break)
- Arena: Large icy cavern with frozen pillars (line-of-sight blockers)
- Drops: Rare materials (60%), Epic materials (30%), Legendary ice shard (10%), Ice Pet Egg (20% chance)

---

**Toxic Swamp: Fungal Grotto**

**Theme**: Organic cave overgrown with giant mushrooms and toxic fungi

**Visual Identity**
- Walls: Pulsating organic tissue, fungal growths
- Ground: Squishy mushroom carpet, poison pools
- Lighting: Bioluminescent green-purple from fungi
- Atmosphere: Spore-filled air, squishy sounds

**Room Count**: 6-8 rooms

**Environmental Hazards**
- **Poison pools**: 3% HP/sec, DoT continues 5 seconds after leaving
- **Spore clouds**: Periodic eruptions from mushrooms (blocks vision 50 studs, 2% HP/sec)
- **Hallucination spores**: Rare spore type causes fake enemies to appear (waste time/resources)
- **Collapsing mushroom platforms**: Large mushrooms used as bridges collapse after 10 seconds
- **Acid drips**: Ceiling drips acid randomly (2-second puddle warning, 10% HP)
- Hazard density: Very High (most hazardous dungeon type)

**Enemy Composition**
- Common: Toxic Toads, Spore Zombies, Poison Beetles (Poison/Bug types)
- Uncommon: Fungal Horrors, Swamp Hags
- Rare: Myconid King (optional elite in deepest chamber)

**Puzzle Mechanic**: Mushroom Growth Sequence
- Must activate mushrooms in correct order (color sequence)
- Correct sequence causes giant mushroom to grow (creates bridge or opens path)
- Wrong sequence triggers spore explosion (10% HP damage)
- Trial-and-error with consequences

**Boss: Plague Spore Lord**
- Level: 32 (mid-high tier dungeon)
- Stars: 3-star
- Type: Poison/Dark
- HP: 6,000
- Mechanics:
  - Spore Burst (arena-wide DoT cloud, 3%/sec for 10 seconds, must use antidote)
  - Summon Spore Minions (spawns 4 weak adds every 30 seconds)
  - Hallucination Wave (all players see fake boss clones, must find real one)
  - Regeneration (heals 2% HP/sec when standing in poison pools)
- Arena: Circular room with poison pools, mushroom platforms
- Drops: Rare materials (50%), Epic materials (40%), Legendary spore sample (10%), Poison Pet Egg (25% chance)

---

**Crystal Caverns: Geode Chamber**

**Theme**: Massive geode interior with reflective crystal surfaces

**Visual Identity**
- Walls: Multi-colored crystal formations (purple, blue, green)
- Ground: Smooth crystal floor, reflective surfaces
- Lighting: Internal crystal glow (rainbow spectrum)
- Atmosphere: Magical hum, crystal resonance sounds

**Room Count**: 5-7 rooms

**Environmental Hazards**
- **Crystal resonance**: Large crystals emit shockwaves (2% HP + knockback every 20 seconds)
- **Falling crystals**: Stalactite crystals drop (3-second warning, 10% HP + bleed DoT)
- **Light beams**: Focused crystal beams burn (1-second sweep warning, 15% HP linear damage)
- **Teleport traps**: Step on wrong crystal, teleport to random room (backtrack penalty)
- Hazard density: Medium

**Enemy Composition**
- Common: Crystal Spiders, Gem Sprites, Stone Golems (Rock/Gem types)
- Uncommon: Prism Guardians, Geode Beetles
- Rare: Diamond Elemental (optional elite guarding rare mining node)

**Puzzle Mechanic**: Crystal Light Sequences
- Must activate crystals in correct sequence (Simon Says style)
- Crystals light up pattern, player must repeat
- Correct sequence unlocks door, wrong sequence damages player (5% HP)
- Increases complexity each room (3 crystals → 5 crystals → 7 crystals)

**Boss: Gemstone Colossus**
- Level: 30 (mid-high tier dungeon)
- Stars: 3-star
- Type: Rock/Gem
- HP: 6,500
- Mechanics:
  - Crystal Spike Eruption (ground AoE, 3-second warning, 20% HP + slow)
  - Prism Beam (fires refracted beam bouncing off arena crystals, unpredictable)
  - Gem Shield (immune to damage, must break 4 crystals around arena to dispel)
  - Enrage Phase (at 25% HP, all attacks faster, arena crystals pulse damage)
- Arena: Octagonal room with 8 large crystals on walls (can be used as cover)
- Drops: Rare materials (50%), Epic materials (40%), Legendary gem (10%), Gem Pet Egg (25% chance)

---

**Volcanic Rift: Magma Core**

**Theme**: Deep inside active volcano, magma everywhere

**Visual Identity**
- Walls: Obsidian and cooling lava
- Ground: Floating obsidian platforms over lava ocean
- Lighting: Intense red-orange from lava
- Atmosphere: Extreme heat, constant rumbling

**Room Count**: 4-6 rooms (smaller dungeon, higher difficulty)

**Environmental Hazards**
- **Lava ocean**: Instant death (entire floor is lava)
- **Platform sinking**: Platforms sink into lava after 20 seconds standing (must keep moving)
- **Lava waves**: Periodic waves crash over platforms (5-second warning rumble, 25% HP)
- **Pyroclastic clouds**: Fast-moving gas walls (instant death if hit, 10-second warning)
- **Eruption columns**: Lava pillars shoot up randomly (3-second warning, 30% HP + launch)
- Hazard density: Extreme (most dangerous dungeon)

**Enemy Composition**
- Rare: Lava Elementals, Magma Drakes, Obsidian Titans (all elite-tier)
- Epic: Inferno Demons, Volcanic Wyrms
- Legendary: Fire Lord (optional secret boss in hidden chamber)

**Puzzle Mechanic**: Obsidian Platform Creation
- Must activate lava vents to create temporary obsidian platforms
- Platforms cool and become solid for 30 seconds, then re-melt
- Must time activation and crossing perfectly
- One wrong step = instant death

**Boss: Inferno Dragon King**
- Level: 55 (legendary tier dungeon)
- Stars: 5-star
- Type: Fire/Dragon (Legendary)
- HP: 15,000
- Mechanics:
  - Meteor Shower (arena-wide falling meteors, 15% HP per hit, must dodge 10+ meteors)
  - Lava Wave (summons lava tsunami, must jump to highest platform)
  - Flight Phase (flies above arena, bombards with fireballs for 30 seconds)
  - Inferno Rage (at 30% HP, entire arena ignites, 5% HP/sec, must defeat quickly)
  - Tail Sweep (close-range AoE, 20% HP + knockback toward lava)
- Arena: Massive chamber with multiple elevation platforms, lava ocean below
- Drops: Epic materials (40%), Legendary materials (50%), Mythic fire essence (10%), Guaranteed Legendary Fire Pet Egg

---

**Void Chasm: Abyssal Rift**

**Theme**: Non-euclidean geometry, reality-warped dimension

**Visual Identity**
- Walls: Impossible geometry, surfaces that shouldn't connect
- Ground: Floating platforms in endless void
- Lighting: Purple-black void energy, distant stars
- Atmosphere: Reality distortion, unsettling whispers

**Room Count**: 3-5 rooms (fewer rooms, extreme complexity)

**Environmental Hazards**
- **Void falls**: Falling off platform = instant death (no respawn)
- **Reality tears**: Random teleportation (10% chance per 30 seconds)
- **Gravity shifts**: "Down" changes direction periodically (disorienting)
- **Madness zones**: Sanity drains 2% per second (hallucinations at low sanity)
- **Paradox doors**: Doors lead to impossible locations (can loop infinitely if wrong)
- Hazard density: Extreme (psychological + physical danger)

**Enemy Composition**
- Rare: Void Wraiths, Reality Horrors, Shadow Demons (Dark/Psychic types)
- Epic: Eldritch Terrors, Void Stalkers
- Legendary: Void God Fragment (optional secret encounter)

**Puzzle Mechanic**: Non-Euclidean Navigation
- Rooms connect in impossible ways (door leads back to same room from different angle)
- Must find "true path" through reality (specific sequence of doors)
- Wrong doors loop infinitely or teleport to start
- Requires trial-and-error or deciphering cryptic rune hints

**Boss: Void Leviathan**
- Level: 58 (legendary tier dungeon)
- Stars: 5-star
- Type: Dark/Void (Legendary)
- HP: 18,000
- Mechanics:
  - Void Rift (opens portal, sucks in players from 100 studs, instant death if pulled in)
  - Reality Fracture (arena splits into 4 floating sections, must jump between)
  - Tentacle Slam (melee AoE, 25% HP + confusion debuff 5 seconds)
  - Sanity Drain Aura (constant 3% sanity drain, must defeat before insanity)
  - Phase Shift (becomes invulnerable, must damage "true" form in alternate dimension)
- Arena: Massive void space with floating island, platform disappears in phases
- Drops: Epic materials (30%), Legendary materials (60%), Mythic void essence (10%), Guaranteed Legendary Void Pet Egg

---

**Storm Peaks: Thunderspire Temple**

**Theme**: Ancient sky temple with exposed platforms, perpetual storm

**Visual Identity**
- Walls: Ancient stone ruins, weathered by wind
- Ground: Stone platforms open to sky, no ceiling
- Lighting: Lightning flashes, dark storm clouds
- Atmosphere: Howling wind, torrential rain, thunder crashes

**Room Count**: 5-7 rooms

**Environmental Hazards**
- **Lightning strikes**: Random 100-stud radius bolts (5-second warning, 20% HP + stun 2 seconds)
- **Wind gusts**: Periodically push players toward edges (must lean into wind)
- **Rain slickness**: Ground slippery, easier to slide off platforms
- **Platform gaps**: Must jump between platforms (miss = fall death)
- **Chain lightning**: Boss room mechanic (lightning chains between players, 15% HP per jump)
- Hazard density: High

**Enemy Composition**
- Rare: Storm Eagles, Lightning Elementals, Thunder Drakes (Electric/Flying types)
- Epic: Tempest Gargoyles, Sky Titans
- Legendary: Storm Avatar (optional secret boss)

**Puzzle Mechanic**: Lightning Rod Placement
- Must place metal rods to attract lightning away from player
- Lightning must hit specific targets to charge door mechanisms
- Incorrect placement causes player to be struck (20% HP)
- Requires understanding of lightning attraction (tallest object in area)

**Boss: Thunder God Phoenix**
- Level: 60 (legendary tier dungeon)
- Stars: 5-star
- Type: Electric/Flying (Legendary)
- HP: 20,000
- Mechanics:
  - Storm Call (summons lightning storm, 10 strikes across arena over 10 seconds)
  - Thunder Dive (flies high, divebombs player, 30% HP AoE impact)
  - Chain Lightning (bounces between all players in arena, 15% HP each)
  - Tornado Summon (creates tornado in arena, sucks in players, 10% HP/sec)
  - Resurrection (at 0% HP, revives once at 50% HP if not captured quickly)
- Arena: Large open-air platform with lightning rod pillars (can be used strategically)
- Drops: Epic materials (30%), Legendary materials (60%), Mythic storm feather (10%), Guaranteed Legendary Storm Pet Egg

---

**Abyssal Depths: Sunken Citadel**

**Theme**: Ancient underwater ruins with air-locked chambers

**Visual Identity**
- Walls: Barnacle-covered stone, coral growths
- Ground: Sandy floors, kelp forests
- Lighting: Dim bioluminescence, darkness at depth
- Atmosphere: Underwater pressure, muffled sounds

**Room Count**: 6-8 rooms

**Environmental Hazards**
- **Flooded chambers**: Some rooms fully underwater (oxygen system active)
- **Pressure zones**: Deep areas deal 10% HP/sec pressure damage
- **Strong currents**: Push players toward hazards (must swim against)
- **Drowning risk**: If oxygen depletes, 5% HP/sec until death
- **Collapsing walls**: Pressure breaches flood dry rooms (30-second warning)
- Hazard density: Very High (oxygen management critical)

**Enemy Composition**
- Rare: Deep Sea Horrors, Abyssal Eels, Kraken Spawn (Water/Dark types)
- Epic: Leviathan Juveniles, Coral Golems
- Legendary: Ancient Leviathan (final boss)

**Puzzle Mechanic**: Pressure Valve System
- Must activate pressure valves to drain flooded rooms
- Valves located in separate underwater chambers (risky to reach)
- Correct valve sequence drains rooms, wrong sequence floods more areas
- Time pressure: Oxygen limits how long player can search for valves

**Boss: Leviathan of the Deep**
- Level: 57 (legendary tier dungeon)
- Stars: 5-star
- Type: Water/Abyss (Legendary)
- HP: 17,000
- Mechanics:
  - Tidal Wave (arena-wide water surge, 25% HP + knockback)
  - Whirlpool (creates suction vortex in center, pulls players in, 10% HP/sec inside)
  - Pressure Crush (targets one player, 5% HP/sec for 10 seconds, must break line-of-sight)
  - Summon Adds (spawns 3 Deep Sea Eels every 45 seconds)
  - Oxygen Drain (passively reduces oxygen timer 2x faster during fight)
- Arena: Partially flooded chamber with air pockets at top, underwater section at bottom
- Drops: Epic materials (30%), Legendary materials (60%), Mythic abyssal pearl (10%), Guaranteed Legendary Water Pet Egg

### 11.4 Dungeon Rewards System

**Guaranteed Loot Structure**

**Per Room Rewards**
- **Common rooms** (first 2 rooms):
  - 0-1 basic chests (common materials 80%, uncommon 20%)
  - Enemy drops (standard pet defeat loot)
- **Uncommon rooms** (middle rooms):
  - 1 uncommon chest (uncommon 60%, rare 40%)
  - Elite enemy drops (better material drop rates)
- **Rare rooms** (final pre-boss rooms):
  - 1 rare chest (rare 70%, epic 30%)
  - Mini-boss optional (guaranteed rare drop)

**Boss Defeat Rewards**
- **Material drops**: Based on biome and difficulty tier
  - Starter dungeon: Uncommon 80%, Rare 20%
  - Mid-tier dungeon: Rare 60%, Epic 30%, Legendary 10%
  - High-tier dungeon: Epic 40%, Legendary 50%, Mythic 10%
- **Pet Egg drops**: 15-25% chance (varies by dungeon)
  - Egg corresponds to boss type (Fire boss = Fire egg)
  - Eggs hatch into guaranteed 2-3 star pets
- **Blueprint drops**: 20% chance for exclusive gear/item recipe
  - Dungeon-specific items (can't get in open world)
  - Examples: Boss-themed weapons, armor sets, special consumables
- **Currency**: 200-500 Expedition Currency (scales with difficulty)

**First Clear Bonus** (Per Expedition)
- First time player clears specific dungeon in current expedition: +50% loot
- Encourages dungeon variety (not farming same dungeon repeatedly)
- Applies to all dungeon types separately (can get bonus for each unique dungeon)

**No-Death Bonus**
- If squad clears dungeon without anyone dying: +25% loot
- Risk vs reward: Encourages careful play
- Stacks with first clear bonus (can get 75% total bonus)

### 11.5 Dungeon Difficulty Modifiers

**Solo vs Squad Scaling**

**Solo Play**
- Enemy HP: 100% (baseline)
- Enemy damage: 100%
- Enemy count: 100%
- Boss HP: 100%
- Intended difficulty: Hard (designed for skilled solo players)

**Duo (2 Players)**
- Enemy HP: 150%
- Enemy damage: 110%
- Enemy count: 120% (1-2 extra enemies per room)
- Boss HP: 175%
- Intended difficulty: Medium (easier than solo, teamwork advantageous)

**Squad (3-4 Players)**
- Enemy HP: 200%
- Enemy damage: 120%
- Enemy count: 150% (3-4 extra enemies per room)
- Boss HP: 250%
- Boss adds: Spawns more adds during fight
- Intended difficulty: Medium (balanced for coordination)

**Scaling Rationale**
- More players = more firepower, but enemies tankier
- Encourages cooperation (revives, buffs, coordinated attacks)
- Prevents trivializing content with large groups

**Hard Mode (Optional Toggle)**
- Available at dungeon entrance: "Enter Hard Mode?"
- Effects:
  - Enemy HP: +50%
  - Enemy damage: +30%
  - Boss mechanics: Additional attack patterns
  - Loot quality: +50% better drops
  - Prestige: Achievement unlocked for hard mode clears
- Intended for experienced players seeking challenge

---

## 12. TRAPPED CHEST SYSTEM

### 12.1 Trapped Chest Overview

**Core Concept**
Trapped chests are high-risk, high-reward loot sources scattered across the open world. When opened, they spawn guardian pets that must be defeated before loot can be collected. Guardian difficulty scales with chest rarity, creating dynamic combat encounters at loot locations.

**Trapped Chest Types**
- Common trapped: 50% of common chests (abundant)
- Uncommon trapped: 80% of uncommon chests (majority)
- Rare trapped: 100% of rare chests (always trapped)
- Legendary trapped: 100% of legendary chests (always + puzzle lock)

### 12.2 Trapped Chest Mechanics

**Discovery Phase**
- Player approaches chest (within 10 studs)
- Visual indicator: Faint red glow around chest edges (subtle warning)
- If player has "Trap Detection" skill (craftable item): "⚠️ Trapped Chest Detected"
- Otherwise: No warning until opened

**Opening Trigger**
1. Player interacts with chest (press E)
2. 3-second animation: Chest lid slowly opens
3. Audio: Ominous click sound (mechanical trap sprung)
4. Warning: "TRAP ACTIVATED" UI message
5. 2-second delay before guardian spawns (player can react)

**Guardian Spawn**
- Guardian pet materializes 10 studs from chest (in front of player)
- Spawn animation: 1-second materialization effect (telegraphed)
- Guardian immediately aggros to player who opened chest
- Guardian tethered to chest (cannot chase beyond 50-stud radius)

**Combat Phase**
- Player must defeat guardian to access loot
- Guardian difficulty scales with chest rarity (see Section 12.3)
- If player flees beyond 50-stud tether: Guardian despawns after 30 seconds, chest re-locks
- If player dies: Standard permadeath rules, chest remains trapped for other players

**Loot Collection**
- Upon guardian defeat: Chest glows green, lid fully opens
- Player can now safely loot chest (no additional traps)
- Loot quality unaffected by guardian defeat (guaranteed chest contents)
- Guardian also drops additional loot (bonus reward for defeating trap)

### 12.3 Guardian Pet Specifications

**Common Trapped Chest Guardian**

**Guardian Stats**
- Pet tier: 1-star (basic)
- Level: Biome minimum level
- HP: 500 (low health, quick fight)
- Damage: 5% player HP per attack (manageable)
- Attack speed: 1 attack per 2 seconds
- AI behavior: Aggressive, no special mechanics

**Guardian Types per Biome**
- Forest: Corrupted Wolf, Angry Boar
- Badlands: Sand Scorpion, Fire Lizard
- Tundra: Ice Fox, Frost Spider
- Swamp: Toxic Toad, Plague Rat

**Defeat Time**: 30-60 seconds (solo player, average skill)

**Bonus Drops**
- Common materials: 2-3 units
- Expedition Currency: 10-20
- Pet capture possible: 5% chance (guardian can be captured if weakened)

---

**Uncommon Trapped Chest Guardian**

**Guardian Stats**
- Pet tier: 2-star (elite)
- Level: Biome average level
- HP: 1,500 (moderate durability)
- Damage: 8% player HP per attack
- Attack speed: 1 attack per 1.5 seconds
- AI behavior: Aggressive with one special mechanic

**Special Mechanics (One per Guardian)**
- **Enrage**: At 30% HP, attack speed +50% for 10 seconds
- **Shield**: Periodically gains damage shield (absorbs 300 damage)
- **Summon**: Spawns 2 weak adds (200 HP each) once during fight
- **Teleport**: Blinks behind player every 20 seconds

**Guardian Types per Biome**
- Forest: Treant Guardian, Venomous Serpent
- Badlands: Lava Hound, Stone Elemental
- Tundra: Yeti Cub, Crystal Golem
- Swamp: Fungal Horror, Swamp Hag

**Defeat Time**: 1-2 minutes (solo player, average skill)

**Bonus Drops**
- Uncommon materials: 3-5 units
- Rare materials: 1-2 units (30% chance)
- Expedition Currency: 30-50
- Pet capture possible: 10% chance

---

**Rare Trapped Chest Guardian**

**Guardian Stats**
- Pet tier: 3-star (boss-tier)
- Level: Biome maximum level
- HP: 3,500 (high durability)
- Damage: 12% player HP per attack
- Attack speed: 1 attack per 1 second
- AI behavior: Aggressive with two special mechanics

**Special Mechanics (Two per Guardian)**
- **AoE Attack**: Every 30 seconds, 50-stud radius AoE (15% HP)
- **Life Steal**: Heals 5% HP per attack landed
- **Berserk**: At 50% and 25% HP, gains attack speed +100% for 5 seconds
- **Regeneration**: Heals 2% HP per second when not taking damage for 5 seconds

**Guardian Types per Biome**
- Forest: Ancient Treant, Alpha Wolf
- Badlands: Magma Drake, Sand Wurm
- Tundra: Frost Giant, Blizzard Drake
- Swamp: Myconid King, Plague Beast

**Defeat Time**: 2-3 minutes (solo player, skilled)

**Bonus Drops**
- Rare materials: 5-7 units
- Epic materials: 2-3 units (50% chance)
- Expedition Currency: 75-100
- Pet capture possible: 15% chance

---

**Legendary Trapped Chest Guardian**

**Guardian Stats**
- Pet tier: 4-star (mini-boss)
- Level: Biome maximum +5 levels
- HP: 8,000 (very high durability)
- Damage: 18% player HP per attack
- Attack speed: 1 attack per 0.8 seconds
- AI behavior: Highly aggressive with three special mechanics

**Special Mechanics (Three per Guardian)**
- **Ultimate Attack**: Every 60 seconds, massive AoE (30% HP, 100-stud radius, 5-second windup)
- **Phase Shift**: At 60% and 30% HP, becomes invulnerable for 5 seconds, heals 10% HP
- **Enrage Aura**: Below 30% HP, all nearby enemies gain +30% damage buff
- **Summon Elite Adds**: Spawns 2 elite adds (1,000 HP each) at 50% HP

**Guardian Types per Biome**
- High-tier biomes only (Volcanic, Void, Storm, Abyssal)
- Volcanic: Inferno Guardian, Obsidian Titan
- Void: Reality Horror, Void Stalker
- Storm: Thunder Lord, Tempest Elemental
- Abyssal: Kraken Spawn, Deep Terror

**Defeat Time**: 4-6 minutes (solo player, highly skilled + good gear)

**Environmental Puzzle Requirement**
- Legendary chests have additional lock: Environmental puzzle must be solved first
- Puzzle types:
  - **Pressure Plate Sequence**: Stand on 4 plates in correct order
  - **Crystal Alignment**: Rotate crystals to form light beam path to chest
  - **Rune Translation**: Decipher rune inscription to speak password
  - **Elemental Lock**: Use specific pet element attack to unlock (e.g., Fire attack on ice lock)
- Solving puzzle: 1-2 minutes (adds to total time investment)
- Wrong solution: No penalty (can retry), but wastes time

**Bonus Drops**
- Epic materials: 8-10 units
- Legendary materials: 5-7 units (100% guaranteed)
- Mythic materials: 1-2 units (25% chance)
- Expedition Currency: 200-300
- Rare blueprint: 30% chance (exclusive legendary gear recipes)
- Pet capture possible: 20% chance (high-value pet)

### 12.4 Trapped Chest Strategy

**Risk Assessment**
- Players must decide: "Is this chest worth the fight?"
- Considerations:
  - Current HP/resources (can I survive guardian?)
  - Time investment (is loot worth 5-minute fight?)
  - Nearby threats (will other pets/players interfere?)
  - Inventory space (can I carry more loot?)

**Trap Avoidance Items**

**Trap Detection Lens** (Craftable)
- Crafting: 5x Crystal + 3x Wire
- Function: Reveals trapped chests from 30 studs (red glow visible)
- Duration: 10 minutes per use
- Allows informed decision: Avoid trapped chests or prepare for fight

**Guardian Pacifier** (Rare Consumable)
- Crafting: 10x Rare materials + 5x Magic essence (expensive)
- Function: Disarms trapped chest (guardian doesn't spawn)
- One-time use per chest
- Strategic value: Use on legendary chests to avoid 5-minute fight

**Trap Disarm Kit** (Premium/Rare Drop)
- Function: 50% chance to disarm trap (success = no guardian, failure = spawns anyway)
- Uses: 3 per kit, then depleted
- Risk/reward: Gamble on disarming vs guaranteed fight

**Squad Tactics**

**Optimal Squad Approach**
1. Tank player opens chest (draws guardian aggro)
2. Damage dealers focus guardian from range
3. Healer/support keeps tank alive
4. Coordination key: Guardian defeated in 50% less time

**Solo Player Tips**
- Clear area of other threats before opening chest
- Open chest with full HP/stamina/companion pet ready
- Use terrain (kite guardian around rocks/trees)
- Save escape stamina (in case fight goes wrong)

---

## 13. LANDMARK & POI SYSTEM

### 13.1 Landmark Overview

**Purpose**
Landmarks are massive, visually distinctive structures scattered across biomes that serve as navigation aids, meeting points, and minor loot locations. Unlike chests/dungeons, landmarks are purely supportive features that enhance world exploration.

**Landmark Characteristics**
- **Size**: 200-300 studs tall (visible from distance)
- **Unique**: One design per biome (instantly recognizable)
- **Static**: Always same position within biome template (not randomized per seed)
- **Discoverable**: Appears on minimap once within 100-stud range
- **Interactive**: Minor loot/NPC at base (optional)

### 13.2 Biome Landmark Designs

**Whispering Forest: The Ancient Tree**

**Visual Design**
- Massive oak tree, 300 studs tall
- Trunk diameter: 50 studs
- Glowing green runes carved into bark
- Bioluminescent moss covering roots
- Birds circling treetop

**Interactive Element**
- Tree hollow at base: Small shrine with 1 uncommon chest
- NPC: Forest Druid (provides lore about forest history)
- Quest: "Collect 10 Forest Herbs" (reward: Forest Pet Egg)

**Navigation Value**
- Visible from forest edges (500+ studs)
- Central landmark in forest biome
- Players use as meetup point: "Meet at Ancient Tree"

---

**Scorched Badlands: The Rock Spire**

**Visual Design**
- Towering sandstone formation, 250 studs tall
- Natural arch at base (30-stud opening)
- Wind-eroded patterns on surface
- Heat shimmer around peak
- Vultures perched on ledges

**Interactive Element**
- Cave at base: 1 rare chest (trapped)
- Climbing challenge: Can scale spire exterior to reach peak (3-minute climb)
- Peak reward: Panoramic view, reveals 300-stud radius fog of war

**Navigation Value**
- Visible across entire Badlands
- Direction indicator: If you see spire, you're facing north (consistent orientation)

---

**Frozen Tundra: The Ice Pillar**

**Visual Design**
- Crystalline ice obelisk, 280 studs tall
- Glowing blue from within
- Aurora ribbons spiral around pillar
- Frozen waterfall base
- Snow drifts at foundation

**Interactive Element**
- Ice cave entrance at base: Leads to small treasure room (2 uncommon chests)
- Puzzle: Melt ice door with fire attack to enter
- Seasonal event: During winter real-world season, pillar grants temporary cold immunity buff (50-stud radius)

**Navigation Value**
- Glows at night (beacon visible 800+ studs)
- Acts as compass: Always northeast of tundra center

---

**Toxic Swamp: The Dead Titan**

**Visual Design**
- Massive skeletal remains (ancient beast), 200 studs long
- Ribcage forms natural cave structure
- Glowing toxic fungi growing on bones
- Poison fog seeping from skull
- Scavenger creatures lurking nearby

**Interactive Element**
- Skull interior: Safe zone (no poison damage inside)
- Loot: 3 uncommon chests hidden in ribcage
- NPC: Necromancer (sells rare poison recipes)

**Navigation Value**
- Most recognizable structure in swamp
- Skull faces south (orientation guide)

---

**Crystal Caverns: The Prismatic Spire**

**Visual Design**
- Enormous crystal formation, 220 studs tall
- Rainbow light refracts through facets
- Hums with magical energy
- Smaller crystals orbit around spire (levitating)
- Pulses in rhythm (visual heartbeat)

**Interactive Element**
- Crystal altar at base: Sacrifice materials for random crystal pet spawn
- Light puzzle: Redirect spire's light beams to unlock hidden chamber (epic loot)
- Mining nodes: Rare crystal deposits around base (one-time harvest)

**Navigation Value**
- Visible throughout entire cavern network
- Light beams point toward nearest dungeon entrance

---

**Volcanic Rift: The Lava Geyser**

**Visual Design**
- Massive lava fountain, erupts 250 studs high
- Erupts every 5 minutes (predictable timing)
- Forms lava lake around base (100-stud radius)
- Obsidian formations surrounding
- Intense heat distortion

**Interactive Element**
- Timed challenge: Cross lava lake during non-eruption window (high risk)
- Reward: Legendary chest on central island (guaranteed fire materials)
- Danger: If caught in eruption, 50% HP instant damage

**Navigation Value**
- Eruption visible across entire biome (smoke plume)
- Sound of eruption audible 1,000+ studs away

---

**Void Chasm: The Floating Ruins**

**Visual Design**
- Ancient temple fragments suspended in void, 200 studs tall combined
- Stone pieces orbit each other (impossible physics)
- Reality distortion around structures
- Cosmic energy arcs between fragments
- Whispers emanate from ruins

**Interactive Element**
- Platforming challenge: Jump between fragments to reach top
- Reward: Cosmic altar (spawn legendary void pet)
- Sanity drain: Increased 2x while inside ruins

**Navigation Value**
- Only stable structure in void (reference point)
- Fragments align to point toward nearest extraction zone

---

**Storm Peaks: The Lightning Rod Tower**

**Visual Design**
- Ancient metal tower, 300 studs tall
- Constantly struck by lightning (every 10 seconds)
- Storm clouds swirl around peak
- Crackling electrical discharge
- Ozone smell (implied)

**Interactive Element**
- Power core at base: Harness lightning strike to charge batteries (craft electric items)
- Danger: Standing near tower during strike = chain lightning (20% HP)
- Timing challenge: Must enter between strikes

**Navigation Value**
- Lightning flash visible entire biome (night beacon)
- Always center of storm activity

---

**Abyssal Depths: The Leviathan Skeleton**

**Visual Design**
- Colossal sea serpent skeleton, 400 studs long
- Spine forms natural tunnel structure
- Bioluminescent coral growing on bones
- Schools of fish swimming through ribs
- Eerie beauty

**Interactive Element**
- Skull chamber: Air pocket safe zone (oxygen refill)
- Loot: 5 uncommon chests scattered in ribcage
- Environmental hazard: Strong current flows through tunnel (fast travel but risky)

**Navigation Value**
- Largest structure in abyss
- Spine points toward surface (up direction guide)

### 13.3 Minor POI Types

**Campsites** (Scattered Throughout Map)

**Characteristics**
- Small campfire with log benches
- Abandoned by previous explorers
- 20-stud safe radius (no pet spawns within)
- Stamina regen +50% when sitting

**Loot**
- 1 common chest (always present)
- Crafting materials scattered around (5-10 units)

**Frequency**: 1 per 500 studs (relatively common)

---

**Shrines** (Rare Spawn)

**Characteristics**
- Ancient stone altar with offerings
- Glowing magical aura
- Inscription in old language (lore flavor)

**Interaction**
- Sacrifice materials: Gain temporary buff (15 minutes)
  - Strength Shrine: +20% damage
  - Protection Shrine: +20% defense
  - Speed Shrine: +20% movement speed
  - Fortune Shrine: +20% loot quality
- Cost: 5 rare materials per buff

**Frequency**: 1-2 per biome (rare find)

---

**Abandoned Structures** (Scattered)

**Types**
- Old watchtowers (forest, badlands)
- Frozen cabins (tundra)
- Ruined temples (all biomes)
- Shipwrecks (abyssal)

**Loot**
- 1-2 uncommon chests
- Environmental storytelling (skeletons, notes, etc.)
- Sometimes spawn trapped chests (ambush inside building)

**Frequency**: 2-3 per biome

---

**Resource Nodes** (Gatherable POIs)

**Types**
- Herb patches: Gather herbs for crafting (respawn after 5 minutes)
- Ore deposits: Mining for metal/gems (one-time harvest per expedition)
- Berry bushes: Food source for consumables (respawn after 3 minutes)
- Water sources: Fill water bottles (unlimited uses)

**Frequency**: 10-15 per biome (common, support crafting needs)

---

# ETERNAL WILDS - WORLD & MAP SYSTEM DESIGN DOCUMENT
## Part 7 of 10: World Events, Pet Spawns & Technical Implementation

---

## 14. WORLD EVENT SYSTEM

### 14.1 World Event Overview

**Core Concept**
World Events are rare, server-wide occurrences that create dramatic moments shared by all players in an expedition. Events alter gameplay temporarily, spawn unique rewards, and create memorable "you had to be there" experiences. Events trigger at specific times or under certain conditions, ensuring unpredictability and excitement.

**Event Characteristics**
- **Server-wide**: All players in expedition experience event simultaneously
- **Rare**: 1-3 events per expedition maximum (not every run has events)
- **Impactful**: Significantly alters gameplay during duration
- **Rewarding**: Exclusive loot, unique pet spawns, or major buffs
- **Announced**: Global notification warns all players before/during event
- **Time-limited**: 3-10 minute duration (creates urgency)

**Event Trigger Types**
- **Scheduled**: Triggers at specific expedition timestamps (e.g., 20:00 mark)
- **Conditional**: Triggers when conditions met (e.g., 50% of pets extinct)
- **Random**: 10-20% chance per eligible time window
- **Player-activated**: Rare items can manually trigger certain events

### 14.2 Event Catalog

**Event Type 1: Blood Moon Rising**

**Theme**: Crimson moon empowers dark creatures

**Trigger Conditions**
- Time: 35:00 mark (night phase begins at 35:00)
- Condition: Must be nighttime (won't trigger during day)
- Frequency: 30% chance when eligible

**Announcement**
```
Global Message: "🌙 BLOOD MOON RISING 🌙"
"Dark energies surge through the Wilds..."
Audio: Ominous choir chant
Visual: Sky turns blood-red, moon glows crimson
Duration: 5 minutes
```

**Gameplay Effects**
- **Visual changes**:
  - Sky crimson-tinted
  - Moon 3x larger, red glow
  - Shadows deeper, darker
  - Ambient light reduced to 20%
  
- **Pet spawn changes**:
  - Dark/Ghost type spawn rate +200%
  - All pets gain "Bloodlust" buff (+30% damage, +20% speed)
  - Nocturnal pets become hyper-aggressive (aggro range +50%)
  - Special "Blood Variant" pets spawn (red-tinted versions with better loot)
  
- **Environmental hazards**:
  - Shadows deal 1% HP/sec damage (must stay in light)
  - Light sources 50% less effective (torches dimmer)
  
- **Player buffs**:
  - Dark/Ghost pets in player's roster gain +50% damage
  - Capturing Dark/Ghost pets during event: 2x capture rate
  
- **Exclusive spawns**:
  - Blood Wolf Alpha (3-star elite, guaranteed epic drops)
  - Crimson Specter (4-star legendary, exclusive blood materials)
  - 5-10 Blood Variants spawn across map

**Strategic Implications**
- High-risk, high-reward: Fight empowered enemies for better loot
- Dark pet collectors prioritize hunting during event
- Light-dependent players extract or hide (can't navigate safely)
- PvP intensifies (reduced visibility, chaotic combat)

**Event End**
- Moon returns to normal color
- Blood Variants despawn (must defeat before timer ends)
- Bloodlust buff fades from all pets
- Global message: "The Blood Moon wanes..."

---

**Event Type 2: Meteor Shower**

**Theme**: Cosmic meteors crash into map, creating loot craters

**Trigger Conditions**
- Time: 15:00 - 30:00 window (mid-expedition)
- Condition: Clear weather required (won't trigger during storms)
- Frequency: 25% chance when eligible

**Announcement**
```
Global Message: "☄️ METEOR SHOWER INCOMING ☄️"
"Seek shelter or claim the fallen stars!"
Audio: Rumbling from sky
Visual: Meteors visible falling from atmosphere
Duration: 3 minutes
```

**Gameplay Effects**
- **Meteor impacts**:
  - 10-15 meteors fall across map (random locations)
  - 5-second warning: Sky glows orange where meteor will land
  - Impact: 100-stud radius explosion (30% HP to anyone in radius)
  - Impact creates crater (20-stud diameter)
  
- **Crater loot**:
  - Each crater contains meteor fragment (rare material)
  - Small crater: 1 uncommon chest + meteor fragment
  - Large crater: 1 rare chest + 3 meteor fragments + chance for cosmic pet egg
  - Craters remain for entire expedition (can revisit)
  
- **Environmental effects**:
  - Dust clouds reduce visibility 50 studs around craters (3 minutes)
  - Craters glow with cosmic energy (visible from 200 studs)
  - Background music shifts to epic orchestral
  
- **Pet spawns**:
  - Cosmic variants spawn at craters (rock/gem types with starry textures)
  - Stardust Elemental (3-star, spawns at largest crater)
  
- **Strategic movement**:
  - Players must track meteor trajectories (dodge or intercept)
  - Risk: Stand at predicted impact for first loot access (might die)
  - Reward: Guaranteed quality loot if survive

**Strategic Implications**
- High-speed looting: Craters attract all nearby players (PvP hotspots)
- Meteor fragments used for cosmic gear crafting (valuable)
- Risky play: Intentionally tank meteor hit to secure crater (50% HP trade)
- Smart positioning: Predict craters near extraction zones

**Event End**
- No more meteors fall
- Craters remain (permanent for expedition)
- Dust clouds dissipate
- Global message: "The meteor shower has passed..."

---

**Event Type 3: Primal Awakening**

**Theme**: Ancient alpha predators awaken and roam biomes

**Trigger Conditions**
- Time: 25:00 mark (mid-late expedition)
- Condition: At least 3 biomes discovered by any player
- Frequency: 20% chance when eligible

**Announcement**
```
Global Message: "🦁 PRIMAL AWAKENING 🦁"
"Ancient predators stir from their slumber!"
Audio: Deep beast roars across map
Visual: Screen rumble, ground tremors
Duration: 10 minutes
```

**Gameplay Effects**
- **Alpha spawns**:
  - 3-5 Alpha Predators spawn (one per discovered biome)
  - Alpha types match biome (Forest Alpha, Volcanic Alpha, etc.)
  - Stats:
    - 4-star legendary pets
    - HP: 10,000 (mini-boss tier)
    - Damage: 20% HP per attack
    - Speed: 1.5x normal movement
    - Aggro range: 200 studs (very aggressive)
  
- **Roaming behavior**:
  - Alphas patrol their biome in 500-stud circular route
  - Path displayed on minimap (red moving skull icon)
  - Players can track and intercept or avoid
  
- **Pack buff**:
  - All non-alpha pets within 100 studs of Alpha gain +50% stats
  - Creates dangerous zones around Alphas
  
- **Exclusive drops**:
  - Alpha Essence (mythic material, 1 per Alpha)
  - Alpha Pet Egg (guaranteed 4-star pet, 100% drop rate)
  - Legendary materials (5-10 units)
  - Exclusive Alpha-themed blueprints
  
- **Global hunt**:
  - Kill count displayed: "Alphas Remaining: 3/5"
  - All players contribute to hunt
  - Bonus reward if all Alphas defeated before event ends

**Strategic Implications**
- Coordinated hunts: Squads call out Alpha positions to others (PvPvE cooperation)
- High-value targets: Alpha loot worth extreme risk
- Avoidance strategy: Track Alpha paths, stay clear
- Competitive capture: First to weaken Alpha can attempt capture (PvP over capture)

**Event End (Two Possible Outcomes)**

**Outcome A: Alphas Survive**
- Alphas despawn at 10-minute mark
- Global message: "The Alphas return to slumber..."
- No bonus reward

**Outcome B: All Alphas Defeated**
- Global message: "🏆 ALL ALPHAS DEFEATED 🏆"
- Bonus: All players receive 500 currency + rare crafting material package
- Achievement unlocked: "Alpha Hunters"
- Encourages server-wide cooperation

---

**Event Type 4: Reality Fracture** (Void Chasm Only)

**Theme**: Reality tears open, Void creatures invade other biomes

**Trigger Conditions**
- Time: 40:00 mark (late expedition)
- Condition: Void Chasm must be discovered by at least one player
- Frequency: 15% chance when eligible

**Announcement**
```
Global Message: "💀 REALITY FRACTURE 💀"
"The Void bleeds into the Wilds!"
Audio: Reality-tearing sound (distorted screech)
Visual: Purple rifts open across map
Duration: 5 minutes
```

**Gameplay Effects**
- **Void rifts**:
  - 8-12 purple portals spawn across non-Void biomes
  - Each rift: 30-stud radius portal on ground
  - Void creatures emerge from rifts every 30 seconds
  
- **Void invasion**:
  - Void Wraiths spawn from rifts (Dark/Void type, 2-3 star)
  - Wraiths attack players on sight (extremely aggressive)
  - Wraiths don't drop normal loot, drop void shards instead
  
- **Sanity effect**:
  - Players within 100 studs of rift lose 1% sanity per second
  - Low sanity causes hallucinations (fake enemies appear)
  
- **Rift sealing**:
  - Players can seal rifts by defeating 5 Void Wraiths near rift
  - Sealed rift drops rare chest (guaranteed void materials)
  - Sealed rifts stop spawning wraiths
  
- **Reality distortion**:
  - Gravity flickers (occasional low-gravity jumps)
  - Colors invert periodically (disorienting)
  - Compass spins randomly (navigation harder)

**Strategic Implications**
- Rift hunting: Proactive players seal rifts for rewards
- Avoidance: Casual players stay far from rifts (too dangerous)
- Void material farming: Best opportunity to get void-exclusive materials outside Void Chasm
- Sanity management: Must have sanity potions or risk madness

**Event End**
- All rifts close simultaneously
- Remaining Void Wraiths despawn
- Reality stabilizes (effects end)
- Global message: "Reality stabilizes..."
- Bonus: Players who sealed 3+ rifts get achievement "Rift Sealer"

---

**Event Type 5: Elemental Convergence**

**Theme**: All elemental energies surge, creating hybrid pets

**Trigger Conditions**
- Time: 30:00 mark (mid-late expedition)
- Condition: At least 4 different biomes discovered
- Frequency: 20% chance when eligible

**Announcement**
```
Global Message: "🌟 ELEMENTAL CONVERGENCE 🌟"
"The elements merge into new forms!"
Audio: Harmonious elemental sounds (fire crackling + water flowing + wind + earth rumble)
Visual: Rainbow aura across map
Duration: 7 minutes
```

**Gameplay Effects**
- **Hybrid pet spawns**:
  - Fusion pets spawn across all biomes
  - Examples:
    - Fire-Water fusion (Steam Elemental)
    - Ice-Electric fusion (Thunderstorm Wisp)
    - Nature-Rock fusion (Living Boulder)
    - Poison-Fire fusion (Toxic Inferno)
  - Hybrid pets have dual-type resistances and attacks
  
- **Elemental zones**:
  - Random 100-stud radius zones gain elemental properties
  - Fire zone: 2% HP/sec heat damage
  - Ice zone: Movement speed -20%
  - Electric zone: Random lightning strikes
  - Nature zone: HP regen +5%/sec (beneficial!)
  
- **Capture bonus**:
  - All pet capture rates +25% during event
  - Hybrid pets only spawn during this event (exclusive)
  - Hybrid pet eggs worth 5x normal eggs
  
- **Crafting boost**:
  - Elemental crafting stations at landmarks activate
  - Can craft fusion gear (requires materials from 2+ elements)
  - Fusion gear has dual-element properties

**Strategic Implications**
- Hybrid collectors prioritize hunting (won't spawn again until next Convergence event)
- Elemental zones create tactical positioning (use beneficial zones)
- Crafting opportunity: Limited-time fusion recipes
- PvE focus: Most players ignore PvP to hunt hybrids

**Event End**
- Elemental zones dissipate
- Hybrid pets despawn if not captured/defeated (30-second warning)
- Global message: "The elements separate..."
- Uncaptured hybrid pets leave behind elemental essence (consolation prize)

---

**Event Type 6: Mythic Manifestation**

**Theme**: Guaranteed mythic pet spawns in random biome

**Trigger Conditions**
- Time: 35:00 - 45:00 window (late expedition)
- Condition: No mythic pets currently active on map
- Frequency: 10% chance (rarest event)

**Announcement**
```
Global Message: "⚡ MYTHIC MANIFESTATION ⚡"
"A Mythic Entity descends upon the [Biome Name]!"
Audio: Epic orchestral crescendo (5 seconds)
Visual: Golden lightning strikes biome center
Duration: Until defeated or 10 minutes
```

**Gameplay Effects**
- **Guaranteed mythic spawn**:
  - One mythic pet spawns at center of random biome
  - Mythic type matches biome (Fire mythic in Volcanic, etc.)
  - Stats:
    - 5-star mythic (strongest tier)
    - HP: 25,000 (world boss tier)
    - Damage: 25% HP per attack
    - Special mechanics: Unique per mythic type
  
- **Global tracking**:
  - Mythic location pinged on all players' minimaps
  - Compass shows direction and distance
  - HP bar visible to all players (shared boss HP)
  
- **Server-wide boss fight**:
  - All players can engage mythic simultaneously
  - Damage shared (everyone contributes)
  - Last player to deal damage gets capture attempt
  - If captured: Capturing player gets mythic, all participants get mythic materials
  - If defeated but not captured: All participants roll for mythic egg (10% chance each)
  
- **Environmental spectacle**:
  - Mythic arrival causes weather change (matches element)
  - Arena effect: 200-stud radius around mythic becomes hazard zone
  - Example: Fire mythic = entire zone becomes lava pools

**Strategic Implications**
- Server rallies: All players rush to biome (massive convergence)
- PvP chaos: Fight over capture attempt rights (last hit)
- Cooperation needed: 25,000 HP requires multiple players (solo nearly impossible)
- Risk vs reward: Die in fight = lose everything, but mythic loot invaluable

**Event End (Two Outcomes)**

**Outcome A: Mythic Defeated & Captured**
- Global message: "[Player Name] has captured the Mythic [Pet Name]!"
- All participants receive mythic material package
- Capturing player becomes server legend

**Outcome B: Mythic Survives 10 Minutes**
- Mythic despawns in dramatic exit (flies away, teleports, etc.)
- Global message: "The Mythic Entity has vanished..."
- No rewards (everyone disappointed)

---

### 14.3 Event Frequency & Balance

**Event Scheduling System**

**Expedition Timeline (45 minutes)**
```
0:00 - 15:00 (Early Phase)
  - No events (players establishing themselves)

15:00 - 30:00 (Mid Phase)
  - Possible events: Meteor Shower (25%), Elemental Convergence (20%)
  - Max 1 event this phase

30:00 - 45:00 (Late Phase)
  - Possible events: Blood Moon (30%), Primal Awakening (20%), Reality Fracture (15%), Mythic Manifestation (10%)
  - Max 2 events this phase (different types)

Total events per expedition: 1-3 (average: 1.5)
```

**Event Cooldowns**
- Same event cannot trigger twice in one expedition
- If Meteor Shower triggers, it's excluded from future rolls
- Ensures variety (players won't see Blood Moon 3 times)

**No-Event Expeditions**
- 30% of expeditions have zero events (bad RNG)
- Ensures events feel special, not routine
- Players appreciate calm expeditions to farm safely

**Event Rarity Tiers**
- Common (25-30% chance): Meteor Shower, Blood Moon, Elemental Convergence
- Uncommon (15-20% chance): Primal Awakening, Reality Fracture
- Rare (10% chance): Mythic Manifestation

### 14.4 Player-Activated Events

**Event Catalyst Items** (Extremely Rare Drops)

**Blood Moon Catalyst**
- Drop source: Blood Variant pets (1% drop during natural Blood Moon)
- Function: Manually trigger Blood Moon event (3-minute duration)
- Strategic use: Activate when squad ready to hunt dark pets
- Trade value: Extremely high (can sell to other players in Laboratory Base)

**Meteor Beacon**
- Drop source: Cosmic pets from meteor craters (2% drop)
- Function: Call down single meteor strike at target location
- Tactical use: Destroy enemy cover, create new crater loot
- Cooldown: 10 minutes after use

**Primal Horn**
- Drop source: Alpha Predators (5% drop)
- Function: Summon one Alpha Predator to current location
- Use case: Farm specific Alpha for materials
- Risk: Might attract other players to your location (PvP)

**Reality Shard**
- Drop source: Sealed rifts during Reality Fracture (10% drop)
- Function: Open personal Void rift (spawns 3 Void Wraiths)
- Use: Farm void materials on-demand
- Risk: Sanity drain still applies

**Elemental Prism**
- Drop source: Hybrid pets during Convergence (3% drop)
- Function: Create temporary elemental zone (player chooses type)
- Duration: 5 minutes, 50-stud radius
- Use: Tactical advantage (place beneficial zone in combat)

**Mythic Essence** (Cannot Manually Trigger Mythic Event)
- Mythic events are special and cannot be forced
- Mythic Essence used for crafting only (mythic-tier gear)
- Preserves rarity and excitement of natural Mythic Manifestation

---

## 15. DYNAMIC PET SPAWN SYSTEM

### 15.1 Pet Spawn Architecture

**Core Concept**
Pet spawns are procedurally distributed across biomes based on density maps, rarity weightings, and elemental affinity. The spawn system ensures appropriate pet distribution while maintaining challenge progression and supporting the extinction mechanic.

**Spawn Authority**
- Server-side spawning (prevents client manipulation)
- Spawn positions calculated during map generation (Phase 3)
- Spawn timers server-authoritative (clients receive spawn notifications)
- Despawn decisions server-controlled (extinction system)

### 15.2 Spawn Density System

**Density Formula per Biome**
```
Base Spawn Density = Biome Area (square studs) / Spawn Spacing

Spawn Spacing by Rarity:
- Common pets: 1 per 200 square studs
- Uncommon pets: 1 per 500 square studs
- Rare pets: 1 per 1,000 square studs
- Epic pets: 1 per 2,000 square studs
- Legendary pets: 1 per 3,000 square studs
- Mythic pets: 1-2 per entire map (special spawn)
```

**Example: Whispering Forest (Starter Biome)**
```
Area: ~7 million square studs (1,500-stud radius ring)

Spawn Calculations:
- Common: 7,000,000 / 200 = 35,000 / 200 = 175 common pets
- Uncommon: 7,000,000 / 500 = 14,000 / 500 = 28 uncommon pets
- Rare: 7,000,000 / 1,000 = 7,000 / 1,000 = 7 rare pets
- Epic: 0 (starter biome doesn't spawn epic)
- Legendary: 0
- Mythic: 0

Total Forest pets: ~210 pets active at expedition start
```

**PvPvE Scaling (20-40 Players)**
- Spawn density increased by 50% for competitive servers
- Example: Forest would have 315 pets instead of 210
- Prevents instant depletion from high player count
- Maintains healthy hunt-to-player ratio

### 15.3 Rarity Distribution by Biome

**Rarity Weighting Tables**

**Starter Biome (Whispering Forest)**
| Rarity | Spawn % | Active Count |
|--------|---------|--------------|
| Common | 70% | 147 pets |
| Uncommon | 25% | 53 pets |
| Rare | 5% | 10 pets |
| Epic | 0% | 0 |
| Legendary | 0% | 0 |
| **Total** | **100%** | **210 pets** |

**Mid-Tier Biome (Scorched Badlands)**
| Rarity | Spawn % | Active Count |
|--------|---------|--------------|
| Common | 40% | 60 pets |
| Uncommon | 35% | 52 pets |
| Rare | 20% | 30 pets |
| Epic | 5% | 8 pets |
| Legendary | 0% | 0 |
| **Total** | **100%** | **150 pets** |

**High-Tier Biome (Volcanic Rift)**
| Rarity | Spawn % | Active Count |
|--------|---------|--------------|
| Common | 0% | 0 |
| Uncommon | 0% | 0 |
| Rare | 30% | 18 pets |
| Epic | 40% | 24 pets |
| Legendary | 25% | 15 pets |
| Mythic | 5% | 3 pets |
| **Total** | **100%** | **60 pets** |

### 15.4 Spawn Point Placement

**Procedural Spawn Point Generation**

**Phase 1: Grid Division**
- Biome area divided into spawn cells (100 x 100 stud squares)
- Each cell assigned spawn probability based on:
  - Terrain type (flat ground = higher probability)
  - Distance from POIs (chests/dungeons get lower spawn density)
  - Proximity to boundaries (edges get 50% spawn rate)

**Phase 2: Spawn Point Distribution**
- Algorithm places spawn points in valid cells
- Spacing rules:
  - Common pets: Minimum 50 studs apart
  - Uncommon pets: Minimum 100 studs apart
  - Rare pets: Minimum 200 studs apart
  - Epic/Legendary: Minimum 300 studs apart
  - Mythic: Minimum 1,000 studs apart (entire map)

**Phase 3: Elemental Affinity Clustering**
- Certain pet types cluster in sub-regions:
  - Fire pets cluster near lava/heat sources
  - Ice pets cluster near frozen areas
  - Water pets cluster near ponds/rivers
  - Nature pets cluster in dense vegetation
- Creates micro-ecosystems within biomes

**Phase 4: Spawn Variation**
- 20% of spawn points marked "roaming" (pet patrols 100-stud radius)
- 5% marked "ambush" (pet hidden, only reveals when player within 20 studs)
- 75% marked "static" (pet stands in place until aggro)

### 15.5 Respawn Mechanics

**Initial Spawn (Expedition Start)**
- All spawn points activated simultaneously at 0:00
- Pets materialize over 30-second window (prevents server lag spike)
- Players who spawn late still see full pet population

**Defeat Respawn Timers**
```
Common pets:
- Respawn timer: 3 minutes after defeat
- Active during: Wave 1 only (0-15 min)
- Disabled: Wave 2+ (extinction begins)

Uncommon pets:
- Respawn timer: 5 minutes after defeat
- Active during: Wave 1-2 (0-30 min)
- Reduced rate Wave 2: 10 minutes
- Disabled: Wave 3+ (30+ min)

Rare pets:
- Respawn timer: 8 minutes after defeat
- Active during: Wave 1-3 (0-45 min)
- Reduced rate Wave 3: No respawn (one-time spawns)

Epic pets:
- Respawn timer: None (one-time spawns)
- Active during: Entire expedition
- Once defeated/captured: Gone permanently

Legendary pets:
- Respawn timer: None (one-time spawns)
- Special rule: New legendaries spawn during Wave 2-3 to replace extinct lower tiers

Mythic pets:
- Respawn timer: None (one-time spawns)
- Unique: Only 1-2 mythic pets per expedition total
```

**Capture vs Defeat Respawn**
- Captured pets do NOT respawn (removed from ecosystem)
- Defeated pets respawn according to timer (ecosystem regenerates)
- Strategic choice: "Do I capture (remove from game) or farm repeatedly?"

### 15.6 Pet Behavior States

**Idle State**
- Pet stands/sits in spawn location
- Plays idle animations (scratching, looking around, etc.)
- Aggro radius: 30 studs (won't attack unless player enters)
- Visual: No threat indicator

**Roaming State** (20% of spawns)
- Pet patrols 100-stud radius circular path from spawn point
- Movement speed: 50% of combat speed
- Aggro radius: 40 studs (slightly more aggressive)
- Returns to spawn point if loses aggro

**Ambush State** (5% of spawns)
- Pet hidden underground/invisible until triggered
- Trigger: Player within 20 studs
- Activation: 1-second warning (ground rumbles, particles)
- Ambush pets deal +20% damage on first attack (surprise bonus)
- After reveal: Behaves as normal aggressive pet

**Aggressive State** (Triggered by Player Proximity)
- Pet locks onto nearest player within aggro radius
- Movement speed: 100% combat speed
- Pursues player for 15 seconds or until 100 studs away (leash range)
- If player escapes leash: Pet returns to spawn point, resets to idle

**Fleeing State** (Triggered at Low HP)
- Activates when pet HP below 20%
- Pet attempts to run away from player (survival instinct)
- Movement speed: 150% (desperate sprint)
- Flee duration: 10 seconds or until player loses sight
- If survives flee: Returns to idle state, HP regenerates slowly (1% per second)
- Strategic: Player must chase fleeing pet to finish/capture

**Pack State** (Special - Group Spawns)
- Some pets spawn in packs (2-4 pets together)
- Pack members within 50 studs of each other
- If one pack member aggros: ALL members aggro simultaneously
- Pack bonus: +15% damage when fighting together
- Strategic: Pulling one pack member pulls entire group (dangerous)

### 15.7 Pet Level Scaling

**Level Calculation Formula**
```
Pet Level = Biome Base Level + Rarity Modifier + Distance Modifier

Biome Base Level:
- Starter biomes: Level 5
- Mid-tier biomes: Level 20
- High-tier biomes: Level 45

Rarity Modifier:
- Common: +0 levels
- Uncommon: +3 levels
- Rare: +5 levels
- Epic: +8 levels
- Legendary: +12 levels
- Mythic: +15 levels

Distance Modifier:
- For every 500 studs from base hub: +1 level
- Example: Pet at 2,500 studs from base = +5 levels
- Encourages deeper exploration (stronger pets further out)
```

**Example Calculations**

**Common Forest Wolf (Starter Biome, Near Base)**
```
Base: 5 (Forest)
Rarity: +0 (Common)
Distance: +1 (500 studs from base)
Final Level: 6
```

**Legendary Inferno Drake (Volcanic Rift, Far Edge)**
```
Base: 45 (Volcanic)
Rarity: +12 (Legendary)
Distance: +10 (5,000 studs from base - maximum distance)
Final Level: 67
```

**Level Cap**: 70 (prevents excessive scaling)

### 15.8 Pet AI Behavior Patterns

**Basic Attack Pattern (Common/Uncommon)**
```
1. Aggro player (enter aggro radius)
2. Chase player (close distance)
3. Basic attack (2-second cooldown)
4. Repeat step 3 until player dead or escaped
```

**Intermediate Pattern (Rare/Epic)**
```
1. Aggro player
2. Chase player
3. Basic attack x2
4. Special ability (unique per pet)
5. Retreat 20 studs (create distance)
6. Repeat from step 2
```

**Advanced Pattern (Legendary/Mythic)**
```
1. Aggro player
2. Assessment phase (circle player for 3 seconds)
3. Opening special ability (telegraphed attack)
4. Combo: Basic attack + Special attack + Basic attack
5. Conditional mechanic (varies per pet):
   - HP threshold (enrage at 50% HP)
   - Summon adds (calls smaller pets)
   - Phase shift (invulnerability, changes tactics)
6. Repeat from step 4 with increased aggression
```

**Pack AI Coordination**
- Alpha member (strongest in pack) leads
- Other members flank player (surround tactic)
- Staggered attacks (one attacks while others reposition)
- Retreat together if alpha dies (morale break)

### 15.9 Super Elusive Pet Spawning

**Super Elusive Definition** (From Part 4)
- Ultra-rare legendary/mythic variants
- 3-5 minute lifespan
- 1-3 spawn per expedition (not guaranteed)
- No map indicators (must physically discover)

**Spawn Mechanics**

**Spawn Timing**
- Only during Wave 2 or Wave 3 (15:00 - 45:00 window)
- Cannot spawn during Wave 1 (too early) or Wave 4 (too late)
- Random spawn chance: 15% per eligible 5-minute interval
  - 15:00 check: 15% chance
  - 20:00 check: 15% chance
  - 25:00 check: 15% chance
  - etc.

**Spawn Location**
- Completely random (any biome, any location within biome)
- No proximity rules (can spawn anywhere, even near players)
- Spawn position logged server-side for tracking

**Discovery Mechanics** (From Part 4)
- No map indicator (minimap shows nothing)
- Visual cue when within 50 studs:
  - Unique particle trail (rainbow sparkles) leading toward pet
  - Faint aura glow visible through terrain (pulsing gold)
- Audio cue when within 50 studs:
  - Ethereal humming (directional, louder when closer)
  - Distinct from normal pet sounds

**Global Announcement** (From Part 4)
```
When Super Elusive spawns:
UI: "⚡ ELUSIVE CREATURE SPOTTED ⚡"
"[Shadow Wraith Dragon] has appeared somewhere in the Wilds!"
"Estimated time remaining: 5 minutes"

Audio: Mysterious chime (creates urgency)
No location given (must search)
```

**Lifespan Countdown**
- 3-5 minute lifespan (randomized per spawn)
- 1-minute warning: Personal notification to players within 100 studs ("The elusive creature is fading...")
- Despawn: Pet vanishes in shimmer effect (no loot if not defeated)

**Super Elusive Types**

**Shadow Wraith Dragon** (Void-type)
- Biomes: Void Chasm, dark areas of other biomes
- Level: 65
- Appearance: Black dragon with purple void energy
- Unique mechanic: Teleports every 15 seconds (hard to pin down)

**Prism Phoenix** (Gem-type)
- Biomes: Crystal Caverns, Storm Peaks
- Level: 63
- Appearance: Rainbow-feathered phoenix
- Unique mechanic: Reflects damage back to attacker (must time attacks carefully)

**Abyssal Leviathan Hatchling** (Water-type)
- Biomes: Abyssal Depths only
- Level: 64
- Appearance: Mini version of Leviathan boss
- Unique mechanic: Creates whirlpools that suck in players

**Infernal Salamander** (Fire-type)
- Biomes: Volcanic Rift, Scorched Badlands
- Level: 66
- Appearance: Glowing red-white salamander
- Unique mechanic: Leaves lava trails that persist (area denial)

**Temporal Stag** (Nature/Psychic-type)
- Biomes: Whispering Forest, Crystal Caverns
- Level: 62
- Appearance: Ethereal deer with clock-like antlers
- Unique mechanic: Rewinds time (heals to full HP once at 10% HP)

---

## 16. PERFORMANCE OPTIMIZATION

### 16.1 Spatial Partitioning System

**Grid-Based Culling**

**Map Division**
- Entire 10,000 x 10,000 map divided into 25 sectors (5x5 grid)
- Each sector: 2,000 x 2,000 studs
- Sector boundaries aligned with biome edges (minimizes cross-sector entities)

**Active Sector Loading**
- Player's current sector: Fully loaded (all entities active)
- Adjacent sectors (8 surrounding): Partially loaded (entities simulated, reduced detail)
- Distant sectors (16+ studs away): Unloaded (entities dormant, no simulation)

**Dynamic Loading Zones**
```
Player position determines loaded sectors:

Example: Player in Sector (2,2)
- Loaded: (2,2) - Full detail
- Partially loaded: (1,1), (1,2), (1,3), (2,1), (2,3), (3,1), (3,2), (3,3)
- Unloaded: All other sectors (17 sectors dormant)

Performance impact:
- Full simulation: 1 sector = ~20% of total map
- Reduces entity count by 80%
- Mobile devices render only 36% of map (massive FPS boost)
```

**Entity Sleep State**
- Unloaded sector entities enter "sleep mode"
  - Position saved
  - AI disabled
  - Physics disabled
  - Render disabled
  - Only core data retained (HP, inventory, timers)
- Wake-up when player enters adjacent sector (0.5-second transition)

### 16.2 Level of Detail (LOD) System

**Distance-Based LOD**

**Terrain LOD**
```
0-500 studs: Full detail (high-poly terrain, all textures)
500-1,000 studs: Medium detail (reduced poly count 50%, texture resolution 50%)
1,000-2,000 studs: Low detail (reduced poly count 75%, simplified textures)
2,000+ studs: Minimal detail (distant terrain boxes, flat colors)
```

**Pet LOD**
```
0-100 studs: Full detail (high-poly models, all animations, physics)
100-300 studs: Medium detail (reduced poly 40%, simplified animations)
300-500 studs: Low detail (reduced poly 70%, static pose, no animations)
500+ studs: Billboard (2D sprite facing camera, no 3D model)
```

**Vegetation LOD**
```
0-200 studs: Full detail (3D trees, grass, flowers)
200-500 studs: Medium detail (simplified trees, no grass)
500+ studs: Minimal (tree billboards only, no undergrowth)
```

**Particle Effects LOD**
```
0-150 studs: Full particles (weather, ambient, magic effects)
150-300 studs: Reduced particles (50% density)
300+ studs: No particles (performance save)
```

### 16.3 Streaming System

**Asset Streaming**
- Biome assets loaded on-demand (not all at once)
- Pre-load adjacent biomes when player approaches boundary (500-stud buffer)
- Unload previous biome assets when player leaves (300-stud buffer)

**Memory Management**
```
Asset Priority Tiers:
1. Critical (always loaded): Player model, UI, core scripts
2. High priority: Current biome terrain, active pets within 200 studs
3. Medium priority: Adjacent biome terrain, pets 200-500 studs
4. Low priority: Distant biomes, inactive dungeon interiors
5. Cached: Previously visited areas (kept in memory if space allows)

Mobile memory budget: 2GB
- Critical: 500MB
- High: 800MB
- Medium: 400MB
- Low: 200MB
- Cached: 100MB
```

**Texture Streaming**
- Low-res textures loaded first (instant appearance)
- High-res textures stream in over 1-2 seconds (progressive enhancement)
- Mobile devices cap at medium-res textures (save memory)

### 16.4 Network Optimization

**Entity Update Frequency**

**Player Updates** (High Priority)
- Position: 20 Hz (50ms intervals) - smooth movement
- Health/stats: 10 Hz (100ms intervals)
- Actions (attacks, abilities): Immediate (0ms delay)

**Pet Updates** (Medium Priority)
- Near players (<100 studs): 10 Hz (100ms)
- Medium distance (100-300 studs): 5 Hz (200ms)
- Far distance (300+ studs): 2 Hz (500ms)
- Dormant (unloaded sectors): 0 Hz (no updates)

**Environmental Updates** (Low Priority)
- Weather changes: 0.5 Hz (2-second intervals)
- Day/night cycle: 0.1 Hz (10-second intervals)
- Chest states: On-demand only (when player interacts)

**Bandwidth Optimization**
- Delta compression: Only send changed values (not full state)
- Position quantization: Round positions to nearest 0.1 stud (reduces packet size)
- Interpolation: Client predicts movement between updates (smooth despite low Hz)

**PvPvE Server Load**
- 20-40 players per server instance (optimal balance)
- More players = more network traffic, but acceptable with optimizations
- Server tick rate: 60 Hz (server simulates world 60 times per second)
- Client receives subsets of that data based on relevance

### 16.5 Mobile-Specific Optimizations

**Graphics Settings (Auto-Detected)**

**Low-End Mobile** (iPhone X, Samsung S8, older)
- Resolution: 720p (reduced from 1080p)
- Frame rate cap: 30 FPS
- Shadow quality: Low (simple blob shadows)
- Particle density: 25%
- View distance: 500 studs
- LOD aggressive: Switch to low-detail at 150 studs

**Mid-Range Mobile** (iPhone 12, Samsung S20)
- Resolution: 1080p
- Frame rate cap: 60 FPS
- Shadow quality: Medium
- Particle density: 50%
- View distance: 1,000 studs
- LOD moderate: Low-detail at 300 studs

**High-End Mobile** (iPhone 15 Pro, Samsung S24 Ultra)
- Resolution: 1080p+ (can go higher)
- Frame rate cap: 60 FPS (can enable 120 FPS)
- Shadow quality: High
- Particle density: 100%
- View distance: 1,500 studs
- LOD standard: Low-detail at 500 studs

**Battery Saver Mode** (User-Toggled)
- Reduces all settings by one tier
- Frame rate: 30 FPS cap
- Disables non-essential particles
- Reduces audio quality (mono instead of stereo)
- Background processes paused

**Touch Input Optimization**
- Large touch targets (80x80 pixels minimum)
- Gesture controls (swipe to dodge, pinch to zoom map)
- Simplified UI (fewer buttons than PC version)
- Auto-target enemies (tap to lock-on, reduces precision needs)

### 16.6 Server Performance

**Instance Management**
- Dedicated server per expedition instance (isolated simulation)
- Server spins up on-demand (player queue joins)
- Server shuts down 5 minutes after last player extracts (cleanup)

**Load Balancing**
- Multiple servers host different expedition instances simultaneously
- Player matchmaking assigns to least-loaded server
- Target: <100ms ping for all players (regional servers)

**Database Optimization**
- Player data cached in memory during expedition (no database hits mid-game)
- Save to database only on extraction or death (reduces write load)
- Batch saves: Multiple players extract → grouped database transaction

**Anti-Cheat Server Authority**
- All critical gameplay server-authoritative:
  - Pet spawns
  - Loot drops
  - Damage calculations
  - Capture success rates
  - Extinction timers
- Client only handles rendering and input
- Prevents client-side exploits

---

# ETERNAL WILDS - WORLD & MAP SYSTEM DESIGN DOCUMENT
## Part 8 of 10: Laboratory Base, Progression & Social Systems

---

## 17. LABORATORY BASE SYSTEM

### 17.1 Laboratory Base Overview

**Core Concept**
The Laboratory Base is the player's **persistent personal instance** that exists outside the expedition loop. This is where players manage their pet collection, craft advanced gear, customize their space, and interact socially with other players. Unlike the temporary Expedition Base Hub (covered in Part 3), the Laboratory Base is permanent and evolves with the player's progression.

**Key Distinctions from Expedition Base Hub**

| Feature | Expedition Base Hub | Laboratory Base |
|---------|---------------------|-----------------|
| **Location** | Inside expedition map (temporary) | Separate instance (permanent) |
| **Persistence** | Exists only during active expedition | Always accessible between expeditions |
| **Function** | Basic crafting, extraction, safety | Pet management, advanced crafting, customization |
| **Social** | See squad members only | Other players can visit your instance |
| **Progression** | No upgrades (static) | Upgradeable structures and expansions |
| **Access** | During expedition only | Main menu hub, always available |

### 17.2 Laboratory Base Layout

**Starting Layout (Tier 1)**

When players first create their account, they receive a basic Laboratory Base with minimal structures:

**Total Area**: 2,000 x 2,000 studs (4 million square studs)
- Much smaller than expedition map (focused, contained space)
- Flat terrain with decorative boundaries (mountains/walls)
- Centralized layout (all structures within 500 studs of center)

**Core Structures (Cannot Be Removed)**

**1. Central Laboratory Building**
- **Size**: 100 x 100 studs, 3 stories tall
- **Function**: Main hub, houses core systems
- **Interior zones**:
  - **Ground floor**: Pet storage terminals, crafting stations, storage chests
  - **Second floor**: Blueprint research lab, alchemy station
  - **Third floor**: Player bedroom (cosmetic), trophy room
- **NPCs**: 
  - Master Craftsman (advanced crafting guide)
  - Pet Keeper (pet management tutorials)
  - Researcher (blueprint analysis)

**2. Pet Habitat Dome**
- **Size**: 300-stud diameter circular enclosure
- **Function**: Display up to 20 pets simultaneously in natural habitat
- **Environment**: Adaptable biome (matches displayed pets' element)
  - Example: Fire pets displayed → volcanic habitat theme
  - Mixed elements → neutral grassland habitat
- **Interaction**: 
  - Click pet to view stats/info
  - Pets perform idle animations (walk around, play, rest)
  - No combat (peaceful sanctuary)
- **Upgrade**: Expand to hold 50 pets (Tier 2), 100 pets (Tier 3)

**3. Crafting Workshop**
- **Size**: 50 x 50 studs outdoor structure
- **Function**: Advanced gear crafting (weapons, armor, tools)
- **Stations**:
  - Forge (metal gear)
  - Loom (fabric gear)
  - Workbench (tools, consumables)
  - Enhancement table (upgrade existing gear)
- **Upgrade**: Add more stations, faster crafting speeds

**4. Storage Warehouse**
- **Size**: 60 x 60 studs building
- **Function**: Permanent material storage (all expedition loot deposited here)
- **Capacity**: 
  - Tier 1: 200 slots (starting)
  - Tier 2: 500 slots (upgrade)
  - Tier 3: 1,000 slots (max upgrade)
- **Organization**: Auto-sorted by material type, rarity, biome source

**5. Training Grounds**
- **Size**: 200 x 200 studs outdoor arena
- **Function**: Train pets (leveling system covered in Pet System doc)
- **Features**:
  - Training dummies (pets attack for XP)
  - Obstacle courses (pets navigate for stat bonuses)
  - Sparring zones (pets fight each other for training)
- **Upgrade**: Add more training equipment, faster XP gains

**6. Garden/Resource Farm** (Optional Structure)
- **Size**: 100 x 100 studs plot
- **Function**: Grow renewable resources (herbs, berries, basic materials)
- **Mechanics**:
  - Plant seeds (obtained from expeditions)
  - Real-time growth (1 hour per harvest)
  - Yield: 5-10 common materials per harvest
- **Strategic value**: Passive resource generation (reduces expedition dependency)
- **Upgrade**: Faster growth, higher yields, rare material plants

### 17.3 Laboratory Base Access & Navigation

**Accessing Laboratory Base**

**From Main Menu**
- Button: "Enter Laboratory"
- Loads personal instance (3-5 second load time)
- Always accessible (no expedition required)

**From Expedition** (Two Methods)
1. **Extract from expedition**: Automatically returns to Laboratory Base
2. **Return during expedition**: Mid-expedition extraction (covered in Part 3)

**Exiting Laboratory Base**
- Button: "Exit to Main Menu" (returns to game lobby)
- Button: "Start New Expedition" (enters matchmaking/solo queue)
- Button: "Visit Friend's Lab" (social feature, see Section 17.7)

**In-Lab Navigation**
- **Teleport waypoints**: Click structure on minimap to instant-travel
- **Walking**: Can manually walk between structures (immersive)
- **Fast travel**: Hold button to open radial menu, select destination

### 17.4 Pet Collection Display System

**Pet Storage Terminal** (Inside Central Laboratory)

**Storage Capacity**
- **Base capacity**: 100 pet slots
- **Expansion**: Purchase additional slots (50 slots per expansion, max 500 total)
- **Currency**: Expedition Currency or Premium Currency

**Pet Organization**

**Sorting Options**
- By rarity (Common → Mythic)
- By element type (Fire, Water, Nature, etc.)
- By star rating (1-star → 5-star)
- By level (1 → 70)
- By acquisition date (newest → oldest)
- By favorite status (favorited pets first)

**Filtering Options**
- Show only specific rarity
- Show only specific element
- Show only breeding-ready pets
- Show only max level pets
- Search by name

**Pet Display Grid**
- Grid view: 4x5 grid (20 pets per page)
- Each cell shows:
  - Pet portrait (animated sprite)
  - Name
  - Element icon
  - Star rating (1-5 stars)
  - Level (1-70)
  - Favorite icon (star, toggleable)

**Pet Detail View** (Click Pet)
```
UI Overlay:
┌─────────────────────────────────────────┐
│  [Pet Portrait - 3D Rotating Model]     │
│  Name: Inferno Salamander               │
│  Type: Fire/Dragon                      │
│  Rarity: Legendary (5★)                 │
│  Level: 45 / 70                         │
│  HP: 5,000 / 5,000                      │
│  ───────────────────────────────────    │
│  Stats:                                 │
│  ├─ Attack: 450                         │
│  ├─ Defense: 320                        │
│  ├─ Speed: 280                          │
│  └─ Special: 500                        │
│  ───────────────────────────────────    │
│  Abilities:                             │
│  ├─ Fireball (Basic Attack)            │
│  ├─ Meteor Strike (Special)            │
│  └─ Inferno Shield (Defensive)         │
│  ───────────────────────────────────    │
│  Origin: Captured in Volcanic Rift     │
│  Date Acquired: Dec 15, 2025           │
│  ───────────────────────────────────    │
│  [Train] [Breed] [Release] [Favorite]  │
└─────────────────────────────────────────┘
```

**Pet Habitat Display** (Outdoor Dome)

**Display Selection**
- Choose up to 20 pets (Tier 1) to showcase in habitat
- Selected pets appear in 3D within dome
- Pets wander, interact, perform animations
- Other players visiting your lab see these pets

**Habitat Customization**
- Environment theme: Matches pet types or choose manually
  - Volcanic theme (lava rocks, fire effects)
  - Aquatic theme (pond, waterfalls)
  - Forest theme (trees, grass, flowers)
  - Void theme (floating platforms, cosmic background)
- Decorations: Place rocks, plants, structures (cosmetic)
- Pet behaviors: Toggle idle animations (sleep, play, etc.)

**Showcase Features**
- Legendary/Mythic pets glow with special aura (prestige)
- Rare pets have particle effects (shimmering, sparks)
- Visitors can click your pets to see stats (read-only, no interaction)
- Trophy status: "Most Impressive Collection" badge if you own all mythics

### 17.5 Advanced Crafting System

**Crafting Tiers**

**Basic Crafting** (Expedition Base Hub)
- Consumables only (bandages, potions, food)
- Low-tier materials required
- No blueprint needed (recipes auto-unlocked)

**Advanced Crafting** (Laboratory Base)
- Weapons, armor, tools, special items
- High-tier materials required (rare+)
- Blueprints required (unlocked via drops, research)
- Crafting time: 5 minutes - 24 hours (real-time)

**Master Crafting** (Late-Game)
- Legendary/Mythic gear
- Extremely rare materials (legendary, mythic essences)
- Master blueprints (1% drop from mythic pets)
- Crafting time: 24-72 hours (real-time)
- Enhancement system (upgrade existing gear to +1, +2, +3, etc.)

**Crafting Stations**

**Forge** (Metal Gear)
- **Weapons**: Swords, axes, hammers, spears
  - Stats: Attack damage +10-50% (scales with materials)
  - Durability: 100-500 uses before repair needed
  - Special effects: Fire damage, ice slow, lightning stun
- **Heavy Armor**: Chest plates, helmets, greaves
  - Stats: Defense +15-40%, HP +10-25%
  - Movement speed penalty: -5% to -15%
  - Elemental resistances (fire, ice, poison, etc.)

**Loom** (Fabric Gear)
- **Light Armor**: Robes, cloaks, hoods
  - Stats: Defense +5-20%, Stamina +10-30%
  - Movement speed bonus: +5% to +15%
  - Evasion bonus: +5% dodge chance
- **Utility Items**: Backpacks (inventory expansion), belts (quickslot items)

**Workbench** (Tools & Consumables)
- **Tools**: 
  - Trap detection lens (reveals trapped chests)
  - Grappling hook (mobility tool)
  - Mining pickaxe (harvest resource nodes faster)
  - Fishing rod (catch aquatic pets, future feature)
- **Advanced Consumables**:
  - Greater healing potion (restore 50% HP)
  - Elemental resistance elixir (50% damage reduction vs element)
  - Capture rate booster (temporary +25% capture chance)
  - Resurrection scroll (revive dead squadmate in PvE co-op)

**Enhancement Table** (Gear Upgrades)
- **Function**: Upgrade existing gear to higher tiers (+1, +2, +3, max +5)
- **Cost**: Duplicate materials + enhancement stones (rare drop)
- **Effect per tier**:
  - +1: +10% stats
  - +2: +20% stats
  - +3: +30% stats + special passive ability
  - +4: +40% stats + improved passive
  - +5: +50% stats + legendary passive (glowing visual effect)
- **Failure chance**: 
  - +1 to +2: 90% success
  - +2 to +3: 70% success
  - +3 to +4: 50% success
  - +4 to +5: 30% success (risky!)
  - Failure: Gear destroyed (harsh penalty, creates risk/reward tension)
- **Protection items**: "Safe Enhancement Stone" prevents destruction on failure (rare premium item)

**Blueprint System**

**Blueprint Acquisition**
- **Dungeon bosses**: 20% drop chance
- **World events**: Guaranteed blueprint for participation
- **Legendary chests**: 30% drop chance
- **Mythic pets**: 100% drop master blueprint
- **Crafting research**: Spend research points to unlock (see Section 17.6)

**Blueprint Rarity Tiers**
- **Common blueprints**: Basic gear (iron sword, leather armor)
- **Uncommon blueprints**: Improved gear (steel sword, reinforced armor)
- **Rare blueprints**: Specialized gear (fire sword, frost armor)
- **Epic blueprints**: Powerful gear (dragon slayer sword, titan armor)
- **Legendary blueprints**: Best-in-slot gear (mythic weapon, legendary armor set)
- **Set blueprints**: Craft entire gear set (4-6 pieces, set bonuses when worn together)

**Example Blueprint: Inferno Blade** (Epic Weapon)
```
Inferno Blade Blueprint
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Type: Sword (Two-Handed)
Rarity: Epic
Crafting Time: 12 hours

Required Materials:
├─ Volcanic Steel Ingot x10 (rare)
├─ Inferno Drake Scale x5 (epic)
├─ Fire Essence x20 (uncommon)
└─ Obsidian Shard x15 (rare)

Stats:
├─ Attack Damage: +35%
├─ Fire Damage: +50 per hit
├─ Durability: 300 uses
└─ Special: "Flame Trail" - Leaves fire on ground, damages enemies who walk through

Crafting Requirements:
├─ Forge Level: 3 (upgraded forge)
├─ Player Level: 30+
└─ Blueprint: Learned
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Crafting Queue System**
- Players can queue up to 3 crafting projects simultaneously
- Projects craft in real-time (continue even when offline)
- Notification when craft completes (mobile push notification)
- Instant craft option: Premium currency skip wait time

### 17.6 Research & Progression System

**Research Lab** (Inside Central Laboratory, 2nd Floor)

**Research Points (RP)**
- **Earn RP**: Complete expeditions, defeat bosses, discover landmarks
  - Successful extraction: 10 RP
  - Boss defeat: 20 RP
  - Legendary pet capture: 50 RP
  - Mythic pet capture: 100 RP
- **RP cap**: 1,000 RP stored maximum (encourages spending)

**Research Tree Categories**

**Category 1: Pet Mastery**
- **Increased Capture Rate**: +5% capture chance per tier (5 tiers, 50 RP each)
- **Pet XP Boost**: +10% pet training XP per tier (5 tiers, 75 RP each)
- **Breeding Success Rate**: +5% breeding success per tier (3 tiers, 100 RP each)
- **Max Pet Level**: Unlock level 75, 80 (2 tiers, 200 RP each)
- **Pet Ability Slots**: Unlock 4th ability slot (1 tier, 300 RP)

**Category 2: Crafting Mastery**
- **Faster Crafting**: -10% crafting time per tier (5 tiers, 50 RP each)
- **Blueprint Research**: Unlock random blueprint (repeatable, 100 RP each)
- **Material Efficiency**: 10% chance to refund materials (3 tiers, 75 RP each)
- **Enhancement Success**: +5% enhancement success per tier (5 tiers, 100 RP each)
- **Set Crafting**: Unlock ability to craft set gear (1 tier, 250 RP)

**Category 3: Expedition Mastery**
- **Starting Loadout**: +1 inventory slot per tier (5 tiers, 50 RP each)
- **Stamina Capacity**: +20 max stamina per tier (3 tiers, 75 RP each)
- **Extraction Speed**: -2 seconds extraction time per tier (3 tiers, 100 RP each)
- **Fog of War Range**: +20 studs reveal radius (3 tiers, 100 RP each)
- **Currency Bonus**: +10% expedition currency per tier (5 tiers, 50 RP each)

**Category 4: Laboratory Upgrades**
- **Pet Habitat Expansion**: +30 display slots (3 tiers, 150 RP each)
- **Storage Expansion**: +100 material slots (5 tiers, 100 RP each)
- **Garden Efficiency**: -20% plant growth time (3 tiers, 75 RP each)
- **Training Speed**: +15% pet training XP (3 tiers, 100 RP each)
- **Crafting Slots**: +1 simultaneous craft queue (2 tiers, 200 RP each)

**Total RP Investment**: ~10,000 RP for full research tree (long-term progression)

**Research Respec**
- Cost: 500 RP or premium currency
- Refunds all spent RP (can redistribute)
- Useful for changing playstyle focus

### 17.7 Social Features

**Visiting Other Players' Laboratories**

**Access Method**
- From Laboratory Base: "Visit Friend" button
- From friend list: Click player → "Visit Lab"
- From leaderboard: Click top player → "Visit Lab"
- From guild roster: Click guildmate → "Visit Lab"

**Visitor Permissions**
- **Default (public)**: Anyone can visit
- **Friends only**: Only friends list can visit
- **Guild only**: Only guild members can visit
- **Private**: No visitors allowed

**What Visitors Can Do**
- Walk around freely (full access to area)
- View pet collection in habitat (click pets to see stats)
- View trophy room (player achievements displayed)
- Leave "visitor book" message (guest log, 100 character limit)
- Give "likes" (thumbs up system, once per day per player)
- Take screenshots (photo mode available)

**What Visitors Cannot Do**
- Access storage (materials are private)
- Use crafting stations (owner only)
- Interact with NPCs (read-only)
- Take items or pets (obviously)

**Prestige System**
- Players earn "Lab Rating" based on:
  - Total pet collection size
  - Number of legendary/mythic pets
  - Crafted gear quality
  - Laboratory decorations
  - Visitor likes
- Leaderboard: "Top 100 Laboratories"
- Reward: Exclusive cosmetic decorations for high-ranking labs

**Player Trading System** (Laboratory-Only)

**Trade Restrictions**
- **Can trade**: Materials, blueprints, consumables, non-equipped gear
- **Cannot trade**: Pets (prevents pay-to-win), equipped gear, premium items

**Trade Interface**
```
Trade Window:
┌─────────────────────────────────────────┐
│  You Offer        ⇄        They Offer   │
├─────────────────────────────────────────┤
│  [Item Slot 1]            [Item Slot 1] │
│  [Item Slot 2]            [Item Slot 2] │
│  [Item Slot 3]            [Item Slot 3] │
│  ...                      ...           │
├─────────────────────────────────────────┤
│  Currency: 500 ⇄ Currency: 1000         │
├─────────────────────────────────────────┤
│  [✓ Ready] [Cancel]   [✓ Ready] [Wait]  │
└─────────────────────────────────────────┘
Both players must click Ready to confirm trade.
```

**Trade Taxes**
- 10% transaction fee on currency trades (gold sink)
- No tax on direct item-for-item trades
- Prevents currency inflation

**Trade Security**
- Both players must confirm twice (prevents scams)
- Trade history logged (support can investigate disputes)
- Cooldown: 1 trade per 5 minutes per player (anti-bot measure)

**Mail System**

**Function**: Send items/currency to offline players

**Usage**
- Send up to 5 items + currency per mail
- Recipient receives notification (in-game + mobile)
- Mail expires after 30 days (items return to sender)

**Restrictions**
- Friends only (can't mail strangers)
- 10 mail limit per day (anti-spam)
- Same trade restrictions apply (no pets)

### 17.8 Guild System

**Guild Creation**
- **Cost**: 10,000 expedition currency or premium currency
- **Requirements**: Player level 20+
- **Guild name**: Unique, 3-20 characters
- **Guild tag**: [TAG], 2-4 characters, displayed next to player name

**Guild Features**

**Guild Hall** (Shared Social Space)
- Separate instance from personal laboratories
- All guild members spawn here when entering "Guild Hall"
- Layout:
  - Central meeting plaza (50 player capacity)
  - Guild trophy room (displays guild achievements)
  - Guild storage (shared material bank, permissions required)
  - Guild message board (announcements, events)
  - Guild shop (special items purchasable with guild points)

**Guild Ranks & Permissions**
| Rank | Permissions |
|------|-------------|
| **Guild Master** | All permissions, can disband guild |
| **Officer** | Invite/kick members, edit message board, manage storage |
| **Veteran** | Access guild storage (withdraw limit), edit message board |
| **Member** | Access guild hall, deposit to storage |
| **Recruit** | Access guild hall only (trial period) |

**Guild Progression**
- **Guild Level**: 1-50 (earned via member activity)
- **XP sources**: 
  - Member extractions: 10 guild XP each
  - Member boss defeats: 50 guild XP each
  - Guild events participation: 100 guild XP per event
- **Level benefits**:
  - Level 5: +5% currency for all members
  - Level 10: Unlock guild storage (50 slots)
  - Level 15: +10% pet XP for all members
  - Level 20: Guild hall customization unlocked
  - Level 25: Unlock guild shop
  - Level 30: +10% capture rate for all members
  - Level 50: Exclusive guild mount (cosmetic pet that follows player)

**Guild Storage**
- Shared material bank (members contribute resources)
- Permissions:
  - Guild Master/Officers: Unlimited withdraw
  - Veterans: 10 items per day withdraw
  - Members: 5 items per day withdraw
  - Recruits: No withdraw (deposit only)
- Purpose: Support guildmates, fund guild events

**Guild Events** (Weekly)

**Event 1: Guild Raid** (Saturday, 8pm server time)
- Special expedition instance (guild-only, 10-20 players)
- Super buffed world boss (100,000+ HP)
- Requires coordination (voice chat recommended)
- Rewards: Exclusive guild gear, guild points, prestige

**Event 2: Guild Wars** (PvP, Sunday, 8pm server time)
- Two guilds matched for PvPvE expedition
- Objective: Extract most combined loot
- Winning guild: Bonus guild XP, currency, title "Champions of the Wilds" (1 week)

**Event 3: Guild Expedition** (Daily, flexible time)
- Members complete expeditions, contribute guild XP
- Daily goal: 500 guild XP from all members
- Reward if met: +20% currency for all members next day

**Guild Shop** (Unlocked at Guild Level 25)
- **Guild Points**: Earned via event participation
- **Shop items**:
  - Exclusive guild-themed gear (cosmetic variants)
  - Guild banners (decoration for personal lab)
  - XP boosts (temporary buffs)
  - Crafting materials (rare tier)
  - Guild mount skins (cosmetic variants)
- **Refresh**: Weekly (new items rotate in)

### 17.9 Achievement System

**Achievement Categories**

**Exploration Achievements**
- "World Traveler": Discover all 9 biomes (Reward: 500 RP)
- "Landmark Hunter": Visit all landmarks (Reward: Compass upgrade)
- "Dungeon Delver": Clear all dungeon types (Reward: Dungeon map item)
- "Event Witness": Experience all 6 world events (Reward: Event catalyst item)

**Combat Achievements**
- "Beast Slayer": Defeat 1,000 pets (Reward: +5% damage title)
- "Boss Hunter": Defeat 50 dungeon bosses (Reward: Boss radar item)
- "Alpha Predator": Defeat all Alpha types (Reward: Alpha-themed weapon skin)
- "Mythic Conqueror": Defeat 5 mythic pets (Reward: Mythic hunter title)

**Collection Achievements**
- "Pet Collector": Capture 100 unique pets (Reward: +50 pet storage)
- "Legendary Keeper": Capture 10 legendary pets (Reward: Legendary capture boost)
- "Mythic Master": Capture all mythic types (Reward: Mythic master title + exclusive mount)
- "Element Expert": Capture all elemental types (Reward: Elemental fusion blueprint)

**Crafting Achievements**
- "Master Craftsman": Craft 100 items (Reward: -10% crafting time)
- "Enhancement Guru": Successfully enhance gear to +5 (Reward: +10% enhancement success)
- "Set Collector": Craft all set gear pieces (Reward: Set bonus +10%)

**Social Achievements**
- "Social Butterfly": Visit 50 different labs (Reward: Visitor badge)
- "Guild Loyalist": Member of same guild for 6 months (Reward: Guild veteran title)
- "Trade Tycoon": Complete 100 trades (Reward: -5% trade tax)

**Prestige Achievements** (Extremely Rare)
- "Eternal Guardian": Own all pets in game (Reward: Eternal title + rainbow name color)
- "Master of the Wilds": Complete all achievements (Reward: Master cape cosmetic)
- "Legend": Rank #1 on any leaderboard for 30 days (Reward: Crown cosmetic)

**Achievement Display**
- Trophy room in personal lab (3D trophies for major achievements)
- Title system (equip one active title, displays above player name)
- Achievement points (displayed on profile, leaderboard category)

### 17.10 Seasonal Content System

**Seasons Overview**
- **Duration**: 3 months per season (4 seasons per year)
- **Theme**: Each season has unique theme (Winter Festival, Summer Expedition, etc.)
- **Content**: Exclusive pets, events, gear, cosmetics

**Season Structure**

**Season Pass** (Battle Pass System)
- **Free track**: 50 tiers, basic rewards (materials, currency, blueprints)
- **Premium track**: 50 tiers, exclusive rewards (pets, cosmetics, titles)
  - Cost: $10 USD or 1,000 premium currency
- **XP sources**: 
  - Complete expeditions: 100 season XP
  - Daily quests: 50 season XP each (3 per day)
  - Weekly quests: 200 season XP each (5 per week)
  - Event participation: 500 season XP
- **Time to complete**: ~50-60 hours of gameplay (casual-friendly)

**Seasonal Events**

**Winter Season: "Frostfall Festival"**
- **Theme**: Ice and snow everywhere
- **Limited pet**: Frost Phoenix (legendary seasonal exclusive)
- **Limited gear**: Frostborn armor set (cosmetic + stats)
- **Special biome**: Temporary "Eternal Glacier" biome spawns in random seeds
- **Event**: Snowball fight PvP mode (fun casual mode)

**Spring Season: "Bloom Awakening"**
- **Theme**: Nature flourishes, cherry blossoms
- **Limited pet**: Sakura Spirit (legendary seasonal exclusive)
- **Limited gear**: Nature guardian armor (flower petal effects)
- **Special biome**: "Enchanted Grove" appears randomly
- **Event**: Flower festival (collect rare flower pets)

**Summer Season: "Sunscorch Trials"**
- **Theme**: Extreme heat, desert expansion
- **Limited pet**: Solar Drake (legendary seasonal exclusive)
- **Limited gear**: Solar knight armor (glowing hot metal effect)
- **Special biome**: "Scorched Wastes" extreme difficulty
- **Event**: Heatwave survival challenge (endurance mode)

**Fall Season: "Harvest Moon"**
- **Theme**: Autumn colors, harvest theme
- **Limited pet**: Lunar Owl (legendary seasonal exclusive)
- **Limited gear**: Harvest lord armor (autumn leaf cloak)
- **Special biome**: "Harvest Fields" agricultural theme
- **Event**: Crop collection competition (farming mode)

**FOMO (Fear of Missing Out) Mitigation**
- Seasonal pets return in future seasons (rotational, not exclusive forever)
- Missed battle pass tiers purchasable next season (at higher cost)
- Seasonal cosmetics available in "Legacy Shop" after 1 year (expensive)
- No gameplay advantages locked behind seasons (cosmetic focus)

**Post-Season**
- Season ends: 2-week grace period to finish battle pass
- Next season begins: New theme, new pets, new rewards
- Previous season items move to "Legacy Collection" (prestige status)

---

## 18. PLAYER PROGRESSION SYSTEM

### 18.1 Player Level System

**Level Progression**
- **Max level**: 100
- **XP sources**:
  - Successful extraction: 500 XP
  - Pet defeat: 10-100 XP (scales with pet rarity)
  - Boss defeat: 500 XP
  - Dungeon clear: 1,000 XP
  - First discovery (biome, landmark, dungeon): 250 XP
  - Event participation: 1,000 XP
- **XP curve**: Exponential (early levels fast, later levels slow)
  - Level 1→10: ~5,000 XP total (1 hour)
  - Level 10→30: ~50,000 XP total (10 hours)
  - Level 30→50: ~250,000 XP total (50 hours)
  - Level 50→100: ~2,000,000 XP total (400+ hours)

**Level Rewards**
- Every level: +100 expedition currency
- Every 5 levels: +50 research points
- Every 10 levels: New blueprint unlocked
- Level 10: Unlock breeding system
- Level 20: Unlock guild creation
- Level 30: Unlock advanced crafting
- Level 50: Unlock master crafting
- Level 75: Unlock legendary gear crafting
- Level 100: Unlock mythic gear crafting + prestige title

**Prestige System** (Post-Level 100)
- Option to "prestige" (reset to level 1, keep all items/pets)
- Rewards:
  - Prestige star (displayed next to name, max 10 stars)
  - +5% XP gain per prestige (stacking, up to +50%)
  - Exclusive prestige cosmetics (glowing aura, particle effects)
  - Prestige-only blueprints (cosmetic weapon skins)
- **Why prestige?**: Endgame progression, show off dedication

### 18.2 Leaderboard System

**Leaderboard Categories**

**1. Pet Collection Leaderboard**
- Metric: Total unique pets owned
- Rankings: Top 100 globally
- Rewards (monthly reset):
  - Top 1: 5,000 premium currency + exclusive title "Pet Master"
  - Top 10: 2,000 premium currency + exclusive mount
  - Top 100: 500 premium currency + nameplate border

**2. Expedition Count Leaderboard**
- Metric: Total successful extractions
- Rankings: Top 100 globally
- Rewards (monthly): Currency + "Veteran Explorer" title

**3. Mythic Hunter Leaderboard**
- Metric: Total mythic pets captured
- Rankings: Top 100 globally
- Rewards (monthly): Premium currency + "Mythic Legend" title

**4. Guild Leaderboard**
- Metric: Guild level + activity score
- Rankings: Top 50 guilds globally
- Rewards (monthly): Guild points, exclusive guild cosmetics

**5. Crafting Leaderboard**
- Metric: Total legendary+ gear crafted
- Rankings: Top 100 globally
- Rewards (monthly): Rare blueprints + "Master Smith" title

**6. Laboratory Prestige Leaderboard**
- Metric: Lab rating (pet collection + decorations + visitor likes)
- Rankings: Top 100 globally
- Rewards (monthly): Exclusive decorations + "Architect" title

**Leaderboard Refresh**
- Daily snapshot at midnight (server time)
- Monthly rewards distributed on 1st of month
- Seasonal leaderboards (separate from monthly, bigger rewards)

### 18.3 Daily & Weekly Quest System

**Daily Quests** (3 per day, reset at midnight)

**Quest Pool** (Random Selection)
- "Complete 3 expeditions" (Reward: 500 currency + 50 season XP)
- "Defeat 20 pets" (Reward: 300 currency + 50 season XP)
- "Capture 5 pets" (Reward: 400 currency + 50 season XP)
- "Clear 1 dungeon" (Reward: 600 currency + 50 season XP)
- "Craft 3 items" (Reward: 300 currency + 50 season XP)
- "Train pets for 10 minutes" (Reward: 200 currency + 50 season XP)
- "Visit 3 friends' labs" (Reward: 100 currency + 50 season XP)

**Quest Reroll**
- Once per day, can reroll one quest (replace with different random quest)
- Useful if daily quest too difficult or time-consuming

**Weekly Quests** (5 per week, reset Monday)

**Quest Pool** (Harder Tasks)
- "Complete 20 expeditions" (Reward: 3,000 currency + 200 season XP + rare blueprint)
- "Defeat 10 dungeon bosses" (Reward: 2,500 currency + 200 season XP + epic materials x10)
- "Capture 3 legendary pets" (Reward: 5,000 currency + 200 season XP + legendary pet egg)
- "Craft 5 epic+ items" (Reward: 2,000 currency + 200 season XP + enhancement stones x3)
- "Participate in 2 world events" (Reward: 3,000 currency + 200 season XP + event catalyst)
- "Earn 10,000 guild XP" (Reward: 1,000 currency + 200 season XP + guild points)
- "Extract successfully 15 times" (Reward: 4,000 currency + 200 season XP + rare blueprint)

**Quest Progress Tracking**
- UI: Quest log button (top-right corner)
- Overlay: Current quest progress displayed in corner during expedition
- Notifications: Quest completed popup (immediate reward claim)

### 18.4 Premium Currency & Monetization

**Currency Types**

**Expedition Currency** (Free, Earned In-Game)
- Earned: Pet defeats, extractions, quests, events
- Spent: Crafting, repairs, NPC purchases, guild fees
- Trade: Yes (can trade with other players)

**Research Points (RP)** (Free, Earned In-Game)
- Earned: Expeditions, bosses, discoveries
- Spent: Research tree upgrades
- Trade: No

**Premium Currency** (Paid, Real Money Purchase)
- Name: "Crystals"
- Purchased: $5 = 500 crystals, $10 = 1,100 crystals (+10% bonus), $50 = 6,000 crystals (+20% bonus)
- Earned (limited): Daily login rewards, season pass, events (small amounts)
- Spent: Cosmetics, battle pass, convenience items, storage expansions
- Trade: No (prevents real-money trading)

**Premium Shop Items** (Non-Pay-to-Win)

**Cosmetics** (No Gameplay Advantage)
- Pet skins: 300-1,000 crystals (visual variants, no stat change)
- Player outfits: 500-1,500 crystals (clothing, hair, accessories)
- Laboratory decorations: 200-800 crystals (furniture, plants, statues)
- Emotes: 100-300 crystals (dances, gestures, reactions)
- Nameplates: 300-600 crystals (borders, backgrounds, effects)
- Mounts: 1,000-2,000 crystals (cosmetic followers, no speed boost)

**Convenience Items** (Save Time, Not Power)
- Instant craft completion: 50-500 crystals (skip crafting timer)
- Storage expansion: 200 crystals (+50 slots)
- Pet slot expansion: 300 crystals (+50 pet slots)
- Inventory expansion: 150 crystals (+10 slots)
- Loadout presets: 100 crystals (save/swap gear sets instantly)

**Premium Items** (Exclusive, Not Pay-to-Win)
- Resurrection scroll: 100 crystals (revive in co-op PvE)
- Safe enhancement stone: 200 crystals (prevent gear destruction on enhance fail)
- Premium battle pass: 1,000 crystals (season rewards)
- XP boost: 50 crystals (2x XP for 24 hours, cosmetic prestige)

**Ethical Monetization Commitment**
- No loot boxes / gambling mechanics
- No random chance purchases
- All items have fixed crystal costs (transparent)
- No power advantages (pets, gear stats cannot be bought)
- Can earn premium currency slowly through gameplay (generous free rewards)

---

# ETERNAL WILDS - WORLD & MAP SYSTEM DESIGN DOCUMENT
## Part 9 of 10: Tutorial, UI/UX, Community & Live Operations

---

## 19. TUTORIAL & NEW PLAYER ONBOARDING

### 19.1 First-Time User Experience (FTUE)

**Account Creation Flow**

**Step 1: Welcome Screen**
```
┌─────────────────────────────────────────┐
│                                         │
│     ETERNAL WILDS                       │
│     ═══════════════                     │
│                                         │
│     [Start Your Journey]                │
│     [Login] [Settings]                  │
│                                         │
│                                         │
│  "Hunt. Collect. Survive."              │
└─────────────────────────────────────────┘
```

**Step 2: Character Customization**
- **Name entry**: 3-16 characters, unique check
- **Avatar selection**: Choose from 12 preset avatars (male/female, diverse ethnicities)
- **Starter pet choice**: Pick one of 3 starter pets
  - **Forest Pup** (Nature type): Balanced stats, easy to use
  - **Ember Fox** (Fire type): High damage, low defense
  - **Aqua Turtle** (Water type): High defense, low damage
- **Display message**: "Your starter pet will be your companion in the Wilds. Choose wisely!"

**Step 3: Cinematic Introduction** (Skippable)
- **Duration**: 2 minutes
- **Content**: 
  - Narrated lore: "The Eternal Wilds... a realm where creatures roam free..."
  - Visual: Sweeping shots of biomes, pets in natural habitats
  - Hook: "But the balance is fragile. Hunters venture in... not all return."
- **Skip button**: Prominent (top-right), skips to tutorial expedition

### 19.2 Tutorial Expedition (Guided First Run)

**Tutorial Structure**: 10-15 minute guided expedition in Whispering Forest only

**Phase 1: Basic Movement & Navigation (0:00 - 2:00)**

**Spawn Location**: Base hub center (safe zone)

**Tutorial Prompts** (Sequential, unskippable)
```
Prompt 1: "Welcome to your Laboratory Base. This is your safe haven."
- Highlight: Central Laboratory building
- Action: Player must walk to marked location (30 studs away)

Prompt 2: "Use [WASD/Joystick] to move. Try walking to the glowing marker."
- Marker: Glowing green waypoint
- Action: Player walks to marker

Prompt 3: "Great! Now let's enter an expedition. Approach the Expedition Portal."
- Marker: Portal at base edge
- Action: Player walks to portal, auto-triggers expedition start
```

**Expedition Entry**: Auto-loads tutorial seed (fixed map, not procedural)

**Phase 2: Exploration & Fog of War (2:00 - 4:00)**

**Spawn Location**: Tutorial expedition base hub

```
Prompt 4: "The Wilds are vast and unknown. Explore to reveal the map."
- UI highlight: Minimap (top-right)
- Objective: Walk 100 studs in any direction
- Effect: Fog of war reveals around player

Prompt 5: "Your minimap shows your surroundings. Use it to navigate."
- Objective: Continue walking, reach first landmark (Ancient Tree sapling, 200 studs away)
```

**Environmental Design**:
- Linear path (no branching, prevents getting lost)
- Visible landmarks guide player forward
- No hostile pets yet (only ambient wildlife, non-aggressive)

**Phase 3: Pet Encounter & Combat (4:00 - 7:00)**

**First Pet Encounter**: Weak Forest Pup (common, level 1)

```
Prompt 6: "A wild pet approaches! Your companion will defend you."
- UI highlight: Pet HP bar (bottom-left)
- Auto-combat: Companion pet attacks automatically
- Tutorial: "Pets fight for you. Watch their HP - if it drops too low, they need healing."

Prompt 7: "Dodge enemy attacks using [Space/Dodge Button]."
- Enemy telegraphs attack (3-second windup, red indicator)
- Objective: Player must press dodge button (forced dodge tutorial)
- Effect: Pet performs dodge animation, avoids damage

Prompt 8: "Great! Timing is key. Dodge when you see red indicators."
- Second enemy attack incoming (player practices dodge again)
```

**Combat Results**:
- Pet defeats enemy automatically after 20-30 seconds
- Enemy drops chest (guaranteed loot for tutorial)

**Phase 4: Looting & Inventory (7:00 - 9:00)**

```
Prompt 9: "The pet dropped a chest. Approach it to collect loot."
- UI highlight: Chest glow effect
- Action: Player walks to chest, auto-opens
- Loot: 5x Wood, 3x Plant Fiber (basic materials)

Prompt 10: "Materials are stored in your inventory. Open your inventory [Tab/Menu Button]."
- UI: Inventory window opens (forced)
- Tutorial: "You'll use materials to craft items and gear. Manage your space wisely."
- UI highlight: Inventory slots (10 occupied, 20 total)
- Close inventory after 5 seconds (auto-close)
```

**Phase 5: Capturing Pets (9:00 - 11:00)**

**Second Pet Encounter**: Another Forest Pup (tutorial capture target)

```
Prompt 11: "This pet is weak enough to capture! Lower its HP first."
- Combat: Player companion attacks, enemy HP drops to 30%
- UI: Capture button appears (glowing, pulsing)

Prompt 12: "Press [C/Capture Button] to attempt capture!"
- Action: Player presses capture button
- Animation: Capture device throws, pet absorbed into light
- Success: 100% guaranteed (tutorial mercy)
- Reward: "Congratulations! You've captured your first pet!"

Prompt 13: "Captured pets are stored safely. You can manage them at your Laboratory Base."
- UI: Pet collection notification (+1 Forest Pup)
```

**Phase 6: Extraction (11:00 - 15:00)**

```
Prompt 14: "Time to extract! Return to the base hub to leave safely."
- UI: Waypoint marker points toward base (500 studs away)
- Objective: Walk back to base (guided path, no enemies)

Prompt 15: "Stand in the extraction zone to leave the expedition."
- Action: Player enters green extraction circle (base center)
- Timer: 5 seconds (reduced from normal 10 for tutorial)
- Effect: Extraction succeeds, returns to Laboratory Base

Prompt 16: "Well done! You've completed your first expedition."
- Rewards screen:
  - Materials collected: 5x Wood, 3x Plant Fiber
  - Pets captured: 1x Forest Pup
  - XP earned: 500 (levels up to level 2)
  - Currency: 100 expedition currency
```

**Phase 7: Laboratory Tour (Post-Expedition)**

```
Prompt 17: "Welcome back to your Laboratory. Let's explore what you can do here."
- Auto-walk: Player character walks to Pet Habitat Dome (guided tour)

Prompt 18: "This is your Pet Habitat. Your captured pets live here safely."
- UI: Pet Habitat interface opens
- Tutorial: "Click a pet to view its stats, train it, or prepare it for breeding."
- Action: Player clicks Forest Pup (tutorial captured pet)

Prompt 19: "Next, let's visit the Crafting Workshop."
- Auto-walk: Player moves to Crafting Workshop

Prompt 20: "Here you can craft gear and consumables using materials."
- UI: Crafting window opens (forced)
- Recipe highlight: Bandage (3x Plant Fiber)
- Tutorial: "Craft a bandage to heal during expeditions."
- Action: Player crafts bandage (instant, free)
- Reward: +1 Bandage in inventory

Prompt 21: "Tutorial complete! You're ready to explore the Wilds on your own."
- Reward: 1,000 expedition currency, 50 RP, 1x Rare Pet Egg
- Message: "Visit the Instructor at the base hub for more guidance."
```

**Tutorial End**: Player now has free control, can start real expeditions

### 19.3 Progressive Tutorials (Contextual Learning)

**System Unlocks Trigger Tutorials**

**Breeding System Tutorial** (Unlocks at Level 10)
```
Notification: "New System Unlocked: Pet Breeding"
Prompt: "Visit the Breeding Grounds at your Laboratory to learn more."
Tutorial: 
1. NPC explains breeding basics (elemental compatibility, star merging)
2. Player breeds two starter-tier pets (guaranteed success)
3. Reward: Breeding guide document (in-game codex entry)
```

**Dungeon Tutorial** (First Dungeon Entry)
```
Notification: "You've discovered a dungeon entrance!"
Prompt: "Dungeons contain powerful enemies and rare loot. Prepare before entering."
Tutorial:
1. Warning: "Dungeons are dangerous. Stock up on healing items."
2. Inside: "Follow the path. Defeat enemies in each room to progress."
3. Boss encounter: "This is the boss! Use all your skills to win!"
4. Completion: "Congratulations! Dungeons reset each expedition for more loot."
```

**PvPvE Tutorial** (First PvPvE Match)
```
Notification: "You've entered a PvPvE expedition. Other players are present."
Prompt: "Be cautious. Other players can attack you and steal your loot if you die."
Tutorial:
1. Minimap: "Red dots are enemy players. Avoid or engage at your discretion."
2. Warning: "If you die, you lose everything except pets in secure slots."
3. Tip: "Extract early if threatened, or form alliances with nearby squads."
```

**Guild Tutorial** (Creating/Joining Guild at Level 20)
```
Notification: "You can now join or create a guild!"
Prompt: "Guilds offer social features, shared resources, and exclusive events."
Tutorial:
1. NPC: "Visit the Guild Hall to meet other members."
2. Storage: "Deposit materials to help your guild progress."
3. Events: "Participate in weekly guild events for rewards."
```

### 19.4 Tutorial Skip & Veteran Onboarding

**Skip Option** (For Experienced Players)

**Main menu option**: "Skip Tutorial" checkbox
- Effect: Starts at level 1, skips all tutorials, drops into Laboratory Base with starter pet
- Warning: "Skipping is recommended for experienced players only."

**Veteran Rewards** (Account Linking/Returning Players)
- If player links previous account (email/social): "Welcome back, Guardian!"
- Rewards: 
  - 5,000 expedition currency
  - 100 RP
  - 1x Rare Pet Egg
  - +50% XP boost for 7 days
- Purpose: Re-engage lapsed players

### 19.5 In-Game Codex (Help System)

**Codex Access**: Menu button → "Codex" → Searchable database

**Codex Categories**:

**Pets**
- Entry for every pet type (unlocked when discovered)
- Stats, element, rarity, biome location
- Lore snippet (flavor text)

**Biomes**
- Description of each biome
- Climate, hazards, pet types
- Recommended level range

**Items & Crafting**
- Recipes for all craftable items
- Material sources (where to find)
- Blueprint list (locked until discovered)

**Game Mechanics**
- Combat system explanation
- Breeding guide
- Extinction mechanic details
- Weather effects reference

**Quests & Achievements**
- Current quests progress
- Achievement list (locked/unlocked)
- Reward previews

**FAQ Section**
- "How do I capture pets?"
- "What happens if I die?"
- "How does breeding work?"
- "What is the extinction mechanic?"
- 50+ common questions answered

---

## 20. UI/UX DESIGN SPECIFICATIONS

### 20.1 HUD Layout (In-Expedition)

**Screen Layout** (1920x1080 reference, scales for mobile)

```
┌───────────────────────────────────────────────────────────────┐
│  [HP: ████████░░ 80%]  [Stamina: ██████████ 100%]    [20:35]  │  TOP
│  [Companion Pet HP: ████████░░ 80%]                 [Minimap]  │
│                                                      [N ↑ ]    │
├───────────────────────────────────────────────────────────────┤
│                                                                │
│                                                                │
│                        GAMEPLAY AREA                           │  CENTER
│                                                                │
│                                                                │
├───────────────────────────────────────────────────────────────┤
│  [Inventory: 15/30]  [Currency: 1,250]         [Dodge] [Menu] │  BOTTOM
│  [Hotbar: Item1] [Item2] [Item3] [Item4]  [Capture] [Attack]  │
└───────────────────────────────────────────────────────────────┘
```

**Top-Left Corner**:
- **Player HP bar**: Red bar, numerical percentage
- **Stamina bar**: Blue bar below HP, depletes during sprint/dodge
- **Companion Pet HP**: Green bar, shows active companion health
- **Status effects**: Icons below HP (poison, burn, freeze, buffs)

**Top-Right Corner**:
- **Minimap**: 200x200 pixels, shows immediate surroundings
  - Toggle zoom: 3 levels (50/100/200 stud radius)
  - Rotation: North-locked (does not rotate with player)
  - Icons: Self (blue arrow), squad (green), enemies (red), POIs (yellow)
- **Expedition timer**: Shows elapsed time (20:35 = 20 minutes, 35 seconds)
- **Wildlife population meter**: Small bar below timer ("Wildlife: 67%")

**Top-Center**:
- **Objective tracker**: Current quest/event objective
- **Event notifications**: "Blood Moon Rising!" (5 seconds display)
- **Warning messages**: "Extraction zones closing in 5 minutes"

**Bottom-Left Corner**:
- **Inventory status**: Current/max slots (15/30)
- **Currency**: Expedition currency count
- **Hotbar**: 4 quick-use item slots (consumables, tools)
  - Keybinds: 1, 2, 3, 4 (PC) or swipe gestures (mobile)

**Bottom-Right Corner**:
- **Action buttons**: 
  - Dodge: Large button (emergency action)
  - Attack: Basic attack button (hold for power attack)
  - Capture: Appears when pet below 30% HP (context-sensitive)
  - Menu: Pause menu, inventory, map, settings

**Center Screen** (Minimal Intrusion):
- **Crosshair**: Subtle dot (aiming reticle)
- **Enemy HP bars**: Above enemy heads (only when in combat)
- **Damage numbers**: Float above enemies when hit (optional, can disable)
- **Interaction prompts**: "[E] Open Chest" (context-sensitive)

### 20.2 Mobile UI Adaptations

**Touch Controls Layout** (6.5" screen reference)

```
┌───────────────────────────────────────────┐
│  [HP/Stam]           [Timer] [Minimap]    │  TOP
├───────────────────────────────────────────┤
│                                           │
│        GAMEPLAY AREA                      │  CENTER
│                                           │
│  [Virtual Joystick]      [Action Ring]   │
│         (Left)               (Right)      │  BOTTOM
├───────────────────────────────────────────┤
│  [Hotbar: Swipe Up for Items]     [Menu] │
└───────────────────────────────────────────┘
```

**Left Side (Movement)**:
- **Virtual joystick**: Translucent circle, drag to move
  - Appears on touch (dynamic position)
  - Larger touch area (150x150 pixels)
  - Sprint: Double-tap center

**Right Side (Actions)**:
- **Action ring**: 4-button radial menu
  - Attack (top)
  - Dodge (right)
  - Capture (bottom, context-sensitive)
  - Ability (left, pet ability)
- **Swipe gestures**:
  - Swipe up: Open inventory
  - Swipe down: Open map
  - Swipe left: Previous hotbar item
  - Swipe right: Next hotbar item

**Auto-Target System** (Mobile Only):
- Tap enemy to lock-on (simplifies aiming)
- Yellow outline on targeted enemy
- Auto-faces target during combat
- Tap empty space to unlock

**Simplified UI Elements**:
- Larger buttons (minimum 80x80 pixels)
- Fewer on-screen elements (less clutter)
- Auto-hide non-critical UI after 3 seconds idle
- Full-screen map (covers gameplay area when opened)

### 20.3 Accessibility Features

**Visual Accessibility**

**Colorblind Modes** (4 Variants)
- **Protanopia** (red-green): Red UI elements → blue/orange
- **Deuteranopia** (red-green): Green UI elements → yellow/blue
- **Tritanopia** (blue-yellow): Blue elements → purple/red
- **Achromatopsia** (full colorblind): High contrast, patterns instead of colors

**UI Scaling**
- **100%**: Default (1920x1080)
- **125%**: Larger text/buttons (recommended for 1366x768)
- **150%**: Maximum scale (accessibility, visually impaired)

**High Contrast Mode**
- Black background, white text
- Thick borders on all UI elements
- Removes transparency effects
- Purpose: Severe visual impairment support

**Font Options**
- **Default**: Custom game font (stylized)
- **OpenDyslexic**: Dyslexia-friendly font (weighted bottom letters)
- **Arial**: Standard sans-serif (maximum readability)

**Text Size** (Independent of UI Scale)
- Small (10pt), Medium (12pt), Large (14pt), Extra Large (16pt)

**Audio Accessibility**

**Subtitles**
- **Size**: Small, Medium, Large
- **Background**: None, Semi-transparent, Opaque black
- **Position**: Bottom-center (default), Top-center, Bottom-left
- **Language**: 15 supported languages (see Section 20.4)

**Audio Cues Visual Indicators**
- **Footsteps**: Directional arrow on screen edge (shows where sound came from)
- **Enemy growls**: Red exclamation mark (enemy nearby)
- **Extraction warning**: Screen border pulse (visual timer)
- **Event notifications**: Full-screen banner (cannot miss)

**Mono Audio** (Single-Ear Headphone Support)
- Combines stereo channels into mono
- Useful for hearing-impaired (one ear only)

**Input Accessibility**

**Remappable Controls** (PC)
- Every action rebindable (keyboard, mouse, controller)
- Multiple binds per action (primary + secondary key)
- Reset to defaults button

**Controller Support**
- Full Xbox/PlayStation/Nintendo controller support (PC)
- Custom sensitivity (analog stick, triggers)
- Vibration intensity (0-100%, or off)
- Button layout presets (A/B swap, inverted Y-axis, etc.)

**One-Handed Mode** (Mobile)
- UI elements cluster to one side (left or right)
- Larger touch targets
- Auto-aim assist increased
- Purpose: Players with limb disability

**Hold vs Toggle** (Accessibility Options)
- Sprint: Hold or toggle (default: hold)
- Crouch: Hold or toggle (default: toggle)
- Map: Hold or toggle (default: hold)
- Purpose: Reduces button-holding strain (RSI prevention)

**Gameplay Accessibility**

**Difficulty Assist Options** (Optional, No Penalties)
- **Slower enemy attacks**: Enemy windup +50% (easier to dodge)
- **Higher capture rates**: +25% capture success (less grind)
- **Reduced permadeath**: Death loses 50% loot instead of 100%
- **Extended extraction timers**: +5 seconds extraction time
- **Purpose**: Make game accessible to players with slower reflexes, disabilities

**Photosensitivity Protection**
- **Seizure warning**: Displayed at game launch
- **Reduced flashing**: Lightning strikes, explosions less intense
- **Disable screen shake**: Removes all camera shake effects
- **Purpose**: Epilepsy safety

### 20.4 Localization & Language Support

**Supported Languages** (15 Total)

**Tier 1 (Full Support)**:
- English (US/UK)
- Spanish (Spain/Latin America)
- French (France/Canada)
- German
- Portuguese (Brazil)
- Japanese
- Korean
- Simplified Chinese
- Traditional Chinese

**Tier 2 (Text Only, No Voice Acting)**:
- Italian
- Russian
- Polish
- Turkish
- Thai
- Arabic (right-to-left text support)

**Localization Features**

**Text Translation**:
- All UI text translated
- All NPC dialogue translated
- All item/pet descriptions translated
- All tutorial prompts translated
- All quest text translated

**Cultural Adaptations**:
- Pet names adjusted for cultural sensitivity
- Avoid culturally insensitive imagery (reviewed per region)
- Date/time formats localized (MM/DD/YYYY vs DD/MM/YYYY)
- Currency symbols localized ($ vs € vs ¥)

**Font Support**:
- Latin scripts: Standard fonts
- Cyrillic (Russian): Cyrillic-compatible font
- CJK (Chinese/Japanese/Korean): Unicode CJK font (large file, ~50MB)
- Arabic: Right-to-left rendering engine

**Voice Acting**:
- English: Full voice acting (NPCs, cinematics)
- Japanese: Full voice acting (large Japanese market)
- Other Tier 1 languages: Subtitles only (budget constraints)
- Option: Toggle voice language independent of text (e.g., Japanese voice + English text)

**Community Translation**:
- After 1 year: Open community translation for additional languages
- Submission portal: Players submit translations, team reviews
- Credit: Community translators credited in-game

---

## 21. COMMUNITY FEATURES

### 21.1 In-Game Communication

**Text Chat System**

**Chat Channels**:
- **Local chat**: Players within 200 studs (expedition only)
- **Squad chat**: Squad members only (persistent)
- **Guild chat**: Guild members (persistent)
- **Global chat**: All online players (main menu only, not during expeditions)
- **Whisper**: Private 1-on-1 messages

**Chat Moderation**:
- **Profanity filter**: Auto-censors blacklist words (can disable in settings, 18+)
- **Spam prevention**: Max 3 messages per 10 seconds
- **Mute function**: Right-click player name → mute (blocks all messages)
- **Report function**: Report player for harassment, hate speech, spam
- **Moderation team**: 24/7 team reviews reports, issues bans (temporary or permanent)

**Quick Chat** (Contextual Pings, No Typing)
- "Help!" (red exclamation)
- "Enemy here!" (red skull)
- "Loot here!" (yellow treasure)
- "Follow me!" (green arrow)
- "Extraction!" (green evacuation symbol)
- Purpose: Communication without keyboard (mobile-friendly, language-agnostic)

**Voice Chat** (Optional, PC/Console Only)
- **Push-to-talk**: Default (hold V to talk)
- **Open mic**: Toggle (always on, voice-activated)
- **Volume control**: Per-player volume sliders
- **Mute options**: Mute all, mute specific players
- **Note**: Mobile voice chat planned for future update

### 21.2 Social Hub (Main Menu)

**Social Menu Tab**

**Friends List**:
- Add friends: Username search, send friend request
- Online status: Green (online), Yellow (away), Gray (offline)
- Last online: "Last seen 3 hours ago"
- Quick actions:
  - Invite to squad
  - Whisper
  - Visit laboratory
  - Remove friend

**Squad System**:
- **Squad size**: 1-4 players
- **Squad leader**: Creates squad, invites members
- **Permissions**: Leader can kick, promote (make co-leader)
- **Ready check**: Leader initiates "Ready?" → all members click ready
- **Matchmaking**: Squad enters queue together (PvE or PvPvE)

**Guild Roster**:
- List all guild members (sorted by rank, then alphabetical)
- Online count: "35 / 150 members online"
- Guild message of the day (MOTD): Displayed at top
- Quick actions:
  - Whisper member
  - Invite to squad
  - View laboratory
  - Promote/demote (officers only)

**Block List**:
- Blocked players cannot:
  - Send messages
  - See your online status
  - Invite to squad
  - Visit your laboratory
- Purpose: Harassment prevention

### 21.3 Content Creator Support

**Streaming Features**

**Streamer Mode** (Toggle in Settings)
- **Hides personal info**: Username replaced with "Streamer", friend list hidden
- **Disables whispers**: Prevents message spam during stream
- **TOS-safe names**: Auto-censors usernames with profanity (prevents Twitch ToS violations)
- **Stream delay warning**: "Streamer Mode Active" watermark (reminds to use OBS delay)

**In-Game Highlights System**
- **Auto-capture**: Records last 30 seconds when:
  - Legendary/Mythic pet captured
  - Boss defeated
  - Event participation
  - Near-death escape (HP below 5%, then survives)
- **Manual capture**: Press keybind (default: F9) to save last 30 seconds
- **Storage**: Saves to `Documents/EternalWilds/Highlights/` (mp4 format, 1080p)
- **Share button**: Upload directly to YouTube, Twitter, Discord (OAuth integration)

**Photo Mode** (Laboratory Base Only)
- **Camera control**: Free camera, rotate 360°, zoom in/out
- **Filters**: Black & white, sepia, vibrant colors, etc.
- **Hide UI**: Toggle to remove all interface elements
- **Pose pets**: Click pet → select animation (sit, stand, roar, sleep)
- **Selfie mode**: Player character poses with pets
- **Save screenshot**: Saves to `Documents/EternalWilds/Screenshots/`

**Creator Code System**
- **Creator codes**: Content creators get unique code ("STREAMER123")
- **Player support**: Players enter code in settings → "Support Creator"
- **Reward**: Creator earns 5% of player's premium currency purchases (paid by game, not player)
- **Player reward**: Player gets exclusive cosmetic nameplate ("Supporter of [Creator]")
- **Purpose**: Incentivize content creation, support creator economy

### 21.4 Official Forums & Community Platforms

**Official Website Forum**

**Forum Categories**:
- **General Discussion**: Open chat about game
- **Guides & Strategies**: Player-written guides, tips
- **Bug Reports**: Technical issues (devs monitor daily)
- **Suggestions & Feedback**: Feature requests (voting system)
- **Trading Post**: Player trade listings (materials, blueprints)
- **Guild Recruitment**: Guilds advertise for members
- **Art & Media**: Fan art, screenshots, videos
- **Off-Topic**: Casual discussion

**Moderation**:
- **Community moderators**: Volunteer players (vetted by dev team)
- **Rules**: No harassment, spam, cheating discussion, NSFW content
- **Infractions**: Warnings → temporary ban → permanent ban

**Dev Presence**:
- Developers post weekly updates (patch notes, upcoming features)
- "Dev Response" tag on threads (developers actively read feedback)
- Monthly AMA (Ask Me Anything) threads

**Official Discord Server**

**Discord Features**:
- 50+ channels (general, help, trading, memes, etc.)
- Voice channels for squad coordination
- LFG (Looking For Group) channel (find squad members)
- Bot commands: `!stats [username]` (pulls player stats), `!wiki [pet]` (links pet info)
- Developer announcements channel (patch notes, events)
- Community events: Screenshot contests, pet naming contests, art competitions

**Subreddit** (r/EternalWilds)
- Community-moderated (not official, but endorsed)
- Daily discussion threads
- Weekly megathreads (trading, guild recruitment, questions)
- Dev team occasionally posts/comments

**Social Media**:
- Twitter: @EternalWilds (daily posts, event announcements)
- Instagram: @EternalWilds_Official (screenshots, art features)
- TikTok: @EternalWilds (short clips, memes)
- YouTube: Official channel (trailers, dev diaries, guides)

### 21.5 Player-Generated Content

**Pet Naming Contests** (Monthly)
- **Theme**: Monthly theme (e.g., "Holiday Pets", "Mythic Legends")
- **Submission**: Players submit pet name ideas (forum thread)
- **Voting**: Community upvotes favorites (top 10 finalists)
- **Winner**: Developers choose from finalists, implement in-game
- **Reward**: Winner gets pet named after them ("Steve's Phoenix"), exclusive title

**Fan Art Showcase**
- **Submission**: Email fan art to community@eternalwilds.com
- **Selection**: Best art featured in-game (Laboratory Base decoration)
- **Reward**: Featured artists get exclusive "Artist" title, premium currency
- **Gallery**: Official website gallery showcases all submissions

**Map Seed Sharing**
- **Community seed database**: Players share expedition seeds
- **Ratings**: Seeds rated for difficulty, loot quality, interesting layouts
- **Featured seeds**: Weekly "Seed of the Week" highlighted on website
- **Leaderboards**: "Best Seeds" by upvotes

**Custom Tournaments** (Community-Organized)
- **PvPvE tournaments**: Community organizes competitive expeditions
- **Prize pools**: Community-funded (premium currency donations)
- **Streaming**: Broadcasted on Twitch (dev team occasionally co-streams)
- **Developer support**: Dev team provides in-game event notifications for major tournaments

---

## 22. LIVE OPERATIONS & CONTENT ROADMAP

### 22.1 Post-Launch Content Schedule

**Month 1-3 (Launch Stabilization)**
- **Weekly hotfixes**: Address critical bugs, balance issues
- **Bi-weekly patches**: QoL improvements, minor content additions
- **Focus**: Stability, player retention, community building

**Month 4-6 (First Major Update)**
- **New biome**: 10th biome added (e.g., "Celestial Observatory" - cosmic theme)
- **New pets**: 20+ new pet types
- **New dungeon types**: 3 new dungeons in new biome
- **Guild update**: Guild wars expanded, new guild rewards
- **QoL**: Enhanced UI, additional accessibility features

**Month 7-9 (Second Major Update)**
- **Seasonal event overhaul**: Permanent seasonal rotation system
- **New game mode**: "Survival Mode" - endless waves, leaderboards
- **Pet balancing**: Major balance pass based on community feedback
- **Crafting expansion**: New gear sets, legendary+ crafting recipes

**Month 10-12 (Year 1 Anniversary)**
- **Anniversary event**: Limited-time celebration (exclusive pets, cosmetics)
- **Endgame content**: New high-difficulty raids (8-player co-op)
- **PvP arena**: Structured PvP mode (ranked ladder)
- **Prestige system**: Post-level 100 progression (covered in Part 8)

**Year 2+ (Long-Term)**
- **Biome expansions**: 2-3 new biomes per year
- **Pet roster expansion**: 50+ new pets per year
- **Seasonal content**: 4 seasons per year (battle passes)
- **Game modes**: New modes every 6 months (e.g., boss rush, time trials)

### 22.2 Patch Cadence & Communication

**Patch Schedule**

**Hotfixes** (As Needed)
- **Frequency**: Within 24-48 hours of critical bugs
- **Scope**: Game-breaking bugs, exploits, server issues
- **Communication**: Twitter post, in-game notification

**Minor Patches** (Bi-Weekly)
- **Frequency**: Every 2 weeks (Tuesdays, 9am PST)
- **Scope**: Bug fixes, balance tweaks, small QoL features
- **Downtime**: 1-2 hours (maintenance window)
- **Communication**: Forum post 24 hours prior, patch notes

**Major Patches** (Every 3 Months)
- **Frequency**: Quarterly (March, June, September, December)
- **Scope**: New content, major features, large balance changes
- **Downtime**: 4-6 hours (extended maintenance)
- **Communication**: Dev blog 1 week prior, trailer, detailed patch notes

**Patch Notes Format**
```
ETERNAL WILDS - PATCH 1.2.3
═══════════════════════════════════════════

NEW CONTENT
- Added 10th biome: Celestial Observatory
- Added 20 new pets (see full list below)
- Added 3 new dungeons

BALANCE CHANGES
- Fire pets: Damage +10% (underperforming)
- Ice pets: Freeze duration -1 second (overperforming)
- Capture rates: Legendary +5% (too difficult)

BUG FIXES
- Fixed: Players could clip through walls in Void Chasm
- Fixed: Pets not respawning correctly during Wave 2
- Fixed: Extraction timer not displaying correctly

QUALITY OF LIFE
- Added: Minimap zoom hotkey (mousewheel)
- Improved: Inventory sorting (auto-sort by rarity)
- Changed: Crafting queues now show estimated completion time

═══════════════════════════════════════════
Full details: www.eternalwilds.com/patch-1-2-3
```

### 22.3 Event Calendar (Live Events)

**Weekly Events** (Rotating)

**Monday: "Mega Spawns"**
- **Effect**: Pet spawn rates +50%, all rarities
- **Purpose**: Easier farming week for casual players

**Tuesday: "Dungeon Delve"**
- **Effect**: Dungeon bosses drop 2x loot
- **Purpose**: Encourage dungeon exploration

**Wednesday: "Capture Bonus"**
- **Effect**: Capture rates +25%
- **Purpose**: Help players fill pet collections

**Thursday: "Crafting Discount"**
- **Effect**: All crafting costs -25% materials
- **Purpose**: Encourage crafting experimentation

**Friday: "PvP Night"**
- **Effect**: PvPvE matchmaking priority, bonus rewards
- **Purpose**: Concentrate PvP population for better matches

**Saturday: "World Event Weekend"**
- **Effect**: World events trigger 2x more frequently
- **Purpose**: Create exciting weekend moments

**Sunday: "Guild Day"**
- **Effect**: Guild XP earned +50%
- **Purpose**: Encourage guild participation

**Monthly Events**

**First Weekend: "Legendary Hunt"**
- **Effect**: Legendary pet spawn rates +100%
- **Duration**: Friday 6pm - Sunday 11:59pm
- **Reward**: Players who capture 5+ legendaries get exclusive title

**Second Weekend: "Extinction Crisis"**
- **Effect**: Extinction waves accelerated (15 min → 10 min intervals)
- **Purpose**: Create intense, fast-paced expeditions

**Third Weekend: "Blood Moon Festival"**
- **Effect**: Permanent Blood Moon event (entire weekend)
- **Purpose**: Dark pet farming event

**Fourth Weekend: "Double XP"**
- **Effect**: All XP sources doubled (player, pet, guild)
- **Purpose**: Help players catch up, popular retention event

**Seasonal Events** (4 per Year)

**Winter (December-February): "Frostfall"**
- **Duration**: 3 months
- **Content**: Winter-themed pets, cosmetics, battle pass
- **Special biome**: Temporary "Eternal Glacier" biome

**Spring (March-May): "Bloom Awakening"**
- **Duration**: 3 months
- **Content**: Nature-themed pets, flower cosmetics, battle pass
- **Special biome**: "Enchanted Grove"

**Summer (June-August): "Sunscorch"**
- **Duration**: 3 months
- **Content**: Fire-themed pets, desert cosmetics, battle pass
- **Special biome**: "Scorched Wastes"

**Fall (September-November): "Harvest Moon"**
- **Duration**: 3 months
- **Content**: Harvest-themed pets, autumn cosmetics, battle pass
- **Special biome**: "Harvest Fields"

### 22.4 Community Feedback Integration

**Feedback Collection Methods**

**In-Game Surveys**
- **Frequency**: Quarterly (after major patches)
- **Format**: 10-question survey (multiple choice + open-ended)
- **Incentive**: 100 premium currency for completion
- **Topics**: Game satisfaction, content preferences, pain points

**Forum Voting System**
- **Suggestion threads**: Players propose features/changes
- **Upvote/downvote**: Community votes on suggestions
- **Developer review**: Top-voted suggestions reviewed monthly
- **Implementation**: High-voted, feasible suggestions added to roadmap

**Discord Polls**
- **Frequency**: Weekly (informal community temperature checks)
- **Topics**: "Which biome should we add next?", "Should we buff Fire pets?"
- **Fast feedback**: Quick yes/no or multiple-choice polls

**Playtesting Program**
- **Public Test Server (PTS)**: Early access to upcoming patches
- **Application**: Players apply to join (limited slots, ~1,000 players)
- **NDA**: Players sign NDA (can test but can't share publicly)
- **Feedback**: Structured feedback forms after testing sessions
- **Reward**: Exclusive "Playtester" title, early cosmetic access

**Developer Transparency**

**Monthly Dev Blog**
- **Format**: Long-form article on website
- **Topics**: Development process, design decisions, roadmap updates
- **Behind-the-scenes**: Art concepts, code snippets, design challenges
- **Community Q&A**: Answers top-voted community questions

**Roadmap Transparency**
- **Public roadmap**: Website page showing planned features (6-month outlook)
- **Status indicators**: "In Development", "Testing", "Coming Soon", "Released"
- **Disclaimer**: "Roadmap subject to change based on feedback and development needs"

---

## 23. ANTI-CHEAT & SECURITY MEASURES

### 23.1 Anti-Cheat System

**Server-Authoritative Design** (Primary Defense)
- **All critical calculations server-side**:
  - Pet spawn locations/timers
  - Damage calculations
  - Loot drops (rarity, quantity)
  - Capture success rates
  - Player position validation (teleport detection)
  - Inventory state
- **Client role**: Rendering, input, prediction only
- **Benefit**: Client cannot manipulate critical values

**Client-Side Validation**
- **Input sanitization**: Reject impossible inputs (e.g., movement speed 1000 studs/sec)
- **Position validation**: Server checks player position every 100ms, teleports back if invalid
- **Action rate limiting**: Max 10 actions per second (prevents macro spam)

**Behavioral Analysis System**
- **Heuristic detection**: Flags suspicious patterns:
  - Perfect capture rates (>90% over 100 attempts = suspicious)
  - Superhuman reaction times (<50ms average = bot-like)
  - Impossible movement (traversing 1,000 studs in 1 second)
  - Perfect dodges (100% dodge rate over 50 attacks = aimbot-like)
- **Machine learning**: AI model trained on cheater behavior (improves over time)
- **Manual review**: Flagged accounts reviewed by anti-cheat team

**Memory Scanning** (PC Only)
- **Detects memory manipulation**: Common cheat engine targets
- **Detects injection**: DLL injection, hooking techniques
- **Privacy-conscious**: Only scans game process memory (not entire system)
- **Warning**: First offense = warning, second = 1-week ban, third = permanent

**Mobile Security**
- **Jailbreak/Root detection**: Refuses to run on compromised devices (security risk)
- **Signature verification**: APK/IPA must be signed by official certificate
- **Encrypted communications**: All client-server traffic encrypted (prevents man-in-the-middle)

### 23.2 Ban System

**Ban Types**

**Chat Bans** (Communication Violations)
- **Duration**: 24 hours → 7 days → 30 days → Permanent
- **Reason**: Harassment, hate speech, spam, toxicity
- **Effect**: Cannot use text chat, all other features accessible
- **Appeal**: Submit ticket to support (reviewed within 48 hours)

**Temporary Bans** (Minor Exploits, First Offenses)
- **Duration**: 3 days → 7 days → 30 days
- **Reason**: Exploiting bugs (non-game-breaking), griefing, offensive names
- **Effect**: Cannot log in at all
- **Appeal**: Submit ticket (reviewed within 7 days)

**Permanent Bans** (Major Violations)
- **Duration**: Forever (account deleted after 6 months)
- **Reason**: Cheating (hacks, bots), RMT (real-money trading), repeated offenses
- **Effect**: Account terminated, cannot create new accounts (IP/HWID ban)
- **Appeal**: Can appeal once within 30 days (rarely overturned)

**Ban Transparency**
- **Email notification**: Player receives email with reason, duration, evidence summary
- **In-game message**: Login screen shows "Account suspended: [reason]"
- **Ban history**: Viewable in account settings (shows all past infractions)

### 23.3 Report System

**In-Game Reporting**
- **Right-click player name**: "Report Player" option
- **Categories**:
  - Cheating/Hacking
  - Harassment/Toxicity
  - Offensive Name/Content
  - Griefing (intentionally ruining experience)
  - RMT (real-money trading, selling accounts)
  - Other (freeform text)
- **Evidence**: Optional screenshot/video upload (encouraged)
- **Confirmation**: "Thank you for reporting. We'll investigate within 48 hours."

**Report Review Process**
1. Report submitted → Enters queue
2. Anti-cheat team reviews (24-48 hour SLA)
3. Evidence examined (chat logs, telemetry data, video)
4. Decision: No action, warning, temporary ban, permanent ban
5. Reporter notified: "Action taken" (doesn't specify what, privacy)

**False Report Protection**
- Players who consistently false-report (>80% reports dismissed) get flagged
- Flagged reporters: Reports deprioritized (reviewed last)
- Malicious false reporting: Can result in ban (abusing system)

---

## 24. DATA ANALYTICS & TELEMETRY

### 24.1 Metrics Collection

**Player Behavior Metrics**
- **Session length**: Average time played per session
- **Retention**: Day 1, Day 7, Day 30 retention rates
- **Churn**: When/why players stop playing
- **Heatmaps**: Where players spend time on map, death locations
- **Drop-off points**: Where players quit (e.g., 80% quit at level 15 = balance issue)

**Economy Metrics**
- **Currency flow**: Income vs spending (inflation tracking)
- **Material supply**: Abundance of each material type
- **Crafting rates**: Which items crafted most/least
- **Trading volume**: Player-to-player trade activity
- **Premium purchases**: What players buy with real money

**Content Engagement**
- **Biome popularity**: Which biomes visited most
- **Dungeon completion rates**: Which dungeons too hard/easy
- **Pet capture rates**: Which pets captured most/least
- **Event participation**: How many players engage with events

**Combat Metrics**
- **Death rates**: Where/when players die most
- **Pet balance**: Win rates, usage rates per pet type
- **Difficulty curves**: Is progression too easy/hard at certain levels

**Privacy & Transparency**
- **Anonymous data**: No personally identifiable information collected
- **Opt-out option**: Players can disable analytics (settings menu)
- **Transparency report**: Annual public report on data collected (builds trust)

### 24.2 A/B Testing

**Controlled Experiments**
- **Split players into groups**: 50% see feature A, 50% see feature B
- **Test examples**:
  - Capture rates: Does +5% increase engagement without reducing challenge?
  - UI changes: Does new inventory layout reduce confusion?
  - Monetization: Does $9.99 battle pass sell better than $10.99?
- **Statistical significance**: Minimum 10,000 players per group, 7-day test duration
- **Winner selection**: Higher engagement/retention/revenue = winning variant

**Ethical Guidelines**
- No predatory tests (e.g., testing if loot boxes increase spending)
- No tests that unfairly advantage/disadvantage players (competitive integrity)
- Transparency: Major tests disclosed in patch notes

---

# ETERNAL WILDS - WORLD & MAP SYSTEM DESIGN DOCUMENT
## Part 10 of 10: Technical Architecture, Development Plan & Conclusion

---

## 25. TECHNICAL ARCHITECTURE SUMMARY

### 25.1 Technology Stack

**Game Engine**
- **Platform**: Roblox Studio
- **Language**: Luau (Roblox's optimized Lua variant)
- **Version**: Latest stable release (updated quarterly)
- **Rationale**: 
  - Cross-platform by default (PC, Mac, iOS, Android, Xbox, PlayStation)
  - Built-in networking and server infrastructure
  - Large existing player base (200M+ monthly active users)
  - No distribution costs (Roblox handles hosting, downloads)

**Server Architecture**

**Backend Services**
- **Game Servers**: Roblox-hosted instances (up to 50 players per server)
- **Database**: Roblox DataStores (persistent player data)
  - Primary: DataStore2 (optimized wrapper, caching, retry logic)
  - Backup: ProfileService (session-locked data, prevents duplication)
- **Memory Store**: Real-time temporary data (expedition state, leaderboards)
- **Messaging Service**: Cross-server communication (global events, announcements)

**External Services**
- **Authentication**: Roblox Account System (OAuth)
- **Payment Processing**: Roblox Developer Exchange (30% platform fee)
- **Analytics**: 
  - Roblox Analytics (built-in, basic metrics)
  - Google Analytics for Games (advanced funnels, cohorts)
- **Customer Support**: Zendesk (ticketing system)
- **Community**: Discord (official server), Discourse (forums)

**Client-Server Architecture**

```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT (Player Device)                │
├─────────────────────────────────────────────────────────┤
│  • Rendering (3D graphics, UI)                          │
│  • Input handling (keyboard, touch, controller)         │
│  • Prediction (movement, animations)                    │
│  • Audio playback                                       │
│  • Local caching (assets, recently visited areas)      │
└─────────────────────────────────────────────────────────┘
                            ↕ (Network - HTTPS/WebSocket)
┌─────────────────────────────────────────────────────────┐
│                  SERVER (Roblox Instance)                │
├─────────────────────────────────────────────────────────┤
│  • World simulation (physics, pet AI, spawns)          │
│  • Authority over game state (HP, inventory, position)  │
│  • Validation (anti-cheat, input sanitization)         │
│  • Persistence (save to DataStore on events)           │
│  • Matchmaking (assign players to instances)           │
└─────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────┐
│                    PERSISTENCE LAYER                     │
├─────────────────────────────────────────────────────────┤
│  • Roblox DataStores (player data, pets, inventory)    │
│  • Memory Store (temporary expedition state)            │
│  • Backup system (hourly snapshots to external DB)     │
└─────────────────────────────────────────────────────────┘
```

**Network Optimization**
- **Update rates** (from Part 7):
  - Players: 20 Hz (50ms)
  - Nearby pets: 10 Hz (100ms)
  - Distant pets: 2 Hz (500ms)
- **Data compression**: Delta encoding (only send changes)
- **Interpolation**: Client smooths movement between updates
- **Prediction**: Client predicts local player movement (corrects on server disagreement)

### 25.2 Code Architecture

**Module Structure** (Organized by System)

```
Game/
├── Client/
│   ├── Controllers/
│   │   ├── InputController.lua (handles all input)
│   │   ├── CameraController.lua (camera management)
│   │   ├── UIController.lua (HUD, menus)
│   │   └── AudioController.lua (sound effects, music)
│   ├── UI/
│   │   ├── HUD.lua (main HUD elements)
│   │   ├── Inventory.lua (inventory UI)
│   │   ├── Map.lua (minimap, full map)
│   │   └── Menus.lua (pause, settings, etc.)
│   └── Utilities/
│       ├── ClientConfig.lua (client-side settings)
│       └── AssetLoader.lua (asset streaming)
│
├── Server/
│   ├── Managers/
│   │   ├── WorldManager.lua (map generation, biome logic)
│   │   ├── SpawnManager.lua (pet spawning, extinction)
│   │   ├── CombatManager.lua (damage calculation, pet AI)
│   │   ├── EventManager.lua (world events, triggers)
│   │   ├── DungeonManager.lua (dungeon generation, bosses)
│   │   └── DataManager.lua (player data persistence)
│   ├── Systems/
│   │   ├── PetSystem.lua (pet stats, breeding, training)
│   │   ├── CraftingSystem.lua (recipes, crafting logic)
│   │   ├── ExtractionSystem.lua (extraction zones, timers)
│   │   ├── WeatherSystem.lua (weather cycles, effects)
│   │   └── ExtinctionSystem.lua (wildlife depletion)
│   └── Utilities/
│       ├── ServerConfig.lua (balance values, spawn rates)
│       ├── MathUtils.lua (RNG, procedural generation)
│       └── ValidationUtils.lua (anti-cheat checks)
│
├── Shared/
│   ├── Data/
│   │   ├── PetData.lua (all pet stats, types)
│   │   ├── BiomeData.lua (biome configs)
│   │   ├── ItemData.lua (items, gear, blueprints)
│   │   └── RecipeData.lua (crafting recipes)
│   ├── Constants.lua (game-wide constants)
│   ├── Enums.lua (enumerations, rarity tiers)
│   └── ReplicatedConfig.lua (shared settings)
│
└── Assets/
    ├── Models/ (3D pet models, environment assets)
    ├── Textures/ (terrain textures, UI sprites)
    ├── Audio/ (SFX, music tracks)
    └── Animations/ (pet animations, player actions)
```

**Design Patterns Used**

**Singleton Pattern** (Managers)
- One instance per manager (WorldManager, SpawnManager, etc.)
- Global access point for systems
- Prevents duplicate initialization

**Observer Pattern** (Events)
- Event-driven architecture (e.g., `PetDefeatedEvent`, `ExtinctionWaveEvent`)
- Decouples systems (CombatManager triggers event, SpawnManager listens)
- Flexible: Easy to add new listeners without modifying core systems

**Object Pool Pattern** (Pet Spawning)
- Pre-instantiate pet objects at server start (pool of 500 pets)
- Reuse objects instead of create/destroy (performance optimization)
- Critical for mobile (reduces garbage collection lag spikes)

**State Machine** (Pet AI)
- Pet states: Idle, Roaming, Aggressive, Fleeing, Dead
- Clean transitions between states
- Easier to debug/balance than spaghetti conditionals

**Factory Pattern** (Procedural Generation)
- BiomeFactory creates biome instances
- DungeonFactory generates dungeon layouts
- Encapsulates complex creation logic

### 25.3 Data Schema

**Player Data Structure** (Saved to DataStore)

```lua
PlayerData = {
    -- Account Info
    UserId = 123456789,
    Username = "PlayerName",
    CreatedAt = 1234567890, -- Unix timestamp
    LastLogin = 1234567890,
    
    -- Progression
    Level = 45,
    XP = 125000,
    ResearchPoints = 750,
    
    -- Currency
    ExpeditionCurrency = 50000,
    PremiumCurrency = 1200,
    GuildPoints = 350,
    
    -- Pets
    PetCollection = {
        {PetID = "ForestWolf_001", Name = "Fang", Level = 30, Stars = 2, ...},
        {PetID = "InfernoDrake_042", Name = "Blaze", Level = 55, Stars = 4, ...},
        -- ... up to 500 pets
    },
    
    -- Inventory
    Materials = {
        {ItemID = "WoodLog", Quantity = 250},
        {ItemID = "FireEssence", Quantity = 45},
        -- ... up to 1000 material slots
    },
    
    Gear = {
        Weapon = {ItemID = "InfernoBlade", Durability = 230/300, Enhancement = 3},
        Armor = {ItemID = "TitanPlate", Durability = 450/500, Enhancement = 2},
        -- ... all gear slots
    },
    
    -- Laboratory
    LabUpgrades = {
        PetHabitat = 2, -- Tier 2 (50 pet display)
        Storage = 3, -- Tier 3 (1000 slots)
        CraftingQueue = 2, -- 3 simultaneous crafts
    },
    
    PetDisplaySlots = {1, 5, 12, 23, ...}, -- Pet IDs displayed in habitat
    
    -- Research Tree
    ResearchUnlocks = {
        "CaptureRate_1", "CaptureRate_2", "PetXPBoost_1", ...
    },
    
    -- Social
    GuildId = "Guild_8472",
    GuildRank = "Veteran",
    FriendsList = {987654321, 123123123, ...}, -- UserIds
    BlockedList = {111222333, ...},
    
    -- Achievements
    Achievements = {
        {ID = "WorldTraveler", UnlockedAt = 1234567890},
        {ID = "BeastSlayer", Progress = 750/1000}, -- In-progress
        -- ... all achievements
    },
    
    -- Statistics
    Stats = {
        TotalExpeditions = 432,
        TotalPetsCaptured = 1205,
        TotalDeaths = 87,
        BossesDefeated = 156,
        -- ... all tracked stats
    },
    
    -- Settings
    Settings = {
        MusicVolume = 0.7,
        SFXVolume = 0.8,
        ColorblindMode = "Deuteranopia",
        Language = "English",
        -- ... all user preferences
    },
    
    -- Seasonal
    SeasonPass = {
        Season = "Winter_2025",
        Tier = 34,
        SeasonXP = 25000,
        ClaimedRewards = {1, 2, 3, ..., 34}, -- Tier numbers
    }
}
```

**Expedition Instance State** (Temporary, Memory Store)

```lua
ExpeditionState = {
    Seed = "EW-2847A", -- Procedural seed
    StartTime = 1234567890,
    Duration = 2700, -- 45 minutes in seconds
    
    -- Players
    Players = {
        {UserId = 123, Position = Vector3.new(100, 0, 200), HP = 80, ...},
        {UserId = 456, Position = Vector3.new(150, 0, 250), HP = 100, ...},
        -- ... up to 40 players (PvPvE)
    },
    
    -- Pet Spawns
    ActivePets = {
        {PetID = "ForestWolf_001", Position = Vector3.new(...), HP = 500, ...},
        -- ... all active pets
    },
    
    ExtinctionWave = 2, -- Current extinction wave (1-4)
    
    -- Events
    ActiveEvents = {
        {Type = "BloodMoon", StartTime = 1234567890, EndTime = 1234568190},
        -- Currently active world events
    },
    
    -- Extraction Zones
    ExtractionZones = {
        {Type = "Early", Position = Vector3.new(...), Active = false, ClosedAt = 1234567890},
        {Type = "Mid", Position = Vector3.new(...), Active = true},
        -- All extraction zones
    },
    
    -- Weather
    CurrentWeather = {
        Biome = "WhisperingForest",
        WeatherType = "HeavyRain",
        StartTime = 1234567890,
        Duration = 600, -- 10 minutes
    }
}
```

### 25.4 Performance Benchmarks

**Target Performance Metrics**

| Platform | FPS Target | Load Time | Network Latency |
|----------|-----------|-----------|-----------------|
| **PC (High-End)** | 60 FPS | <10s | <50ms |
| **PC (Low-End)** | 30 FPS | <20s | <50ms |
| **Mobile (High-End)** | 60 FPS | <15s | <100ms |
| **Mobile (Low-End)** | 30 FPS | <30s | <100ms |
| **Console (Xbox/PS)** | 60 FPS | <15s | <50ms |

**Optimization Strategies**
- **LOD system** (Part 7): Reduces poly count at distance
- **Spatial partitioning** (Part 7): Only simulates nearby sectors
- **Asset streaming** (Part 7): Loads content on-demand
- **Occlusion culling**: Don't render what's behind walls/terrain
- **Texture atlasing**: Combines textures to reduce draw calls
- **Instance batching**: Renders similar objects in single draw call

**Stress Testing**
- **40-player PvPvE**: Maintain 30+ FPS on mobile
- **500+ active pets**: No lag spikes during extinction waves
- **100+ players in Laboratory Base**: Social hub handles traffic
- **Procedural generation**: <3 seconds to generate map on server

---

## 26. DEVELOPMENT MILESTONES & TIMELINE

### 26.1 Development Phases

**Phase 1: Pre-Production (Months 1-3)**

**Milestone 1.1: Core Systems Prototyping** (Month 1)
- Basic player movement and controls
- Simple combat system (player attacks pet)
- Placeholder pet AI (chase and attack)
- Basic inventory system
- **Deliverable**: Vertical slice (5-minute playable demo)

**Milestone 1.2: Procedural Generation Prototype** (Month 2)
- Seed-based map generation (one biome: Whispering Forest)
- Fog of war system
- Spawn point placement algorithm
- **Deliverable**: Generated maps with consistent layouts

**Milestone 1.3: Pet System Foundation** (Month 3)
- Pet stats system (HP, attack, defense, speed)
- Pet capture mechanic
- Pet companion system (follows player, auto-attacks)
- Pet storage/collection UI
- **Deliverable**: Capture and collect 10 placeholder pets

**Phase 2: Alpha Development (Months 4-9)**

**Milestone 2.1: Core Biomes & Combat** (Months 4-5)
- Implement 5 core biomes (Forest, Badlands, Tundra, Swamp, Caverns)
- Expand combat system (dodge, timing mechanics, pet abilities)
- Enemy variety (20 pet types, common to rare)
- **Deliverable**: 30-minute expedition loop with 5 biomes

**Milestone 2.2: Dungeons & Bosses** (Month 6)
- Dungeon generation system (templates + randomization)
- 5 dungeon types (one per biome)
- Boss encounters (unique mechanics per boss)
- **Deliverable**: Playable dungeons with boss fights

**Milestone 2.3: Extraction & Permadeath** (Month 7)
- Extraction zone system (timers, closures)
- Permadeath mechanics (loot loss)
- Base hub (safe zone, crafting, NPCs)
- **Deliverable**: Full expedition cycle with risk/reward

**Milestone 2.4: Pet Progression & Breeding** (Months 8-9)
- Pet leveling and training system
- Star merging system
- Breeding mechanics (elemental compatibility, mutations)
- **Deliverable**: Long-term pet progression loop

**Phase 3: Beta Development (Months 10-15)**

**Milestone 3.1: Laboratory Base** (Months 10-11)
- Personal laboratory instance
- Pet habitat display
- Advanced crafting systems
- Storage and organization
- **Deliverable**: Persistent player hub between expeditions

**Milestone 3.2: High-Tier Content** (Month 12)
- 4 legendary biomes (Volcanic, Void, Storm, Abyssal)
- Legendary and mythic pets
- High-difficulty dungeons
- **Deliverable**: Endgame content for level 50+ players

**Milestone 3.3: Multiplayer & Social** (Months 13-14)
- Squad system (1-4 players, co-op PvE)
- PvPvE mode (20-40 players)
- Guild system (creation, progression, events)
- Trading and mail systems
- **Deliverable**: Full multiplayer experience

**Milestone 3.4: World Events & Weather** (Month 15)
- 6 world events (Blood Moon, Meteor Shower, etc.)
- Dynamic weather system (all biomes)
- Day/night cycle with gameplay impact
- **Deliverable**: Dynamic world with varied conditions

**Phase 4: Polish & Optimization (Months 16-18)**

**Milestone 4.1: UI/UX Polish** (Month 16)
- Finalize HUD design
- Mobile UI optimization
- Accessibility features (colorblind modes, subtitles, etc.)
- Tutorial and onboarding
- **Deliverable**: User-tested, polished interface

**Milestone 4.2: Content Expansion** (Month 17)
- Expand pet roster to 150+ unique types
- Add rare "super elusive" pets
- 20+ dungeons across all biomes
- Legendary gear sets and blueprints
- **Deliverable**: Content-complete game

**Milestone 4.3: Performance & Stability** (Month 18)
- Optimize for low-end mobile devices
- Server load testing (40-player PvPvE stress tests)
- Bug fixing and stability improvements
- Anti-cheat implementation
- **Deliverable**: Launch-ready build

**Phase 5: Soft Launch & Iteration (Months 19-21)**

**Milestone 5.1: Soft Launch** (Month 19)
- Limited release (selected regions: US, UK, Canada)
- 10,000 player cap (controlled scaling)
- Collect feedback and analytics
- **Deliverable**: Live game with active player base

**Milestone 5.2: Iteration Based on Feedback** (Months 20-21)
- Balance patches (pet stats, capture rates, extinction timing)
- QoL improvements (UI tweaks, inventory management)
- Bug fixes (issues discovered during soft launch)
- Content adjustments (difficulty tuning)
- **Deliverable**: Improved game ready for global launch

**Phase 6: Global Launch (Month 22)**

**Milestone 6.1: Global Release**
- Launch in all regions worldwide
- Marketing campaign (trailers, influencer partnerships)
- Day 1 patch (final bug fixes)
- **Deliverable**: Publicly available game

**Milestone 6.2: Post-Launch Support** (Month 22+)
- Weekly hotfixes (critical bugs)
- Bi-weekly patches (balance, QoL)
- Quarterly major updates (new biomes, pets, features)
- Seasonal content (battle passes, events)
- **Deliverable**: Live operations and ongoing support

### 26.2 Development Timeline Visualization

```
ETERNAL WILDS - 22-MONTH DEVELOPMENT TIMELINE
═══════════════════════════════════════════════════════════════

MONTHS 1-3: PRE-PRODUCTION
[■■■] Prototyping, Core Systems, Procedural Generation

MONTHS 4-9: ALPHA DEVELOPMENT
[■■■■■■] Biomes, Combat, Dungeons, Extraction, Pet Progression

MONTHS 10-15: BETA DEVELOPMENT
[■■■■■■] Laboratory Base, Endgame, Multiplayer, Events

MONTHS 16-18: POLISH & OPTIMIZATION
[■■■] UI/UX, Content Expansion, Performance

MONTHS 19-21: SOFT LAUNCH & ITERATION
[■■■] Limited Release, Feedback, Improvements

MONTH 22: GLOBAL LAUNCH
[■] Worldwide Release, Post-Launch Support

═══════════════════════════════════════════════════════════════
Total Development Time: 22 months (approx. 1 year 10 months)
```

---

## 27. TEAM STRUCTURE & ROLES

### 27.1 Core Development Team (Minimum Viable Team)

**Leadership (2 people)**
- **1x Game Director**: Oversees vision, design decisions, final approvals
- **1x Project Manager**: Schedules, milestones, team coordination, budget

**Engineering (5 people)**
- **1x Lead Programmer**: Architecture, code reviews, technical direction
- **2x Gameplay Programmers**: Combat, pets, systems implementation
- **1x Network Programmer**: Multiplayer, server-client communication, anti-cheat
- **1x Tools Programmer**: Editor tools, procedural generation systems

**Design (3 people)**
- **1x Lead Designer**: Systems design, balancing, documentation
- **1x Level Designer**: Biome layouts, dungeon design, world pacing
- **1x Economy Designer**: Progression curves, monetization, balance

**Art (4 people)**
- **1x Art Director**: Visual style, art pipeline, quality control
- **1x 3D Artist**: Pet models, environment assets
- **1x Animator**: Pet animations, combat animations
- **1x UI/UX Artist**: Interface design, iconography, user flows

**Audio (1 person)**
- **1x Audio Designer**: SFX, music composition, audio implementation

**QA (2 people)**
- **1x QA Lead**: Test planning, bug tracking, quality standards
- **1x QA Tester**: Playtesting, bug reporting, regression testing

**Community & Marketing (2 people)**
- **1x Community Manager**: Discord moderation, player feedback, social media
- **1x Marketing Manager**: Launch campaigns, influencer partnerships, PR

**Total Core Team: 19 people**

### 27.2 Extended Team (Full Production Team)

As development progresses, team scales up:

**Months 1-6 (Pre-Production/Early Alpha)**: 10-12 people (core roles only)
**Months 7-12 (Alpha/Early Beta)**: 15-20 people (add QA, community)
**Months 13-18 (Beta/Polish)**: 25-30 people (scale art, QA, engineering)
**Months 19-22 (Soft Launch/Launch)**: 30-35 people (add CS, live ops)
**Post-Launch (Live Operations)**: 20-25 people (maintain, add content team)

**Additional Roles Post-Launch:**
- **3x Customer Support Specialists**: Handle player tickets, issues
- **2x Live Ops Designers**: Seasonal events, limited-time content
- **1x Data Analyst**: Metrics analysis, A/B testing, player behavior
- **1x DevOps Engineer**: Server management, deployment, monitoring

### 27.3 External Contractors & Outsourcing

**Art Outsourcing**
- **3D asset creation**: Outsource 40-60 pet models to external studios
  - Cost: $500-1,000 per pet model (high-quality, animated)
  - Timeline: 2-4 weeks per batch of 10 pets
- **Environment assets**: Outsource decorative props, vegetation
  - Cost: $200-500 per asset pack (10-20 models)

**Audio Outsourcing**
- **Music composition**: Hire composer for 20+ tracks
  - Cost: $1,000-3,000 per track (licensed for game use)
- **SFX**: Purchase from asset libraries (less expensive than custom)
  - Cost: $500-1,000 for comprehensive SFX pack

**Localization**
- **Translation services**: Professional translation for 15 languages
  - Cost: $0.10-0.25 per word x ~50,000 words = $5,000-12,500 per language
  - Total: $75,000-187,500 for all languages

**QA Outsourcing**
- **External QA studio**: Supplement internal QA during crunch
  - Cost: $3,000-5,000 per week (5-10 testers)
  - Used during beta and pre-launch (months 16-21)

---

## 28. BUDGET & RESOURCE ALLOCATION

### 28.1 Estimated Development Budget

**Personnel Costs** (22 Months, Average Team Size: ~20 people)
- **Average salary**: $80,000/year per person (US market, full-time)
- **Team cost**: 20 people x $80,000 x 1.83 years = **$2,928,000**
- **Payroll overhead** (benefits, taxes, etc.): +30% = **$3,806,400**

**Software & Tools**
- **Roblox Studio**: Free (built-in engine)
- **3D modeling**: Blender (free), Maya licenses ($1,620/year x 4 artists) = **$5,940** (22 months)
- **Project management**: Jira, Confluence ($10/user/month x 20) = **$4,400** (22 months)
- **Version control**: GitHub Enterprise ($21/user/month x 20) = **$9,240** (22 months)
- **Communication**: Slack, Discord (free/cheap) = **$1,000** (22 months)
- **Total software**: **~$20,000**

**Art & Audio Outsourcing**
- **3D models**: 60 pets x $750 = **$45,000**
- **Environment assets**: 10 packs x $350 = **$3,500**
- **Music**: 20 tracks x $2,000 = **$40,000**
- **SFX**: Comprehensive pack = **$1,000**
- **Localization**: 15 languages x $8,000 = **$120,000**
- **Total outsourcing**: **~$210,000**

**Marketing & Launch**
- **Trailer production**: Professional game trailer = **$15,000-25,000**
- **Influencer partnerships**: Sponsorships for YouTubers/streamers = **$30,000-50,000**
- **Social media ads**: Facebook, Instagram, TikTok campaigns = **$25,000-40,000**
- **PR agency**: 6-month contract (pre-launch, launch, post-launch) = **$30,000-50,000**
- **Total marketing**: **~$120,000**

**Infrastructure & Operations**
- **Roblox hosting**: Included (Roblox handles server costs)
- **External database backups**: AWS S3 storage = **$500/month x 22 = $11,000**
- **Analytics services**: Google Analytics for Games = **$2,000/year**
- **Customer support tools**: Zendesk ($89/agent/month x 3 agents x 12 months post-launch) = **$3,204**
- **Total infrastructure**: **~$17,000**

**Contingency & Miscellaneous**
- **Unexpected costs**: 10% of total budget = **~$417,000**
- **Office/equipment**: Assuming remote team = **$50,000** (laptops, monitors, peripherals)
- **Legal/accounting**: Contracts, trademarks, taxes = **$30,000**
- **Total contingency**: **~$497,000**

**TOTAL ESTIMATED BUDGET: ~$4,670,000**

### 28.2 Revenue Model & Break-Even Analysis

**Revenue Streams**

**Premium Currency Sales**
- **Average revenue per paying user (ARPPU)**: $15-25 (industry average for Roblox games)
- **Conversion rate**: 2-5% of players make purchases (conservative estimate)
- **Expected player base**: 100,000 MAU (monthly active users) at launch, growing to 500,000+ within 6 months

**Revenue Projections (First Year Post-Launch)**

**Month 1-3 (Launch Period)**
- **Players**: 100,000 MAU
- **Paying players**: 2,500 (2.5% conversion)
- **Revenue**: 2,500 x $20 ARPPU = **$50,000/month**
- **3-month total**: **$150,000**

**Month 4-6 (Early Growth)**
- **Players**: 200,000 MAU (word-of-mouth, content updates)
- **Paying players**: 5,000 (2.5% conversion)
- **Revenue**: 5,000 x $20 = **$100,000/month**
- **3-month total**: **$300,000**

**Month 7-9 (Established Growth)**
- **Players**: 350,000 MAU
- **Paying players**: 10,500 (3% conversion, increased engagement)
- **Revenue**: 10,500 x $22 = **$231,000/month**
- **3-month total**: **$693,000**

**Month 10-12 (Mature Phase)**
- **Players**: 500,000 MAU
- **Paying players**: 17,500 (3.5% conversion)
- **Revenue**: 17,500 x $25 = **$437,500/month**
- **3-month total**: **$1,312,500**

**First Year Total Revenue (Post-Launch)**: **~$2,455,500**

**Roblox Platform Fee**: 30% = **-$736,650**

**Net Revenue (First Year)**: **~$1,718,850**

**Break-Even Analysis**
- **Development cost**: $4,670,000
- **First year net revenue**: $1,718,850
- **Break-even timeline**: ~2.7 years at current trajectory
- **Accelerated scenario** (viral growth, 1M+ MAU): Break-even within 18 months

**Sustainability**
- **Live ops team cost**: ~$2M/year (20-25 people)
- **Required revenue to sustain**: ~$2.9M/year (after Roblox fee)
- **Required MAU**: ~400,000 at 3% conversion, $23 ARPPU (achievable with good retention)

---

## 29. RISK ASSESSMENT & MITIGATION

### 29.1 Technical Risks

**Risk 1: Roblox Platform Limitations**
- **Description**: Roblox engine may not handle complex procedural generation or 40-player servers well
- **Probability**: Medium (Roblox continuously improves, but has known constraints)
- **Impact**: High (could require major architecture changes)
- **Mitigation**:
  - Early prototyping (test procedural generation in Month 2)
  - Stress testing throughout development (40-player tests in Month 13)
  - Fallback plan: Reduce player count to 20 per server if performance issues
  - Alternative: Simplify procedural generation (fewer biomes, simpler layouts)

**Risk 2: Mobile Performance Issues**
- **Description**: Low-end mobile devices struggle with complex 3D world
- **Probability**: Medium-High (mobile is notoriously difficult to optimize)
- **Impact**: High (50%+ of Roblox players are mobile)
- **Mitigation**:
  - Aggressive LOD system (Part 7)
  - Graphics settings auto-detection (low/medium/high presets)
  - Regular mobile device testing (test on iPhone X, Samsung S8, budget Androids)
  - Fallback: Disable certain visual effects on low-end devices

**Risk 3: Network Latency & Lag**
- **Description**: High-latency players (200ms+) have poor experience
- **Probability**: Medium (inevitable with global player base)
- **Impact**: Medium (affects PvPvE more than PvE)
- **Mitigation**:
  - Client-side prediction (smooth movement despite lag)
  - Generous hitboxes for combat (reduces "I dodged but still got hit" complaints)
  - Regional servers (Roblox handles this automatically, but can request specific routing)
  - Lag compensation techniques (favor shooter in PvP)

### 29.2 Design Risks

**Risk 1: Permadeath Too Punishing**
- **Description**: Players quit due to frustration from losing hours of progress
- **Probability**: High (permadeath is divisive mechanic)
- **Impact**: High (directly affects retention)
- **Mitigation**:
  - Soft launch testing (gather feedback in Month 19)
  - "Secure slot" for pets (never lose captured pets, covered in Part 1)
  - Insurance system for gear (premium item to recover lost gear)
  - Difficulty assist options (lose 50% instead of 100%, for accessibility)
  - Iterate based on data: If churn spikes after deaths, reduce penalty

**Risk 2: Extinction Mechanic Too Confusing**
- **Description**: Players don't understand why pets are disappearing
- **Probability**: Medium (novel mechanic, requires explanation)
- **Impact**: Medium (confusion = negative reviews)
- **Mitigation**:
  - Clear tutorial explaining extinction (Part 9)
  - Visual/audio warnings before each wave (Part 4)
  - UI indicators showing remaining spawns (Part 4)
  - Optional "Classic Mode" without extinction (for players who want traditional hunting)

**Risk 3: Endgame Content Insufficient**
- **Description**: Level 100 players run out of things to do, quit
- **Probability**: Medium (common issue in games)
- **Impact**: High (lose most engaged players)
- **Mitigation**:
  - Prestige system (Part 8) for infinite progression
  - Monthly leaderboards (always competing)
  - Regular content updates (new biomes, pets every 3 months)
  - Guild events provide repeatable endgame

### 29.3 Business Risks

**Risk 1: Roblox Algorithm Changes**
- **Description**: Roblox changes discovery algorithm, game loses visibility
- **Probability**: Medium (Roblox frequently updates platform)
- **Impact**: High (could tank player acquisition)
- **Mitigation**:
  - Build community outside Roblox (Discord, YouTube, TikTok)
  - Incentivize word-of-mouth (referral rewards)
  - Diversify traffic sources (not reliant on Roblox homepage alone)
  - Maintain high engagement (Roblox algorithm favors games with good retention)

**Risk 2: Competitor Launches Similar Game**
- **Description**: Another team releases pet collection extraction game first
- **Probability**: Medium-Low (niche genre, but possible)
- **Impact**: Medium (first-mover advantage important)
- **Mitigation**:
  - Differentiation: Unique extinction mechanic, procedural generation, ethical monetization
  - Quality over speed: Better to launch polished than rushed
  - Leverage strengths: If competitor launches, analyze weaknesses and improve on them

**Risk 3: Revenue Underperforms**
- **Description**: Players don't spend enough, game unprofitable
- **Probability**: Medium (monetization is always uncertain)
- **Impact**: High (can't sustain live ops, game shuts down)
- **Mitigation**:
  - Multiple monetization avenues (cosmetics, convenience, battle pass)
  - A/B test pricing (optimize for conversion, not just ARPPU)
  - Generous free content (retain non-payers who populate servers)
  - Fallback: Premium subscription model ($5/month for 10% XP boost, monthly currency)

### 29.4 Team Risks

**Risk 1: Key Personnel Leave**
- **Description**: Lead programmer, game director, or other critical role quits mid-development
- **Probability**: Medium (common in game industry)
- **Impact**: Very High (delays, knowledge loss)
- **Mitigation**:
  - Comprehensive documentation (all systems documented, not tribal knowledge)
  - Cross-training (multiple people understand each system)
  - Competitive compensation (reduce turnover likelihood)
  - Succession planning (identify potential replacements early)

**Risk 2: Scope Creep**
- **Description**: Team keeps adding features, never finishes game
- **Probability**: High (very common in development)
- **Impact**: High (budget overruns, missed deadlines)
- **Mitigation**:
  - Strict milestone reviews (reject features not on roadmap)
  - "Post-launch" feature list (good ideas delayed to updates)
  - Project manager enforces scope (empowered to say "no")
  - Monthly scope reviews (cut low-priority features if behind schedule)

**Risk 3: Burnout**
- **Description**: Team overworked, morale drops, productivity plummets
- **Probability**: Medium-High (especially near launch)
- **Impact**: High (quality suffers, people quit)
- **Mitigation**:
  - Realistic schedules (no mandatory crunch)
  - Buffer time in timeline (22 months includes cushion)
  - Regular breaks (mandatory PTO, no "hero" culture)
  - Mental health support (counseling services available)

---

## 30. SCALABILITY & LONG-TERM MAINTENANCE

### 30.1 Infrastructure Scalability

**Handling Growth** (100K → 1M+ Players)

**Roblox Auto-Scaling**
- Roblox automatically spins up new server instances as player count increases
- No manual intervention required (platform handles load balancing)
- Cost scales with player count (Roblox takes 30% revenue, handles expenses)

**Database Optimization**
- **Sharding**: Split player data across multiple DataStores (by UserId range)
  - Example: Users 0-1M in DataStore1, 1M-2M in DataStore2, etc.
- **Caching**: Use Memory Store for frequently accessed data (leaderboards, guild rosters)
- **Batch writes**: Group multiple database saves into single transaction (reduces load)

**Content Delivery**
- **Asset caching**: Roblox CDN caches 3D models, textures globally
- **Progressive loading**: Load critical assets first, stream rest in background
- **Mobile optimization**: Lower-res assets served to mobile clients automatically

### 30.2 Content Roadmap Sustainability

**Quarterly Major Updates** (Year 1+)
- **Q1**: New biome (10th biome), 20 new pets, 3 dungeons
- **Q2**: New game mode (Survival Mode), balance pass, QoL features
- **Q3**: Endgame raids (8-player co-op), new legendary pets, gear sets
- **Q4**: PvP arena (ranked ladder), new biomes, anniversary event

**Live Ops Team Capacity**
- **2x Live Ops Designers**: Create weekly events, seasonal content
- **1x Content Artist**: New pets, cosmetics (ongoing)
- **1x Level Designer**: New dungeons, biomes (ongoing)
- **Estimated output**: 40-50 new pets/year, 2-3 new biomes/year, 10+ dungeons/year

**Community Content**
- **Pet design contests**: Community submits designs, winners implemented (low dev cost)
- **Map seed curation**: Community finds interesting seeds, developers feature them
- **Moderation tools**: Empower community moderators to handle minor issues (scales well)

### 30.3 Technical Debt Management

**Refactoring Cadence**
- **Monthly code reviews**: Identify areas needing cleanup
- **Quarterly refactoring sprints**: Dedicate 1 week per quarter to improving code quality
- **Deprecation schedule**: Remove old, unused systems every 6 months

**Documentation Maintenance**
- **Living design docs**: Update design docs with every major feature change
- **Code comments**: Enforce comment standards (what, not how)
- **Onboarding guides**: Keep new developer onboarding materials up-to-date

**Version Control**
- **Semantic versioning**: Major.Minor.Patch (e.g., 1.3.5)
- **Release branches**: Separate branch for live game, development on main branch
- **Hotfix process**: Critical fixes bypass normal approval (emergency only)

---

## 31. SUCCESS METRICS & KPIs

### 31.1 Player Engagement Metrics

**Retention**
- **Day 1 Retention**: Target **40%+** (industry average: 25-35%)
- **Day 7 Retention**: Target **20%+** (industry average: 10-15%)
- **Day 30 Retention**: Target **10%+** (industry average: 5-8%)

**Session Metrics**
- **Average session length**: Target **30+ minutes** (depth over breadth)
- **Sessions per day**: Target **2-3 sessions** (habitual engagement)
- **Daily Active Users (DAU)**: Target **30-40%** of MAU

**Progression Metrics**
- **Tutorial completion rate**: Target **70%+** (onboarding effectiveness)
- **Time to level 10**: Target **3-5 hours** (smooth early game)
- **Percentage reaching endgame (level 50+)**: Target **15%+** (healthy endgame)

### 31.2 Monetization Metrics

**Conversion**
- **Paying user conversion**: Target **3-5%** (reasonable for free-to-play)
- **Repeat purchase rate**: Target **40%+** (of paying users buy again)

**Revenue**
- **ARPU** (Average Revenue Per User): Target **$0.50-1.00** (includes non-payers)
- **ARPPU** (Average Revenue Per Paying User): Target **$20-30** (higher than ARPU)
- **Lifetime Value (LTV)**: Target **$5-10 per player** (over 12 months)

**Revenue Mix**
- **Cosmetics**: Target **50-60%** of revenue (non-pay-to-win)
- **Convenience**: Target **20-30%** (instant crafting, storage expansions)
- **Battle Pass**: Target **15-20%** (seasonal content)
- **Premium Items**: Target **5-10%** (resurrection scrolls, safe enhancement)

### 31.3 Community Health Metrics

**Social Engagement**
- **Guild membership rate**: Target **40%+** of active players
- **Friend list size**: Target **5+ friends per player** (social graph density)
- **Co-op participation**: Target **30%+** of expeditions are squad-based

**Content Creation**
- **YouTube videos**: Target **1,000+ videos** within 6 months of launch
- **Twitch streams**: Target **50+ concurrent streamers** regularly
- **Fan art submissions**: Target **100+ pieces per month** (community creativity)

**Support Metrics**
- **Ticket resolution time**: Target **<48 hours** average
- **Player satisfaction**: Target **80%+** positive support interactions
- **Ban rate**: Target **<1%** of players (low toxicity, good moderation)

### 31.4 Technical Performance Metrics

**Client Performance**
- **Average FPS**: Target **45+ FPS** on mobile (stable experience)
- **Load time**: Target **<20 seconds** on mobile (acceptable wait)
- **Crash rate**: Target **<1%** of sessions (stability)

**Server Performance**
- **Server uptime**: Target **99.5%+** (minimal downtime)
- **Average latency**: Target **<100ms** for 80% of players
- **Data loss incidents**: Target **0** (perfect data integrity)

---

## 32. FINAL SUMMARY & CONCLUSION

### 32.1 Executive Summary

**Eternal Wilds** is an ambitious **pet collection extraction game** set in a procedurally generated wilderness where players hunt, capture, and train creatures while managing the tension between risk (permadeath) and reward (rare loot). The game innovates within the extraction genre by:

1. **Procedural Generation**: Every expedition features a unique map layout via seed-based generation, ensuring fresh exploration
2. **Wildlife Extinction Mechanic**: Dynamic spawn depletion creates organic time pressure without artificial zones
3. **Ethical Monetization**: Cosmetic and convenience-focused premium items, zero pay-to-win
4. **Mobile-First Design**: Optimized for touchscreens while maintaining depth for PC/console players
5. **Long-Term Progression**: Pet breeding, crafting, guilds, and seasonal content support years of engagement

### 32.2 Core Value Propositions

**For Players:**
- **Skill-Based Gameplay**: Timing-based combat rewards mastery, not wallet size
- **Meaningful Choices**: Risk vs reward decisions every moment (extract or push deeper?)
- **Collection Goals**: 150+ unique pets to capture, train, and breed
- **Social Features**: Guilds, co-op, trading create lasting friendships
- **Replayability**: Procedural generation ensures no two expeditions identical

**For Investors/Stakeholders:**
- **Proven Market**: Extraction games (Tarkov, Hunt Showdown) and pet games (Pokémon, Palworld) both demonstrate strong demand
- **Sustainable Model**: Ethical monetization supports long-term revenue without alienating players
- **Scalable Platform**: Roblox infrastructure handles growth from 10K to 10M+ players
- **Community-Driven**: Player-generated content and live ops extend game lifespan indefinitely
- **Break-Even Path**: Conservative projections show profitability within 2-3 years

### 32.3 Why This Game Will Succeed

**1. Unique Positioning**
- **No direct competitors**: First major extraction game with pet collection mechanics on Roblox
- **Differentiated from Pokémon**: Permadeath stakes, procedural worlds, multiplayer focus
- **Differentiated from Tarkov**: Accessible controls, pet progression, non-toxic monetization

**2. Strong Foundation**
- **22 months of development**: Adequate time to build polished, feature-complete game
- **Experienced team**: 19-35 person team with clear roles and responsibilities
- **Robust documentation**: This 10-part design document ensures alignment and clarity

**3. Player-First Design**
- **Accessibility**: Colorblind modes, subtitles, difficulty assists welcome all players
- **Fairness**: No pay-to-win preserves competitive integrity
- **Respect for Time**: Secure pet slots, insurance options reduce frustration

**4. Sustainable Live Ops**
- **Content Roadmap**: Quarterly updates, seasonal content, monthly events
- **Community Engagement**: Active Discord, forums, creator support program
- **Responsive Development**: Player feedback integrated via surveys, playtesting, data analysis

### 32.4 Critical Success Factors

To achieve success, the team must:

1. **Hit Milestones**: Stay on schedule (22-month timeline), avoid scope creep
2. **Maintain Quality**: Polish over quantity, especially for mobile experience
3. **Listen to Players**: Soft launch feedback is critical for tuning balance
4. **Build Community**: Invest in Discord, forums, content creators early
5. **Iterate Relentlessly**: No game is perfect at launch; be ready to adapt

### 32.5 Final Word

**Eternal Wilds represents a bold vision**: a game that respects players' time, skill, and intelligence while delivering thrilling high-stakes gameplay. By combining the best elements of extraction shooters, pet collection RPGs, and survival games, we're creating something truly unique in the Roblox ecosystem.

The journey from concept to launch will be challenging—procedural generation is complex, mobile optimization is demanding, and balancing permadeath is delicate. But with a talented team, comprehensive planning, and unwavering commitment to player experience, **Eternal Wilds can become a flagship title that defines a new genre on Roblox**.

**The wilds await. Let's build something eternal.**

---

## 33. APPENDICES

### Appendix A: Glossary of Terms

- **ARPPU**: Average Revenue Per Paying User
- **ARPU**: Average Revenue Per User
- **DAU**: Daily Active Users
- **Extinction Mechanic**: System where pet spawns gradually disappear over expedition duration
- **FTUE**: First-Time User Experience (tutorial/onboarding)
- **LOD**: Level of Detail (graphics optimization technique)
- **MAU**: Monthly Active Users
- **PvE**: Player vs Environment (solo/co-op against AI)
- **PvPvE**: Player vs Player vs Environment (multiplayer with both PvP and PvE)
- **QoL**: Quality of Life (usability improvements)
- **RNG**: Random Number Generator (procedural randomness)
- **Seed**: Code that determines procedurally generated map layout
- **Stud**: Roblox unit of measurement (1 stud ≈ 1 foot)

### Appendix B: Reference Documents

This design document references:
- **COMBAT_SYSTEM_DESIGN.md**: Combat mechanics, pet abilities, timing system
- **MULTIPLAYER_COMBAT_SYSTEM_DESIGN.md**: PvP, squad mechanics, anti-griefing
- **PET_SYSTEM_DESIGN_DOCUMENT.md**: Pet stats, breeding, training, progression

### Appendix C: Change Log

**Version 1.0** (December 17, 2025)
- Initial comprehensive design document
- 10 parts covering all major systems
- Ready for development kickoff

---


