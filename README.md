golang-db-sql-benchmark
====================

A collection of benchmarks for popular Go database/SQL utilities

# Libraries under test

*  [database/sql](https://golang.org/pkg/database/sql/) + [go-sql-driver/mysql](https://github.com/go-sql-driver/mysql)
*  [gocraft/dbr](https://github.com/gocraft/dbr)
*  [Gorp](https://github.com/coopernurse/gorp)
*  [Sqlx](https://github.com/jmoiron/sqlx)
*  [SQLBoiler](https://github.com/vattle/sqlboiler)
*  [Squirrel](https://github.com/lann/squirrel)

# database/sql SQL Execution Benchmarks:

* **BenchmarkPreparedStatementsNone** - Runs simple queries without query arguments, so database/sql doesn't need to create a prepared statement
* **BenchmarkPreparedStatementsThrowaway** - Runs queries with query arguments. database/sql must create and then throwaway a prepared statement each time
* **BenchmarkPreparedStatementsSingle** - Runs queries with query arguments, but creates and reuses the a single prepared statement


# Dbr/Sqlx/Gorp/SQLBoiler SQL Execution Benchmarks:
Each library under test has the same set of benchmarks, just replace `Dbr` in the examples with `Sqlx` or `Gorp`.
Each one is run with varying number of rows, N.

* **BenchmarkDbrSelectIntsN** - Select rows of integers into []int64's
* **BenchmarkDbrSelectAllN** - Select rows into structs using no query arguments
* **BenchmarkDbrSelectAllWithArgsN** - Select rows into structs using query arguments

# Dbr/Squrrel SQL Building Benchamrks
Test building (but not executing) various SQL statements

* **BenchmarkBuilderDbrSimple** - Simple SQL query with dbr
* **BenchmarkBuilderDbrComplex** - Complex SQL query with dbr
* **BenchmarkBuilderSquirrelSimple** - Simple SQL query with squirrel
* **BenchmarkBuilderSquirrelComplex** - Complex SQL query with squirrel

# Bench

```
BenchmarkPreparedStatementsNone-4            	   10000	    197758 ns/op	     552 B/op	      19 allocs/op
BenchmarkPreparedStatementsThrowaway-4       	    5000	    299326 ns/op	     737 B/op	      27 allocs/op
BenchmarkPreparedStatementsSingle-4          	   10000	    167421 ns/op	     512 B/op	      21 allocs/op

BenchmarkDbrSelectInts1-4                    	   10000	    158974 ns/op	    1480 B/op	      28 allocs/op
BenchmarkDbrSelectInts100-4                  	   10000	    158488 ns/op	    1592 B/op	      34 allocs/op
BenchmarkDbrSelectInts1000-4                 	   10000	    171229 ns/op	    1592 B/op	      34 allocs/op
BenchmarkDbrSelectInts10000-4                	   10000	    179411 ns/op	    1592 B/op	      34 allocs/op
BenchmarkDbrSelectAll1-4                     	    5000	    211225 ns/op	    2945 B/op	      46 allocs/op
BenchmarkDbrSelectAll100-4                   	    5000	    227243 ns/op	    4057 B/op	      70 allocs/op
BenchmarkDbrSelectAll1000-4                  	    5000	    223814 ns/op	    4057 B/op	      70 allocs/op
BenchmarkDbrSelectAll10000-4                 	    5000	    227796 ns/op	    4057 B/op	      70 allocs/op
BenchmarkDbrSelectAllWithArgs1-4             	    5000	    259579 ns/op	    3393 B/op	      58 allocs/op
BenchmarkDbrSelectAllWithArgs100-4           	    5000	    240712 ns/op	    4513 B/op	      82 allocs/op
BenchmarkDbrSelectAllWithArgs1000-4          	    5000	    237579 ns/op	    4513 B/op	      82 allocs/op
BenchmarkDbrSelectAllWithArgs10000-4         	    5000	    252805 ns/op	    4513 B/op	      82 allocs/op

BenchmarkSqlxSelectInts1-4                   	    5000	    391918 ns/op	     576 B/op	      24 allocs/op
BenchmarkSqlxSelectInts100-4                 	    3000	    391969 ns/op	     664 B/op	      30 allocs/op
BenchmarkSqlxSelectInts1000-4                	    3000	    467722 ns/op	     664 B/op	      30 allocs/op
BenchmarkSqlxSelectInts10000-4               	    3000	    440100 ns/op	     664 B/op	      30 allocs/op
BenchmarkSqlxSelectAll1-4                    	    5000	    278827 ns/op	     888 B/op	      24 allocs/op
BenchmarkSqlxSelectAll100-4                  	    5000	    316276 ns/op	    1096 B/op	      33 allocs/op
BenchmarkSqlxSelectAll1000-4                 	    5000	    293700 ns/op	    1096 B/op	      33 allocs/op
BenchmarkSqlxSelectAll10000-4                	    5000	    283353 ns/op	    1096 B/op	      33 allocs/op
BenchmarkSqlxSelectAllWithArgs1-4            	    3000	    503494 ns/op	    1192 B/op	      35 allocs/op
BenchmarkSqlxSelectAllWithArgs100-4          	    2000	    519654 ns/op	    1368 B/op	      43 allocs/op
BenchmarkSqlxSelectAllWithArgs1000-4         	    3000	    576125 ns/op	    1368 B/op	      43 allocs/op
BenchmarkSqlxSelectAllWithArgs10000-4        	    2000	    566950 ns/op	    1368 B/op	      43 allocs/op

BenchmarkGorpSelectInts1-4                   	    2000	    536336 ns/op	     387 B/op	      17 allocs/op
BenchmarkGorpSelectAll1-4                    	    5000	    399204 ns/op	    1786 B/op	      68 allocs/op
BenchmarkGorpSelectAll100-4                  	    3000	    388126 ns/op	    2043 B/op	      78 allocs/op
BenchmarkGorpSelectAll1000-4                 	    3000	    395568 ns/op	    2043 B/op	      78 allocs/op
BenchmarkGorpSelectAll10000-4                	    5000	    381177 ns/op	    2042 B/op	      78 allocs/op
BenchmarkGorpSelectAllWithArgs1-4            	    2000	    670428 ns/op	    2092 B/op	      79 allocs/op
BenchmarkGorpSelectAllWithArgs100-4          	    2000	    725952 ns/op	    2316 B/op	      88 allocs/op
BenchmarkGorpSelectAllWithArgs1000-4         	    2000	    724523 ns/op	    2316 B/op	      88 allocs/op
BenchmarkGorpSelectAllWithArgs10000-4        	    2000	    728395 ns/op	    2316 B/op	      88 allocs/op

BenchmarkSQLBoilerSelectInts1-4              	    5000	    238310 ns/op	     850 B/op	      21 allocs/op
BenchmarkSQLBoilerSelectInts100-4            	    5000	    252447 ns/op	     850 B/op	      21 allocs/op
BenchmarkSQLBoilerSelectInts1000-4           	    5000	    240472 ns/op	     850 B/op	      21 allocs/op
BenchmarkSQLBoilerSelectInts10000-4          	    5000	    267841 ns/op	     850 B/op	      21 allocs/op
BenchmarkSQLBoilerSelectAll1-4               	    5000	    303593 ns/op	    1450 B/op	      35 allocs/op
BenchmarkSQLBoilerSelectAll100-4             	    5000	    300622 ns/op	    1786 B/op	      47 allocs/op
BenchmarkSQLBoilerSelectAll1000-4            	    5000	    289008 ns/op	    1786 B/op	      47 allocs/op
BenchmarkSQLBoilerSelectAll10000-4           	    5000	    303211 ns/op	    1786 B/op	      47 allocs/op
BenchmarkSQLBoilerSelectAllWithArgs1-4       	    2000	    694815 ns/op	    2302 B/op	      65 allocs/op
BenchmarkSQLBoilerSelectAllWithArgs100-4     	    2000	    679760 ns/op	    2574 B/op	      77 allocs/op
BenchmarkSQLBoilerSelectAllWithArgs1000-4    	    2000	    663936 ns/op	    2590 B/op	      77 allocs/op
BenchmarkSQLBoilerSelectAllWithArgs10000-4   	    2000	    682127 ns/op	    2590 B/op	      77 allocs/op

BenchmarkDbrBuilderSimple-4                  	 1000000	      1532 ns/op	     984 B/op	      17 allocs/op
BenchmarkDbrBuilderComplex-4                 	  200000	      6972 ns/op	    2824 B/op	      64 allocs/op

BenchmarkSquirrelBuilderSimple-4             	  200000	      6694 ns/op	    2552 B/op	      51 allocs/op
BenchmarkSquirrelBuilderComplex-4            	   50000	     34412 ns/op	   11539 B/op	     276 allocs/op
```
## date

Jan 18, 2017

## env

go version: go1.7.4 darwin/amd64  
MacBook Pro, 2.7 GHz Intel Core i5, 8 GB 1867 MHz DDR3