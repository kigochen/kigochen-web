---
title: "SQL Basic"
date: 2019-02-20T23:03:28+08:00
categories:
- Notes
- SQL
tags:
- SQL
thumbnailImagePosition: left
thumbnailImage: //media.licdn.com/media/AAEAAQAAAAAAAAB1AAAAJDg1Y2YyNTVjLTJiMjgtNDc3ZS1hYmRjLTZkOTMzZGMxNDRiNw.jpg =700x200
---

## This are some notes for basic SQL. 

<!--more-->

## DBMS
![](https://i.imgur.com/nJble7Z.png)
- DBMS: Oracle, MySQL, PostgresSQL, Ms SQL server...etc.

- SQL: 用以操作 DBMS 的系統的語言 (**Structured Query Language**)

    - DDL(Data Definition Language)
        - 用來定義資料庫/表格概念和實體階層的內容與其存在關係，也就是描述資料庫中的資料，包括欄位、型態和資料結構等等。

        - CREATE, DROP, ALTER

    - DML(Data Manipulation Language):

        - 允許使用者存取或是處理資料庫中的資料

        - **SELECT**, INSERT, DELETE, UPDATE
    
    
## DML Syntax:tada:

### SELECT - extracts data from a database

* SELECT

> select the column names of the table you want from table
```sql=
SELECT table_name, owner FROM all_tables;
```
```sql=+
SELECT * FROM all_tables;
```
* SELECT DISTINCT

> used to return only distinct result
```sql=
SELECT cf_value_11 FROM SPACE.T_CHANNEL_DEF
;

SELECT DISTINCT cf_value_11 FROM SPACE.T_CHANNEL_DEF
;
```
```sql=+
SELECT COUNT(DISTINCT cf_value_11) FROM SPACE.T_CHANNEL_DEF
;
```
* WHERE

> Used to extract only those records that fulfill a specified condition
```sql=
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
```sql=+
SELECT DISTINCT CH_ID, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 = 'PHOTO'
;
SELECT CH_ID, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE CH_ID = '142'
;
SELECT * FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 = 'PHOTO'
AND (CH_ID=142 OR CH_ID=143)
;
SELECT DISTINCT cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE NOT cf_value_11 = 'PHOTO'
;
SELECT DISTINCT cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
;
```



| Operator | Description| 
| -------- | -------- | -------- |
| =	| Equal|
| <> |	Not equal. Note: In some versions of SQL this operator may be written as **!=**|
| > |	Greater than|
| < |	Less than|
| >=|	Greater than or equal|
| <=|	Less than or equal|
| BETWEEN|	Between an inclusive range|
| LIKE|	Search for a pattern|
| IN|	To specify multiple possible values for a column|


* ORDER BY

> The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

```sql=
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```
```sql=
SELECT * FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
ORDER BY ch_id
;

SELECT * FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
ORDER BY ch_id DESC, cf_value_11 ASC
;
```

* SELECT LIMIT

> used to specify the number of records to return.

ANSI
```sql=
SELECT * FROM Customers
LIMIT 3
;
```
ORACLE
```sql=
SELECT * FROM SPACE.SAMPLES_RAW_WAFER
WHERE ROWNUM <= 10
;
```

* FUNCTIONS

    - [oracle functions](https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions001.htm)

```sql=
SELECT AVG(Price)
FROM Products;
```

* LIKE

> Used in a WHERE clause to search for a specified pattern in a column

    % : The percent sign represents zero, one, or multiple characters
    _ : The underscore represents a single character

```sql=
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
AND CH_NAME LIKE '5030%'
ORDER BY ch_id DESC, cf_value_11 ASC
;
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
AND CH_NAME LIKE '5030-_2%'
ORDER BY ch_id DESC, cf_value_11 ASC
;
```

* IN

> Allows you to specify multiple values in a WHERE clause

```sql=
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
AND ch_id IN (5566,9527,9487,8763)
;
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE ch_id IN (
SELECT DISTINCT ch_id FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 = 'PHOTO')
;

-- pair condition in
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE (ch_id, ch_name) IN (
SELECT DISTINCT ch_id, ch_name FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 = 'PHOTO')
;

-- remind that limit of condition number is 1000
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
AND ch_id IN (1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,136,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,152,153,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,169,170,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,186,187,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,203,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,221,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,238,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,254,255,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,271,272,273,274,275,276,277,278,279,280,281,282,283,284,285,286,287,288,289,290,291,292,293,294,295,296,297,298,299,300,301,302,303,304,305,306,307,308,309,310,311,312,313,314,315,316,317,318,319,320,321,322,323,324,325,326,327,328,329,330,331,332,333,334,335,336,337,338,339,340,341,342,343,344,345,346,347,348,349,350,351,352,353,354,355,356,357,358,359,360,361,362,363,364,365,366,367,368,369,370,371,372,373,374,375,376,377,378,379,380,381,382,383,384,385,386,387,388,389,390,391,392,393,394,395,396,397,398,399,400,401,402,403,404,405,406,407,408,409,410,411,412,413,414,415,416,417,418,419,420,421,422,423,424,425,426,427,428,429,430,431,432,433,434,435,436,437,438,439,440,441,442,443,444,445,446,447,448,449,450,451,452,453,454,455,456,457,458,459,460,461,462,463,464,465,466,467,468,469,470,471,472,473,474,475,476,477,478,479,480,481,482,483,484,485,486,487,488,489,490,491,492,493,494,495,496,497,498,499,500,501,502,503,504,505,506,507,508,509,510,511,512,513,514,515,516,517,518,519,520,521,522,523,524,525,526,527,528,529,530,531,532,533,534,535,536,537,538,539,540,541,542,543,544,545,546,547,548,549,550,551,552,553,554,555,556,557,558,559,560,561,562,563,564,565,566,567,568,569,570,571,572,573,574,575,576,577,578,579,580,581,582,583,584,585,586,587,588,589,590,591,592,593,594,595,596,597,598,599,600,601,602,603,604,605,606,607,608,609,610,611,612,613,614,615,616,617,618,619,620,621,622,623,624,625,626,627,628,629,630,631,632,633,634,635,636,637,638,639,640,641,642,643,644,645,646,647,648,649,650,651,652,653,654,655,656,657,658,659,660,661,662,663,664,665,666,667,668,669,670,671,672,673,674,675,676,677,678,679,680,681,682,683,684,685,686,687,688,689,690,691,692,693,694,695,696,697,698,699,700,701,702,703,704,705,706,707,708,709,710,711,712,713,714,715,716,717,718,719,720,721,722,723,724,725,726,727,728,729,730,731,732,733,734,735,736,737,738,739,740,741,742,743,744,745,746,747,748,749,750,751,752,753,754,755,756,757,758,759,760,761,762,763,764,765,766,767,768,769,770,771,772,773,774,775,776,777,778,779,780,781,782,783,784,785,786,787,788,789,790,791,792,793,794,795,796,797,798,799,800,801,802,803,804,805,806,807,808,809,810,811,812,813,814,815,816,817,818,819,820,821,822,823,824,825,826,827,828,829,830,831,832,833,834,835,836,837,838,839,840,841,842,843,844,845,846,847,848,849,850,851,852,853,854,855,856,857,858,859,860,861,862,863,864,865,866,867,868,869,870,871,872,873,874,875,876,877,878,879,880,881,882,883,884,885,886,887,888,889,890,891,892,893,894,895,896,897,898,899,900,901,902,903,904,905,906,907,908,909,910,911,912,913,914,915,916,917,918,919,920,921,922,923,924,925,926,927,928,929,930,931,932,933,934,935,936,937,938,939,940,941,942,943,944,945,946,947,948,949,950,951,952,953,954,955,956,957,958,959,960,961,962,963,964,965,966,967,968,969,970,971,972,973,974,975,976,977,978,979,980,981,982,983,984,985,986,987,988,989,990,991,992,993,994,995,996,997,998,999,1000,1001,1002,1003,1004,1005,1006,1007,1008,1009,1010,1011,1012,1013,1014,1015,1016,1017,1018,1019,1020,1021,1022,1023,1024,1025)
;

-- use subquery as condition if you got plenty of it
SELECT ch_id, ch_name, cf_value_11 AS AREA FROM SPACE.T_CHANNEL_DEF
WHERE cf_value_11 IS NOT NULL
AND ch_id IN (SELECT Rownum r FROM dual
Connect By Rownum <= 1025)
;
```
 * ALIAS
 > Renames columns
```sql=
SELECT CONCAT(CONCAT(TO_CHAR(ch_id),'_'),ch_name) AS id_name
FROM SPACE.T_CHANNEL_DEF
;
 ```
* JOIN
    * **(INNER) JOIN**: Returns records that have matching values in both tables
    * **LEFT (OUTER) JOIN**: Return all records from the left table, and the matched records from the right table
    * **RIGHT (OUTER) JOIN**: Return all records from the right table, and the matched records from the left table
    * **FULL (OUTER) JOIN**: Return all records when there is a match in either left or right table
> Used to combine rows from two or more tables, based on a related column between them.

![](https://i.imgur.com/nEp6gAK.png)

```sql=
SELECT
      SC.CH_ID as CHANNEL_ID,
      SC.CKC_ID,
      SA.SAMPLE_ID,
	  SA.LOT_ID,
      SA.WAFER_ID,
      SRW.RV_SEQ_NUM as SITE_NUMBER,
      SRW.RAW_VALUE,
      SA.SAMPLE_DATE,
      SA.DESIGN_ID,
      TCD.CH_NAME as CHANNEL_NAME,
      SA.PROCESS_STEP_NAME,
      SA.PARAMETER_NAME,
      SA.PROCESS_TOOL_NAME,
      ST.TAG_ID,
      SA.WAFER_SCRIBE,
      TCD.CF_VALUE_11 as AREA
    FROM SPACE.SAMPLES_RAW_WAFER SRW
      INNER JOIN SPACE.SAMPLES_ALL_V SA
        ON SRW.SAMPLE_DATE = SA.SAMPLE_DATE
           AND SRW.SAMPLE_ID = SA.SAMPLE_ID
      INNER JOIN SPACE.SAMPLES_CALC SC
        ON SRW.SAMPLE_DATE = SC.SAMPLE_DATE
           AND SRW.SAMPLE_ID = SC.SAMPLE_ID
      INNER JOIN SPACE.T_CHANNEL_DEF TCD
        ON SC.CH_ID = TCD.CH_ID
      LEFT JOIN SPACE.SAMPLES_TAG ST
        ON SA.SAMPLE_ID = ST.SAMPLE_ID
    WHERE SC.CKC_ID = 0
          AND TCD.CH_ID IN (658)
          AND NOT REGEXP_LIKE(SA.SWR_AT_STEP, '^.+(SWR|TARGET|ENGINEERING)') --exclude SWR/ENG
          AND SA.SPC_FLAG_EXTERN = 'N'
          AND SA.SPC_FLAG_INTERN = 'N'
          AND ST.TAG_ID IS NULL
          AND SA.SAMPLE_DATE > TO_DATE('03/01/2017 07:00:00 PM', 'MM/DD/YYYY HH:MI:SS AM')
          AND SA.SAMPLE_DATE < TO_DATE('03/30/2017 07:00:00 PM', 'MM/DD/YYYY HH:MI:SS AM');

```
* UNION Operator
    * Each SELECT statement within UNION must have the same number of columns
    * The columns must also have similar data types
    * The columns in each SELECT statement must also be in the same order
> Used to combine the result-set of two or more SELECT statements.

```sql=
-- list all (duplicate values also)
SELECT DISTINCT cf_value_11 FROM SPACE.T_CHANNEL_DEF
UNION ALL 
SELECT DISTINCT cf_value_11 FROM SPACE.T_CHANNEL_DEF
;


-- only distinct values
SELECT DISTINCT cf_value_11 FROM SPACE.T_CHANNEL_DEF
UNION 
SELECT DISTINCT cf_value_11 FROM SPACE.T_CHANNEL_DEF
;
```

* GROUP BY
> Used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group result by some columns

```sql=
SELECT COUNT(*), cf_value_11 AS AREA
FROM SPACE.T_CHANNEL_DEF
GROUP BY cf_value_11
;
```

* HAVING
```sql=
SELECT COUNT(*), cf_value_11 AS AREA
FROM SPACE.T_CHANNEL_DEF
GROUP BY cf_value_11
HAVING COUNT(*) > 5566
ORDER BY COUNT(*)
;
```

* NULL Functions
> User COALESCE instead of NVL (for performance)
```sql=
SELECT COUNT(*), COALESCE(cf_value_11, 'EMPTY_AREA') AS AREA
FROM SPACE.T_CHANNEL_DEF
GROUP BY cf_value_11
HAVING COUNT(*) > 5566
ORDER BY COUNT(*)
;
```


### UPDATE - updates data in a database

### DELETE - deletes data from a database

### INSERT INTO - inserts new data into a database



## DML Syntax

### CREATE DATABASE - creates a new database

### ALTER DATABASE - modifies a database

### CREATE TABLE - creates a new table

### ALTER TABLE - modifies a table

### DROP TABLE - deletes a table

### CREATE INDEX - creates an index (search key)

### DROP INDEX - deletes an index




# Connect DB Setting

### R Connect server and Get data

* Oracle

```R=
library(RODBC)
con <- odbcConnect("DD1", uid="rquser", pwd="rquser", rows_at_time = 500)
d <- sqlQuery(con, "select * from TEST_TABLE")
close(con)
```

* Teradata

```R=
options(java.parameters = "-Xmx8048m")
options(java.home="********") #set path for loading jvm.dll
library(rJava)
library(RJDBC)
drv=JDBC("com.teradata.jdbc.TeraDriver","c:\\teradataJDBCdRIVER\\terajdbc4.jar;c:\\teradataJDBCdRIVER\\tdgssconfig.jar")

conn <- dbConnect(drv, "jdbc:teradata://servername/database=dbname,LOGMECH=LDAP", "login name", "password")
querystring <- paste0("SELECT * from testDB")

results <- dbSendQuery(conn, querystring)
dataset <- dbFetch(results)
dbDisconnect(conn)
```
