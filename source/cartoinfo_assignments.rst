Cartographic Information Systems - Assignments
==============================================

Exercise 1 - Spatial Databases
------------------------------

**List all countries for which our test data contains more than 20 cities**
, and return the number of cities for each such country.

.. code-block:: psql

    SELECT COUNT(*),
           country.name
    FROM (city
          LEFT JOIN country ON city.c_id = country.c_id)
    GROUP BY country.name
    HAVING COUNT(city.c_id) > 20;


.. image:: _static/img/cartoinfo/ex1_group_by.png
    :align: center


* ``SELECT`` selects one or several collumns from a dataset.
* ``COUNT`` calculates the number of entries returned
* ``LEFT JOIN`` joins a second dataset to the present one, keeping all entries
    from the original dataset (in this case *city*), and discarding all
    entries from the second that cannot be matched. This is done here to
    have full country names in the query result.
* ``GROUP BY`` is used to group rows by a certain condition (in this case
    *country.name*). It can be used in conjuncture with ``HAVING``
    to filter datasets based on aggregated statistics. In this example only
    groups (countries) that contain more than 20 cities are retained.

Select neighbors countries of Austria and Italy

    .. code-block:: psql

        SELECT *
        FROM neighbors
        WHERE country1 IN ('A', 'I');

.. image:: _static/img/cartoinfo/ex1_neighbors.png
    :align: center

* ``WHERE`` can be used to filter datasets based on conditions.
* ``IN`` checks wheter a value is in a list of values.

**Select all cities with a population higher than the average population.**

.. code-block:: psql

    SELECT population, name
    FROM city
    WHERE population >
    	(SELECT AVG(population)
    	FROM city)
    ORDER BY population;

.. image:: _static/img/cartoinfo/ex1_avg.png
    :align: center

* ``AVG`` calculates the arithmethic mean of a collumn. There is also ``MAX`` for maximum, ``MIN`` for minimum, etc..

**Select all cities with a population between 120 000 and 140 000.**

.. code-block:: psql

    SELECT population, name
    FROM city
    WHERE population BETWEEN 120000 AND 140000
    ORDER BY population;

.. image:: _static/img/cartoinfo/ex1_between.png
    :align: center

* ``BETWEEN`` checks wheter a value falls inside a range (closed interval)
