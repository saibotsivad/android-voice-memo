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

- Android application built with ...TODO...

## Development Commands

- Build: ...TODO...
- Test: ...TODO...
- Lint: ...TODO...

## Key Files

- TODO
