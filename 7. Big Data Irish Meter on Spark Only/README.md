# 7. Big Data Irish Meter on Spark Only

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Full%20Solution.png)

### Load Data
![Full Solution - Load Data](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Full%20Solution%20-%20Load%20Data.png)

### Extract Date-time Attributes
![Full Solution - Extract Date-time Attributes](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Full%20Solution%20-%20Extract%20Date-time%20Attributes.png)

### Aggregations and Time Series
![Full Solution - Aggregations and Time Series](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Full%20Solution%20-%20Aggregations%20and%20Time%20Series.png)

### PCA, K-means, Scatter Plot
![Full Solution - PCA, K-means, Scatter Plot](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Full%20Solution%20-%20PCA%2C%20K-means%2C%20Scatter%20Plot.png)

## Business Undestanding

Given data of Electicity Meters in Time Series form data. We were asked to Analyze the data to provide a point of view from the data. We were asked to Clustering based on given data.

## Data Understanding

|  Column Name | Description                      |
|-------------:|----------------------------------|
| meterID      | ID of Electricity Meters         |
| enc_datetime | Meta Data of Data Signifies date |
| reading      | Result of Electricity Meters     |

## Data Preperation

![Data Preparation - Full](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Full.png)

### 1. Read Dataset
We need to read the Dataset. We can use ```File Reader``` Module. Result of this module shown bellow: 

![Data Preparation - File Reader Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20File%20Reader%20Result.png)

### 2. Create BigData Environtment

We need to create BigData Environment to Store and Process Massive data. We can use ```CreateL Local Big Data Environtment``` Module.

### 3. Load Data

![Data Preparation - Load Data](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Load%20Data.png)

- We need to create Hive Table on BigData Environtment. We can create Hive Table using ```DB Table Creator``` Module.
- After Hive Table created in BigData Environtment, we need to Load the data into BigData Environtment on Hive Table. We can use ```DB Loader``` Module.

### 4. Convert Hive Table to Spark Dataframe.

Because we want to Calculate a Massive data faster we need to convert the Table into Spark Dataframe. We can use ```Hive to Spark``` Module.

### 5. Exrtract Date-time Attributes

![Data Preparation - Extract Date-time Attributes](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-Extract%20Date-time%20Attributes.png)

We need to decrypt the enc_datetime into several Date-time attribute.

<strong>INITIAL DATETIME CONVERSION RESULT</strong>

First, we need to Extract Date in Format ```dd.M.yyyy``` and Time in Format ```hh:mm```. We can use ```Spark SQL Query``` to query the input data. We use query shown bellow :

```sql
SELECT 
    meterid,
    enc_datetime,
    reading as kw30,
    date_add(cast('2008-12-31' as timestamp), cast(substr(enc_datetime, 1, 3) as int)) as eventDate,
    concat(
        substr(concat("00", cast(cast((cast(substr(enc_datetime, 4) as int) * 30 / 60) as int) %24 as string)), -2, 2),":", 
        substr(concat("00", cast(cast(cast(substr(enc_datetime, 4) as int) * 30 % 60 as int) as string)), -2, 2)
    ) as my_time

FROM 
    #table# t1
```

and the result shown bellow :

![Data Preparation - Initial Datetime Conversion Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Initial%20Datetime%20Conversion%20Result.png)


<strong>EXTRACT NEW DATETIME ATTRIBUTES</strong>

After that we need to extract:
- year
- month
- week
- dayofweek
- hour
We can use query bellow :

```sql
SELECT 
    meterid,
    kw30,
    eventDate,
    year(eventDate) as year,
    month(eventDate) as month,
    weekofyear(eventDate) as week,
    date_format(eventDate, 'EEEE') as dayOfWeek,
    hour(my_time) as hour
FROM 
    #table# t1
```

and the result shown bellow :

![Data Preparation - Extract New Datetime Attributes Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Extract%20New%20Datetime%20Attributes%20Result.png)

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

![Data Preparation - Assign Weekend or Weekday Resul](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Assign%20Weekend%20or%20Weekday%20Result.png)

<strong>ASSIGN HOURLY BINS (daySegment)</strong>

We need to add daySegment, with condition bellow :
- If ```hour``` >= 7 and hour < 9, then daySegment is ```7-9```
- If ```hour``` >= 9 and hour < 13, then daySegment is ```9-13```
- If ```hour``` >= 13 and hour < 17, then daySegment is ```13-17```
- If ```hour``` >= 17 and hour < 21, then daySegment is ```17-21```
- If ```hour``` >= 21 or hour < 7, then daySegment is ```21-7```

We can use Query bellow :

```sql
SELECT 
    meterID, 
    kw30, 
    eventDate, 
    year, 
    month, 
    week, 
    dayOfWeek, 
    dayClassifier, 
    hour,
    CASE 
        WHEN hour >=7 AND hour <9 THEN '7-9'
        WHEN hour >=9 AND hour <13 THEN '9-13' 
        WHEN hour >=13 AND hour <17 THEN '13-17' 
        WHEN hour >=17 AND hour <21 THEN '17-21' 
        WHEN hour >=21 OR hour <7 THEN '21-7' 
    END as daySegment
FROM 
    #table#
```

and the result shown bellow :

![Data Preparation - Assign DaySegment Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Assign%20DaySegment%20Result.png)

### 6. Aggregation and Time Series

![Data Preparation - Aggregation and Time Series](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Aggregation%20and%20Time%20Series.png)

In this step we were asked to Aggregate the data using Mean / Avarage by some category shown bellow:
- Total Usage
- Usage by Year
- Usage by Month
- Usage by Week
- Usage by Day of Week
- Usage by Day
- Usage by daySegment
- Usage by dayClassifier
- Usage by Hour

