# AI 101 — CesiumJS Flight Lab

This is an original teaching starter: a steerable moving point, not a realistic aircraft simulator.

## Run
Upload all files in this folder to the root of a public GitHub repository. In Settings → Pages choose Deploy from a branch, main, /(root). Open the site URL after deployment. Alternatively serve this folder with your editor's local web server. If Python is already installed: `python -m http.server 8000`, then open http://localhost:8000.

Internet and WebGL are required. CesiumJS 1.145 and its matching CSS load from Cesium's CDN. No build step or Node installation is needed. Real satellite imagery needs a free Cesium ion access token, which goes in `config.js` (`window.APP_CONFIG.ionToken`). Without a token the lab still runs on the plain grid globe. Keep Cesium's on-screen credits visible.

## Controls
Fly starts motion; Pause stops it. **Slow Tour** (added) sets speed to 30 m/s and height to 300 m and starts moving; the status line then reads "Slow Tour". Editing speed or height by hand, or pressing Reset, returns to normal "Flying" wording. Left/Right change heading by 10 degrees. Speed is 0–250 meters/second; height is 50–5000 meters above the model ellipsoid. Height changes instantly: this starter does not simulate climbing. Reset restores the paused initial state. Switching to another browser tab pauses the app. On returning, press Fly again. The camera follows while flying.

## Test
Open tests.html on the same site. Also perform the six manual checks on Canvas page 05. Optional developer command: `node -e "require('./flight-core.js');require('./tests.js')"`.

## Model and geography
Uses spherical destination-point math with Earth radius 6,371,000 m, displayed on Cesium's ellipsoid globe. This approximation is for learning. Heading remains constant between clicks. Frame dt is capped at 0.1 s to prevent large jumps after stalls, so low frame rates can slow simulated time. Imagery is a visual backdrop only. Terrain stays flat (ellipsoid), so height is not height above real ground. There is no lift, drag, bank, pitch, collision, flight data, or navigation accuracy. The marker is a point, not an aircraft model. Grid lines provide visual reference, not roads. The imagery comes from Cesium ion and keeps Cesium's credits visible.
The approximate origin (-75.93, 40.33) is a Reading-area classroom reference, not a verified Alvernia campus location. Validate real location claims separately.

## Student additions — complete before submission
**CesiumJS version:** 1.145 (loaded from Cesium's CDN; see index.html)

**Run steps (exact):**
1. Unzip Flight_Lab.zip. Make sure `config.js` contains a valid Cesium ion token.
2. In the folder, run `python -m http.server 8000` (or use your editor's local server).
3. Open http://localhost:8000 (internet and WebGL required).
4. Expected on load: a satellite-imagery globe with the grid and gold dot, and the status line starts with "Satellite imagery: Cesium ion." Then press **Slow Tour**. Expected: speed box shows 30, height box shows 300, status reads "Slow Tour — simulated movement at 30 m/s, 300 m", and the readout latitude starts increasing.
5. Open http://localhost:8000/tests.html. Expected: 10 lines, all `PASS` (7 starter checks + 3 Slow Tour checks).

**Audience and purpose:** TODO — write your pitch: "I want to help ___ do ___ using ___ data." Add one sentence on what you will verify before sharing.

**Feature changed:** Added a **Slow Tour** button. Rules live in `flight-core.js` (`Flight.slowTour`, constants in `Flight.SLOW_TOUR`) so they can be unit-tested; `app.js` only wires the button and updates the status text. Also added a `tour` flag to state and clearer status wording. Three new checks (8-10) were added to `tests.js`; the original seven are unchanged.

**AI assistance accepted/rejected:** TODO — summarize in your own words (see your three conversation excerpts).

**Tests and evidence:** See Test_Log.csv. Automated checks were run in Node; re-run `tests.html` in your browser and record the result. Manual checks and break-and-repair: TODO.

**Partner reproduction feedback:** TODO — partner name, what confused them, what you changed.

**Geographic/API sources:** Imagery from Cesium ion (World Imagery) via an access token in `config.js`; TODO — also the origin (-75.93, 40.33) is a Reading-area teaching reference, not a verified campus location. If you make any real-location claim, cite where you checked it and the date.

**Known limitations:** The token in `config.js` is visible to anyone who views the site; if imagery stops loading, the token may have expired or been restricted. Slow Tour changes only speed and height; it is not a route and has no real navigation. At 30 m/s with the camera 2,500 m back, movement looks subtle, which is intentional but may be hard to see. Height still changes instantly (no climb simulation). Frame dt is capped at 0.1 s, so low frame rates slow simulated time. TODO — add one limitation you found yourself.

## References
https://cesium.com/learn/cesiumjs-learn/
https://cesium.com/learn/cesiumjs/ref-doc/Viewer.html
https://cesium.com/learn/cesiumjs/ref-doc/Cartesian3.html
https://cesium.com/learn/cesiumjs/ref-doc/GridImageryProvider.html

CesiumJS is an external dependency with its own license and notices. It is not bundled in this resource ZIP.
