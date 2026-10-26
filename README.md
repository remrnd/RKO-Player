# RKO Player

A retro cable-TV station player for Linux and SteamOS (Steam Deck friendly). It runs in its own full-screen window, not a browser tab. Load your own videos, set up channels, build a 24-hour schedule, and flip through it like cable: weather channel, TV guide, commercial breaks, block sign-ons and all.

> RKO Player ships **no media**. You supply your own video files and links.

---

## Features

**Channels**
- **CH 0: Weather.** Live weather with a 5-day forecast (Open-Meteo, free, no API key).
- **CH 1: Guide.** Scrolling TV guide with block names and optional channel logos.
- **CH 2+: Your channels.** Add as many as you like, each with a name and optional logo.

**Library** (Settings → Library)
- **Search-first library:** the Library opens clean. Type in the search bar to pull up any show, movie, commercial or block at once, or tap a tab to browse (tap again to collapse).
- Drop or add files and whole folders; sort them into **Shows**, **Movies** or **Commercials**.
- **Commercial groups A to Z:** sort your commercials into groups and use a whole group in a block break, on the schedule, or in a Commercial Flow break.
- Add links: YouTube, Vimeo, Dailymotion, Archive.org or direct `.mp4` links. Links stream only; nothing is downloaded or saved.
- **Blocks**: group shows into a named programming block (think Saturday cartoon blocks).
  - **Sign On Video** plays before the block's first item.
  - **Sign Off Video** plays after its last item.
  - **+ Add break** puts a commercial break inside the block. Each break can pull from the Commercial Flow or from a specific commercial group.
- **Schedule**: place shows, movies or blocks at exact start times on a 24-hour grid. Scheduled start times win, and anything can run across midnight. Optional auto-fill for gaps.
- **Commercial Flow**: build your commercial breaks by drag and drop (see below).

**Look**
- 4 guide skins: Night Cable, Sky Dish, Reel Time, Big Cable.
- 5 picture effects: CRT, 90's Fuzz, 2003 Clear, Problematic VHS, Off.
- Choice of guide and TV fonts, remote-button styles, and channel logos in the guide.
- Gradient Settings menu that follows the colors of the skin you pick.

**Extras**
- **Planner**, **Save Slots** (swap whole setups), **Sleep** (1989 sign-off, ocean, white or fan noise, swim), and an **alarm** with 6-minute snooze.
- Weather screen changes with time of day (day, dawn, dusk, twilight, night).

---

## Install

**Needs:** Linux x64 (SteamOS works), internet once to fetch the Electron runtime (~100 MB).

```bash
bash rko-player.sh              # install on first run, then launch
bash rko-player.sh --install    # install only
bash rko-player.sh --uninstall  # remove everything
```

No internet? Download `electron-v33.2.0-linux-x64.zip` from the Electron releases page and put it next to the script. It is used automatically.

It installs to `~/.local/share/rko-player` and adds a menu entry (plus a Desktop icon if you have a `~/Desktop` folder).

**Steam Deck:** in Desktop Mode, right-click the installed launcher and add it to Steam (or use *Add a Non-Steam Game*) to launch it from Game Mode.

**Controls:** Up/Down arrows change channel, Left/Right change volume, **F11** toggles full screen, **Ctrl+Q** quits.

---

## Manual

### 1. Add your media
1. Open **Settings → Library**.
2. Choose **Add as** (Shows, Movies or Commercials) and **On channel**, then drop files or folders, or use **Add files** / **Add folder**.
3. For links, open **Add a link**, paste the URL, give it a guide label and a length in minutes.

**Find things fast:** the Library starts collapsed. Type in the search bar to search shows, movies, commercials and blocks together. Results can be edited, regrouped or scheduled right there, and block results have an **Open** button. Type `group A` to list every clip in that group. Tap a tab (Shows, Movies, Commercials, Blocks) to browse that list instead, and tap it again to hide it.

### 2. Set up channels
**Settings → Channels** → **+ Add channel**. Name it and optionally add a logo.

