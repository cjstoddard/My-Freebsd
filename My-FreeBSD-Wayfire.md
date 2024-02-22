# Install Wayfire under FreeBSD

pkg install drm-kmod

sysrc kld_list+=amdgpu     #for AMD graphics

sysrc kld_list+=i915kms     #for intel graphics

pw groupmod video -m user

pkg install wayland seatd

mkdir ~/.cache/run

chmod 700 ~/.cache/run

add this line to your .bashrc or .zshrc file and reboot

export XDG_RUNTIME_DIR=~/.cache/run

sysrc seatd_enable=”YES”

service seatd start

service seatd status

sysrc dbus_enable="YES"

service dbus start

service dbus status


pkg install wayfire wf-shell alacritty swaylock-effects swayidle wlogout kanshi mako wlsunset

mkdir ~/.config/wayfire

cp /usr/local/share/examples/wayfire/wayfire.ini ~/.config/wayfire

To Run:

wayfire -c ~/.config/wayfire/wayfire.ini
