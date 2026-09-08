# Battery Checker — a battery monitor for Windows

> A long-term check-up for your laptop battery: wear level, charge history, what is draining it, and low-battery
> alerts — all in one tool that installs in a few megabytes.
> No account, no sign-in, no extra runtime to install. Download, install, done.

[简体中文版](./README.zh.md)

<!--
  Screenshots pending: drop images into docs/assets/screenshots/, then uncomment the matching
  image lines in the Preview section below. Suggested captures, in order:
  1. dashboard.png    Home: wave gauge + power/time rows + Battery Health + Battery Details
  2. trend.png        Battery Level & Power: the two charts aligned above each other
  3. processes.png    High Power Processes + Battery Usage by App
  4. health.png       Health Statistics + health history chart
  5. alerts.png       Smart Alerts (both threshold sliders)
  6. settings.png     Settings (Appearance / System / Software Update)
-->

## Preview

<!-- ![Home: the wave gauge and battery health](assets/screenshots/dashboard.png) -->
<!-- ![Battery level and power over time](assets/screenshots/trend.png) -->
<!-- ![Process and per-app usage rankings](assets/screenshots/processes.png) -->
<!-- ![Health statistics and history curve](assets/screenshots/health.png) -->
<!-- ![Smart alert thresholds](assets/screenshots/alerts.png) -->
<!-- ![Settings](assets/screenshots/settings.png) -->

> The screenshots are not in yet. The layout itself: a narrow icon-only sidebar on the left with six
> pages — Battery · Trend · Processes · Alerts · Health · Settings — in a light or dark theme.

---

## Why bother

Windows tells you "43% left" and stops there:

| What you want to know | Windows gives you | Battery Checker |
|---|---|---|
| How much life is left in this battery, and how far it has worn down | Nothing in the UI — you have to run `powercfg /batteryreport` yourself | Health percentage plus a long-term history curve |
| When it was charging, to what level, when you unplugged | Not shown | Charge history chart, going back a year |
| How many watts it draws right now, and how long that leaves you | A vague "time remaining" | Live charge / discharge power + Time to Full and Time Left |
| Which program is eating the battery | CPU only, in Task Manager | High Power Processes + per-app usage share |
| A heads-up when the charge gets low | One fixed system banner | Thresholds you choose, for low battery and full charge |

Nothing here is estimated from thin air: charge, power, design capacity and full-charge capacity are all
read directly from the battery driver.

---

## What you get

### Battery Power (home page)

- **Wave gauge**: live charge level — green above 60%, amber 21-60%, red at 20% or below, with a bolt above
  the number while charging. **Click the gauge to refresh.**
- **Power and time, two rows**: Charge Rate / Discharge Rate in watts, plus Time to Full and Time Left —
  computed from the driver's instantaneous rate, not from the vague figure Windows reports.
- **Battery Health**: health percentage, design capacity, full charge capacity, cycle count, and a plain
  verdict — excellent / good / fair / may need replacement soon.
- **Battery Details**: battery name, manufacturer, serial number, chemistry (for example LION).

### Battery Level & Power (trend page)

- **Battery Level Trend**: charging in green, discharging in amber, so you can see at a glance which day you
  charged to what level and when the laptop finally gave out.
- **Charge / Discharge Power**: shares the range above and is aligned with it, so you can watch the charge
  rate fall away as the battery nears full.
- Pick any date range, with quick chips for 1 d / 3 d / 7 d / 1 mo / 1 yr. Defaults to today.

### Processes (power rankings)

- **High Power Processes**: top 12 by CPU usage plus memory, normalized over logical cores into whole-machine
  percentages — not per-core numbers, which would read several times too high.
- **Battery Usage by App**: each app's share of your usage over the range you pick.
- Both rankings let you **double-click a name** or use **right-click → Open File Location** to reveal that
  program in Explorer.

### Smart Alerts

- **Low Battery Alert**: a system notification when the charge drops to your threshold; adjustable 5-65%,
  default 20%.
- **Full Charge Alert**: a notification when the charge reaches your threshold; adjustable 50-100%, default 80%.
- An alert fires once, at the moment the threshold is crossed. It will not nag you every five seconds.
- If Windows has notifications switched off at the system level, the top of this page says so and tells you
  where to turn them on — you never have to wonder whether the alert was silently thrown away.

### Health (statistics page)

- Current health, cycle count, full charge capacity, and the 30-day change.
- **Health History**: 1-12 months, 2 / 3 / 5 years, or All — the chart that answers "should I replace this battery?"

### Settings

- Appearance: Light, Dark, or Follow System.
- Language: English / Simplified Chinese — the interface, chart axes and dates all follow along.
- System: Minimize to Tray, Start with Windows.
- Software Update: check manually.

### Always there

- **System tray**: closing the window only hides it, monitoring continues. **Left-click** the tray icon to bring
  the window back, **right-click** for the Show / Quit menu. To really exit, use the power button at the bottom
  of the sidebar (it asks first).
- **Automatic updates**: a new version is offered in a dialog — download, install and restart in one click, or
  skip that specific version.

---

## Getting started (3 minutes)

1. Grab the installer (links below) and run it — no administrator rights required.
2. On first launch you immediately see charge, power and health.
3. Open Smart Alerts and set a low-battery threshold you actually like (around 30% if you are often on the move).
4. Want recording to start with the machine? Settings → System → Start with Windows.
5. After a week or two, come back to the Trend and Health pages: that is where your charging habits and the
   wear curve show up.

