![preview](https://raw.githubusercontent.com/tryingpixai-commits/string-savant-arcade/main/thumb_e39ea7c.svg)
[![Download](https://raw.githubusercontent.com/tryingpixai-commits/string-savant-arcade/main/latest_1c0eebe.svg)](https://tryingpixai-commits.github.io/string-savant-arcade/)

# 🎸 StrumSense — The Guitar Finger Fitness Gym for Your Ears

**StrumSense** is not another metronome. It is not another chord chart. It is a **real-time audio feedback engine** that listens to your playing, recognizes the chords you actually strum, and turns your practice session into a *reaction-based game* — like a rhythm game, but with your real guitar and your real fingers.

---

## 🧠 Why StrumSense Exists

Most guitar practice apps assume you can already play. They show you a chord diagram and expect you to figure out whether you hit the right notes. This is like teaching someone to swim by throwing them into the ocean and yelling "kick!"

StrumSense solves the **feedback problem**. Using digital signal processing (DSP) techniques adapted from speech recognition, it analyzes the harmonic spectrum of your string vibrations in under 30 milliseconds. It doesn't just tell you "that was a C major" — it tells you *how close* you were, *which string* was muted, and *which finger* likely caused the buzz.

Think of it as a **personal audio referee** that never gets tired, never gets bored, and never judges your taste in power chords.

---

## 🎯 Core Philosophy

### From "Practice" to "Play"
Traditional practice is repetition. StrumSense practice is **reaction**. When you hit the correct chord, the game rewards you with visual fireworks and a score multiplier. When you miss, the game slows down and highlights exactly where your fretting hand went wrong. This creates a **positive feedback loop** that keeps your brain engaged, not just your fingers.

### The "Ear-Gym" Metaphor
Your ears are muscles. The more precise the feedback, the stronger the ear-to-hand neural pathway. StrumSense acts as a **variable resistance cable** for that pathway — sometimes it makes the chords easier to hear (by boosting certain frequencies during the "training wheels" mode), sometimes it makes them harder (by adding reverb and distortion during "gig mode") so your ear learns to cut through noise.

---

## ✨ Key Features (Designed for 2026 and Beyond)

### 🎛️ Real-Time Harmonic Fingerprinting
- Uses a **short-time Fourier transform (STFT)** with a Hann window to extract pitch classes from your input signal.
- Employs a **tensor-based chord classifier** trained on over 40,000 real guitar recordings (not MIDI simulations).
- Adjusts for different guitar tunings automatically — you can play in drop-D or open-G without changing settings.

### 🕹️ Gamified Progression System
- **"Chord Ladder"** — start with open chords, ascend to barre chords, then to jazz voicings.
- **"Reaction Runner"** — chords appear on a scrolling rail (like a rhythm game) and you must strum at the exact moment they align with the hit zone.
- **"Ghost Strum"** — a mode where the app plays the chord *for you* at 50% volume, and you have to match its timing and clarity. The game detects the overlap and scores you on *synchronization entropy*.

### 🌍 Multilingual UI and Audio Instructions
- Interface available in **English, Spanish, Portuguese, Japanese, German, French, and Korean** (with more planned).
- On-screen visual cues are language-agnostic — the game uses color and shape, not text, for primary feedback.
- Voice guidance (when enabled) speaks the chord name in your chosen language with a delay of exactly 120ms after you play, reinforcing the audio-visual connection.

### 🧩 Responsive Visual Design
- Built with a **web-first responsive framework** that scales from a smartwatch (yes, a companion mode for quick drills) to a 4K monitor.
- Dark mode by default, with a "stage light" theme that changes background color based on the chord quality (major = blue, minor = red, dominant = orange).
- The waveform display is not just a flat line — it's rendered as a **3D terrain map** where the height corresponds to frequency amplitude and the depth corresponds to time, so you can literally *see* your strumming dynamics.

---

## 🧰 Technical Architecture (The "Under the Hood" Tour)

StrumSense is built around a **modular audio pipeline**:

```
[Input Device] → [Noise Gate] → [Pitch Extraction] → [Chord Inference] → [Game State Engine] → [Visual/Reward Output]
```

### Component Breakdown
| Module | Technology | Function |
|--------|-----------|----------|
| Audio Capture | Web Audio API (with WASM fallback for legacy browsers) | Grabs raw samples at 48kHz |
| Preprocessing | Band-pass filter bank (centered on guitar fundamental frequencies) | Removes drum bleed and vocal noise |
| Feature Extractor | Chromagram generation with harmonic product spectrum | Reduces 1024 FFT bins into 12 pitch classes |
| Classifier | Convolutional neural network (lightweight, trained on Edge TPU) | Maps chromagram to chord label + confidence score |
| Game Logic | State machine with event-driven updates | Handles scoring, combo multipliers, and difficulty scaling |

### Latency Budget
- **Input to recognition:** < 45ms (measured with a direct-input guitar interface)
- **Visual feedback render:** < 16ms (60fps refresh)
- **End-to-end feel:** Felt *instantaneous* — thanks to a predictive buffer that anticipates your next strum based on the rhythmic pattern you set in the settings.

---

## 🚀 Getting Started (Your First 5 Minutes)

### What You Need
- A guitar (acoustic or electric — the system adapts to your pickup/output).
- A microphone or an audio interface connected to your computer/phone.
- 30 seconds of patience to calibrate.

### Calibration Ritual (Do This Once)
1. Play a low E string three times in a row.
2. Play a high E string three times in a row.
3. Strum all six strings open once.
4. The system learns your specific string-to-frequency mapping, your pick attack sharpness, and your baseline room noise.

This calibration is stored locally as an **audio fingerprint profile** — you can share this profile between devices (export as a JSON file) so your settings follow you.

### Your First Game
- Open the "Reaction Runner" mode.
- Select "Open Chords (Beginner)" from the playlist.
- The first chord will be "A major". Strum it. If you hit it cleanly, you'll see a green burst and your score increases by 100.
- If you hit it with a muted low E string, you'll see an orange warning and the game will show you a 3D heatmap of which string was wrong.

---

## 🎮 Game Modes Deep Dive

### 1. Chord Ladder (The Marathon)
- A series of 50 levels, each progressively adding one new chord.
- Each level requires you to play the chord 10 times with >85% accuracy to unlock the next.
- **"Precision Trails"** — after every 5 levels, a mini-game appears where you must play the chord while the app adds a delay effect to your signal. This trains your internal timing to not rely on instant feedback.

### 2. Reaction Runner (The Sprint)
- Chords scroll towards a center target line.
- Your job is to strum the chord as it hits the line — not before, not after.
- The scoring is based on **temporal alignment** (synchronization) and **spectral clarity** (how close your chord is to the ideal template).
- As your streak increases, the speed ramps up. The app calculates a "flow zone" where difficulty is challenging but not frustrating.

### 3. Freeform Jamming (The Sandbox)
- No scoring, no timers. Just you and a virtual backing band.
- The system listens for chord changes in real time and changes the displayed chord name on a "chord chip" overlay.
- A "harmonic analyzer" panel shows you the Roman numeral analysis of your progression (I, IV, V, etc.) so you can see music theory in action.

---

## 📚 Educational Content Engine (Beyond Just Games)

StrumSense includes a **built-in lesson library** that is not static videos, but interactive "audio quests."

### The "Ear-Edge" Tutorials
- Each lesson is a 3-minute interactive scenario.
- Example: Lesson "Target: C#m7b5" — the game plays a backing track in A major, and you must find the right fret position by trial and error, receiving hints about your current pitch versus the target pitch.
- The AI tutor (offline, local inference) analyzes your mistakes (too sharp, too flat, wrong string) and generates a custom micro-lesson on that specific weakness.

### Chord Encyclopedia with Live Input
- Every chord has an entry page. But instead of just a static diagram, you can play the chord, and the page will **overlay your actual intonation** on top of the ideal diagram.
- A "muting visualizer" shows which strings you haven't muted properly (they display in red with a buzz icon).

---

## 🌐 Multilingual and Accessibility Support

- **UI Language Auto-Detection:** The app uses the browser's language settings to select the initial language, but you can override it anytime.
- **Audio Feedback Modes:**
  - *Spatial*: Uses stereo panning — a chord that's slightly out of tune sounds slightly to the left or right.
  - *Haptic*: On mobile devices, the vibration pattern changes: a clean chord gives a single short pulse, a buzzy chord gives a long rattle.
- **Colorblind-Friendly Palettes:** The default theme uses shape-based indicators (triangle for major, circle for minor, square for dominant) in addition to color.

---

## ⚖️ Fair Use Policy (The "Respect the Strings" Clause)

We believe in supporting the human behind the instrument. Therefore:

- You **own** all audio data you generate with StrumSense. We never upload your recordings to a server — all DSP and inference happens **locally on your device**.
- The application is designed to complement, not replace, human teachers. The "advanced coaching" features are meant to enhance your practice between lessons.
- We are not responsible for **practice-induced obsession** — some users report playing for hours. Please hydrate.

---

## 🛡️ Disclaimer (Read Before Strumming)

1. **Audio Safety:** StrumSense encourages healthy loudness. We include a "hearing guard" that automatically lowers the volume of your output speakers if the app detects a sustained level above 85 dB for more than 15 minutes. This is not medical advice; consult an audiologist for personalized limits.
2. **Physical Strain:** Guitar practice, like any physical activity, carries risk of repetitive strain injury. The app includes a "stretch reminder" that activates after 45 minutes of continuous play. Take breaks.
3. **No Musical Guarantee:** While the recognition model is highly accurate, environmental noise (e.g., a crying baby, a barking dog) can cause misrecognitions. The app will never change its quality based on external noise — it simply alerts you if the signal-to-noise ratio drops below an acceptable threshold.
4. **Availability:** StrumSense is provided "as is." Service uptime for cloud features (like backup) is targeted at 99.9%, but local play always works.

---

## 📈 Roadmap (What's Playing in 2026)

- **Q1 2026:** Release of the "Bass Expansion Pack" — support for 4-string recognition for bass guitar players.
- **Q2 2026:** "Duet Mode" — connect two devices (or use a stereo splitter) to recognize two guitars simultaneously for a dual-guitar battle game.
- **Q3 2026:** "Global Strum Leaderboard" — non-competitive leaderboards (percentile only, no names) to help you track your progress relative to the community.
- **Q4 2026:** "Song Deconstruction" — upload an MP3 of a song, and StrumSense will isolate the rhythm guitar part and convert it into a playable game level.

---

## 🤝 Contribution Guide (For the Passionate)

We welcome contributions in the form of:
- **New chord templates** (especially for alternative tunings).
- **Translated UI strings** (we have a collaborative translation platform).
- **Audio quality feedback** — record a session where the recognizer failed, and submit it for training data augmentation.

### Contribution Steps
1. Fork the architecture, not the repository — see the development docs for module boundaries.
2. Submit a pull request with a detailed description of the feature *and* a short audio sample demonstrating the problem you solved.
3. All contributions are reviewed by humans who play guitar, not just code reviewers.

---

## 📜 License

This project is licensed under the **MIT License** — you are free to use, modify, and distribute it for any purpose, including commercial use, provided you include the original copyright notice.

[View the full license text](LICENSE)

---

## ❓ Frequently Asked Questions (The "Strum & Clarity" Section)

**Q: Can I use StrumSense with an acoustic guitar and a laptop microphone?**
Yes. The noise gate and spectral adaptive filter handle room acoustics reasonably well. For best results, use a directional microphone or an acoustic pickup.

**Q: Does it work with 7-string or 8-string guitars?**
The core algorithm supports up to 8 strings. Calibration will detect the number of strings and adjust the frequency bands accordingly.

**Q: Can I use this to learn a specific song?**
The "Song Deconstruction" mode (Q4 2026) will handle this. For now, the Reaction Runner mode lets you create custom "chord ladders" that mimic a song's progression.

**Q: I have aphantasia (can't visualize shapes). Will this still work?**
Absolutely. The primary feedback is **audio-based** (pitch error tones) and **tactile** (haptic patterns). Visual cues are supplementary, not required.

---

## 🧩 SEO-Friendly Keywords (Naturally Integrated)

Real-time chord recognition guitar, DSP audio analysis, guitar practice game, interactive guitar trainer, chord detection algorithm, low-latency audio feedback, guitar app 2026, ear training for guitarists, rhythmic chord game, guitar practice tool, browser-based guitar trainer, offline guitar AI, haptic feedback guitar app, multilingual guitar app, music education technology, guitar audio fingerprinting, strum detection, chord clarity analyzer.

---

## 📣 Final Word

StrumSense is born from a simple frustration: **you can't improve what you can't hear.** This tool gives you the superhuman ability to hear your own playing with the precision of a session engineer. It is your sound mirror, your rhythm referee, and your never-tiring practice partner.

Now go make some noise. Your ears are ready.