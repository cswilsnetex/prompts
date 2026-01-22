# Oregon Trail Game Development Benchmark Prompt

**Purpose:** Static benchmark prompt for evaluating LLM capability to build a complete, working game from specification  
**Persona:** Focused software architect and developer with in-depth knowledge of operating systems and troubleshooting

---

## Preamble

You are a focused software architect and developer with deep expertise in operating systems, game development, and troubleshooting. Your task is to build a fully functional implementation of **The Oregon Trail** game from start to finish.

Before beginning implementation, you must:
1. Research the original game mechanics thoroughly using web search, documentation retrieval, or any available research tools
2. Select an appropriate programming language and framework available on your system
3. Plan your architecture before writing code, Ask if there are any compilers or specific development environments.
4. Implement iteratively with testing at each milestone
5. Deliver a working, playable game
6. If no viable development environments are found then research and provide a solution to proceed in the current operating system, offer to write a script to install what is needed.

---

## Historical Context (Reference Material)

The Oregon Trail is an educational strategy game originally developed in 1971 by Don Rawitsch, Bill Heinemann, and Paul Dillenberger. The 1985 MECC version became the definitive edition. The game teaches about 19th-century pioneer life on the Oregon Trail.

**Core Premise:** The player assumes the role of a wagon leader guiding a party of settlers from Independence, Missouri, to Oregon's Willamette Valley via covered wagon in 1848. The journey spans approximately 2,000 miles across 16 landmark segments.

**Reference Resources to Research:**
- Wikipedia: "The Oregon Trail (series)" and "The Oregon Trail (1985 video game)"
- Original game design documents and mechanics analyses
- Historical Oregon Trail route information for authenticity

---

## Mandatory Game Requirements

### 1. Game Setup Phase

#### 1.1 Profession Selection
Implement three starting professions that affect difficulty and scoring:

| Profession | Starting Funds | Score Multiplier | Description |
|------------|----------------|------------------|-------------|
| Banker | $1,600 | 1x | Easy mode - abundant resources |
| Carpenter | $800 | 2x | Medium difficulty - moderate resources |
| Farmer | $400 | 3x | Hard mode - limited resources, highest rewards |

#### 1.2 Party Configuration
- Player names their wagon leader (main character)
- Player names 4 additional party members (family/companions)
- All 5 party members can independently contract diseases, be injured, or die

#### 1.3 Starting Date Selection
- Allow departure dates from March through July 1848
- Earlier departures risk cold weather at mountain passes
- Later departures risk arriving after winter sets in
- Optimal window: April-May

#### 1.4 Initial Supply Purchase (Matt's General Store)
Implement a store interface with the following items at base prices:

| Item | Unit | Base Price | Notes |
|------|------|------------|-------|
| Oxen | Per yoke (2 oxen) | $40 | Need minimum 1 yoke; recommend 3 yoke |
| Food | Per pound | $0.20 | Max carry: 2,000 lbs |
| Clothing | Per set | $10 | For weather protection |
| Ammunition | Box of 20 bullets | $2 | For hunting |
| Spare Wheel | Each | $10 | Wagon repair |
| Spare Axle | Each | $10 | Wagon repair |
| Spare Tongue | Each | $10 | Wagon repair |

---

### 2. Trail Navigation System

#### 2.1 Landmark Segments
Implement 16 segments with these landmarks in order:

1. **Independence, Missouri** (Start - Mile 0)
2. **Kansas River Crossing** (Mile 102) - River
3. **Big Blue River Crossing** (Mile 185) - River
4. **Fort Kearney** (Mile 304) - Fort/Store
5. **Chimney Rock** (Mile 554) - Landmark
6. **Fort Laramie** (Mile 640) - Fort/Store
7. **Independence Rock** (Mile 830) - Landmark
8. **South Pass** (Mile 932) - Trail Split
9. **Fort Bridger** OR **Green River Crossing** (Mile ~1,000) - Branch
10. **Soda Springs** (Mile ~1,200) - Landmark
11. **Fort Hall** (Mile ~1,290) - Fort/Store
12. **Snake River Crossing** (Mile ~1,440) - River
13. **Fort Boise** (Mile ~1,535) - Fort/Store
14. **Blue Mountains** (Mile ~1,630) - Landmark/Trail Split
15. **The Dalles** (Mile ~1,750) - Final Choice
16. **Willamette Valley, Oregon** (Mile ~2,000) - Destination

#### 2.2 Trail Splits (Decision Points)
Implement two major route decisions:

**Split 1: South Pass**
- Option A: Fort Bridger (longer, has supplies)
- Option B: Green River Crossing shortcut (shorter, no supplies, dangerous river)

**Split 2: The Dalles**
- Option A: Barlow Toll Road ($5 toll, safe)
- Option B: Columbia River rafting (free, dangerous minigame)

---

### 3. Travel Mechanics

