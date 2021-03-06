# 1. Missing Value Strategy - Hive Modelling

## Question
![Question](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/1.%20Hive%20Modelling/Screenshoot/Question.png)

## Solution
Here the solution for this question that we provide

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/1.%20Hive%20Modelling/Screenshoot/Full%20Solution.png)

1. **Big Data Environtment Connect and Filtering**

    ![BigData Env Connect and Filtering](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/1.%20Hive%20Modelling/Screenshoot/1.%20BigData%20Env%20Connect%20and%20Filtering.png)

    - We need to make a Local Big Data Environtment to Store and Process massive data. We can use ```Create Local Big Data Environtment``` so we don't need to setup Hadoop, HDFS, and Hive Manualy.
    - Then we need to select particular table, 05111740000184_ss13pme table. We can use ```DB Selector``` to select that table.
    - After we select the table, we are asked to remove all PUMA* and PWGTP* Column in 05111740000184_ss13hme Table. We can use ```DB Colum Filter``` to remove those all column that we asked to.

2. **Filter Data which COW Column is NULL and Not NULL**

    ![Filter Data COW is NULL and Not NULL](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/1.%20Hive%20Modelling/Screenshoot/2.%20Filter%20Data%20COW%20is%20Null%20and%20Not%20Null.png)

    - In this first question we asked to Split data into 2, which COW Column is NULL and COW Column is Not NULL. We can use 2 ```DB Row Filter```, one for filtering COW Column is NULL and other for filtering COW Column is Not NULL.
    - For the case that COW Column is NULL we need to Remove COW Column because the data is NULL, it can be bad effecting to future processing. We can use ```DB Column Filter``` to remove COW Column.
    - After that we need to read both data. We can use 2 ```DB Reader``` to read those 2 data.

3. **Train Decision Tree using Data which COW Column is Not NULL**

    ![Train COW is Not NULL](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/1.%20Hive%20Modelling/Screenshoot/3%20Train%20Cow%20is%20Not%20Null.png)

    - To train the data we need to convert the COW Column from Number to be String. We can use ```Number to String``` so we only need to spesify which column that we want to transform from Number to String.
    - After COW Column transformed we can train the model using ```Decision Tree Learner``` and it will output the model.

4. **Predict Data which COW Column is NULL in The Model**

    ![Predict Model with Cow is Null](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/3.%20Hadoop%20%26%20Hive%20Processing%20-%20Missing%20Value%20Strategy/1.%20Hive%20Modelling/Screenshoot/4.%20Predict%20Model%20with%20Cow%20is%20Null.png)

    Now we can predict the data which COW Column is NULL using ```Decission Tree Predictor``` and it will output the prediction of the data.