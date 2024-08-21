# Types of Internal Structure Indexes

- fast searching in relational databases is based on the use of indexes. Instead of searching the entire content of records in one or more tables to find the desired results, the query optimizer significantly shortens the search process by using indexes created on those same tables.
  - It is common to classify indexes based on their role in a specific table into:
    - primary indexes (keys)
    - unique indexes
    - "regular" indexes

## B-Tree Indexes

- in most cases, when database indexes are mentioned in relational database management systems, B-Tree indexes or their variants are usually implied.

  - B-Tree indexes were developed based on the work of Rudolf Bayer and Edward McCreight in 1972. Although their name is very similar to binary trees, they differ in several important characteristics. These experts developed B-Tree indexes to overcome the practical shortcomings of binary trees for use with large databases.

  ![binary tree example](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2018/indeksi-1.png)

- in a binary tree, each node can point to a maximum of two elements (children or descendants), and the node itself contains the key by which it is arranged in the binary tree, as well as the node's value (data).

  - a binary tree represents an efficient structure for data searching but has shortcomings when data needs to be frequently modified.
  - in extreme cases, after modifying a single piece of data, the entire tree may need to be reorganized, which is practically unusable in database management systems due to performance degradation.

- in B-Tree indexes, each node can contain multiple key values and can point to a larger number of elements (children or descendants).

  ![B-Tree example](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2018/indeksi-2.png)

- from a data search perspective, B-Tree indexes are similar to binary trees, except instead of two possible lower-level element values, the search decision now needs to be made based on a larger number of possible elements that the node points to.
  - the algorithm for making such a decision is slightly more complex than in a binary tree, but due to the possibility of having more child elements than in a binary tree (a maximum of two), the overall search time is shorter, requiring fewer levels to reach the desired result.
  - operations like adding and deleting data are also much more efficient than in a binary tree.
    - The larger number of possible elements at the lower level of the tree often allows new values to be added without the need for detailed restructuring of data throughout the tree.
    - in the case of deletion, leaving an empty space in the structure also reduces the need for changes across the entire tree.
  - B-Tree indexes are particularly suitable for storing data on external media such as disks (as used by most databases due to the difference in capacity between external and RAM memory), which are significantly slower in data access than RAM memory.
    - accessing specific data on external media using B-Tree indexes significantly reduces the number of reads due to the fast traversal from the top to the bottom of the tree in a relatively small number of steps.

## B+Tree Indexes

- B+Tree indexes represent a specially modified version of B-Tree indexes where only the lowest level nodes (so-called leaf nodes) contain actual data, while all other higher-level nodes contain only keys and links to other nodes in the tree.

  - this tree organization requires fewer operations on the tree when updating data compared to the basic B-Tree index form, which is why it is used in many relational database management systems (e.g., SQL Server, MySQL InnoDB, and others).

  ![B+Tree example](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2018/indeksi-3.png)

## T-Tree Indexes

- the main idea behind the development of T-Tree indexes was the assumption that constant hardware development leads to servers with enormous amounts of RAM where even the largest databases can be implemented without the need for slow external media. In this type of index, nodes can contain entire arrays of data. As a result, add and delete operations often conclude within such an array without the need to create new nodes or remove existing ones.

  - each node in the tree contains a pointer to the parent node and two child nodes, making it similar to a binary tree. T-Tree indexes are used in database management systems that aim to store all database data in the computer's RAM (e.g., Oracle TimesTen).
  - a problem with T-Tree indexes may arise from insufficient utilization of available data storage in individual tree nodes (depending on the type of data) and slower traversal through the binary-organized tree compared to B-Tree indexes. This second drawback should be compensated by the fact that the entire tree structure is in RAM, which operates much faster than external media.
    - recent research comparing the performance of B-Tree and T-Tree indexes has shown that T-Tree index performance declines if database operations require a large number of locks on existing data, causing them to lose their speed advantage over B-Tree indexes.

  ![T-Tree example](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2018/indeksi-4.png)

## R-Tree Indexes

- for certain categories of data, none of the previously mentioned types of indexes represent an optimal choice. This usually applies to special types of data, such as geographically oriented data, where the database often needs to respond to queries about the spatial distribution of objects (e.g., a list of all museums within 3 km of a given reference point). In such cases, R-Tree indexes, whose conceptual originator was Antonin Guttman in 1984, offer a better solution.

  - R-Tree indexes group close objects into the smallest possible rectangle that encompasses them. At the lowest node level, this rectangle is an individual object, while higher levels represent groupings of two or more close objects.
  - the biggest problem with R-Tree indexes is the relatively low data occupancy in the tree and the possibility of constructing theoretical examples where using R-Tree trees is very problematic (fortunately, this is not the case for most real-world examples). R-Tree indexes are often added to standard database implementations as special modules if needed (e.g., IBM Informix Spatial DataBlade Module).

  ![R-Tree example](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2018/indeksi-5.png)

## Fractal Indexes

- Fractal indexes are fundamentally similar in structure to B-Tree indexes, with one very significant enhancement.
  - the nodes in the tree contain special buffers for temporarily storing changes in the nodes during add or delete operations.
  - the idea of using such buffers is that each small change in the tree is not immediately written to the external (slow) medium but is recorded all at once along with a larger number of changes collected in the buffers of various nodes.
  - in this way, a significantly faster operation speed is achieved for most data modification operations in tables than with classic B-Tree or B+Tree indexes.
  - an example of the implementation of fractal indexes is TokuDB—a special Storage Engine module for MySQL or MariaDB.
