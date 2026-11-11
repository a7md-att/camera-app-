# Native Camera Pro (Android Camera2 API Project)

This is a native Android application (`com.rawcam.nativepro`) written in **Kotlin** using Android's low-level **`android.hardware.camera2`** and **`MediaRecorder`** APIs to replicate **Native Camera (`com.rawcam.app`)**.

## Core Features Implemented
1. **ISP Post-Processing Bypass (`RAW ISP: ON`)**:
   - Sets `CaptureRequest.EDGE_MODE_OFF` to strip away stock digital sharpening halos.
   - Sets `CaptureRequest.NOISE_REDUCTION_MODE_MINIMAL` (or `OFF`) to prevent waxy temporal smoothing.
   - Includes hardware capability checks (`CameraCharacteristics`) so devices like the **Samsung Galaxy A16** fall back gracefully if a specific ISP flag is locked by OEM firmware.
2. **Custom High Bitrates & Framerates**:
   - Record H.264 `.mp4` at **20 Mbps, 50 Mbps, 80 Mbps, or 120 Mbps** at **24, 30, or 60 FPS**.
3. **Single-Page Manual Controls**:
   - Real-time manual **ISO** (`SENSOR_SENSITIVITY`) + **Boosted ISO**, **Shutter Speed** (`SENSOR_EXPOSURE_TIME` from `1/24s` to `1/2000s`), **Manual Focus** (`LENS_FOCUS_DISTANCE`), and **White Balance Lock** (`CONTROL_AWB_LOCK`).
4. **Pro Audio Routing**:
   - Switches between `MediaRecorder.AudioSource.UNPROCESSED` (raw mic feed without aggressive AGC) and `CAMCORDER` at **48 kHz / 320 kbps Stereo AAC**.
5. **Direct Scoped Storage Output**:
   - Saves all footage directly to `DCIM/NativeCamera/` on Android 10–15 without cloud accounts or tracking.

---

## How to Get Your `.apk` File (2 Fast Ways)

### Option A: Zero-Install Cloud Build via GitHub Actions (~90 Seconds)
If you don't want to install Android Studio (which is several gigabytes):
1. Create a new repository on GitHub and upload the contents of this folder.
2. Click the **Actions** tab in your GitHub repository -> **Build Native Camera Pro APK** -> **Run workflow**.
3. Once it finishes (~90 seconds), download **`NativeCameraPro-debug-apk`** from the **Artifacts** section, extract `app-debug.apk`, and install it on your phone.

### Option B: Local Build on Your PC (Android Studio or Command Line)
1. Open this folder in **Android Studio** -> wait for Gradle Sync -> click **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
2. Your installable APK will be generated at:
   `app/build/outputs/apk/debug/app-debug.apk`
