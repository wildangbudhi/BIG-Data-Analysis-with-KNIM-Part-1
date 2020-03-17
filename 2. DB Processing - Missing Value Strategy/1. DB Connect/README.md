# 1. Missing Value Strategy - DB Connect

## Question 
![Question](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/1.%20DB%20Connect/Screenshoot/Question.png)

## Solution
Here is the solution that i provide to Connect to Database or DB using KNIME:

![Solution](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/2.%20DB%20Processing%20-%20Missing%20Value%20Strategy/1.%20DB%20Connect/Screenshoot/Workflow.png)

1. **Connect to DB using DB Connector**
Firstly we need to init an instance of Database Connection, in this case the DB is using SQLite so we can use SQLite Connector.

2. **Select Table using Table Selector**
We need to select particular table. To select table we can use Table Selector for all kind of DB Instance.

3. **Read Selected Table using DB Reader**
Then we need to fetch the data from Selected Table. Here we can user DB Reader to get data From Table Selector.
