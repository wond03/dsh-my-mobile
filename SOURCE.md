# DSH Mobile Community — source branch

This branch contains the complete plugin source (TypeScript), build scripts and the
Android app source. The `main` branch keeps the built `lib/` distribution and the
Android release source.

## Build the plugin
```bash
npm install
npm run build
```

## Build the Android app
```bash
cd apps/mobile/android
./gradlew :app:assembleDebug   # com.dshmobile.community.debug
```
Release signing needs a private keystore; see the main README.

## Community changes
- The mobile admin API requires a live DSH session for every method.
- No personal domain or server address is hardcoded.
- Pairing links show the target origin and require confirmation.
- The mobile control panel is full-screen with an advanced-settings toggle.
- The app reconnects immediately when it returns to the foreground.
- The simple panel keeps the App download entry visible and points it at this repository's APK, not the upstream release.
- Release metadata and download URLs follow the community repository's `community-v*` tags.

## Attribution
Forked from [saya-ch/dsh-mobile](https://github.com/saya-ch/dsh-mobile), Apache-2.0.
