# বাকির হিসাব (Baki Khata)

A simple, offline **credit ledger app for small shops**, built for Bangladeshi shopkeepers. Record who owes you how much, log payments, and see old dues at a glance. It is a single-page web app (HTML/CSS/JS) wrapped in an Android `WebView`, so there is no backend and no account: all data stays on the phone.

> দোকানের বাকির খাতা, এখন মোবাইলে। কোনো ইন্টারনেট বা অ্যাকাউন্ট লাগে না।

## Features

- **Customer ledger**: add credit (baki) and payment entries per customer, with date and note
- **Smart due calculation**: payments are applied to the oldest credit first (FIFO)
- **Dashboard**: total due, today's collection, number of customers with dues
- **Monthly reminders** for credits older than 30 days
- **Search** customers by name, call them with one tap
- **Bangla / English** toggle and **light / dark** theme
- **PIN app lock**: 4-digit PIN, auto-lock when you leave the app, attempt limiting, and a recovery code
- **Works fully offline**, including the Hind Siliguri Bangla font bundled inside the app

## Tech stack

| Part | Details |
|------|---------|
| UI | Vanilla HTML, CSS, JavaScript (single `index.html`) |
| Storage | Browser `localStorage` inside the WebView |
| Android | Java, `WebView`, Gradle (AGP 8.5.2, Gradle 8.7) |
| SDK | minSdk 26 (Android 8.0), targetSdk 34 |
| Font | Hind Siliguri (bundled, offline) |

## Project structure

```
baki-hisab-android/
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/fahim/bakihisab/MainActivity.java
│       ├── assets/
│       │   ├── index.html          # the whole app UI + logic
│       │   └── fonts/              # offline Bangla font files
│       └── res/                    # app name, theme, launcher icon
├── build.gradle
├── settings.gradle
└── gradle/wrapper/
```

## Build and run

**Requirements:** Android Studio (recent version) and internet for the first Gradle sync.

1. Clone the repo into a folder whose path contains **only English characters** (for example `G:\baki-hisab-android`). Non-ASCII paths break the Android build on Windows.
   ```bash
   git clone https://github.com/samifahim07/baki-hisab-android.git
   ```
2. Open Android Studio, choose **Open**, and select the cloned folder.
3. Let Gradle sync finish (install any missing SDK when asked).
4. Run on an emulator or a USB-connected phone with the green **Run** button, or build an APK from `Build > Generate App Bundles or APKs > Generate APKs`.
5. The debug APK is created at `app/build/outputs/apk/debug/app-debug.apk`.

You can also download a ready-made APK from the [Releases](../../releases) page.

## PIN lock: how it works and its limits

- The PIN is stored only as a salted, iterated SHA-256 hash, never as plain text.
- After 5 wrong attempts the app makes you wait, and the wait grows with further mistakes.
- When you set a PIN the app shows a one-time **recovery code**. Write it down: it is the only way to reset a forgotten PIN.
- This is an **app-level lock to keep casual snoopers out**. The ledger data itself is not encrypted, so clearing the app's data or uninstalling the app permanently deletes all records. Keep a backup if the data matters.

## Roadmap

- [ ] Backup and restore (export / import JSON)
- [ ] Release-signed APK for Play Store
- [ ] Optional SMS reminder to customers

## Author

**Fahim Abrar Chowdhury**
Computer Science and Engineering, East West University
GitHub: [@samifahim07](https://github.com/samifahim07)

## License

Add a license of your choice (for example MIT) before sharing the project publicly.
