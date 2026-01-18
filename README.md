
# Airport Arrivals & Departures Display (BUN)

This package contains a single-page web app you can deploy to Vercel/Netlify/GitHub Pages or embed in SharePoint. It reads flight data from **CSV**, **JSON**, or **Excel (.xlsx)** via a link and auto-refreshes every 60 seconds.

## Files
- `index.html` — the display app (Arrivals/Departures) with filters and fullscreen.
- `flights.xlsx` — Excel template with a table named `Flights` and sample rows.
- `flights_sample.csv` — same sample data in CSV format for quick testing.

## Data format (columns)
```
type,flight,airline,from,to,scheduled,estimated,status,terminal,gate,belt
```
- `type`: `arrival` or `departure`
- `scheduled` / `estimated`: **ISO 8601 with timezone**, e.g. `2026-01-18T11:45:00-05:00` (Colombia is UTC-05:00)

## Run locally
Open `index.html` in a static server (recommended) and test with the bundled CSV:
```
index.html?airport=BUN&data=flights_sample.csv
```
You can also load the Excel file directly (SheetJS is included):
```
index.html?airport=BUN&data=flights.xlsx
```

## Deploy
You can drag & drop this folder to Netlify or publish with Vercel/GitHub Pages. After deployment, share a link like:
```
https://YOUR_DOMAIN/index.html?airport=BUN&data=URL_TO_YOUR_DATA
```

### Examples
- Using the bundled CSV after deploy:
  ```
  https://YOUR_DOMAIN/index.html?airport=BUN&data=flights_sample.csv
  ```
- Using the bundled Excel after deploy:
  ```
  https://YOUR_DOMAIN/index.html?airport=BUN&data=flights.xlsx
  ```
- Using a published Google Sheet as CSV (replace with your published CSV URL):
  ```
  https://YOUR_DOMAIN/index.html?airport=BUN&data=https://docs.google.com/spreadsheets/d/e/.../pub?output=csv
  ```
- Using SharePoint/OneDrive Excel file (requires an **anonymous view link**). Ensure the link is publicly accessible and append `&download=1` if needed:
  ```
  https://YOUR_DOMAIN/index.html?airport=BUN&data=https://yourtenant.sharepoint.com/.../Flights.xlsx?download=1
  ```

## Optional parameters
- `airport`: display name, e.g. `airport=Aeropuerto%20Gerardo%20Tovar%20L%C3%B3pez%20%E2%80%93%20BUN`
- `refresh`: milliseconds between refreshes (default 60000)
- `logo`: URL to a logo image to show in the header

## Notes
- If your data source requires authentication (SharePoint internal), the wall display needs access (logged-in session or use a published/anonymous endpoint).
- For production, prefer a read-only data source or an API gateway that returns sanitized CSV/JSON.

