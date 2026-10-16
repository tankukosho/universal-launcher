# Gaming Launcher Prototype

A responsive, text-first design project with real remote game artwork URLs in the app interface. The app name is intentionally undecided.

## Run it

### Quickest: open the page
Open `index.html` in a modern browser. Most features work locally. Some browsers restrict `fetch()` requests when a page is opened using `file://`, so Steam catalogue search and the PWA service worker may require a local web server.

### Recommended: run a local server
If Python is installed on your PC, open a terminal in this folder and run:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

On Android, put the folder on a static web host (for example GitHub Pages) or use a local development server app. Then open the HTTPS page in Chrome and use **Add to Home screen**.

## Included
- Responsive purple-neon dashboard and sidebar navigation
- Home screen with wide featured banner
- Balanced grid of vertical library covers
- Search, platform filters, sorting, favourites
- Game detail panel with launch choices
- Steam public store search attempt for automatic metadata/artwork
- Manual game entry and artwork overrides
- Local browser persistence using `localStorage`
- JSON and CSV import, JSON export
- PWA manifest and service worker

## Important prototype limits
- The sample covers and banners use remote Steam CDN image URLs. Internet access is required for them.
- Steam catalogue search uses public Steam Store endpoints. These can change or be blocked by browser CORS, network settings, or regional availability. The app falls back to manual entry.
- A browser cannot scan installed Windows games or launch arbitrary Windows executables. PC detection and native launching need a trusted desktop companion (for example, a later Tauri/Electron build with explicit permissions).
- Android browser apps cannot enumerate or launch arbitrary installed Android packages. Android-native integration would be a separate later phase.
- Browser storage is per browser/device. Export a JSON backup to move your collection.
- Manual artwork overrides are stored as data URLs in local browser storage; very large images may exceed storage limits. Use smaller images for this prototype.
- Sample Android entries are examples and are not proof that the corresponding app is installed.

## Import file formats

JSON array example:

```json
[
  {
    "name": "Example Game",
    "platform": "PC",
    "source": "Steam",
    "url": "https://store.steampowered.com/app/123456/",
    "description": "Optional description",
    "cover": "https://example.com/cover.jpg",
    "banner": "https://example.com/banner.jpg"
  }
]
```

CSV header example:

```csv
name,platform,source,url,description
Example Game,PC,Steam,https://example.com,An example description
```

## Next build phase
1. Verify artwork endpoints and improve metadata fetching.
2. Add a native PC companion for installed-game discovery and safe launch handoff.
3. Add launcher-specific adapters (starting with Steam) where technically and legally supported.
4. Package for Android using a trusted PWA/TWA or native wrapper.
5. Add cloud sync only if desired.
