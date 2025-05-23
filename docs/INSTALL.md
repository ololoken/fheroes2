# [fheroes2](README.md) Installation Guide

## Requirements

You will need to have a demo version or the full version of **Heroes of Might and Magic II** game to be able to play. We strongly
advise to purchase the original game on [**GOG**](https://www.gog.com) or [**Ubisoft Store**](https://store.ubi.com) platforms.

Alternatively, you can **download a free demo version of the game (in English only) using the bundled script**. See detailed
instructions below.

## Installation

Precompiled binaries of the release version are currently available for the following platforms and operating systems:

* [**Windows**](#windows)
  * [**Windows installer**](#windows-installer)
  * [**Windows ZIP archive**](#windows-zip-archive)
* [**macOS**](#macos)
  * [**Homebrew**](#homebrew-on-macos)
  * [**MacPorts**](#macports)
  * [**macOS ZIP archive**](#macos-zip-archive)
  * [**macOS native app**](#macos-native-app)
* [**Linux**](#linux)
  * [**Flatpak**](#flatpak)
  * [**Gentoo**](#gentoo-package)
  * [**Homebrew**](#homebrew-on-linux)
  * [**AUR package**](#aur-package)
  * [**Debian and Ubuntu**](#debian-and-ubuntu)
  * [**Linux ZIP archive**](#linux-zip-archive)
* [**Android**](#android)
* [**PlayStation Vita**](#playstation-vita)
* [**Nintendo Switch**](#nintendo-switch)

Alternatively, you can download the precompiled binaries of the latest commit (snapshot) [**here**](#snapshots-latest-builds).

## Windows

### Windows Installer

* Download one of the following Windows installer packages:
  * [**Windows x64 (64-bit)**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_windows_x64_SDL2_installer.exe)
  * [**Windows x86 (32-bit)**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_windows_x86_SDL2_installer.exe)
* After downloading the installer, launch it and follow the instructions.
* During the installation process, you will be prompted to extract game resources from the original game (select this option if you
  already have a legally purchased copy of the original game installed), or download the demo version of the original game and extract
  game resources from it (you can also do this later by clicking the appropriate shortcut in the program's group in the Windows Start
  menu).
* If you purchased a copy of the original game only after installing fheroes2, you can run the `Extract game resources from the original
  distribution of HoMM2` shortcut in the program's group in the Windows Start menu. This script will try to perform an automatic search
  for an existing installation of the original game and extract all the necessary resource files. If it can't find an existing installation,
  you will be prompted to enter the location of the original game manually.
* As an alternative to the previous step, you can manually copy the subdirectories `ANIM`, `DATA`, `MAPS` and `MUSIC` (some of them may
  be missing depending on the version of the original game) from the original game directory to the fheroes2 installation directory.

### Windows ZIP Archive

* Download one of the following Windows ZIP archives:
  * [**Windows x64 (64-bit)**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_windows_x64_SDL2.zip)
  * [**Windows x86 (32-bit)**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_windows_x86_SDL2.zip)
* After downloading the ZIP archive, extract it to a suitable directory of your choice.
* If you have a legally purchased copy of the original game, run the `extract_homm2_resources.bat` script supplied in the ZIP archive.
  This script will try to perform an automatic search for an existing installation of the original game and extract all the necessary
  resource files. If it can't find an existing installation, you will be prompted to enter the location of the original game manually.
* As an alternative to the previous step, you can manually copy the subdirectories `ANIM`, `DATA`, `MAPS` and `MUSIC` (some of them may
  be missing depending on the version of the original game) from the original game directory to the fheroes2 installation directory.
* If you don't have a legally purchased copy of the original game, you can download and install the demo version of the original game
  by running the `download_demo_version.bat` script supplied in the ZIP archive.

#### Troubleshooting Missing Microsoft Visual C++ DLLs

If you see complaints about missing DLLs when running fheroes2, then you may need to install the Microsoft Visual C++ redistributable package.

You can download it using the following URLs:

| Windows Version | C++ Package |
|--------|--------|
| For 64-bit x64 fheroes2 builds | [**https://aka.ms/vs/17/release/vc_redist.x64.exe**](https://aka.ms/vs/17/release/vc_redist.x64.exe) |
| for 32-bit x86 fheroes2 builds | [**https://aka.ms/vs/17/release/vc_redist.x86.exe**](https://aka.ms/vs/17/release/vc_redist.x86.exe) |

## macOS

### Homebrew on macOS

If you are using [**Homebrew**](https://brew.sh/), you can install the game by running the following command:

```sh
brew install fheroes2
```

Follow the [**instructions below**](#gathering-game-resources) to gather resources necessary for fheroes2 to function as expected.

### MacPorts

If you are using [**MacPorts**](https://www.macports.org/), you can install the game by running the following command:

```sh
port install fheroes2
```

Then follow the instructions on the screen.

Follow the [**instructions below**](#gathering-game-resources) to gather resources necessary for fheroes2 to function as expected.

### macOS ZIP Archive

* Download the [**macOS ZIP archive**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_macos_x86-64_SDL2.zip).
  Currently only x86-64 binaries are provided. If you use a machine with an Apple Silicon chip, you should choose another installation
  method (using [**MacPorts**](#macports) or [**Homebrew**](#homebrew-on-macos)), or
  [**build the project from source**](DEVELOPMENT.md#macos-and-linux).
* After downloading the ZIP archive, extract it to a suitable directory of your choice and then run `brew bundle` from
  the `script/macos` subdirectory. This will install the SDL libraries required to run the game.

Follow the [**instructions below**](#gathering-game-resources) to gather resources necessary for fheroes2 to function as expected.

### macOS Native App

* Install the required dependencies using the provided Brewfile:

```sh
brew bundle --file script/macos/Brewfile.app_bundle
```

* Download the source and compile with the `-DMACOS_APP_BUNDLE=ON` option (if using CMake) or using the following command (with make):

```sh
make FHEROES2_MACOS_APP_BUNDLE=ON
```

Follow the [**instructions below**](#gathering-game-resources) to gather resources necessary for fheroes2 to function as expected.

### Gathering Game Resources

Once you obtain the fheroes2 executable using any of the options above, you should follow these steps to load in the correct resources:

* If you have a legally purchased copy of the original game in a self-extracting Windows executable (such as from GOG), you can utilize
  [`innoextract`](https://constexpr.org/innoextract/#use) to extract files out of the exe without having to use Wine/Windows emulation
  software on your *UNIX-based machine.
* If you have a legally purchased copy of the original game, run the extract resources script which will prompt you to enter
  the location of the original game, and will extract all the necessary resource files. The script can be run from the following paths depending on
  how you installed fheroes2:

  | Installation Method | Script |
  |--------|--------|
  | If you used a package manager (MacPorts or Homebrew) | `fheroes2-extract-resources` |
  | If you built from source using the [**macOS native app**](#macos-native-app) method | `script/homm2/extract_homm2_resources_for_app_bundle.sh` |
  | All other cases | `script/homm2/extract_homm2_resources.sh` |

  Alternatively, you may manually copy the subdirectories `ANIM`, `DATA`, `MAPS` and `MUSIC` (some of them may be missing depending on the version of the original game)

  | Installation Method | Destination |
  |--------|--------|
  | built from source using the [**macOS native app**](#macos-native-app) | `~/Library/Application Support/fheroes2` |
  | All other cases | `~/.fheroes2` |

* If you don't have a legally purchased copy of the original game, you can download and install the demo version of the original game
  by running the download demo script. The script can be run from the following paths depending on how you installed fheroes2:

  | Installation Method | Script |
  |--------|--------|
  | If you used a package manager (MacPorts or Homebrew) | `fheroes2-install-demo` |
  | If you built from source using the [**macOS native app**](#macos-native-app) method | `script/demo/download_demo_version_for_app_bundle.sh` |
  | All other cases | `script/demo/download_demo_version.sh` |

## Linux

### Flatpak

If you are using [**Flatpak**](https://flatpak.org) and [**Flathub**](https://flathub.org), you can install the game by running the
following command:

```sh
flatpak install flathub io.github.ihhub.Fheroes2
```

And launch from the start menu or the console:

```sh
flatpak run io.github.ihhub.Fheroes2
```

Alternatively, you can use an application manager like Discover, which is also available on Steam Deck.

After the first start you will be asked for the original files. There are three possibilities:

1. Install GOG version (recommended)
2. Manual install
3. Install demo

The recommended option requires the Heroes of Might and Magic II installer file (*.exe) from GOG. This will extract the appropriate resources by itself.

For the manual installation you have to copy the subdirectories `ANIM`, `DATA`, `MAPS` and `MUSIC` from the original game or demo directory to the
`~/.var/app/io.github.ihhub.Fheroes2/data/fheroes2` directory. The destination folder will be opened when this option is selected.

### Gentoo Package

If you are using [**Gentoo**](https://gentoo.org), you can install the game using package manager. There are several options:

#### GOG Version

If you purchased the game from GOG, add `games-strategy/homm2-gold-gog GOG-EULA` line to your `/etc/portage/package.license`, then use the following command:

```sh
sudo emerge -av games-strategy/homm2-gold-gog
```

It will ask you to put the .exe installer of the game and optionally the zip file with FLAC music to your distfiles directory,
and if it's there, it will unpack everything to the correct places and pull `games-engines/fheroes2` as a dependency.

USE-flag `flac` determines whether the game will use FLAC music or OGG music.

#### Demo Version

You can install the demo version for free by adding `games-strategy/homm2-demo HoMM2-Demo` line to your `/etc/portage/package.license`, then using the following command:

```sh
sudo emerge -av games-strategy/homm2-demo
```

#### Another Legal Installation

If you installed the game from original CD, use the following commands:

```sh
sudo emerge -av games-engines/fheroes2
/usr/share/fheroes2/extract_homm2_resources.sh
```

The second command (Note: run it without root) will ask you where your data files are.

### Homebrew on Linux

If you are using [**Homebrew**](https://brew.sh/), you can install the game by running the following command:

```sh
brew install fheroes2
```

If you have a legally purchased copy of the original game, copy the subdirectories `ANIM`, `DATA`, `MAPS` and `MUSIC` (some of them may
be missing depending on the version of the original game) from the original game directory to the `$XDG_DATA_HOME/fheroes2` (usually
`~/.local/share/fheroes2`) directory. Otherwise, you can download and install the demo version of the original game by running the
`/usr/share/fheroes2/download_demo_version.sh` script.

### AUR Package

If you are using Arch Linux or compatible distribution, you can install [**fheroes2 package**](https://aur.archlinux.org/packages/fheroes2)
from AUR (Arch User Repository).

#### Install Using AUR Helper

If you use one of AUR helpers, e.g. `yay`, you can install the game by running the following command:

```sh
yay -S aur/fheroes2
```

#### Install Using the Official Guide

Follow the [**official guide**](https://wiki.archlinux.org/title/Arch_User_Repository#Installing_and_upgrading_packages).
One of possible command sets:

```sh
git clone https://aur.archlinux.org/fheroes2.git
cd fheroes2
makepkg -si
```

### Debian and Ubuntu

fheroes2 is available from `contrib` repositories for Debian (since 13) and Ubuntu (since 24.04). You can install it by running:

```sh
apt install fheroes2
```

These distributions may not provide the latest version of the game due to their release cycle.

#### Game Resources

To play the game you need the original game resources. You can install them to per-user paths (`man fheroes2` for more info, or you
can install them to the system-wide path (`/usr/share/games/fheroes2`) with `game-data-packager` program (since v70).
To make the resource package:

```sh
game-data-packager heroes2 <path_to_installed_original_game>
apt install ./homm2-data_<version>_all.deb
```

You can get more info about resource packaging by running `game-data-packager heroes2 --help`

### Linux ZIP Archive

* Download one of the following Linux ZIP archives:
  * [**Linux x86-64**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_ubuntu_x86-64_SDL2.zip)
  * [**Linux ARM64**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_ubuntu_arm64_SDL2.zip)
* After downloading the ZIP archive, extract it to a suitable directory of your choice. Then you will need to install the SDL libraries
  required to run the game. The installation procedure depends on the Linux distribution you are using:
  * **Debian-based**: run the script `install_sdl2.sh` from the `script/linux` subdirectory.
  * **Pacman-based (e.g. Arch Linux)**: run the following command: `sudo pacman -S sdl2 sdl2_mixer`.
  * **RedHat-based**: for RPM-based distributions (such as Fedora or RedHat) use the commands `sudo yum install SDL*` or `sudo dnf install SDL*`.
  * **openSUSE**: openSUSE supports the One-Click-Install using the `SDL_mixer.ymp` file from the `script/linux` subdirectory.
  * **Gentoo**: run the following command: `emerge --ask media-libs/sdl2-mixer`.
* After all dependencies are installed, run the `extract_homm2_resources.sh` script supplied in the ZIP archive if you have a legally purchased
  copy of the original game. You will be prompted to enter the location of the original game, and the script will extract all the necessary
  resource files.
* As an alternative to the previous step, you can manually copy the subdirectories `ANIM`, `DATA`, `MAPS` and `MUSIC` (some of them may
  be missing depending on the version of the original game) from the original game directory to the fheroes2 installation directory.
* If you don't have a legally purchased copy of the original game, you can download and install the demo version of the original game
  by running the `download_demo_version.sh` script supplied in the ZIP archive.

## Android

* Install the fheroes2 app from [**Google Play**](https://play.google.com/store/apps/details?id=org.fheroes2) or download the
  [**Android ZIP archive**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_android.zip).
* Follow the [**instructions**](README_android.md).

## PlayStation Vita

**Please note**: you need to be running custom firmware for it to work.

* Download the [**PlayStation Vita ZIP archive**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_psv.zip).
* Follow the [**instructions**](README_PSV.md).

## Nintendo Switch

**Please note**: you need to be running custom firmware for it to work.

* Download the [**Nintendo Switch ZIP archive**](https://github.com/ihhub/fheroes2/releases/latest/download/fheroes2_switch.zip).
* Follow the [**instructions**](README_switch.md).

## Snapshots (Latest Builds)

You can download the precompiled binaries of the latest commit (snapshot)

| Platform Version | Release                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------|
| Windows x64 SDL2 | [fheroes2-windows-x64-SDL2](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-windows-x64-SDL2)     |
| Windows x86 SDL2 | [fheroes2-windows-x86-SDL2](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-windows-x86-SDL2)     |
| macOS x86-64     | [fheroes2-osx-sdl2_dev](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-osx-sdl2_dev)             |
| Ubuntu x86-64    | [fheroes2-linux-sdl2_dev](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-linux-sdl2_dev)         |
| Ubuntu ARM       | [fheroes2-linux-arm-sdl2_dev](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-linux-arm-sdl2_dev) |
| Android          | [fheroes2-android](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-android)                       |
| PlayStation Vita | [fheroes2-psv-sdl2_dev](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-psv-sdl2_dev)             |
| Nintendo Switch  | [fheroes2-switch-sdl2_dev](https://github.com/ihhub/fheroes2/releases/tag/fheroes2-switch-sdl2_dev)       |

**These binaries incorporate all the latest changes, but also all the latest bugs, and are mainly intended for developers.**

**DON'T EXPECT THEM TO WORK PROPERLY.**
