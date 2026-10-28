# RA2 Mod

Configuration mod for CnCNet Yuri's Revenge: slower Nightmare AI, instant construction, an Elite Combat Academy, and a free player Nuclear Reactor.

Requires a separately installed compatible copy of Yuri's Revenge with CnCNet, Ares, and Phobos. Game executables and assets are not included.

## Mod features at a glance

- **Instant build:** Very fast construction of buildings, infantry, vehicles, aircraft, and ships. Also benefits AI.
- **Elite rank (3 chevrons):** Build the free Elite Combat Academy to give eligible newly produced units Elite rank.
- **Allied nuclear reactor:** Allies can build a free nuclear reactor immediately after deploying their MCV; also available to Soviet and Yuri factions.
- **+2000 power:** The custom reactor supplies a large amount of power and unlocks power-dependent construction.
- **Free player buildings:** The academy and custom reactor cost $0 and are configured to prevent AI construction.
- **Unlimited money & 90% price discount (Player-only):** Custom buildings grant instant +$1,000,000 cash, +$50,000/sec continuous income, and a 90% price discount on all units, tanks, aircraft, and defenses for the human player only. AI opponents pay normal prices.
- **Larger build queues:** Queue up to 99 items.
- **2.5-minute defense grace period:** AttackDelay=2.5 prevents AI attack waves for the first 4.5 minutes (at 60 FPS), giving you complete peace to construct bases, layered defenses, and 3-chevron armies.
- **Relentless Nightmare swarms:** After the grace period, rapid attack intervals (TeamDelays=200, ~6.6s) and maximum team capacity (TotalAITeamCap=100) unleash continuous, massive assaults against your defenses.
- **Endless AI funding:** Restores the 4800x income multiplier and virtual purifiers so the AI continuously pumps out high-tier heavy armor and swarms.
- **Parallel AI production:** AI builds units simultaneously across multiple factories.
- **All factions configured:** Academy and custom reactor ownership includes all ten countries.
- **Ten customized game modes:** Shared changes cover Battle/Standard, Cooperative, Free For All, Land Rush, Meat Grinder, Megawealth, Naval War, Survival, Team Alliance, and Unholy Alliance.

## Included mods and changes

| Modification | What it does |
| --- | --- |
| Instant construction | Sets global `BuildSpeed=0.001` for very fast production and `BuildupTime=0.001` for fast building placement animations. This applies globally, including AI; actual production time depends on the item and engine rules. |
| Larger production queues | Sets `MaximumQueuedObjects=99`. |
| Elite Combat Academy | Adds the free `PLAYERACAD` building, available after deploying an Allied, Soviet, or Yuri construction yard. Uses the hospital image, requires no power, has a build limit of one, and is configured with `AIBuildThis=no`. |
| Elite training | The academy sets infantry, vehicle, aircraft, and building academy veterancy to `2.0`, intended to give eligible newly produced units Elite rank (three chevrons). Build the academy before producing your army. |
| Player Nuclear Reactor | Adds free `PLAYERNRCT`, available after deploying a construction yard, with **+2000 power**, no tech-center requirement, and `AIBuildThis=no`. It also satisfies the power prerequisite for further construction. |
| Original reactor restriction | Sets the standard Soviet `NANRCT` to `TechLevel=-1` and `AIBuildThis=no`; the custom reactor is the player's replacement. |
| Baseline anti-rush rules | The ten customized map-code files set slower team creation, reduced AI economy bonuses, smaller team caps, no global hunt/fire-sale, restored team retaliation, and no parallel AI unit queues. Some settings are overridden by the selected AI modifier. |
| Nightmare AI anti-rush patch | Directly adjusts RAZER's Nightmare AI to preserve slower team creation and reduced economic bonuses when Nightmare is selected. Details appear below. |
| AI academy suppression attempt | Map code sets academy bonuses on `RAZER-GAOREP`, `RAZER-NAINDP`, and `RAZER-NACLON` to zero. However, the later Nightmare option defines them as `1`, so AI starting at recruit rank is **not guaranteed** with Nightmare selected. |

The academy and custom reactor list all ten countries as owners: America, Korea, France, Germany, Great Britain, Russia, Iraq, Cuba, Libya, and Yuri. Their faction prerequisites are configured for Allied, Soviet, and Yuri construction yards; gameplay across every country has not been verified.

### Customized game modes

The shared construction, academy, reactor, and baseline anti-rush changes are present in these files:

