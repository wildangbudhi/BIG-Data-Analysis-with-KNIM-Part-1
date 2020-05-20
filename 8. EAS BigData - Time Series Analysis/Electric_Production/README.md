# EAS BigData - Time Series Analysis (Electric_Production)

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Full%20Solution.png)

## Business Undestanding

Given data of Electicity Production in Time Series form data. We were asked to Analyze the data to provide a point of view from the data. We were asked to Forcast incoming Production based on given data.

## Data Understanding

| Column Name |            Description            |
|:-----------:|:---------------------------------:|
|     DATE    | Meta Data of Time                 |
|  IPG2211A2N | Total Production at Spesific Date |

## Data Preperation

![Full Solution 1](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Data%20Preparation%201.png)

![Full Solution 2](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Data%20Preparation%202.png)

![Full Solution 2](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Data%20Preparation%203.png)

1. First we need to read the data from CSV file format. We can use ```File Reader``` Module.
2. Because the data is big, we need to store it in BigData Environment so we can store it and Calculate it faster. We can use ```Create Local Big Data Environtment``` Module.
3. Than we need to Load the Data into DB. We can use Custome Metanode ```Load Data```, that contains 2 Modules, ```DB Table Creator``` Module for Creating Hive Table in HDFS and ```DB Loader``` Module to load the Data into the Hive Table.
4. We want to do some calculation and transformation of the data faster, so we need to convert it from Table form to Spark Dataframes. We can use ```Hive to Spark``` Module.
5. Because it was Time Series data we need the data in Ascending Order by ```DATE``` Column. We can sort the data using ```Spark Sorter``` Module.
6. We want to crate Windows Width of the data with 40 Data Backward. We can use ```Spark SQL Query``` Module and use Windows Function to Get Data Before called ```LAG()```. The query shown bellow :
    ```sql
    SELECT   
        `DATE` as datetime,
        LAG(`IPG2211A2N`, 30) 
            OVER( 
                ORDER BY `DATE`
                ) as prev30,

        LAG(`IPG2211A2N`, 29) 
            OVER( 
                ORDER BY `DATE`
                ) as prev29,

        LAG(`IPG2211A2N`, 28) 
            OVER( 
                ORDER BY `DATE`
                ) as prev28,

        LAG(`IPG2211A2N`, 27) 
            OVER( 
                ORDER BY `DATE`
                ) as prev27,

        LAG(`IPG2211A2N`, 26) 
            OVER( 
                ORDER BY `DATE`
                ) as prev26,

        LAG(`IPG2211A2N`, 25) 
            OVER( 
                ORDER BY `DATE`
                ) as prev25,

        LAG(`IPG2211A2N`, 24) 
            OVER( 
                ORDER BY `DATE`
                ) as prev24,

        LAG(`IPG2211A2N`, 23) 
            OVER( 
                ORDER BY `DATE`
                ) as prev23,

        LAG(`IPG2211A2N`, 22) 
            OVER( 
                ORDER BY `DATE`
                ) as prev22,

        LAG(`IPG2211A2N`, 21) 
            OVER( 
                ORDER BY `DATE`
                ) as prev21,

        LAG(`IPG2211A2N`, 20) 
            OVER( 
                ORDER BY `DATE`
                ) as prev20,

        LAG(`IPG2211A2N`, 19) 
            OVER( 
                ORDER BY `DATE`
                ) as prev19,

        LAG(`IPG2211A2N`, 18) 
            OVER( 
                ORDER BY `DATE`
                ) as prev18,

        LAG(`IPG2211A2N`, 17) 
            OVER( 
                ORDER BY `DATE`
                ) as prev17,

        LAG(`IPG2211A2N`, 16) 
            OVER( 
                ORDER BY `DATE`
                ) as prev16,

        LAG(`IPG2211A2N`, 15) 
            OVER( 
                ORDER BY `DATE`
                ) as prev15,

        LAG(`IPG2211A2N`, 14) 
            OVER( 
                ORDER BY `DATE`
                ) as prev14,

        LAG(`IPG2211A2N`, 13) 
            OVER( 
                ORDER BY `DATE`
                ) as prev13,

        LAG(`IPG2211A2N`, 12) 
            OVER( 
                ORDER BY `DATE`
                ) as prev12,

        LAG(`IPG2211A2N`, 11) 
            OVER( 
                ORDER BY `DATE`
                ) as prev11,

        LAG(`IPG2211A2N`, 10) 
            OVER( 
                ORDER BY `DATE`
                ) as prev10,

        LAG(`IPG2211A2N`, 9) 
            OVER( 
                ORDER BY `DATE`
                ) as prev9,

        LAG(`IPG2211A2N`, 8) 
            OVER( 
                ORDER BY `DATE`
                ) as prev8,

        LAG(`IPG2211A2N`, 7) 
            OVER( 
                ORDER BY `DATE`
                ) as prev7,

        LAG(`IPG2211A2N`, 6) 
            OVER( 
                ORDER BY `DATE`
                ) as prev6,

        LAG(`IPG2211A2N`, 5) 
            OVER( 
                ORDER BY `DATE`
                ) as prev5,

        LAG(`IPG2211A2N`, 4) 
            OVER( 
                ORDER BY `DATE`
                ) as prev4,

        LAG(`IPG2211A2N`, 3) 
            OVER( 
                ORDER BY `DATE`
                ) as prev3,

        LAG(`IPG2211A2N`, 2) 
            OVER( 
                ORDER BY `DATE`
                ) as prev2,

        LAG(`IPG2211A2N`, 1) 
            OVER( 
                ORDER BY `DATE`
                ) as prev1,

        `IPG2211A2N` as curr
    FROM 
        #table# t1
    ```
