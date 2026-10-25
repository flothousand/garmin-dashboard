# Garmin to Google Sheets (n8n template)

Pulls your last 365 days of Garmin sleep, HRV, daily health data and activities into a Google Sheet, then lets Claude build a dashboard from it.
Free tools only. **Personal use only: use your own Garmin key and your own data.**

## What is in this repo
- `Garmin_to_Google_Sheets_n8n_template.json`: the n8n workflow
- `GarminData_sheet_template.xlsx`: the Google Sheet template (headers only)

## Setup
1. Get n8n: https://n8n.io (self-hosting is free)
2. Create your Garmin Personal API key (log in first, the key is shown only once): https://connect.garmin.com/app/settings/personalApiToken
3. Import the workflow into n8n: open a new workflow, then menu > Import from file, or Import from URL with
   `https://github.com/flothousand/garmin-dashboard/raw/refs/heads/main/Garmin_to_Google_Sheets_n8n_template.json`
4. In **Get Garmin Token**, create a Header Auth credential: Name `Authorization`, Value `ApiKey YOUR_KEY` (one space after ApiKey)
5. Upload `GarminData_sheet_template.xlsx` to Google Drive and open it with Google Sheets. Keep the tab names (Daily, Activities) and the header row.
6. In **Write Daily** and **Write Activities**, connect your Google account, select your sheet and click the refresh icon so n8n reads the headers
7. Press **Execute workflow**. The first run takes a few minutes because it asks Garmin for data slowly on purpose.

## Build the dashboard with Claude
Connect Google Drive in Claude, then paste this prompt:

```
Build an interactive dashboard from my Google Sheet "GarminData" (tabs Daily and Activities). Dark, futuristic, cyan and pink accents, animated.

Header: a rotating 3D sphere with a glowing core and hundreds of spikes (one per day), plus labelled spikes for my best moments (best sleep, fastest pace, best bike power). Sticky bar: "Every insight is built on N connected data points".

Health: readiness gauge, HRV vs baseline, sleep stages and score, resting HR, Body Battery, vital-sign tiles, correlation network.

Performance: weekly distance for bike, run, swim, training calendar, load, running pace, economy, race potential, bike power, FTP estimate, efficiency, zones.

Coach: the 5 biggest areas to improve, each with a small chart.

Calculate everything from my data, add hover tooltips.
```

## Good to know
- If Garmin answers HTTP 429 (too many requests), run the workflow again. Rows are updated, never duplicated.
- Daily rows match on `Date`, activities on `ActivityID`.
- The period is set by `TOTAL_DAYS` in the **Build Requests** node (365 by default).
- Never share your API key. It stays in your n8n credentials.
- Not affiliated with Garmin, n8n, Google or Anthropic.
