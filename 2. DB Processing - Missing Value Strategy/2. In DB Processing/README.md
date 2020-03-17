# 2. Missing Value Strategy - In DB Processing

## Question
![Question](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/Question.png)

## Solution
Here the solution for this question that we provide 

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/Full%20Solution.png)

0. **Read Data in DB and Filter**

    ![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/2.%20In%20DB%20Processing/Screenshoot/Full%20Solution.png)

    - Before we do all the processing we need to read the data which stored in Database. In this case the data is Stored in SQLite Database, so we can use SQLite Connector to make connection and the instance.

1. **Do Inner Join in Both Table on SERIALNO Column**
