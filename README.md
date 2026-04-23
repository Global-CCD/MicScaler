# MicScaler

MicScaler is a lightweight, single-page web application designed to demonstrate the strict mathematical scaling of live microphone data streams across up to 50 concurrent tracks.

Unlike standard audio mixing concepts (where Gain is pre-processing signal strength and Volume is post-processing balancing), **MicScaler treats audio as pure data**. It isolates the process of shrinking and expanding data ranges using high-precision multiplicative mathematics ($x$).

## 🚀 Quick Start
1. Clone this repository or download `index.html`.
2. Open `index.html` in any modern web browser.
3. Select your desired number of tracks (1 to 50).
4. *(Mobile Users)*: Select your audio routing via the **Mobile Earpiece Mode** toggle.
5. Click **Start Microphone** and allow browser permissions.
6. Alter the text input boxes to adjust the scaling percentage per track, and optionally invert the polarity via individual tracks or the Master toggle.

## 📱 Mobile Audio Routing Explained (Earpiece vs Spotify Speaker)
Mobile browsers (Safari/Chrome on iOS/Android) aggressively hijack audio routing when the microphone is turned on. By default, they assume you are making a phone call and route all output to the **Earpiece** to prevent echo. 
*   **To output to the main Loudspeaker (like Spotify):** Uncheck "Mobile Earpiece Mode" (This disables OS-level echo cancellation and tricks the phone into media mode).
*   **To output to the Earpiece (like a phone call):** Check "Mobile Earpiece Mode".

## 🧮 The Math Logic
This app strictly adheres to the following definitions for processing:
*   **Gain:** Pre-processing / Signal saturation / Additive/Subtractive (dB) - *Not used here*
*   **Volume:** Post-processing / Mixing / Additive/Subtractive (dB) - *Not used here*
*   **Scale (This App):** Data control / Shrinking/Expanding ranges / Multiplicative ($x$)
*   **Offset:** Data control / Shifting the baseline / Constant Addition ($+$) - *See Roadmap*

### How it works under the hood
The app grabs the raw floating-point time-domain data of your microphone (`-1.0` to `1.0`). 
For every track, the app runs the following equation:
`ScaledValue = RawInput * (TrackPercentage / 100) * TrackPolarity * MasterPolarity`

*Because phase flipping is pure multiplication, applying an inversion to the Master Toggle (`-1`) AND the Individual Track (`-1`) cancels out, resulting in a positive state (`1`).*

## ✨ Features
*   **Zero-Dependency Architecture:** A pure Vanilla HTML/CSS/JavaScript single-page app.
*   **Massive Dynamic Multi-Tracking:** Spawn between 1 and **50 concurrent tracks** dynamically on the fly.
*   **Cascading Polarity Inversion:** Apply phase flipping on an individual track level, or flip the entire global signal using the **Master Invert (+/-)** toggle. Canvas waveforms turn red when their net math output is inverted.
*   **Precision Text-Input Control:** Each track features a direct numerical text input box allowing you to define the exact multiplication scale, supporting 2 decimal places (e.g., `0.01%`).
*   **Programmatic Default Sequencing:** Auto-populates an ascending fractional scale sequence for newly generated tracks (`0.01, 0.02, 0.03... 0.1... 1.0... up to 5.0%`).
*   **Algorithmic Sequence Continuation:** If tracks are spawned beyond the base preset of Track 23 (5.0%), the app automatically calculates a continuous `+1.0%` stepping sequence for the remainder of the tracks (Track 24 = 6.0%, Track 25 = 7.0%... up to Track 50 = 32.0%).
*   **Hardware Audio Routing Bypass:** Features a WebRTC constraint override to force mobile devices to route audio to the main loudspeaker (Spotify mode) instead of defaulting to the VoIP Earpiece.
*   **Live Microphone Capture:** Utilizes the Web Audio API to capture raw, uncompressed floating-point audio data.
*   **Real-Time Data Visualization:** Individual HTML5 Canvas oscilloscopes for every track, rendering the mathematically scaled output at 60fps.

## ⚠️ Requirements
*   A working microphone.
*   Must be run on `localhost` or an `https` connection, as browsers block microphone access on unsecure `http` connections.
