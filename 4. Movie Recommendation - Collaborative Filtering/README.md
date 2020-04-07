# 4. Movie Recommendation - Collaborative Filtering

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/Full%20Solution.png)

## Business Undestanding

This dataset are consist of 2 table of data:
| No |  File Name  |                           Description                           |
|:--:|:-----------:|:---------------------------------------------------------------:|
|  1 | movies.csv  | Containing List of Movies                                       |
|  2 | ratings.csv | Containing List of Ratings of Movie inside movies.csv from user |

In this task we asked to Make TOP 20 Recommendation Base on Ratings. Ratings of Movie obtained from table ```ratings.csv``` and some input rating from User ( Using KNIME )

## Data Understanding

There are 2 data or tables

### MOVIES ( movies.csv )
| Column Name |          Description          |
|:-----------:|:-----------------------------:|
| movieId     | ID or Identifier of the movie |
| title       | Title of the movie            |
| genres      | List of Genre from the movie  |

### RATINGS ( ratings.csv )
| Column Name |                 Description                 |
|:-----------:|:-------------------------------------------:|
| userId      | ID of user that gives the movie rating      |
| movieId     | ID or Identifier of the movie in movies.csv |
| rating      | Rating of movie that given from user        |
| timestamp   | Timestamp when the rating is written        |

## Data Preperation

### 1. Create Local BigData Environtment Contex

![Local BigData Environtment Contex](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/%5BData%20Preparation%5D%20Create%20BigData%20Env%20Instance.png)

Because the data is massive so we need to make BigData Environtment to save the data faster and process the data in parallel way so its faster than Sequence Processing.

### 2. Read Data and Prepare for Training and Evaluation

![For Training and Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/%5BData%20Preparation%5D%20For%20Training%20and%20Evaluation.png)

- To train the Model we need to prepare the data read the data from file ```ratings.csv```. To save the data in distributed node or server in BigData Environtment Contex we need to Convert table to Spark Dataframe for faster processing too. We can use ```CSV to Spark``` Module to Read CSV and Save the Table in BigData Environtment in Spark Dataframe Format.
- We need to split the data into 80% - 20%. 80% for Training and 20% for Evaluation. Since the data are in Spark Dataframe format we can use ```Spark Partitioning``` Module

### 2. Read Data and Prepare for Training and Testing

![For Training and Testing](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/%5BData%20Preparation%5D%20For%20Training%20and%20Testing.png)

- In this case we are given data which contain List of Movie and we need to input rating of 20 Random Movie to be used in Training Data
- First we need to read the data. We can use ```File Reader``` Module to Read ```movies.csv```
- Then we need to add userid column and timestamp column. In this case we can make Custom Module contains many existing module. Called ```add field``` Module.
- After that, we need to split 20 data for the train and rest of it for the testing. Since the data is in Ordinary Table format we can split it using ```Row Splitter``` Module.
- Then we need to Shape and Remove unused Column, Like Title using custom Module called ```Ask User for Movie Ratings```. Inside that module there is ```Table Editor``` module to input the user rating as follows <br />
![User Input Rating](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/%5BData%20Preparation%5D%20For%20Training%20and%20Testing%20-%20User%20Input%20TOP%2020%20Movies%20Ratings.png)
- After the 20 data ratings is inputed, considering the previous data format we should save the data in BigData Environtment in Spart format. We can use ```Table to Spark``` Module.
- For the testing data we also need to shape, remove unused column and add ratings column fill it with 0. In this case we use Costum Modul, called ```no rating``` Module.
- We also should save the data in BigData Environtment in Spart format. We can use ```Table to Spark``` Module.

## Modeling

![Modeling](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/%5BModeling%5D%20Full%20Solution.png)

- First we need to combine tha data from ```ratings.csv``` data and 20 Data from User Input. Considering those 2 data is in Spark Dataframe format we can use ```Spark Concatenate``` Module.
- Then we need to train a model using ```Spark Collaborative Filtering Learner (MDLib)``` Module.

## Evaluation

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/4.%20Movie%20Recommendation%20-%20Collaborative%20Filtering/Screenshoot/%5BEvaluation%5D%20Full%20Solution.png)



## Deployment