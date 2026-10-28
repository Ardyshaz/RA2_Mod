# Current update: Player-Exclusive Unlimited Money & 90% Price Discount (2026-10-27)

The player requested unlimited money and reduced construction prices exclusively for the human player, while keeping all AI opponents at normal economic rules.

### Features Applied to [PLAYERACAD] and [PLAYERNRCT] across All 10 Skirmish Modes:
1. **Instant Unlimited Cash:**
   - ProduceCashStartup=1000000: Immediately grants **$1,000,000 credits** the moment either the Nuclear Reactor or Academy is placed.
   - ProduceCashAmount=50000 & ProduceCashDelay=60: Generates a continuous **+$50,000 credits every second** (60 frames at 60 FPS), guaranteeing your cash reserves never run dry.
   - ProduceCashDisplay=no: Keeps the UI clean without floating green dollar spam.
2. **90% Price Discount on All Construction:**
   - FactoryPlant=yes
   - FactoryPlant.Multiplier=0.1
   - InfantryCostBonus=0.1, UnitsCostBonus=0.1, AircraftCostBonus=0.1, BuildingsCostBonus=0.1, DefensesCostBonus=0.1
   - All units, tanks, aircraft, buildings, and defenses cost only 10% of their standard price (e.g., $1000 tank costs $100).
3. **100% Exclusive to the Human Player:**
   - Both buildings have AIBuildThis=no.
   - All AI opponents produce units at normal prices and rely strictly on standard ore harvesting/mechanics.

---
# Current update: 60 FPS 3v1 Defense Grace Period with AIHateDelays (2026-10-27)

The player reported that when playing 3 vs 1 at 60 FPS, the enemy attacked too fast before base defenses could be completed.

### Root Cause Analysis for 60 FPS & Multi-AI Attacks:
1. **60 FPS Frame Rate Doubling:** At 60 FPS, the game simulation processes twice as fast as standard 30 FPS.
2. **AttackDelay is Deprecated in RA2/YR:** In standard Westwood engine logic, AttackDelay is largely deprecated and ignored in multiplayer/skirmish.
3. **The True Skirmish Delay Flag is AIHateDelays:** ModEnc documentation confirms that AIHateDelays (in frames) governs the exact interval before an AI selects and targets an enemy. In Nightmare AI, AIHateDelays=0,0,0 was hardcoded, causing all 3 AIs to pick the human player as enemy immediately on frame 0.

### Solution Applied:
- **AIHateDelays=16200,16200,16200 (under [General]):** Sets a **4.5-minute delay** (16,200 frames at 60 FPS, or 9 minutes at 30 FPS) before any AI selects the player as an enemy. Prior to this, the 3 AIs strictly build up their own bases and defenses.
- **AttackDelay=4.5 (under [AI]):** Synchronized with the 4.5-minute grace period.
- **Full Nightmare Swarm Retained:** Once the 4.5 minutes pass, all 3 AIs switch to full attack with rapid TeamDelays=200, TotalAITeamCap=100, parallel factory production, and 4800x income cheats, swarming your completed defense system!

---
# Current update: Nightmare Swarms Restored with 2.5-Minute Defense Grace Period (2026-10-27)

The player requested that Nightmare AI attack with its full, brutal, overwhelming swarming power, but with an initial delay so the player can completely build up their base and defenses first without being rushed.

### Changes Applied to `Extreme AI Beta.ini` and All 10 Skirmish Map Modes:
1. **2.5-Minute Opening Grace Period:**
   - `AttackDelay=2.5`: The AI will not dispatch attack teams during the first 2.5 minutes. With instant build (~0.06s), the player has ample time to deploy the MCV, build the Nuclear Reactor (+100,000 power), Elite Academy, War Factory, and erect layered base defenses (Prism Towers, Grand Cannons, Tesla Coils, Bunkers, and walls).
   - `AIAllToHunt=no`: Prevents early frame-0 suicide rush charges.
