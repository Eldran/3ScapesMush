# 3Scapes MUSHclient - Command Guide
*(3Scapes mud setup, updated 2026-06-10)*

All commands are typed in the normal input line. Windows are dragged by
their title bars; positions are remembered.

---

## Area bot / stepper  (ThreeS_Stepper)

Walks the converted TinTin++ area paths from `3s_areas.lua`.

**The bots share ONE window** with Area / Chaos / Deadman tabs at the
top - click a tab to switch, just like the Viking Status window. The
window keeps its position when switching. `areabot` opens it on Area,
`cs win` on Chaos, `deadman` on Deadman.

**Everything is clickable** in the Area tab (`areabot` shows/hides
it): click an area name to start, then Walk / Pause / Stop / Resume / Kill.
The toggle buttons AutoR (auto-resume), Hard (hard mobs)
and Loot light up when on. A progress bar tracks your position on the path,
and the banner shows WALKING / FIGHTING / stopped. Hover anything for help.

| Command | What it does |
|---|---|
| `- <area>` or `walker <area>` | Start botting an area, e.g. `- aegis` |
| `.areas` | List all 20 areas |
| `..` | Step / resume walking |
| `.stop` | Stop and save position |
| `.pause` | Pause (keeps position) |
| `.resume` | Resume from saved position |
| `.dcr` | Resume after a disconnect |
| `.stack <n>` | Stack up to n mobs on the next move |
| `killbot` | Kill the bot completely |
| `v on` / `v off` | Vacuum looting on/off |
| `pa <name>` / `pr <name>` | Party add/remove (party members don't trigger player-skip) |
| *(automatic)* | Showing the in-game party table captures the member list by itself - members who left are dropped. `pa` is only needed for disguised characters. One list serves both bots. |
| `.set autoresume on\|off` | Auto-resume walking on "There is no X here." |
| `.set hardmode on\|off` | Also engage 'hard' mobs (e.g. Otyg in afield) |
| `.set stackit\|bagit\|necbagit\|bardit on\|off` | Loot styles |
| `.binfo` | Help |

**Recording a new area** - walk it once, the bot writes the file:

| Command | What it does |
|---|---|
| `record <name>` | Start recording; every direction you type is captured |
| `r: <command>` | Record a special step (e.g. `r: open door`) - also sends it |
| `record kill <word>` | What to kill for the mobs seen (e.g. `record kill troll`) |
| `record undo` | Drop the last step (failed moves drop automatically) |
| `record` | Show progress       `record cancel` discards |
| `record save` | Write to 3s_areas.lua + usable immediately in the area list |

Mobs you encounter while recording are noted automatically (condition
tags stripped). Walk the route so it ends where looping should restart.

**Deadman switch** (own little window, drag it anywhere): stops BOTH bots
(area + chaos sea) after too long without keyboard input. ON/OFF button,
- / + adjust the minutes, live idle counter that turns red near the limit.

| Command | What it does |
|---|---|
| `deadman` | Show/hide the deadman window |
| `deadman on` / `deadman off` | Arm / disarm |
| `deadman <secs>` | Set the timeout (60-7200, default 600) |

---

## Chaos sea bot  (ThreeS_ChaosSea)

Maps the sea on a 3D grid, dives down exits, stops at the cask.
Everything is clickable in the map window - text commands optional.
Map: green = you, blue outline = unexplored, blue dot = down exit.

**Normal session, buttons only:** walk to your entry room, click **Reset**,
click **ON**, click **Auto**. The banner shows what the bot is doing
(READY / AUTO-EXPLORING / WALKING / FIGHTING / PAUSED / OFF). **Pause**
holds everything mid-run - click again to continue. **Loot** toggles
looting, **- / +** adjust the pause after kills, **Leave** walks home,
**X** hides the window (`cs win` brings it back). Hover any button for a
tooltip. Don't walk manually while ON (it desyncs - see `cs set`).

| Command | What it does |
|---|---|
| `cs` | Help |
| `cs reset` | Wipe the map, current room becomes start (0 0 0) |
| `cs enable` / `cs disable` | Room mapping on/off |
| `cs step` | Walk to the next unexplored room (one careful step at a time) |
| `cs auto on` / `cs auto off` | Keep exploring + fight mobs on the way |
| `cs leave` | Walk back to the start room |
| `cs kill <name>` | What to attack when a mob appears (default: mutant) |
| `cs exclude <mob long name>` | Never attack this mob (Tibbers + otters built in) |
| `cs goal <words>` | Stop when any goal item is seen (default: cask portal; cask also gets opened). Goal re-arms every `cs auto on`. |
| `cs delay <secs>` | Pause after killing blows before moving on (default 2.5s) |
| `cs rest <seid> [secs]` | Rest when Seid drops below the threshold (60s rounds until recovered; 0 = off) |
| `cs vacuum on\|off` | Loot rooms (default on) |
| `cs set <x> <y> <z>` | Correct the bot's position after a desync |
| `cs find <x> <y> <z>` | Print the path to a coordinate |
| `cs win` | Show/hide the map window |
| `cs debug_all` | Dump the mapped grid as text |

**Wimpy protection:** if the mud's wimpy yanks you out of a room
mid-fight, the chaos bot auto-PAUSES (walk back, click Pause to continue)
and the area bot stops with its position saved ('.resume' after walking
back). The room you fled into is never added to the map.

Built-in behaviour: **down exits always have priority** (dives immediately);
up exits are used for backtracking but never explored; won't move while the
MIP feed shows an enemy; after a kill it re-checks the room (`kill mutant`)
and only walks on at "There is no mutant here."; stops + opens when the
goal item (cask) is in the room. Map survives restarts.

---

## Viking Status window  (ThreeS_VikingStatus)

Tabbed window: Stats / City / People / Goods / Holds / Map / Feeds.
Click the tabs, drag the title bar.

| Command | What it does |
|---|---|
| `vikbar` | Show/hide the window |
| `viktab <name>` | Switch tab from the command line |
| `vikdump` | Write the full live feed to `vmip_dump.txt` (for building new tabs) |
| `vikloc <x> <y> <name>` | Name a town on the Map tab (no name = clear). Hover any town for its coords. |

**Map tab travel:** click a town name in the Locations list to walk there
(the routes are built into this plugin - any pair is chained via Midgard). Your starting town is read
from your live map position; if you're somewhere unrecognized, right-click
the town you're in first, then click the destination.
| `vtick on\|off` | The old 5-minute `l` keepalive ticker |

The feed comes from your mud-side `vtoggle` settings (all mip_* are ON).
**Don't run `vmapon`** - vtoggle flips settings, it would turn feeds OFF.
The Sea tab shows the active voyage: status, hull/morale/supplies/stress
bars, the chart (S = your ship, X = objective, letters per the legend) and
the saga log. With no voyage running it lists your fleet instead.

---

## Chat window  (ThreeS_Chat)

All channels + tells with timestamps and colours, logged to `3s_chat.log`.

| Command | What it does |
|---|---|
| `chatwin` | Show/hide the window |
| `chat watch <name>` | Bell + highlight when the name appears |
| `chat unwatch <name>` / `chat watched` | Manage/list watch names |
| `chat clear` | Clear the buffer |
| `chatup` / `chatdown` / `chatend` | Scroll back / forward / live (also Up/Dn/End buttons) |
| `chatsize <w> <h>` | Resize the window (default 682x273) |

---


## MIP core  (ThreeS_MIP)

Runs by itself: handshake ~2s after login ("[MIP] handshake sent"),
feeds stats/Viking data/chat to the other plugins, hides the raw lines.

| Command | What it does |
|---|---|
| `mipstart` | Re-send the handshake manually if the feeds ever look dead |
| `mipecho on\|off` | Show/hide the raw MIP lines (debugging) |
| `mipdebug on\|off` | Extra debug prints |

If the mud's text HP bar reappears after a plugin reinstall, type
`3klient HAA off` once to hide it again.

---

## Mapper  (ThreeS_Mapper)

Maps wherever you walk (one map per area), drawn in its own draggable
window. Auto-suspends while the area bot or chaos bot is driving.

| Command | What it does |
|---|---|
| `mm` | Status + help |
| `mm on` / `mm off` | Tracking on/off |
| `mm area <name>` | Switch to (or create) that area's map |
| `mm list` | List your maps       `mm clear` wipes the current one |
| `mm stop` | Abort click-walking  `mm win` show/hide window |

**Click a room** to walk there (step-confirmed BFS). **Right-click a
room** = "I am here" - use it after teleports/summons or when the status
says LOST. Hover rooms for their names. Yellow dot = up exit, blue = down.
After switching areas or turning mapping on with an existing map, sync
once with a right-click.

---

## Setting up another character (or a friend)

Nothing in the plugins is character-specific - any viking on 3Scapes can
use this folder as-is:

1. Copy the whole folder (the six `3S_*.xml`, `3s_areas.lua`, this file).
2. Make a new world in MUSHclient (3k.org port 3200), set name/password
   under Game -> Configure -> Connecting (Connect: LP-mud style).
3. File -> Plugins -> Add all six, in this order: MIP, Stepper, ChaosSea,
   VikingStatus, Chat, Mapper. Save the world file.
4. **In the game**, set the line prefixes the plugins listen for (these are
   mud-side, per character - copy the values from someone who has them):
   `aset room_short`, `aset look_monster`, `aset look_player` etc. with the
   `=S=`/`=M= `/`=P= ` style tags, and a plain `>` prompt.
5. `vtoggle` all the `mip_*` feeds ON (viking guild) for the status window.

The MIP handshake, maps, settings and window positions are all per-install
and sort themselves out.

## If something breaks

- Plugin errors after an update: Plugins dialog -> select it -> **Reinstall**.
- "Cannot load" + state file warning: delete the named file in
  `MUSHclient\worlds\plugins\state\` and Add the plugin again.
- Chaos bot lost: `cs set x y z` (read position from the map) or `cs reset`.
- Stats frozen at 0/0: check "[MIP] handshake sent" appeared; reconnect or
  Reinstall ThreeS_MIP.
