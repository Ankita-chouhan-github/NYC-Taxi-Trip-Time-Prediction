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

Exploratory Data Analysis: We removed id variable as it doesn’t give much interpretation. We saw in our dataset that we have coordinates in the form of longitude and latitude for pickup and dropoff. But, we can’t really gather any insights or draw conclusions from that. So, the most obvious feature that we can extract from this is distance, so we found out the distance using great_circle from geopy.distance and we also removed trips which had more than 100km distance and less than 0km as they are clearly outliers as shown in the graphs. We then defined a function that gave us the time of the day. Then we plotted the box plot for the variable and found out that there are outliers and We should get rid of the outliers to maintain the consistency of our data. (Trip durations greater than 5000 seconds as well as less than 60 second are outliers, so we remove them from our data). We then checked Passenger count variable has entries from 0 to 9. Since there is no trips with 0 passenger either this a miss entry or the driver forgot to enter passenger count of that trip. Also in a taxi maximum six person are allowed to sit including minor. So we eliminate 0 and 7-9 records from our dataset. We also created a variable speed to find out the average speed of vehicles and found that There are trips that were done at a speed of over 100 km/h. As per the rule in NYC, the speed limit is 25 mph(approx. 40km/h) in New York City unless another limit is posted. So having average speed of over 60km/h is quite unreasonable. so we removed data with speeds more than 60km/h. We found out Trips per hour and see that the busiest hours are 6:00pm to 7:00pm which makes sense as this is the time for people to return home from work. We plotted Trips per week day and found that the fridays are the busiest days followed by saturdays and this is possibly because it's weekend. When we plotted Trips per month there is not much difference observed in the trips across months, but March sees the highest number of trips among all the other months due to good weather (possible reason). We plotted out Trip Duration Per Hour and we see the trip duration is the maximum around 3 pm which may be because of traffic on the roads. Trip duration is the lowest around 6 am as streets may not be busy. By plotting Trip duration per weekday we came to know trip duration on thursday is longest among all days. When we plotted Trip duration per month we found From February, we can see trip duration rising every month. There might be some seasonal parameters like wind/rain which can be a factor of this gradual increase in trip duration over a period. And we did this exploration with many variables and found interesting facts from our data. After EDA we did **Feature Engineering :**

**Feature Engineering :** It is a machine learning technique that leverages data to create new variables that aren’t in the training set. It can produce new features for both supervised and unsupervised learning, with the goal of simplifying and speeding up data transformations while also enhancing model accuracy.
We scaled our data and split it, did correlation analysis which gave us insights such as
* We can see store_and_fwd_flag_y and store_and_fwd_flag_N are highly correlated.
* Also they do not affect the target varible i.e. trip_duration_hour much. Hence we should remove these features from our dataset.
* At the same time vendor_id doesn't affect much either so we can remove that as well.

We degined a function for evaluation metric for regression so that we can utilise it after fitting models in our data.

At last we started Model Building by applying following Regression ML algorithms :

**Linear Regression:** Linear Regression is a regression of dependent variable on independent variable. It is a linear model that assumes a linear relationship between dependent (y) and independent variables (x).
We performed regularization 
1. Lasso Regression : This (Least Absolute Shrinkage and Selection Operator) adds “absolute value of magnitude” of coefficient as penalty term to the loss function.
2. Ridge Regression : It adds “squared magnitude” of coefficient as penalty term to the loss function. Here the highlighted part represents L2 regularization element.

**Decision Tree:** A decision tree is a flowchart-like structure in which each internal node represents a "test" on an attribute (e.g. whether a coin flip comes up heads or tails), each branch represents the outcome of the test, and each leaf node represents a class label (decision taken after computing all attributes).

**XGBoost:** XGBoost comes under boosting and is known as extra gradient boosting. GBM first calculates the model using X and Y then after the prediction is obtain. It will again calculates the model based on residual of previous model, here loss function will give more weightage to error of previous model.

**LightGBM:** Light GBM is based on decision tree algorithm. But it splits the tree leaf wise rather then level wise like other boosting algorithm. So when growing on the same leaf in Light GBM, the leaf-wise algorithm can reduce more loss than the level-wise algorithm and hence results in much better accuracy which can rarely be achieved by any of the existing boosting algorithms.

## **Conclusion**

In this project we covered various aspects of the Machine learning development cycle. We observed that the data exploration and variable analysis is a very important aspect of the whole cycle and should be done for thorough understanding of the data. We also cleaned the data while exploring as there were some outliers which should be treated before feature engineering. Further we did feature engineering to filter and gather only the optimal features which are more significant and covered most of the variance in the dataset. Then finally we trained the models on the optimum featureset to get the results.

At this point, here are a few things we could do to improve our model:

Add more training instances to improve validation curve in the XGBoost model.
Increase the regularization for the learning algorithm. This should decrease the variance and increase the bias towards the validation curve.
Reduce the numbers of features in the training data that we currently use. The algorithm will still fit the training data very well, but due to the decreased number of features, it will build less complex models. This should increase the bias and decrease the variance.






