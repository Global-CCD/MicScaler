# MicScaler

MicScaler is a lightweight, single-page web application designed to demonstrate the strict mathematical scaling of live microphone data streams. 

Unlike standard audio mixing concepts (where Gain is pre-processing signal strength and Volume is post-processing balancing), **MicScaler treats audio as pure data**. It isolates the process of shrinking and expanding data ranges using multiplicative mathematics ($x$).

## 🚀 Quick Start
1. Clone this repository or download `index.html`.
2. Open `index.html` in any modern web browser (Chrome, Firefox, Safari).
3. Click **Start Microphone** and allow browser permissions.
4. Speak into your microphone and adjust the scaling sliders per track.

## 🧮 The Math Logic
This app strictly adheres to the following definitions for processing:
*   **Gain:** Pre-processing / Signal saturation / Additive/Subtractive (dB) - *Not used here*
*   **Volume:** Post-processing / Mixing / Additive/Subtractive (dB) - *Not used here*
*   **Scale (This App):** Data control / Shrinking/Expanding ranges / Multiplicative ($x$)
*   **Offset:** Data control / Shifting the baseline / Constant Addition ($+$) - *See Roadmap*

### How it works under the hood
The app grabs the raw floating-point time-domain data of your microphone (`-1.0` to `1.0`). 
For every track, the app runs the following equation:
`ScaledValue = RawInput * (TrackPercentage / 100)`

If the raw input is `0.5` and Track 1 is set to `5%`:
`0.5 * 0.05 = 0.025` (The data range is mathematically shrunken).

## ⚠️ Requirements
*   A working microphone.
*   Must be run on `localhost` or an `https` connection, as browsers block microphone access on unsecure `http` connections.
```

---

### 3. List of Features

*   **Zero-Dependency Architecture:** A pure Vanilla HTML/CSS/JavaScript single-page app. No Node.js, React, or Webpack required.
*   **Live Microphone Capture:** Utilizes the Web Audio API (`AnalyserNode` and `FloatTimeDomainData`) to capture raw, uncompressed floating-point audio data.
*   **Dynamic Multi-Tracking:** Spawn between 1 and 10 concurrent tracks dynamically on the fly without interrupting the data stream.
*   **Independent Multiplicative Scaling:** Each track possesses a discrete slider to mathematically shrink or expand the incoming data stream range via multiplication (1% to 100%).
*   **Real-Time Data Visualization:** Individual HTML5 Canvas oscilloscopes for every track, rendering the mathematically scaled output at 60fps so you can visually verify the range shrinking/expanding.
*   **Feedback Prevention:** Audio data is routed exclusively to the math/visualization engine and is intentionally *not* connected to the speaker destination to prevent audio feedback loops.

---

### 4. Roadmap of Future Features

**Phase 1: Advanced Data Manipulation**
*   **Offset Integration (+):** Add an "Offset" slider to each track to fulfill the final logic tier: shifting the baseline via Constant Addition (e.g., `(RawInput * Scale) + Offset`).
*   **Inverted Scaling:** Allow negative scaling percentages (e.g., -5%) to invert the phase/data polarity while shrinking/expanding.
*   **Max/Min Clamping:** Introduce hard mathematical limits to clip the data if it exceeds user-defined thresholds after scaling is applied.

**Phase 2: Data Output & Routing**
*   **WebSockets/OSC Export:** Broadcast the scaled data streams over Localhost to control external software (like TouchDesigner, Resolume, or Max/MSP).
*   **Web MIDI API Integration:** Convert the scaled, multi-track data into continuous MIDI Control Change (CC) messages to drive DAW parameters (e.g., Track 1 controls filter cutoff, Track 2 controls reverb decay).

**Phase 3: Audio Functionality**
*   **AudioWorklet Implementation:** Transition the math logic from the main thread UI visualizer to an `AudioWorkletProcessor` to allow sample-accurate scaling for actual audio rendering.
*   **Data Recording:** Ability to record the scaled data tracks and export them as a multi-channel `.wav` file or a `.csv` file for data-science applications. 
*   **Input Selection:** A dropdown menu to select specific audio interfaces and inputs, rather than defaulting to the system's primary microphone.
