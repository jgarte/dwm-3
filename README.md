My dwm
---
A Dynamic Window Manager

dwm is an extremely fast, small, and dynamic window manager for X.
It is written with the [suckless philosophy][15]
in mind and is objectively one of the best window managers out there.

## What my build has to offer
I have patched dwm extensively using official  patches but also with the
awesome patches [Floris Laporte][16] makes for his own build to
make the experience more enjoyable. Here are the following patches which I
installed:

- [dwm-activetagindicatorbar-6.2][1]
- [dwm-alpha-20180613-b69c870][2]
- [dwm-bar-height-6.2][3]
- [dwm-centeredmaster-6.1][4]
- [dwm-dwmc-6.2][5]
- [dwm-focusmaster][6]
- [dwm-fullscreen][7]
- [dwm-gaplessgrid-20160731-56a31dc][8]
- [dwm-libxft-bgra][9]
- [dwm-movestack-6.1][10]
- [dwm-rotatestack-20161021-ab9571b][11]
- [dwm-statuscmd-signal-6.2][21]
- [dwm-tilegap][12]
- [dwm-zoomswap-6.2][13]
- [flaport-center][14]
- [flaport-mastermon][14]
- [flaport-swallow][14]

So that's a nice list... But what does it actually mean?  Here are the main
points that make my build stand out.

**Decentralized keybindings:**

So if I have a piece of software that does one thing and does it well, why
would I use anything else. I personally use the *Simple X Hotkey Daemon*
([SXHKD][17]) to manage all my keybindings and dwm should be no exception.
That's why I use the [dwmc][5] patch to allow sxhkd to control dwm.

For this reason, I highly recommend you take a look at my [dotfiles][18]
repository as it contains my current configuration for sxhkd. **This build
of dwm is basically unusable until you have sxhkd setup for it.** This also
means sxhkd should be launched along dwm inside your `.xinitrc`. As a bonus,
if you install this build of dwm with my dotfiles using [archer][19], you
can press `super + alt + shift + h` to view a procedurally generated pdf of
all my keybindings.

**Window swallowing:**

This is a feature which allows terminals to "transform" themselves into the
software they are launching (essentially saving screen real estate). For
example: If I were to open a video inside mpv from my terminal, the terminal
window would disapear and where it once was, mpv would appear.

**Aesthetics:**

I love transparency and that's why I added the [alpha][2] patch to my build.
While I was at it, I switched the standard corner square bar indicator for a
centered rectangle on each tag using the [activetagindicatorbar][1] patch.
Most fonts don't play well with it so I added the [bar-height][3] patch to make
the bar taller. I don't like to have gaps everywhere, but I don't dislike them
either. Therefore, I only added them to the tiling layout (which is where they
make the most sense).

**Emoji Compatibility:**

Some Suckless software have a frustrating tendency of crashing when
encountering color emoji. This got fixed with the [libxft-bgra][9] patch.  I'm
not the greatest fan of emojis (I personally prefer the fontawesome fonts for
icons), but in the unlikely event that one makes it's way to my statusbar, it
will not crash.

**dwmblocks compatibility:**

I personnally have a personal build of [dwmblocks][20] which is capable of
handling click events. For that to work, I had to add the
[statuscmd-signal][21] patch.

**Accessible stack navigation and manipulation:**

I don't want to spend half an hour placing a window where I want in in the
stack. I need a suite of functions aiding me to do certain motions
either to position windows or navigate through them:

- [Rotatestack][11]: Rotate the entire stack (clockwise/couterclockwise).
- [Movestack][10]: Move the current window up or down the stack.
- [FocusMaster][6]: Focus the master window (the last spawned window).
- [ZoomSwap][13]: Swap the master window with the currently focused one.

**Diverse but consise tiling modes:**

I'm not a fan of having so many tiling modes I need a patch just to switch
through all of them. I only included those I found usefull on a day to day
basis. The following schematics will showcase these (1 being the newest
spawned window):

