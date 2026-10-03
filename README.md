# TurfCommand

A weather dashboard for bermudagrass lawns. TurfCommand runs on your Windows PC and shows:

- your conditions and the 7-day forecast
- live radar
- rain totals and how much irrigation you still need this week
- growing degree days (GDD) for PGR and mowing timing
- soil temperature for pre-emergent timing
- a sprayer mix calculator (TurfLab)

It works best with an Ecowitt weather gateway and sensors, but it also runs without any sensors.

> **This is an alpha.** It is shared with a few friends for testing. Expect rough edges. Tell the person who sent you this link when something looks wrong (see [Reporting a problem](#reporting-a-problem)).

**[Download the latest version](https://github.com/TurfCommand/Releases/releases/latest)**: under **Assets**, click `TurfCommand-Setup-<version>.exe`.

---

## What you need

- **A Windows 10 or 11 PC (64-bit)** that stays on. TurfCommand only collects weather while it is running. An always-on desktop or mini PC is ideal.
- **An internet connection**, for the forecast, radar and map.
- **A location in the lower 48 US states.** The radar and map cover only the continental US.
- **Optional: an Ecowitt gateway** (tested with the GW1200; GW1000, GW1100 and GW2000 should also work) on the **same home network** as the PC, with:
  - an outdoor temperature/humidity sensor
  - a soil temperature probe
  - a rain gauge

  Without a gateway, TurfCommand uses modeled weather for your location instead.
- **No administrator rights needed.** TurfCommand installs just for your Windows account.

## Install

1. Download `TurfCommand-Setup-<version>.exe` from the [latest release](https://github.com/TurfCommand/Releases/releases/latest) (under **Assets**).
2. Run it. **Windows will probably warn you** with a blue "Windows protected your PC" box. The installer isn't code-signed yet (signing certificates are expensive for an alpha), so Windows doesn't recognize the publisher. Click **More info**, then **Run anyway**.
3. In the installer:
   - Tick **Start TurfCommand when I sign in to Windows**. This is recommended, so it's always collecting.
   - Optionally tick **Create a desktop shortcut**.
   - Click through to finish.
4. If the installer says your PC needs the **Microsoft Edge WebView2 Runtime**:
   1. Click **Yes**.
   2. On Microsoft's page, download and install the **Evergreen Bootstrapper**.
   3. Run the TurfCommand installer again.

   Most Windows 10 and 11 PCs already have it.

TurfCommand installs to `%LOCALAPPDATA%\Programs\TurfCommand` and adds a Start menu entry.

## First-time setup

The first time TurfCommand opens, it walks you through a short setup. Everything you enter stays on your PC.

### 1. Location

- Type your city or ZIP and click **Search**, then pick the right match.
- Or click the map where your lawn is.

This sets the forecast, radar, and the time zone used for daily totals. After you save, TurfCommand downloads a detailed street map of your area once (about 40 MB). Until that finishes, the map is less detailed.

### 2. Weather data

**If you have an Ecowitt gateway:**
1. Click **Find my gateway**. TurfCommand searches your home network. With one gateway, it picks it and tests it for you.
2. If nothing is found, check these:
   - The gateway is powered.
   - The PC is on the **same network** as the gateway. A guest Wi-Fi network usually can't see other devices.

   You can also type the gateway's IP address yourself. Find it in your router's device list or in the **WS View Plus** app. Then click **Test connection**.
3. Check the sensor choices that appear:
   - **Air temperature & humidity**: pick your outdoor sensor.
   - **Soil temperature**: pick your soil probe.

   Each choice shows its current reading, so you can tell which is which. If it says "No rain gauge found", the rain meter stays empty.

**If you don't have sensors:** choose **No sensors**. TurfCommand uses modeled weather for your location (from Open-Meteo, updated every 15 minutes), and the dashboard marks those readings **· modeled**. Modeled soil temperature usually runs a few degrees warmer than a real probe, so treat the pre-emergent timing as a rough guide.

### 3. Ecowitt cloud (optional, but recommended with a gateway)

If your gateway also uploads to **ecowitt.net**, TurfCommand can:
- fill in readings missed while your PC was off;
- import your last 90 days of history.

You need two keys:
1. Sign in at [ecowitt.net](https://www.ecowitt.net).
2. Open **User Profile** and create an **Application Key** and an **API Key**.
3. Paste both into setup and click **Check and save keys**.

The keys are stored in Windows Credential Manager, not in a file. Uploading to ecowitt.net is set up in the WS View Plus app. If you never set that up, skip this section.

### 4. Your lawn

- **Last PGR application** and **Last mow**: enter the dates if you know them. They start the PGR and mowing counters. If you leave them blank, the counters start today, and the PGR card shows **Not Set** until you log an application.
- The PGR target, pre-emergent temperatures and sprayer settings come with sensible defaults. Change them later if you like.

Click **Save and open dashboard**. If you saved Ecowitt keys, the 90-day history import starts. It takes a minute or two, and you can open the dashboard while it runs.

## Everyday use

- **Closing the window doesn't quit TurfCommand.** It keeps collecting in the background, with an icon in the system tray (bottom right, near the clock; it may be under the **^** arrow).
- Right-click the tray icon for these options:
  - **Open TurfCommand**
  - **Start with Windows**
  - **Check for updates**
  - **Install updates automatically**
  - **Quit**
- **Settings** (gear button, top of the dashboard): change your location, gateway, keys and lawn settings. With Ecowitt keys saved, it also has **Import last 90 days**.
- **Keep it running.** Weather is only recorded while TurfCommand is running.
  - With Ecowitt keys, missed hours are filled in from the cloud later.
  - Without keys, missed hours are estimated.

## Updates

TurfCommand updates itself:

- It checks for a new version when it starts and every 6 hours.
- A new version downloads in the background and installs **around 3 AM**. TurfCommand closes and reopens by itself. There's no admin prompt.
- Every update is checked against a digital signature before it runs, so only genuine TurfCommand updates install.
- To update right away, right-click the tray icon and choose **Check for updates**.
- To turn automatic installs off, untick **Install updates automatically** in the tray menu. Updates then install only when you choose **Check for updates**.

## Uninstall

1. Open **Windows Settings → Apps**.
2. Find **TurfCommand** and choose **Uninstall**.
3. Windows asks whether to **also delete your TurfCommand data**: weather history, spray log, settings and saved Ecowitt keys.
   - Choose **No** (the default) to keep it for a later reinstall.
   - Choose **Yes** to remove everything.

## Known issues (alpha)

- **"Windows protected your PC" warning** at install: expected. The installer isn't code-signed yet. Use **More info → Run anyway**.
- **US only:** radar and the map cover the lower 48 states. Panning far from home shows where the radar and detailed map stop.
- **Modeled readings (no-sensor mode):** soil temperature runs warmer than a real probe, so the fall pre-emergent alert may come late.
- **A sensor in direct sun reads hot.** The temperature sensor built into the gateway (and any unshielded outdoor sensor) can read 15–20°F high in sunlight. That inflates GDD totals. Keep the sensor shaded, ideally in a radiation shield.
- **A new install has no history** unless you run the 90-day Ecowitt import. Until then, 7-day totals and 5-day soil averages fill in over the first week.
- **Only one copy can run.** If TurfCommand says port 8000 is already in use, another copy (or another program) is using it. Quit the other copy from its tray icon, or restart the PC.

## Privacy

TurfCommand runs entirely on your PC. The dashboard is only reachable from that PC, not from your network or the internet. It has no account and sends no tracking or usage data.

It contacts these services:

| Service | What for |
| --- | --- |
| Open-Meteo | Forecast, place search, modeled weather |
| NOAA | Radar |
| Protomaps | The one-time map download for your area (OpenStreetMap data) |
| GitHub | Update checks |
| ecowitt.net | Only if you saved keys |
| Your Ecowitt gateway | Local readings, on your home network |

Your data lives in `%LOCALAPPDATA%\TurfCommand`.

## Reporting a problem

Tell the person who sent you this link. Include:

- what you were doing;
- what you saw (a screenshot helps);
- the TurfCommand version, shown at the top of the dashboard.

For errors, also send the log files from `%LOCALAPPDATA%\TurfCommand\logs`. To find them, paste that path into the File Explorer address bar.

---

TurfCommand is proprietary software (© Zachary Marcille). Third-party credits and licenses ship with the app (`THIRD_PARTY_NOTICES.md` and the `licenses` folder in the install directory). Map data © OpenStreetMap contributors. Weather data by Open-Meteo.com (CC BY 4.0). Radar: NOAA MRMS.
