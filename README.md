# MicScaler

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It isolates the process of signal scaling and inversion, turning your browser into a **1,000-channel mathematical processor**.

## Demo Links on Cloudflare
* v1.0.0 - 
* v1.1.0 - 
* v1.2.0 - https://v1-2-0-micscaler.pages.dev/
* v1.3.0 - https://v1-3-0-micscaler.pages.dev/
* v1.4.0 - https://v1-4-0-micscaler.pages.dev/
* v1.5.0 - https://v1-5-0-micscaler.pages.dev/

## 🚀 Quick Start
1. Download `index.html`.
2. Open in any modern web browser.
3. Set your track count (up to 1,000) and click **Start Microphone**.
4. Use the **Step (+%)** tool to instantly apply cascading mathematical sequences across the entire array.

## 🧮 The Math Logic
Unlike standard audio mixers, MicScaler processes audio as pure floating-point data streams.
*   **Scale:** Multiplicative range control ($Input \times Scale\%$).
*   **Net Polarity:** Cascading phase logic ($GlobalMaster \times TrackSpecific$).
*   **Precision:** Supports scaling inputs down to **0.0001%** precision.

## ✨ Key Features
*   **1,000-Channel Throughput:** Optimized to perform over 500,000+ multiplicative math operations per animation frame while maintaining 60fps.
*   **Zero-Canvas Overhead:** By removing individual track visualizers, the app focuses on pure data throughput, drastically reducing GPU/CPU thermal load.
*   **Cascading Logic:** Apply global master inversions or individual track-level phase flips.
*   **Dynamic Step Progression:** Automatically calculate complex sequences across the entire track array with high-precision (0.0001) step increments.
*   **Hardware Bypass:** Built-in mobile audio routing controls to prevent OS-level VoIP "Earpiece" hijacking.

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
