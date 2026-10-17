# AmiStudio Browser — releases

AmiStudio Browser lets a classic Amiga browse the modern web. A real Chromium runs on a Linux PC
(for AmiKit users: the PC that runs AmiKit) and the small host program `asb-chromed` sends the
finished page pictures and sound to the Amiga, which sends back mouse and keys.
This repository has release downloads only (no source).

## Latest: 0.76
Popup menus (main menu, right-click menu) and the address suggestion list no longer flicker over a playing page.
0.75 made video fullscreen fill the view and stopped Esc closing the MUI window; 0.74 added sound and the AmiKit edition.

## Downloads
See [Releases](../../releases). Each version has:

| File | What it is |
|---|---|
| `AmiStudioBrowser-<ver>-AmiKit.lha` | **AmiKit edition**: the Amiga drawer with the Linux engine (headless Chromium) inside `AmiStudioBrowser/Host/` |
| `AmiStudioBrowser-<ver>.lha` | Amiga program only (use with your own host) |
| `amistudio-browser-amikit-host-<ver>-linux-x86_64.tar.gz` | the Linux engine alone; unpack next to the drawer |

## Install — AmiKit edition (one archive)
1. Unpack `AmiStudioBrowser-<ver>-AmiKit.lha` onto an AmiKit drive that Linux can see (a folder
   drive under your AmiKit directory, not inside an `.hdf` hardfile):
   in AmiKit `lha x AmiStudioBrowser-<ver>-AmiKit.lha <drive>:`, or on Linux `lha x` / `lhasa x`.
2. Start **AmiStudioBrowser**. With Rabbit Hole (Amiberry host tools, `C:host-run`) it starts the
   Linux engine by itself. Otherwise run `sh AmiStudioBrowser/Host/run-host.sh` on Linux first.
   LHA does not keep Linux exec bits; `run-host.sh` puts them back.
3. Sound needs `pactl`/`parec` (package `pulseaudio-utils`) or `ffmpeg` on Linux.
   Details: `AmiStudioBrowser/Host/README-AMIKIT.txt`.

## Install — Amiga-only LHA
Unpack `AmiStudioBrowser-<ver>.lha` anywhere, run a host (`asb-chromed`) on a Linux PC, and point the
program at it with the `CHROMEHOST=`, `PORT=` and `TOKEN=` tooltypes. See the ReadMe in the drawer.

## Requirements
* AmigaOS 3.1+; MUI 3.8+ for the main builds (a GadTools build is included)
* 68040/060, or 68020/030 with FPU; 16 MB Fast RAM minimum
* bsdsocket.library TCP/IP (AmiKit/Amiberry emulation, Roadshow, Miami, AmiTCP...)
* RTG recommended (AGA works with dithering); sound through AHI or Paula
* Linux x86_64 for the engine (glibc 2.25+, usual desktop libraries)

## Credits and licences
* Icons: **Ken's Icons** (Kenneth's DualPNG icons, also shipped in AmiKit).
* The AmiKit edition bundles ungoogled-chromium (portable Linux build), BSD-licensed, with
  Chromium's third-party components; licences are in `Host/LICENSES/`. Source of that build:
  https://github.com/ungoogled-software/ungoogled-chromium-portablelinux
* Third-party notices for the Amiga program: `ATTRIBUTIONS` and `LICENSES` in the drawer.
