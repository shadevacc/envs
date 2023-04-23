LINUX
=====

ENV SETUP
---------
Ubuntu
~~~~~~
.. _v2.3.3/FantasqueSansMono.zip: https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/FantasqueSansMono.zip
.. _how-to-allow-gui-root-login-on-ubuntu-20-04-focal-fossa-linux: https://linuxconfig.org/how-to-allow-gui-root-login-on-ubuntu-20-04-focal-fossa-linux

| 1. Download FantasqueSansMono NF font from `v2.3.3/FantasqueSansMono.zip`_

    .. code:: bash

        cd ~/Download
        wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/FantasqueSansMono.zip
        mkdir -p F_NF
        unzip FantasqueSansMono.zip -d F_NF
        cd F_NF && mkdir -p ~/.fonts
        mv *.ttf ~/.fonts
        fc-cache

    Apply this font to terminal

| 2. we should not login as a user so need to do root login, so please read
| `how-to-allow-gui-root-login-on-ubuntu-20-04-focal-fossa-linux`_ for more details

    .. code:: bash

        sudo passwd root # Give the password and it will change
        su root          # Now you will be able to login as root
                        # Just give the password and enter
        apt install vim  # vim is must to do editing of any files
        # Add below content in the file
        vim /etc/gdm3/custom.conf
        # TimedLoginDelay = 10
        AllowRoot = true
        # Below line needs to be commented out so do it
        vim /etc/pam.d/gdm-password
        # auth   required        pam_succeed_if.so user != root quiet_success
        # Enable or Uncomment password authentication
        vim /etc/ssh/sshd_config
        # PasswordAuthentication = yes
        PasswordAuthentication yes
        PermitRootLogin yes
        reboot

| 3. setup done for user to be done for root

    .. code:: bash

        sudo apt install net-tools -y
        sudo apt install openssh-server -y
        mkdr -p ~/.fonts && cd ~/.fonts
        sftp user@ipaddr -y
        get -r *
        fc-cache

    Apply this font(FantasqueSansMono) to terminal

| 4. Install vbox guest addtions

    .. code:: bash

        # do not install vbox guest addtions without installing build-essential
        # you will see half display
        # link: https://askubuntu.com/questions/1408406/how-to-fix-partial-black-screen-on-virtual-box-ubuntu-linux
        sudo apt install make gcc flex bison build-essential

lolcat
~~~~~~

To install lolcat we need python3 installed.
After installing python3 we need to upgrade pip if it is not latest.
Now we can install lolcat tool.

    .. code:: bash

        # Check for python3
        which python3
        /usr/bin/python3

        # Python3 exists. so i will upgrade pip
        python3 -m pip install --upgrade pip

        # Now i will install lolcat
        python3 -m pip install lolcat

Powerline symbols showing dashes?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. _powerline.readthedocs: https://powerline.readthedocs.io/en/master/installation/linux.html

Follow below steps in Ubuntu22.04.02 and refer `powerline.readthedocs`_:

    .. code:: bash

        # https://powerline.readthedocs.io/en/master/installation/linux.html
        python3 -m pip install powerline-status
        # Do not use apt pkg manager just do it manually
        cd ~/Downloads
        git clone https://github.com/powerline/powerline.git
        git clone https://github.com/powerline/fonts.git
        cd fonts && bash install.sh && cd ..
        sudo apt install powerline
        mkdir -p ~/.local/share/fonts
        mkdir -p ~/.config/fontconfig/conf.d/
        cp -rf powerline/font/PowerlineSymbols.otf ~/.local/share/fonts
        cp -rf powerline/font/10-powerline-symbols.conf ~/.config/fontconfig/conf.d
        fc-cache -vf ~/.local/share/fonts/
        # Install the fontconfig file. For newer versions of fontconfig the config
        # path is ~/.config/fontconfig/conf.d/, for older versions it’s ~/.fonts.conf.d/:

CapsLock key to behave as Control key in Ubuntu 22.04
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   1. Open the ``Tweaks``

   2. Open ``Keyboard and mouse``

   3. Open ``Additional layout options``

   4. Open the ``Caps Lock behaviour``

   5. Open the ``Make Caps Lock and additional ctrl``

Install gnome-tweaks & gnome-shell-extension-manager
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~    
.. _Install and change themes in Ubuntu22.04.02: https://ubuntuhandbook.org/index.php/2022/05/install-themes-ubuntu-22-04/#:~:text=Enable%20Shell%20theme%20selection%20box%3A&text=To%20enable%20it%2C%20you%20have,install%20%E2%80%9CUser%20Themes%E2%80%9D%20extension.&text=Next%2C%20click%20on%20the%20%E2%80%9CActivities,%2C%20re%2Dopen%20Gnome%20Tweaks
.. _gnome-look.org: https://www.gnome-look.org/browse?cat=135&ord=rating

| 1. **gnome-tweaks**

    | Tutorial = `Install and change themes in Ubuntu22.04.02`_.
    | Gnome themes can be downloaded from this site: `gnome-look.org`_.

        .. code:: bash

            sudo apt install gnome-tweaks
            mkdir -p ~/.themes
            # After downloading WhiteSur-Dark-solid.tar.xz from gnome-look.org
            tar -xvf WhiteSur-Dark-solid.tar.xz
            mv WhiteSur-Dark-solid ~/.themes
            fc-cache

    | Now open application tweaks from GUI and select the installed theme

    ``Tweaks`` -> ``Appearance`` -> ``Themes`` -> ``Applications``

| 2. **gnome-shell-extension-manager**

    .. code:: bash

        sudo apt install gnome-shell-extension-manager

