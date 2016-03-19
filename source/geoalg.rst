Geometric Algorithms
####################

Exam Topics
===========

* Basic geometric problems
    * f.e. pseudocode for point in polygon, line intersection, etc..
* Asymptotic notation
    * 3x proof f(m) = O(g(m))
    * 2x analyse runtime of algorithm
* Plane sweep
    * Open questions
    * Application to one computational geometry problem
    * Look at plain approach vs polar sweep
    * What kinds of data structures do you need, etc..


* Computational Geometry - Algorithms and Applications

point position
--------------
http://en.wikipedia.org/wiki/Cross_product

plane sweep
-----------
* A methodology, not an algorythm
* A line that sweeps from top to bottom introduces an order to the lines
* Only check neighbors for intersection

data structures:
    * Point
    * Line
    * Q: Event Que: Ordered (first) from top to bottom and (second) from left to right
        * Discretices position of the sweep line
        * self-balancing binary search tree as data structure for the que
            * BST = Binary tree with sorted elements
                * right children smaller than parent
                * left children bigger than parent
                * allows searching in log time
            https://en.wikipedia.org/wiki/Binary_search_tree
    * S: Status Structure
        Indicates which lines intersect sweep line

Que vs Stack
------------

http://en.wikipedia.org/wiki/Queue_%28abstract_data_type%29

* List with specific rules for inputing and outputing element
* Que: First element put in, is the first to take out
* Stack: Last element put in is first to take out

* 'pop': take on element from a list and return it
