# Post Installation Bits

## Start Up

With the ventoy media not plugged in, reboot / turn the machine on.

## Updating

Somehow kept getting hash checksum errors during `apt get update`.

One thing that seemed to work was doing:

```
sudo rm -rf /var/lib/apt/lists/*
sudo apt-get update -o Acquire::CompressionTypes::Order::=gz
```

and then proceeding as normal.

Various other methods are described [here](https://askubuntu.com/questions/41605/trouble-downloading-packages-list-due-to-a-hash-sum-mismatch-error).

historical note: it may have been that [the timing was unlucky](https://askubuntu.com/a/1555547).

## Disable IPv6

Disable IPv6 via grub.  Edit `/etc/default/grub` so it has:
  
```
GRUB_CMDLINE_LINUX="ipv6.disable=1"
```

then `sudo update-grub` to update grub.
  
Note that `update-grub2` is a symlink to `update-grub` -- either should give
the same results

## `$HOME/.local`

Make the `~/.local` directory available for per-user software
installation (to be done later): `mkdir ~/.local`

Nicer to do now because logging back in / rebooting makes things more
straight-forward.

## Add Additional Users

* Add additional users if neceesary via `users-admin` (or "Users and
  Groups" via the text field that comes up when the mint logo at the
  left of the panel is clicked).
  
* Use `vigr` and `vigr -s` to add users to the `sudo` group if needed
  (for `sudo` use) -- possibly might want to add to other groups too.
  depends on one's uses.

## Disabling Network Services

* Follow steps
  [here](https://gist.github.com/sogaiu/a824178f1a2f62a6a77815c3693917ef#finish-setup)
  to disable unwanted network services.
  
  Use `sudo netstat -tunlp` to check what is running:
  
    ```
    $ sudo netstat -tunlp
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
    tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      576/systemd-resolve 
    tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      966/cupsd           
    tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      576/systemd-resolve 
    udp        0      0 0.0.0.0:5353            0.0.0.0:*                           666/avahi-daemon: r 
    udp        0      0 0.0.0.0:53118           0.0.0.0:*                           666/avahi-daemon: r 
    udp        0      0 127.0.0.54:53           0.0.0.0:*                           576/systemd-resolve 
    udp        0      0 127.0.0.53:53           0.0.0.0:*                           576/systemd-resolve 
    ```

* Reboot and check via `sudo netstat -tunlp` to see:

    ```
    $ sudo netstat -tunlp
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
    ```

## Packaged Software Additions and Removals

* `sudo apt install vlc handbrake gimp qemu-kvm`

* `sudo apt remove firefox thunderbird transmission-gtk hypnotix rhythmbox`

