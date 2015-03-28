Setup Postgresql / PostGIS
==========================


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

Handy commands
--------------

.. code-block:: bash

    # Execute sql script from command line
    psql -U username -d myDataBase -a -f myInsertFile


.. code-block:: psql

    -- check size of data base
    select pg_size_pretty(pg_database_size('akonadi'));
