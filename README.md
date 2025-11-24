# Aurynk (Flatpak)

This repository contains the Flatpak manifest for **Aurynk**.

* **Upstream Project:** [IshuSinghSE/aurynk](https://github.com/IshuSinghSE/aurynk)
* **Report Issues:** [Upstream Issue Tracker](https://github.com/IshuSinghSE/aurynk/issues)

## 📦 Build Strategy

This package uses a **hybrid build strategy** to satisfy Flathub requirements while avoiding massive build dependencies:

1.  **Scrcpy:** The C client is built from source (using Meson) to ensure native performance and architecture compatibility. The Java server (`scrcpy-server.jar`) is downloaded as a prebuilt binary because the Android SDK is not available in the Flatpak build environment.
2.  **ADB:** We use the official Google `platform-tools` binaries.

### Architecture Support
⚠️ **x86_64 Only.**
Builds for `aarch64` (ARM64) are explicitly disabled in `flathub.json`. This is because Google does not provide standalone `platform-tools` (ADB) binaries for Linux ARM64.

## 🛠 Building Locally

To test this package locally:

```bash
# 1. Install standard Freedesktop SDK
flatpak install flathub org.freedesktop.Sdk//24.08 org.freedesktop.Platform//24.08

# 2. Build
flatpak-builder --force-clean build-dir io.github.IshuSinghSE.aurynk.yml

# 3. Install & Run
flatpak-builder --user --install --force-clean build-dir io.github.IshuSinghSE.aurynk.yml
flatpak run io.github.IshuSinghSE.aurynk