```
                           Tile (Regular):
┌───────────────────────────────┐┌────────────────────────────────┐
│ 1                             ││ 2                              │
│                               ││                                │
│                               │└────────────────────────────────┘
│                               │┌────────────────────────────────┐
│                               ││ 3                              │
│                               ││                                │
│                               │└────────────────────────────────┘
│                               │┌────────────────────────────────┐
│                               ││ 4                              │
│                               ││                                │
│                               │└────────────────────────────────┘
│                               │┌────────────────────────────────┐
│                               ││ 5                              │
│                               ││                                │
│                               │└────────────────────────────────┘
│                               │┌────────────────────────────────┐
│                               ││ 6                              │
│                               ││                                │
└───────────────────────────────┘└────────────────────────────────┘

                          Centered Master:
┌───────────────┐┌───────────────────────────────┐┌───────────────┐
│ 3             ││ 1                             ││ 2             │
│               ││                               ││               │
└───────────────┘│                               │└───────────────┘
┌───────────────┐│                               │┌───────────────┐
│ 5             ││                               ││ 4             │
│               ││                               ││               │
└───────────────┘│                               │└───────────────┘
┌───────────────┐│                               │┌───────────────┐
│ 7             ││                               ││ 6             │
│               ││                               ││               │
└───────────────┘│                               │└───────────────┘
┌───────────────┐│                               │┌───────────────┐
│ 9             ││                               ││ 8             │
│               ││                               ││               │
└───────────────┘│                               │└───────────────┘
┌───────────────┐│                               │┌───────────────┐
│ 11            ││                               ││ 10            │
│               ││                               ││               │
└───────────────┘└───────────────────────────────┘└───────────────┘

                     Floating Centered Master:
┌───────────────┐┌───────────────┐┌───────────────┐┌───────────────┐
│ 2             ││ 3             ││ 4             ││ 5             │
│               ││               ││               ││               │
│             ┌──────────────────────────────────────┐             │
│             │ 1                                    │             │
│             │                                      │             │
│             │                                      │             │
│             │                                      │             │
│             │                                      │             │
│             │                                      │             │
│             │                                      │             │
│             │                                      │             │
│             │                                      │             │
│             └──────────────────────────────────────┘             │
│               ││               ││               ││               │
│               ││               ││               ││               │
│               ││               ││               ││               │
│               ││               ││               ││               │
│               ││               ││               ││               │
└───────────────┘└───────────────┘└───────────────┘└───────────────┘

                           Gappless Grid:
┌───────────────┐┌───────────────┐┌───────────────┐┌───────────────┐
│ 1             ││ 5             ││ 9             ││ 13            │
│               ││               ││               ││               │
│               ││               ││               ││               │
└───────────────┘└───────────────┘└───────────────┘└───────────────┘
┌───────────────┐┌───────────────┐┌───────────────┐┌───────────────┐
│ 2             ││ 6             ││ 10            ││ 14            │
│               ││               ││               ││               │
│               ││               ││               ││               │
└───────────────┘└───────────────┘└───────────────┘└───────────────┘
┌───────────────┐┌───────────────┐┌───────────────┐┌───────────────┐
│ 3             ││ 7             ││ 11            ││ 15            │
│               ││               ││               ││               │
│               ││               ││               ││               │
└───────────────┘└───────────────┘└───────────────┘└───────────────┘
┌───────────────┐┌───────────────┐┌───────────────┐┌───────────────┐
│ 4             ││ 8             ││ 12            ││ 16            │
│               ││               ││               ││               │
│               ││               ││               ││               │
└───────────────┘└───────────────┘└───────────────┘└───────────────┘

```
There are 3 more layout which don't require drawings:
- Fullscreen
- Monocle: Windows are stacked one over the over in "fullscreen"
  (the statusbar remains).
- Floating: Windows don't respond to any tiling function and simply
  spawn in the top left corner (they remain in place coming from
	another tiling function).

## Requirements
In order to build dwm you need the Xlib header files.


## Installation
Edit config.mk to match your local setup (dwm is installed into
the /usr/local namespace by default).

Afterwards enter the following command to build and install dwm (if
necessary as root):
```
    make clean install
```

## Running dwm
Add the following line to your .xinitrc to start dwm using startx:
```
    exec dwm
```

## Configuration
The configuration of dwm is done by creating a custom config.h
and (re)compiling the source code.


[1]:  https://dwm.suckless.org/patches/activetagindicatorbar/
[2]:  https://dwm.suckless.org/patches/alpha/
[3]:  https://dwm.suckless.org/patches/bar_height/
[4]:  https://dwm.suckless.org/patches/centeredmaster/
[5]:  https://dwm.suckless.org/patches/dwmc/
[6]:  https://dwm.suckless.org/patches/focusmaster/
[7]:  https://dwm.suckless.org/patches/fullscreen/
[8]:  https://dwm.suckless.org/patches/gaplessgrid/
[9]:  https://youtu.be/f9qNXV01yzg
[10]: https://dwm.suckless.org/patches/movestack/
[11]: https://dwm.suckless.org/patches/rotatestack/
[12]: https://dwm.suckless.org/patches/tilegap/
[13]: https://dwm.suckless.org/patches/zoomswap/
[14]: https://github.com/flaport/dwm
[15]: https://suckless.org/philosophy/
[16]: https://github.com/flaport
[17]: https://github.com/baskerville/sxhkd
[18]: https://git.chausse.xyz/dotfiles/
[19]: https://git.chausse.xyz/archer/
[20]: https://git.chausse.xyz/dwmblocks/
[21]: https://dwm.suckless.org/patches/statuscmd/
