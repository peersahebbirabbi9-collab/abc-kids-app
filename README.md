# ABC Kids 🎈 — Alphabet Learning App

A colorful, simple Flutter app that teaches kids (ages 4-6) the alphabet A-Z with:
- 🔊 **Spoken sounds** for every letter and word (via built-in text-to-speech — no audio files needed)
- 🖼️ **Pictures** for every letter (emoji-based, so the app stays lightweight)
- ⭐ **Progress tracking** — saves which letters a child has viewed, with a progress bar
- 🎉 **Confetti celebration** as they move through letters
- 👆 **Swipe navigation** between letters, or tap any letter from the home grid

## Project Structure
```
alphabet_app/
├── lib/
│   ├── main.dart                     # App entry point
│   ├── models/letter_data.dart       # A-Z data: letter, word, emoji, color
│   ├── screens/home_screen.dart      # Grid of all 26 letters + progress
│   ├── screens/letter_detail_screen.dart  # Full-screen letter view w/ TTS
│   └── widgets/letter_card.dart      # Single letter tile
├── android/                          # Android platform files (ready to build)
└── pubspec.yaml                      # Dependencies
```

## How to Run This (Step by Step)

### 1. Install Flutter
If you don't have Flutter installed yet:
- Go to https://docs.flutter.dev/get-started/install
- Follow the instructions for your OS (Windows/Mac/Linux)
- Run `flutter doctor` in your terminal to confirm everything is set up

### 2. Get the project running
```bash
cd alphabet_app
flutter pub get
flutter run
```
This will launch the app on a connected Android device or emulator.

### 3. Open in Android Studio (recommended)
- Open Android Studio → **Open** → select the `alphabet_app` folder
- Let it index and sync Gradle
- Click the green ▶️ Run button

## Before You Publish to Play Store

There are a few things you **must** change — they're marked with `TODO` comments in the code:

### A. Change the Application ID
In `android/app/build.gradle`, change:
```gradle
applicationId "com.yourcompany.alphabet_kids"
```
to something unique to you, e.g. `com.johndoe.abckids`. This ID **cannot be changed after publishing**, so pick carefully.

### B. Add Your Own App Signing Key
Right now the app uses the default debug signing key, which **cannot be uploaded to Play Store**. You need to:
1. Generate a keystore:
   ```bash
   keytool -genkey -v -keystore ~/upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
   ```
2. Create `android/key.properties`:
   ```
   storePassword=<your password>
   keyPassword=<your password>
   keyAlias=upload
   storeFile=<path to upload-keystore.jks>
   ```
3. Update `android/app/build.gradle`'s `signingConfigs` to reference it (Flutter's official docs have the exact snippet: https://docs.flutter.dev/deployment/android)

### C. Add a real app icon
Replace the default Flutter icon in `android/app/src/main/res/mipmap-*` folders. Easiest way: use the `flutter_launcher_icons` package — add your 512x512 PNG icon and run one command to generate all sizes.

### D. Build the release bundle
```bash
flutter build appbundle
```
This creates `build/app/outputs/bundle/release/app-release.aab` — this is the file you upload to Play Console.

### E. Play Console Setup
1. Create a developer account at https://play.google.com/console (one-time $25 fee)
2. Create a new app → fill in store listing (title, description, screenshots)
3. Upload the `.aab` file under **Production → Create new release**
4. Since this app targets children, complete Google's **Target Audience and Content** section honestly — this affects required compliance (Families Policy, ads restrictions, data collection rules)
5. Submit for review

## Ideas for v2 (easy additions later)
- Add simple tap-to-trace letter writing practice
- Add a quiz mode ("Tap the letter that says... 🍎")
- Add background music toggle
- Add multiple language support (e.g., Kannada script letters)

## Notes
- No internet permission is required — everything works offline.
- Text-to-speech uses the device's built-in engine, so no audio asset files are bundled (keeps app size small).
