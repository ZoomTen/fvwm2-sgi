# FVWM2-SGI

This is a FVWM2 theme that simulates the look and feel of the default window manager in Silicon Graphics systems, 4DWM. Or at least, my take on it anyway.

## What it comes with

* Vector button layout
* Pixmap iconbox to provide a "irix-like" overlaay
* Toolchest for accessing standard tools
* Full range of icons (iconbox and launchers) ripped from various screenshots, icon themes and the [MaXX Interactive Desktop](https://maxxinteractive.com)

## Setup

### What you need

Basic stuff:

* Xorg fonts (can be found under `xfonts-75dpi` or `xorg-fonts-75dpi`)
* `stalonetray` (for desktop tray)
* `xclock` (digital clock)
* `exo-open` (if you're on a modern linux system, I assume this will be available)
* `expr` (should be available with gnu coreutils)

Thumbnailing:

* `xwd`
* ImageMagick (`convert`)

`hsetroot` is used for background images. If this is unavailable, it will fallback onto a blue background set using `xsetroot`.

Support for `panther_launcher` is added by default in the submenus as "All Apps"

### Installing

```
git clone https://github.com/zoomten/fvwm2-sgi
```

Then, either:

* Copy the contents of the resulting `fvwm2-sgi` folder into your home directory
* Use [GNU stow](https://www.gnu.org/software/stow), assuming you cloned the repo into your `stow` package directory, and then do `stow -v 2 fvwm2-sgi`.

### Setting up virtual desktops

In FVWM, virtual desktops can have virtual "pages" - that is, extending the size of your screen and splitting it into individual pages. This can be configured using the **DesktopSize** option in `~/.fvwm/config`.

You can set desktop names right below that option. 3 desktops will have been defined as-cloned. To add another, add a line `AddDesktop "desktop_name_here"`, it will automatically reflect on the pager. However, you will need to adjust your keybindings.

### Setting up autostart

Here, these are simply `.desktop` files inside the `autostart` folder that relies on `exo-open`. Simply find the application you want to autostart with FVWM in `/usr/share/applications` (or its user equivalent in `~/.local/share/applications`) and then paste it into the folder.

There are also additional applications autostarted within `~/.fvwm/config` by default:

* `xclock` for a sticky digital clock.
* `stalonetray` for storing tray icons.
* `xfsettingsd`, to load fonts, keybinding and screen configurations set within XFCE
* `xfce4-power-manager`
* `hsetroot` or `xsetroot`, for desktop wallpaper.

### Setting up keybindings

Keybindings can be configured within `~/.fvwm/keyboard.fvwm2rc` and `~/.fvwm/mouse.fvwm2rc`.

For now, refer to the [FVWM documentation](https://www.fvwm.org/Wiki/Config/Bindings/) to figure out how to set them.

### Make certain apps iconify to a thumbnail

Near the end of the keybinding configuration there are overrides specifically set aside for the Chromium web browser, so that when any of its windows are iconified, it will display the thumbnail of the window instead of showing its icon.

If you want to add a configuration for e.g. Firefox, add these lines:

in keyboard.fvwm2rc
```
Key ("Firefox") M	W	4 Thumbnail
Key ("Firefox") M	I	4 DeThumbnail
```

in mouse.fvwm2rc
```
Mouse ("Firefox") 1		I       A       DeThumbnail
Mouse ("Firefox") 0		4    	A     	Thumbnail
```

The name of the string inside the parentheses can be found out using FvwmIdentify, accessed through right-clicking on the desktop -> Identify -> click on a window. Its name will be listed under `Class:`.

### Change to dark mode

Main window colors, etc. can be found under `~/.fvwm/components/colors.fvwm2rc`. A basic "dark mode" theme has been included, uncomment it to switch to dark mode.

### Customizing iconified application images

Can be configured under `~/.fvwm/components/icons.fvwm2rc`. All icon images are relative to `~/.fvwm/icons`. When adding an icon, don't forget to specify `IconOverride`, just in case the application has its own icon. Use FvwmIdentify to figure out the correct class name.

### Adding desktop icons

Desktop icons ("launchers") configuration can be found under `~/.fvwm/components/desktop_launchers.fvwm2rc`. You can add as many icons as you like, adding columns manually if need be.

Don't forget to adjust the iconbox size in `~/.fvwm/icons.fvwm2rc` though.

### Adding items to the menu

This theme does not use XDG menu integration, you may add that yourself if your FVWM2 distribution comes with `fvwm-menu-desktop`, output the resulting file somewhere in `~/.fvwm/menus`, include that in `config` just before the root menu file (`~/.fvwm/menus/root.fvwm2rc`) and then modify the root menu file to pop up one of the resulting menus.

Otherwise, you can edit `~/.fvwm/menus/submenus.fvwm2rc` to modify the submenus that appear as you right click the desktop (and in the "Toolchest").

You can also edit the window operations menu in `~/.fvwm/menus/window_ops.fvwm2rc`

### Setting up GTK3 integration

Add this line into your `~/.config/gtk-3.0/gtk.css`:

```css
@import url("4dwmlike-font-integration.css");
```

### Setting up X11 integration

Add the following lines into your `~/.Xresources` (you will need a C++ preprocessor for this):

```
#include ".config/Xresources.d/nedit"
#include ".config/Xresources.d/xnedit"
#include ".config/Xresources.d/xosview"
```

## Links

* [original fvwm2 config](https://datagubbe.se/fvwm/config.txt)
* [IndigoMagic gtk3 theme](https://www.gnome-look.org/p/1371886/), for better results

