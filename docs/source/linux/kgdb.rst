KGDB
====

SETUP
-----
1. Install pre-requisites and dependencies

.. code:: bash

    ➜ apt install exuberent-ctags cscope tree -y
    ➜ apt install build-essential libncurses-dev bison flex libssl-dev libelf-dev git fakeroot ncurses-dev xz-utils bc dwarves 
    ➜ 
    ➜ 
    ➜ 
    ➜ 
    ➜ 
    ➜ 
    ➜ 
    ➜ 
    ➜ 

1. Download respective kernel from www.kernel.org

wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.10.176.tar.xz

3. Incase you are using UBUNTU 22.04.1 os

# extract it in /usr/src

4. KGDB setup on target vm. bring up vm using virt-install.
Next edit the vm domains configuration to get target vm ready.
.. code:: bash

	➜ virsh edit domain_name
	# Below line is 1st line and it should look similar in the domain config u r using.
	<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>
	  <qemu:commandline>
	    <qemu:arg value='-gdb'/>
	    <qemu:arg value='tcp::1200'/>
	  </qemu:commandline>
	</domain>
	
	➜ # once you start above domain target will be listening to port 1200
	➜ netstat -tapn | grep 1200
	
	➜ # Now this target will be listening on "localhost:1200", on development machine
	➜ # use gdb client and connect to this target. Ex:
	➜ gdb vmlinux
	➜ (gdb) target remote localhost:1200
	➜ gdb vmlinux
PROBLEMS & SOLUTIONS
--------------------

1. Your Kernel boots and `SysRq + g` is not working.

.. code:: bash

    ➜ # This will enable sending SysRq commands.
    ➜ # If you get tired of doing this manually,
    ➜ # consider adding `sysrq_always_enabled` to your kernel command line arguments.
    ➜ echo 1 > /proc/sys/kernel/sysrq

2. When stopping execution through SysRq key on "TARGET MACHINE", it stops but then it is not able
to communicate over serial cable with "DEVELOPMENT MACHINE".

The reason can be, your KGDB I/O driver is not passed arguments properly and you may need to
reconfigure the driver in below way:

.. code:: bash

    ➜ # The reason can be, your KGDB I/O driver is not passed arguments properly and you may need to
    ➜ # reconfigure the driver in below way:
    ➜ echo "ttyS0,115200" > /sys/modules/<module name>/parameters

3. How to use agent-proxy kdmx to debug linux kernel, link = 
https://docs.windriver.com/bundle/Wind_River_Linux_Tutorial_Kernel_Debugging_with_GDB_and_KGDB_9_1/page/mxx1551912688078.html

Download agent-proxy from below link:
https://git.kernel.org/pub/scm/utils/kernel/kgdb/agent-proxy.git/

