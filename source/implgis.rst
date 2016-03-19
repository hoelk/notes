Implementation of a GIS
#######################

https://en.wikipedia.org/wiki/User:Hoelk/Books/Data_Structures_and_Algorithms

https://www.youtube.com/watch?v=HtSuA80QTyo&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb

http://en.wikibooks.org/wiki/Algorithms
http://en.wikibooks.org/wiki/Data_Structures

Data Structures
===============
* Vector -> stored sequentially:
    * To insert an element, a new vector must be created. All elements
    plus the new one are moved to this new vector. relatively costly.
* Concatenated list -> entries stored arbitrarily, with pointer to the next entry
    * more efficient to insert new entry

Algorithms
==========

Complexity
----------

http://en.wikipedia.org/wiki/Computational_complexity_theory

Sorting Algorithms
------------------

http://en.wikipedia.org/wiki/Insertion_sort

*     has a worst case time complexity of O(n²)
*     works in-loco (does not require extra space, just the one variable (aux))
*     there are better solutions. We know optimal sorting algorithms are O(n * log n)

http://en.wikipedia.org/wiki/Merge_sort

*    O(n log n)
*    does not work in-loco

http://en.wikipedia.org/wiki/Quicksort

Search Algorythms
-----------------

Dictionary of Algorithms and Data Structures

http://xlinux.nist.gov/dads//

ANIMAL Algorithm Animation System

http://www.animal.ahrgr.de/


Binary Search
^^^^^^^^^^^^^
http://en.wikipedia.org/wiki/Binary_search_algorithm


HEAP data structure and optimal sorting
---------------------------------------

Graphs
^^^^^^

Abstract data structre, set of nodes and links between nodes

Trees
^^^^^

http://en.wikipedia.org/wiki/Tree_%28data_structure%29

Special kind of graph.
    * A tree consists of one single node

A tree node x is an abstract data structure consisting of
    * A set of values of different data types
    * A list of nodes called sons (children?) connecting it to other nodes
    * The node x is the parent of its *sons*
    * nodes with the same parent are *siblings*
    * special nodes:
        * a *root* r of a tree T is a node without a parent
        * a *leaf* is a node without sons
        * an *internal node* is a node with a parent and at least one son
        * A branch is the path from the root to a leaf
            * The length of a branch is the number of its arcs
            * The depth of a node is the length of the path going from the node
                to the root
            * the heigth h of a tree is the length of its longest branch.
            * Trees can be divided into *levels*, depending on the distance
            from the root (the root has level 0, the maximum length is the
            height of the tree)
        * A tree is *k-ary* if each node admits no more than k sons
            * A tree where ich node has a maximum of two nodes is called binary
        * A tree is said complete if each non-leaf node hast exactly k sons

HEAP
^^^^

http://en.wikipedia.org/wiki/Heap_%28data_structure%29

A heap is a vector V of n elements such that... (see slides)

Heapsort
''''''''

Annotation (Heapify works of node + parent, Build Heap iterates over whole tree)
Heapify always moves down the whole tree, that's why i only need to iterate
n = height of the tree times.


Binary search tree
^^^^^^^^^^^^^^^^^^

Even more important than heap for us (geodata),

    * All nodes on the right side are bigger
    * All nodes on the left are smaller

http://en.wikipedia.org/wiki/Binary_search_tree


In Databases
------------

Create indices for the columns im likely to search (but not to many)

In memory vs on harddrive
-------------------------

On harddrive i have an extra constraint: i need to limit the number of accesses

Spatial Acces Methods
---------------------

* Elements of multi-dimensional space cannot be ordered uniquely --> how to make indices?

* Hash coding
* Hirarchical indices (tree-like)
* Space-filling curve: See slide -> imagine a line that goes through all points/elements and has a diretion


* Polygons are usually approximated with minimum bounding rectangles (MBR)
    * can be represented by only two points
* Two step search process
    * Filter step: first search for the MBRs
    * Refinement:  then check the actual features if they match the actual search

R-Tree Family
^^^^^^^^^^^^^

