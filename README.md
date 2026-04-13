# 🎼 The Orchestra

> **Conduct a full 3D orchestra with your hand. No plugins. No installs. Pure browser magic.**

## ✨ Live Demo

https://theorchestra.netlify.app

## 🎬 What It Is

A fully interactive 3D concert hall where **you are the conductor**. Move your cursor or raise your hand to the webcam, and 16 tuxedo-dressed musicians react in real time — swaying, bowing, leaning forward as the music builds.

Three ways to experience it:

| Mode | How |
|---|---|
| 🖱️ **Cursor Conducting** | Move mouse — speed = volume, position = which section plays |
| ✋ **Hand Conducting** | MediaPipe skeleton tracks your fingers — gesture controls the orchestra |
| 🎼 **Orchestra Mode** | Choose from 4 synthesized classical pieces and watch musicians perform |

## 🎮 How to Conduct

### Cursor Mode
| Action | Effect |
|---|---|
| Move fast | Loud, energetic — musicians lean forward |
| Move slow | Soft, gentle — musicians settle back |
| Stop moving | Complete silence — everyone freezes |
| Top-left | Strings section solos |
| Top-right | Woodwind section solos |
| Bottom-left | Brass section solos |
| Bottom-right | Percussion triggers |
| Center | All sections together |

### Hand Mode (✋ button, top-left)
| Gesture | Section | Effect |
|---|---|---|
| ✊ Fist | — | Complete silence |
| ☝️ 1 finger | Strings | Violins play softly |
| ✌️ 2 fingers | + Woodwind | Clarinets join |
| 🤟 3 fingers | + Brass | Horns join |
| 🖐️ Open hand | Full orchestra | Everything plays loud |
| Hand higher | — | Louder |
| Hand lower | — | Softer |

### Orchestra Mode (🎼 button, top-right)
Click to open the track panel and select a synthesized classical piece:
- **Symphony No. 5 · I** — Beethoven · Allegro con brio
- **Symphony No. 7 · II** — Beethoven · Allegretto
- **Eine Kleine Nachtmusik** — Mozart · Allegro
- **Eroica · I** — Beethoven · Allegro con brio

Musicians automatically animate to the beat energy of the music.

---

## 🏗️ Architecture

Built in **4 phases**, each building on the last:

```
Phase 1 — The Hall
  └─ Three.js concert hall: columns, balconies, chandelier, curtains, lighting

Phase 2 — The Musicians  
  └─ 16 dressed figures in semicircle: strings, woodwind, brass, percussion
     Each musician has: tuxedo, instrument, music stand, idle animations

Phase 3 — The Music Engine
  └─ Web Audio API synthesizer: 4 orchestral voices
     Chord progression: D minor → F major → C major → A minor
     Cursor velocity → volume + tempo mapping

Phase 4 — Hand Conducting
  └─ MediaPipe Hands: 21-point skeleton, finger counting
     Gestures → section selection + volume control
```

---

## 🛠️ Tech Stack

| Technology | Used For |
|---|---|
| **Three.js r128** | 3D concert hall, 16 musician figures, lighting, shadows |
| **Web Audio API** | Synthesized orchestral music — no audio files needed |
| **MediaPipe Hands** | Real-time hand skeleton tracking via webcam |
| **Canvas 2D API** | Camera preview with skeleton overlay |
| **Vanilla JS** | Everything else — no framework |

**Zero dependencies to install.** Everything loads from CDN or is self-contained.

---

## 🎵 Music Engine

All music is **synthesized in real-time** using Web Audio API oscillators — no MP3 files, no external APIs, works completely offline (cursor mode).

```
Strings   → Detuned sawtooth oscillators (±3 cents) → warm shimmer
Woodwind  → Sine + triangle mix → breathy clarity  
Brass     → Square wave through lowpass filter → horn buzz
Percussion→ Filtered noise burst + pitch drop → timpani hit
```

Chord progression cycles every 3 seconds:
```
D minor → F major → C major → A minor → repeat
```

---

## 📁 File Structure

```
orchestra-phase4-final.html   ← Main application (single file, ~75KB)
START_ORCHESTRA.bat            ← Windows double-click launcher
START_ORCHESTRA.sh             ← Mac/Linux launcher
README.md                      ← This file
```



## 🖥️ Browser Compatibility

| Browser | Cursor Mode | Orchestra Mode | Hand Tracking |
|---|---|---|---|
| Chrome 115+ (HTTP) | ✅ | ✅ | ✅ |
| Chrome (file://) | ✅ | ✅ | ⚠️ Load CDN scripts then works |
| Firefox | ✅ | ✅ | ✅ |
| Edge | ✅ | ✅ | ✅ |
| Safari | ✅ | ✅ | ⚠️ Limited MediaPipe support |

> **Recommended:** Chrome over HTTP (use the provided launcher scripts)

---

## 🎨 Design Decisions

**Why a single HTML file?**  
Zero setup for judges. Download → double-click → it works. No npm, no build step, no missing dependencies.

**Why synthesized music instead of MP3s?**  
No CORS issues, works offline, infinite length, responds to tempo changes in real time.

**Why motion detection fallback?**  
MediaPipe requires HTTP. The pixel-diff fallback ensures the feature degrades gracefully to still work from `file://`.

**Why 16 musicians instead of 80?**  
Quality over quantity. Each figure is individually detailed with tuxedo, instrument, and section-specific animations. 16 well-crafted figures look more impressive than 80 blocks.

---

## 👩‍💻 Built By

**Arya**   

---

## 📜 Credits

- **Three.js** — MIT License
- **MediaPipe Hands** — Apache 2.0 (Google)
- Classical music pieces referenced: Beethoven, Mozart (all public domain compositions)
- Synthesized performances generated in-browser — original recordings

