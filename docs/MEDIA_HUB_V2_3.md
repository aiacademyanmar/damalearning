# Dhamma Learning AI — Media Hub V2.3 integration guide

This is a **source manifest and implementation specification**, not a claim that the APK has been rebuilt.

## Navigation / UI
Bottom tabs: Home · TV · Video · Audio · Books; premium community link from account page.
Design: midnight teal #063A40, gold #D9A441, ivory #FFF9EC; consistent logo and accessible Myanmar labels.
- TV: PUBLIC — YouTube playlist via YouTube official player/embed, not unofficial stream extraction.
- Video: premium library grid + featured hero, search, progress/resume, fullscreen, captions, quality where supported, PiP.
- Audio: premium cassette deck and FM tuner visual skins, play/pause, seek, speed, playlists, sleep timer, background media controls.
- Books: premium PDF, EPUB, HTML native/offline-capable readers; PPTX converted server-side into PDF/page images before reading. Bookmarks, notes, zoom, font settings.
- Telegram: PREMIUM only; entitlement-checked join button. **An ordinary Telegram invite URL cannot enforce membership status:** use an admin bot, expiring invite links and removal on expiry.

## Backend architecture
1. Connect Drive with a **server-side OAuth / service account with explicitly granted folder access**. Never embed OAuth credentials or Drive files' raw sharing URLs in the APK.
2. Index folders recursively into a catalog with id, parent, title, type, mime, thumbnail, duration/page count when known, checksum, revision, access, and lastSyncedAt. Only sync files readable by the authorized integration identity.
3. API: GET /v1/media/catalog?type=&cursor=; GET /v1/media/{id}; POST /v1/media/{id}/playback-token; GET /v1/auth/entitlements; POST /v1/telegram/join-link. Enforce premium on **every** protected endpoint, including download and preview.
4. Issue short-lived, bound media playback URLs or authenticated streaming/proxy. Handle range requests and content types for Android Media3. Don't expose protected Drive items through public sharing.
5. Download premium items only through approved, authorized paths; store encrypted in app-private storage and recheck entitlement on access/renewal.
6. Convert PPTX at the server into per-page images or a PDF with caching. Preserve original PPTX in Drive.
7. UI: loading/error/empty/offline states; sync progress; thumbnails; no forced downloads of all media.

## Source folders
Video: https://drive.google.com/drive/folders/1f7tfMTouyQ5iQZPRXujApTQ8Aar6yclY
Audio: https://drive.google.com/drive/folders/1qtjVG0KZlxpSG0G_poYluIaFLU2UbK-7
Books: https://drive.google.com/drive/folders/1arcX4FjJF5-Y2z3ngCXHroYX3IbAVS5F

The Books folder was discoverable from the linked Personal Drive account and contains PPTX files. Video/Audio folder contents were not verified in the connected accounts at preparation time. Drive folder links are **source references**, not authenticated stream URLs.

## Acceptance tests
- Free account: TV works; protected lists/stream/Telegram join unavailable.
- Premium account: token checked by backend; video/audio play and seek; PDF/EPUB/HTML read; PPTX renders as slides.
- Expired premium: protected playback URLs revoke/expire, offline access obeys subscription terms, Telegram membership reconciles.
- No API secrets embedded in APK; deep links verified; error handling for missing inaccessible files.
- Android build should run only after full source ZIP is committed to the repository.

## Blocker
The current repository README states that the complete Android source ZIP is backed up on Drive and **not yet committed**. A new production APK cannot be claimed from this manifest alone.
