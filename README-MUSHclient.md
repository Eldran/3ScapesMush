## 1. Install MUSHclient

1. Download from https://www.gammon.com.au/downloads/dlmushclient.htm
2. Install (default location is fine, e.g. `C:\Program Files (x86)\MUSHclient`).
3. Start MUSHclient once so it creates its `worlds` folder.

## 2. Install this package

1. Copy this whole `mushclient` folder somewhere permanent, e.g.
   `Documents\MUSHclient-3s\`. **Keep `3s_areas.lua` in the same folder as
   the plugin XML files** - the stepper loads it from there.
2. In MUSHclient: File -> Open World -> pick `Goran_3Scapes.mcl`.
3. With the world open: File -> Plugins -> Add, and add **in this order**:
   1. `3S_MIP.xml`           (stats + Viking feed - required by the others)
   2. `3S_Stepper.xml`       (the bot)
   3. `3S_VikingStatus.xml`  (graphical status window)
   4. `3S_ChaosSea.xml`      (chaos sea explorer with live map window)
4. File -> Save World File, so the plugins are remembered.


## 3. Mud-side requirement (one time)

The scripts rely on the same `aset` prefixes you already use on Goran
(`=S=` room short, `=M= ` monsters, `=P= ` players, `=K=` kill blows,
`=A=/=W=/=I=` items). Since these are stored mud-side, nothing to do -
they carry over automatically. The old `[MONSTAR!]`-style prefixes are
also recognized.

## 4. Using it

MIP connects automatically ~2s after login (you'll see "[MIP] handshake
sent"). HP/SP and enemy bars start immediately; run `vmapon` once to get
the Seid/Vig/Rad + settlement feed flowing into the status window.