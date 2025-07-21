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

## CI/CD Pipeline

### Overview
This project uses GitHub Actions for automated continuous integration and deployment. The pipeline automatically runs on every pull request and push to the main branch, ensuring code quality and providing downloadable APK artifacts for testing.

### Pipeline Steps
1. **Lint Checks**: Runs Android lint to catch potential issues and enforce code quality
2. **Unit Tests**: Executes all unit tests to verify functionality
3. **Build**: Compiles and assembles a debug APK
4. **Artifact Upload**: Uploads the built APK as a downloadable artifact (retained for 3 days)

### Branch Protection
The main branch is protected with the following requirements:
- Pull requests must pass the "Pull Request Validation" status check
- Branches must be up to date before merging
- At least one review is recommended before merging

### Downloading APK Artifacts

To download and test APKs from pull requests:

1. **From a Pull Request**:
   - Navigate to the PR page on GitHub
   - Click on "Checks" tab
   - Find the "Pull Request Validation" workflow
   - Click on the workflow run
   - Scroll to the "Artifacts" section at the bottom
   - Download the `voice-memo-{commit-hash}` artifact

2. **From the Actions Tab**:
   - Go to the repository's "Actions" tab
   - Click on any completed "Pull Request Validation" workflow run
   - Download artifacts from the bottom of the page

3. **Installing the APK**:
   - Extract the downloaded zip file to get the APK
   - Enable "Install from unknown sources" on your Android device
   - Transfer and install the APK file

### Troubleshooting CI Issues

**Build Failures**:
- Check the workflow logs in the Actions tab for detailed error messages
- Common issues: lint errors, test failures, or compilation problems
- Use `--stacktrace` in local Gradle commands to debug issues locally

**Lint Errors**:
- Run `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew lint` locally
- Fix any reported issues before pushing
- Lint reports are available in `app/build/reports/lint-results-debug.html`

**Test Failures**:
- Run `JAVA_HOME=/opt/homebrew/opt/openjdk@17 ./gradlew test` locally
- Check test output for specific failing tests
- Ensure all dependencies and test setup are correct

**Java Version Issues**:
- The CI pipeline uses Java 17 with Temurin distribution
- Ensure local development uses the same Java version
- Check that JAVA_HOME is set correctly for local builds

**Artifact Download Issues**:
- Artifacts are only available for 3 days after the workflow run
- Only successful builds generate downloadable APK artifacts
- Artifacts are compressed in zip format and need to be extracted
