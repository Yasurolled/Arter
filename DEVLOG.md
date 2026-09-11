# Development Log

This file records notable repository changes so they remain visible alongside commits.

## Project identity

arter is the successor fork of agte. The application, source file, executable, CMake target, and public documentation use the arter name.

The project was developed with the help of GitHub Copilot.

The copyright attribution for the arter source is `YasuRolled`.

## 2026-09-11

- Redesigned the raylib editor shell around a responsive layout instead of fixed 1200x720 panel coordinates.
- Added a toolbar with the document path and shortcut hints.
- Added a responsive sidebar for save and Caps Lock indicators.
- Added a status bar showing line, column, line count, character count, and modified/ready state.
- Added a right-click context menu with Copy, Cut, Paste, and Select All actions.
- Added `Ctrl+Q` to request a clean application exit and `F11` to toggle fullscreen.
- Allowed startup without a filename; the editor opens `untitled.txt` in the current directory.
- Added resizable-window support with a 640x360 minimum size.
- Added `CMakeLists.txt` with raylib/raygui discovery and Windows, macOS, and Linux link handling.
- Updated `README.md` with the new controls, responsive behavior, and CMake instructions.
- Installed portable CMake 4.1.1 under the ignored `.tools/` directory.
- CMake configuration was attempted and reached the generator step, but no C compiler or `nmake` is installed.
- Attempted to extract the official LLVM 23.1.1 Windows MSI locally; Windows Installer did not produce a usable `clang.exe`.
- Confirmed the installed MinGW GCC 6.3.0 works for trivial C programs after adding `C:\MinGW\bin` to `PATH`.
- Raylib 5.5 configuration succeeds, but its build fails against the old MinGW.org Windows headers (`minwindef.h` missing and `CloseWindow`/`ShowCursor` conflicts). A modern MinGW-w64 toolchain is required to finish the Windows build.
- Installed MSYS2 UCRT64 and built raylib 5.5 locally with GCC 16.2.0.
- Added the Windows `winmm` link dependency required by raylib's timer functions.
- Successfully built `build/agte.exe` with the MSYS2 UCRT64 toolchain.
- Improved font rendering by enabling bilinear filtering for the embedded Lilex and icon textures, and increased toolbar text sizes to prevent clipped-looking glyphs.
- Centralized text insertion so typing, Enter, Tab, and paste replace active selections instead of inserting inside them.
- Added save-result handling, save error feedback, caret auto-scrolling, right-side modifier support, macOS Command shortcuts, and initialization checks for the window and embedded fonts.
- Removed obsolete commented-out autoscroll code and hardened buffer growth and existing-file read failures.