| Mode | Configuration |
| --- | --- |
| Battle / Standard | `INI/Map Code/Standard.ini` |
| Cooperative | `INI/Map Code/Cooperative.ini` |
| Free For All | `INI/Map Code/Free For All.ini` |
| Land Rush | `INI/Map Code/Land Rush.ini` |
| Meat Grinder | `INI/Map Code/Meat Grinder.ini` |
| Megawealth | `INI/Map Code/Megawealth.ini` |
| Naval War | `INI/Map Code/Naval War.ini` |
| Survival | `INI/Map Code/Survival.ini` |
| Team Alliance | `INI/Map Code/Team Alliance.ini` |
| Unholy Alliance | `INI/Map Code/Unholy Alliance.ini` |

Other map-code files included in this repository retain their existing mode rules. They do not all contain the shared custom modifications. Custom maps may impose additional overrides or scripted attacks.

### Existing Nightmare content retained

This mod uses **Nightmare AI V1.0.0 by RAZER**, with its existing custom task forces, team scripts, AI triggers, and AI-specific structures. Those include Allied/Soviet/Yuri refineries, a Slave Miner, Industrial Plant, Ore Processor, Cloning Vats, Bio Reactor, and AI versions of base defenses. These are retained Nightmare features, alongside the local anti-rush changes above.

**CnCNet** supplies the skirmish client; **Ares** supplies the academy functionality; **Phobos** supplies additional engine features used by Nightmare. Install those through your compatible game setup; their binaries are not distributed in this repository.

## Install

1. Close the game and CnCNet client.
2. Back up the matching files in your game installation.
3. Copy this repository's `INI` directory into the game directory, merging folders and replacing matching files.
4. Reopen CnCNet, select **Nightmare AI (Beta)**, and set **Starting Units** to **0**.
5. Start a **new skirmish**. Existing saved games retain their old rules.

In configured modes, deploy your MCV and build the Elite Combat Academy and player Nuclear Reactor from the building tab. Both cost $0; the reactor supplies 2000 power.

## Nightmare adjustment

The Nightmare option is patched directly because it overrides the earlier map-code anti-rush rules. The adjustment reduces AI economy bonuses, disables parallel AI production, limits active teams, and sets team creation intervals to 5,400 frames: about 3 minutes at 30 FPS or 90 seconds at 60 FPS. The previous 18,000-frame interval and three-team cap were too restrictive in play, so the cap is now 12 / 8 / 5 teams and AI structure delays are shorter. This interval also applies between later team creation checks; it is not a separate opening-only timer.
| Nightmare setting | Modified value |
| --- | --- |
| Opening grace period | `AIHateDelays=16200,16200,16200` & `AttackDelay=4.5` (4.5-minute grace period at 60 FPS) |
| Global hunt and AI fire sale | Disabled (`AIAllToHunt=no`, prevents frame-0 rush) |
| Team retaliation | Enabled (`TeamRetaliate=yes`) |
| Team creation interval | `TeamDelays=200,200,200` (~6.6s rapid attack wave frequency) |
| Active team caps, Hard / Normal / Easy | `TotalAITeamCap=100,100,100` (up to 100 squads swarming) |
| AI income multiplier | `MultiplayerAICM=4800,4800,4800` (unlimited AI funds) |
| Virtual ore purifiers | `AIVirtualPurifiers=50,50,50` |
| AI Slave Miner number setting | `AISlaveMinerNumber=2,2,2` |
| Target bias | `BaseBias=20`, `EnemyHouseThreatBonus=50.0` |
| Supplementary attack/autocreate settings | `AttackInterval=0.1`, `AutocreateTime=0.5` |
| Parallel production | Enabled for infantry, vehicles, navy, aircraft, and buildings |
| AI structure build delay | `BuildDelay=0.01` in all difficulty sections |

This is not a guaranteed ceasefire. Map scripts and existing units can still cause combat. INI parsing and the configuration differences were checked; in-game timing still needs testing. Global instant build also benefits AI production. Client updates may overwrite these customizations.

## Files and rollback

- `INI/Map Code/`: game-mode configuration and historical `.original_backup` files.
- `INI/Game Options/AI/Extreme AI Beta.ini`: adjusted Nightmare AI.
- `doc/status.md`: current findings and historical notes.
- `doc/backups/`: Nightmare option and status document before the latest adjustment.

To undo the latest Nightmare adjustment, copy `Extreme AI Beta.ini` from the relevant folder under `doc/backups/` back into `INI/Game Options/AI/`. Restore your own installation backup to undo the entire mod.

Original Nightmare AI by RAZER; credits remain in the configuration file.
