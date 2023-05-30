# My-Freebsd

This is the process I go through to get a basic install of Freebsd with the programs I generally use. As a rule to be generally productive I need the following things; text editor, e-mail client, Web browser, file manager, calendar/to-do list.

I start with a basic install of FreeBSD, I pretty much take all the defaults, make sure you setup a normal user account.

Once I log in as root for the first time, I install all the text mode programs I use;

    pkg install sudo mc links neofetch cmus htop nano wget git zsh
    
This generally goes pretty quick. Next comes Xorg, I use emwm as my window manager. I Like to install all the things needed to make it work out of the box, with no configurations, plus the stuff I use.

    pkg install open-motif nedit gimp blender thunderbird mutt xedit xclipboard xmag bitmap xman xcalc xpdf gv xorg nomacs firefox-esr emacs audacious audacious-plugins
    
 Next I download and compile emwm, since it is not availble as a Freebsd package or in ports.
 
    cd /usr/src
    mkdir emwm
    cd emwm
    wget http://fastestcode.org/dl/emwm-src-1.1.tar.xz
    tar -xf emwm-src-1.1.tar.xz
    cd emwm-src-1.1
    make && make install
    cd ..
    wget http://fastestcode.org/dl/emwm-utils-src-1.1.tar.xz
    tar -xf emwm-utils-src-1.1.tar.xz
    cd emwm-utils-src-1.1
    make && make install
    cd ..
    wget http://fastestcode.org/dl/xfile-src-1.0-beta.tar.xz
    tar -xf xfile-src-1.0-beta.tar.xz
    cd xfile-beta
    make && make install
    cd ..
    wget http://fastestcode.org/dl/ximaging-src-1.7.tar.xz
    tar -xf ximaging-src-1.7.tar.xz
    cd ximaging-src-1.7
    make && make install
    cd ..
 
 The next step is to install the terminal emulator I like best, which is tilix. This is availble in the ports repo. Before installing it via ports, it is a good idea to install its dependancies via the pkg tool, if you don't it will compile all the dependencies from source and will take a lot of time.
 
    pkg install cmake po4a gtkd desktop-file-utils gettext-tools meson ninja pkgconf ldc harfbuzz libsecret libunwind gettext-runtime at-spi2-core cairo gtk3 librsvg2-rust pango vte3 dub
    
 Once that is done we need to download the ports collection.
 
    git clone https://git.FreeBSD.org/ports.git /usr/ports
    
Then we can finally install tilix

    cd /usr/port/x11/tilix
    make install

Once this is all done, copy the dot files to the home directory of your user account, renaming them to; .xinitrc, .toolboxrc and .emwmrc. If you want to make changes to the menu box, edit the .toolboxrc and if you want to make changes to how emwm works, edit the .emwmrc file.

You should now be able to log in as you regular user account, type startx and you should be ready to go.
 