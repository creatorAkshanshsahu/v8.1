# AK TV TG Player compatibility change (v9)

## What changed
- Channel selection now opens TG TV's own `/embed/{id}` or `/v2/embed/{id}` page immediately. Native Media3 stream extraction is no longer the first playback path. This lets TG's own player run its server selection and retry logic.
- Keeps the existing bundled GeckoView engine (157.0.20260910085851) instead of Android 9's system WebView. GeckoView is a self-contained browser engine and supports Android 8+ according to Mozilla's documentation.
- Removed app-level GeckoView anti-tracking configuration so cross-origin scripts/CDN/server-selection requests are not deliberately filtered by this app.
- Bumped versionCode to 5 / versionName to 3.1-tg-embed.

## Important limitation
This source change has not been built or tested on the user's Android 9 TV box in this environment. It cannot guarantee every channel: the actual TG embed, DRM/media codec support, network/TLS, and TG's own server endpoints must work in GeckoView on the box. If it still black-screens, capture GeckoView console/network errors and TG's embed behavior on that device; do not switch back to native stream extraction if the requirement is to preserve TG's player.

## Build
Use the included GitHub Actions workflow. It builds separate arm32 and arm64 APKs; install the APK matching the TV box CPU ABI.
