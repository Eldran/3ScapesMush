# 3ScapesMush — MUSHclient plugin suite

A set of [MUSHclient](https://www.gammon.com.au/mushclient) plugins for the
**3Scapes** MUD, focused on the Viking settlement and Chaos Sea content. They
share a single live data feed (MIP) and add graphical windows, automation bots,
and quality‑of‑life tools.

All windows are draggable miniwindows; the bots drive the game step‑by‑step and
can be paused/stopped at any time.

## Plugins

| File | Plugin | What it does |
|------|--------|--------------|
| `3S_MIP.xml` | ThreeS_MIP | **Required by everything else.** Parses the MUD's MIP/BBE feed (stats, enemy, and the Viking settlement data) and broadcasts it to the other plugins. |
| `3S_VikingStatus.xml` | Viking Status | Tabbed graphical status window for your settlement — Stats, City, People, Settlers, Goods, Holds, Sea, Map, Mission, Feeds. Clickable travel, mission/errand actions, patrol commit, and more. |
| `3S_Stepper.xml` | Area bot | Walks pre‑recorded area routes and kills the area's mobs. Record new routes from the window, loop runs, rewind to the start, pause/resume. Hosts the shared **Bots** window (Area / Chaos / Deadman tabs). |
| `3S_ChaosSea.xml` | Chaos Sea | Explores the Chaos Sea, mapping rooms on a 3D grid and fighting as it goes. Pauses when it finds the cask; one‑click "New Sea" with a 60‑minute cooldown timer. |
| `3S_Mapper.xml` | ThreeS_Mapper | Maps wherever you walk (one map per named area) in a draggable window. Click a room to walk there; right‑click to resync "I am here". Auto‑suspends while a bot is driving. |
| `3S_Chat.xml` | ThreeS_Chat | Captures all chat channels and tells into a timestamped, colour‑coded window with scrollback, and logs them to `3s_chat.log`. |

Supporting files:

- `3s_areas.lua` — area route + mob data for the Area bot (kept next to the plugins; new recordings are appended here).
- `COMMANDS.md` — full command reference for every plugin.
- `README-MUSHclient.md` — step‑by‑step install / setup guide.

## Quick start

1. Install MUSHclient and open your 3Scapes world.
2. Add the plugins via **File → Plugins → Add**, in this order (MIP first — the
   others depend on its feed):
   1. `3S_MIP.xml`
   2. `3S_Stepper.xml`
   3. `3S_VikingStatus.xml`
   4. `3S_ChaosSea.xml`
   5. `3S_Mapper.xml` / `3S_Chat.xml` (optional)
3. Save the world file so the plugins are remembered.
4. After login, run `vmapon` once to start the Viking settlement feed.

See **[README‑MUSHclient.md](README-MUSHclient.md)** for the detailed walkthrough
and the one‑time mud‑side requirements, and **[COMMANDS.md](COMMANDS.md)** for
every command.

## Requirements

- MUSHclient (Windows).
- A 3Scapes character with the standard `aset` line prefixes
  (`=S=`, `=M=`, `=P=`, `=I=`, …) — these are stored mud‑side and carry over
  automatically.

## Notes

- `3S_MIP` must be loaded for any of the windows to show live data.
- Personal/session files (`Goran_3Scapes.mcl`, `3s_chat.log`, feed dumps, logs)
  are git‑ignored.
