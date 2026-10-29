# Sony BRAVIA 7 II (K-55XR75M2)

Google TV 14, `BRAVIA_AE3_EU`, build `UKN4.250422.001 603100`. The same board and build as
[`../sony-bravia-9-ii/`](../sony-bravia-9-ii/); this list is the same packages, applied to the 55 inch UK/EU model.

## Remote buttons with the stock launcher off

With `com.google.android.apps.tv.launcherx` disabled, the app buttons and Settings stop answering. Their scancodes
(read with `tools/tv.py 'getevent -t'`, decimal):

| Button | Scancode |
|---|---|
| YouTube | 485 |
| Netflix | 583 |
| Prime Video | 490 |
| Disney+ | 491 |
| Crunchyroll | 507 |
| Sony Pictures Core | 496 |
| Settings (gear) | 646 |
| STAR (the user-assignable macro button) | 423 |

A theme's `config.json` maps them with `InputKeyService`, which one helper covers:

```json
{
  "app_keys": [
    "scan:485:com.google.android.youtube.tv",
    "scan:583:com.netflix.ninja",
    "scan:490:com.amazon.amazonvideo.livingroom",
    "scan:491:com.disney.disneyplus",
    "scan:507:com.crunchyroll.crunchyroid",
    "scan:496:com.sonypicturescore",
    "scan:646:settings"
  ]
}
```

Install the launcher with `INPUT_KEY_SERVICE=1`. The Input key, Home and the voice button need nothing.

## Notes

- **Settings screens:** Sony's own Display & Sound screen returns empty screenshots; `uiautomator dump` still
  reads its text. Back from it lands in the Live TV app, not in Settings.
- **Screensaver path:** Settings > System > Ambient screensaver (Start now, Settings).
- **Wireless debugging port:** the TV picks a new one at every restart. `adb mdns services` shows it, and a
  server can look it up with mDNS before each connection.
