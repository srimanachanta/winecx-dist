# WineCX Distributables

Prebuilt macOS binaries of Wine based on CrossOver sources from CodeWeavers.

## What this is

A GitHub Actions workflow that downloads CrossOver source tarballs, builds Wine from them on an Intel macOS runner, and publishes the result as a GitHub release.

Each release contains a `winecx-<version>-osx64.tar.gz` artifact with a `bin/wine` binary and supporting libraries.

## Building a release

1. Go to the Actions tab.
2. Run the **Build winecx** workflow.
3. Enter the CrossOver source version (e.g. `25.0.1`).

The workflow fetches `crossover-sources-<version>.tar.gz` from CodeWeavers, builds Wine with the Homebrew toolchain, and attaches the tarball to a `v<version>` release.

## Build options

Wine is configured for 64-bit with 32-bit support (`i386,x86_64`), MinGW, CoreAudio, Vulkan, GnuTLS, FreeType, SDL, and CUPS. Tests, `winedbg`, X11, OpenGL, PulseAudio, and GStreamer are disabled. Deployment target is macOS 10.15.

See [scripts/build-wine.sh](scripts/build-wine.sh) for the full configure line.

## Running locally

You can run the build script on an Intel Mac with the required Homebrew packages installed:

```
brew install bison ccache gettext mingw-w64 pkgconfig freetype gnutls libpcap sdl2
./scripts/build-wine.sh 25.0.1
```

The output tarball lands at the repository root.
