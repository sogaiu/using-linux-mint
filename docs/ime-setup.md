# Input Method Editor Configuration

Linux Mint seems to prefer fcitx over ibus...may be it makes sense to
use fcitx eventually.  Below are instructions for ibus for the moment.

## Add Various Japanese, Korean, etc. IMEs

In any case, via "Settings Manager":

* Choose "Input method"

* Select desired language on left pane (if multiple desired, do one at a time)

* In the right pane, click on "Install" button.

* Follow the rest of the instructions, though choosing "IBus" for the
  drop-down labeled "Input method framework" at the top seems to also
  work.

* Before logging out and back in, may want to run `ibus-setup` from
  a terminal and do some configuration.

* May also want to add following to `~/.bashrc`:

    ```
    export GTK_IM_MODULE=ibus
    export XMODIFIERS=@im=ibus
    export QT_IM_MODULE=ibus
    ```

## Add English IME

Having an English IME may be handy for switching among different IMEs.
That may allow one to dispense with each individual IME's method of
providing "Latin" / "Roman" input.

* Right-click the IBus (tray applet?) and choose "Preferences"

* Choose the "Input Method" tab

* Click the "Add" button on the right side

* From the resulting dialog, choose "English"

* Select one of the "English (...)" items

* Click on the "Add" button

## Disable Unwanted Key Bindings

Some of the default key bindings may interfere with other settings.
Disabling is one way to reduce confusion and/or unwanted feature
activation.

* Right-click the IBus (tray applet?) and choose "Preferences"

* Choose the "Emoji" tab

* Click on the "..." button to the right of "Emoji annotation"
  and "Unicode code point" (one at a time)

* Delete existing key bindings

* Click the "OK" button

May need to repeat some of the operations above to delete remaining
key bindings as after deleting one, remaining ones may for some reason
not be accessible.

## Make Mozc Use Hiragana as Default

If "Japanese" was a chosen IME, likely Mozc was what was available.
Unfortunately, Mozc seems to default to "ro-maji" (roughly speaking,
ASCII) input and there doesn't appear to be a way to configure this
via a GUI.

Edit `~/.config/mozc/ibus_config.textproto` so that it has:

```
active_on_launch: True
```

References:

* https://askubuntu.com/a/890376
* https://wiki.archlinux.org/title/Mozc#Configuration
* https://github.com/google/mozc/blob/master/docs/configurations.md

