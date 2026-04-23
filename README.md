# MicScaler

MicScaler is a high-precision, single-page web application designed to demonstrate the strict mathematical scaling of live microphone data streams across up to 100 concurrent tracks.

Unlike standard audio mixing concepts (where Gain is pre-processing signal strength and Volume is post-processing balancing), **MicScaler treats audio as pure data**. It isolates the process of shrinking and expanding data ranges using multiplicative mathematics ($x$).

## 🚀 Quick Start
1. Clone this repository or download `index.html`.
2. Open `index.html` in any modern web browser.
3. Select your desired number of tracks (1 to 100).
4. *(Diagnostic Mode)*: Click **Enable Diagnostic Test** to generate a perfect Sine wave across all tracks, allowing you to visually verify scaling and phase logic.
5. *(Mobile Users)*: Select your audio routing via the **Earpiece Mode** toggle.
6. Click **Start Microphone** to begin live data processing.

## 🧮 The Math Logic
This app strictly adheres to the following definitions for processing:
*   **Scale:** Data control / Shrinking/Expanding ranges / Multiplicative ($x$)
*   **Net Polarity:** The result of three cascading inversion layers:
    `NetPolarity = GlobalMaster * TrackSpecific * AlternateEverySecond`

## ✨ Features
*   **Massive Multi-Tracking:** Manage up to **100 concurrent tracks** dynamically.
*   **Diagnostic Mode:** A built-in test generator that replaces microphone noise with a perfect Sine wave, allowing for visual verification of math accuracy across all 100 tracks.
*   **Three-Tier Polarity Inversion:** 
    *   **Master Invert:** Flips the phase of all tracks.
    *   **Alternate Invert:** Automatically flips the phase of every 2nd track (Track 2, 4, 6...).
    *   **Track Invert:** Granularly flip the phase of an individual track.
*   **Algorithmic Sequence Continuation:** Tracks automatically populate their default inputs based on a fractional curve, followed by an algorithmic linear step of `+1.0%` for higher tracks.
*   **Mobile Routing Bypass:** Force mobile devices to route audio to the main loudspeaker (Spotify mode) by toggling Earpiece mode.
*   **Real-Time Data Visualization:** Individual HTML5 Canvas oscilloscopes that dynamically change color to **Red** when the net mathematical polarity of the track is inverted.

## ⚠️ Requirements
*   A working microphone.
*   Must be run on `localhost` or an `https` connection, as browsers block microphone access on unsecure `http` connections.
