# EAS BigData - Time Series Analysis (sales-of-shampoo-over-a-three-ye)

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Full%20Solution.png)

### Load Data
![Full Solution - Load Data](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Full%20Solution%20-%20Load%20Data.png)

### Extract Date-time Attributes
![Full Solution - Extract Date-time Attributes](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Full%20Solution%20-%20Extract%20Date-time%20Attibutes.png)

### PCA, K-means, Scatter Plot
![Full Solution - PCA, K-means, Scatter Plot](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Full%20Solution%20-%20PCA%2C%20K-means%2C%20Scatter%20Plot.png)

## Business Undestanding

Given data of Sales of Shampoo Over a Three Year in Time Series form data. We were asked to Analyze the data to provide a point of view from the data. We were asked to Clustering based on given data.

## Data Understanding

|                Column Name                |                Description                |
|:-----------------------------------------:|:-----------------------------------------:|
|                   Month                   | Meta Data of Time                         |
| Sales of shampoo over a three year period | Sales of shampoo over a three year period |

## Data Preperation

![Data Preparation - Full](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation.png)

### 1. Read Dataset
We need to read the Dataset. We can use ```File Reader``` Module. Result of this module shown bellow: 

![Data Preparation - File Reader Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20File%20Reader%20Result.png)

### 2. Create BigData Environtment

We need to create BigData Environment to Store and Process Massive data. We can use ```CreateL Local Big Data Environtment``` Module.

### 3. Load Data

![Data Preparation - Load Data](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20Load%20Data.png)

- We need to create Hive Table on BigData Environtment. We can create Hive Table using ```DB Table Creator``` Module.
- After Hive Table created in BigData Environtment, we need to Load the data into BigData Environtment on Hive Table. We can use ```DB Loader``` Module.

### 4. Convert Hive Table to Spark Dataframe.

Because we want to Calculate a Massive data faster we need to convert the Table into Spark Dataframe. We can use ```Hive to Spark``` Module.

### 5. Exrtract Date-time Attributes

![Data Preparation - Extract Date-time Attributes](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20Extract%20Date-time%20Attributes.png)

<strong>INITIAL DATETIME</strong>

We need to add "0" in front of the Date and initiate fake years.  We can use ```Spark SQL Query``` to query the input data. We use query shown bellow :

```sql
SELECT 
	`Sales of shampoo over a three year period` as curr,
	CONCAT( "0", `Month`, "-2020" ) AS datetime
FROM 
	#table# t1
```

and the result shown bellow :

![Data Preparation - Initial Datetime Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20Initial%20Datetime%20Result.png)

<strong>EXTRACT DATETIME FEATURES</strong>

We need to convert the datetime input Date data type to ease extraction of datetime features. We can use ```Spark SQL Query``` to query the input data. We use query shown bellow :

```sql
SELECT 
	`curr`,
	TO_DATE( `datetime`, 'dd-MMMM-yyyy' ) AS datetime

FROM 
	#table# t1
```

and the result shown bellow :

![Data Preparation - Initial Datetime Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20Extract%20Datetime%20Result.png)

<strong>EXTRACT DATETIME FEATURES 2</strong>

We need to extract datetime feature :
- month
- week
- dayOfWeek
We can use ```Spark SQL Query``` to query the input data. We use query shown bellow :

```sql
SELECT 
	`curr`,
	`datetime`,
	month( `datetime` ) as month,
	weekofyear( `datetime` ) as week,
	date_format( `datetime` , 'EEEE') as dayOfWeek

FROM 
	#table# t1
```

and the result shown bellow :

![Data Preparation - Initial Datetime Result]https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20Extract%20Datetime%202%20Result.png)

<strong>ASSIGN WEEKEND OR WEEKDAY</strong>

We need to create a class that identify wheter the day is weekend or weekdays with column name ```dayClassifier``` and with class :
- WE --> Weekend
- BD --> Weekday

We can use query bellow :

```sql
SELECT 
	*, 
	CASE 
		WHEN dayOfWeek in ('Saturday','Sunday') THEN 'WE' 
		ELSE 'BD' 
	END as dayClassifier
FROM 
	#table#
```
and the result shown bellow :

![Data Preparation - Assign Weekend or Weekday Resul](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Data%20Preparation%20-%20Assigen%20Weekedn%20or%20Weekdays.png)

## Modeling


![Modeling](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Modeling.png)

In this problem we wan to use 2 method, PCA and k-Means. Why do we need PCA ? PCA or Principle Component Analisys, common to used as Data Dimension Reduction, used to find New Axis of Data with Maximum Variance, and Find Different Data Point of View. So we can get more useful information from PCA result. And k-Means algorith used to get the Cluster of the Data only.

1. Considering we will use PCA method that needs the input data has minimum range, so we need to Normalize the data. We can use ```Spark Normalizer```.
2. Apply PCA Algorithm to get more information. We can use ```Spark PCA``` module, with minimum information fraction to preserve setted 96% and exlcude ```meterID``` column.
3. Apply k-Means Algorithm to get the cluster of the Data. We can use ```Spark k-Means``` module using ```Spark Normalizer``` output as input, set the number of cluster to 3, and exlude ```metedID``` column.
4. Remembering the goals of Applyment of k-Means is to get the Cluster of the Data. Than we need to remove all the column Except ```meterID``` column as the data id and ```Cluster``` column as cluster of the data. We can use ```Spark Column Filter``` module.
5. Than we need to join the result of PCA with the Cluster obtained from k-Means. We can use ```Spark Joiner``` Module.`
6. Considering in the Evaluation Step we want to Plot the data, we need to convert the data from Spart Dataframe to Table. We can use ```Spark to Table``` Module.
7. Remembering the data is in Normalized data, we want to denormalize the data to get the actual data with original range. We can use the output of ```Spark Normalizer``` which give a matrix of Normalization Factor as input in ```Denormalizer (PMML)``` to Denormalize the data.

## Evaluation

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Evaluation.png)

In this we want to Plot the data in Graph with different color each cluster and Show in table too.
1. First we need to convert all data which in Number Data Type to String. We can use ```Number to String``` module.
2. Add Color for each Cluster. We can use ```Color Manager``` Module.
3. Show the data in Grah using ```Scatter Plot``` Module.
4. Show the data in Table using ```Table View``` Module.

and the result shown bellow :

![Evaluation - Plot](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Evaluation%20-%20Plot.png)

## Deployment

![Deployment 1](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Deployment%201.png)

![Deployment 2](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/8.%20EAS%20BigData%20-%20Time%20Series%20Analysis/sales-of-shampoo-over-a-three-ye/Screenshoot/Deployment%202.png)

We want to save the result in HDFS back in Hive Table format and Parquet Format.
1. Considering the Result of Modeling Step is in Table Format, then we need to Convert it back to Spark Dataframe. We can use ```Table to Spark``` Module.
2. Considering when we write data to Hive table we can't have column name with space. then we need to rename all column name with space to remove the space. We can user ```Spark Column Rename``` Module.
3. Write it to Have Table using ```Spark to Hive``` Module.
4. Write it to Parquet using ```Spark to Parquet``` Module.