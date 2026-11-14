# P2P project state — 2026-11-14

Current shipped baseline: rc30 (66). Owner confirmed calling now works after installation. Agent validation: 101 JVM/Robolectric tests, release APK bootstrap check, signature check and bundled native/media comparison. Do not interpret one successful call as exhaustive notification/background/network verification.

## Recent history

- rc28 reconstructed an editable project after original rc27 workspace was unavailable. Its R8 build removed JNI Zero helpers and crashed on WebRTC startup.
- rc29 disabled shrinking and preserved JNI Zero bootstrap. Native startup was repaired, but call setup and Clear log regressions remained.
- rc30 restored call timing, candidate-less answer handling, audio error callbacks, safe call diagnostics and Clear log. User has now confirmed a successful call.
- Recovery documentation and manifests were added after rc30 without altering application source or the published APK.

## Product constraints to preserve

Android Kotlin/Compose app using Chatmail for encrypted messaging and WebRTC for Talk. Bottom sections: Talk, Chats, Groups, Social. Do not revert to the old no-relay experimental transport. No Firebase or companion notification app. No paid service dependency introduced without user agreement.

Settings and contacts use full pages; simple choices use bottom sheets. Persistent top navigation: contextual create, search, contacts, settings. Preserve theme consistency, readable contrast, selected font sizing, 18 color choices and opaque bubbles/cards. Buttons and bubbles have no outlines; text fields may. User backgrounds appear on full pages and main tabs, with optional 0–100% mode-colored overlay (10% default) and preview. Top/bottom bars remain solid. Do not retint image assets themselves.

Chats/groups: left/right offset bubbles, caption and attachment together, consistent padding, speaker/reaction/star controls, received reactions at bottom right, no reply-arrow feature. Feed/Gallery/Starred share Inbox/Archive/Trash styling. Conversation title has name without avatar. Bell toggles notifications. Long press bubble background offers local Delete/Cancel; text supports selection/copy. Preserve smooth swipe action backgrounds and archive/trash/block behavior.

Social: My Page/Friends/Feed, no friend count, Feed has no composer; it shows friends' posts. Preserve polished post appearance. Local delete is long press rather than X. Friends have explicit remove/mute controls. Search covers Social.

Talk: Voicemail and Call are two independent buttons, not a selected toggle. Voicemail bottom sheet lists received voicemail only, separate from chat; unread indicators direct users to it. Recent calls use time today/short date otherwise and start fresh calls. Preserve microphone mute, speaker, progress animation and genuine call-state labels. Do not sacrifice connection reliability for shorter setup delay.

Settings labels: App log, Connections, P2P address, Read aloud, Updates, Recovery. Two columns; Profile/Setup first; Updates/App log at bottom. App log includes normal activity and errors, with copy and clear controls. Only two built-in speech voices; male default. Dark mode/Cosmic Drift/purple defaults were requested. Verify existing behavior before changing; this list records user constraints, not proof every UI path was exhaustively checked.

## Outstanding work

No new application change requested in the recovery task. Do not invent a new APK. On a future bug report, reproduce narrowly against rc30 and retain working fixes. Device behavior beyond the reported successful call still needs evidence if relevant. Original pre-rc28 signing key and exact rc27 Kotlin source were not recovered; never substitute old source for this current baseline.

## Where to work

Read CONTINUE-HERE.md and REBUILD.md inside the recovery workspace. Core files: app/src/main/java/app/p2p/TalkAudio.kt, TalkCalls.kt, AppLog.kt, MainActivity.kt, P2pModel.kt. Find actual paths with rg --files if layout changes. The app/build.gradle.kts and scripts/check-call-apk.py define critical release protections.
