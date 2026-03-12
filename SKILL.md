---
name: voicekey-flow
description: Use when the user wants to connect DJI Mic Mini with Typeless or a macOS dictation workflow, map the Mic Mini bluetooth button in Karabiner-Elements, diagnose button events, or build a voice-to-text shortcut flow for faster office input. Trigger this whenever the user mentions DJI Mic Mini, Typeless, Karabiner, dictation hotkeys, voice typing, hardware button mapping, or improving typing efficiency with speech input.
---

# VoiceKey Flow

Use this skill to turn `DJI Mic Mini` into a voice-input trigger for `Typeless` or a macOS dictation workflow.

This skill is for the workflow, not just the device. The goal is to help the user:

- connect `DJI Mic Mini` to macOS
- identify what button event the Mic Mini exposes
- bind that event in `Karabiner-Elements`
- connect the button press to a speech-to-text or dictation shortcut
- avoid unstable mappings such as device-side double click or long press

## When to use this skill

Use this skill whenever the user is trying to:

- map a `DJI Mic Mini` button on macOS
- combine `DJI Mic Mini` with `Typeless`
- configure `Karabiner-Elements` for voice input
- trigger dictation or voice-to-text from a hardware key
- debug why a bluetooth media/headset button is not mapping correctly

## Workflow

1. Confirm the user is on macOS and has `DJI Mic Mini`, `Karabiner-Elements`, and either `Typeless` or a dictation shortcut available.
2. Check whether the Mic Mini button is visible in `Karabiner-EventViewer`.
3. Determine whether the event is `consumer_key_code` or `key_code`.
4. Start with a minimal mapping without `device_if` to confirm the event is capturable.
5. Once the event works, bind it to the Mic Mini device using its Karabiner-visible identifiers.
6. Map the button to the user's real target:
   - a Typeless shortcut
   - a macOS dictation shortcut
   - or a temporary test key such as `a`
7. Warn about device-side hardware limits before suggesting double-click or long-press behavior.

## Known device facts

For the validated Mic Mini device used in this workflow:

- Device name may appear as `DJI Mic Mini` or a suffixed variant such as `DJI Mic Mini-7FB415`
- Karabiner-visible device identifiers:
  - `is_consumer: true`
  - `vendor_id: 11427`
  - `product_id: 16401`
- Verified button event:
  - `consumer_key_code: volume_increment`

## Recommended debugging order

1. Open:

```text
/Applications/Karabiner-EventViewer.app
```

2. Press the Mic Mini bluetooth button and confirm whether any event appears.
3. If an event appears, record whether it is a `consumer_key_code` or a `key_code`.
4. Use a minimal test rule first:

```json
{
  "description": "test volume_increment to a",
  "manipulators": [
    {
      "type": "basic",
      "from": {
        "consumer_key_code": "volume_increment"
      },
      "to": [
        {
          "key_code": "a"
        }
      ]
    }
  ]
}
```

5. Only after the test succeeds, add `device_if`.

## Stable mapping pattern

Use this pattern to bind the Mic Mini button to a target key such as `fn`:

```json
{
  "description": "DJI Mic Mini: volume_increment -> Fn",
  "manipulators": [
    {
      "type": "basic",
      "conditions": [
        {
          "type": "device_if",
          "identifiers": [
            {
              "is_consumer": true,
              "vendor_id": 11427,
              "product_id": 16401
            }
          ]
        }
      ],
      "from": {
        "consumer_key_code": "volume_increment"
      },
      "to": [
        {
          "key_code": "fn"
        }
      ]
    }
  ]
}
```

If `fn` is not honored by the host workflow, prefer mapping to a normal shortcut combination instead of insisting on `fn`.

## Hardware limits to call out

Do not overpromise on gesture logic for this device.

- Double-click may trigger the Mic Mini's own bluetooth pairing behavior.
- Long press may not be exposed to macOS as a stable held-down input.
- For this device, single-press mappings are the safest recommendation.

If the user needs "dictate" and "submit" in one workflow, prefer:

- Mic Mini single press for dictation trigger
- another keyboard shortcut for `Enter`

## Reference

If the user needs the full step-by-step setup and troubleshooting guide, read:

- `references/manual.md`
