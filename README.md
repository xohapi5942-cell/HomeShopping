# Home Shopping – Android APK project

The app is your existing Claude Artifact, **unchanged**, wrapped in a thin Android shell (WebView).
`app/src/main/assets/index.html` is your Artifact file itself, so the design and every feature stay exactly the same.

## Technologies found in your Artifact
- One self-contained HTML file: HTML5 + CSS3 (CSS variables, grid/flex) + **vanilla JavaScript** (no React, no framework, no build step)
- **SheetJS (xlsx 0.18.5)** – Excel/CSV import of items (loaded from cdnjs; the build bundles it inside the APK)
- Browser APIs: MediaRecorder + getUserMedia (voice recording), Geolocation (current location), FileReader + Canvas (pictures), file inputs (Excel / images), `<input type="date">`, `<datalist>`, `<audio>`
- App data is kept **in memory** (same as in the Artifact): it resets when the app is fully closed

## Android side
- Native Java `MainActivity` with WebView, served from `https://appassets.androidplatform.net/` (secure origin, so mic and location work)
- Permissions handled: microphone, location, file/photo picker
- Back button: goes to the "Login page" (4 buttons), exits from there
- minSdk 26 (Android 8+), targetSdk 34, package `com.homeshopping.app`

## Easiest build (no powerful computer, no Android Studio) – GitHub Actions
1. Create a free account at github.com and make a **new repository** (any name, Public or Private).
2. Click **Add file → Upload files**, drag in ALL files and folders from this project, and commit.
   - If the `.github` folder did not upload (hidden folder): click **Add file → Create new file**, type the name
     `.github/workflows/build-apk.yml`, paste the contents of `build-apk.yml` from this project, and commit.
3. Open the **Actions** tab → **Build APK** → **Run workflow** (it also starts by itself after the upload).
4. Wait about 4–6 minutes until the run shows a green tick.
5. Open the finished run → scroll to **Artifacts** → download **HomeShopping-APK** (a zip containing `app-debug.apk`).
6. Copy the APK to your phone, tap it, and allow **Install unknown apps** when Android asks.

## Alternative: Android Studio
Open this folder in Android Studio and press Run / Build → Build APK(s).
For offline Excel import, also download
https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js
into `app/src/main/assets/` and change the script tag in `index.html` to `src="xlsx.full.min.js"`.

## Notes
- The APK is a debug-signed build: fine for installing and sharing. A Play Store release needs your own signing key.
- To update the app later: replace `app/src/main/assets/index.html` with the new Artifact HTML and run the workflow again.
- The app always uses the light theme.
