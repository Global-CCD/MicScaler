# MicScaler

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It isolates the process of signal scaling, inversion, and microsecond data gating, turning your browser into a **1,000-channel mathematical processor**.

## Demo Links on Cloudflare
* v1.0.0 - 
* v1.1.0 - 
* v1.2.0 - https://v1-2-0-micscaler.pages.dev/
* v1.3.0 - https://v1-3-0-micscaler.pages.dev/
* v1.4.0 - https://v1-4-0-micscaler.pages.dev/
* v1.5.0 - https://v1-5-0-micscaler.pages.dev/

## 🚀 Quick Start
1. Download `index.html` and open in any modern web browser.
2. Set your track count (up to 1,000).
3. *(Optional)* Set an **Auto-Toggle (ms)** to chop the signal at high speeds.
4. Click **Start Microphone**.
5. Use the **Step (+%)** tool to instantly apply cascading mathematical sequences.

## ⏱️ Sub-Millisecond Digital Gating (Auto-Toggle)
Traditional hardware microphones cannot be turned on and off in 0.1 milliseconds without crashing the operating system. MicScaler overcomes this by implementing a **Sample-Accurate Digital Gate**. 

By calculating the passage of time using audio sample rates (e.g., 48,000Hz), the app mathematically "zeros out" the data stream at exact sub-millisecond intervals. 
*   **0.1ms:** Generates a 10,000Hz Amplitude Modulation effect.
*   **100ms:** Creates a fast stutter/chopper effect.
*   **1000ms (1s):** Standard 1-second auto-mute cycle.

## ✨ Key Features
*   **1,000-Channel Throughput:** Optimized to perform over 500,000+ multiplicative math operations per frame.
*   **Hyper-Precision:** Supports scaling inputs down to **0.0001%** precision.
*   **Cascading Logic:** Apply global master inversions or individual track-level phase flips.
*   **Dynamic Step Progression:** Automatically calculate complex sequences across the entire track array with high-precision step increments.

## 🗺️ Roadmap: Future Features

**Phase 1: Data Bridge**
*   **OSC & WebSocket Integration:** Stream the processed 1,000-track math data to external software like TouchDesigner, Resolume, or Max/MSP.
*   **Web MIDI Output:** Map the mathematical outputs of the 1,000 tracks to MIDI CC data for DAW integration.

**Phase 2: Advanced DSP**
*   **Offset Engine (+):** Implement `(Input * Scale) + Offset` logic to shift signal baselines for sensor calibration.
*   **Clipping/Clamping:** Add hard/soft saturation limits for the 1,000 channels.

**Phase 3: Deep Audio**
*   **AudioWorklet Processing:** Shift the math engine from the UI thread to a dedicated `AudioWorklet` to enable sample-accurate multi-channel audio rendering without UI stutter.
*   **Export/Recording:** Multi-channel .wav or .csv recording of the scaled data streams.

## ⚠️ Requirements
*   A working microphone.
*   HTTPS or `localhost` required for microphone access.
