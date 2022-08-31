# krita-patched

This is an unofficial Arch Linux package (the official one is
[here](https://archlinux.org/packages/extra/x86_64/krita/)) for https://krita.org,
containing a patch for a [window-focus related bug](https://bugs.kde.org/show_bug.cgi?id=428080).
The [patch](https://github.com/Luminiscental/krita-patched/blob/main/key-focus.patch)
just removes a small block of input-handling code, as described in the bug thread.