### 2b. Commercial groups
1. Open **Library → Commercials**, expand a clip and choose a **Group** (A to Z).
2. Use the group filter above the list to see each group with its clip count and total length.
3. Use a group:
   - **In a block:** on a break row, change the dropdown from "Commercial Flow" to "Group A" (and so on).
   - **On the schedule:** pick it under "Commercial groups" and set a start time.
   - **In Commercial Flow:** use **+ Add group…** on a break.
4. Anywhere a group is used as a break, it fills up to 4:00 with the clips that fit.

### 3. Build blocks
1. **Library → Blocks → + New block**, name it.
2. Pick a **Sign On Video** and/or **Sign Off Video** (any local video file).
3. Add shows or movies from the dropdown; reorder with the arrows.
4. Press **+ Add break** wherever you want a commercial break, then choose its source: **Commercial Flow** (the default) or a **Group A to Z**.
5. Press **Schedule this block** to place it.

A block's guide time covers everything: sign-on, shows, breaks and sign-off. No commercials play directly after a sign-on or sign-off video.

### 4. Schedule
**Library → Schedule**: choose the channel, pick a show, movie, block or commercial group, set a start time and add it. A scheduled group plays at that time (up to 4:00). Gaps are filled automatically if auto-fill is on for that channel.

### 5. Commercial Flow
**Library → Commercial Flow** controls what plays in every break.
- **+ New break** makes a 4:00 slot.
- Drag clips from the **Commercial Pool** into a break. Drag within a break to reorder, between breaks to move, or back to the pool to remove. A clip can be used in more than one break.
- Each break has a bar showing how full it is (for example `2:35 / 4:00 · 65% filled · 1:25 left`). Grey is under 50%, amber 50 to 89%, green 90% and up.
- A drop that would pass 4:00 is refused. **Auto-fill** adds clips that still fit.
- Prefer not to drag? Use the **+ Add commercial…** dropdown and the **×** button on each clip.
- Your breaks **rotate** in order: Break 1, Break 2, and so on, across the day. This covers breaks after shows and the break slots inside blocks.
- Each break also has **+ Add group…**, which adds every clip from a group that still fits.
- With no Flow breaks defined, RKO Player falls back to the automatic commercial fill (up to 4:00 per break).

### 6. Weather
**Settings → Weather (Channel 0)**: enter a US zip code or a city name, choose °F or °C, and press **Update now**. It refreshes every 30 minutes and whenever the network returns. The manual High/Low/Condition fields are only a fallback for when you are offline.

---

## Limitations

- **Linux x64 only.** No Windows, macOS or ARM builds.
- **Media is yours.** Nothing is bundled. File-based items need access to the original file path (works in the installed app; not in a plain browser).
- **Link playback depends on the host.** Streams from YouTube, Vimeo, Dailymotion and others can break if the site changes or blocks embedding. Links also need internet, and you enter the length yourself.
- **Weather needs internet.** US zip codes use zippopotam.us; anything else is looked up as a city name via Open-Meteo, so outside the US use a city name. Offline, the last known or manual values are shown.
- **Fonts** are fetched online; offline you get fallback fonts.
- **Breaks are capped at 4:00**, including a scheduled commercial group, so clips that don't fit are skipped. Commercial Flow breaks rotate in order, and you cannot yet pin one specific Flow break to a spot in a block (you can pin a commercial group instead).
- **Groups are A to Z (26 max)**, and a commercial belongs to one group at a time.
- **Sign On/Off videos** are local files only (no links), and a video shorter than 1 second is rejected.
- **Not an official product** of, or affiliated with, any network or brand. Sign-on and sign-off ideas are inspired by classic TV blocks.

---

## Troubleshooting

| Problem | Try this |
|---|---|
| Electron download fails | Download the zip manually and place it next to the script |
| Window won't start | Run `bash rko-player.sh` in a terminal and read the output |
| A video won't play | Check the codec (H.264 MP4 or WebM is safest) and that the file hasn't moved |
| Weather says "not found" | Use a 5-digit US zip or a city name; check your connection |
| Need a clean slate | `bash rko-player.sh --uninstall`, then reinstall |

---

## Uninstall
```bash
bash rko-player.sh --uninstall
```
