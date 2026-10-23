Android Utility (Linux rewrite) v1.0.0
=====================================================

INSTALL / RUN
-------------
  chmod +x AndroidUtility_v1.0.0-x86_64.AppImage   (if not executable)
  ./AndroidUtility_v1.0.0-x86_64.AppImage

That's it. The AppImage bundles its own Python 3.12 runtime,
mtkclient engine, adb and fastboot - no system installs needed.
Requires only: basic desktop libs + fuse2 (Arch: sudo pacman -S fuse2).
If your system lacks FUSE, run with --appimage-extract-and-run.

DATA FOLDER
-----------
The tool writes new logs, dumps and backups to the folder:
    <directory where the AppImage sits>/AndroidUtility.v200

If you drop this AppImage into "~/Desktop" (Área de trabalho), it will
REUSE your existing AndroidUtility.v200 working folder directly.
If the folder next to the AppImage cannot be created (read-only), it
falls back to ~/.local/share/AndroidUtility.v200.

WHAT IS IMPLEMENTED (v1)
------------------------
ADB tab:
  device list/serial targeting, device info, install/uninstall APK,
  push to /sdcard, pull file, custom shell, reboot (system / bootloader /
  recovery / EDL), adb server start/kill.

Fastboot tab:
  device list, getvar info, flash image to partition, bootloader unlock /
  unlock_critical / oem unlock, factory reset (-w), reboots.

MTK tab (mtkclient engine - phone OFF in BROM mode, plug USB):
  print partition table, get target config, backup all partitions,
  read/write partition, read/write FULL flash dump, erase FRP,
  erase user data, bootloader unlock via seccfg, send BROM payload, reset.

NOT IMPLEMENTED YET (roadmap):
  Kirin/Hisilicon loader ops, Unisoc/SPD bootrom ops, Samsung Knox/MTP
  tricks, NV cryptographic operations. The original AndroidUtility.exe is
  NOT bundled here - this is a fresh, native rewrite.

LICENSES
--------
  App code: MIT.  mtkclient: GPLv3.
  platform-tools (adb/fastboot): Apache-2.0.
  Bundled Python runtime: PSF license (via python-appimage).
  Full texts in /usr/share/licenses inside the AppImage.

TROUBLESHOOTING
---------------
- "no permissions" for adb/fastboot device:
    sudo pacman -S android-udev        (Arch-based distros)
    or run the app once with sudo.
- MTK device not detected:
    power the phone OFF, hold both volume keys (BROM/preloader method),
    then plug the cable; some devices need the "Send BROM payload" button
    first. Check udev rules for MediaTek USB IDs.
- No window on Wayland:
    the app runs as an X11 (XWayland) session window; most desktops
    provide this automatically.
