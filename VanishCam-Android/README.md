# VanishCam for Android (mobile port)

This is an Android WebView wrapper around a mobile adaptation of the actual VanishCam source in the supplied repository ZIP.

## Implemented in this Android port

- Front-camera preview, mirrored like a selfie camera.
- Normal Vanish: V-sign detection, background calibration, person-mask dissolve.
- Naruto Vanish: joined-hands trigger, smoke animation, supplied wooden-log sprite, and supplied vanish sound.
- Capture-background, vanish-now, and reappear controls.
- Camera frames and effects are processed locally in the WebView. No video recording or upload is implemented.

## Important source-repository discrepancy

The supplied ZIP's README describes Particles and Goku modes, but the runnable `vanish_cam.py` actually exposes only `normal` and `naruto`. `run3.py` is a separate meme/pose tracker and is not those missing modes. This mobile port therefore does not claim to implement Particles or Goku.

## First launch requirements

- Android 8.0 (API 26) or newer.
- Camera permission.
- Internet access on first launch to load MediaPipe Tasks Vision from jsDelivr and the selfie-segmentation model from Google Cloud Storage. The included hand landmark task and Naruto visual/audio assets are packaged inside the app.
- Use a device with a reasonably capable CPU; the vision pipeline is configured for CPU inference to maximize compatibility.

## Build the APK

Open this folder in Android Studio and let Gradle sync, then select **Build > Build Bundle(s) / APK(s) > Build APK(s)**.

Or build from a machine with Java 17, Android SDK Platform 36, and Gradle 8.13:

```bash
gradle --no-daemon assembleDebug
```

The debug APK is created at:

`app/build/outputs/apk/debug/app-debug.apk`

## Build using GitHub Actions

Push this project to a GitHub repository. The included workflow `.github/workflows/build-apk.yml` runs on push or can be started manually from the repository's **Actions** tab. Download the `VanishCam-debug-apk` artifact from the completed workflow run.

## Technical notes

This is a mobile adaptation, not a binary repackaging of the desktop Python program. Android does not provide the desktop OpenCV window, keyboard controls, or OBS/Unity virtual-camera backend. The app uses WebView's secure local asset origin for browser camera access and runs MediaPipe Tasks in the WebView.
