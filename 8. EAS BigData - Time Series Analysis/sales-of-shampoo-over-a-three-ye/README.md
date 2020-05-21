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

![Data Preparation - File Reader Result]())

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

## Modeling

## Evaluation

## Deployment