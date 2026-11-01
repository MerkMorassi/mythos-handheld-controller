# mythos-handheld-controller

Generic USB game controller / macro pad.

## Hardware inputs

- 12 keys
- 2 rotary encoders (20 steps per turn), each also clickable (push)
- Use: map keys and dials to macros

## Repo contents

- `MINI_KEYBOARD.exe`: Windows configuration app for the device (prebuilt).
- `KEYPAD-CONTROLLER.7z`: Windows bundle with `MINI_KEYBOARD.exe`, the Qt 5 and `hidapi.dll` runtime DLLs it needs, and the same build files as the repo root. No source code inside.
- `Makefile`, `Makefile.Debug`, `Makefile.Release`: qmake-generated (Qt 5.14.2, project `KEY_PRO.pro`, spec `win32-g++`).
- `moc_*.cpp`, `qrc_image.cpp`, `moc_predefs.h`: Qt-generated code.
- `*.o`: compiled objects from a previous build.
- `lanague_*.qm`: compiled UI translations (en, cn).

The app talks to the device over USB HID through `hidapi`. Its UI has key mapping (keyboard, mouse, multimedia keys), layers, delay settings and LED / RGB LED modes.

## Build

Status: **cannot be rebuilt from this repo yet.** The Makefiles need the original sources, which are not here:

- `KEY_PRO.pro`
- `main.cpp`, `widget.cpp/.h/.ui`, `dialog1.cpp/.h/.ui`, `dialog2.cpp/.h/.ui`, `dialog3.cpp/.h/.ui`, `reminderwidget.cpp/.h/.ui`
- `hidapi.h`

With those added, the generated Makefiles expect:

- Windows, Qt 5.14.2 with MinGW 7.3 32-bit (`mingw73_32`)
- hidapi (`-lhidapi`)
- Rerun `qmake` locally: the Makefiles hard-code the original machine's Qt and library paths.

Commands (from a Qt MinGW shell):

```
qmake KEY_PRO.pro -spec win32-g++
mingw32-make release
```

`mingw32-make` with no target builds `debug`. Output: `KEY_PRO.exe`.

## Run

Windows only. Unpack `KEYPAD-CONTROLLER.7z` and run `MINI_KEYBOARD.exe` from the unpacked folder, where its DLLs sit next to it.
