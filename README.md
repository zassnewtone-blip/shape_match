# Shape Match

The learning cards and games cover 12 shapes: triangle, square, rectangle, circle, oval, pentagon, hexagon, octagon, diamond, star, trapezoid, and parallelogram. Each practice turn selects a target plus two randomized choices.

## Run locally

Install Node.js, then run one of these commands from the project folder in PowerShell:

```powershell
npm.cmd start
```

or run the server directly:

```powershell
node .\server.mjs
```

Then open the URL printed by the server (normally <http://localhost:4173>). If that port is already occupied, the server tries the next available port and prints its URL. `npm.cmd` avoids PowerShell's script execution policy block on `npm.ps1`; no policy change is needed. The local server is needed for service worker and install support; opening `index.html` directly as a file will not enable offline caching.

After the first successful visit, the app shell is cached for offline use. Learner progress is stored in the browser's IndexedDB, with existing `shape-match-v1` local storage data migrated on first launch. Users can create local accounts from the login page; account credentials and progress stay in that browser and do not sync to other devices. The status badge reports connectivity and reminds learners that progress is saved on the current device.

## Hosting online

The static files are staged in `public-site`. To publish them, open [Netlify Drop](https://app.netlify.com/drop) and drag the `public-site` folder from this project onto the page. Netlify will provide a public URL after the deploy completes. For a Git-connected Netlify project, `netlify.toml` sets `public-site` as the publish folder. The service worker requires HTTPS (or localhost). No external font or image downloads are required.

## Current data boundary

Publishing makes the site reachable online; learner accounts and progress still remain local to each browser and device. Multi-device accounts, classroom records, and teacher/student synchronization require a hosted authenticated API and database. The current role checks are part of the static page and are not suitable for protecting real student records.
