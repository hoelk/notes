Programming of Cartographic Tasks - Assignments
###############################################

2015-03-27
==========

Assignment 1 start
------------------

* Setup this diary
* Basic project setup:
    * Outline project
    * Setup version control
* Migrated code from lab
    * Refactoing the draw map function into smaller functions

2015-03-28 Refactoring and implementing
---------------------------------------

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
-------------------------------

* Clean up code
* Better colours for the graphs

2015-04-08 Added a Legend
-------------------------

* Added a legend to the map

Assignment 2
============

2015-05-17 Project start
------------------------

* Copied the lecture 6 example code files and removed code that
    is not required for this assignment
* Implemented buttons to switch between income-variables

2015-05-19
-----------

* Removed more of the lecture 6 example code that is not required for this exercise
* Added legend. I tried as svg element first, but then decided to create an
    html overlay and construct the legend from div elements.
    SVG would have the advantage that the whole map is one image that the user
    could save; but ultimately I decided to do it as an html overlay
    to have an unified look for infobox and legend.
* Added an infobox that displays district details after clicking on a district.
* Adapted variable and function names to google style guide for JS
* Cleaned up code, moved functions into a logical order

2015-05-20

* Changed projection to azimuthalEquidistant. Technically speaking
    azimuthalEqualArea would probably better as is preserves relative
    area, but I still decided on azimuthalEquidistant because it
    looks subjectively more familiar, and area preservation
    was not a priority for this kind of data (on this scale).
* Added a few comments to the source code
