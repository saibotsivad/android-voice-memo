# Android Voice Memo

Very simple Android app that records audio and posts the recording and/or transacript to your own API.

## Audio Recording

From in the app you can click a very large button to easily start recording audio.

The file is saved to a configurable folder, defaulting to a folder named "VoiceMemo" placed in the users home directory.

## Post-Recording Action

You can add a single action to take after a recording is stopped, which is to post the recording to an AWS S3 bucket.

## Configuration

There are not many things to configure:

- Where to save the local recording. By default it saves to the user's "Documents" folder, in a sub-folder named "VoiceMemo".
- Give it an S3 bucket URL and IAM credentials to push audio files to after recording is complete.

## Project Structure

- Android application built with Kotlin and Jetpack Compose
- Uses Material Design 3 for UI components
- Target Android API 36+ (Android 15+)
- Single Activity architecture with Compose UI

```
android-voice-memo/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/saibotsivad/androidvoicememo/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   └── ui/theme/
│   │   │   │       ├── Color.kt
│   │   │   │       ├── Theme.kt
│   │   │   │       └── Type.kt
│   │   │   ├── res/
│   │   │   │   ├── values/
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   ├── xml/
│   │   │   │   │   ├── backup_rules.xml
│   │   │   │   │   └── data_extraction_rules.xml
│   │   │   │   └── mipmap-*/
│   │   │   │       └── launcher icons
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   └── build.gradle.kts
├── gradle/
│   └── libs.versions.toml
├── build.gradle.kts
├── settings.gradle.kts
├── CLAUDE.md
├── PRP.md
├── README.md
└── TODO.md
```

## Development Commands

**Note: All Gradle commands require Java 17. Use the JAVA_HOME prefix shown below.**

- Build: `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew build`
- Test: `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew test`
- Lint: `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew lint`
- Assemble Debug APK: `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew assembleDebug`
- Install on Device: `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew installDebug`

## Key Files

- `MainActivity.kt`: Main application entry point using ComponentActivity
- `ui/theme/Theme.kt`: Material Design 3 theme configuration with dynamic colors
- `ui/theme/Color.kt`: Color scheme definitions for light and dark themes
- `ui/theme/Type.kt`: Typography definitions
- `app/build.gradle.kts`: App-level Gradle configuration with Compose dependencies
- `gradle/libs.versions.toml`: Version catalog for dependency management
