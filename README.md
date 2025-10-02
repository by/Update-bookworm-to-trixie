# Update-bookworm-to-trixie
In-place update from Raspberry Pi OS bookworm to trixie (according to https://forums.raspberrypi.com/viewtopic.php?t=389477 and other sources)

```bash
sudo apt purge -y raspberrypi-ui-mods
## Make sure that you have purged
#sudo dpkg -P raspberrypi-ui-mods 
#sudo dpkg -P lxplug-batt
#sudo dpkg -P lxplug-cpu
#sudo apt autoremove -y

sudo sed -i.bak 's/bookworm/trixie/g' /etc/apt/sources.list /etc/apt/sources.list.d/*.list
sudo apt update
sudo apt full-upgrade -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confnew" --purge --auto-remove
sync
```
