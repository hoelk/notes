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
