Flight Lab

A small, interactive 3D globe where you steer a simulated moving marker. Built with CesiumJS as a learning project for AI 101 at Alvernia University.

Live demo: [https://<your-username>.github.io/Flight](https://evanbeitler.github.io/FlightSimLab/index.html)

This is a teaching demo, not a flight simulator and not for navigation. The marker is a point that moves in a straight line. There is no lift, drag, banking, pitch, collision or real aircraft data.

What you can do
Control	What it does
Fly	Start moving
Slow Tour	Fly slowly (30 m/s) at a low height (300 m) so the scene is easy to follow
Pause	Stop moving
Left / Right 10°	Turn the heading by 10 degrees
Speed	0–250 meters per second
Height	50–5,000 meters above the model ellipsoid
Reset	Return to the paused starting state

Switching to another browser tab pauses the app; press Fly again when you return. The camera follows the marker while it is flying. The readout under the controls shows heading, longitude, latitude, height and speed as numbers.

Run it yourself

You need an internet connection and a browser with WebGL.

Download or clone this repository.
In the project folder, run: python -m http.server 8000 (or use your editor's local server).
Open http://localhost:8000.

To publish with GitHub Pages: put the files in the root of a public repository, then go to Settings → Pages, choose Deploy from a branch, main, /(root).

Cesium ion token (for satellite imagery)

The satellite imagery needs a free Cesium ion access token. Create one at cesium.com/ion and put it in config.js:

js
window.APP_CONFIG = { ionToken: "YOUR_TOKEN_HERE" };

Without a token, the app still runs on a plain grid globe, and the status line says so. Anything you publish is public, so use a token made just for this project, give it read-only access, and restrict it to your site's URL if you can.

Tests

Open tests.html on the same site (or at http://localhost:8000/tests.html). It runs 10 checks on the movement math, such as north increasing latitude and one second matching ten 0.1-second steps. These test the math only, not the globe or buttons.

Optional command-line run: node -e "require('./flight-core.js');require('./tests.js')"

How it's organized
File	Purpose
index.html	The main page; loads Cesium, then the scripts below
flight-core.js	Movement math (no screen code, so it can be tested)
app.js	Draws the globe and connects the controls
config.js	Cesium ion token
tests.html, tests.js	Automated checks
style.css	Layout and colors
Accuracy and limitations
Movement uses simplified spherical math with an Earth radius of 6,371,000 m, shown on Cesium's ellipsoid globe. It is an approximation for learning.
Heading stays constant between clicks. Frame time is capped at 0.1 s to avoid big jumps after a stall, so on a slow device simulated time can run slower than real time.
Satellite imagery is a backdrop only. Terrain is flat, so height is not height above real ground.
The grid is a visual scale reference, not roads.
The starting point (-75.93, 40.33) is an approximate Reading-area teaching reference, not a verified campus location. Check any real-world location claim separately.
The ion token in config.js is visible to anyone who views the site. If imagery stops loading, the token may have expired or been restricted.
Credits and licenses
Built with CesiumJS 1.145, loaded from Cesium's CDN. CesiumJS is an external dependency with its own license and notices; it is not bundled here.
Satellite imagery is provided through Cesium ion. Keep Cesium's on-screen credits visible.
Starter code for this lab was provided for AI 101; the Slow Tour feature, imagery setup and documentation were added by the project author with AI assistance.
References
https://cesium.com/learn/cesiumjs-learn/
https://cesium.com/learn/cesiumjs/ref-doc/Viewer.html
https://cesium.com/learn/cesiumjs/ref-doc/Cartesian3.html
https://cesium.com/learn/cesiumjs/ref-doc/GridImageryProvider.html
