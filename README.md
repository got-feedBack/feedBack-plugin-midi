# Slopsmith Plugin: MIDI Amp Control

A plugin for [Slopsmith](https://github.com/got-feedback/feedBack) that sends MIDI Program Change messages to your guitar amp/modeler, automatically switching presets when song tones change during playback.

## Features

- **Auto-detect MIDI devices** — uses the Web MIDI API to find connected USB MIDI devices
- **Per-song tone mapping** — map each song tone to a MIDI program number (preset) on your device
- **Bank Select support** — MSB and LSB for devices with more than 128 presets
- **Channel selection** — route to any MIDI channel (0-15)
- **Test button** — send a Program Change manually to verify your mapping
- **Player integration** — "MIDI" button in the player controls opens the mapping editor for the current song
- **Auto-save** — mappings persist in SQLite, saved automatically on change

## Compatible Devices

Works with any MIDI-capable guitar amp or modeler connected via USB MIDI:

- Line 6 Helix / HX Stomp
- Kemper Profiler
- Fractal Axe-FX / FM3 / FM9
- Boss GT-1000 / GX-100
- Headrush Pedalboard
- Valeton GP-100 / GP-200 / GP-5
- Neural DSP Quad Cortex
- Any device that accepts MIDI Program Change messages

## Requirements

- **Chrome or Edge browser** (Firefox does not support Web MIDI)
- USB MIDI connection between your computer and your amp/modeler
- Some devices need a USB-to-MIDI adapter; some connect directly via USB

## Installation

```bash
cd /path/to/slopsmith/plugins
git clone https://github.com/got-feedback/feedBack-plugin-midi.git midi_amp
docker compose restart
```

## How It Works

1. Connect your amp/modeler via USB MIDI
2. Go to "MIDI" in the navigation (or click "MIDI" in the player controls)
3. Search for a song and click it
4. Each tone in the song is listed — set the MIDI channel, bank, and program number for each
5. Use the "Test" button to verify the correct preset switches on your device
6. During playback, the plugin auto-sends Program Change messages when the song's tone switches

### Mapping Example

For a song with two tones (Clean and Distortion):

| Tone | Channel | Bank MSB | Bank LSB | Program |
|------|---------|----------|----------|---------|
| Clean Verse | 0 | 0 | 0 | 3 |
| Distortion Chorus | 0 | 0 | 0 | 15 |

The exact program numbers depend on how your presets are organized on your device.

## License

MIT
