# Compiling and fixing issue on Android 14

## Compile locally after FFmpeg has been configured

```bash
echo $PKG_CONFIG_PATH # check library path
meson setup x --buildtype=release --strip -Db_lto=true
ninja -Cx
sudo ninja -Cx install    # without sudo on Windows
```

This installs several files:

/usr/local/bin/scrcpy (main app)
/usr/local/share/scrcpy/scrcpy-server (server to push to the device)
/usr/local/share/man/man1/scrcpy.1 (manpage)
/usr/local/share/icons/hicolor/256x256/apps/icon.png (app icon)
/usr/local/share/zsh/site-functions/_scrcpy (zsh completion)
/usr/local/share/bash-completion/completions/scrcpy (bash completion)
You can then run scrcpy.

uninstall via bash

```bash
sudo ninja -Cx uninstall  # without sudo on Windows
```

## Check built files in folder x/

```bash
scrcpy --video-codec=h265 --max-size=1920 --max-fps=60 --no-audio --keyboard=uhid
```
