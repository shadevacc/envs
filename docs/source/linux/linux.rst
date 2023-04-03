LINUX
=====

UBUNTU Environment setup
------------------------

1. Download FantasqueSansMono NF font from below link:

https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/FantasqueSansMono.zip

.. code:: bash

    ➜ cd ~/Download
    ➜ wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/FantasqueSansMono.zip
    ➜ mkdir -p F_NF
    ➜ unzip FantasqueSansMono.zip -d F_NF
    ➜ cd F_NF && mkdir -p ~/.fonts
    ➜ mv *.ttf ~/.fonts
    ➜ fc-cache

Apply this font to terminal

2. we should not login as a user so need to do root login

link: https://linuxconfig.org/how-to-allow-gui-root-login-on-ubuntu-20-04-focal-fossa-linux

.. code:: bash

    ➜ sudo passwd root # Give the password and it will change
    ➜ su root          # Now you will be able to login as root
                       # Just give the password and enter
    ➜ apt install vim  # vim is must to do editing of any files
    # Add below content in the file
    ➜ vim /etc/gdm3/custom.conf
    # TimedLoginDelay = 10
    AllowRoot = true
    # Below line needs to be commented out so do it
    ➜ vim /etc/pam.d/gdm-password
    # auth   required        pam_succeed_if.so user != root quiet_success
    # Enable or Uncomment password authentication
    ➜ vim /etc/ssh/sshd_config
    # PasswordAuthentication = yes
    PasswordAuthentication yes
    PermitRootLogin yes
    ➜ reboot

3. setup done for user to be done for root

.. code:: bash

    ➜ sudo apt install net-tools -y
    ➜ sudo apt install openssh-server -y
    ➜ mkdr -p ~/.fonts && cd ~/.fonts
    ➜ sftp user@ipaddr -y
    ➜ get -r *
    ➜ fc-cache

Apply this font(FantasqueSansMono) to terminal

4. Install vbox guest addtions

.. code:: bash

    ➜ # do not install vbox guest addtions without installing build-essential
    ➜ # you will see half display
    ➜ # link: https://askubuntu.com/questions/1408406/how-to-fix-partial-black-screen-on-virtual-box-ubuntu-linux
    ➜ sudo apt install make gcc flex bison build-essential

Install lolcat
--------------

To install lolcat we need python3 installed.
After installing python3 we need to upgrade pip if it is not latest.
Now we can install lolcat tool.

.. code:: bash

    # Check for python3
    ➜ which python3
    /usr/bin/python3

    # Python3 exists. so i will upgrade pip
    ➜ python3 -m pip install --upgrade pip

    # Now i will install lolcat
    ➜ python3 -m pip install lolcat