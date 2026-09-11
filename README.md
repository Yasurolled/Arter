# arter

arter is a small, keyboard-first graphical text editor written in C. It is a fork of [agte](https://github.com/bkeskinsoftware/agte), redesigned with a responsive layout, a context menu, and a cross-platform CMake build. It uses raylib for its window, input, clipboard, and rendering layer, so the same source can target Windows, Linux, and macOS.

This project keeps the original agte codebase's lightweight spirit while evolving its interface and build workflow under the arter name.

Development of arter was made with the help of GitHub Copilot.

## Installation

Use a release package when available, or build from source with raylib and raygui installed. No platform-specific UI toolkit is required.

## Usage

```text
arter [filename]
```

The filename is optional. Starting without one opens `untitled.txt` in the current directory. A missing file is created when you save it.

It will create the file in your current directory, or open it if the file already exists.

The responsive sidebar shows the save state and Caps Lock state. Resize the window freely, or press F11 for fullscreen.

arter treats files as text and does not inspect their encoding. Opening a folder or a binary file is unsupported.

<img width="1443" height="918" alt="image" src="https://github.com/user-attachments/assets/05b00403-0b92-4b5d-a820-42a158e8101e" />

## Controls

Arrow keys move the cursor to their respective directions.

Page Up moves the cursor to the beginning of the file.
Page Down moves the cursor to the end of the file.

All movement keys combined with the "Shift" key will move your selection area with the cursor. "Shift" needs to be held down for adjustments and the selection area will reset if any input is given or a movement key is pressed without holding "Shift".

CTRL + C copies the selected area or the current line to the clipboard.
CTRL + X cuts the selected area or the current line to the clipboard.
CTRL + V pastes the clipboard on the cursor's current location.

if no selection is provided, these controls will work on the current line as whole ('\n' to '\n'). In other words, it falls back/defaults the line selection.

CTRL + S saves the document.

CTRL + Q closes the editor. F11 toggles fullscreen. Right-click opens a context menu with copy, cut, paste, and select-all actions.

Tab indents 2 characters deep.

## Compilation

The recommended route is CMake:

```bash
cmake -S . -B build
cmake --build build --config Release
```

Install raylib through your platform's package manager and place `raygui.h` in the project root, or point CMake at its containing directory with `-DRAYGUI_INCLUDE_DIR=/path/to/raygui`.

On Windows with MSYS2, use the **UCRT64** terminal:

```bash
pacman -S --needed mingw-w64-ucrt-x86_64-toolchain mingw-w64-ucrt-x86_64-cmake mingw-w64-ucrt-x86_64-raylib
curl --fail --location --output raygui.h https://raw.githubusercontent.com/raysan5/raygui/master/src/raygui.h
cmake -S . -B build -G "MinGW Makefiles" -DRAYGUI_INCLUDE_DIR="$PWD"
cmake --build build
```

The project links raylib's required Windows libraries automatically.

On Debian or Ubuntu:

```bash
sudo apt-get install build-essential cmake libraylib-dev
curl --fail --location --output raygui.h https://raw.githubusercontent.com/raysan5/raygui/master/src/raygui.h
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DRAYGUI_INCLUDE_DIR="$PWD"
cmake --build build --parallel
```

On macOS, install raylib with Homebrew, place `raygui.h` in the project root, and use the same CMake commands. The source does not assume a path separator or OS-specific input API.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the development setup and pull request expectations. Bug reports and feature ideas are welcome through GitHub Issues.

## License

[AGPL-3.0](https://choosealicense.com/licenses/agpl-3.0/)

## footnote
Known limitations are:
* No "valid format" check present.
* No full UTF support has been implemented.
* No "undo" and "redo" functions.
* Poor Caps Lock logic that only shows if the state has been changed, doesn't check the actual position. Kept that way to ensure OS Agnostic nature.

The editor intentionally stays small: it has no bundled file explorer, terminal, or platform-specific file dialog yet.

raylib source code is NOT distributed along the program, it is baked into the binary statically.

Do you have any ideas or would you like to help in any way? Please let me know via e-mail.
