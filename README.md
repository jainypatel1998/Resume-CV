# KD-Trees and PR-QuadTrees

## Overview



## What you need to implement



## Code base

### Top level




### KD-Tree and Bounded Priority Queue


### PR-QuadTree



### Goodies

 * If you are using the `Archiver` class to generate archives, you
   might find that you have problems if you somehow have a large chain
   of "recursive" directory structures. If this happens, try using
   `AdvancedArchiver` or the `ant` build file `build.xml`, which you
   can run from the terminal by running `ant` in the top-level
   directory.
 * Take a look at `KDTree.treeDescription()` and
   `PRQuadTree.treeDescription()` for visualizations of your trees
   that you can generate. Those visualizations follow, more or less,
   the style of http://jimblackler.net/treefun/index.html

### Important note about implementation of spatial queries



## Hints

 * Don't spend too much time reviewing `BigDecimal`. Just make sure
   you understand that you compare them using `equals()`,
   `compareTo()`, and you can always retrieve an underlying `double`
   valud by applying the "getter" method `doubleValue()`. You do
   **not** need to understand how `BigDecimal` ensures immeasurably
   higher accuracy than a primitive `double` in this project.

 * For the KD-Tree component:

    * For deletions, consider the routine `findMin()` that we did in
      class. How can you use it to cover the special cases of
      deletion?

    * Consider the theory behind range and NN-Queries **before** you
      attempt to implement them. How do we behave in the
      descending/greedy phase? How do we behave in the
      ascending/pruning phase? What about the edge cases? How do we
      behave?

    * You can choose to leave the implementation of
      `BoundedPriorityQueue` implementation for after you implement
      `kNearestNeighbors()` if you wish, but realize that proper
      $`k`$-NN functionality depends on proper BPQ functionality.

 * For the PR-QuadTree component:

    * There are three types of students in this class. Those who study
      the parameter `PRQuadTreeNode.k` **well**, those who don't, and
      others.

    * In the backtracking phase of the range and nearest neighbor
      queries in a PR-QuadTree, while you **should** only recurse to
      quadrants which **intersect** with the given range (or current
      *worst* range, for $`k`$-NN), you should **not** be prioritizing
      the quadrants by the area of intersection; instead, keep it
      simple and loop through only the **valid** quadrants in
      **Z-order**. Finding the area of intersection is a hard
      numerical problem which we will not solve in this project.

   * Speaking of intersection of a quadrant with a given range, check
     the `protected` method
     `PRQuadNode.doesQuadIntersectAnchorRange()`. It might be useful
     to you.
