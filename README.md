# Update from Raspberry Pi OS Debian bookworm to trixie
In-place update from Raspberry Pi OS bookworm to trixie (according to https://forums.raspberrypi.com/viewtopic.php?t=389477 and other sources)

```bash
sudo apt purge -y raspberrypi-ui-mods
sudo dpkg -P lxplug-batt
sudo dpkg -P lxplug-cpu
sudo apt autoremove -y

sudo sed -i.bak 's/bookworm/trixie/g' /etc/apt/sources.list /etc/apt/sources.list.d/*.list
sudo apt update
## I prefer to do the upgrade interactively
sudo apt full-upgrade --purge --auto-remove
```

Now, execute for every prompt:
1. At dpkg prompt, choose 'Z'.
2. In parallel SSH session run ```diff -u /etc/foo.conf /etc/foo.conf.dpkg-dist```.
3. In 'Z' shell edit maintainer's new  ```/etc/foo.conf.dpkg-dist```, add your tweaks and mark them.
4. Test syntax using the edited .dpkg-dist.
5. Exit 'Z' and, back at prompt, choose install maintainer’s version.

Thus, we have
* ```/etc/foo.conf``` now = new baseline + your edits.\
* ```/etc/foo.conf.dpkg-old``` = your old Bookworm file.

Alternatively, you may want to make it silent and automatic with\
```bash
#sudo apt full-upgrade -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confnew" --purge --auto-remove
```

Lastly, you can add ```rpd-applications```, ```rpd-common```, ```rpd-developer```, ```rpd-graphics```, ```rpd-plym-splash```, ```rpd-preferences```, ```rpd-theme```, ```rpd-utilities```, ```rpd-wallpaper*```, ```rpd-wayland-*```, ```rpd-x-*``` to your liking

End with ```sync``` to be extra safe.
