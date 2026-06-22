## 1. Install MUSHclient

1. Download from https://www.gammon.com.au/downloads/dlmushclient.htm
2. Install (default location is fine, e.g. `C:\Program Files (x86)\MUSHclient`).
3. Start MUSHclient once so it creates its `worlds` folder.

## 2. Install this package

1. Copy this whole `mushclient` folder somewhere permanent, e.g.
   `Documents\MUSHclient-3s\`. **Keep `3s_areas.lua` in the same folder as
   the plugin XML files** - the stepper loads it from there.
2. In MUSHclient: open (or create) **your own** world connected to the 3Scapes
   mud - File -> New World, then enter the 3Scapes address and your character.
   (Don't use someone else's `.mcl` world file - it has their login.)
3. With the world open: File -> Plugins -> Add, and add **in this order**:
   1. `3S_MIP.xml`           (stats + Viking feed - required by the others)
   2. `3S_Stepper.xml`       (the bot)
   3. `3S_VikingStatus.xml`  (graphical status window)
   4. `3S_ChaosSea.xml`      (chaos sea explorer with live map window)
4. File -> Save World File, so the plugins are remembered.


## 3. Mud-side setup (one time, required)

The plugins detect rooms, mobs, items and players by line **prefixes** the mud
prepends. Set them once with `aset` (stored mud-side, they persist). Type these
at the mud, one per line.

(If you already have another character of your own with these set, `aset_copy
<your-other-character>` copies them over — but it only works between your own
characters, so a fresh player should just set them manually below.)

`<ESC>` below is the **escape character (ASCII 27)** - in the colour codes it
must be a real ESC byte before the `[`. The colours are purely cosmetic, so the
simplest option is to **drop the colour codes** and set just the plain marker,
e.g. `aset room_short_pref =S=`. The plugins strip colour before matching, so
either way works.

    aset room_short_pref   <ESC>[33;1m=S=<ESC>[0m
    aset room_short_suff   <ESC>[33;1m=S=<ESC>[0m
    aset look_monster_pref <ESC>[36m=M= <ESC>[0m
    aset look_player_pref  <ESC>[32;1m=P= <ESC>[0m
    aset look_other_pref   <ESC>[34;1m=I= <ESC>[0m
    aset look_weapon_pref  <ESC>[34;1m=W= <ESC>[0m
    aset look_armor_pref   <ESC>[34;1m=A= <ESC>[0m
    prompt >$nl$
    setmod MAPCOLS CLEAR

### What each bot needs

- **Area bot (Stepper):** the `=S=` pair (`room_short_pref` + `room_short_suff`),
  `=M=` (`look_monster_pref`), `=P=` (`look_player_pref`), and the `>` prompt.
  It does **not** use the item markers.
- **Chaos Sea bot:** all of the above **plus** the item markers `=I=`/`=W=`/`=A=`
  (`look_other_pref` / `look_weapon_pref` / `look_armor_pref`). The `=I=` item
  line is how it spots the cask and stops.
- **Both:** the prompt (`prompt >$nl$`) is essential - every step, attack and the
  cask-pause fire on the `>` line.

**Not needed by either bot:** the `=X=` exit markers (`room_exits_pref/suff`) -
the chaos bot reads exits from the room short's `(s,w)`, and the area bot follows
a recorded path. `setmod MAPCOLS CLEAR` just keeps the room output clean.

The combat/movement triggers (`dealt the killing blow to...`, `There is no X
here.`, `You cannot go X.`) match the mud's **English messages**, not these
prefixes - so don't translate or alter those lines. The old `[MONSTAR!]` /
`[PLAYAR!]`-style prefixes are also recognised.

## 4. Using it

MIP connects automatically ~2s after login (you'll see "[MIP] handshake
sent"). HP/SP and enemy bars start immediately; run `vmapon` once to get
the Seid/Vig/Rad + settlement feed flowing into the status window.