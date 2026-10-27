# RA2 Mod

Configuration mod for CnCNet Yuri's Revenge: slower Nightmare AI, instant construction, an Elite Combat Academy, and a free player Nuclear Reactor.

Requires a separately installed compatible copy of Yuri's Revenge with CnCNet, Ares, and Phobos. Game executables and assets are not included.

## Install

1. Close the game and CnCNet client.
2. Back up the matching files in your game installation.
3. Copy this repository's `INI` directory into the game directory, merging folders and replacing matching files.
4. Reopen CnCNet, select **Nightmare AI (Beta)**, and set **Starting Units** to **0**.
5. Start a **new skirmish**. Existing saved games retain their old rules.

In configured modes, deploy your MCV and build the Elite Combat Academy and player Nuclear Reactor from the building tab. Both cost $0; the reactor supplies 2000 power.

## Nightmare adjustment

The Nightmare option is patched directly because it overrides the earlier map-code anti-rush rules. The adjustment reduces AI economy bonuses, disables parallel AI production, limits active teams, and increases team creation intervals to 18,000 frames: about 10 minutes at 30 FPS or 5 minutes at 60 FPS.

This is not a guaranteed ceasefire. Map scripts and existing units can still cause combat. INI parsing and the configuration differences were checked; in-game timing still needs testing. Global instant build also benefits AI production. Client updates may overwrite these customizations.

## Files and rollback

- `INI/Map Code/`: game-mode configuration and historical `.original_backup` files.
- `INI/Game Options/AI/Extreme AI Beta.ini`: adjusted Nightmare AI.
- `doc/status.md`: current findings and historical notes.
- `doc/backups/`: Nightmare option and status document before the latest adjustment.

To undo the latest Nightmare adjustment, copy `Extreme AI Beta.ini` from the relevant folder under `doc/backups/` back into `INI/Game Options/AI/`. Restore your own installation backup to undo the entire mod.

Original Nightmare AI by RAZER; credits remain in the configuration file.
