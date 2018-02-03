This is what I do when I install Arch Linux to improve the fonts.

You may consider the following settings to improve your fonts for system-wide usage without installing a patched font library packages (eg. Infinality):

Install some fonts, for example:

```bash
sudo pacman -S ttf-dejavu ttf-liberation noto-fonts
```

Enable font presets by creating symbolic links:

```bash
sudo ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d
sudo ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf /etc/fonts/conf.d
sudo ln -s /etc/fonts/conf.avail/11-lcdfilter-default.conf /etc/fonts/conf.d
```

The above will disable embedded bitmap for all fonts, enable sub-pixel RGB rendering, and enable the LCD filter which is designed to reduce colour fringing when subpixel rendering is used.

Enable FreeType subpixel hinting mode by editing:

```bash
/etc/profile.d/freetype2.sh
```

Uncomment the desired mode at the end:

```
export FREETYPE_PROPERTIES="truetype:interpreter-version=40"
```

For font consistency, all applications should be set to use the serif, sans-serif, and monospace aliases, which are mapped to particular fonts by fontconfig.

Create /etc/fonts/local.conf with following:

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match>
        <edit mode="prepend" name="family"><string>Noto Sans</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Noto Serif</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>sans-serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Noto Sans</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>monospace</string></test>
        <edit name="family" mode="assign" binding="same"><string>Noto Mono</string></edit>
    </match>
</fontconfig>
```

Set your font settings to match above in your DE system settings.
