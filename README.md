# Torn War Helper

A Tampermonkey userscript for Torn's ranked war page. It adds extra info and alerts on that page only. It never clicks Attack, never opens pages for you, and never automates any game action.

Made by **Everwood [62912]** of **Aqua**.

## What it does

- Shows **stats** and a **group tag** (G1 / G2 / G3) next to each enemy, from your target Google Sheet
- Live **hospital countdown** on enemies in hospital, then a count-up after they leave
- Optional short **beep** when an enemy you saw in hospital comes out (only while the Torn tab is in front)
- **Wide** or **side-by-side** layout, with extra columns in wide mode (Reason, and Last action between Status and Attack)
- Click a column header to **sort** the enemy list (the order stays put until you click again)
- **Last action** colours: recent / mid / older
- **Termed war maxes:** enemy team max, our team max, and a per-player max for your side. Scores turn pink near the cap and bold red at the cap
- **Faction calls:** STAY IN HOSP and PUSH banners (from your Torn message subjects, and optionally new chat lines on the war page)
- **Push timer alerts** and a **war horn** when a timed PUSH hits zero
- **Your own hospital alerts** before you get out
- Alerts and sounds only play while the Torn tab is in front (Torn's rules do not allow alerts from a page you are not viewing). Missed alerts are not replayed when you come back; a current faction call can still show on the banner, silently
- Optional **FF Scouter** fair fight badge and estimated stats for each enemy (off by default, see below)
- Stops all Torn API calls if Torn reports your key as wrong, disabled or paused, as Torn's API rules require
- **Custom sounds** and volume, plus a built-in FAQ in settings
- **Clear sheet**, **Reset max points**, and **Delete stored data & reset**

## Install

1. Install the [Tampermonkey](https://www.tampermonkey.net/) extension for your browser. In Chrome you may also need to turn on **Developer mode** at `chrome://extensions`.
2. Open this install link (Tampermonkey will prompt you to install):

   https://raw.githubusercontent.com/everwood1220/torn-war-helper/main/torn-war-helper.user.js

3. Open your faction's ranked war page on torn.com (`factions.php` with the war view). Click the round **⚙** button in the bottom-left corner.

Until the GitHub repo is up, you can also install by opening the `torn-war-helper.user.js` file (drag it onto the browser, or Tampermonkey Dashboard > Utilities > Import from file).

## API key

Use a **Limited Access** key from Torn (Settings > API Keys). Paste it in ⚙ and click **Save**.

Your key is stored only in your browser, in Tampermonkey storage. It is sent only to `api.torn.com`. If you turn on FF Scouter, it is also sent to `ffscouter.com` (see below). The script does not send it anywhere else.

Only faction calls need Limited Access, because they read your message subjects. Everything else (war, enemy members, your status, player refresh) works with a Public key.

### How the key is used (Torn API terms)

| | |
|---|---|
| **Data Storage** | Only locally (your browser's Tampermonkey storage) |
| **Data Sharing** | Nobody. If you turn on FF Scouter, your FF Scouter key (your Torn key unless you enter another) and the enemy player IDs are sent to ffscouter.com ([FF Scouter Data Policy](https://ffscouter.com/), [Privacy Policy](https://ffscouter.com/privacy)) |
| **Purpose of Use** | Faction war helper (enemy list, hospital timers, faction calls, alerts) |
| **Key Storage & Sharing** | Stored locally in the userscript storage, not shared |
| **Key Access Level** | Limited Access (needed for faction calls from message subjects; everything else works with Public) |

Torn endpoints used (API v2): `user/faction`, `faction/wars`, `faction/{id}/members`, `user/basic`, `user/{id}/basic` (all Public) and `user/messages` (Limited).

### If your key stops working

If Torn says the key is wrong (error 2), its owner is in federal jail (10), it was disabled for inactivity (13), or it is paused (18), the script stops **all** Torn calls right away. You get a red message in settings and a red ring on the ⚙ button, and the calls stay stopped after a reload. Fix the key on Torn or paste a new one, then press **Save** to resume. Error 16 (access level too low) stops only the check that needs it. Error 5 (too many requests) pauses Torn calls for 60 seconds.

## Target sheet (optional)

If you want stats and group tags, paste a Google Sheets link in ⚙ and Save. Share the sheet as **Anyone with the link can view** (or File > Share > Publish to web).

Write players as `Name [ID]` with their stats in the next cell. A header like `Group 1` puts everyone below it in G1. The sheet is re-read about every 10 minutes.

Leave the sheet field blank if you only want timers, calls, and alerts.

## FF Scouter (optional)

[FF Scouter](https://ffscouter.com/) is a separate community site, not part of Torn or this script. It estimates battle stats and fair fight from attack data. If you turn it on, each enemy gets a fair fight (FF) badge in the Stats column:

- **Green** (under 2): much weaker than you
- **Yellow** (2 to 4): a good fight
- **Red** (4 and up): likely much stronger than you
- **Grey ?**: FF Scouter has no estimate yet. A faded badge means the estimate is more than 14 days old.

Your target sheet's stats always come first. If the sheet has no stats for a player, FF Scouter's estimate shows instead, with a `~` in front (for example `~3.1B`), and sorting by Stats uses it. Hover a badge to see the estimated stats, where the estimate came from, how old it is, the build (premium only), spy totals and the battle stat score. In the 50/50 layout (neither layout box ticked), the column shows only the FF badge so names still fit.

**Setup (one time):**

1. Register your Torn API key on [ffscouter.com](https://ffscouter.com/). Or, in ⚙ > FF Scouter, tick **I have read FF Scouter's Data Policy** and press **Register key**. You do **not** need the FF Scouter userscript.
2. Tick **Show FF Scouter fair fight + estimated stats**.
3. Press **Check key**. It should say **Key registered** and whether you have premium. New sign-ups can take about 5 minutes before estimates show.

The **FF Scouter key** box is optional. Leave it blank to use your Torn key, or enter the key you registered on ffscouter.com if it's a different one.

**What is sent, and how often:** only when FF Scouter is on, your FF Scouter key and the enemy player IDs go to `ffscouter.com/api/v1` (`check-key`, `get-stats`, and `register` if you press the button). Players are requested in batches of up to 100 and each one is cached for 1 hour, as FF Scouter recommends, so a war usually needs one or two calls an hour. The key is checked once a day. Requests only run while the war page is in front. A rate limit or network error waits and retries later. A key problem (not registered, bad format, banned) stops FF Scouter until you change its settings or press Check key.

Before you turn it on, read FF Scouter's [Data Policy / Terms](https://ffscouter.com/) (on their sign-up page) and [Privacy Policy](https://ffscouter.com/privacy). Their data policy covers what they store from your key.

## Settings (the ⚙ button)

- **Setup:** API key and sheet link (Save appears when those have changed)
- **Display:** wide layout, narrow-my-team, hospital-exit beep
- **FF Scouter:** on/off, optional separate key, Data Policy box, Check key / Register key / Clear FF cache, and status
- **Faction calls:** STAY IN HOSP / PUSH sounds, banner, optional chat watching, and how often to check message subjects (3–60 seconds, default 5)
- **Push timer alerts:** first and final alerts before push time, plus the war horn at zero
- **My hospital alerts:** first and final alerts before you leave hospital
- **Custom sounds:** add an audio file up to 1 MB
- **Termed war max:** enemy team, our team, and our player max (leave blank to turn off)
- **FAQ** and **Tools** (clear sheet, reset maxes, or wipe everything this script stored)

Click the page once after it loads so the browser allows sound. Use ▶ Test to preview a sound.

## Faction calls

The script reads the **subjects** of your newest Torn messages (it does not open them or mark them read) and, if you leave the option on, new chat lines on the war page:

- "Stay in hosp" / "Stay in hospital" / "Turtle" → red **STAY IN HOSP** banner
- "Push at 18:30" (TCT) → amber countdown, then green **PUSH NOW** and the war horn at that time
- A chat line like **PUSH** means push now

The banner can be dragged; its position is remembered. Click the small **×** in its corner to close it; a new call brings it back. It clears on its own after a few minutes, or when the other call comes in.

## Updates

Once the script is on GitHub, Tampermonkey will check that raw link for updates. You can also re-open the install link or import a new file; your key and settings stay saved.

## Torn rules

This script is **read-only**. It displays information and plays alerts on the war page. It never auto-clicks, auto-attacks, or performs any game action for you. Attack and profile links only open in a new tab when **you** click them.

Torn API calls are paced (about 700 ms apart), stay far under Torn's 100 calls per minute, and pause when the tab is hidden. Member data is refreshed about every 30 seconds; message subjects are checked on the interval you set.

Alerts, sounds, and chat-call reading run only while the Torn tab is in front, in line with Torn's rule against using an unfocused page to generate alerts or draw attention. The script does not change the tab title, send desktop notifications, or steal focus. Alerts that come due while you are on another tab are marked as already fired and are not replayed when you return; a current faction call may still appear on the banner, silently.

## License and credit

MIT License. Made by **Everwood [62912]** of **Aqua**.

## Issues

Report problems or ideas at: https://github.com/everwood1220/torn-war-helper/issues
