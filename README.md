# nvidia-graphics-on-linux
It can be such a pain

# Laptops with Hybrid GPUs (NVIDIA and Intel)

## Fedora
1. Follow instructions from https://github.com/gridhead/nvidia-auto-installer-for-fedora-linux
2. Use envycontrol (dnf install python3-envycontrol): `sudo envycontrol --use-nvidia-current -s nvidia --force-comp`

If using SDDM:
1. Edit `/etc/sddm.conf` and set line `DisplayServer` to `x11`
2. Edit `/etc/sddm/Xsetup` and append lines `xrandr --setprovideroutputsource modesetting NVIDIA-G0` and `xrandr --auto`
3. Reboot

SDDM should show up, else if not, there is a problem.  I use glmark2 to test if the default/primary GPU reports NVIDIA.

## Ubuntu
1. `sudo add-apt-repository ppa:graphics-drivers/ppa`
2. `sudo apt update`
3. `sudo apt install nvidia-drivers-XXX`
4. Go to the nvidia settings panel, make NVIDIA the default under power settings, then reboot
