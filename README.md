# GearLever AppImage Builds

<p align="center">
  <img width="150" src="https://raw.githubusercontent.com/mijorus/gearlever/master/data/icons/hicolor/scalable/apps/it.mijorus.gearlever.svg" alt="GearLever Icon">
</p>

<p align="center">
  <strong><a href="https://github.com/T3sT3ro/gearlever/releases/latest">Download Latest AppImage</a></strong>
</p>

<p align="center">
  <a href="https://buymeacoffee.com/tooster" target="_blank">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" width="180" height="50">
  </a>
  <br>
  <sub><i>If you find these AppImage builds useful, consider buying me a ~~coffee~~ pair of socks!</i></sub>
  <br>
  <sub><i>(Note: This supports the fork maintainer, not the original GearLever developer)</i></sub>
</p>

Automated AppImage builds for [GearLever](https://github.com/mijorus/gearlever) - manage AppImages with ease.

## About

This is an **orphan branch fork** that provides automated AppImage builds from the upstream [mijorus/gearlever](https://github.com/mijorus/gearlever) repository.

**Key Features:**
- ✅ Automated daily sync with upstream releases
- ✅ Built with Docker for reproducibility
- ✅ Includes update information (works with AppImageUpdate)
- ✅ Includes all necessary scripts for proper AppImage execution
- ✅ Minimal patches applied only for AppImage compatibility

## Installation and Integration

Download the latest GearLever AppImage from the [Releases](https://github.com/T3sT3ro/gearlever/releases/latest). page and make it executable:

```bash
chmod +x GearLever-x86_64.AppImage
./GearLever-x86_64.AppImage
```

Add the AppImage to GearLever (with manual OPEN action to select the appimage at top-right) and enjoy seamless integration from now on!

## What is GearLever?

GearLever is a tool to integrate AppImages into your desktop environment:
- Integrate AppImages into your app menu with just one click
- Drag and drop files directly from your file manager
- Keep all AppImages organized in a custom folder
- Manage updates - keep older versions or replace with latest
- Modern GTK4/libadwaita UI

**Prefer Flatpak?** Get it on [Flathub](https://flathub.org/apps/details/it.mijorus.gearlever)

## Repository Structure

```
main branch (orphan):
├── .docker/
│   ├── Dockerfile           # Multi-stage Docker build
│   └── patches/             # AppImage compatibility patches
│       └── 01-appimage-pkgdatadir.patch
├── .github/workflows/
│   ├── sync-upstream-release.yml  # Daily upstream sync
│   └── appimage-build.yml         # CI builds
├── gearlever/               # Git submodule → mijorus/gearlever
└── README.md
```

The AppImage is built from upstream's official release code with minimal patches applied only for AppImage compatibility.

## Building Locally

```bash
# Clone with submodules
git clone --recursive https://github.com/T3sT3ro/gearlever.git
cd gearlever

# (Optional) Checkout specific upstream version
cd gearlever
git checkout v3.4.5
cd ..

# Build
docker build -t gearlever-appimage -f .docker/Dockerfile .
docker run --rm -v $(pwd)/build:/output:rw gearlever-appimage

# The AppImage will be in ./build/GearLever-x86_64.AppImage
# Note: You may need to fix ownership since Docker creates files as root
sudo chown -R $USER:$USER ./build
```

## How It Works

1. GitHub Actions runs daily (or on manual trigger)
2. Checks for new releases in upstream repository
3. Updates submodule to the release tag
4. Builds AppImage using Docker with applied patches
5. Creates GitHub release with AppImage + .zsync file

The AppImage includes embedded update information pointing to this repository, so users can update via AppImageUpdate.

## Links

- **Upstream Repository**: https://github.com/mijorus/gearlever
- **GearLever Website**: https://mijorus.it/projects/gearlever/
- **Flathub (Flatpak)**: https://flathub.org/apps/details/it.mijorus.gearlever
- **Changelog**: https://gearlever.mijorus.it/changelog

## License

Same as upstream: See [gearlever/COPYING](gearlever/COPYING)
