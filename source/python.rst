Python
######


I/O
===

* numpy (ascii, binary files)
* pandas (ascii)
* struct (binary files) (http://pymotw.com/2/struct/)
    * conversions between Python values and C structs represented as Python strings
* pickle (http://www.diveintopython3.net/serializing.html)
    * native python serialization format
* pytables / H5py (http://www.h5py.org/)
    * efficient for large arrays


Virtual Environemnts
====================

.. code-block:: bash

    sudo pip install virtualenv
    virtualenv env
    ./activate
	source env/bin/activate

    pip list # to list installed packages

virtualenvs tend to break if you move the folder, in this case the easiest thing
is to delete and reinstall

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

Pandas
======

pandas series ~ R vector

.. code-block:: python

    s[s > s.median()]

    'e' in s

pandas DataFrame ~ R data.frame


Access Postgres
================

.. code-block:: python

    import psycopg2 as database
    import postgresql_secret as secret
    # for MySQL, we would install MySQLdb and use
    # import MySQLdb as database


    connection = database.connect(
        host=secret.SERVER,
        user=secret.USERNAME,
        passwd=secret.PASSWORD,
        db=secret.DB
    )


    data = []

    cursor = connection.cursor()
    cursor.execute("SELECT * FROM places")

    fieldnames = []
    for desc in cursor.description:
        fieldnames.append(desc[0])

    for row in cursor:
        row_data = {}

        for i, fname in enumerate(fieldnames):
            row_data[fname] = row[i]

        data.append(row_data)

The output is a list of dictionaries containing the data from the table "places"


Web APIs
========

OSM / Overpass query language
-----------------------------

Test overpass at http://www.overpass-turbo.eu/


.. code-block:: python

    query = """
    [out:json]
    [timeout:25]
    ;
    node
      (46.3,9.5,49.0,17.1)
      [amenity="ice_cream"];
    out body;
    """

    full_query = {
        'data': query
    }

    import urllib

    url = "http://overpass-api.de/api/interpreter?" + urllib.urlencode(full_query)

    print "Downloading overpass data ..."

    urllib.urlretrieve (url, 'data/overpass_raw.json')

    print "Done."


Object orientation
==================

Encapsulation
-------------

pseudo-encapsulation realized through "_" and "__" in variable names

http://stackoverflow.com/questions/1301346/the-meaning-of-a-single-and-a-double-underscore-before-an-object-name-in-python


Inheritance
-----------

.. code-block:: python

    class Human(object):
        def core_functionality():
            ....

    class Student(Human):
        def additional_functionality(self):
            ....


.. code-block:: python

    class Shape(object):
        def __init__(self, color):
            self.color = color


    class Rectangle(Shape):
        def __init__(self, width, height, color):
            super(Rectange, self).__init__(color)
            self.width = width
            self.height = height


    class Circle(Shape):
        def __init__(self, color, radius):
            super(Rectange, self).__init__(color)
            self.radius = radius

        def calculate_area(self):
            import math
            print(self.radius * self.radius * math.pi)



redefining methods


.. code-block:: python

    import math

    class Pizza (object):
        def __init__ ( self , radius):
            self .radius = radius

        def circumference ( self ):
            return 2 * math.pi * self .radius

    class Calzone (Pizza):
        def circumference ( self ):
            c = super(Calzone, self ).cf()
            return c / 2. + 2 * self .radius


netCDF4
=======

required workaround for netcdf4 install

.. code-block:: python

    sudo CFLAGS="-I/usr/include/hdf5/serial/" pip install netCDF4

GDAL / Rasterio
===============

Import raster data and display some info with rasterio

.. code-block:: python

    import os
    import rasterio

    os.chdir('/home/hoelk/Dropbox/uni/geopython/12_gdal/')

    with rasterio.drivers():
        with rasterio.open(os.path.join("07 dsm_zco.tif")) as src:
            print(src.driver)
            print 'Origin = (', src.affine[2], ',', src.affine[5], ')'
            print 'Pixel Size = (', src.affine[0], ',', src.affine[4], ')'
            print(src.crs_wkt)
            print(src.res)
            print(src.nodatavals)
            print(src.dtypes)
