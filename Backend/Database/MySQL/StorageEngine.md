# MySQL Storage Engine

- a specific feature of the architecture of the relational database management system MySQL is that the lowest layer (`MySQL Storage Engine - MSE`) allows the use of different modules for accessing data stored on disk.

![MySQL system architecture](https://sistemac.srce.hr/sites/sistemac.srce.hr/files/docs/2017/mysql-dbe-1.png)

- the available and most popular modules for MSE are:
  - MyISAM
  - InnoDB
  - Memory
  - NDB
- the modules have certain advantages, but also disadvantages.
  - In the same database, it is possible to use different MSE modules simultaneously for defining tables - if there are no specific reasons for such a solution, it is better to build the entire database on the same MSE module.
- different modules do not communicate directly with each other, but do so through a higher layer that contains a parser, optimizer, and other modules for analyzing and executing SQL queries.
  - communication is carried out through the Storage API system.

## Comparative Overview of Characteristics

![Comparison of several well-known MSE modules](https://www.supportsages.com/sscontent/uploads/2010/08/sss.png)

### MyISAM

#### Advanced Features

- full-text indexes
- data compression
- support for spatially oriented data types

#### Disadvantages

- lack of transaction support
- the smallest scope of data locking
- weak data recoverability

#### Usage in Solutions

- read-only oriented solutions - when most operations involve only reading or searching existing data.

### InnoDB

#### Advanced Features

- most advanced features expected from relational databases are built-in.
- support for using transactions
- resource locking at the row level
- improved resistance to potential system crashes

### Memory

#### Advanced Features and Limitations

- all data accessed is located in the computer's RAM.
- due to the orientation towards using the computer's RAM, MSE brings several significant limitations:
  - data is lost after the server is restarted.
  - limited capacity of RAM.
  - some standard data types are not supported - tables with such data cannot be implemented directly.

### NDB

- intended for use in distributed environments with a larger number of servers.
- like InnoDB, it supports many advanced features implied in relational databases.

### Archive

- MSE modules based on Archive technology are intended for storing and subsequent access to very large amounts of non-indexed data (so-called data archives).
  - to reduce disk space usage, data is automatically compressed using the zlib library during storage.

### Blackhole

- the MSE module allows the preparation of tables into which your own solution can write data, but such data is not permanently stored anywhere.
  - due to this feature, Blackhole can be applicable in various (automatic) forms of testing a project where it doesn't make sense to permanently store temporary test data.

### CSV

- as the name suggests - data is stored in the form of text tables in CSV format (Comma-Separated Values).
  - text-oriented data, as encountered in practice during ETL (Extract, Transform, and Load) projects.
    - MySQL database and ETL projects.