7. Because we calculate all 40 data backwards for every data then the first 40 data must contains Null. We need to remove it remembering the data it self has already recorder in next data. We can use ``Spark SQL Query``` Module and run query shown bellow :
    ```sql
    SELECT
        *
    FROM 
        #table# t1
    WHERE
        `prev30` IS NOT NULL
    ```
7. We need to split the data by 90-10 for Training the Model and Evaluation. We can use ```Spark Partitioning``` Module.
8. Considering we want to use 2 Algorithm, Principle Componen Analisys and Polynomial Regression, that Principle Component Analisys need the data have minimum range, we need to Normalize the data. We can use ```Spark Normalizer``` Module of both Partition.

## Modeling

![Modeling](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Modeling.png)

In this step we are going to use 2 Algorithm, Principle Component Analisyst (PCA) and Polynomial Regression. PCA or Principle Component Analisys, common to used as Data Dimension Reduction, used to find New Axis of Data with Maximum Variance, and Find Different Data Point of View. So we can get more useful information from PCA result. And Polynoliam Regression is one of Algorithm to Find Function that represent the data so we can predict the next value with "Poly" Attribute or Dimenssion.

1. First we need to Find the PCA, in this case we use 3 Principle Component. We can use ```Spark PCA``` Module. 
2. After that we need to remove all original attribute except ```cur``` column and ```datetime``` column. We can use ```Spark SQL Query``` Module and run Query bellow :
    ```sql
    SELECT
        `datetime`,
        `PCA dimension 0`,
        `PCA dimension 1`,
        `PCA dimension 2`,
        `curr`
    FROM 
        #table# t1
    ```
3. Considering the Polynomial Regression Module that we want to use are required the input in Table format, then we need to transform it into Table. We can use ```Spark to Table``` Module.
4. To make the model we can use ```Polynomial Regression Learner``` Module and set the ```cur``` column as the target, because we always want to predict the current value of next data, and set all other column except ```datetime``` column as Feature.
4. From the learner we can calculate the Score of the Model. We can use ```Numeric Scorer``` Module. And the result shown bellow :

    ![Modeling Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Modeling%20Evaluation.png)

## Evaluation

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Evaluation.png)

1. First we need to Find the PCA, in this case we use 3 Principle Component. We can use ```Spark PCA``` Module. 
2. After that we need to remove all original attribute except ```cur``` column and ```datetime``` column. We can use ```Spark SQL Query``` Module and run Query bellow :
    ```sql
    SELECT
        `datetime`,
        `PCA dimension 0`,
        `PCA dimension 1`,
        `PCA dimension 2`,
        `curr`
    FROM 
        #table# t1
    ```
3. Considering the Predictore Module that we want to use are required the input in Table format, then we need to transform it into Table. We can use ```Spark to Table``` Module.
4. To create the prediction we can use existing model. We can use ```Regression Predictor``` Module.
4. From the prediction result we can calculate the Score of the Model. We can use ```Numeric Scorer``` Module. And the result shown bellow :

    ![Evaluation - Test](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Evaluation%20Test.png)

## Deployment

![Deployment](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/Electric_Production/Screenshoot/Deployment.png)

In this case we want to deploy the result of Prediction into HDFS back with Parquet Format.
1. We need to tranform the data into Spark. We can use ```Table to Sprark``` Module.
2, We don't want the PCA Attributes included in the data. So we need to remove it. We can use ```Spark SQL Query``` Module and run Query bellow :
    ```sql
    SELECT
        `datetime`,
        `Prediction (curr)` as curr
    FROM 
        #table# t1
    ```
3. Than we need to Joind Back the Original Attribute. We can use ```Spark Joiner``` Module and join the data on ```datetime``` column.
4. The last we need to Save the data into HDFS in Parquet Format. We can use ```Spark to Parquet``` Module.