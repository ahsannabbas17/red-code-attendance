# Red Code Attendance

Phone-first attendance app for Red Code Developers. It includes an Android app build and a shared Node.js API with live updates for employee check-ins, requests, and administrator changes.

## Android APK

The Android app targets Android API 24 and later. APK builds require a public HTTPS shared API URL and Android/JDK build tools. Set the GitHub repository variable `RED_CODE_API_URL` to a URL ending in `/api`, then run the **Android APK** workflow. The resulting test APK is available from its workflow artifact.

For a local build, install Node.js 22+, Android Studio with Android SDK Platform 36 and Build Tools 35.0.0, and JDK 21. Then run:

```powershell
$env:RED_CODE_API_URL = 'https://attendance.example.com/api'
npm ci
npm run android:debug
```

The file is written to `android/app/build/outputs/apk/debug/app-debug.apk`. A debug APK is intended for testing; production distribution needs a protected, persistent release signing key.

## Shared server

GitHub stores source and builds APKs; it does not run the attendance API. Deploy `server.mjs` as one always-on Node service with persistent storage and HTTPS. Set a unique `ADMIN_PASSWORD` of at least 16 characters, `ADMIN_USER`, `NODE_ENV=production`, `DATA_DIR`, and `APP_ORIGINS=https://localhost`. Keep the service on a single instance so its JSON database and live event stream remain consistent. See [the full setup guide](outputs/README.md).

## App details

- Android package: `com.redcode.attendance`
- Android minimum: API 24 (Android 7.0)
- Target SDK: API 36
- Developer: AHSAN ABBAS
