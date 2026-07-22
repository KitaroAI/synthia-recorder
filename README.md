# synthia-recorder

Static microphone-recorder bridge page for the SOJC board meeting console
(Google Apps Script web app). The console runs inside Google's sandbox iframe,
whose permissions policy blocks `getUserMedia` in every browser. This page is
opened as a top-level popup at a real origin, so the browser can prompt for
and grant the microphone.

Flow: the console opens `index.html#<one-time-nonce>` in a popup. The page
records (30-second cap, or Stop), posts the audio back to `window.opener` via
`postMessage` tagged with the nonce, and closes itself. The nonce rides the
URL fragment, which never reaches any server. No audio or data is stored or
sent anywhere except back to the opening console window.

Served via GitHub Pages. No build step, no dependencies.
