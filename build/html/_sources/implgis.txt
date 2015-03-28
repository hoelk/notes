IMPLGIS - Notes
###############

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

Algorythms
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
-------------

http://en.wikipedia.org/wiki/R-tree

* Balanced (all leaf nodes at the same level)
* Maintains references to DB in leaves
* Variable fanout (between m and M) (number of children per node)
* Most popular SAM

R-Tree Basics
-------------
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
----------

Hash Tables
-----------

* insertion, deletion and search work in **constant time**
* requires O(|U|) storage space (which is a lot)
* Only acceptable when |K| (set of used key) is similar to |U| (set of possible keys)
* Usually |K| is much smaller than |U|





IMPLGIS - Plpython
##################

IMPLGIS - plypython
-------------------

Data Types
    * None
    * Boolean
    * Numbers (Integer, Long, Float, Complex)
    * Sequences (Strings, Lists, Tuples, Dictionaries)


Scope of a variable, is the area of code where a variable is defined

    * Input parameters of a function only exist in the body of the function
    *


Homework
========

Assignment 1
^^^^^^^^^^^^

Given a spatial dataset S1 consisting of linestrings write an SQL function that
does the following:
    * computes the straight lines connecting the 2 extremes of each linestring in S1 to the extremes of any other linestring in S
    * creates a new dataset S2 consisting of all the intersection points between the lines computed in the previous step (without repetitions)

Create the test dataset
-----------------------

.. code-block:: plpgsql

    CREATE TABLE test_set (
      id       BIGSERIAL PRIMARY KEY, --in automatically incremented id is almost always a good idea
      the_geom GEOMETRY --here comes the magic: this column if of type "geometry"
    );

    INSERT INTO test_set (the_geom)
    VALUES
       (st_geomfromtext('LINESTRING(-46 -40, -4 -6, -5 -5, -6 -4, -8 -5, 50 30 )')),
       (st_geomfromtext('LINESTRING(-3 -10, -10 -5, 17 3, 23 66)')),
       (st_geomfromtext('LINESTRING(-20 20, -2 0, 15 -15, 65 -1)')),
       (st_geomfromtext('LINESTRING(-50 -50, -47 46)')),
       (st_geomfromtext('LINESTRING(70 70, 80 -40, 0 -50 )'));

Connect the extremes (start and endpoints) of each line
-------------------------------------------------------

First attempt requiring a temporary dataset (36 sec on 1000 lines)

.. code-block:: plpgsql

  CREATE TABLE extremes_points (
      id       BIGSERIAL PRIMARY KEY,
      the_geom GEOMETRY
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
        current_sp := ST_StartPoint(current_line.the_geom);
        current_ep := ST_EndPoint(current_line.the_geom);

        /* Loop over all lines in test set with an id > then  id of current_line */
        FOR other_extremes IN (
          SELECT ST_StartPoint(the_geom)
          FROM
            test_set
          WHERE
            id > current_line.id
          UNION ALL
          SELECT ST_EndPoint(the_geom)
          FROM
            test_set
          WHERE
            id > current_line.id
        )
        LOOP

          /* Output table with values */
          INSERT INTO extremes_lines (the_geom) VALUES
            (ST_MakeLine(current_ep, other_extremes)),
            (ST_MakeLine(current_sp, other_extremes));
        END LOOP;
      END LOOP;
    END
    $BODY$ LANGUAGE plpgsql;

  // Usage:
  DO $$
  BEGIN
    PERFORM connect_linestring_extremes();
  END
  $$;

Second attempt, slightly faster (30 sec on 1000 lines)

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
            ST_StartPoint(the_geom), id
          FROM test_set
          UNION ALL
          SELECT
            ST_EndPoint(the_geom), id
          FROM test_set
        ) AS t1,
        (
          SELECT
            ST_StartPoint(the_geom), id
          FROM test_set
          UNION ALL
          SELECT
            ST_EndPoint(the_geom), id
          FROM test_set
        ) AS t2
      WHERE t1.id > t2.id;
    $$ LANGUAGE SQL;

  // Usage
  INSERT INTO extremes_lines2 (the_geom)
    SELECT connect_linestring_extremes2();

Intersect the resulting lines

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
            INSERT INTO intersect_points (the_geom)
              SELECT ST_Intersection(current_line.the_geom, other_lines.the_geom);
          END LOOP;
        END LOOP;

        /* Remove empty geometries prodcued by ST_Intersection  */
        DELETE FROM intersect_points
        WHERE ST_IsEmpty(the_geom);

        /* Remove duplicate points */
        DELETE FROM intersect_points
        WHERE intersect_points.id NOT IN (
          SELECT id
          FROM (SELECT DISTINCT ON (the_geom) *
                FROM intersect_points) AS a);
      END
      $BODY$ LANGUAGE plpgsql;
