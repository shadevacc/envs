BASH SCRIPT TRICKS
==================

CODE
----

* Print custom string in kernel ring or dmesg buffer

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

	.. code:: bash

		echo "STRING" #> /dev/kmsg

* For ex if above code is pasted in a executable file **emsg**
	.. code:: bash
		
		chmod 755 -c emsg

* Above code when executed with no args prints **OUTPUT A**

* Above code when executed with args prints output **OUTPUT B**

OUTPUT A
--------
	
	.. code:: bash

		➜ ./emsg
		----------
		----------

OUTPUT B
--------
	.. code:: bash

		➜ ./emsg "HELLO"
		---------
		# HELLO #
		---------


	
