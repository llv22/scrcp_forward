# Compiling and fixing issue on Android 14

## Compile locally after FFmpeg has been configured

```bash
echo $PKG_CONFIG_PATH # check library path
meson setup x --buildtype=release --strip -Db_lto=true # release model
meson setup x --reconfigure -Dserver_debugger=true # start to debugging

ninja -Cx
sudo ninja -Cx install    # without sudo on Windows
cp /Users/llv23/Documents/05_machine_learning/02_phd/1_flow_action/2_screen_to_web/scrcpy/x/server/scrcpy-server /Users/llv23/Documents/05_machine_learning/02_phd/1_flow_action/PlanForAndroidOnline/asynch/scrcpy-server-v2.4
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
scrcpy --video-codec=h264 --max-size=1920 --max-fps=60 --no-audio --keyboard=uhid

adb shell CLASSPATH=/data/local/tmp/scrcpy-server-manual.jar \
    app_process / com.genymobile.scrcpy.Server 2.4 \
    tunnel_forward=true audio=false control=false cleanup=false \
    raw_stream=true max_size=1920
```

## Check new option from java/com/genymobile/scrcpy/Options.java and change for [PlanForAndroidOnline](https://github.com/llv22/PlanForAndroidOnline/blob/develop/asynch/controller.py)

Already updated with protocol for Android 2.4

## Build for release

```bash
bash release.sh
```