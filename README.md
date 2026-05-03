# MicScaler 🎛️

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. 

Unlike standard audio mixing concepts (where Gain is pre-processing signal strength and Volume is post-processing balancing), **MicScaler treats audio as pure data**. It transforms your browser into a **1,000-channel mathematical processor**, isolating the process of shrinking and expanding data ranges using multiplicative mathematics ($x$) at exact sub-millisecond precision.

## 🚀 Quick Start
1. Download the `index.html` file. (No installation, Node.js, or bundlers required).
2. Open it in any modern web browser (Chrome, Edge, Safari, Firefox).
3. Set your track count (up to 1,000) and click **Start Microphone**.
4. **Automate:** Use the "Auto-Step LFO" to sweep your signal spreads.
5. **Gate & Chop:** Enable the AuraConv comb filter or the sub-millisecond hardware gates.
6. **Record:** Set an auto-stop limit and capture the manipulated soundscape natively to `.wav`.

---

## 🧮 The Math Engine & Architecture
MicScaler utilizes the modern **Web Audio API `AudioWorklet`** standard. To maintain our strict "Single HTML File" zero-dependency rule, the C++ style processor class is converted to a virtual Blob in the device's RAM and injected dynamically. 

This guarantees **zero-latency background math**, processing over 500,000+ multiplicative operations per frame on a dedicated audio thread, completely immune to UI thread stutters (such as scrolling on mobile devices).

*   **Scale Multiplier:** Multiplicative range control ($Input \times Scale\%$).
*   **Net Polarity:** The signal phase is determined by three cascading layers: 
    `NetPolarity = GlobalMaster * PatternInvert * TrackSpecific`
*   **Hyper-Precision:** Supports mathematical scaling with **0.0001%** precision.

---

## ✨ Full List of Features

### 📡 Core Processing
*   **1,000-Channel Throughput:** Run up to 1,000 parallel tracks of data scaling simultaneously.
*   **Three-Tier Cascading Polarity:** Apply phase flipping on an individual track level, use **Pattern Invert** to automatically flip interleaved tracks (e.g., every 2nd, 3rd, 4th, or 5th track), or flip the entire global signal using the **Master Invert** toggle.
*   **Master Visualizer:** An optimized, 60fps HTML5 Canvas oscilloscope that maps the global input and polarity state without bottlenecking the CPU.

### ⏱️ Sequence Automation (Auto-Step LFO)
*   **Custom Boundary LFO:** Define any arbitrary `Start` and `End` scaling limits (e.g., from `1.0%` down to `0.0001%` or vice versa) and automate the array spread over a user-defined time duration.
*   **Infinite Looping:** The LFO utilizes drift-proof timing math to repeat the sequence endlessly without drifting out of sync.
*   **Bi-Directional Logarithmic Sweeps:** The automation interpolates logarithmically (`start * (end/start)^progress`), guaranteeing perfectly smooth perceptual sweeps through microscopic decimal fractions in both ascending and descending directions.
*   **UI Throttling:** The memory array calculates the LFO sweep at native audio rates, while the 1,000 visual HTML text boxes are cleanly throttled to repaint at 10fps to prevent audio-thread choking.

### 🔪 AuraConv Interval Engine
*   **Sample-Accurate Comb Filter:** Tracks the absolute hardware sample counter (e.g., 48,000Hz) to perfectly chop the data arrays into exact $N$-sample blocks (e.g., every 50 or 100 samples).
*   **Burst & Gap Modes:** Choose to either `Allow` audio through in rhythmic bursts or `Block` it to create rhythmic silence gaps.
*   **Synthetic Convolution Reverb:** Mathematically generates a lush, 2-second exponential-decay white-noise array on the fly to act as an Impulse Response (IR) smear, requiring no external `.wav` files.
*   **HRTF 3D Rotation:** Real-time spatial rotation utilizing Web Audio's `PannerNode`, rotating the chopped signal around the listener's head.

### 🎚️ Dual-Layer Sub-Millisecond Gating
*   **Math Input Auto-Toggle:** A digital gate that mathematically zeroes out the bit-stream feeding *into* the 1,000 tracks.
*   **Speaker Output Auto-Toggle:** Physically modulates the hardware speaker output using a 10kHz square-wave oscillator attached to a `GainNode`. Allows for brutal Amplitude Modulation (AM) effects down to `0.1ms`.

### 💾 Native Recording & Export
*   **Zero-Dependency WAV Compiler:** Bypasses compressed browser audio. Captures the raw `Float32` data array and mathematically compiles a valid 16-bit Mono `RIFF/WAVE` header on the fly inside the browser.
*   **MediaRecorder Support:** Supports highly compressed OPUS (`.webm`) and lossless FLAC exports (browser permitting).
*   **Auto-Stop Timers:** Enter a minute limit to record unattended. The app will automatically halt, compile, and trigger a local file download when the timer hits, preventing RAM overflows.

### 📱 Hardware Control
*   **Mobile Audio Routing Override:** Android and iOS natively hijack microphone streams for VoIP ("Phone Call") echo cancellation, which forces audio to the quiet top earpiece. The **Earpiece Mode** toggle overrides WebRTC constraints (`echoCancellation: false`), forcing the OS to blast the uncompressed signal out of the main bottom loudspeakers.

---

## 🗺️ Roadmap of Future Features

We are actively expanding MicScaler into a comprehensive suite for scientific signal analysis, acoustic research, and edge-device deployment.

### Phase 1: Advanced DSP & Data Manipulation
*   **Offset Engine (+):** Implement `(Input * Scale) + Offset` logic to shift signal baselines for sensor calibration and bias correction.
*   **Hard Clipping & Clamping:** Add user-defined mathematical limits to introduce intentional saturation, data-clipping, and threshold bounds across the 1,000 channels.
*   **DC Offset Filtering:** A dedicated high-pass filter at 5Hz to mathematically center raw Android microphone feeds that suffer from native electrical offsets.

### Phase 2: Hardware & Edge Integrations
*   **The "Wall Plug" Port (Python/Raspberry Pi):** Refactor the core Math Engine into a vectorized NumPy/Python script to be flashed onto headless Raspberry Pi Zero / ESP32 hardware. This will allow for dedicated hardware I2S microphone processing in embedded acoustic environments.
*   **Hardware Output Selection (`setSinkId`):** Utilize experimental browser APIs to allow users to explicitly define which physical audio output channel (Bluetooth, USB interface, specific Studio Monitor pairs) the app routes the data to.

### Phase 3: External Data Routing
*   **WebSockets & OSC (Open Sound Control):** Broadcast the processed mathematical results of the 1,000 tracks over `localhost` to drive reactive data visualization in external software like TouchDesigner, Resolume, or Processing.
*   **Web MIDI API Integration:** Convert the scaled, multi-track data outputs into continuous MIDI Control Change (CC) messages to drive DAW parameters (e.g., Track 1 controls a cutoff filter, Track 2 controls reverb decay in Ableton Live).

---

## ⚠️ Requirements & Safety
*   **Environment:** Must be run on `localhost` or an `https` connection, as browsers strictly block microphone access on unsecure `http` connections.
*   **Acoustic Feedback:** Using the "Speaker Out" feature on laptops/phones without headphones will likely result in an instantaneous and severe acoustic feedback loop. Use caution.
