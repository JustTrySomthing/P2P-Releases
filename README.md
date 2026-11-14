# P2P for Android

**[Download the latest APK — 0.7.23-rc30](https://github.com/JustTrySomthing/P2P-Releases/releases/download/v0.7.23-rc30/P2P-0.7.23-rc30-ARM64-Preview.apk)**

Version **0.7.23-rc30 (66)** · ARM64 · Android 12 or later · 141 MB

**Update directly over rc28 or rc29—do not uninstall.** The signing key is unchanged and app data is preserved. Users on rc27 or earlier need the one-time clean install introduced by rc28.

Restores **Clear log**, the full ringing window after offer preparation, the 30-second connection allowance, audio-error handling, and detailed call diagnostics. Preserves WebRTC/JNI Zero startup protection. Code/resource shrinking remains disabled. Only the same two built-in voices are included.

101 automated tests passed. Release APK bootstrap and signature checks passed. **The owner confirmed calling works on rc30 on November 14, 2026.** Broader device behavior is not exhaustively tested.

[Release notes and APK checksum](https://github.com/JustTrySomthing/P2P-Releases/releases/tag/v0.7.23-rc30)

## Continue or recover development

**[START HERE — complete project recovery instructions](CONTINUE-HERE.md)**

[Download the matching workspace](https://github.com/JustTrySomthing/P2P-Releases/releases/download/v0.7.23-rc30/P2P-0.7.23-rc30-Workspace-Recovery.zip) · [Current project state](PROJECT-STATE.md) · [Recovery hashes and signing fingerprint](recovery-manifest.json)

The named workspace includes editable source, bundled native libraries, wallpapers, two voices, Gradle configuration/wrapper, tests, build instructions, and an integrity checker. GitHub’s automatic “Source code” archives are not the Android workspace.

Signing credentials are protected in a separate private backup, with exact retrieval instructions in the guide. Future updates must reuse that key. Recovery documentation was added without changing the working APK.
