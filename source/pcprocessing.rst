Point Cloud Processing
######################

! Different Terms: Coordinate System / Coordinate Frame


Data Structures
###############
 basis: binary search trees  (small, only two pointers per node, awesome in memory)
 b-tree: more than two children, on hard drive (larger chunks can be written at once)

 Quad / Octree: good for dynamic insertions / deletions as tree always says the same
 Bad if you have an imhomogenous point distrubtions (tree is badly balanced

 R/tree:

    Outperforms quad/octree and does not care about inhomogenous point distribution but number of points only.
    Based on bounding boxes of point sets, important to minimize coverage and overlap of bounding boxes, different algorithms exist
    heavy update operations lead to unballanced trees

KD tree : Split at median, awesome for NN search (only need one comparison per node), static data structure, works only well in memory
