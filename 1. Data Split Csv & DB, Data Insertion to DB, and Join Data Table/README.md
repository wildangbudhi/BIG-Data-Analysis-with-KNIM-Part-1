# Data Split Csv & DB, Data Insertion to DB, and Join Data Table

## Business Undestanding
This dataset are consist of 3 table of data:
| No. |   File Name  |                               Description                               |
|:---:|:------------:|:-----------------------------------------------------------------------:|
|  1  | flights.csv  | containing detailed data from flights that occur cancellation and delay |
|  2  | airlines.csv | containing list of airlines that available in flight.csv                |
|  3  | airports.csv | containing list of airports that available in flight.csv                |

We can see that there are columns in flights.csv that coresponding to airlines.csv and airports.csv. So we can joining ```airline.csv``` and ```airports.csv``` to the ```flights.csv```. All Join Operation used Left Join because ```filght``` table as a reference for Join Operation. But we first need to figure it out which column in base table is the ```Foreign Key``` and which column in other table is the ```Primary Key```.

### Airlines Table to Flights Table

| AIRLINES (Primary Key) | FLIGHTS (Foreign Key) |
|:----------------------:|:---------------------:|
|        IATA_CODE       |        AIRLINES       |

### Airports Table to Flights Table for Origin Airport

| AIRPORTS (Primary Key) | FLIGHTS (Foreign Key) |
|:----------------------:|:---------------------:|
|        IATA_CODE       |     ORIGIN_AIRPORT    |

### Airports Table to Flights Table for Destination Airport

| AIRPORTS (Primary Key) | FLIGHTS (Foreign Key) |
|:----------------------:|:---------------------:|
|        IATA_CODE       |  DESTINATION_AIRPORT  |

From this we can see that this 3 data or tables is able to be joined into one table, by doing 3 times joining, for the airlines data, airports data for Origin Airport, and airports data for Destination Airport. But we need to rename column name for Airports data becouse it will be joined 2 times and for different purpose to handle same column name when joining.

## Data Undersatnding
There are 3 data or tables

### FLIGHTS ( flights.csv )
|     COLUMN NAME     |                                                 DESCRIPTION                                                |
|:-------------------:|:----------------------------------------------------------------------------------------------------------:|
|         YEAR        | DESTINATION_AIRPORT                                                                                        |
|        MONTH        | Month of the Flight Trip                                                                                   |
|         DAY         | Day of the Flight Trip                                                                                     |
|     DAY_OF_WEEK     | Day of week of the Flight Trip                                                                             |
|       AIRLINE       | Airline Identifier (FK)                                                                                    |
|    FLIGHT_NUMBER    | Flight Identifier                                                                                          |
|     TAIL_NUMBER     | Aircraft Identifier                                                                                        |
|    ORIGIN_AIRPORT   | Starting Airport (FK)                                                                                      |
| DESTINATION_AIRPORT | Destination Airport (FK)                                                                                   |
| SCHEDULED_DEPARTURE | Planned Departure Time                                                                                     |
|    DEPARTURE_TIME   | WHEEL_OFF - TAXI_OUT                                                                                       |
|   DEPARTURE_DELAY   | Total Delay on Departure                                                                                   |
|       TAXI_OUT      | The time duration elapsed between departure from the origin airport gate and wheels off                    |
|      WHEELS_OFF     | The time point that the aircraft's wheels leave the ground                                                 |
|    SCHEDULED_TIME   | Planned time amount needed for the flight trip                                                             |
|     ELAPSED_TIME    | AIR_TIME + TAXI_IN + TAXI_OUT                                                                              |
|       AIR_TIME      | The time duration between wheels_off and wheels_on time                                                    |
|       DISTANCE      | Distance between two airports                                                                              |
|      WHEELS_ON      | The time point that the aircraft's wheels touch on the ground                                              |
|       TAXI_IN       | The time duration elapsed between wheels-on and gate arrival at the destination airport                    |
|  SCHEDULED_ARRIVAL  | Planned arrival time                                                                                       |
|     ARRIVAL_TIME    | WHEELS_ON + TAXI_IN                                                                                        |
|    ARRIVAL_DELAY    | ARRIVAL_TIME - SCHEDULED_ARRIVAL                                                                           |
|       DIVERTED      | Aircraft landed on airport that out of schedule                                                            |
|      CANCELLED      | Flight Cancelled (1 = cancelled)                                                                           |
| CANCELLATION_REASON | Reason for Cancellation of flight: A - Airline/Carrier; B - Weather; C - National Air System; D - Security |
|   AIR_SYSTEM_DELAY  | Delay caused by air system                                                                                 |
|    SECURITY_DELAY   | Delay caused by security                                                                                   |
|    AIRLINE_DELAY    | Delay caused by the airline                                                                                |
| LATE_AIRCRAFT_DELAY | Delay caused by aircraft                                                                                   |
|    WEATHER_DELAY    | Delay caused by weather                                                                                    |

### AIRLINES ( airlines.csv )

| COLUMN NAME |     DESCRIPTION    |
|:-----------:|:------------------:|
|  IATA_CODE  | Airline Identifier |
|   AIRLINE   | Airline's Name     |

### AIRPORTS ( airports.csv )

| COLUMN NAME |         DESCRIPTION         |
|:-----------:|:---------------------------:|
|  IATA_CODE  | Location Identifier         |
|   AIRPORT   | Airport's Name              |
|     CITY    | City Name                   |
|    STATE    | State Name                  |
|   COUNTRY   | Country Name of the Airport |
|   LATITUDE  | Latitude of the Airport     |
|  LONGITUDE  | Longitude of the Airport    |

## Data Preperation
We can see that the data is already splitted into 3 file.

![Data Preparation - Split Data](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/1.%20Data%20Split%20Csv%20%26%20DB%2C%20Data%20Insertion%20to%20DB%2C%20and%20Join%20Data%20Table/screenshot/Data%20Preparation%20-%20Split%20Data.PNG)

And we just need to move one data to DB

![Data Preparation - Save One Data in DB](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/1.%20Data%20Split%20Csv%20%26%20DB%2C%20Data%20Insertion%20to%20DB%2C%20and%20Join%20Data%20Table/screenshot/Data%20Preparation%20-%20Save%20One%20Data%20in%20DB.PNG)

## Modeling

- Read Fligts Data from DB

    ![Modelling - Read Data from DB](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/1.%20Data%20Split%20Csv%20%26%20DB%2C%20Data%20Insertion%20to%20DB%2C%20and%20Join%20Data%20Table/screenshot/Modelling%20-%20Read%20Data%20from%20DB.PNG)

- Read AIRLINES & AIRPORTS Data from CSV

    ![Modelling - Read Data from CSV](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/1.%20Data%20Split%20Csv%20%26%20DB%2C%20Data%20Insertion%20to%20DB%2C%20and%20Join%20Data%20Table/screenshot/Modelling%20-%20Read%20Data%20from%20CSV.PNG)

- Joining Table

    ![Modelling - Join Operation](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/1.%20Data%20Split%20Csv%20%26%20DB%2C%20Data%20Insertion%20to%20DB%2C%20and%20Join%20Data%20Table/screenshot/Modelling%20-%20Join%20Operation.PNG)


## Evaluation
Column in AIRLINES and AIRPORTS data is available in Joined Table

## Deployment
The last is we need top deploy the data in both DB and CSV FILE

![Deployment](https://github.com/wildangbudhi/BIG-Data-with-KNIM/blob/master/1.%20Data%20Split%20Csv%20%26%20DB%2C%20Data%20Insertion%20to%20DB%2C%20and%20Join%20Data%20Table/screenshot/Deployment.PNG)