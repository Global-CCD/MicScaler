# MicScaler

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **1,000-channel mathematical processor**, allowing for real-time signal scaling, multi-tier polarity inversion, microsecond signal gating, and now, **native audio export**.

**Now featuring the AuraConv Engine:** This version integrates the sample-accurate interval blocking, convolution smear, and HRTF spatial rotation made famous by the [AuraConv repository](https://github.com/Transparency-2025/AuraConv), acting directly on the live audio feed.

## Demo Links on Cloudflare
* v1.0.0 - 
* v1.1.0 - 
* v1.2.0 - https://v1-2-0-micscaler.pages.dev/
* v1.3.0 - https://v1-3-0-micscaler.pages.dev/
* v1.4.0 - https://v1-4-0-micscaler.pages.dev/
* v1.5.0 - https://v1-5-0-micscaler.pages.dev/
* v1.6.0 -
* v1.7.0 -
* v1.8.0 - https://v1-8-0-micscaler.pages.dev/
* v1.9.0 - https://v1-9-0-micscaler.pages.dev/

  ## 🚀 Quick Start
1. Download `index.html` and open it in any modern web browser.
2. Set your track count (up to 1,000) and click **Start Microphone**.
3. **AuraConv Comb:** Enable the AuraConv row to chop the signal into micro-intervals (e.g., block every 50 samples) and rotate the chopped signal in 3D space.
4. **Automate:** Use the "Step (+%)" tool to calculate cascading signal spreads or enable "Pattern Invert" to phase-shift interleaved tracks.
5. **Record:** Set an auto-stop limit and capture the manipulated soundscape natively to `.wav`.

## 💾 Zero-Dependency Audio Recording Engine
Modern web browsers natively record audio into compressed `.webm` containers. Because professional audio workflows require pure, uncompressed raw data, MicScaler features a custom-built, zero-dependency **PCM-to-WAV compiler**.

*   **WAV (Uncompressed PCM):** Captures the raw Float32 data array post-processing and mathematically generates a valid 16-bit RIFF/WAVE header on the fly inside the browser.
*   **OPUS / FLAC:** Utilizes the native `MediaRecorder` API for highly compressed (Opus) or lossless (FLAC) exports. *(Note: FLAC support depends on your specific browser engine).*
*   **X-Minute Auto-Stops:** Built-in `setTimeout` logic prevents memory overflows by automatically halting the recording loop and prompting the download exactly when your desired time limit is reached.

## 🎛️ The AuraConv Engine
The second control row is entirely dedicated to integrating AuraConv's mechanics:
*   **Sample-Accurate Chopping:** Rather than relying on unreliable JavaScript `setInterval` clocks, the engine tracks the absolute sample counter (e.g., 48,000Hz). You can strictly block or allow audio in exact N-sample chunks.
*   **Mode Polarity:** `Burst` allows audio every N-samples. `Gap` blocks audio every N-samples.
*   **Synthetic Convolution Reverb:** We generate a mathematical 2-second white-noise exponential decay array to smear the chopped transients without relying on external `.wav` Impulse Responses.
*   **HRTF 3D Rotation:** Real-time spatial rotation utilizing Web Audio's `PannerNode`, rotating the chopped bursts around your head at 2.0 radians per second.

## 🎛️ The Sequence Automation Engine
In addition to the static "Apply Step" feature, MicScaler now includes a time-based automation envelope.
*   **Logarithmic Descent:** When activated, the engine applies an exponential/logarithmic calculation across the timeline. This ensures that the descent through microscopic fractions (e.g., from `0.01` to `0.0001`) feels mathematically linear to the ear and signal path.
*   **Throttled DOM Handling:** Updating 1,000 visual inputs 60 times a second creates severe lag in standard browsers. The Auto-Step engine solves this by decoupling the math from the UI. The memory array processes the descent at native audio-rates, while the HTML text boxes are cleanly throttled to update at 10 frames per second.

## ✨ Key Features
*   **1,000-Channel Throughput:** Optimized to perform over 500,000+ multiplicative math operations per animation frame.
*   **Pattern-Based Inversion:** Automatically invert every 2nd, 3rd, 4th, or 5th track.
*   **Native Audio Export:** Bypass the browser's compressed WebM engine with our custom, zero-dependency PCM-to-WAV compiler.
*   **Hardware Routing:** Built-in WebRTC constraints to bypass Android/iOS VoIP hijacking, enabling pure loudspeaker output.
