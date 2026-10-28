# RA2 Mod

Custom configuration mod for CnCNet Yuri's Revenge: Player God-Mode Sandbox (Instant Build, Infinite Cash, 90% Discount, Elite Units, +100,000 Power) paired with brutal, swarming Nightmare AI and a 4.5-minute base defense grace period.

---

## 📋 Step-by-Step Installation Instructions

### Prerequisites
- A working installation of **Command & Conquer: Red Alert 2 & Yuri's Revenge** with **CnCNet 5** (includes Ares and Phobos engines).

### Installation Steps
1. **Close the Game & Client:** Ensure `RA2MD.exe` and `CnCNetYRLauncher.exe` are completely closed before copying files.
2. **Download this Repository:**
   - Click the green **Code** button at the top of this GitHub page $\rightarrow$ **Download ZIP** (or run `git clone https://github.com/Ardyshaz/RA2_Mod.git`).
3. **Extract to Base Game Directory:**
   - Extract the contents directly into your **base game installation directory** (where `gamemd.exe`, `CnCNetYRLauncher.exe`, and `ra2.ini` are located).
   - When prompted by Windows, choose **Replace / Overwrite all existing files**.
4. **⚠️ DO NOT UPDATE THE CNCNET CLIENT:**
   - When launching the CnCNet client, if a prompt asks to check for updates or install a client update, **do not update** (or click No/Cancel).
   - *Updating CnCNet will overwrite and reset your customized INI files back to stock!*
5. **Skirmish Lobby Settings:**
   - Open CnCNet and go to **Skirmish**.
   - **Game Mode:** Choose any mode (Battle / Standard, Free For All, Team Alliance, Survival, etc.).
   - **AI Modifier:** Select **Nightmare AI (Beta)**.
   - **Starting Units:** Set to **`0`** *(CRITICAL: prevents AI from starting with free rush tanks at second 1)*.
   - **Starting Credits:** Any amount (custom buildings supply infinite money).
6. **In-Game Play:**
   - Deploy your MCV / Construction Yard.
   - Open **Building Tab 1** and immediately place:
     - **Player Mega Nuclear Reactor** ($0, instant)
     - **Elite Combat Academy** ($0, instant)
   - Enjoy instant construction, infinite money, +100,000 power, and 3-chevron Elite armies!
   - You have **4.5 minutes** of opening peace to build a fortress before the Nightmare AI swarm attacks!

---

## ⚡ Summary of All Mods & Cheats Used

| Mod / Cheat | Short Description | Exclusive To |
| :--- | :--- | :--- |
| **Instant Construction** | `BuildSpeed=0.001` and `BuildupTime=0.001` allow all buildings, infantry, tanks, and aircraft to finish in a fraction of a second (~0.06s). | Player-focused |
| **Unlimited Money** | Custom buildings grant **+$1,000,000 startup cash** immediately upon placement, plus **+$50,000/sec continuous cash flow**. Your credits never run dry. | **Player Only** (`AIBuildThis=no`) |
| **90% Price Discount** | Ares `FactoryPlant` modifier slashes all unit, building, and defense costs by 90% (e.g., a $1,000 battle tank costs only $100). | **Player Only** (`AIBuildThis=no`) |
| **Elite Combat Academy** | Instant $0 structure (`PLAYERACAD`) grants **3-chevron Elite rank** (veterancy level 2.0) to all newly trained infantry, vehicles, and aircraft. | **Player Only** (`AIBuildThis=no`) |
| **Mega Nuclear Reactor** | Instant $0 reactor (`PLAYERNRCT`) generates **+100,000 Power**. Just 1 single plant powers 1,000+ French Grand Cannons or Prism Towers. Available to Allied, Soviet, and Yuri. | **Player Only** (`AIBuildThis=no`) |
| **4.5-Minute Defense Grace Period** | Calibrated for 60 FPS (`AIHateDelays=16200` frames, `AttackDelay=4.5`). AI will not target or attack your base for the first 4.5 minutes, allowing you to complete layered defenses in peace. | Map & AI Options |
| **Relentless Nightmare Swarms** | After the 4.5-minute grace period, AI attacks relentlessly: wave interval every ~3.3s–6.6s (`TeamDelays=200`), up to 100 simultaneous squads (`TotalAITeamCap=100`), and parallel factory queues enabled. | AI Opponents |
| **Unlimited AI Wartime Economy** | Nightmare AI retains `MultiplayerAICM=4800` (4800x income multiplier) & virtual ore purifiers to continuously build and replace massive high-tier armies. | AI Opponents |
| **Maximum Queues** | Queue capacity expanded to **99 items** per factory (`MaximumQueuedObjects=99`). | Global |
| **All Factions & Modes Covered** | Custom buildings and balance rules cover all 10 playable countries and all 10 Skirmish game modes. | Universal |
| **Strict AI Separation** | Vanilla Soviet reactor (`NANRCT`) disabled for AI (`AIBuildThis=no`, `TechLevel=-1`). Custom buildings blocked from AI, so AI opponents play with normal recruits and normal prices. | Fair Separation |

