# RPC Wine [![CI](https://img.shields.io/circleci/project/github/Marc3842h/rpc-wine.svg)](https://circleci.com/gh/Marc3842h/rpc-wine)

`discord-rpc.dll` implementation for Wine allowing your Wine games to interact
with your native Discord instance.

## Installation

Some users have provided distro packages for this library:

* Arch Linux: [`discord-rpc-wine-git`](https://aur.archlinux.org/packages/discord-rpc-wine-git/) by @999eagle

If your distro isn't listed above, the library can still
be installed with a few simple steps.

#### Dependencies

Install the following dependencies, they are required for either building
or running RPC Wine:

* make
* wine-devel (including `winegcc` and headers)
* RapidJson

#### Building

After installing dependencies and cloning the repository, the `build.sh`
can be used to build both a 32-bit aswell as a 64-bit version of this library.
The resulting binaries can be found in the `bin32` respectively the `bin64` directory
in the source tree.

#### Setup in Wineprefix

Append to the `WINEDLLPATH` environment variable both the `bin32` and
`bin64` directory containing the built library.

Then configure your Wineprefix (`winecfg`) to add `discord-rpc`
(without `.dll` extension) to the DLL overrides list:

![winecfg](https://wontfix.club/i/UUusAV3s.png)

and mark it to prefer the Builtin version over the native one:

![winecfg edit override](https://wontfix.club/i/ihlrxiAp.png)

## Restrictions

RPC Wine currently has not all Discord-RPC methods implemented. This will
be solved with future updates. However, there are other problems with RPC Wine:

RPC Wine is **not** able to run by design:

* Games which don't use the native `discord-rpc.dll` library but their own or a third-party wrapper.
* Games with statically linked `discord-rpc.dll`


Press J to jump to the feed. Press question mark to learn the rest of the keyboard shortcuts
Log In
Sign Up
1
Enabling Discord RPC
guide
1
Posted byu/momitsreddit
29 days ago
Enabling Discord RPC
guide
Enabling Discord RPC for games under Wine/Proton

Since Wine doesn't offer a "native" interface for games running under it to connect to the Discord Rich Presence listener on Linux, here's a short guide on how to make RPC work.

I used this method on Manjaro 20.2.1 'Nibia,' though it should work the same on all other distros too.
Requirements

    [x] An internet connection

    [x] Wine/Proton already set up with winetricks/protontricks installed

    [x] This tarball by Marc3842h

    [x] A Terminal

How-to

    Download the tarball and extract it to a folder. You can extract it anywhere, but I'll be using /opt/discord-rpc

    Make sure you have the bin64 and the bin32 folders in /opt/discord-rpc

    Open a terminal and append the locations of the bin64 and bin32 folders to the WINEDLLPATH environment variable using the following command export WINEDLLPATH=$WINEDLLPATH:/opt/discord-rpc/bin64:/opt/discord-rpc/bin32

    Run winetricks/protontricks, select your wine prefix (default prefix if using protontricks), and run winecfg

    Head to the libraries tab, and add a new override for library by typing in discord-rpc and clicking add. Hit Apply, and then OK

    Run your game the way you usually would, and RPC should be working now
