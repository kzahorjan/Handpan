# Handpan

A browser-based handpan instrument with polyrhythmic sequencer and audio effects. No dependencies, no build step — a single HTML file.

**[Live demo →](https://your-username.github.io/handpan)**

---

## Features

### Instrument
- **5 tone fields** tuned to D Dorian pentatonic: D4 · F4 · A4 · C5 · E5
- **Velocity sensitivity** via pointer pressure (Apple Pencil / supported touch screens)
- **Multi-touch** — play multiple notes simultaneously
- **Ripple animation** on each hit

### Looper
- **Record** up to 2 bars, auto-quantises to bar length at detected BPM
- **Playback** loops continuously with a visual arc progress indicator
- Hit markers shown on the loop arc, sized by velocity

### Polyrhythm
- **3 independent lanes** (A / B / C) running simultaneously
- Each lane has its own **ratio** (1:1 · 2:3 · 3:4 · 3:5 · 4:5 · 5:6 · 5:7 · 2:1)
- Each lane has its own **note sequence** and **volume**
- Per-lane **mute** without stopping playback
- Animated **playhead dots** orbit the disc showing each lane's position

### Tempo
- **Tap** the BPM display to tap-tempo
- **Hold ± buttons** to sweep continuously
- **Auto-detect** from your playing

### Effects
- **Reverb** — synthesised convolution IR (size + mix)
- **Delay** — tempo-synced (1/32 → 1/1), feedback, mix
- **Chorus** — LFO-modulated short delay (rate, depth, mix)
- **Filter** — low-pass with resonance
- All effects are collapsible and toggled independently

---

## Usage

### Locally
Just open `index.html` in any modern browser. No server required.

```bash
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

### GitHub Pages
1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your instrument will be live at `https://your-username.github.io/handpan`

### iOS Safari note
The first tap triggers a motion/audio permission prompt on iOS 13+. Tap **once anywhere** to unlock audio, then play.

---

## Browser support

| Browser | Support |
|---|---|
| Chrome / Edge | ✅ Full |
| Safari (macOS) | ✅ Full |
| Safari (iOS) | ✅ Full (requires first tap for audio) |
| Firefox | ✅ Full |

---

## Project structure

```
handpan/
└── index.html    # Everything — HTML, CSS, JS, audio engine
```

---

## Audio engine notes

All sound is synthesised via the Web Audio API — no samples, no external files.

Each note is built from:
- Three sine wave partials (fundamental + octave + octave+fifth)
- A short pitch-drop on attack (characteristic handpan "thwack")
- A metallic band-pass noise transient

Signal chain:
```
noteGain → preFX → [chorus insert] → [delay insert] → [filter] → output
                                   ↘ [reverb send] → output
```

Effects use a clean serial insert topology — notes connect only to `preFX`, never directly to FX nodes, avoiding frequency binding issues with shared delay nodes.

---

## License

MIT — do whatever you want with it.
