Postgresql & PostGIS
####################

Database Management
===================

SQL Operation Order
-------------------

https://blog.jooq.org/2016/12/09/a-beginners-guide-to-the-true-order-of-sql-operations/

* FROM: This is actually the first thing that happens, logically. Before anything else, we’re loading all the rows from all the tables and join them. Before you scream and get mad: Again, this is what happens first logically, not actually. The optimiser will very probably not do this operation first, that would be silly, but access some index based on the WHERE clause. But again, logically, this happens first. Also: all the JOIN clauses are actually part of this FROM clause. JOIN is an operator in relational algebra. Just like + and - are operators in arithmetics. It is not an independent clause, like SELECT or FROM
* WHERE: Once we have loaded all the rows from the tables above, we can now throw them away again using WHERE
* GROUP BY: If you want, you can take the rows that remain after WHERE and put them in groups or buckets, where each group contains the same value for the GROUP BY expression (and all the other rows are put in a list for that group). In Java, you would get something like: Map<String, List<Row>>. If you do specify a GROUP BY clause, then your actual rows contain only the group columns, no longer the remaining columns, which are now in that list. Those columns in the list are only visible to aggregate functions that can operate upon that list. See below.
* aggregations: This is important to understand. No matter where you put your aggregate function syntactically (i.e. in the SELECT clause, or in the ORDER BY clause), this here is the step where aggregate functions are calculated. Right after GROUP BY. (remember: logically. Clever databases may have calculated them before, actually). This explains why you cannot put an aggregate function in the WHERE clause, because its value cannot be accessed yet. The WHERE clause logically happens before the aggregation step. Aggregate functions can access columns that you have put in “this list” for each group, above. After aggregation, “this list” will disappear and no longer be available. If you don’t have a GROUP BY clause, there will just be one big group without any key, containing all the rows.
* HAVING: … but now you can access aggregation function values. For instance, you can check that count(*) > 1 in the HAVING clause. Because HAVING is after GROUP BY (or implies GROUP BY), we can no longer access columns or expressions that were not GROUP BY columns.
* WINDOW: If you’re using the awesome window function feature, this is the step where they’re all calculated. Only now. And the cool thing is, because we have already calculated (logically!) all the aggregate functions, we can nest aggregate functions in window functions. It’s thus perfectly fine to write things like sum(count(*)) OVER () or row_number() OVER (ORDER BY count(*)). Window functions being logically calculated only now also explains why you can put them only in the SELECT or ORDER BY clauses. They’re not available to the WHERE clause, which happened before. Note that PostgreSQL and Sybase SQL Anywhere have an actual WINDOW clause!
* SELECT: Finally. We can now use all the rows that are produced from the above clauses and create new rows / tuples from them using SELECT. We can access all the window functions that we’ve calculated, all the aggregate functions that we’ve calculated, all the grouping columns that we’ve specified, or if we didn’t group/aggregate, we can use all the columns from our FROM clause. Remember: Even if it looks like we’re aggregating stuff inside of SELECT, this has happened long ago, and the sweet sweet count(*) function is nothing more than a reference to the result.
* DISTINCT: Yes! DISTINCT happens after SELECT, even if it is put before your SELECT column list, syntax-wise. But think about it. It makes perfect sense. How else can we remove distinct rows, if we don’t know all the rows (and their columns) yet?
* UNION, INTERSECT, EXCEPT: This is a no-brainer. A UNION is an operator that connects two subqueries. Everything we’ve talked about thus far was a subquery. The output of a union is a new query containing the same row types (i.e. same columns) as the first subquery. Usually. Because in wacko Oracle, the penultimate subquery is the right one to define the column name. Oracle database, the syntactic troll😉
* ORDER BY: It makes total sense to postpone the decision of ordering a result until the end, because all other operations might use hashmaps, internally, so any intermediate order might be lost again. So we can now order the result. Normally, you can access a lot of rows from the ORDER BY clause, including rows (or expressions) that you did not SELECT. But when you specified DISTINCT, before, you can no longer order by rows / expressions that were not selected. Why? Because the ordering would be quite undefined.
* OFFSET: Don’t use offset
* LIMIT, FETCH, TOP: Now, sane databases put the LIMIT (MySQL, PostgreSQL) or FETCH (DB2, Oracle 12c, SQL Server 2012) clause at the very end, syntactically. In the old days, Sybase and SQL Server thought it would be a good idea to have TOP as a keyword in SELECT. As if the correct ordering of SELECT DISTINCT wasn’t already confusing enough.

Create database user
--------------------

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

      -- change owener of table
      alter table travels owner to hoelk;



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

SQL Support in R
================

.. code-block:: R

    library(RPostgreSQL)    # SQL Driver
    library(sqldf)          # Send SQL from R
    library(rgdal)          # For postgis layers

    # Read tables via RPostgreSQL and sqldf
    options(sqldf.RPostgreSQL.user ="lbs",
      sqldf.RPostgreSQL.password ="lbs",
      sqldf.RPostgreSQL.dbname ="lbs",
      sqldf.RPostgreSQL.host ="localhost")

    travels <- sqldf("select * from travels")
    travels_motionpatterns <- sqldf("select * from travels_motionpatterns")

    # Read spatial data via rgdal
    dsn="PG:dbname='lbs' host='localhost' user='lbs' password='lbs'"
    ogrListLayers(dsn)

    waysegment_gip_at_14_06_20140807 <- readOGR(dsn, "waysegment_gip_at_14_06_20140807")
