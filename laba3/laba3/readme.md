# Tailwind Version

This folder contains a Tailwind CSS (CDN) implementation of the mobile onboarding + login/register screens.

Files:
- `index.html` — the page styled with Tailwind Play CDN (`https://cdn.tailwindcss.com`).

How to view:
1. Open `index.html` in your browser directly (double-click) or
2. Serve with a simple local server (recommended):

PowerShell (from the folder containing `index.html`):

```powershell
# change to the project folder (adjust path if needed)
Set-Location 'e:\Work Space\laba3'
# start a simple HTTP server (requires Python installed)
python -m http.server 8000
# open the page in your default browser (run in a new shell or after starting the server)
Start-Process 'http://localhost:8000'
```

Notes:
- This uses the Tailwind Play CDN for quick prototyping; no build step required.
- The page uses simple SVG placeholders instead of external illustrations.
