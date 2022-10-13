# base16-gtk-flatcolor
This is a [Base16](https://github.com/tinted-theming/home) template for [FlatColor](https://github.com/jasperro/FlatColor), a gtk3 theme by jasperro and deviantfero,

## Usage
First download FlatColor theme from jasperro's repo to your .themes folder:
`git clone https://github.com/jasperro/FlatColor ~/.themes/FlatColor`

Before anything, you need to make a few changes in FlatColor so the base16 builder of your choice can inject to it. 

Open `~/.themes/FlatColor/gtk-2.0/gtkrc` with your favorite text editor.

Delete `gtk-color-scheme` and everything inside quotes following it, and replace with:
```
include "../colors2"
```

Now open `.~/.themes/FlatColor/gtk-3.0/gtk.css`.

Delete all in lines in section `/* Default color scheme */`, and replace with:
```
@import url("../colors3");
```
Do the same with `~/.themes/FlatColor/gtk-3.20/gtk.css`.

Now using your injector (if you don't have one, check out [flavours](https://github.com/misterio77/flavours)), and configure it so the template will be built to both `~/.themes/FlatColor/colors3` and `~/.themes/FlatColors/colors2`, using the subtemplates `gtk-2` and `gtk-3`, respectively.

*Tip*: Most gtk apps only update when restarted, but you can use `gsettings` or `xsettingsd` to change to some theme, and back to FlatColor so all applications re-theme without restart (Thanks jasperro for the [workaround](https://github.com/deviantfero/wpgtk/issues/112)). (If you use flavours, you can set that as an hook).

First of all, create a dummy theme as a symlink to FlatColor (so your theme doesn't flash when changing):
```
ln -Ts ~/.themes/FlatColor ~/.themes/dummy
```

Now here's the two ways to reload your theme:

#### [Xsettingsd](https://github.com/derat/xsettingsd)
After [installing](https://github.com/derat/xsettingsd/wiki/Installation) it, edit your `~/.xsettings` so it has the theme set:
```
Net/ThemeName "dummy"
```
Now just running `xsettings` should reload the theme! You can background the process, or make a systemd service to reload it more easily (check out my dotfiles if you want an example).

#### Gsettings (requires gnome packages)
Use this command to reload:
```
gsettings set org.gnome.desktop.interface gtk-theme dummy && gsettings set org.gnome.desktop.interface gtk-theme FlatColor
```

If nothing happens, make sure `/usr/lib/gsd-xsettings` is running. You do need some gnome packages installed, though.
