# base16-gtk-flatcolor
This is a [Base16](https://github.com/chriskempson/base16) template for [FlatColor](https://github.com/jasperro/FlatColor), a gtk theme by jasperro and deviantfero,

## Usage
First download FlatColor theme from jasperro's repo to your .themes folder:
`git clone https://github.com/jasperro/FlatColor ~/.themes`

Before anything, you need to make a few changes in FlatColor so the base16 builder of your choice can inject to it. 

Navigate to `~/.themes/FlatColor/gtk-2.0` and open `gtkrc` with your favorite text editor.

Delete `gtk-color-scheme` and everything inside quotes following it (so keep gtk-auto-mnemonics), and replace with:
```
# %%base16_template: gtk-flatcolor##gtk-2 %%
# %%base16_template_end%%
```

Now move on to `.~/.themes/FlatColor/gtk-3.0`, and open `gtk.css`.

Delete all in lines in section `/* Default color scheme */`, and replace with:
```
/* %%base16_template: flat-color##gtk-3 %%
/* %%base16_template_end%%
*/
```
(The comments look weird, blame CSS, but they will work nicely after injection)

Do the same as above, but with `.~/.themes/FlatColor/gtk-3.20`'s `gtk.css`.

Now using your injector (if you don't have one, check out [InspectorMustache's](https://github.com/InspectorMustache/base16-builder-python), it includes steps on how to use it as well), inject to those 3 files you edited (plus any other you use with Base16's templates) and voila! Now your gtk theme matches with your chosen Base16 scheme.

*Tip*: Most gtk apps only update when restarted, but you can use `gsettings` to change to some theme, and back to FlatColor so all applications re-theme without restart (Thanks jasperro for the [workaround](https://github.com/deviantfero/wpgtk/issues/112))

Here's how i do it:

First create a dummy theme as a symlink to FlatColor (so your theme doesn't flashes when changinng):
```
ln -Ts ~/.themes/FlatColor ~/.themes/dummy
```

And then use this command to reload:
```
gsettings set org.gnome.desktop.interface gtk-theme dummy && gsettings set org.gnome.desktop.interface gtk-theme FlatColor
```

If nothing happens, make sure `/usr/lib/gsd-xsettings` is running. You can include that in your WM's configuration so it starts automatically. You do need some gnome packages installed, though.
