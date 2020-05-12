# 5. Mass Learning Event Prediction MLlib to PMML

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Full%20Solution.png)

## Business Undestanding

In this case given data of iris flower containing sepal size, petal size, and the iris class. We were asked to create Compiled Model and predict realtime or event data ( Fast Event )

## Data Understanding

| Column Name  | Description          |
|--------------|----------------------|
| sepal lenght | Lenght of Iris Sepal |
| sepal width  | Width of Iris Sepal  |
| petal lenght | Lenght of Iris Petal |
| petal width  | Width of Iris Petal  |
| class        | class of iris flower |

## Data Preperation

### 1. Data Preparation for Training Model

![Data Preparation - Train](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Data%20Preparation%20-%20Train.png)

- We need to read data to train the model, in this case the data format was in csv format, so we can read the data using ```File Reader``` Module.
- Because the data was pretty big we need to store it in Big Data Environtment, we can use ```Create Local Big Data Environtment``` Module.
- Output of File Reader were in Table Format, we need to store it in BigData Environtment and Convert it in Spark table to make the data process faster and parallel. We can use ```Table to Spark``` Module.

### 2. Data Preparation for Model Evaluation

![Data Preparation - Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Data%20Preparation%20Evaluation.png)

We need to read data to Evaluation the model, in this case the data format was in csv format, so we can read the data using ```File Reader``` Module.

### 3. Data Preparation for Deployment Model

![Data Preparation - Deployment](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Data%20Preparation%20-%20Deployment.png)

- In this case for the realtime or event data we can simulate it using ```Container Input (JSON)``` Module
- Because the model predictor need the input data in Table format we need to convert it into Table format. We can use ```JSON to Table``` Module.

## Modeling

![Modeling](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Modeling.png)

- In this case we were asked to make model to predict Iris using k-Means Algorithm. considering the data is in Spark format, we can use ```Spark k-Means``` Module.
- We need to Convert the model format from ```Spark MLlib``` to format tha required by Model Compiller, named ```PMML```. We can use ```Spark MLlib to PMML Compiler```.
- Then we need to Compile the model. We can use ```PMML Compiler``` Module.

## Evaluation

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Evaluation.png)

- We need to predict data For Evaluation and using Compiled Model. We can use ```Compiled Model Predictor``` Module.
- After we get the prediction, we need to calculate the score. We can use ```Entropy Scorer``` Model.

## Deployment

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/5.%20Mass%20Learning%20Event%20Prediction%20MLlib%20to%20PMML/Screenshoot/Deployment.png)

- Same with Evaluation, but we need to predict data from Event Data and using Compiled Model. We can use ```Compiled Model Predictor``` Module.
- Considering the output that needed is in JSON format and result of ```Compiled Model Predictor``` Module are in Table format. We need to convert it into JSON format, we can use ```Table to JSON``` Module.
- Then we need to output that on JSON format, we can use ```Container Output (JSON)``` Module.