# Torn War Helper

A Tampermonkey userscript for Torn's ranked war page. It adds extra info and alerts on that page only. It never clicks Attack, never opens pages for you, and never automates any game action.

Made by **Everwood [62912]** of **Aqua**.

## What it does

- Shows **stats** and a **group tag** (G1 / G2 / G3) next to each enemy, from your target Google Sheet
- Live **hospital countdown** on enemies in hospital, then a count-up after they leave
- Optional short **beep** when an enemy you saw in hospital comes out
- **Wide** or **side-by-side** layout, with extra columns in wide mode (Reason, Last action)
- Click a column header to **sort** the enemy list (the order stays put until you click again)
- **Last action** colours: recent / mid / older
- **Termed war maxes:** enemy team max, our team max, and a per-player max for your side. Scores turn pink near the cap and bold red at the cap
- **Faction calls:** STAY IN HOSP and PUSH banners (from your Torn message subjects, and optionally new chat lines on the war page)
- **Push timer alerts** and a **war horn** when a timed PUSH hits zero
- **Your own hospital alerts** before you get out
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

Your key is stored only in your browser, in Tampermonkey storage. It is sent only to `api.torn.com`. The script does not send it anywhere else.

## Target sheet (optional)

If you want stats and group tags, paste a Google Sheets link in ⚙ and Save. Share the sheet as **Anyone with the link can view** (or File > Share > Publish to web).

Write players as `Name [ID]` with their stats in the next cell. A header like `Group 1` puts everyone below it in G1. The sheet is re-read about every 10 minutes.

Leave the sheet field blank if you only want timers, calls, and alerts.

## Settings (the ⚙ button)

- **Setup:** API key and sheet link (Save appears when those have changed)
- **Display:** wide layout, narrow-my-team, hospital-exit beep
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

The banner can be dragged; its position is remembered. It clears on its own after a few minutes, or when the other call comes in.

## Updates

Once the script is on GitHub, Tampermonkey will check that raw link for updates. You can also re-open the install link or import a new file; your key and settings stay saved.

## Torn rules

This script is **read-only**. It displays information and plays alerts on the war page. It never auto-clicks, auto-attacks, or performs any game action for you. Attack and profile links only open in a new tab when **you** click them.

API calls are paced (about 700 ms apart) and pause when the tab is hidden. Member data is refreshed about every 30 seconds; message subjects are checked on the interval you set.

## License and credit

MIT License. Made by **Everwood [62912]** of **Aqua**.

## Issues

Report problems or ideas at: https://github.com/everwood1220/torn-war-helper/issues
