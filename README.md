# MicScaler

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **1,000-channel mathematical processor**, allowing for real-time signal scaling, multi-tier polarity inversion, and microsecond signal gating.

## 🚀 Quick Start
1. Download `index.html` and open it in any modern web browser.
2. Set your track count (up to 1,000) and click **Start Microphone**.
3. **Automate:** Use the "Step (+%)" tool to calculate cascading signal spreads or enable "Pattern Invert" to phase-shift interleaved tracks (2nd, 3rd, 4th, 5th).
4. **Gate:** Enable the "Math Gate" or "Speaker Gate" to chop signal at sub-millisecond speeds.

## 🧮 The Math Engine
MicScaler treats audio as pure floating-point data streams.
*   **Scale:** Multiplicative range control ($Input \times Scale\%$).
*   **Net Polarity:** The signal phase is determined by three cascading layers: 
    `NetPolarity = GlobalMaster * PatternInvert * TrackSpecific`
*   **Precision:** Supports mathematical scaling with **0.0001%** precision.

## ✨ Key Features
*   **1,000-Channel Throughput:** Optimized to perform over 500,000+ multiplicative math operations per animation frame.
*   **Pattern-Based Inversion:** Automatically invert every 2nd, 3rd, 4th, or 5th track to create complex phase-interleaved arrays.
*   **Dual-Layer Signal Gating:** 
    *   **Math Input Gate:** Chops the data stream *before* it hits the math engine.
    *   **Speaker Output Gate:** Physically modulates the hardware speaker output using a 10kHz square-wave gate.
*   **Hyper-Precision Controls:** Fine-tune every track down to 0.0001% for exact signal calibration.
*   **Mobile Hardware Routing:** Built-in WebRTC constraints to bypass Android/iOS VoIP hijacking, enabling pure loudspeaker output.

## 🗺️ Roadmap: Future Features

**Phase 1: Advanced Data Manipulation**
*   **Offset Engine (+):** Implement `(Input * Scale) + Offset` logic to shift signal baselines for sensor calibration and bias correction.
*   **Hard Clipping/Clamping:** Add threshold controls to introduce intentional saturation/distortion at specific track levels.

**Phase 2: External Data Bridge**
*   **WebSockets/OSC/MIDI:** Broadcast the processed math results to external software (TouchDesigner, Max/MSP, or DAWs) for live-coding and reactive data visualization.

**Phase 3: Kernel/Hardware Integration**
*   **AudioWorklet Processing:** Move the math engine to a high-priority background audio thread to enable sample-accurate multi-channel rendering without UI-thread latency.
*   **Python/Pi Port:** Native support for Raspberry Pi/I2S hardware setups for dedicated "Wall Plug" signal conditioning.

## ⚠️ Requirements
*   A working microphone.
*   Must be run on `localhost` or an `https` connection.
