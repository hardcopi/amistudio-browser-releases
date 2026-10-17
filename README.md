# AmiStudio Browser — releases

AmiStudio Browser lets a classic Amiga browse the modern web. A real Chromium runs on a Linux PC
(for AmiKit users: the PC that runs AmiKit) and the small host program `asb-chromed` sends the
finished page pictures and sound to the Amiga, which sends back mouse and keys.
This repository has release downloads only (no source).

## Latest: 0.80
* **DRM video (Netflix, Spotify, Prime Video, Disney+ ...)** can work in the AmiKit edition once Google's Widevine
  CDM is added. It is Google's and may not be redistributed, so no download here contains it. Add it once on Linux:
  `sh AmiStudioBrowser/Host/get-widevine.sh` - it copies the CDM from Google Chrome if installed, or (after asking)
  downloads Google's Chrome package from dl.google.com and keeps only its WidevineCdm folder. Restart the engine
  afterwards. With Google Chrome installed the engine finds Chrome's CDM by itself. Without it Netflix shows M7701-1003.
* Quality limits on Linux (Widevine L3 only): Netflix up to 1080p (often 720p), Disney+ 480p-720p, Prime Video SD.
* Tested with a public Widevine test stream (picture and sound reach the Amiga). Netflix itself is not tested yet.

Earlier: 0.79 made the hamburger menu MUI's own popup menu on MUI 5 (no more strobing); 0.78 fixed @gmail.com sign-in
and the save-password bar; 0.77 fixed Backspace in the address bar and added the Amiga-side log; 0.76 reduced menu
flicker, 0.75 made video fullscreen fill the view, 0.74 added sound and the AmiKit edition.

## Where things are kept (0.77 and later)
* Amiga log: `AmiStudioBrowser.log` next to the AmiStudioBrowser program (the previous run is kept as
  `AmiStudioBrowser.log.old`). `LOG=<file>` moves it, `LOG=OFF` turns it off.
* AmiKit edition, Linux side: `AmiStudioBrowser/Host/data/`, which holds `host.log` (engine log), `config/`
  (history.tsv, bookmarks.tsv, settings, passwords) and `profile/` (Chromium profile). It is created on first
  start, and data from `~/.local/state/amistudio-browser-amikit/` is moved there automatically. If the drawer
  is read-only, noexec or cannot hold symlinks, the old folder is used and `host.log` says why.
  `ASB_STATE=/folder` overrides.
* Downloads still go to `~/Downloads`.

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
* Toolbar icon shapes: **Lucide** (ISC licence).
* Frame decoding in the Amiga program and the engine: **stb_image** (public domain / MIT) and **QOI** (MIT).
* The Linux engine `asb-chromed` statically links **OpenSSL** 3 libcrypto (Apache 2.0), **zlib** (zlib licence)
  and **Zstandard** (BSD-3-Clause); licence texts are in `Host/LICENSES/`.
* The AmiKit edition bundles ungoogled-chromium (portable Linux build), BSD-licensed, with
  Chromium's third-party components; licences are in `Host/LICENSES/`. Source of that build:
  https://github.com/ungoogled-software/ungoogled-chromium-portablelinux
* Third-party notices for the Amiga program: `ATTRIBUTIONS` and `LICENSES` in the drawer.
