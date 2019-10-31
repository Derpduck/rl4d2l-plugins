# RL4D2L Plugins

Original and modified plugins used by the RL4D2L servers currently running SM 1.7.3 using Sir's [Server4Dead Project](https://github.com/SirPlease/Server4Dead-Project) and a [slightly modified ZoneMod](https://github.com/devilesk/ZoneMod/blob/master/CHANGELOG.md) config.

## Original Plugins

### chat_spam_throttle.sp
* Chat filter to prevent spamming the same message too often.
  * `chat_spam_throttle_debug` - cvar for logging.
  * `chat_spam_throttle_time` - cvar for time in seconds before a message can be repeated.
  * `chat_spam_throttle_check_sender` - cvar to allow repeating messages sent by someone else.

### discord_scoreboard.sp
* End of round scores reported to discord via webhook.
* Requires discord_webhook plugin.
  * Add `discord_scoreboard` entry to `discord_webhook.cfg`.

### discord_webhook.sp
* Plugin library for making discord webhook requests.
* Requires [SteamWorks](https://forums.alliedmods.net/showthread.php?t=229556) extension.
* Create a `addons/sourcemod/configs/discord_webhook.cfg`.
  ```
  "Discord"
  {
      "discord_test"
      {
          "url"	"<webhook_url>"
      }
  }
  ```

### l4d2_ladder_editor.sp
* Commands for cloning and moving special infected ladders.
* `sm_edit` - Toggle edit mode on or off.
  * While in edit mode, ladders you are aiming at can be selected using MOUSE1 and moved using MOUSE2 or WASD, USE, and RELOAD.
  * TAB to toggle edit mode. SHIFT to rotate ladders in 90 degree increments.
* `sm_step <size>` - Number of units to move when moving ladders in edit mode.
* `sm_select` - Select the ladder you are aiming at.
* `sm_clone` - Clone the selected ladder.
* `sm_move <x> <y> <z>` - Move the selected ladder to the given coordinate on the map.
* `sm_nudge <x> <y> <z>` - Move the selected ladder relative to its current position.
* `sm_rotate <x> <y> <z>` - Rotate the selected ladder.
* `sm_kill` - Remove the selected ladder.
* `sm_info` - Display info about the selected ladder entity.
* `sm_togglehud` - Toggle selected ladder info HUD on or off.

### l4d2_practice.sp
* Combined several features from existing plugins for use in a practice config.
* `sm_goto`, `sm_bring` - Teleport players around.
* Switch zombieclass with MOUSE2.

### l4d2_restartmap.sp
* Adds `sm_restartmap` to restart the current map. Preserves scores and who has played tank. Automatically restarts map when broken flow detected.
  * `sm_restartmap_debug` cvar for logging.
  * `sm_restartmap_autofix` cvar for autofix. Enabled by default.
  * `sm_restartmap_autofix_max_tries` cvar for max autofix map restart attempts.
* Score setting based on Visor's [SetScores](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d2_setscores.sp).
* Optional requirement: Lux's [l4d2_changelevel](https://github.com/LuxLuma/Left-4-fix/tree/master/left%204%20fix/l4d2_levelchanging) plugin.

### l4d2_tank_spawn_fix.sp
* Fixes inconsistency between rounds where teams have to reach slightly different locations to spawn the same tank.
* The plugin accounts for the variation in total map distance that can exist between rounds and adjusts the second round tank flow % to make the spawn trigger location match the first round.

### parish_finale_ladder_fix.sp
* Fixes infected ladders on the Parish finale bridge disappearing in the second round.

### saferoom_gnome.sp
* Spawns a gnome in the saferoom that is removed when the round goes live.

### spawn_secondary.sp
* Spawn pistol and axe for survivors plugin.
* Adds `sm_spawnsecondary <target>`, `sm_spawnaxe <target>`, and `sm_spawnpistol <target>` commands.
* Intended to be used when missing starting axes.

### static_tank_control.sp
* Requires l4d_tank_control_eq plugin and overrides its tank selection process with a predetermined one.
* Adds `static_tank_control` server command to specify if a given player should play a given tank on a given map.
  * Usage: `static_tank_control <tank_number> <map_name> [steam_id...]`
    * `tank_number` 1 or 2 representing which tank spawn to apply to.
    * `map_name` the map id to apply to.
    * `steam_id` any number of steam ids. The first player that is currently infected will be given the tank.
  * Example:
    ```
    static_tank_control 1 c1m1_hotel "STEAM_1:1:TEAMA_PLAYER1" "STEAM_1:1:TEAMB_PLAYER1"
    static_tank_control 1 c1m2_streets "STEAM_1:1:TEAMA_PLAYER2" "STEAM_1:1:TEAMB_PLAYER2"
    static_tank_control 1 c1m3_mall "STEAM_1:1:TEAMA_PLAYER3" "STEAM_1:1:TEAMB_PLAYER3"
    static_tank_control 1 c1m4_atrium "STEAM_1:1:TEAMA_PLAYER4" "STEAM_1:1:TEAMB_PLAYER4"
    static_tank_control 2 c1m4_atrium "STEAM_1:1:TEAMA_PLAYER1" "STEAM_1:1:TEAMB_PLAYER1"
    ```

### teleport_tank.sp
* Tank teleport plugin to unstuck tanks.
* Adds `sm_teleporttank [x] [y] [z]` command.
  * xyz arguments optional. If not provided, teleports tank to where it spawned.
* Adds `sm_teleport_tank_debug` cvar for logging.
* Adds `sm_spawntank` to set flow tank % to zero and spawn tank.

### whitelist.sp
* Restricts server to Steam IDs in a whitelist database.
* Adds server commands to add players to the whitelist database.
  * `sm_vouchnext` - Autovouch the next unvouched player to join the server.
  * `sm_vouchprev`, `sm_vouchlast` - Vouch the last unvouched player to join the server.
  * `sm_vouch` - Vouch the given steam id.

## Modified Plugins

*Significant changes*

### 8ball.sp
* Modified spoon's [8ball](https://github.com/spoon-l4d2/Plugins/blob/master/source/8ball.sp) v1.2.7 to load responses from a config file.

### basecommands.sp
* Updated to optionally use Lux's [l4d2_changelevel](https://github.com/LuxLuma/Left-4-fix/tree/master/left%204%20fix/l4d2_levelchanging) plugin if it is loaded.

### basevotes.sp
* Updated to optionally use Lux's [l4d2_changelevel](https://github.com/LuxLuma/Left-4-fix/tree/master/left%204%20fix/l4d2_levelchanging) plugin if it is loaded.

### confoglcompmod.sp
* Updated [confoglcompmod](https://github.com/devilesk/confoglcompmod/tree/rl4d2l) forked from [v2.2.3](https://github.com/epilimic/confoglcompmod) merged with optional l4d2_changelevel and bugfixes from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/confoglcompmod.sp).

### current.sp
* Updated [L4D2 Survivor Progress](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/current.sp) v2.0.1 used in ZoneMod 1.9.3 with changes from [v2.2](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/current.sp).
* Added optional precision argument `sm_current <precision>` to display 0 to 3 decimal places.
* Added `current_precision` cvar that specifies the default precision to use if no precision argument is given.

### eq_finale_tanks.sp
* Modified Visor's [EQ2 Finale Manager](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/eq_finale_tanks.sp).
  Reworked to no longer manage flow tanks, since that can be handled by the `static_tank_map` cvar used in the [tank\_and\_nowitch\_ifier](https://github.com/devilesk/rl4d2l-plugins/blob/master/tank_and_nowitch_ifier.sp) plugin. Cvars:
  * `tank_map_only_second_event` (formerly `tank_map_flow_and_second_event`)
  * `tank_map_only_first_event` (unchanged)
* Added `sm_tank_map_debug` cvar for logging.
* Updated to handle tanks on gauntlet finales.
  * `bridge_escape_fix.smx` no longer needed.

### l4d_tank_control_eq.sp
* Modified arti's [L4D2 Tank Control](https://github.com/alexberriman/l4d2-plugins/blob/master/l4d_tank_control/l4d_tank_control.sp).
  * Merged with SirPlease's changes from decompiled [ZoneMod version](https://github.com/SirPlease/ZoneMod/blob/master/addons/sourcemod/plugins/optional/zonemod/l4d_tank_control_eq.smx).
* Fixed handle leaks.
* Added commands for viewing and modifying the pool of players who have not played tank:
  * `sm_tankpool` displays the tank pool.
  * `sm_addtankpool`, `sm_queuetank` adds a player to the tank pool.
  * `sm_removetankpool`, `sm_dequeuetank` removes a player from the tank pool.
* Added natives:
  * `TankControlEQ_SetTank`
  * `TankControlEQ_GetWhosHadTank`
  * `TankControlEQ_ClearWhosHadTank`
  * `TankControlEQ_GetTankPool`
* Added forwards:
  * `TankControlEQ_OnChooseTank` called whenever a tank is chosen from the tank pool.
    * Return `Plugin_Continue` to continue with default tank choosing process.
    * Return `Plugin_Handled` to block the default tank choosing process.
  * `TankControlEQ_OnTankGiven` called when player has been given control of the tank.
    * Called with Steam ID of tank player.
  * `TankControlEQ_OnTankControlReset` called when new game detected and pools are reset.

### l4d\_tank_damage\_announce.sp
* Added discord_scoreboard plugin integration.
* Requires discord_scoreboard plugin.
* Fixed bug in damage to tank percent fudging by removing it.
  
### l4d_tank_rush.sp
* Added cvar `l4d_no_tank_rush_debug` to [L4D2 No Tank Rush](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d_tank_rush.sp) for debug logging.
* Fixed a bug where if survivors wiped to a 2nd half tank, then the next map would have its max points set to the previous map's max points.

### l4d2_playstats.sp
* Based on Tabun's [Player Statistics](https://github.com/Tabbernaut/L4D2-Plugins/tree/master/stats) plugin.
* Source code broken up into multiple files.
* More stats tracked.
* Adds logging to database.
  * Add a "l4d2_playstats" configuration to databases.cfg.
* Executes system command after last stats of the match have been logged.
  * Requires [system2](https://forums.alliedmods.net/showthread.php?t=146019) extension.
  * Create a `addons/sourcemod/configs/l4d2_playstats.cfg`.
    ```
    "l4d2_playstats.cfg"
    {
        "match_end_script_cmd"	"ls /home"
    }
    ```
* Adds `l4d2_playstats_customcfg` cvar to store a confogl custom config name that will get logged and saved with stats.
* Added discord_scoreboard plugin integration to send a fun fact embed.

### l4d2_saferoom_detect.sp
* Updated Tabun's [Saferoom Detect](https://github.com/Tabbernaut/L4D2-Plugins/tree/master/saferoom_detect) plugin replacing lgofnoc with confogl.

### l4d2_sound_manipulation.sp
* Updated [Sound Manipulation](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_sound_manipulation.sp) to allow for more control over which sounds are blocked by using `sound_block_for_comp` to set flags.
  * Block flags: 1 - World, 2 - Look, 4 - Ask, 8 - Follow Me, 16 - Getting Revived, 32 - Give Item Alert, 64 - I'm With You, 128 - Laughter, 256 - Name, 512 - Lead On, 1024 - Move On, 2048 - Friendly Fire, 4096 - Splat.
  * Block default: 8190 (allow world).
  * Block all: 8191.

### player_skill_stats.sp
* Psykotikism's [player skill stats](https://github.com/Psykotikism/Player_Skill_Stats) modified by bscal to save to database.
* No longer in use and replaced by modified l4d2_playstats plugin.

### suicideblitzfinalefix.sp
* Modified ProdigySim's [spawnstatefix](https://gist.github.com/ProdigySim/04912e5e76f69027f8c4) plugin to autofix Suicide Blitz 2 finale.

### tank\_and\_nowitch\_ifier.sp
* Fixed AdjustBossFlow to properly use boss ban flow min and max.
* Added `sm_tank_nowitch_debug` cvar for logging.
* Added `sm_tank_nowitch_debug_info` command for dumping info on current spawn configuration.
  * Requires `sm_tank_nowitch_debug` set to 1.

---

*Fixes applied to reconstructed sources from decompiled plugins*

### l4d_boss_percent.sp
* Reconstructed [L4D2 Boss Flow Announce](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d_boss_percent.sp) v1.6.2 used in [Zonemod 1.9.3](https://github.com/SirPlease/ZoneMod/blob/master/addons/sourcemod/plugins/optional/zonemod/l4d_boss_percent.smx).
* Recompiled with a fixed `l4d2_direct` include that addresses this [issue](https://github.com/ConfoglTeam/l4d2_direct/issues/13).

### pause.sp
* Reconstructed [Pause](https://github.com/MatthewClair/l4d2readyup/blob/master/pause.sp) v6.1 used in [Zonemod 1.9.3](https://github.com/SirPlease/ZoneMod/blob/master/addons/sourcemod/plugins/optional/zonemod/pause.smx) with a minor fix to check for valid client index in IsPlayer function.

### readyup.sp
* Reconstructed L4D2 Ready-Up v9.2 used in [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/plugins/optional/zonemod/readyup.smx).
* Applied spoon's [bugfix](https://github.com/spoon-l4d2/Plugins/blob/19b55c3c3122333bba0ce2e2cec202b4af623cab/source/readyup.sp#L1409) to prevent unbreakable doors from being made breakable.
* Replace checkboxes with diamonds from spoon's version.

### spechud.sp
* Reconstructed [Hyper-V HUD Manager](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/spechud.sp) v3.0 used in [Zonemod 1.9.3](https://github.com/SirPlease/ZoneMod/blob/master/addons/sourcemod/plugins/optional/zonemod/pause.smx) with fix to health, damage, and pills bonus not displaying.
* Refactored to use `l4d2util` include library and merged `l4d2_weapon_stocks.inc` into `l4d2util_weapons.inc`

---

*Insignificant changes*

### l4d_weapon_limits.sp
* Minor edit to [L4D Weapon Limits](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d_weapon_limits.sp) to fix off-by-one entity loop error.

### l4d_stuckzombiemeleefix.sp
* Minor edit to AtomicStryker's [Stuck Zombie Melee Fix](http://forums.alliedmods.net/showthread.php?p=932416) to use recommended datapack timer practices described in the wiki and eliminate possible handle leak.

### l4d2_blind_infected.sp
* Minor edit to [Blind Infected](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d2_blind_infected.sp) to fix off-by-one entity loop error.

### l4d2_getupfix.sp
* Minor edit to [L4D2 Get-Up Fix](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d2_getupfix.sp) v1.7 to use datapack instead of stack and use recommended datapack timer practices described in the wiki and eliminate possible handle leak.

### l4d2_godframes_control_merge.sp
* Minor edit to [L4D2 Godframes Control](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_godframes_control_merge.sp) v0.6 from L4D2 Competitive Rework v0.6.4.

### l4d2\_horde\_equaliser.sp
* Minor edit to [L4D2 Horde Equaliser](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_horde_equaliser.sp) v3.0.7 from L4D2 Competitive Rework v0.6.5.

### l4d2_saferoom_gun_control.sp
* Minor edit to [Saferoom Gun Control](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d2_saferoom_gun_control.sp) to fix off-by-one entity loop error.

### l4d2_saferoom_item_remove.sp
* Minor edit to [Saferoom Item Remover](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d2_saferoom_item_remove.sp) to fix off-by-one entity loop error.

### l4d2_static_shotgun_spread.sp
* Recompiled [L4D2 Static Shotgun Spread](https://github.com/Attano/L4D2-Competitive-Framework/blob/master/addons/sourcemod/scripting/l4d2_static_shotgun_spread.sp) v1.0 with an updated code_patcher include.
  * The code_patcher.inc change fixes the plugin name not being used in the method names according to the [wiki](https://wiki.alliedmods.net/Optional_Requirements_(SourceMod_Scripting)#Creating_a_Dependency), but I don't think it makes a difference here.

### l4d2_weaponrules.sp
* Minor edit to [L4D2 Weapon Rules](https://github.com/Stabbath/ProMod/blob/master/addons/sourcemod/scripting/l4d2_weaponrules.sp) to fix off-by-one entity loop error.

### tankdoorfix.sp
* Minor edit to Dr. Greg House's [TankDoorFix](https://forums.alliedmods.net/showthread.php?t=225087) v1.4 to fix `Array index is out of bounds` error.

---

*No change or minor edits to allow compilation on older SourceMod version.*

### caster_assister.sp
* Caster Assister v2.2 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/caster_assister.sp).
  * executes sm_spechud for casters joining server
  * fixes throwing client errors due to clients not being in-game.

### l4d_rock_lagcomp.sp
* Luckylock's [L4D(2) Tank Rock Lag Compensation](https://github.com/LuckyServ/sourcemod-plugins/blob/master/source/l4d_rock_lagcomp.sp) v1.10 with a minor edit to compile on older SourceMod versions.

### l4d_votepoll_fix.sp
* [L4D & L4D2] Vote Poll Fix v1.3 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d_votepoll_fix.sp) v0.3.

### l4d2_car_alarm_hittable_fix.sp
* L4D2 Car Alarm Hittable Fix v1.1 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_car_alarm_hittable_fix.sp) v0.4 with a minor edit to compile on older SourceMod versions.

### l4d2_duplicate_survivor_fix.sp
* Duplicate Survivor Fix v1.1 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_duplicate_survivor_fix.sp) v0.1 that fixes a loophole.

### l4d2_fireworks_noise_block.sp
* L4D2 Fireworks Noise Blocker v0.3 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_fireworks_noise_block.sp) v0.5.5 fixes sound blocking.

### l4d2_getup_slide_fix.sp
* Stagger Blocker v1.3 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/playermanagement.sp) v0.6.4.

### l4d2_nobhaps.sp
* Simple Anti-Bunnyhop v0.2 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_nobhaps.sp) v0.6.2 fixes throwing client errors due to clients not being in-game.

### l4d2_script_cmd_swap.sp
* [Script Command Swap - Mem Leak Fix](https://forums.alliedmods.net/showthread.php?p=2657025) v1.0 used in L4D2-Competitive-Rework.

### l4d2_uniform_spit.sp
* L4D2 Uniform Spit v1.3 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/l4d2_uniform_spit.sp) v0.5.4 renames l4d2_uniform_spit_zone back to l4d2_uniform_spit.

### playermanagement.sp
* Player Management Plugin v7 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/playermanagement.sp) v0.1 that fixes issues with creating bots and leaving the server full with bots called "k9Q6CK42".

### sv_consistency_fix.sp
* sv_consistency fixes v1.3 from [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework/blob/master/addons/sourcemod/scripting/sv_consistency_fix.sp) v0.6.4 fixes wrongly formatted chat printout.

## Include Library Updates

### l4d2_direct.inc
* Fixed an off by one error in the valid client check for `L4D2Direct_DoAnimationEvent`.
* Fixed round related functions [not accounting for flipped teams](https://github.com/ConfoglTeam/l4d2_direct/issues/13).