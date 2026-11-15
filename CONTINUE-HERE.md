# Continue P2P here

This repository and its named recovery asset are the starting point when the local workspace or chat history is unavailable. Do not ask the owner to locate source before following this procedure.

## Current baseline

- **P2P 0.7.23-rc42 (78)**, package `app.p2p.preview`, ARM64, Android 12 or later.
- The toolbar has an app-wide mute bell and consistent controls. Talk has a Clear recent button that clears local call history after confirmation and keeps voicemail.
- 113 automated tests passed, Android lint reported zero errors, and APK signature and WebRTC bootstrap checks passed.
- Call ringtone behavior and the Talk layout still need physical-device verification on rc42.
- The release repository stores documentation and downloadable assets. The named workspace recovery ZIP holds the Android source.
- Future updates must increase the version code and reuse the same signing certificate.

## Recover the workspace

1. Download **P2P-0.7.23-rc42-Workspace-Recovery.zip** from [the rc42 release](https://github.com/JustTrySomthing/P2P-Releases/releases/tag/v0.7.23-rc42). Use the named workspace recovery asset.
2. Check its SHA-256 against recovery-manifest.json in this repository. Extract it into a new directory. It contains the editable P2P Android workspace, Gradle wrapper/configuration, Rust reference sources, bundled ARM64 native libraries, wallpapers, the two speech voices, regression tests, and build/recovery documentation.
3. Run `python3 P2P/scripts/verify-recovery.py` to verify the bundled file manifest. Read P2P/AGENTS.md, P2P/REBUILD.md, and P2P/docs/PROJECT-STATE.md before editing.
4. Restore the private signing backup described below. Confirm the certificate fingerprint BEFORE producing an update.
5. Use JDK 21 (17 also supported), Gradle wrapper 8.11.1, Android SDK Platform 35, Build Tools 35.0.0. Set JAVA_HOME and ANDROID_HOME or create local.properties. First build requires Google Maven/Maven Central access; dependency caches and SDK installers are not bundled.
6. Run `./gradlew --no-daemon :app:testDebugUnitTest :app:assembleRelease` inside P2P with signing environment variables set. Run `python3 scripts/check-call-apk.py app/build/outputs/apk/release/app-release.apk` and Android apksigner verification on the ACTUAL release APK.
7. Compare resulting package/certificate with the manifest. Do not generate a replacement key, downgrade source, or require uninstall as a workaround for missing files.

## Signing recovery — private, required for upgrades

Public GitHub intentionally does not contain the key or password. The complete existing private backup is named **P2P-rc28-PRIVATE-Signing-Recovery.zip** in the owner's ChatGPT Library. Search that exact filename using the owner's connected Library; it contains p2p-release.p12, password.txt, and RECOVERY.txt. This backup was saved on 2026-11-14. Do not publish its contents or print its password.

Set P2P_KEYSTORE to the recovered .p12 absolute path, and P2P_KEY_PASSWORD to the password through a private environment variable. Alias: p2p.

Expected signing certificate SHA-256:
`39e8ffec3e664cfd6b3865aa68e8ee43f9707fc8d7bbb14248a363f093314d13`

A public certificate or fingerprint alone cannot sign updates. If private access is unavailable, source work and debug builds can continue, but a compatible release cannot be signed. Report that exact access problem; do not create another key. This arrangement depends on continued access to GitHub and the owner's private backup; it is not a promise that access can never fail.

## Preserve working behavior

- Keep code minification AND resource shrinking disabled. Preserve org.jni_zero and org.webrtc. rc28 lost JNI Zero helpers and crashed in JNI_OnLoad.
- Keep the bundled native libraries and two-voice assets; do not rebuild legacy native scripts or strip/compress/remove runtime components to reduce APK size.
- Preserve candidate-less answer handling; do not reintroduce the anonymous prepare check that caused rc19/rc29 failures.
- Full 45-second ringing window starts after offer preparation. Accepted calls get 30 seconds for connection. Keep audio failure handling, safe diagnostics, and Clear log.
- Do not shorten ICE gathering or alter call routing simply to reduce the startup wait. Reliability was explicitly prioritized.
- Preserve package, signing key, stored account/data compatibility, update asset naming, and version-code monotonicity.

## Every future work session / release

- Start from this guide and latest recovery-manifest.json. Read PROJECT-STATE before acting.
- Before ending a session with changes, save a named source/recovery checkpoint to GitHub, including work-in-progress status if no APK is released. A local commit alone is not a remote backup.
- For every APK publish the matching complete workspace recovery asset, hashes, version/package/certificate, build instructions, validation results, and completed/pending work. Update this guide, manifest and README together.
- Verify uploaded asset hashes and that the source archive contains wrapper, Kotlin source, native libraries and media. Record actual tests separately from user reports.
- Keep the private key backup available, unchanged, and separately protected. Never publish credentials, passwords, private identities/messages, local configuration or account databases.
- Preserve previous recovery checkpoints; do not silently overwrite an earlier release's source with later code.