http://en.wikipedia.org/wiki/R-tree

* Balanced (all leaf nodes at the same level)
* Maintains references to DB in leaves
* Variable fanout (between m and M) (number of children per node)
* Most popular SAM

R-Tree Basics
^^^^^^^^^^^^^
* group elements by proximity (based on the MBRs of the elements)
* Level 0 contains the leaves of the tree contain the MBR of the datasets
    * Level 1 contains MBR of all leaves that fall within a specific group
    * Level 2 contains MBR of all groups of level one within a specific souper-group, etc...

* Each node contains between m and M index entries (root is an exception from this rule)
    * in Leaf nodes An index entry is a pair of kind: E = (R,r)  (R = bounding rectangle, r = reference to actualy database object)
    * in non-leaf nodes
        *r is a reference toa node located at level 1 - I
        * R is the the MBR enclosing all MBRs of the referenced nodes

notes
'''''

* Splitting especially important since it has a huge influence on the structure of the tree
(how do we split the tree nodes, so that for further searches we can minimize search time)

Quad Trees
^^^^^^^^^^

Hash Tables
^^^^^^^^^^^

* insertion, deletion and search work in **constant time**
* requires O(|U|) storage space (which is a lot)
* Only acceptable when |K| (set of used key) is similar to |U| (set of possible keys)
* Usually |K| is much smaller than |U|



Assignments
===========

EX 1: Connect linestring extremes
---------------------------------

Given a spatial dataset S1 consisting of linestrings write an SQL function that
does the following:
    * computes the straight lines connecting the 2 extremes of each linestring in S1 to the extremes of any other linestring in S
    * creates a new dataset S2 consisting of all the intersection points between the lines computed in the previous step (without repetitions)

Create the test dataset
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: plpgsql

    CREATE TABLE test_set (
      id       BIGSERIAL PRIMARY KEY,
      geom GEOMETRY
    );

    INSERT INTO test_set (geom)
    VALUES
       (st_geomfromtext('LINESTRING(-46 -40, -4 -6, -5 -5, -6 -4, -8 -5, 50 30 )')),
       (st_geomfromtext('LINESTRING(-3 -10, -10 -5, 17 3, 23 66)')),
       (st_geomfromtext('LINESTRING(-20 20, -2 0, 15 -15, 65 -1)')),
       (st_geomfromtext('LINESTRING(-50 -50, -47 46)')),
       (st_geomfromtext('LINESTRING(70 70, 80 -40, 0 -50 )'));


SQL Version (best version)
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: psql

   CREATE OR REPLACE FUNCTION intersect_extreme_lines()
     RETURNS SETOF GEOMETRY AS
     $BODY$

     -- Points at extremes of input lines
     WITH extremes_points AS (
       SELECT
         ST_StartPoint(geom) AS geom,
         id
       FROM test_set
       UNION ALL
       SELECT
         ST_EndPoint(geom) AS geom,
         id
       FROM test_set
     ),

     -- Connect points at extremes of each input lines with the extremes of all other lines
     extremes_lines AS (
         SELECT ST_MakeLine(epoints_1.geom, epoints_2.geom) AS geom
         FROM extremes_points AS epoints_1, extremes_points AS epoints_2
         WHERE epoints_2.id > epoints_1.id
     )

     -- Intersect those lines
     SELECT DISTINCT ST_intersection(lines_1.geom, lines_2.geom) AS geom
     FROM extremes_lines AS lines_1, extremes_lines AS lines_2
     WHERE ST_GeometryType(ST_intersection(lines_1.geom, lines_2.geom)) = 'ST_Point'

     $BODY$ LANGUAGE SQL;

.. code-block:: sql

   CREATE TABLE intersect_points (
     id   BIGSERIAL PRIMARY KEY,
     geom GEOMETRY
   );

   INSERT INTO intersect_points (geom)
     SELECT intersect_extreme_lines();

   SELECT * FROM intersect_points;


First attempt (plpgsql)
^^^^^^^^^^^^^^^^^^^^^^^

The first two attempts are pretty unelegant and slow compared to the plain
sql version. This one requires an intermediate temporary dataset.

.. code-block:: plpgsql

  CREATE TABLE extremes_points (
      id       BIGSERIAL PRIMARY KEY,
      geom GEOMETRY
    );

  CREATE OR REPLACE FUNCTION connect_linestring_extremes()
    RETURNS VOID AS
    $BODY$
    DECLARE
      current_line   RECORD;   -- Current line
      current_sp     geometry; -- Start point of current linestring
      current_ep     geometry; -- End point of current linestrig
      other_extremes geometry; -- SP/EP of lines with higher id than the current line
    BEGIN

      /* Loop over all lines of test_set */
      FOR current_line IN (
        SELECT *
        FROM test_set
      )
      LOOP
        current_sp := ST_StartPoint(current_line.geom);
        current_ep := ST_EndPoint(current_line.geom);

        /* Loop over all lines in test set with an id > then  id of current_line */
        FOR other_extremes IN (
          SELECT ST_StartPoint(geom)
          FROM
            test_set
          WHERE
            id > current_line.id
          UNION ALL
          SELECT ST_EndPoint(geom)
          FROM
            test_set
          WHERE
            id > current_line.id
        )
        LOOP

          /* Output table with values */
          INSERT INTO extremes_lines (geom) VALUES
            (ST_MakeLine(current_ep, other_extremes)),
            (ST_MakeLine(current_sp, other_extremes));
        END LOOP;
      END LOOP;
    END
    $BODY$ LANGUAGE plpgsql;

.. code-block:: plpgsql

      DO $$
      BEGIN
        PERFORM connect_linestring_extremes();
      END
      $$;

Second attempt (plpgsql)
^^^^^^^^^^^^^^^^^^^^^^^^

Slightly better but still bad

.. code-block:: plpgsql

  CREATE OR REPLACE FUNCTION connect_linestring_extremes2()
    RETURNS SETOF GEOMETRY AS
    $$
      SELECT ST_MakeLine(
          t1.st_startpoint,
          t2.st_startpoint
      )
      FROM
        (
          SELECT
            ST_StartPoint(geom), id
          FROM test_set
          UNION ALL
          SELECT
            ST_EndPoint(geom), id
          FROM test_set
        ) AS t1,
        (
          SELECT
            ST_StartPoint(geom), id
          FROM test_set
          UNION ALL
          SELECT
            ST_EndPoint(geom), id
          FROM test_set
        ) AS t2
      WHERE t1.id > t2.id;
    $$ LANGUAGE SQL;

.. code-block:: plpgsql

      INSERT INTO extremes_lines2 (geom)
        SELECT connect_linestring_extremes2();

.. code-block:: plpgsql

    CREATE OR REPLACE FUNCTION intersect_extreme_lines()
      RETURNS VOID AS
      $BODY$
      DECLARE
        current_line RECORD; -- Current line to be connected to others
        other_lines  RECORD; -- SP/EP of lines with higher id than the current line
      BEGIN
        DELETE FROM intersect_points; -- Reset intersect_points table
        FOR current_line IN (
          SELECT *
          FROM extremes_lines
        )
        LOOP
          FOR other_lines IN (
            SELECT *
            FROM
              extremes_lines
            WHERE
              extremes_lines.id > current_line.id
          )
          LOOP
            INSERT INTO intersect_points (geom)
              SELECT ST_Intersection(current_line.geom, other_lines.geom);
          END LOOP;
        END LOOP;

        /* Remove empty geometries prodcued by ST_Intersection  */
        DELETE FROM intersect_points
        WHERE ST_IsEmpty(geom);

        /* Remove duplicate points */
        DELETE FROM intersect_points
        WHERE intersect_points.id NOT IN (
          SELECT id
          FROM (SELECT DISTINCT ON (geom) *
                FROM intersect_points) AS a);
      END
      $BODY$ LANGUAGE plpgsql;


Execute the function

.. code-block:: plpgsql

      DO $$
      BEGIN
        PERFORM connect_linestring_extremes();
        PERFORM intersect_extreme_lines();
      END
      $$;

      SELECT * FROM intersect_points_plpsql;


Ex 2: Nona Grid
---------------

Create test data
^^^^^^^^^^^^^^^^

.. code-block:: sql

    DROP TABLE IF EXISTS test_set;

    CREATE TABLE test_set (
      id   BIGSERIAL PRIMARY KEY, --in automatically incremented id is almost always a good idea
      geom GEOMETRY --here comes the magic: this column if of type ''geometry''
    );

    INSERT INTO test_set (geom)
    VALUES
      (st_geomfromtext('POLYGON((2.40309828723774 1.4684052885979,2.78140531783743 1.1025017671982,3.03567725643723 1.50561581619787,3.03567725643723 1.50561581619787,2.40309828723774 1.4684052885979))')),
      (st_geomfromtext('POLYGON((0.0996690914231216 0.742986500305513,0.104795724997313 0.922418675402197,1.27879481348706 0.814759370344187,0.0996690914231216 0.742986500305513))')),
      (st_geomfromtext('POLYGON((0.0945424578489315 0.599440760228165,0.0945424578489318 0.414881951557288,2.58608637490576 0.502034722318536,0.0945424578489315 0.599440760228165))')),
      (st_geomfromtext('POLYGON((0.193870983348881 1.94390041505976,0.0343045133521856 1.99324426321135,0.0259737337941256 1.90865480923719,0.193870983348881 1.94390041505976))')),
      (st_geomfromtext('POLYGON((0.232320735155314 1.72794097574696,0.356641599329446 1.77023570273404,0.356000770132672 1.68628707795666,0.232320735155314 1.72794097574696))')),
      (st_geomfromtext('POLYGON((0.145808793590841 1.83816359759207,0.183617716200499 1.73627175530502,0.247700635877887 1.83303696401788,0.145808793590841 1.83816359759207))')),
      (st_geomfromtext('POLYGON((0.0554518768457236 1.81701623409853,0.00226305351349254 1.71896936699213,0.0894158242747396 1.71704687940181,0.0554518768457236 1.81701623409853))')),
      (st_geomfromtext('POLYGON((4.03346953290769 0.179990861663712,0.0974346370780548 0.0669736931977908,0.127076883310316 0.248787340179801,4.03346953290769 0.179990861663712))')),
      (st_geomfromtext('POLYGON((2.73876393103716 2.03802220333592,4.05887207639138 2.03545888654882,4.05374544281719 3.02489916636771,3.20016095271436 3.032589116729,3.20272426950146 2.66603481617433,2.73107398067587 2.65321823223886,2.73876393103716 2.03802220333592))')),
      (st_geomfromtext('POLYGON((1.51773029298447 2.91605720717402,1.51783356166834 2.81451478834183,1.65441786573918 2.81718137381279,1.51773029298447 2.91605720717402))')),
      (st_geomfromtext('POLYGON((1.36519135820989 2.80366736035583,1.36364321638798 2.69798764647994,1.50047611200803 2.70212448446307,1.50248108256427 2.80329301458742,1.36519135820989 2.80366736035583))')),
      (st_geomfromtext('POLYGON((1.3644680460472 2.91482267420021,1.36646667175991 2.81279759019899,1.49550809952216 2.81789884439904,1.50114232057894 2.91514626122036,1.3644680460472 2.91482267420021))')),
      (st_geomfromtext('POLYGON((1.80415301315647 2.77409404465126,1.76607760711846 2.80333108364862,1.80457177282962 2.80263949570359,1.80415301315647 2.77409404465126))')),
      (st_geomfromtext('POLYGON((1.65240973523523 2.70445304203947,1.51374952467785 2.69871095864264,1.51641435896146 2.80498708781058,1.65240973523523 2.70445304203947))')),
      (st_geomfromtext('POLYGON((1.66376066031471 2.8032295661521,1.66770080814834 2.69868557926851,1.80773150490874 2.70243538179616,1.66376066031471 2.8032295661521))')),
      (st_geomfromtext('POLYGON((1.66714246191749 2.91533660652634,1.67091764381929 2.81536090698608,1.80421011674824 2.81640146132539,1.66714246191749 2.91533660652634))')),
      (st_geomfromtext('POLYGON((1.66727570363168 3.02869992591998,1.66701556504685 2.92703649800011,1.80535218858408 2.92751870610857,1.66727570363168 3.02869992591998))')),
      (st_geomfromtext('POLYGON((1.51393352514029 3.02989910134761,1.51615422037663 2.92855926044788,1.65320918552031 2.92997416055561,1.51393352514029 3.02989910134761))')),
      (st_geomfromtext('POLYGON((1.36270417954519 3.02800199313141,1.3630785253136 2.92741084376852,1.5016816322792 2.92829277701952,1.50194811570756 3.02795123438316,1.36270417954519 3.02800199313141))')),
      (st_geomfromtext('POLYGON((2.72594734710168 2.90442327737422,2.88102801272096 2.90442327737422,2.87910552513064 3.0204133619903,3.1597887133176 3.02297667877739,3.16107037171115 2.703843738784,2.72402485951136 2.70063959280012,2.72594734710168 2.90442327737422))')),
      (st_geomfromtext('POLYGON((0.306576818331486 2.01559318144883,0.306897232929874 1.91274009536663,0.393729589092733 1.9156238267521,0.394050003691121 2.01559318144883,0.306576818331486 2.01559318144883))')),
      (st_geomfromtext('POLYGON((0.404033175919342 1.98190124727006,0.419454806633041 1.96212820230717,0.433992645064481 1.98172052707328,0.404033175919342 1.98190124727006))')),
      (st_geomfromtext('POLYGON((2.71721604929565 2.99838485835123,2.76207409306982 2.99934610214639,2.76303533686498 3.02914465979637,2.71721604929565 2.99838485835123))')),
      (st_geomfromtext('POLYGON((0.0140081489135115 3.02537157169423,0.00494883219698153 2.95874479183339,0.0277300943227677 2.93662132801847,0.0739221350283838 2.95344274233581,0.100836961292888 3.02649727076803,0.0140081489135115 3.02537157169423))')),
      (st_geomfromtext('POLYGON((4.07162546919071 0.00133239413789184,4.05739710751661 0.00148394083104753,4.06366922606253 0.010953282441011,4.07162546919071 0.00133239413789184))')),
      (st_geomfromtext('POLYGON((2.86244396601452 2.92364815327744,2.72338403031458 2.92364815327744,2.80028353392745 2.97683697660967,2.86084189302259 3.02201543498223,2.86244396601452 2.92364815327744))')),
      (st_geomfromtext('POLYGON((0.0486430666299815 0.0931055911271812,-0.000220159624029492 0.0011466013901239,0.111284120614632 0.0251776962691462,0.0486430666299815 0.0931055911271812))')),
      (st_geomfromtext('POLYGON((0.0197256491253304 0.0940868608346643,0.0761186184414364 0.00949740686050521,0.103674273902716 0.0857560812766031,0.0197256491253304 0.0940868608346643))'));

    drop function if exists nona_grid ();
    drop function if exists nona_grid (text, text, text);


Nona grid spatial index (Plpython)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: guess

    CREATE OR REPLACE FUNCTION nona_grid(input_set text, create_grid_points text default 'False', geometrycolumn text default 'geom')
      RETURNS VOID AS
      $$

    import os, sys #, logging

    # The "create_grid_points" option defines wether or not a dataset
    # containing the corner points of the quadrants should be created.
    # It's only in there for debugging purposes.

    # LOG_FILENAME = '/tmp/plpython.log'
    # logging.basicConfig(filename=LOG_FILENAME, level=logging.DEBUG)
    # logging.debug('============================================')
    # logging.debug('python version: %s' % sys.version)
    # view with sudo tail -f /tmp/plpython.log


    def flatten_plyresult(x):
        x = x[0]
        x = x[list(x.keys())[0]]
        return x


    def bb_max(input_set, parameter, geometrycolumn):
        sql_query = "SELECT %s(ST_Extent(%s)) FROM %s;" % (parameter, geometrycolumn, input_set)
        cur = plpy.cursor(sql_query)
        x = cur.fetch(1)
        x = flatten_plyresult(x)
        return (x)


    def bb_xmax(x=input_set):
        return bb_max(x, 'st_xmax', geometrycolumn)


    def bb_xmin(x=input_set):
        return bb_max(x, 'st_xmin', geometrycolumn)


    def bb_ymax(x=input_set):
        return bb_max(x, 'st_ymax', geometrycolumn)


    def bb_ymin(x=input_set):
        return bb_max(x, 'st_ymin', geometrycolumn)


    def calculate_dataset_boundaries(input_set=input_set):
        boundaries = {}
        boundaries["xmax"] = bb_xmax(input_set)
        boundaries["xmin"] = bb_xmin(input_set)
        boundaries["ymax"] = bb_ymax(input_set)
        boundaries["ymin"] = bb_ymin(input_set)
        return boundaries


    def create_grid_points_table():
        sql_query = '''
          DROP TABLE IF EXISTS grid_points;

          CREATE TABLE grid_points (
            id   BIGSERIAL PRIMARY KEY, --in automatically incremented id is almost always a good idea
            gp   TEXT,
            geom GEOMETRY --here comes the magic: this column if of type ''geometry''
          );'''
        plpy.execute(sql_query)


    def calculate_grid_points(boundaries, create_table=eval(create_grid_points)):
        grid_cell_length_x = ( boundaries["xmax"] - boundaries["xmin"]  ) * 1. / 3.
        grid_cell_length_y = ( boundaries["ymax"] - boundaries["ymin"]  ) * 1. / 3.
        grid_points = {}

        for i in range(0, 4):
            for j in range(0, 4):
                if (i == 3):
                    x = boundaries["xmax"]  # necessary to prevent misclassification of polygons due to rounding errors!
                else:
                    x = boundaries["xmin"] + i * grid_cell_length_x
                if (j == 3):
                    y = boundaries["ymin"]  # necessary to prevent misclassification of polygons due to rounding errors!
                else:
                    y = boundaries["ymax"] - j * grid_cell_length_y

                value = (x, y)
                key = "gp" + str(i) + str(j)
                if create_table == True:
                    sql_string = '''INSERT INTO grid_points (geom, gp) VALUES (st_makepoint(%s, %s), '%s');''' % (x, y, key)
                    plpy.execute(sql_string)
                grid_points[key] = value

        return grid_points


    def calculate_polygon_bbs(input_set=input_set):
        sql_xmin = "SELECT st_xmin(st_envelope(geom)) as polygon_bb FROM %s;" % input_set
        sql_xmax = "SELECT st_xmax(st_envelope(geom)) as polygon_bb FROM %s;" % input_set
        sql_ymin = "SELECT st_ymin(st_envelope(geom)) as polygon_bb FROM %s;" % input_set
        sql_ymax = "SELECT st_ymax(st_envelope(geom)) as polygon_bb FROM %s;" % input_set
        sql_id = "SELECT id FROM %s;" % input_set
        geoms = {}

        try:
            cur_xmin = plpy.cursor(sql_xmin)
            cur_xmax = plpy.cursor(sql_xmax)
            cur_ymin = plpy.cursor(sql_ymin)
            cur_ymax = plpy.cursor(sql_ymax)
            cur_id = plpy.cursor(sql_id)

            while True:
                xmin = cur_xmin.fetch(1)
                xmax = cur_xmax.fetch(1)
                ymin = cur_ymin.fetch(1)
                ymax = cur_ymax.fetch(1)
                id = cur_id.fetch(1)

                if not xmin: break

                xmin = flatten_plyresult(xmin)
                xmax = flatten_plyresult(xmax)
                ymin = flatten_plyresult(ymin)
                ymax = flatten_plyresult(ymax)
                id = flatten_plyresult(id)

                polygon = {}
                polygon["xmin"] = xmin
                polygon["xmax"] = xmax
                polygon["ymin"] = ymin
                polygon["ymax"] = ymax

                key = id
                geoms[key] = polygon

        except plpy.SPIError as e:
            return "ERROR:" + str(e)
        return geoms


    def identify_nona_col(polygon_bb, nona_grid):
        xmax = polygon_bb['xmax']
        xmin = polygon_bb['xmin']
        grid_x0 = nona_grid['gp00'][0]
        grid_x1 = nona_grid['gp10'][0]
        grid_x2 = nona_grid['gp20'][0]
        grid_x3 = nona_grid['gp30'][0]
        col = 9

        if (xmin >= grid_x0) and (xmax < grid_x1):
            col = 0
        elif (xmin >= grid_x1) and (xmax <= grid_x2):
            col = 1
        elif (xmin > grid_x2) and (xmax <= grid_x3):
            col = 2
        return col


    def identify_nona_row(polygon_bb, nona_grid):
        ymax = polygon_bb['ymax']
        ymin = polygon_bb['ymin']
        grid_y0 = nona_grid['gp00'][1]
        grid_y1 = nona_grid['gp01'][1]
        grid_y2 = nona_grid['gp02'][1]
        grid_y3 = nona_grid['gp03'][1]
        row = 9

        if (ymin > grid_y1) and (ymax <= grid_y0):
            row = 0
        elif (ymin >= grid_y2) and (ymax <= grid_y1):
            row = 1
        elif (ymin >= grid_y3) and (ymax < grid_y2):
            row = 2
        return row


    def calculate_grid_cell_boundaries(row, col, grid):
        key_lu_corner = "gp" + str(col) + str(row)
        key_rl_corner = "gp" + str(col + 1) + str(row + 1)
        lu_corner = grid[key_lu_corner]
        rl_corner = grid[key_rl_corner]
        sub_boundaries = {}
        sub_boundaries["xmax"] = rl_corner[0]
        sub_boundaries["xmin"] = lu_corner[0]
        sub_boundaries["ymax"] = lu_corner[1]
        sub_boundaries["ymin"] = rl_corner[1]
        return sub_boundaries


    def calculate_nona_index(polygon, grid, index_start=0):
        col = identify_nona_col(polygon, grid)
        row = identify_nona_row(polygon, grid)
        pos = 0
        nona_index = str(index_start)
        if (row < 9) and (col < 9):
            pos = (col + 1) + 3 * (row)
            nona_index = nona_index + str(pos)
            sub_boundaries = calculate_grid_cell_boundaries(row, col, grid)
            sub_grid = calculate_grid_points(sub_boundaries, create_table=eval(create_grid_points))
            nona_index = calculate_nona_index(polygon, sub_grid, nona_index)
            return int(nona_index)
        else:
            return int(nona_index)


    def index_all_polygons(polygons_bb, nona_grid):
        indices = {}
        for key in polygons_bb:
            id = key
            nona_index = str(calculate_nona_index(polygons_bb[key], nona_grid))
            indices[id] = nona_index
        return indices


    def create_nona_table(input_set, nona_indices):
        table_name = "nona_" + input_set
        sql_query = '''
          DROP TABLE IF EXISTS %s;
          CREATE TABLE %s (id BIGSERIAL PRIMARY KEY, index INTEGER);''' % (table_name, table_name)
        plpy.execute(sql_query)

        for row in nona_indices:
            sql_query = "INSERT INTO %s (id, index) VALUES (%s, %s);" % (table_name, row, nona_indices[row])
            plpy.execute(sql_query)


    dataset_boundaries = calculate_dataset_boundaries(input_set)
    polygons_bb = calculate_polygon_bbs(input_set)

    if eval(create_grid_points) == True: create_grid_points_table()
    main_grid = calculate_grid_points(dataset_boundaries, create_table=eval(create_grid_points))

    nona_indices = index_all_polygons(polygons_bb, main_grid)
    create_nona_table(input_set, nona_indices)

    $$
    LANGUAGE plpython3u;

.. code-block:: psql

    -- if set to 'False' no grid points table will be created
    select nona_grid('test_set', 'True');
