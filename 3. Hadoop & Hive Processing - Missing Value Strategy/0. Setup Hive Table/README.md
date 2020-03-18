# 0. Missing Value Strategy - Setup Hive Table

## Question
![Question](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/0.%20Setup%20Hive%20Table/Screenshoot/Question.png)


## Solution
Here the solution for this question that we provide

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/0.%20Setup%20Hive%20Table/Screenshoot/Full%20Solution.png)

1. **Create Temp Directory and Compitable Path For HDFS**

    ![Create Temp Dir & Compatible Path](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/0.%20Setup%20Hive%20Table/Screenshoot/1.%20Create%20Temp%20Dir%20%26%20Compatible%20Path.png)

    - We need to make a Temporary Directory for the HDFS so we can remove it and not permanently. We can use ```Create Temp Dir``` to make a Temporary Directory.
    - Then we need to Manipulate The String Path to be a Path that Compatible with HDFS. We can use ```String Manipulation (Variable)```

2. ** Create Local Big Data Environment**

    ![Create Local Big Data Env](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/0.%20Setup%20Hive%20Table/Screenshoot/2.%20Create%20Local%20Big%20Data%20Env.png)

    Now we need to create the Local Big Data Environtment to Store and Processing Massive Data. We can use ```Create Local Big Data Environtment```, so we don't need to setup Hadoop, HDFS, and Hive manualy we only need to choose the settings of this node.

3. **Load Table**

    ![Load Table](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/0.%20Setup%20Hive%20Table/Screenshoot/3.%20Load%20Table.png)

    - We need to Read the Table. In this case we need to read 2 table, 05111740000184_ss13pme and 05111740000184_ss13hme. We can use 2 ```Table Reader``` to read those 2 table.
    - After that we need to create Table in Hive to Load those 2 table. We can use 2 ```DB Table Creator```, one for 05111740000184_ss13pme and other for 05111740000184_ss13hme.
    - After we create the table in Hive now we can Load the table into HDFS from Hive using ```DB Loader```.