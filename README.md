# Slopsmith Plugin: MIDI Amp Control

A plugin for [Slopsmith](https://github.com/got-feedback/feedback) that sends MIDI Control Change (CC) or Program Change (PC) messages to your guitar amp/modeler, automatically switching presets when song tones change during playback.

## Features

- **Auto-detect MIDI devices** — uses the Web MIDI API to find connected USB MIDI devices
- **Per-song tone mapping** — map each song tone to a message for your device
- **CC or PC per tone**: each mapping sends either a Control Change (**CC**, the default: CC number + value) or a Program Change (**PC**: the value is the program number)
- **Bank Select support** — for PC mappings, MSB and LSB for devices with more than 128 presets. Bank Select is only sent when MSB or LSB is non-zero
- **Optional second CC**: each mapping can also send one extra CC (`CC2#` + `CC2 Value`) on the same tone change, whatever the type
- **Channel selection** — route to any MIDI channel (0-15)
- **Test button** — send a CC or PC manually to verify your mapping
- **Player integration** — "MIDI" button in the player opens the mapping editor for the current song. In the v3 UI it sits in the **Plugin controls** popover on the player rail
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
- Any device that accepts MIDI CC or Program Change messages

## Requirements

- **Chrome or Edge browser** (Firefox does not support Web MIDI)
- USB MIDI connection between your computer and your amp/modeler
- Some devices need a USB-to-MIDI adapter; some connect directly via USB

## Installation

```bash
cd /path/to/slopsmith/plugins
git clone https://github.com/got-feedback/feedback-plugin-midi.git midi_amp
docker compose restart
```

## How It Works

1. Connect your amp/modeler via USB MIDI
2. Go to "MIDI" in the navigation (or click "MIDI" in the player controls)
3. Search for a song and click it
4. Each tone in the song is listed. Pick the **Type** (CC or PC), then set the channel and the **Value**. For CC, also set the **CC#**. For PC, the **MSB** and **LSB** bank fields appear
5. Use the "Test" button to verify the correct preset switches on your device
6. During playback, the plugin sends the mapped message when the song's tone switches

### Mapping Example

For a song with two tones (Clean and Distortion), switching presets with Program Change:

| Tone | Type | Channel | Bank MSB | Bank LSB | Value |
|------|------|---------|----------|----------|-------|
| Clean Verse | PC | 0 | 0 | 0 | 3 |
| Distortion Chorus | PC | 0 | 0 | 0 | 15 |

Or with Control Change (the CC number and values here are only an example):

| Tone | Type | Channel | CC# | Value |
|------|------|---------|-----|-------|
| Clean Verse | CC | 0 | 69 | 0 |
| Distortion Chorus | CC | 0 | 69 | 1 |

The exact CC and program numbers depend on your device and how your presets are organized on it.

## License

MIT
