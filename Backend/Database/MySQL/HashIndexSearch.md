# MySQL Hash-index for Searching

- different types of MySQL Storage Engine system modules support various types of indexes according to their internal structure.

## Properties

- instead of storing the original values from the tables (or parts of them) as index values, specially calculated (hash) values are stored for each row of the table.
- since these calculated values occupy relatively small amounts of memory, they are an ideal type of index for the `Memory Storage Engine` module, where hash indexes are the default type of index.
- with very large datasets, there is a possibility that two different pieces of data will receive the same hash value.
- because they do not contain the original data values but calculated values, these indexes cannot be used:

  - as covering indexes (indexes from which the desired data is directly retrieved without needing to access the original table row)
  - to speed up data sorting
  - for searching by partial matching of the desired values or for searching for a range of values in the data

- in other types of MySQL Storage Engine system modules, hash indexes can be simulated using the MySQL `CRC32` function and `B-Tree` indexes.

  - the `CRC32` function enables the use of simulated hash indexes for optimized searching of certain types of data in systems that do not support them—such as InnoDB or MyISAM.

- data that is poorly suited for indexing in terms of index size and performance when using the B-Tree type of index (the default type of index for InnoDB and MyISAM) typically has values that often repeat at the beginning, with differences between data only appearing at the very end of the values.

  - a typical example of such data is web addresses—where the initial part of the address is repeated in a large number of cases, and the differences between data appear only at the end of the specific website or page name.

- using B-Tree indexes for such data results in very large space consumption (because the entire web address must be indexed, which is quite long) and somewhat slower searching compared to using simulated hash indexes for the same data.

## Example

- below is an example of using simulated hash indexes in practice. Suppose the original value of a web page to be indexed is:

```md
http://www.index.hr/vijesti/clanak/infografika-koja-je-razlika-izmedju-hidrogenske-i-obicne-nuklearne-bombe/992309.aspx
```

- the length of the previous string is 119 characters.

  - if the MySQL CRC32 function is applied to the same value, the result is 1,082,117,441 with a total length of 10 characters (almost 12 times smaller). Since the result of the function execution is actually a number, the obtained result can be stored in the database as an INT data type, further reducing the amount of occupied space and speeding up operations on the data

- if a B-Tree index is created on the table column with the CRC value instead of the column with the original values, the result is a simulated hash index that takes up less space and offers faster search speeds.

  - this change requires modifying the original SQL statement for finding the table row from the example:

    ```sql
    select * from testtable where webpage = 'http://www.index.hr/vijesti/clanak/infografika-koja-je-razlika-izmedju-hidrogenske-i-obicne-nuklearne-bombe/992309.aspx'
    ```

  - to a slightly different form:

    ```sql
    SET @hash = crc32('http://www.index.hr/vijesti/clanak/infografika-koja-je-razlika-izmedju-hidrogenske-i-obicne-nuklearne-bombe/992309.aspx');
    select * from testtable where hash = @hash;
    ```

  - the problem with this first version of the modified SELECT statement is one of the characteristics of hash indexes mentioned in the introductory part of the text. With a sufficiently large dataset, there is a possibility that the CRC32 function will return the same value for two completely different pieces of data, ultimately resulting in incorrect operation of the SELECT statement. Therefore, the previous statement should be modified to the following form:

    ```sql
    SET @webpage = 'http://www.index.hr/vijesti/clanak/infografika-koja-je-razlika-izmedju-hidrogenske-i-obicne-nuklearne-bombe/992309.aspx';
    SET @hash = crc32(@webpage);
    select * from testtable where hash = @hash and webpage = @webpage;
    ```

  - the built-in query optimizer will quickly find the desired table row (or rows) based on the hash value, and the second part of the query (after AND) ensures the return of the exact desired data in any returned result set

  - the built-in query optimizer will quickly find the desired table row (or rows) based on the hash value, and the second part of the query (after AND) ensures the return of the exact desired data in any returned result set

    - the ideal solution to this problem is to add two triggers to the same table. The first one automatically calculates the hash value when a new web address is added, and the second one does so when it is modified

      ```sql
      DELIMITER //

      CREATE TRIGGER urlsearch_insert BEFORE INSERT ON urlsearch FOR EACH ROW BEGIN

          SET NEW.urlcrc=crc32(NEW.url);

      END;

      //

      CREATE TRIGGER urlsearch_update BEFORE UPDATE ON urlsearch FOR EACH ROW BEGIN

          SET NEW.urlcrc=crc32(NEW.url);

      END;

      //

      DELIMITER ;
      ```

- **a similar approach to using simulated hash indexes can be applied to optimize the search of any type of text-oriented data where there is a large amount of data with repeating initial parts**
