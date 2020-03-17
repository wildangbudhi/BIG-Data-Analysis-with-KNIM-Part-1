# 2. Missing Value Strategy - In DB Processing

## Question
![Question](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/Question.png)

## Solution
Here the solution for this question that we provide 

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/Full%20Solution.png)

0. **Read Data in DB and Filter**

    ![Read Data In DB and Filter](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/0.%20Read%20Data%20and%20Filter.png)

    - Before we do all the processing we need to read the data which stored in Database. In this case the data is Stored in SQLite Database, so we can use SQLite Connector to make connection and the instance.
    - Then we need to select particular table that we need to process the data. In this case we need to process 2 table, 05111740000184_ss13hme and 05111740000184_ss13pme. We can use 2 DB Selector to select that 2 table.
    - After we select the table, we are asked to remove all PUMA* and PWGTP* Column in 05111740000184_ss13hme Table. We can use DB Colum Filter to remove those all column that we asked to.

1. **Do Inner Join in Both Table on SERIALNO Column**
