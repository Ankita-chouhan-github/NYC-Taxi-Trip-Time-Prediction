# NYC-Taxi-Trip-Time-Prediction
## **Capstone Project**

## **Introduction**

More than 7 billion people exist on earth. With necessities of food, water and shelter there also a key requirement of commutating from one place to other. Rapid advancement in technology in the last two decades leads to adaption of a more efficient way of transportation via internet and app-based transport system. New York city is one of such advanced city with extensive use of transportation via subways, buses and taxi services. New York has more then 10,000 plus taxi and nearly 50% of population doesn’t have a personal vehicle. Due to this facts most people used taxi has a there primary mode of transport and it accounts for more than 100 millions taxi trips per year.

## **Problem Statement**

The main objective is to build a predictive model, which could help the business in predicting the trip duration of taxi. This would in turn help the business in matching the right cabs with the right customers quickly and efficiently.

## **Data Summary**

The dataset is based on the 2016 NYC Yellow Cab trip record data made available in Big Query on Google Cloud Platform. The data was originally published by the NYC Taxi and Limousine commission (TLC). 
### The contents of NYC Taxi Time Prediction are:
**id -** a unique identifier for each trip.

**vendor_id -** a code indicating the provider associated with the trip record.

**pickup_datetime -** date and time when the meter was engaged.

**dropoff_datetime -** date and time when the meter was disengaged.

**passenger_count -** the number of passengers in the vehicle (driver entered value).

**pickup_longitude -** the longitude where the meter was engaged.

**pickup_latitude -** the latitude where the meter was engaged.

**dropoff_longitude -** the longitude where the meter was disengaged.

**dropoff_latitude -** the latitude where the meter was disengaged.

**store_and_fwd_flag -** This flag indicates whether the trip record was held in vehicle memory before sending to the vendor because the vehicle did not have a connection to the server - Y=store and forward; N=not a store and forward trip.

**trip_duration -** duration of the trip in seconds.

## **Exploring Solutions:**

Having a deeper understanding of what problem we are trying to solve, what the users' needs, and frustrations are, and what the goals are for  achieving the best possible solution for both the business as well as the user, i began by listing out hte possible solutions that were arrived from the research.

## **Steps involved:**

The full code for this article can be found here. It is implemented in Python and different machine learning algorithms are used. Below is a brief description of the general approach that I employed:

Data Loading and general checkups: We have loaded the data from the given csv files using a function from pandas library. Then we checked the general information about data

Exploratory Data Analysis: We removed id variable as it doesn’t give much interpretation. We then calculated the distance based on haversine formula from pickup and drop-off latitude and longitude. Then we plotted the box plot for the variable and observed there are many outlier so we segregate this variable and see that most of the trip are within 10km, some trip are within 50km while a very few trip crosses 50km. so we eliminate trip with 0 and above 50km distance. We then checked for categorical variable store_and_fwd_flag and passenger_count. We observed the store and fwd. flag contain majority of one category. So we drop this feature. Passenger count variable has entries from 0 to 9. Since there is no trips with 0 passenger either this a miss entry or the driver forgot to enter passenger count of that trip. Also in a taxi maximum six person are allowed to sit including minor. So we eliminate 0 and 7-9 records from our dataset.

Linear Regression: Linear Regression is a regression of dependent variable on independent variable. It is a linear model that assumes a linear relationship between dependent (y) and independent variables (x).

XGBoost: XGBoost comes under boosting and is known as extra gradient boosting. GBM first calculates the model using X and Y then after the prediction is obtain. It will again calculates the model based on residual of previous model, here loss function will give more weightage to error of previous model.

LightGBM: Light GBM is based on decision tree algorithm. But it splits the tree leaf wise rather then level wise like other boosting algorithm. So when growing on the same leaf in Light GBM, the leaf-wise algorithm can reduce more loss than the level-wise algorithm and hence results in much better accuracy which can rarely be achieved by any of the existing boosting algorithms.

## **Conclusion**

In this project we covered various aspects of the Machine learning development cycle. We observed that the data exploration and variable analysis is a very important aspect of the whole cycle and should be done for thorough understanding of the data. We also cleaned the data while exploring as there were some outliers which should be treated before feature engineering. Further we did feature engineering to filter and gather only the optimal features which are more significant and covered most of the variance in the dataset. Then finally we trained the models on the optimum featureset to get the results.






