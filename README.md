# Aboso Church Membership Portal

## Overview

This repository now separates the static frontend from the Google Apps Script backend.

- `frontend/` contains the GitHub Pages-ready static app:
  - `frontend/index.html`
  - `frontend/camera.html`
- `code.gs` remains the Apps Script backend that stores data in Google Sheets.

## How it works

- The static frontend runs from GitHub Pages.
- The frontend calls the Apps Script backend via a REST-style JSON API at `GAS_API_URL`.
- Camera capture is handled by `frontend/camera.html` and returns image data via `postMessage`.

## Setup

### 1. Deploy the Apps Script backend

1. Open the Apps Script project containing `code.gs`.
2. Deploy a new web app:
   - `Execute as`: `Me`
   - `Who has access`: `Anyone, even anonymous`
3. Copy the deployment URL.
4. Open `frontend/index.html` and replace `GAS_API_URL` with the Apps Script URL.

### 2. Publish the frontend to GitHub Pages

#### Option A: Use a dedicated `gh-pages` branch

1. Build or copy the contents of `frontend/` into the branch root of `gh-pages`.
2. In GitHub repo settings, set Pages source to the `gh-pages` branch.
3. The site will be available at `https://<user>.github.io/<repo>/`.

#### Option B: Use `docs/` folder (recommended if you want main branch deployment)

1. Rename `frontend/` to `docs/`.
2. In GitHub repo settings, set Pages source to the `docs` folder on the main branch.
3. The site will be available at `https://<user>.github.io/<repo>/`.

### 3. Optional: Custom domain

1. In GitHub Pages settings, add your custom domain.
2. Create a DNS record:
   - `CNAME` pointing to `your-username.github.io`
3. If you use an apex domain, add the GitHub Pages A records:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
4. Optionally create a `CNAME` file in the Pages site root with your domain name.

## Notes

- `frontend/index.html` is now a pure static page and no longer depends on `google.script.run`.
- `camera.html` is hosted alongside the frontend and uses a relative URL to open from the portal.
- The backend still uses `code.gs` and Google Sheets for data storage.
- Make sure the Apps Script deployment URL is reachable from the GitHub Pages site.

## Recommended next step

Once the frontend is published, verify that:

- `index.html` loads correctly from GitHub Pages
- `camera.html` opens from the portal and returns photo data
- the backend calls succeed against the configured `GAS_API_URL`
