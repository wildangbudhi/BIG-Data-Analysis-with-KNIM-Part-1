# 6. PMML to Spark Comprehensive Mode Learning Mass Prediction

![Full Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Full%20Solution.png)

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

### 1. Data Preparation for Model Train

![Data Preparation - Train](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Data%20Preparation%20-%20Train.png)

We need to read data to Train the model, in this case the data format was in csv format, so we can read the data using ```File Reader``` Module.

### 2. Data Preparation for Model Evaluation

![Data Preparation - Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Data%20Preparation%20-%20Evaluation.png)

- We need to read data to Evaluate the model, in this case the data format was in csv format, so we can read the data using ```File Reader``` Module.
- Because the data was pretty big we need to store it in Big Data Environtment, we can use ```Create Local Big Data Environtment``` Module.
- Output of File Reader were in Table Format, we need to store it in BigData Environtment and Convert it in Spark table to make the data process faster and parallel. We can use ```Table to Spark``` Module.

### 3. Data Preparation for Model Deployment

![Data Preparation - Deployment](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Data%20Preparation%20-%20Deployment.png)

- In this case for the realtime or event data we can simulate it using ```Container Input (JSON)``` Module
- Because the model predictor need the input data in Table format we need to convert it into Table format. We can use ```JSON to Table``` Module.

## Modeling

![Modelling](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Data%20Preparation%20-%20Train.png)

- In this case we are using 2 algorithm, Decision Tree and Multi Layer Perceptron using RProp Optimation. We can use ```Decission Tree Learner``` Module and ```RProp MLP Learner``` Module. Both we set to output on PMML Format
- Because we neet to concate those 2 model we need to convert it into Cell Format. We can use ```PMML to Cell``` Module.
- Than we can concate the model using ```Concatenate``` Module.
- Considering result of ```Concatenate``` Module was in Table Format we need to convert it into PMML Format. We can use ```Table to PMML Ensemble``` Module.
- Than we need to compile the model, we can use ```PMML Compiler``` Module.

## Evaluation

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Evaluation.png)

- We need to predict the Evaluation Data using Spark Compiled Model. We can use ```Spark Compiled Model Predictor``` Module.
- Considering the result of ``Spark Compiled Model Predictor``` Module was Spark format we need to convert it into Table format.
- After the prediction format became Table, we can calculate the score. We can use ```Scorer``` Module.

## Deployment

![Evaluation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/6%20PMML%20to%20Spark%20Comprehensive%20Mode%20Learning%20Mass%20Prediction/Screenshoot/Deployment.png)

- Same with Evaluation, but we need to predict data from Event Data and using Compiled Model. We can use ```Compiled Model Predictor``` Module.
- Considering the output that needed is in JSON format and result of ```Compiled Model Predictor``` Module are in Table format. We need to convert it into JSON format, we can use ```Table to JSON``` Module.
- Then we need to output that on JSON format, we can use ```Container Output (JSON)``` Module.