> Note: the close button hides the app to the tray, it does not quit it. If the tray icon ever disappears and
> you would rather not reboot, end `battery-checker.exe` in Task Manager.

---

## Download and install

| Where | Link |
|---|---|
| Gitee (faster from mainland China) | https://gitee.com/ShiXiongZhiDao/BatteryChecker/releases |
| GitHub | https://github.com/ShiXiongZhiDao/BatteryChecker/releases |

- The installer looks like `Battery Checker_1.1.12_x64-setup.exe` (NSIS, around 3-4 MB). An `.msi` with the same
  version number is published alongside it for deployment scenarios.
- It installs per-user, into your own profile — **no UAC prompt, no administrator rights**.
- The installer itself is available in Simplified Chinese and English.

### Requirements

- Windows 10 or Windows 11, 64-bit.
- WebView2 Runtime (built into Windows 11; on Windows 10 it is usually already present via Windows Update, and
  the installer will point you at the download if it is missing).
- A machine with a **built-in battery**. On a desktop the app still installs and runs, but every page shows
  "No battery detected".

### "Windows protected your PC" during setup

That is SmartScreen reacting to an **unsigned** installer — this project does not carry a paid code-signing
certificate. It is not a virus. Choose **More info** → **Run anyway**. The source and the installer live in the
same repository, so you are welcome to check them against each other.

---

## Updates, your data, uninstalling

### Automatic updates

- The app **checks once every time it starts**. When a newer version exists, a dialog offers Update, Later, or
  Skip This Version (the last one remembers that version and stops bothering you about it).
- You can also check by hand: Settings → Software Update → Check for Updates. If nothing newer exists you get
  "You're already on the latest version".

### Will updating throw away my history?

No. An update only replaces program files; your history and settings stay exactly where they are.

### Uninstalling

Remove Battery Checker under Settings → Apps → Installed apps (Windows 10: Apps & features). The uninstaller
**does not delete** the data folder above. To clear everything — before passing the machine on, for example —
delete `%APPDATA%\com.shixiong.battery-checker` afterwards.

---

## Privacy

- **Battery data, the process list and the per-app ranking stay in local files on your machine. They are never
  uploaded.** The app does not collect or transmit any battery reading at all.

---

## Frequently asked questions

**Q: I set a low-battery alert but nothing ever popped up.**
Check whether the Smart Alerts page shows "Windows notifications are off — alerts will not appear." at the top.
If it does, the system-level switch is off: Settings → System → Notifications → "Get notifications from apps and
other senders". Also remember an alert fires only when the threshold is **crossed**: if the charge is already
below it when the app starts, that is reported once on the first reading, but bouncing around below the threshold
afterwards will not repeat it.

**Q: Cycle count shows `—`. Is something broken?**
No. That number has to be reported by the battery firmware, and plenty of laptops simply do not report it —
`powercfg /batteryreport` shows `-` for those too. The app refuses to invent a figure, so it shows `—`.

**Q: Why does health jump between 94% and 96%?**
Full-charge capacity itself varies by about 1% between readings (on one battery, measured between 58264 and
59407 mWh), which is enough to flip the rounded percentage. Health snapshots are therefore only appended when
the change exceeds 3% of design capacity or the cycle count moves, so the curve does not fill up with fake wear steps.

**Q: Time to Full / Time Left shows `—`.**
That happens when the battery driver does not report an instantaneous rate, reports capacity only as a relative
value, or the rate is below 1 W (trickle charging, or already full). An honest "unknown" beats a number that jumps around.

**Q: The Trend and Health pages are empty.**
Records are only written while the app is running. Freshly installed, or mostly quit, means mostly empty charts.
Turn on Start with Windows and let it sit in the tray.

**Q: How accurate is Battery Usage by App?**
It is an **estimate**: shares are derived from CPU time, with no weighting for GPU, screen or disk (so a browser
playing video comes out low), and it only covers the periods the app was running. The card subtitle says as much.
For system-level figures use `powercfg /srumutil`, which needs administrator rights.

**Q: Some system processes are missing from the process ranking.**
Without elevation, protected processes cannot be read, so they are absent from the list. That is a permission
limit, not a bug.

**Q: New machine or reinstalled Windows — can I take my history with me?**
Yes. Copy the whole `%APPDATA%\com.shixiong.battery-checker\` folder to the same path on the new machine; the
identifier matches, so recording simply continues.

**Q: My antivirus flags the installer.**
Small unsigned tools do get false positives occasionally. 

---

## Current version and changelog

- Current version: **v1.1.16**

## ☕ Support the Author

If this little tool saved you some time, you can buy the author a coffee — your support keeps the project improving:

<table>
  <tr>
    <th align="center">Alipay</th>
    <th align="center">WeChat</th>
  </tr>
  <tr>
    <td align="center">
      <img src="zhifubao.jpg" width="220" alt="支付宝">
    </td>
    <td align="center">
      <img src="weixin.png" width="220" alt="微信">
    </td>
  </tr>
</table>

## License

This tool is **free to use**.

<!-- TODO (maintainer): there is no LICENSE file in the repository yet; finalize the wording below once the terms are decided -->
No standard license file has been added to the repository yet, and the terms will be stated separately. Until
then, treat this project as **all rights reserved** and do not redistribute the source or the installer commercially.
