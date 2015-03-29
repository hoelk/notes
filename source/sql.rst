Postgresql & PostGIS
====================


Create database user
-------------------

1. Add a Linux/UNIX user called tom

  .. code-block:: bash

      adduser tom
      passwd tom

2. Login with the postgres super-user and connect to the database

  .. code-block:: bash

      su - postgres
      psql template1

4. Add a postgres user called tom.

  .. code-block:: psql

      template1=# CREATE ROLE tom WITH PASSWORD 'myPassword';
      template1=# ALTER ROLE tom WITH LOGIN; -- allow role to log in
      template1=# CREATE DATABASE jerry;
      template1=# GRANT ALL PRIVILEGES ON DATABASE jerry to tom;
      template1=# \q -- quit

5. Test tom user login

  .. code-block:: bash

      $ su - tom
      $ psql -d jerry -U tom

  Output:

  .. code-block:: bash

      Welcome to psql 7.4.16, the PostgreSQL interactive terminal.
      Type:  \\copyright for distribution terms
             \\h for help with SQL commands
             \\? for help on internal slash commands
             \\g or terminate with semicolon to execute query
             \\q to quit
      jerry=>

6. Misc commands

  .. code-block:: psql

      -- change password for user
      template1=# ALTER USER tom WITH PASSWORD 'blubb'


Create empty test table
-----------------------

.. code-block:: psql

        CREATE TABLE test_set (
          id       BIGSERIAL PRIMARY KEY, --in automatically incremented id is almost always a good idea
          geom GEOMETRY --here comes the magic: this column if of type "geometry"
        );

        INSERT INTO test_set (the_geom)
        VALUES
          (st_geomfromtext('LINESTRING(-46 -40, -4 -6, -5 -5, -6 -4, -8 -5, 50 30 )')),
          (st_geomfromtext('LINESTRING(-3 -10, -10 -5, 17 3, 23 66)')),
          (st_geomfromtext('LINESTRING(-20 20, -2 0, 15 -15, 65 -1)')),
          (st_geomfromtext('LINESTRING(-50 -50, -47 46)')),
          (st_geomfromtext('LINESTRING(70 70, 80 -40, 0 -50 )'));

        INSERT INTO test_set (geom)
        VALUES
          (st_geomfromtext('POLYGON((2.40309828723774 1.4684052885979,2.78140531783743 1.1025017671982,3.03567725643723 1.50561581619787,3.03567725643723 1.50561581619787,2.40309828723774 1.4684052885979))')),

Functions
=========

Convert spatial data to sql script (PLPYTHON)
---------------------------------------------

Output coordinates are WGS84 (SRID 4326)

.. code-block:: psql

    CREATE OR REPLACE FUNCTION spatial_data_to_sql(input_set text, output_path text default '/tmp/', geometry_column text default 'geom')
       RETURNS VOID AS
       $$
       import os, sys, logging
       LOG_FILENAME = '/tmp/plpython.log'
       logging.basicConfig(filename=LOG_FILENAME,level=logging.DEBUG)
       logging.debug('============================================')
       logging.debug('python version: %s' % sys.version)

       def delete_content(pfile):
        pfile.seek(0)
        pfile.truncate()

       def flatten_plyresult(x):
         x = x[0]
         x = x[list(x.keys())[0]]
         return x

       f = open(output_path + input_set +".sql", 'w')

       delete_content(f)

       logging.debug('writing to %s' % f)

       sql_query = "CREATE TABLE %s (\n  id BIGSERIAL PRIMARY KEY, \n  geom GEOMETRY \n);\n\n" % input_set
       f.write(sql_query)
       sql_query = "INSERT INTO %s (geom) \nVALUES\n" % input_set
       f.write(sql_query)

       sql_query = "SELECT ST_AsText(%s) FROM %s;" %(geometry_column, input_set)
       cur = plpy.cursor(sql_query)

       spatial_objects = ()
       while True:
         row = cur.fetch(1)
         if not row: break
         row = flatten_plyresult(row)
         spatial_objects = spatial_objects + (row ,)

       for i in range(0,len(spatial_objects)):
         logging.debug(spatial_objects[i])
         line = "  (st_geomfromtext('%s'))" % spatial_objects[i]
         if i < len(spatial_objects)-1:
           line = line + ",\n"
         else:
           line = line + ";\n\n"
         f.write(line)
       $$
       LANGUAGE plpython3u;

Usage:

.. code-block:: psql

    SELECT spatial_data_to_sql('test_set');


Handy commands
==============

.. code-block:: bash

    # Execute sql script from command line
    psql -U username -d myDataBase -a -f myInsertFile


.. code-block:: psql

    -- check size of data base
    select pg_size_pretty(pg_database_size('akonadi'))

    -- change owner of DB
    ALTER table country owner to hoelk
