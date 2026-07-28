# RigForge Mobile

RigForge Mobile is an Android-first rigging and weight-painting editor foundation for GLB/glTF assets.

This branch contains the first production vertical slice:

- Kotlin and Jetpack Compose application shell
- C++20 native rig document through JNI
- OpenGL ES 3 viewport
- GLB/glTF 2.0 mesh import
- Armature, Pose and Weight Paint workspace modes
- Touch orbit, zoom and weight-paint input
- Normalized vertex influences, undo/redo and diagnostics
- Architecture boundary checks and native core tests
- GitHub Actions debug APK build

This is not yet full Blender feature parity. It establishes the modular document, operator, renderer and import foundations required to implement parity without replacing the architecture later.

## Source archive

The source tree is stored as ordered Base64 chunks under `archive/` because this initial branch was published through the GitHub connector. CI concatenates and verifies them before extraction.

Expected source ZIP SHA-256:

```text
7831d0da61c73f008d169d2e073f51378d197e07952e5cd812a5f41a2c1a7efb
```

Reconstruct locally:

```bash
cat archive/part*.b64 | base64 --decode > RigForgeMobile-source.zip
echo "7831d0da61c73f008d169d2e073f51378d197e07952e5cd812a5f41a2c1a7efb  RigForgeMobile-source.zip" | sha256sum --check -
unzip RigForgeMobile-source.zip
```

The extracted project directory is `MobileRig/`.

## Build

Requirements:

- JDK 17
- Android SDK 35
- Android NDK 27.2.12479018
- CMake 3.22.1
- Gradle 8.10.2

```bash
cd MobileRig
./scripts/architecture_check.sh
./scripts/native_core_test.sh
gradle --no-daemon :app:assembleDebug :app:testDebugUnitTest
```

The APK is produced at:

```text
MobileRig/app/build/outputs/apk/debug/app-debug.apk
```
