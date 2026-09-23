# RustDesk iOS

Lean build-only fork of [rustdesk/rustdesk](https://github.com/rustdesk/rustdesk) containing
**only the source needed to build the iOS ipa** (Rust core + Flutter iOS app + CI).

## What's included

- `src/`, `libs/`, `res/` — Rust core (compiled for `aarch64-apple-ios`)
- `flutter/` — Flutter app, iOS-only subset (`lib`, `ios`, `macos`, `assets`)
- `.github/workflows/` — `ios-only-build.yml` (manual trigger, single macOS job) + `bridge.yml`

## Customizations

- iOS remote-control and camera-view toolbars hide the chat button (`isWeb || isIOS` in
  `flutter/lib/mobile/pages/remote_page.dart` and `view_camera_page.dart`).
- The ipa is packaged manually from `flutter build ios` output because this repo's
  `exportOptions.plist` targets App Store signing, which makes `flutter build ipa --no-codesign`
  produce only an xcarchive.

## Build the ipa

```bash
gh workflow run ios-only-build.yml
```

or via the Actions tab → "iOS Only Build" → "Run workflow".

The unsigned `rustdesk-ios-1.5.0.ipa` (~27 MB) is uploaded as a workflow artifact.
Install on a device with a free Apple ID (re-sign every 7 days) or a paid developer account.

## License

[AGPL-3.0](LICENCE) — same as upstream rustdesk.