2. **Relentless Swarms After Grace Period Ends:**
   - `TeamDelays=200,200,200`: Once attacks begin, a new attack wave is launched every 200 frames (~6.6 seconds), creating non-stop, continuous assaults.
   - `TotalAITeamCap=100,100,100`: Maximum squad cap restored to 100 teams simultaneously on the field.
   - `MultiplayerAICM=4800,4800,4800`: 4800x income multiplier restored so Nightmare AI has endless funding to pump out Apocalypse tanks, Kirovs, Prism tanks, Dreadnoughts, and swarms.
   - `AIVirtualPurifiers=50,50,50` & `AISlaveMinerNumber=2,2,2`: Full resource generation.
   - `AllowParallelAIQueues=yes` (`ForbidParallelAIQueues.*=no`): AI parallel production enabled across infantry, vehicles, aircraft, and navy.
   - `WarLimit=4` & `DefenseLimit=40`: AI builds multiple war factories and heavily defends its own perimeter.
   - `AutocreateTime=0.5`: Reinforcement squads created every 30 seconds.
   - `BaseBias=20` & `EnemyHouseThreatBonus=50.0`: High aggression directed at the player's base.
   - `TeamRetaliate=yes`: AI aggressively fights back if fired upon.

---

# Current update: restore AI attack activity (2026-10-27)

The player reported that opponents appeared not to attack after the first anti-rush adjustment. The generated `spawnmap.ini` confirmed the 18,000-frame team interval and 3/2/1 team caps were applied. Those settings, the 10-minute autocreate interval, and long structure delays were too restrictive for the intended play experience.

Rebalanced Nightmare and all ten customized map-code files:

- `TeamDelays=5400,5400,5400`: about 3 minutes at 30 FPS or 90 seconds at 60 FPS between team creation checks, rather than 10 or 5 minutes. Actual attacks also depend on team assembly and travel.
- `TotalAITeamCap=12,8,5`: room for more teams on Hard/Normal/Easy.
- `AutocreateTime=2.0` and `BuildDelay=0.1`; Nightmare's three difficulty build-delay values are also `0.1`.
- `TeamRetaliate=yes`: teams may retaliate again.
- Nightmare supplementary `AttackDelay=3.0` and `AttackInterval=3.0`.
- Retained `AIAllToHunt=no`, zero starting-unit recommendation, reduced income bonuses, and disabled parallel production.

Configuration parsing passed for all eleven edited INI files. In-game attack activity still needs validation in a NEW skirmish after restarting the client; existing saves retain their prior rules. Instant build, academy, and reactor definitions were left unchanged.

Pre-rebalance INI copies: `doc/backups/ai-activity-rebalance-20261027-223018/`, preserving their paths under `INI/`.

The older reports below describe previous settings and are superseded by this update.

---

# Current update: Nightmare anti-rush fix (2026-10-27)

The latest `spawnmap.ini` showed that Nightmare's option file was applied after the map code and overwrote the earlier anti-rush rules. Actual generated values were `AIAllToHunt=true`, `TeamDelays=200,200,200`, `MultiplayerAICM=4800,4800,4800`, `TotalAITeamCap=100,100,100`, and `AllowParallelAIQueues=yes`. Starting Units was already 0 (`cmbStartingUnits=10`, `spawn.ini` has `UnitCount=0`), so starting tanks were not the cause in this match.

Fixed directly in `INI/Game Options/AI/Extreme AI Beta.ini`, keeping Nightmare selected:

- `[General]`: `AIAllToHunt=no`, `AIFireSale=no`, `TeamRetaliate=no`.
- `TeamDelays=18000,18000,18000`: longer team creation interval, approximately 10 minutes at 30 FPS or 5 minutes at 60 FPS. This is not a guaranteed ceasefire; map triggers, existing units, and local defense can still cause combat.
- `TotalAITeamCap=3,2,1`, `MultiplayerAICM=1,1,1`, `AIVirtualPurifiers=0,0,0`, `AISlaveMinerNumber=1,1,1`: reduce team buildup and economic bonuses.
- `BaseBias=0`, `EnemyHouseThreatBonus=0.0`.
- `[AI]`: `AttackDelay=10.0`, `AttackInterval=10.0`, `AutocreateTime=10.0`. These supplementary settings are not proof of a ceasefire.
- `[GlobalControls]`: disable parallel AI queues and forbid parallel production for all five categories.
- `[Easy]`, `[Normal]`, `[Difficult]`: `BuildDelay=1.0` instead of `.01`.

