# SQL vs NoSQL

## SQL Database

### History

- the theoretical foundation for what is today the leading relational database type was laid over four decades ago by Edgar F. Codd in his paper, _A Relational Model of Data for Large Shared Data Banks_ (published in 1970 in the _Communications of the ACM_). Based on this work, a team of IBM researchers developed the first database management system, `System R`, at the San Jose Research Center.
  - in System R, all operations on data were performed using a special language called **Structured English Query Language** or **SEQUEL** for short. Since the acronym SEQUEL was already trademarked by the British company Hawker-Siddeley, the original name of the language was shortened to `SQL (Structured Query Language)`. while System R was based on Codd's work, the SQL language itself was developed by two other IBM experts, Donald D. Chamberlin and Raymond F. Boyce.

### Properties and Advantages

1. due to its long presence in the market, SQL is well-known both theoretically and practically, resulting in high-quality and stable software solutions from various vendors.
2. accessing and performing operations on data is done using the standardized and well-known SQL query language. There is extensive support available for this language in various forms (books, manuals, courses, etc.).
3. the financial aspects of implementing relational databases are well-understood, making it easier to plan costs for introducing new systems or upgrading existing ones.
4. basic concepts in the relational model (such as tables, columns, etc.) are relatively simple to understand.

### Disadvantages

1. relational databases (especially older versions) do not directly support some of the data types that are increasingly common in modern business and/or multimedia-oriented IT systems.
2. when grouping basic data types into more complex data structures, the relational data model often is not optimal regarding system performance.
3. the standard SQL query language is also not the optimal choice for accessing non-standard data types.
4. to access data, it is necessary to understand the structure and organization of the database.
5. internal resource locking mechanisms are not suitable for certain complex data types.

## NoSQL Database

- NoSQL databases aim to address the shortcomings of relational databases in various ways.
  - therefore, it's not possible to speak of a single NoSQL database model but rather of a larger number of different models supported by various vendors. Some of the most important groups of NoSQL databases include:
    - Document Databases
    - Graph Databases
    - Columnar Databases
    - In-Memory Data Grids

### Document Databases

- tne of the most well-known forms of NoSQL databases are document databases.

  - instead of using tables to store simple data types in columns, in this model, the basic "data unit" is a document, along with various additional metadata about the document itself.
  - if only one specific type of document needs to be stored in the database, such a case can be relatively easily simulated in relational databases by using additional columns with the most important metadata about the document.
  - problems with the relational model arise when a large amount of diverse documents need to be stored in the same database.
  - in such cases, document databases represent a more suitable way of storing data. Along with natural support for storing different types of documents and their metadata, they also allow for the establishment of appropriate relationships between documents.

- one of the most well-known examples of a document database is `MongoDB`.
  - MongoDB uses data prepared in the `JSON (JavaScript Object Notation)` format for storing documents, with support for dynamic data schemas. This means that when starting to work with the database, it's not necessary to know all the details about the documents that will be stored in the database.

### Graph Databases

- this type of database is based on graph theory, where the key concepts managed during data processing are nodes and properties.
  - such a data structure is particularly suitable for establishing very complex relationships among data, as often required in modern business environments (and beyond).
  - the most popular graph database management system is `Neo4j`.

### Columnar Databases

- this type of database emphasizes fast data access, as in today's systems with vast amounts of data, access speed is becoming an increasingly significant problem.
  - SQL can still generally be used as the query language, which is certainly one of the important advantages, as there is no need to learn a completely new language to use the database.

#### Example

- the way this data organization speeds up data access compared to the standard relational model is easiest to explain with an example.

  - the overall speed of data access is largely influenced by their organization on disks (due to the slowness of disks compared to other computer components). Let's assume the following data needs to be stored:

| EmpID | Lastname | Firstname | Salary |
| ----- | -------- | --------- | ------ |
| 10    | Smith    | Joe       | 40000  |
| 12    | Jones    | Mary      | 50000  |
| 11    | Jonson   | Cathy     | 44000  |
| 22    | Jones    | Bob       | 55000  |

- in a relational database model, the above data is sequentially stored on the disk as:

  ```sql
  001:10,Smith,Joe,40000;002:12,Jones,Mary,50000;003:11,Johnson,Cathy,44000;004:22,Jones,Bob,55000;
  ```

- in column-oriented databases, the data is stored on disk in a completely different order (or even as separate files):

  ```sql
  10:001,12:002,11:003,22:004;Smith:001,Jones:002,Johnson:003,Jones:004;Joe:001,Mary:002,
  Cathy:003,Bob:004;40000:001,50000:002,44000:003,55000:004;
  ```

  - in this model, the data looks like a larger number of indexes from the relational model listed one after another. In cases where the same data is repeated (e.g., the name "Jones" in the previous example), it is possible to simply list all the places where such data appears instead of writing the same data multiple times. This automatically achieves compression of the stored data. For example:

    ```sql
    …;Smith:001,Jones:002,004,Johnson:003;…
    ```

![Comparison of different ways of data saving](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2019/slika02.png)

### In-Memory Data Grids

- one of the simplest ways to speed up database operations is to store part of the database (or the entire database) in the computer's RAM instead of much slower disks.

  - many database vendors, regardless of their internal organization, now offer this possibility.
  - in a relational database, part of the data (or all data) can always reside in the computer's RAM, but it still remains a standard relational database model.
  - a special type of database, In-Memory Data Grids, not only maps data from disks to RAM but also offers performance improvements through various changes in data organization.
    - instead of storing data in the form of records or columns (as in the previously explained database models), in this model, data is usually stored as key/value pairs.
  - these changes lead to some limitations of the standard relational database capabilities (e.g., some SQL query or indexing capabilities), but they also offer numerous advantages for systems with a large number of processors (high query execution speed and easy addition of new hardware resources).

    ![Activating a new hardware resources](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2019/slika03.png)

## Relation database - MariaDB

- `MariaDB`, currently one of the most popular relational database management systems (developed by the same creators as MySQL), allows the use of various modules for accessing data stored on disk at the lowest system level (Storage Engine). Besides the default general-purpose modules (XtraDB up to version 10.1 and InnoDB from version 10.2), MariaDB supports the use of various additional modules.
  - one such module is MariaDB ColumnStore, which allows the replacement of relationally-oriented data organization on disk with column-oriented data storage (as explained in detail earlier).
    - the MariaDB ColumnStore module still supports existing SQL syntax but is better suited for working with very large amounts of data. In the same query, it is even possible to link tables with different data organizations—relationally organized tables and column-oriented tables.
    - this approach demonstrates one possible way in which relational database vendors can enhance the classic relational model by including support for other forms of data organization while retaining all the advantages of the basic relational model.

### JSON

- one way relational databases can be extended to support unstructured data types is by using the well-known JSON (JavaScript Object Notation) data format.

- since JSON data is essentially a specially organized type of text data, it can be stored in ordinary tables as a separate column in the database.

  - for example, in Microsoft SQL Server, this is a column of type nvarchar(max). This means that all standard features for text-oriented data types (indexes, functions, etc.) are available for JSON data in the table.
  - there are two possible approaches to handling JSON data:

    - simpler – all JSON processing is done in the application using the data, while the database treats it as ordinary text.
    - advanced – the database "understands" the JSON data type and directly supports it with additional extensions in the SQL language.

- newer versions of SQL Server have many built-in extensions for the JSON data type, so it is possible to combine parts for accessing standard relational data and JSON records in the same SQL query.
