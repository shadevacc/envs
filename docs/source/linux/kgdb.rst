KGDB
====

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

