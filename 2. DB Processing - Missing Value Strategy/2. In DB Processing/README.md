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

    ![Join Table on SERIALNO Column](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/1%20Join%20Table%20on%20SERIALNO.png)

    - In the first question we were asked to Join those 2 table with SERIALNO Column as the join key. We can use DB Joiner to do that, we just need to define the Column for the Join Key.
    - After the table is Joined we need to read the data of the result as an table too. We can use DB Reader to read the data.

2. **Filter 05111740000184_ss13pme Table that COW Is NULL**

    ![Filter Table Cow is Null](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/2.%20Filter%20Table%20COW%20is%20Null.png)

    - The second question is asked us to get all rows in 05111740000184_ss13pme Table which is Null. We can use DB Row Filter, so we just need to assign the filter.
    - After we filter the data, we need to read the data of those result. We can use DB Reader to read the data as Table.

3. **Filter 05111740000184_ss13pme Table that COW Is Not NULL**

    ![Filter Table Cow is Not Null](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/3.%20Filter%20Table%20COW%20is%20Not%20Null.png)

    - The third question is similar to second question, but in this case we asked to get all rows that is Not NULL. We also can use DB Row Filter, , so we just need to assign the filter.
    - After we filter the data, we need to read the data of those result. We can use DB Reader to read the data as Table.

4. **Do Group By SEX Column and Average Agregate Function on AGEP Column**

    ![Group Bu SEX and AVG on AGEP](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/4.%20AVG%20of%20AGEP%20for%20SEX%20Groups.png)

    - The fourth question is asked us to to do Avarage Agregate Function on AGEP Column for All SEX Groups. So firstly we need to Grouping the data by SEX Column by do ```Group By``` Function. After the data Grouped we can do the Average Agregate Function on AGEP Column. All these operation can be don by implementing DB Group By, and we just need to define which column to be the Group By Key and we Also need to Define What Agregate Function that we want to Apply.
    - After that we need to read the data. We can use DB Reader to read the data as Table.

5 **Sort Data by Desc AGEP and Extract TOP 10**

    ![Group Bu SEX and AVG on AGEP](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/5.%20Sort%20by%20Desc%20AGEP%20and%20Extracy%20Top%2010.png)