# Contributing to arter

Thanks for helping improve arter.

## Development setup

arter is a C11 fork of agte, built with CMake, raylib, and raygui. On Windows, use the MSYS2 UCRT64 terminal and install:

```bash
pacman -S --needed mingw-w64-ucrt-x86_64-toolchain mingw-w64-ucrt-x86_64-cmake mingw-w64-ucrt-x86_64-raylib
```

Place `raygui.h` in the project root or pass its containing directory with `-DRAYGUI_INCLUDE_DIR`.

Configure and build:

```bash
cmake -S . -B build -G "MinGW Makefiles" \
  -DRAYGUI_INCLUDE_DIR="$PWD"
cmake --build build
```

## Changes

- Keep changes focused and consistent with the existing C style.
- Update `README.md` when user-facing behavior changes.
- Add a short entry to `DEVLOG.md` for notable changes.
- Do not commit `build/`, `.tools/`, generated binaries, or personal test documents.
- Test the application manually when changing input, rendering, or file handling.

## Pull requests

Describe what changed, how it was tested, and any platform-specific details. Small, focused pull requests are easier to review.
