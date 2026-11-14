# P2P continuity rules

Before any project work, read CONTINUE-HERE.md and recovery-manifest.json. This repository's named release recovery ZIP contains the Android workspace; GitHub's automatic source archive is not the app source.

Follow the handoff to restore source and private signing backup without asking the owner to find files that are already recorded. Never generate a replacement key to solve a missing-workspace problem. Preserve app.p2p.preview, the recorded certificate and increasing versionCode. Never publish private keys/passwords or account data.

Keep release minification/resource shrinking disabled, preserve WebRTC/JNI Zero, and validate the ACTUAL signed APK with scripts/check-call-apk.py. Do not discard working call fixes to reduce size or setup delay.

Every completed work session with changes needs a remote source checkpoint and updated status. Every published APK needs matching source/recovery asset, checksums, build instructions and validation. Update README, CONTINUE-HERE and recovery-manifest together. Verify uploads; a local Git commit does not constitute a remote backup. Preserve earlier recovery checkpoints.

Record automated results, user device reports and unresolved issues separately. The owner confirmed rc30 calling works on 2026-11-14. Do not claim comprehensive device testing from that one report.