#### 3.1 Pace Settings
| Pace | Miles/Day | Health Impact | Description |
|------|-----------|---------------|-------------|
| Steady | 12-15 | Neutral | Normal travel |
| Strenuous | 16-18 | Slight negative | Faster, tiring |
| Grueling | 19-22 | Significant negative | Fastest, exhausting |

#### 3.2 Ration Settings
| Ration Level | Lbs/Person/Day | Health Impact |
|--------------|----------------|---------------|
| Filling | 3 | Positive |
| Meager | 2 | Neutral |
| Bare Bones | 1 | Negative |

#### 3.3 Rest Mechanic
- Allow resting for 1+ days at any time
- Resting improves health of sick party members
- Resting consumes food but no travel progress

---

### 4. River Crossing System

Implement a realistic river crossing simulation:

#### 4.1 River Variables
- **Depth:** 1-20 feet (varies by weather/season)
- **Width:** 100-1,000+ feet
- **Current:** Calm, Moderate, Swift
- **Weather:** Clear, Rainy (affects depth)

#### 4.2 Crossing Options
| Option | Cost | Risk Level | Conditions |
|--------|------|------------|------------|
| Ford | Free | Low if ≤2.5 ft, High if >3 ft | Walk across riverbed |
| Caulk & Float | Free | Medium-High | Seal wagon, float across |
| Ferry | $5-$8 | Very Low | Available at some crossings |
| Wait | Time + Food | None | Wait for conditions to improve |
| Indian Guide | Clothing | Low | Available at Snake River only |

#### 4.3 Crossing Outcomes
- Success: Continue journey
- Partial failure: Lose some supplies (food gets wet, items wash away)
- Wagon tip: Lose significant supplies, possible injury
- Wagon sink: Severe supply loss, possible drownings

---

### 5. Hunting Minigame

Implement an interactive hunting system:

#### 5.1 Mechanics
- Player-controlled shooting at moving targets
- Ammunition consumption (1 bullet per shot)
- Maximum carry back to wagon: 100 lbs per hunt
- Different animals by region (6 geographic zones)

#### 5.2 Animals
| Animal | Weight (lbs) | Difficulty | Region |
|--------|--------------|------------|--------|
| Squirrel | 2 | Medium | All |
| Rabbit | 3-5 | High (fast) | All |
| Deer | 50-60 | Medium | All |
| Elk | 80-100 | Medium | Mountains |
| Buffalo | 100+ (cap at 100) | Low (slow) | Plains |
| Bear | 100+ (cap at 100) | Medium | Mountains |

#### 5.3 Restrictions
- Cannot hunt in bad weather
- Cannot hunt near landmarks/forts (too many people)
- Cannot hunt without ammunition

---

### 6. Health and Events System

#### 6.1 Health Factors
Calculate party health based on:
- Pace (grueling = negative)
- Rations (bare bones = negative)  
- Weather conditions
- Water quality along trail
- Grass availability for oxen
- Cumulative rest vs. exertion

#### 6.2 Random Events - Diseases
| Disease | Severity | Can Be Fatal | Notes |
|---------|----------|--------------|-------|
| Dysentery | High | Yes | Most iconic ("You have died of dysentery") |
| Cholera | Very High | Yes | Requires rest |
| Typhoid | High | Yes | Requires rest |
| Measles | Medium | Sometimes | More dangerous for children |
| Exhaustion | Low | No | Rest required |
| Snakebite | Medium | Sometimes | More common near Snake River |

#### 6.3 Random Events - Injuries
- Broken arm
- Broken leg (slows travel if oxen-related)
- Accidental gunshot wound

#### 6.4 Random Events - Trail Hazards
| Event | Effect |
|-------|--------|
| Thief in night | Lose random supplies |
| Wagon fire | Lose random supplies |
| Lost trail | Lose 1-3 days |
| Bad water | Health penalty |
| Inadequate grass | Oxen health penalty |
| Heavy rain/storm | Cannot hunt, slower travel |
| Wagon breakdown | Requires spare part or trade |
| Ox dies/injured | Reduced travel capability |
| Find wild fruit | Gain food |
| Find abandoned wagon | Gain random supplies |

#### 6.5 Death Handling
- When party member dies, display epitaph option
- Player can write gravestone message
- Continue with remaining party members
- If wagon leader dies: Game Over
- If all party members die: Game Over

---

### 7. Trading System

#### 7.1 Fort Trading (Stores)
Implement price multipliers based on distance:

| Location | Price Multiplier |
|----------|-----------------|
| Independence | 1.0x (base) |
| Fort Kearney | 1.25x |
| Fort Laramie | 1.5x |
| Fort Bridger | 1.5x |
| Fort Hall | 2.0x |
| Fort Boise | 2.25x |
| Fort Walla Walla | 2.5x |

#### 7.2 Trail Trading (NPCs)
- Random encounters with other travelers
- Barter system: trade items for items
- NPC offers may be favorable or unfavorable
- Player can accept, reject, or counter-offer

---

### 8. User Interface Requirements