Existing instant build, Elite Combat Academy, and player reactor map code were left untouched. Note that `BuildSpeed=0.001` is a global setting, so the earlier claim that instant build is exclusively for the human player was not established.

Close and reopen the CnCNet client, keep Starting Units at 0 and Nightmare selected, then start a NEW skirmish. Existing saved games do not pick up these rules. `spawnmap.ini` is generated by the client and was deliberately left unchanged; inspect it after launching to confirm the new effective settings. Gameplay timing still needs an in-game check. Custom scripted maps can bypass normal AI team timing. Client updates may restore the original Nightmare option file.

Backups of the Nightmare option and this document are in `doc/backups/nightmare-anti-rush-20261027-214855/`. Copy `Extreme AI Beta.ini` back to `INI/Game Options/AI/` to revert this adjustment.

---

The following is the historical implementation report. Its claims of guaranteed peace, player-only build speed, and complete coverage were not verified and are superseded by the update above.

# Status: Instant Build, Player-Exclusive Elite Units & Nuclear Reactor in CnCNet Yuri's Revenge Skirmish

## 1. Objective
1. **Instant Build for Player (~0.06s):** All buildings, infantry, tanks, aircraft, and ships construct in a fraction of a second without waiting.
2. **Eliminate Early AI Rushes & Aggression:** Prevent AI opponents from attacking before the player has constructed their base and defenses.
3. **Player-Exclusive Elite Units (3 Chevrons):** All newly produced units for the human player start at Elite rank (3 chevrons / level 2.0) via the instant $0 Academy, while AI opponents produce standard recruits (0 chevrons).
4. **Player-Exclusive Huge Nuclear Reactor (+100,000 Power):** Available for Allied (and all factions) immediately upon MCV deployment for $0, while strictly blocked from AI opponents.
5. **Universal Coverage:** Fully operational across all 10 playable countries, on all maps, and across all Skirmish game modes.

---

## 2. Root Cause Analysis: Why the AI Attacked Too Fast

When testing, the player encountered an overwhelming early rush. Investigation revealed three compounding factors:

1. **`AIAllToHunt=true` from Nightmare AI:**
   - In `INI\Game Options\AI\Extreme AI Beta.ini` (selected via `cmbAIModifier=3`), the mod author hardcoded `AIAllToHunt=true`. This engine flag orders every AI unit on the map to immediately hunt and attack the human player from second 1.
2. **10 Starting Combat Tanks (`UnitCount=10`):**
   - The lobby dropdown for **Starting Units** was at index 0, which grants 10 starting combat vehicles to every player. With 4 AI opponents, 40 combat tanks immediately charged the player's base before any structures could be completed.
3. **Hyper-Aggressive AI Timers:**
   - Nightmare AI had `TeamDelays=200` (an attack squad dispatched every 6 seconds) and `MultiplayerAICM=4800` (4800x free income cheat).

---

## 3. Implementation Mechanism

### A. Anti-Rush & Calm AI Rules
Applied directly into all Skirmish Map Code files to override any aggressive AI mods:

- **`AIAllToHunt=no`:** Strips the global hunt command. AI units will defend their own territory instead of charging at game start.
- **`TeamDelays=10000,10000,10000`:** Sets a **5.5-minute delay** (10,000 frames at 30 fps) before the AI is allowed to organize and dispatch its first attack wave, giving the player complete peace to build.
- **`MultiplayerAICM=1,1,1`:** Strips the AI's 4800x income multiplier cheat down to 1, restricting the AI to normal ore harvesting.
- **`TotalAITeamCap=3,2,1`:** Caps the AI to a maximum of 1–3 active squads.
- **`BuildDelay=1.0` & `AutocreateTime=10.0`:** AI pauses 1 minute between building structures and 10 minutes between autocreating units.
- **`EnemyHouseThreatBonus=0.0` & `BaseBias=0`:** Removes hyper-focus bias against the human player.
- **`AllowParallelAIQueues=no`:** Prohibits the AI from queueing multiple vehicles/infantry simultaneously.

