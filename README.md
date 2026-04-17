# jarvis-device-resideo

Resideo / Honeywell Home thermostat control via the Home API v2 for [Jarvis](https://github.com/alexberardi/jarvis-node-setup).

## Install

```bash
python scripts/command_store.py install --url https://github.com/alexberardi/jarvis-device-resideo
```

## Setup

1. Create a developer account at [developer.honeywellhome.com](https://developer.honeywellhome.com)
2. Create an app to get your Consumer Key and Consumer Secret
3. Set `RESIDEO_CONSUMER_KEY` and `RESIDEO_CONSUMER_SECRET` in Jarvis
4. Complete OAuth setup through the Jarvis mobile app to link your Honeywell Home account

## Supported Devices

- Honeywell Home Pro Series thermostats (LCC-*)
- Honeywell Home T-Series thermostats

## Actions

| Action | Params | Description |
|--------|--------|-------------|
| `set_temperature` | `temperature`, `mode`, `hold` | Set target temperature |
| `set_mode` | `mode` (Heat/Cool/Auto/Off) | Change thermostat mode |
| `turn_on` | — | Resume previous mode |
| `turn_off` | — | Turn off thermostat |
| `set_fan` | `mode` (Auto/On/Circulate) | Change fan mode |
| `resume_schedule` | — | Cancel hold, resume schedule |

### Hold Types

When setting temperature, the `hold` param controls schedule behavior:

| Hold | Behavior |
|------|----------|
| `PermanentHold` (default) | Hold until manually changed |
| `TemporaryHold` | Hold until next schedule period |
| `NoHold` | Follow schedule |
| `HoldUntil` | Hold until `nextPeriodTime` |

## Secrets

| Key | Required | Description |
|-----|----------|-------------|
| `RESIDEO_CONSUMER_KEY` | Yes | Honeywell Home API consumer key |
| `RESIDEO_CONSUMER_SECRET` | Yes | Honeywell Home API consumer secret |
| `RESIDEO_ACCESS_TOKEN` | Auto | OAuth access token (auto-populated after auth) |
| `RESIDEO_REFRESH_TOKEN` | Auto | OAuth refresh token (auto-populated after auth) |
| `RESIDEO_TEMP_UNIT` | No | Temperature unit: `F` (default) or `C` |

## Structure

```
device_families/resideo/protocol.py   # Device protocol adapter
```
