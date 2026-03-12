# VoiceKey Flow

`VoiceKey Flow` is a Codex skill project for connecting `DJI Mic Mini` with `Typeless` or a macOS dictation workflow.

It is designed to improve office input efficiency by turning a hardware microphone button into a reliable voice-to-text trigger.

## What this project does

- identifies the button event exposed by `DJI Mic Mini`
- uses `Karabiner-Elements` to map that event
- binds the mapping to `Typeless` or dictation shortcuts
- documents the stable path and the device-side limitations

## Core scenario

The skill is built for workflows such as:

1. press the Mic Mini button
2. start voice-to-text or dictation
3. speak instead of typing
4. finish input faster in chat, notes, or office tools

## Files

- `SKILL.md`: trigger description and execution workflow
- `references/manual.md`: detailed setup, installation, IDs, and troubleshooting

## Verified device facts

- Device family: `DJI Mic Mini`
- `vendor_id`: `11427`
- `product_id`: `16401`
- button event: `consumer_key_code: volume_increment`

## Notes

This project intentionally documents that double-click and long-press behaviors are not reliable on this device, because the hardware itself may consume those gestures.
