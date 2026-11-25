# Android Audio Shim

Experimental Android audio bridge for [Simple Voice Chat](https://modrinth.com/plugin/simple-voice-chat) on MojoLauncher and PojavLauncher.

## Target build

- Minecraft Java Edition **1.21.11**
- Fabric Loader
- Java 21 or newer
- Android 8.0+
- arm64-v8a device

This build targets Fabric on Minecraft 1.21.11. The native audio library uses AAudio for microphone input and OpenSL ES for speaker output. It does not guarantee that every Android device or launcher exposes the microphone correctly.

## How it works

Android does not provide the desktop Java Sound audio devices expected by Simple Voice Chat. This JAR registers a Java Sound MixerProvider and routes microphone and speaker audio through Android's native audio APIs.

The native library (`libaudioshim.so`) is bundled in the JAR and extracted when the audio provider loads.

## Installation

1. Use a Fabric profile for Minecraft 1.21.11.
2. Put the JAR in that profile's `mods` folder.
3. Keep a compatible Simple Voice Chat Fabric mod installed.
4. Grant MojoLauncher microphone permission in Android settings.
5. Start Minecraft and check the Simple Voice Chat microphone list.

The shim may not appear as a normal entry in the Mods screen because it registers a Java audio service rather than a typical gameplay entrypoint.

## Important limitations

- This is an experimental compatibility layer, not an official Simple Voice Chat Android port.
- The bundled native library is built for Android arm64-v8a.
- A successful build only confirms that the files compile and package; actual microphone and speaker operation must be tested on the device.
- The microphone may appear as a default Android audio input rather than by the earphones' product name.

## Building

The GitHub Actions workflow builds the arm64 Android native library with the Android NDK, compiles the Java classes, packages the Fabric metadata and service provider, and uploads the JAR as an Actions artifact.
