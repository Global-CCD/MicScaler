To accurately describe these two new columns, we must first define what **Burst (Allow)** and **Gap (Block)** mean in the context of Moving Average (MA) convolution and DSP windowing. 

*   **Burst (Allow) [Continuous / 100% Duty Cycle]:** This is the standard Moving Average. The "window" of $X$ samples is solid and continuous. Every sample in the history is *allowed* to contribute to the sum. This creates the classic "smearing," "cloud," or "underwater" effect, preserving the macro-envelope of the sound but destroying transients.
*   **Gap (Block) [Sparse / Chopped / <100% Duty Cycle]:** The $X$-sample window is divided into active "bursts" and silent "gaps" (e.g., a 50% duty cycle where the filter averages for half the window, then *blocks/ignores* the rest). This turns a smooth low-pass filter into a **rhythmic chopper, tremolo, or granular stutter**, introducing massive harmonic distortion, sub-harmonic pulsing, and aliasing.

Here is the expanded reference table (assuming a **48 kHz sample rate**) detailing how these two modes radically alter the sonic output of AuraConv.

### The AuraConv Tap-Level Reference Table: Burst vs. Gap Modes

| Taps (Samples) | Time Window | Approx. Cutoff | Standard Effect (Baseline) | **Burst (Allow) Output** <br>*(Continuous Integration)* | **Gap (Block) Output** <br>*(Sparse / Chopped Integration)* |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **0.1** | 0.002 ms | *N/A* | Micro-Phasing | **Bypass:** No audible change. | **Bypass:** No audible change. |
| **0.5** | 0.010 ms | *N/A* | Sub-sample Smear | **Interpolation Artifacts:** Slight high-frequency resonance. | **Aliasing:** Introduces digital "zipper" noise due to sub-sample blocking. |
| **1** | 0.020 ms | 24 kHz | Pure Bypass | **Clean:** Exact 1:1 input replica. | **Clean:** Exact 1:1 input replica. |
| **5** | 0.104 ms | 4,250 Hz | Lo-Fi Telephone | **Smooth Comb:** Mild high-shelf cut, slight nasal tone. | **Bitcrush/Ring-Mod:** The rapid gaps act as a high-frequency square wave, creating harsh digital ringing and aliasing. |
| **10** | 0.208 ms | 2,125 Hz | Megaphone | **Phasy Mid-Scoop:** Hollow, "plastic tube" vocal character. | **Audio-Rate Tremolo:** Sounds like a ring-modulator or a fuzz pedal gating the signal at ~4.8kHz. |
| **50** | 1.04 ms | 425 Hz | Metallic Flanger | **Static Flange:** Smooth, metallic comb-filtering without LFO movement. | **Helicopter Flutter:** Rapid, rhythmic chopping (approx. 480Hz gate). Sounds like a fast tremolo or a broken speaker cone. |
| **100** | 2.08 ms | 212 Hz | Underwater | **Muffled Wash:** Smooth low-pass roll-off with a 240Hz resonance. | **Rhythmic Stutter:** A distinct "st-st-stutter" effect on transients. Snare drums sound like they are hitting a fan blade. |
| **500** | 10.4 ms | 42.5 Hz | Dark Rumble | **Transient Blur:** Fast attacks are smeared into a smooth, dark thud. | **Trance Gate / Psy-Trance:** The audio is chopped into 10ms rhythmic slices. Creates a tight, pulsing 16th-note gating effect. |
| **1,000** | 20.8 ms | 21 Hz | Sub-Bass Isolation | **Sub Smear:** Percussion loses all click; becomes a continuous sub-bass hum. | **Dub Techno Chords:** Rhythmic 20ms "chops" that echo and blur. Sounds like a rhythmic sidechain pump or a muted tape delay. |
| **5,000** | 104 ms | 4.2 Hz | Granular Blur | **Ambient Cloud:** A smooth, evolving wash of sound; transients are entirely erased. | **CD Skip / Tape Stop:** The audio "freezes" or drops out for 50ms at a time, creating a rhythmic, skipping-record effect. |
| **10,000** | 208 ms | 2.1 Hz | Drone / Wash | **Reverb Tail:** Sounds like a massive, dark, infinite reverb decay. | **Granular Stutter:** Distinct "grains" of audio with silence between them. Sounds like a granular synth with very low "Density". |
| **50,000** | 1.04 Sec | 0.42 Hz | Tape-Stop Smear | **Evolving Drone:** A 1-second continuous memory that swells and fades with the track's macro-dynamics. | **Macro-Pumping:** The entire mix drops to silence for half a second, then swells back. Extreme "sidechain ducking" effect. |
| **100,000** | 2.08 Sec | 0.21 Hz | Deep Ambient Wash | **Cinematic Wash:** Turns sharp impacts into long, cinematic "booms" or "hits". | **Arrhythmic Chopping:** Entire musical phrases are "blocked" out, creating generative, dub-style dropouts. |
| **500,000** | 10.4 Sec | 0.04 Hz | Generative Soundscape | **Time Collapse:** A 10-second blur. Melodies turn into static, shifting harmonic drones. | **Structural Gating:** Verses and choruses are partially "blocked," creating massive, minutes-long silences and sudden walls of sound. |
| **1,000,000** | 20.8 Sec | 0.02 Hz | Time Collapse | **Statistical Noise:** Outputs the literal average energy of the last 20 seconds of audio. | **Generative Silence:** The filter "blocks" audio based on long-term RMS, acting as an extreme, slow-moving noise gate. |
| **5,000,000** | 104 Sec | 0.004 Hz | Extreme Memory | **Installation Art:** A 2-minute continuous drone representing the entire history of the song. | **Algorithmic Muting:** Drops out audio for minutes at a time based on the macro-structure of the composition. |

