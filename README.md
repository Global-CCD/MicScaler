# MicScaler

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **1,000-channel mathematical processor**, allowing for real-time signal scaling, multi-tier polarity inversion, microsecond signal gating, and now, **native audio export**.

## 🚀 Quick Start
1. Download `index.html` and open it in any modern web browser.
2. Set your track count (up to 1,000) and click **Start Microphone**.
3. **Automate:** Use the "Step (+%)" tool to calculate cascading signal spreads or enable "Pattern Invert" to phase-shift interleaved tracks.
4. **Record:** Set an auto-stop limit (e.g., 5 mins) and click **Start Recording**. The file will automatically compile and download to your device when the timer finishes.

## 💾 Zero-Dependency Audio Recording Engine
Modern web browsers natively record audio into compressed `.webm` containers. Because professional audio workflows require pure, uncompressed raw data, MicScaler features a custom-built, zero-dependency **PCM-to-WAV compiler**.

*   **WAV (Uncompressed PCM):** Captures the raw Float32 data array post-processing and mathematically generates a valid 16-bit RIFF/WAVE header on the fly inside the browser.
*   **OPUS / FLAC:** Utilizes the native `MediaRecorder` API for highly compressed (Opus) or lossless (FLAC) exports. *(Note: FLAC support depends on your specific browser engine).*
*   **X-Minute Auto-Stops:** Built-in `setTimeout` logic prevents memory overflows by automatically halting the recording loop and prompting the download exactly when your desired time limit is reached.

## ✨ Key Features
*   **1,000-Channel Throughput:** Optimized to perform over 500,000+ multiplicative math operations per animation frame.
*   **Pattern-Based Inversion:** Automatically invert every 2nd, 3rd, 4th, or 5th track to create complex phase-interleaved arrays.
*   **Dual-Layer Signal Gating:** Physical and Mathematical sub-millisecond choppers.
*   **Hyper-Precision Controls:** Fine-tune every track down to 0.0001% for exact signal calibration.