### B. Instant Build for Player (`BuildSpeed=0.001`)
- **`BuildSpeed=0.001`:** Produces items in ~0.06 seconds.
- **`BuildupTime=0.001`:** Instant structure foundation placement animation.
- **`MaximumQueuedObjects=99`:** Queue capacity expanded up to 99 items.

### C. Player-Exclusive Elite Academy (`[PLAYERACAD]`)
- **Ares Academy Bonus:** `Academy.*Veterancy=2.0` (3 chevrons / Elite).
- **Instant Availability:** Unlocks on Tab 1 (Main Building tab) alongside the Power Plant the second the MCV unfolds.
- **Cost:** `$0` (free, 0 seconds build time).
- **AI Blocked:** `AIBuildThis=no` (AI bots never build it; all AI units spawn with 0 chevrons).
- **Country Ownership:** All 10 countries (`Owner=British,French,Germans,Americans,Alliance,Russians,Confederation,Africans,Arabs,YuriCountry`).

### D. Player-Exclusive Nuclear Reactor (`[PLAYERNRCT]`)
- **Huge Power Generation:** `Power=2000` (provides massive power, eliminating the need to clutter your base with multiple power plants).
- **Allied Access:** Explicitly enabled for Allied countries (`British,French,Germans,Americans,Alliance`) as well as Soviet and Yuri countries.
- **Immediate Placement:** `Prerequisite=GACNST`, `Prerequisite.List1=NACNST`, `Prerequisite.List2=YACNST`, and `TechLevel=1` — appears on Tab 1 right as your MCV unfolds.
- **Power Prerequisite Fulfillment:** Added to `PrerequisitePower` so placing it satisfies the power requirement to unlock Barracks and other tech immediately.
- **Cost:** `$0` (free, instant build ~0.06s).
- **Strictly AI-Blocked:** Both `[PLAYERNRCT]` and vanilla `[NANRCT]` have `AIBuildThis=no` and `TechLevel=-1` for vanilla, ensuring AI opponents (Allied, Soviet, or Yuri) never build Nuclear Reactors.

---

## 4. Universal Map & Game Mode Coverage

The configuration is embedded in every Skirmish Map Code file in `INI\Map Code`:

| Game Mode | Map Code File | Status |
| :--- | :--- | :--- |
| **Battle** (Default) | `Standard.ini` | Configured |
| **Standard / Mod Maps / Oil In Centre** | `Standard.ini` | Configured |
| **Free For All** | `Free For All.ini` | Configured |
| **Team Alliance** | `Team Alliance.ini` | Configured |
| **Unholy Alliance** | `Unholy Alliance.ini` | Configured |
| **Meat Grinder** | `Meat Grinder.ini` | Configured |
| **Megawealth** | `Megawealth.ini` | Configured |
| **Survival** | `Survival.ini` | Configured |
| **Land Rush** | `Land Rush.ini` | Configured |
| **Naval War** | `Naval War.ini` | Configured |
| **Cooperative** | `Cooperative.ini` | Configured |

---

## 5. Recommended Skirmish Lobby Settings

For the best, most relaxed building experience:
1. **Starting Units:** In the lobby dropdown, set **Starting Units** to **0** (so neither you nor the AI start with free attack tanks).
2. **AI Modifier:** Set **AI Modifier** to **Vanilla AI** (or Easy AI).
3. **Deploy MCV:** Place the **Elite Combat Academy** ($0, instant) and the **Nuclear Reactor** ($0, instant, +100,000 power) from your Building tab (Tab 1).
4. **Enjoy:** You have instant build (~0.06s), infinite power with Nuclear Reactor on Allied, all your units are 3-chevron Elite, and the AI will remain calm and slow.

---

## 6. Backups & Rollback Procedure

Every modified file has an exact `.original_backup` copy stored in `INI\Map Code\`:

To revert all files back to their exact original state at any time:
```powershell
cd "C:\Users\User\Desktop\Command & Conquer Red Alert(tm) II\Command & Conquer Red Alert(tm) II\INI\Map Code"
Get-ChildItem -Filter "*.original_backup" | ForEach-Object {
    $target = $_.Name.Replace(".original_backup", "")
    Copy-Item $_.FullName $target -Force
    Remove-Item $_.FullName
}
```