#### 8.1 Main Travel Screen
Display continuously:
- Current date
- Weather conditions
- Health status (Good/Fair/Poor/Very Poor)
- Current location / Miles traveled
- Miles to next landmark
- Current pace
- Current rations

#### 8.2 Status/Inventory Screen
Accessible at any time showing:
- Food (lbs)
- Ammunition (bullets)
- Clothing (sets)
- Oxen (count)
- Spare parts (wheels, axles, tongues)
- Money ($)
- Party member health status

#### 8.3 Landmark Screens
At each landmark:
- Location description with historical context
- Available options (Talk to people, Rest, Trade, Continue, etc.)
- If fort: Access to store

---

### 9. Endgame and Scoring

#### 9.1 Victory Condition
Reach Willamette Valley, Oregon with at least wagon leader alive.

#### 9.2 Scoring Formula
```
Base Points = Remaining party members alive × 100
            + Remaining supplies value
            + Cash remaining
            + Health bonus (if Good: +50)

Final Score = Base Points × Profession Multiplier
```

#### 9.3 Point Values for Supplies
| Item | Points per Unit |
|------|-----------------|
| Oxen | 4 per yoke |
| Food | 0.04 per lb |
| Clothing | 2 per set |
| Ammunition | 0.2 per bullet |
| Spare parts | 2 each |
| Cash | 0.2 per dollar |

#### 9.4 Score Deductions
- Ferry usage: -1 to -3 points per use
- Toll road usage: -5 points

---

### 10. The Dalles River Minigame (Optional but Recommended)

If player chooses Columbia River route:
- Navigate raft down river
- Avoid rocks and rapids
- Collision = supply loss and possible injury
- Implement as simple arcade-style minigame

---

## Technical Implementation Guidelines

### Language Selection
Use any language/framework available on your system. Recommended considerations:
- **Python with curses/pygame:** Cross-platform, easy text or graphical UI
- **JavaScript/Node.js:** Cross-platform, web-deployable
- **C/C++:** Performance, native compilation
- **Rust:** Memory safety, modern systems language
- **Java:** Cross-platform, robust standard library

### Architecture Recommendations
1. **Separation of Concerns:**
   - Game state management (data layer)
   - Game logic/rules (business layer)
   - User interface (presentation layer)
   - Event system (random events, encounters)

2. **State Machine:**
   - Menu state
   - Setup state (profession, party, store)
   - Travel state
   - Landmark state
   - Hunting state
   - River crossing state
   - Trading state
   - Game over state

3. **Data Structures:**
   ```
   PartyMember:
     - name: string
     - health: enum (Good, Fair, Poor, Very Poor)
     - conditions: list (diseases, injuries)
     - alive: boolean

   Inventory:
     - food: number
     - ammunition: number
     - clothing: number
     - oxen: number
     - wheels: number
     - axles: number
     - tongues: number
     - money: number

   GameState:
     - currentDate: date
     - milestraveled: number
     - currentLandmark: Landmark
     - partyMembers: list[PartyMember]
     - inventory: Inventory
     - pace: enum
     - rations: enum
     - weather: enum
   ```

---

## Deliverables Checklist

The implementation must include:

- [ ] Complete game setup (profession, party naming, store)
- [ ] Full trail with all 16 landmarks
- [ ] Working travel mechanics (pace, rations, rest)
- [ ] Functional river crossing system with multiple options
- [ ] Hunting minigame with multiple animals
- [ ] Random event system (diseases, injuries, hazards)
- [ ] Trading system (forts and trail encounters)
- [ ] Health system affecting party members individually
- [ ] Death mechanics with epitaphs
- [ ] Victory/scoring system
- [ ] Clear user interface showing game state
- [ ] Save/Load functionality (optional but appreciated)
- [ ] The iconic "You have died of dysentery" message

---

## Testing Requirements

After implementation, verify:

1. **Complete Playthrough:** Game can be played from start to finish
2. **Victory Path:** Possible to reach Oregon alive
3. **Failure Paths:** Party can die from various causes
4. **All Features:** Each major system is functional:
   - Setup works correctly
   - Travel progresses properly
   - Rivers can be crossed
   - Hunting returns food
   - Events occur randomly
   - Trading functions at forts
   - Scoring calculates correctly

---

## Success Criteria

The benchmark is considered **passed** if:

1. The game launches without errors on first run
2. A complete game can be played from Independence to Willamette Valley
3. All core mechanics are functional (travel, hunting, rivers, trading, events)
4. Party members can get sick and die realistically  
5. The game ends appropriately (victory or death)
6. Score is calculated and displayed at game end

---

## Notes for Implementation

- **Be original:** While following the game mechanics, create your own implementation style
- **Prioritize functionality:** A working text-based game beats a broken graphical one
- **Test iteratively:** Verify each system works before moving to the next
- **Document your code:** Future benchmark evaluations may assess code quality
- **Handle edge cases:** What if the player has no food? No oxen? No money?

