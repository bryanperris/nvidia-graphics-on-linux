# nvidia-graphics-on-linux
It can be such a pain

# Laptops with Hybrid Graphics (NVIDIA and Intel)

## Fedora
### Forcing NVIDIA to be the default GPU for X11
1. Follow instructions from https://github.com/gridhead/nvidia-auto-installer-for-fedora-linux
2. Use envycontrol (dnf install python3-envycontrol): `sudo envycontrol --use-nvidia-current -s hybrid --force-comp`

If using SDDM:
1. Edit `/etc/sddm.conf` and set line `DisplayServer` to `x11` (If you want to avoid using wayland)
2. Edit `/etc/sddm/Xsetup` and append lines `xrandr --setprovideroutputsource modesetting NVIDIA-0` (it could be also called NVIDIA-G0) and `xrandr --auto`
3. Reboot

* Note: Make sure PRIME offloading is enabled, else X11 on an external display really lags ~1FPS
* Use glmark2 to check the default GPU
Known issues:
* SDDM on external monitor may look a bit funny, like duplicate wallpapers at different sizes, just a cosmetic issue

### Using the Hybrid model under Wayland [Intel HD/NVIDIA]
1. Allow your login manager to start with wayland
2. Login into your wayland based DE
3. for your shell create a `prime-run` alias: `alias prime-run="__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia"`
4. By default apps will render to Intel, run the app with `prime-run` to use the NVIDIA GPU instead (tested this works under wayland)

Known issues:
* Wayland rendering on Intel to an external display feels less responsive than X11 on NVIDIA, this could be a sync issue since the HDMI port is probably only wired to the NVIDIA GPU.
* WineD3D has an issue with wayland, such as the `D3DERR_CONFLICTINGRENDERSTATE` error, at least with D3D7, with D3D8/9/10/11/12, one can simply use a vulkan wrapper

## Ubuntu
1. `sudo add-apt-repository ppa:graphics-drivers/ppa`
2. `sudo apt update`
3. `sudo apt install nvidia-drivers-XXX`
4. Go to the nvidia settings panel, make NVIDIA the default under power settings, then reboot
