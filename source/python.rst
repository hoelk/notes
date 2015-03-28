Python
######

Virtual Environemnts
====================

.. code-block:: bash

    sudo pip install virtualenv
    virtualenv env
    ./activate
	source env/bin/activate

    pip list # to list installed packages

List comprehension
==================

.. code-block:: python

    dataset1= [1,2,3,4]

    print(dataset1)
    result = [k**2 for k in dataset1] # {} for dict comprehension
    print(result)


CLI
===

.. code-block:: python

    # Simple CLI
    if __name__ == '__main__':
        import sys
        print sys.argv

    # Advanced CLI
    import argparse
    if __name__ == '__main__':
        parser = argparse.ArgumentParser(
            description="get the given name, optionally also the surname")
        parser.add_argument("given_name", help="given name of the person")
        parser.add_argument(
            "‐s", "‐‐surname", help="the surname of the person")
        args = parser.parse_args()
        print(args.given_name)
        if args.surname:
            print(args.surname)


Try-Except Block
================

.. code-block:: python

    def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError:
        print "division by zero!"
    else:
        print "result is", result
    finally:
        print "executing finally clause"

    divide(2, 1)
    divide(2, 0)


Renaming files code example
===========================

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
