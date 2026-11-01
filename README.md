# Dhamma Learning AI · Native Android V1.8

Myanmar-language Dhamma Learning AI: native Kotlin/Jetpack Compose shell, offline HTML book (20 chapters, 96 images), and 1,000 draft Q&A candidates.

## Build source
The complete source ZIP is backed up to [Google Drive](https://drive.google.com/file/d/1i2vo44sgS7XigbIjCMmyYuSlzRfUtsXZ/view?usp=drivesdk).

**Note:** This repository is being bootstrapped. It does not yet contain the complete 71 MB Android source and cannot compile an APK until those files are present. Download/extract the source ZIP and copy its project contents into the repository root, then push to `main`.

Expected: `settings.gradle.kts`, `build.gradle.kts`, `app/`, `content/`, `.github/workflows/build-apk.yml`.

The Q&A entries are candidates, not expert-verified Canonical Dhamma translations. No Google Drive functionality is included inside the Android app.

## How to build
`gradle :app:assembleDebug` with JDK 17 and Android SDK 35, or use the GitHub Actions workflow after the source is committed.
