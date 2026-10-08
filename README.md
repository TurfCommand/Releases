# TurfCommand

A weather dashboard for bermudagrass lawns. TurfCommand runs on your Windows PC or Mac and shows:

- your conditions and the 7-day forecast
- live radar
- rain totals and how much irrigation you still need this week
- growing degree days (GDD) for PGR and mowing timing
- soil temperature for pre-emergent timing
- a sprayer mix calculator (TurfLab)

It works best with an Ecowitt weather gateway and sensors, but it also runs without any sensors.

> **This is an alpha.** It is shared with a few friends for testing. Expect rough edges. Tell the person who sent you this link when something looks wrong (see [Reporting a problem](#reporting-a-problem)).

**[Download the latest version](https://github.com/TurfCommand/Releases/releases/latest)**. Under **Assets**, click:
- **Windows:** `TurfCommand-Setup-<version>.exe`
- **Mac:** `TurfCommand-<version>-mac.dmg`

---

## What you need

- **A computer that stays on.** TurfCommand only collects weather while it is running. An always-on desktop or mini PC is ideal.
  - **Windows:** Windows 10 or 11 (64-bit).
  - **Mac:** a Mac with Apple silicon (M1 or newer) on macOS 13 Ventura or later. Intel Macs aren't supported yet.
- **An internet connection**, for the forecast, radar and map.
- **A location in the lower 48 US states.** The radar and map cover only the continental US.
- **Optional: an Ecowitt gateway** (tested with the GW1200; GW1000, GW1100 and GW2000 should also work) on the **same home network** as the computer, with:
  - an outdoor temperature/humidity sensor
  - a soil temperature probe
  - a rain gauge

  Without a gateway, TurfCommand uses modeled weather for your location instead.
- **No administrator rights needed on Windows.** TurfCommand installs just for your Windows account.

## Install on Windows

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

## Install on a Mac

1. Download `TurfCommand-<version>-mac.dmg` from the [latest release](https://github.com/TurfCommand/Releases/releases/latest) (under **Assets**) and open it.
2. In the window that opens, **drag TurfCommand onto the Applications folder**. It has to live in Applications to update itself, so don't run it straight from the download.
3. Open TurfCommand from your Applications folder. **macOS will block it the first time** with a message that it "can't be verified" or that Apple "could not verify" it. The app isn't notarized by Apple yet (that needs a paid Apple developer account, which this alpha doesn't have). Click **Done**, then:
   1. Open **System Settings → Privacy & Security**.
   2. Scroll down to the message about TurfCommand and click **Open Anyway**.
   3. Enter your Mac's password if asked, then click **Open Anyway** again.

   You only do this once.
4. If macOS asks whether TurfCommand may **find devices on your local network**, click **Allow**. TurfCommand needs this to read your Ecowitt gateway.
5. **Keep the Mac awake.** A sleeping Mac collects nothing. In **System Settings**, open **Energy** (called **Energy Saver** on some versions) on a desktop Mac, or **Battery → Options** on a laptop, and turn on **Prevent automatic sleeping** (on a laptop: *on power adapter*) **when the display is off**. The screen can still turn off.

## First-time setup

The first time TurfCommand opens, it walks you through a short setup. Everything you enter stays on your computer.

### 1. Location

- Type your city or ZIP and click **Search**, then pick the right match.
- Or click the map where your lawn is.

This sets the forecast, radar, and the time zone used for daily totals. After you save, TurfCommand downloads a detailed street map of your area once (about 40 MB). Until that finishes, the map is less detailed.

### 2. Weather data

**If you have an Ecowitt gateway:**
1. Click **Find my gateway**. TurfCommand searches your home network. With one gateway, it picks it and tests it for you.
2. If nothing is found, check these:
   - The gateway is powered.
   - The computer is on the **same network** as the gateway. A guest Wi-Fi network usually can't see other devices.
   - **On a Mac:** TurfCommand is allowed on the local network (**System Settings → Privacy & Security → Local Network**, TurfCommand switched on).

   You can also type the gateway's IP address yourself. Find it in your router's device list or in the **WS View Plus** app. Then click **Test connection**.
3. Check the sensor choices that appear:
   - **Air temperature & humidity**: pick your outdoor sensor.
   - **Soil temperature**: pick your soil probe.

   Each choice shows its current reading, so you can tell which is which. If it says "No rain gauge found", the rain meter stays empty.

**If you don't have sensors (yet):** choose **No sensors**. TurfCommand uses modeled weather for your location (from Open-Meteo, updated every 15 minutes), and the dashboard marks those readings **· modeled**. Modeled soil temperature usually runs a few degrees warmer than a real probe, so treat the pre-emergent timing as a rough guide. When your gateway is set up later, switch to it in **Settings**.

### 3. Ecowitt cloud (optional, but recommended with a gateway)

If your gateway also uploads to **ecowitt.net**, TurfCommand can:
- fill in readings missed while your computer was off;
- import your last 90 days of history.

You need two keys:
1. Sign in at [ecowitt.net](https://www.ecowitt.net).
2. Open **User Profile** and create an **Application Key** and an **API Key**.
3. Paste both into setup and click **Check and save keys**.

The keys are stored in Windows Credential Manager or the macOS Keychain, not in a file. Uploading to ecowitt.net is set up in the WS View Plus app. If you never set that up, skip this section.

### 4. Your lawn

- **Height of cut**: how short you mow, in inches (for example 0.5). The Mowing Pressure card uses it to tell you when to mow: **Low pressure**, **Mow soon**, **Mow**, **Mow now**, **Overdue**. Leave it blank to see just the GDD count. Heights above 1" use estimated levels.
- **Last PGR application** and **Last mow**: enter the dates if you know them. They start the PGR and mowing counters. If you leave them blank, the counters start today, and the PGR card shows **Not Set** until you log an application.
- The PGR target, pre-emergent temperatures, weekly irrigation target and sprayer settings come with sensible defaults. Change them later if you like.

Click **Save and open dashboard**. If you saved Ecowitt keys, the 90-day history import starts. It takes a minute or two, and you can open the dashboard while it runs.

## Everyday use

- **Closing the window doesn't quit TurfCommand.** It keeps collecting in the background.
  - **Windows:** the window hides to the system tray icon (bottom right, near the clock; it may be under the **^** arrow).
  - **Mac:** the window goes to the Dock; click TurfCommand in the Dock to bring it back. The TurfCommand icon also sits in the menu bar at the top of the screen.
- The tray icon (Windows, right-click) and the menu-bar icon (Mac) have:
  - **Open TurfCommand**
  - **Full screen**: fills the whole screen with no window frame, handy for a wall display. You can also press **F11** in the TurfCommand window; **Esc** leaves full screen. Each computer remembers its own choice.
  - **Start with Windows** / **Start at login**
  - **Check for updates** and **Install updates automatically**
  - **Save logs for support…** and **Open log folder** (see [Reporting a problem](#reporting-a-problem))
  - **Quit**: the way to really quit TurfCommand.
- **Settings** (gear button, top of the dashboard): change your location, gateway, keys and lawn settings. With Ecowitt keys saved, it also has **Import last 90 days**.
- **Keep it running.** Weather is only recorded while TurfCommand is running.
  - With Ecowitt keys, missed hours are filled in from the cloud later.
  - Without keys, missed hours are estimated.

## Updates

TurfCommand updates itself:

- It checks for a new version when it starts and every 6 hours.
- A new version downloads in the background. If TurfCommand finds it right after starting, it installs right away; otherwise it installs **around 3 AM**, or the next time your computer is on after a 3 AM it slept through. TurfCommand closes and reopens by itself.
- Every update is checked against a digital signature before it runs, so only genuine TurfCommand updates install.
- To update right away, choose **Check for updates** in the tray or menu-bar icon.
- To turn automatic installs off, untick **Install updates automatically**. Updates then install only when you choose **Check for updates**.
- **Mac:** updates only install when TurfCommand is in your **Applications** folder. If you saved Ecowitt keys, macOS may ask after an update whether TurfCommand may use them from your Keychain: enter your Mac's password and click **Always Allow**.

## Sharing with other computers at home (optional)

If you have more than one computer, one of them can be the TurfCommand that collects, and the others can show it:

1. On the computer that stays on: **Settings → Sharing → Share this TurfCommand on my home network**, save, then quit and reopen TurfCommand. Settings then shows its address.
2. On another computer with TurfCommand installed: **Settings → Use the TurfCommand on another PC**, enter that address, then **Test** and **Use it and restart**. To go back, choose **Stop viewing** in its tray or menu-bar icon.

Anyone on your home Wi-Fi can then open the shared dashboard and change its settings, so only turn sharing on for a home network you trust.

## Uninstall

**Windows:**
1. Open **Windows Settings → Apps**.
2. Find **TurfCommand** and choose **Uninstall**.
3. Windows asks whether to **also delete your TurfCommand data**: weather history, spray log, settings and saved Ecowitt keys.
   - Choose **No** (the default) to keep it for a later reinstall.
   - Choose **Yes** to remove everything.

**Mac:**
1. In the menu-bar icon, untick **Start at login**, then choose **Quit**.
2. Drag **TurfCommand** from Applications to the Trash.
3. To also remove your data, delete the folder `~/Library/Application Support/TurfCommand` (in Finder, **Go → Go to Folder…** and paste that path). Saved Ecowitt keys are in **Keychain Access**, listed under `TurfCommand:EcowittCloud`.

## Known issues (alpha)

- **Security warnings at install:** expected on both systems for now. Windows: **More info → Run anyway**. Mac: **System Settings → Privacy & Security → Open Anyway**.
- **US only:** radar and the map cover the lower 48 states. Panning far from home shows where the radar and detailed map stop.
- **Modeled readings (no-sensor mode):** soil temperature runs warmer than a real probe, so the fall pre-emergent alert may come late.
- **A sensor in direct sun reads hot.** The temperature sensor built into the gateway (and any unshielded outdoor sensor) can read 15–20°F high in sunlight. That inflates GDD totals. Keep the sensor shaded, ideally in a radiation shield.
- **A new install has no history** unless you run the 90-day Ecowitt import. Until then, 7-day totals and 5-day soil averages fill in over the first week.
- **Only one copy can run.** If TurfCommand says port 8000 is already in use, another copy (or another program) is using it. Quit the other copy, or restart the computer.
- **Mac (new):** this is the Mac version's first alpha. The menu-bar icon, the Dock behavior and **Start at login** are the parts most likely to need fixes. If **Cmd+Q** doesn't quit, use **Quit** in the menu-bar icon.

## Privacy

TurfCommand runs entirely on your computer. Unless you turn on sharing (above), the dashboard is only reachable from that computer, not from your network or the internet. It has no account and sends no tracking or usage data.

It contacts these services:

| Service | What for |
| --- | --- |
| Open-Meteo | Forecast, place search, modeled weather |
| NOAA | Radar |
| Protomaps | The one-time map download for your area (OpenStreetMap data) |
| GitHub | Update checks |
| ecowitt.net | Only if you saved keys |
| Your Ecowitt gateway | Local readings, on your home network |

Your data lives in `%LOCALAPPDATA%\TurfCommand` (Windows) or `~/Library/Application Support/TurfCommand` (Mac).

## Reporting a problem

Tell the person who sent you this link. Include:

- what you were doing;
- what you saw (a screenshot helps);
- the TurfCommand version, shown at the top of the dashboard.

For errors, also send the logs: choose **Save logs for support…** in the tray or menu-bar icon (or **Settings → Help**). It saves one file, `TurfCommand-logs-<date>-<time>.zip`, to your Desktop and shows it to you. Send that file. Your home coordinates and your user name are removed from it, and it never includes your settings, keys or history.

---

TurfCommand is proprietary software (© Zachary Marcille). Third-party credits and licenses ship with the app (`THIRD_PARTY_NOTICES.md` and the `licenses` folder in the install directory). Map data © OpenStreetMap contributors. Weather data by Open-Meteo.com (CC BY 4.0). Radar: NOAA MRMS.
