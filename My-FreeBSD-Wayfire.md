# Install Wayfire under FreeBSD

If you prefer a more standard desktop envirnment, here is how I got Wayfire running under FreeBSD. The first step of course is getting the proper graphics firmware.
This command install the firmware needed

    pkg install drm-kmod

This makes sure proper driver get loaded at boot. For AMD graphics

    sysrc kld_list+=amdgpu

and for intel graphics

    sysrc kld_list+=i915kms

This adds the user to the video group which allows direct access to the video hardware

    pw groupmod video -m user


Install the basic packages needed for Wayland

    pkg install wayland seatd

The following is needed to make sure Wayfire can operate properly.

    mkdir ~/.cache/run

    chmod 700 ~/.cache/run

add this lines to your .bashrc, .zshrc, .cshrc or whatever rc file for the shell you use and reboot.

    export XDG_RUNTIME_DIR=~/.cache/run
    alias wayfire='dbus-launch wayfire'

Next, we need to start the services needed for proper functioning of Wayfire.

    sysrc seatd_enable=”YES”

    service seatd start

    service seatd status

    sysrc dbus_enable="YES"

    service dbus start

    service dbus status

Next we install Wayfire.

    pkg install wayfire wf-shell alacritty swaylock-effects swayidle wlogout kanshi mako wlsunset

    mkdir ~/.config/wayfire

    cp /usr/local/share/examples/wayfire/wayfire.ini ~/.config/wayfire

Finally to run Wayfire:

    wayfire
