Python
######

Virtual Environemnts
--------------------

.. code-block:: bash

	virtualenv env
	source env/bin/activate

	pip install <packagename>
	

renaming files
--------------

.. code-block:: python

	import os

	for filename in os.listdir('.'):
		if filename.startswith("Algorithms lecture"):
			os.rename(filename, "0" + filename[19:])

	def remove_values_from_list(the_list, val):
	   return [value for value in the_list if value != val]

	for filename in os.listdir('.'):
	    if filename.startswith('Lecture '):

	        leading_number = filename.split()[1][0:-1]  # get leading number and remove _ from it
	        leading_number = "0" + leading_number
	        if( len(leading_number) > 2):
	            leading_number = leading_number[1:]

	        rest_of_filename = filename.split()[2:-4]
	        for i in ("Richard", "Buckland", "-"):
	            rest_of_filename = remove_values_from_list(rest_of_filename, i)

	        filename_new = leading_number + ' ' + ' '.join(rest_of_filename)
	        os.rename(filename, filename_new)

	for filename in os.listdir('.'):
	    if filename.startswith('Lecture'):
	        leading_number = filename[7:10].replace("_", "") # Lecture13a_ -> 13a
	        filename_new = leading_number + " Data Structures and Algorithms"
	        os.rename(filename, filename_new)

	for filename in os.listdir('.'):
	    filename_new = filename.replace(" - Richard Buckland", "")
	    filename_new = filename_new.replace(" UNSW", "")
	    filename_new = filename_new.replace(" (720p)", "")
	    filename_new = filename_new.replace("_", "")
	    os.rename(filename, filename_new)
