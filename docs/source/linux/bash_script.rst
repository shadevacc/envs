BASH SCRIPT TRICKS
==================

CODE
----

.. code:: bash

	msg="$1"
	start=$(echo ${#msg})
	if [ 0 -eq ${#msg} ]; then
	        start=6
	fi
	let "start=start+4"
	str=$(for ((i=1; i<=$start; i++)); do echo -n -; done)
	echo $str #> /dev/kmsg
	if [ 0 -ne ${#msg} ]; then
	        echo "# $msg #" #> /dev/kmsg
	fi
	echo $str #> /dev/kmsg

OUTPUT A
--------
.. code:: bash

	➜ ./emsg
	----------
	----------

OUTPUT A
--------
.. code:: bash

	➜ ./emsg "HELLO"
	---------
	# HELLO #
	---------

* For ex if above code is pasted in a executable file **emsg**

	chmod 755 -c emsg

* Above code when executed with no args prints **OUTPUT A**

* Above code when executed with args prints output **OUTPUT B**
	
