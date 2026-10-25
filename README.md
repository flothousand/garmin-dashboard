# Garmin to Google Sheets (n8n template)

Pulls your last 365 days of Garmin sleep, HRV, daily health data and
activities into a Google Sheet, then lets Claude build a dashboard from it.
Free tools only. Personal use: use your own Garmin key and data.

## Setup
1. Get n8n: https://n8n.io
2. Create your Garmin key: https://connect.garmin.com/app/settings/personalApiToken
3. Import the workflow JSON into n8n (setup notes are inside)
4. Open the sheet template in Google Sheets and select it in the two Sheets nodes
5. Press run, then ask Claude to build a dashboard from the sheet
