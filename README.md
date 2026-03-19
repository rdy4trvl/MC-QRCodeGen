# Marin Century 2026 — QR + UTM Generator v2

## What this does

A web app where anyone on the marketing team can:
1. Pick a placement type, destination, and enter a location
2. Instantly get a UTM-tagged URL and branded QR code (with MC logo)
3. Save the entry to a shared Google Sheet for tracking

## Features

- **Placement types**: Postcard, yard sign, flyer, banner, poster, event handout, sticker, plus custom "other"
- **Destinations**: RedPodium registration, MarinCentury.com, ride director email, volunteer email
- **Email destinations**: Generate QR code only (opens blank email — no UTMs)
- **Web destinations**: Full UTM tracking (utm_source, utm_medium, utm_campaign, utm_content)
- **Logo overlay**: Marin Century logo embedded in center of every QR code
- **Slug enforcement**: Location field only allows lowercase + underscores for clean UTMs
- **Sheet logging**: Every generated QR is saved to a shared Google Sheet

## Files

- `index.html` — The web app (host on GitHub Pages)
- `apps-script.js` — Google Apps Script for Sheet logging

## Setup (15 minutes)

### Step 1: Deploy the Apps Script

1. Go to [script.google.com](https://script.google.com)
2. Click **New project**, name it `MC QR Tracking Logger`
3. Delete default code, paste everything from `apps-script.js`
4. Click **Deploy > New deployment**
5. Type: **Web app**, Execute as: **Me**, Access: **Anyone**
6. Click **Deploy**, authorize when prompted
7. **Copy the Web App URL**

### Step 2: Configure the web app

1. Open `index.html` in a text editor
2. Find: `var APPS_SCRIPT_URL = 'YOUR_APPS_SCRIPT_URL_HERE';`
3. Replace `YOUR_APPS_SCRIPT_URL_HERE` with URL from Step 1
4. Save

### Step 3: Host on GitHub Pages

Add to your existing marin-century repo:
1. Create a `qr-generator` folder in the repo
2. Upload `index.html` into it
3. Commit and push
4. Access at: `rdy4trvl.github.io/marin-century/qr-generator/`

## UTM naming conventions

| Parameter     | Value                    | Purpose                                  |
|---------------|--------------------------|------------------------------------------|
| utm_source    | postcard, yardsign, etc. | Material type                            |
| utm_medium    | print (always)           | Groups all offline traffic in GA4        |
| utm_campaign  | 2026mc (always)          | Groups all MC marketing                  |
| utm_content   | user-entered slug        | Identifies specific placement location   |

## Viewing results

- **Google Sheet**: `MC QR Tracking Log` in Google Drive
- **GA4**: Acquisition > Traffic Acquisition > filter utm_medium = print
- **RedPodium**: Cross-reference discount codes with GA4 sessions per utm_content

## Updating for 2027

1. Update `utm_campaign` from `2026mc` to `2027mc` in the script section
2. Update the RedPodium URL in the destination dropdown
3. Update page title/header year
4. Start fresh tracking sheet (or add new tab)