---

## 🗺️ Customized Skirmish Game Modes

The shared instant construction, academy, mega reactor, unlimited money, and 60 FPS grace period rules are present in all 10 mode files:

| Game Mode | Configuration File |
| :--- | :--- |
| **Battle / Standard** | `INI/Map Code/Standard.ini` |
| **Cooperative** | `INI/Map Code/Cooperative.ini` |
| **Free For All** | `INI/Map Code/Free For All.ini` |
| **Land Rush** | `INI/Map Code/Land Rush.ini` |
| **Meat Grinder** | `INI/Map Code/Meat Grinder.ini` |
| **Megawealth** | `INI/Map Code/Megawealth.ini` |
| **Naval War** | `INI/Map Code/Naval War.ini` |
| **Survival** | `INI/Map Code/Survival.ini` |
| **Team Alliance** | `INI/Map Code/Team Alliance.ini` |
| **Unholy Alliance** | `INI/Map Code/Unholy Alliance.ini` |

---

## ⚙️ Nightmare AI Parameter Reference

Directly tuned in `INI/Game Options/AI/Extreme AI Beta.ini`:

| Nightmare Setting | Configured Value | Explanation |
| :--- | :--- | :--- |
| **Opening Grace Period** | `AIHateDelays=16200,16200,16200` & `AttackDelay=4.5` | 4.5-minute delay (16,200 frames at 60 FPS) before AI chooses an enemy to target. |
| **Global Hunt & Fire Sale** | Disabled (`AIAllToHunt=no`, `AIFireSale=no`) | Prevents immediate suicide tank charges at frame 0. |
| **Team Retaliation** | Enabled (`TeamRetaliate=yes`) | AI vigorously fights back if fired upon. |
| **Wave Frequency** | `TeamDelays=200,200,200` | Rapid wave intervals (~3.3s at 60 FPS, ~6.6s at 30 FPS). |
| **Active Team Cap** | `TotalAITeamCap=100,100,100` | Up to 100 active combat squads on the map simultaneously. |
| **AI Credit Multiplier** | `MultiplayerAICM=4800,4800,4800` | 4800x income multiplier cheat for endless enemy funding. |
| **Virtual Ore Purifiers** | `AIVirtualPurifiers=50,50,50` | Maximum refinery income for AI bots. |
| **Base Targeting Bias** | `BaseBias=20`, `EnemyHouseThreatBonus=50.0` | Focuses attacks directly into the player's base defense system. |
| **Parallel AI Queues** | Enabled (`AllowParallelAIQueues=yes`) | AI builds infantry, armor, and air from multiple factories simultaneously. |
| **AI Structure Build Delay** | `BuildDelay=0.01` in all difficulty sections | AI constructs bases and replacement buildings rapidly. |

---

## 📁 Repository Structure & Rollback

- `INI/Map Code/`: Game mode configurations and historical `.original_backup` files.
- `INI/Game Options/AI/Extreme AI Beta.ini`: Adjusted Nightmare AI option file.
- `doc/status.md`: Detailed changelog, technical documentation, and findings.
- `doc/backups/`: Historical backups of configuration files.

Original Nightmare AI V1.0.0 by RAZER; credits remain in the configuration file.