Programming of Cartographic Tasks - Assignments
###############################################

2015-03-27 Project start
========================

* Setup this diary
* Basic project setup:
    * Outline project
    * Setup version control
* Migrated code from lab
    * Refactoing the draw map function into smaller functions

2015-03-28 Refactoring and implementing
=======================================

* Refactoring drawing function into functions to:
    * draw bars
    * draw circles
    * calculate positon
* First version: Draw mean income
* Second version: Draw sepparate bars for mean income of men and women
* Removed coloring the population-size circles by county as it is not required
    by the assignment and distracts from the income information.

I first wanted to make a generic element drawing function with different
input parameters, but the decided against it because of the fine tuning
required for each element (especially psoitioning).

2015-04-03 Project finalisation
===============================

* Clean up code
* Better colours for the graphs

2015-04-08 Added a Legend
=========================

* Added a legend to the map
