# Simple Terminal Config (taken from Luke Smith)

The [suckless terminal (st)](https://st.suckless.org/) with some additional
features that make it literally the best terminal emulator ever:

## Unique features (using dmenu)

+ **follow urls** by pressing `alt-l`
+ **copy urls** in the same way with `alt-y`
+ **copy the output of commands** with `alt-o`

## Bindings for

+ **scrollback** with `alt-↑/↓` or `alt-pageup/down` or `shift` while scrolling the
  mouse.
+ OR **vim-bindings**: scroll up/down in history with `alt-k` and `alt-j`.
  Faster with `alt-u`/`alt-d`.
+ **zoom/change font size**: same bindings as above, but holding down shift as
  well. `alt-home` returns to default
+ **copy text** with `alt-c`, **paste** is `alt-v` or `shift-insert`

## Pretty stuff

+ Compatibility with `Xresources` and `pywal` for dynamic colors.
+ Transparency/alpha, which is also adjustable from your `Xresources`.
+ Default font is system "mono" at 30pt, due to HiDPI, meaning the font will match your
  system font.

## Other st patches

+ Boxdraw
+ Ligatures
+ font2
+ updated to latest version 0.8.5

## Installation for newbs

You should have xlib header files and libharfbuzz build files installed.

```
git clone https://github.com/LukeSmithxyz/st
cd st
sudo make install
```

Obviously, `make` is required to build. `fontconfig` is required for the
default build, since it asks `fontconfig` for your system monospace font. It
might be obvious, but `libX11` and `libXft` are required as well. Chances are,
you have all of this installed already.

On OpenBSD, be sure to edit `config.mk` first and remove `-lrt` from the
`$LIBS` before compiling.

Be sure to have a composite manager (`xcompmgr`, `picom`, etc.) running if you
want transparency.

## How to configure dynamically with Xresources

For many key variables, this build of `st` will look for X settings set in
either `~/.Xdefaults` or `~/.Xresources`. You must run `xrdb` on one of these
files to load the settings.

For example, you can define your desired fonts, transparency or colors:

```
*.font:	Liberation Mono:pixelsize=12:antialias=true:autohint=true;
*.alpha: 0.9
*.color0: #111
...
```

The `alpha` value (for transparency) goes from `0` (transparent) to `1`
(opaque). There is an example `Xdefaults` file in this respository.

### Colors

To be clear about the color settings:

- This build will use gruvbox colors by default and as a fallback.
- If there are Xresources colors defined, those will take priority.
- But if `wal` has run in your session, its colors will take priority.

Note that when you run `wal`, it will negate the transparency of existing windows, but new windows will continue with the previously defined transparency.