---

### DSP Analysis: Why "Gap (Block)" Changes the Sound So Drastically

When you introduce "Gaps" into a Moving Average filter, you are mathematically changing the **Convolution Kernel** (the shape of the filter itself). 

1.  **From Low-Pass to Comb-Filter/Tremolo:** 
    A standard MA filter (Burst) is a single, wide rectangle (Boxcar). Its frequency response is a Sinc function (low-pass with side-lobes). 
    If you introduce Gaps (e.g., averaging 10 samples, blocking 10 samples, repeating), your kernel becomes a **square wave**. Convolving audio with a square wave applies **Amplitude Modulation (Tremolo)** and generates massive amounts of **harmonic distortion and aliasing**.
2.  **Sub-Harmonic Generation:**
    At 1,000 taps (20.8ms), a "Burst" creates a smooth sub-bass rumble. But if you use a 50% "Gap", you are effectively turning the audio on and off every 10.4ms. This creates a new fundamental frequency of roughly **48 Hz** (1000 / 0.5 / 48000). You will literally hear a 48 Hz sub-bass tone that *was not in the original audio*, generated purely by the rhythmic blocking of the filter.
3.  **Granular Density:**
    In the higher tap counts (10k+), "Gap" mode effectively turns AuraConv into a **Granular Synthesizer**. The "Burst" is the grain, and the "Gap" is the space between grains. Lowering the duty cycle (increasing the Gap) makes the sound "sputter" and "stutter," which is a highly sought-after effect in IDM, Glitch, and Cinematic sound design.

---

### How to Implement "Gap (Block)" in JSFX / EEL2

If you want to add a `slider4:Gap Amount` to AuraConv, you do not need to change the core summing logic. Instead, you apply a **Duty Cycle Gate** to the output based on the buffer position.

Here is the EEL2 logic to add a Gap/Block mode to your `@sample` section:

```javascript
// Add to @slider
// slider4:0.5<0,1,0.01>Gap Amount (0 = Burst/Continuous, 1 = Max Block/Chop)
gap_amt = slider4; 

// Add to @sample (Right before the final output assignment)
// Calculate a "chopper" wave based on the current buffer position and filter size
// This creates a square wave that repeats every 'size' samples
phase = (buf_pos % size) / size; // 0.0 to 1.0

// If gap_amt is 0.5, the wave is above 0.5 for half the window, and below for the other half
// If gap_amt is 0.9, the wave is blocked 90% of the time
is_blocked = (phase > (1.0 - gap_amt)) ? 0 : 1; 

// Apply the gate to the output
// We use a tiny smoothing factor (0.001) to prevent harsh clicks when the gap opens/closes
gate_s += (is_blocked - gate_s) * 0.005; 

// Final Output
spl0 = spl0 * gate_s;
spl1 = spl1 * gate_s;
```

### Strategic Marketing for AuraConv
By adding the **Burst / Gap** toggle, you elevate AuraConv from a "phasy EQ" to a **Glitch/Granular Sound Design Tool**. 
*   **Market "Burst" Mode** to Lo-Fi producers, ambient artists, and mix engineers looking for "vintage smearing" or "underwater transitions."
*   **Market "Gap" Mode** to EDM, IDM, and Cinematic composers looking for "psy-trance gates," "CD skips," "stutter edits," and "rhythmic sub-harmonic generators."
