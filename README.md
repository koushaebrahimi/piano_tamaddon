# 🎹 Persian Piano

A fully client-side piano in the browser with **quarter-tone support**, **four synthesized instruments**, and **editable key bindings**.

**🔗 Live demo:** https://YOUR-USERNAME.github.io/persian-piano/

![Persian Piano screenshot](screenshot.png)

---

## Features

- **4 octaves** (C2–C6, 49 keys)
- **Persian dastgāh tunings** — Shur, Mahur, Segah, Chahargah, Bayati, Nava, Homayoun, Isfahan, Abu-Ata, Rast-Panjgah
- **Quarter tones** — koron (𝄳, −50¢) and sori (𝄲, +50¢) rendered on the keys
- **Four instruments** — Piano, Violin, Flute, Orchestra, all synthesized live with the Web Audio API
- **Editable bindings** — every piano key can be triggered by one *or several* computer keys
- **Per-note frequency editor** — set any note to any Hz
- **Sustain pedal**, octave shift, master volume up to 200 %
- **Zero dependencies, zero samples, zero network requests** — one HTML file does everything
- Works offline, works on desktop and mobile

## How the sounds are made

There are **no audio files**. Every note is generated in real time with `OscillatorNode`, `GainNode`, `BiquadFilterNode`, and `ConvolverNode`:

| Instrument | Technique |
|-----------|-----------|
| Piano | 6 sine partials with per-partial decay + inharmonicity + lowpass sweep |
| Violin | 3 detuned sawtooths + 5.5 Hz vibrato LFO + bandpass bow noise |
| Flute | sine + 2nd-harmonic triangle + breath noise + gentle vibrato |
| Orchestra | 4 stereo-spread sawtooths + sub-octave sine + slow filter swell |

Reverb is a **synthesized impulse response** — exponentially decaying random noise fed into a convolver. No recordings involved.

## Quick start

Just open `index.html` in any modern browser. That's it.

Or run a local server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Keyboard bindings (default)

| Bottom row | Note | Upper row | Note |
|-----------|------|-----------|------|
| `Z` | C3 | `Q` and `,` | C4 |
| `S` | C#3 | `2` | C#4 |
| `X` | D3 | `W` and `.` | D4 |
| `D` | D#3 | `3` | D#4 |
| `C` | E3 | `E` | E4 |
| `V` | F3 | `R` | F4 |
| `G` | F#3 | `5` | F#4 |
| `B` | G3 | `T` | G4 |
| `H` | G#3 | `6` | G#4 |
| `N` | A3 | `Y` | A4 |
| `J` | A#3 | `7` | A#4 |
| `M` | B3 | `U` | B4 |
| | | `I` | C5 |
| | | `O` | D5 |
| | | `P` and `]` | E5 |
| | | `[` | F5 |

- **Space** = sustain pedal
- **↑ / ↓** = shift keyboard octave
- **Esc** = release all notes

## Editing bindings

Open the **Note & frequency editor** panel at the bottom of the page:

- **Replace a binding** → click a Key button, press a key
- **Add a second binding** → click a Key button, hold **Shift**, press the extra key
- **Type bindings directly** → right-click a Key button, type e.g. `q,,` (comma-separated)
- **Change frequency** → type a new Hz value, or adjust the cents offset

All changes are saved to `localStorage`, so they survive a page reload.

## Roadmap

- [ ] MIDI input support
- [ ] Recording / playback
- [ ] Persian notation display (dastgāh-based staff)
- [ ] Optional sampled piano mode (Salamander Grand Piano)

