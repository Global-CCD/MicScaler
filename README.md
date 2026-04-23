# MicScaler

MicScaler is a high-performance, single-page web application designed to demonstrate the strict mathematical scaling of live microphone data streams across up to **500 concurrent tracks**.

Unlike standard audio mixing concepts (where Gain is pre-processing signal strength and Volume is post-processing balancing), **MicScaler treats audio as pure data**. It isolates the process of shrinking and expanding data ranges using high-precision multiplicative mathematics ($x$).

## Demo Links on Cloudflare
* v1.0.0 - https://v1-2-0-micscaler.pages.dev/
* v1.1.0 - https://v1-2-0-micscaler.pages.dev/
* v1.2.0 - https://v1-2-0-micscaler.pages.dev/
* v1.3.0

## 🚀 Quick Start
1. Clone this repository or download `index.html`.
2. Open `index.html` in any modern web browser.
3. Select your desired number of tracks (1 to 500).
4. *(Optional)* Use the **Step (+%)** tool to instantly apply a sequential mathematical spread across all tracks.
5. *(Mobile Users)*: Select your audio routing via the **Earpiece Mode** toggle.
6. Click **Start Microphone** and allow browser permissions.

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

## ✨ Key Features
*   **Massive Dynamic Multi-Tracking:** Spawn up to **500 concurrent tracks** dynamically. The rendering engine utilizes a native `ResizeObserver` to decouple DOM measurements from the animation loop, allowing over 250,000 math operations per frame at a buttery smooth 60fps.
*   **Hyper-Precision Control:** Direct numerical text inputs allow you to define exact multiplication scales down to **3 decimal places (0.001%)**.
*   **Dynamic Sequential Stepping:** A global "Step" tool allows you to automatically spread your math across the array. Set Track 1 to `0.01`, set a Step of `0.005`, and instantly calculate the cascading sequence for all 500 tracks.
*   **Cascading Polarity Inversion:** Apply phase flipping on an individual track level, or flip the entire global signal using the **Master Invert (+/-)** toggle. Canvas waveforms turn red when their net math output is inverted.
*   **Hardware Audio Routing Bypass:** Features a WebRTC constraint override to force mobile devices to route audio to the main loudspeaker (Spotify mode) instead of defaulting to the VoIP Earpiece.
*   **Real-Time Data Visualization:** Individual HTML5 Canvas oscilloscopes for every track rendering the exact mathematical output.

## 🗺️ Roadmap of Future Features

**Phase 1: Advanced Data Manipulation**
*   **Diagnostic Overlays:** Re-introduce a "Test Mode" that replaces unpredictable mic noise with a mathematically perfect Sine wave, allowing for visual verification of phase cancellation and array stepping.
*   **Offset Integration (+):** Add an "Offset" slider/input to each track to fulfill the final logic tier: shifting the baseline via Constant Addition (e.g., `(RawInput * Scale) + Offset`).
*   **Max/Min Clamping:** Introduce hard mathematical limits to clip the data if it exceeds user-defined thresholds after scaling is applied.

**Phase 2: Data Output & Routing**
*   **WebSockets/OSC Export:** Broadcast the scaled data streams over Localhost to control external software (like TouchDesigner, Resolume, or Max/MSP).
*   **Web MIDI API Integration:** Convert the scaled, multi-track data into continuous MIDI Control Change (CC) messages to drive DAW parameters (e.g., Track 1 controls filter cutoff, Track 2 controls reverb decay).

**Phase 3: Core Audio Functionality**
*   **AudioWorklet Implementation:** Transition the math logic from the main thread UI visualizer to an `AudioWorkletProcessor` to allow sample-accurate scaling for true multi-channel audio rendering.
*   **Data Recording:** Ability to record the scaled data tracks and export them as a multi-channel `.wav` file or a `.csv` file for data-science applications. 
*   **Device Output Selection (`setSinkId`):** Utilize experimental browser APIs to allow users to specifically define which audio output channel (Bluetooth, USB interface, Speakers) the app routes data to.

## ⚠️ Requirements
*   A working microphone.
*   Must be run on `localhost` or an `https` connection.
