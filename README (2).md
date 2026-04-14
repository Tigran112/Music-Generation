# 🎵 AI Music Generation with Transformer

> Generating music using a Transformer model trained on the MAESTRO dataset

**Authors:** Harutyunyan Tigran · Meliqyan Zareh

---

## About

This project trains a Transformer model on classical MIDI files from the [MAESTRO v2.0.0](https://magenta.tensorflow.org/datasets/maestro) dataset and generates original melodies in MIDI/MP3 format.

---

## Stack

- Python 3.x
- TensorFlow / Keras
- music21
- FluidSynth + midi2audio (for MP3 conversion)
- Google Colab

---

## Quick Start

1. Open the notebook in Google Colab
2. Run all cells in order
3. After training, download `ai_project_melody.mid` or `ai_project_melody.mp3`

---

## Project Structure

```
├── ai_music_generation_fixed.py   # main code
├── best_music_model.keras         # saved model (after training)
├── note_to_int.npy                # vocabulary: note → index
├── int_to_note.npy                # vocabulary: index → note
├── ai_project_melody.mid          # generated melody
└── README.md
```

---

## Model Architecture

```
Input (sequence_length=50)
    → Embedding (n_vocab, 128)
    → Positional Encoding
    → Transformer Block × 3 (4 heads, ff_dim=256)
    → GlobalAveragePooling1D
    → Dense(256, relu)
    → Dropout(0.3)
    → Dense(n_vocab, softmax)
```

---

## Generation Parameters

| Parameter | Value | Description |
|---|---|---|
| `TEMPERATURE` | `1.0` | Sampling randomness |
| `MELODY_LENGTH` | `500` | Number of notes to generate |
| `SPEED` | `0.8` | Playback speed multiplier |
| `MIN_DURATION` | `0.5` | Minimum note duration |
| `MAX_DURATION` | `2.0` | Maximum note duration |

---

## MP3 Conversion

```python
!apt-get install -y fluidsynth
!pip install midi2audio
!wget -q "https://keymusician01.s3.amazonaws.com/FluidR3_GM.zip"
!unzip -q FluidR3_GM.zip

from midi2audio import FluidSynth
fs = FluidSynth("FluidR3_GM.sf2")
fs.midi_to_audio("ai_project_melody.mid", "ai_project_melody.mp3")
```

---

## Dataset

[MAESTRO v2.0.0](https://magenta.tensorflow.org/datasets/maestro) — ~200 hours of classical piano music in MIDI format, recorded at the International Piano-e-Competition.

---

## Лицензия

MIT License
