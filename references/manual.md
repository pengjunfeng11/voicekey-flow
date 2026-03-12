# VoiceKey Flow Manual

This manual documents how to connect `DJI Mic Mini` to macOS and use `Karabiner-Elements` to map the Mic Mini button for `Typeless` or dictation workflows.

## Recommended software

- `Karabiner-Elements`
- Recommended version: `v15.9.0`
- Download page: <https://karabiner-elements.pqrs.org/>
- Installation guide: <https://karabiner-elements.pqrs.org/docs/getting-started/installation/>
- Release notes: <https://karabiner-elements.pqrs.org/docs/releasenotes/>

## Key paths

Karabiner config:

```text
~/.config/karabiner/karabiner.json
```

Karabiner logs:

```text
~/.local/share/karabiner/log/
```

## Validated device identifiers

- Name may appear as `DJI Mic Mini` or similar suffixed variants
- `is_consumer: true`
- `vendor_id: 11427`
- `product_id: 16401`

## Validated button event

```json
{
  "consumer_key_code": "volume_increment"
}
```

## Minimal test rule

Use this first to verify the Mic Mini event is capturable:

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

## Bound rule example

Use this once the test rule succeeds:

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

## Recommended setup order

1. Pair `DJI Mic Mini` with the Mac.
2. Install `Karabiner-Elements`.
3. Grant the required permissions in macOS.
4. Open `Karabiner-EventViewer`.
5. Press the Mic Mini button and confirm the event appears.
6. Test with a simple output such as `a`.
7. Add device binding with `vendor_id` and `product_id`.
8. Replace the test output with the user's Typeless or dictation shortcut.

## Limitations

- Single press is the most reliable interaction.
- Double-click may trigger bluetooth pairing on the device.
- Long press may not be reported to macOS as a stable hold event.
- If `fn` does not work in the user's workflow, map to a standard shortcut combination instead.