All category created by the same procedure. 
1. We need to do SUM Aggregate with Group By depent on category. 
    |         Category        |              Group By Column              |
    |:-----------------------:|:-----------------------------------------:|
    |       Total Usage       | meterID                                   |
    |      Usage by Year      | meterID, year                             |
    |      Usage by Month     | meterID, year, month                      |
    |      Usage by Week      | meterID, year, week                       |
    |   Usage by Day Of Week  | meterID, year, dayOfWeek                  |
    |      Usage by Date      | meterID, eventDate                        |
    |   Usage by Day Segment  | meterID, eventDate, daySegment            |
    | Usage by Day Classifier | meterID, year, month, week, dayClassifier |
    |      Usage by Hour      | meterID, eventDate, hour                  |

2. Check wheter the Categorical Column in result of Step 1 have the same value of not. If they have the same value we just need to do Mean Aggregate with Group By ```meterID```, but if they have different value than we need to do the same Mean Aggregate with Group By ```meterID``` using Pivot and set the Pivot based on All Categorical Column Value which have different value.

3. After that we need to rename the column with ```avg``` prefix.

4. When all set we can join all table.

See the result bellow :

![Data Preparation - Aggregation and Time Series Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Aggregation%20and%20Time%20Series%20Result.png)

### 7. Compute Daily and Day Segment Percentages

We need to calculate the Percentages of all daily avarage column or feature and daySegment column or feature. We can use Query bellow :

```sql
SELECT 
    `meterID`, 
    `totalKW`, 
    `avgYearlyKW`,
    `avgMonthlyKW`,
    `avgWeeklyKW`,
    `avgMonday`,
    `avgTuesday`,
    `avgWednesday`,
    `avgThursday`,
    `avgFriday`,
    `avgSaturday`,
    `avgSunday`,
    `avgDaily`,
    `avg_7to9`,
    `avg_9to13`,
    `avg_13to17`,
    `avg_17to21`,
    `avg_21to7`,
    `avg_BD`,
    `avg_WE`,
    `avgHourly`,
    (avgMonday / avgWeeklyKW) * 100.0       as pctMonday,
    (avgTuesday / avgWeeklyKW) * 100.0      as pctTuesday,
    (avgWednesday / avgWeeklyKW) * 100.0    as pctWednesday,
    (avgThursday / avgWeeklyKW) * 100.0     as pctThursday,
    (avgFriday / avgWeeklyKW) * 100.0       as pctFriday,
    (avgSaturday / avgWeeklyKW) * 100.0     as pctSaturday,
    (avgSunday / avgWeeklyKW) * 100.0       as pctSunday,
    (avg_7to9 / avgDaily) * 100.0           as pct_7to9,
    (avg_9to13 / avgDaily) * 100.0          as pct_9to13,
    (avg_13to17 / avgDaily) * 100.0         as pct_13to17,
    (avg_17to21 / avgDaily) * 100.0         as pct_17to21,
    (avg_21to7 / avgDaily) * 100.0          as pct_21to7
       
FROM 
    #table#
```

and the result shown bellow :

![Data Preparation - Compute Daily and Day Segment Percentages Result](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Data%20Preparation%20-%20Compute%20Daily%20and%20Day%20Segment%20Percentages%20Result.png)

## Modeling

![Modeling](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Modeling.png)

In this problem we wan to use 2 method, PCA and k-Means. Why do we need PCA ? PCA or Principle Component Analisys, common to used as Data Dimension Reduction, used to find New Axis of Data with Maximum Variance, and Find Different Data Point of View. So we can get more useful information from PCA result. And k-Means algorith used to get the Cluster of the Data only.

1. Considering we will use PCA method that needs the input data has minimum range, so we need to Normalize the data. We can use ```Spark Normalizer```.
2. Apply PCA Algorithm to get more information. We can use ```Spark PCA``` module, with minimum information fraction to preserve setted 96% and exlcude ```meterID``` column.
3. Apply k-Means Algorithm to get the cluster of the Data. We can use ```Spark k-Means``` module using ```Spark Normalizer``` output as input, set the number of cluster to 3, and exlude ```metedID``` column.
4. Remembering the goals of Applyment of k-Means is to get the Cluster of the Data. Than we need to remove all the column Except ```meterID``` column as the data id and ```Cluster``` column as cluster of the data. We can use ```Spark Column Filter``` module.
5. Than we need to join the result of PCA with the Cluster obtained from k-Means. We can use ```Spark Joiner``` Module.`
6. Considering in the Evaluation Step we want to Plot the data, we need to convert the data from Spart Dataframe to Table. We can use ```Spark to Table``` Module.
7. Remembering the data is in Normalized data, we want to denormalize the data to get the actual data with original range. We can use the output of ```Spark Normalizer``` which give a matrix of Normalization Factor as input in ```Denormalizer (PMML)``` to Denormalize the data.

## Evaluation

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Evaluation.png)

In this we want to Plot the data in Graph with different color each cluster and Show in table too.
1. First we need to convert all data which in Number Data Type to String. We can use ```Number to String``` module.
2. Add Color for each Cluster. We can use ```Color Manager``` Module.
3. Show the data in Grah using ```Scatter Plot``` Module.
4. Show the data in Table using ```Table View``` Module.

and the result shown bellow :

![Evaluation - Plot](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/7.%20Big%20Data%20Irish%20Meter%20on%20Spark%20Only/Screenshoot/Evaluation%20-%20Plot.png)

## Deployment