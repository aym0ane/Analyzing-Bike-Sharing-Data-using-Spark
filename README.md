
# Exploring Usage Patterns and Trends in Bikesharing Data: Insights for Improved Ride-Sharing Experience | Using Apache Spark
![profile](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark/blob/main/images/bikesharinganalysis.png)

## Introduction

Bike-sharing has become a popular mode of transportation in many cities, offering commuters an affordable and eco-friendly alternative to traditional modes of transit. However, as the popularity of bike-sharing services grows, so does the volume of data generated from these services. This presents an opportunity for companies to leverage this data to gain valuable insights into user behavior and preferences.

This project aims to analyze bike-sharing data using various techniques to extract insights regarding usage patterns, popular routes, peak hours/days, demographics etc. The primary objective is to provide actionable insights that can be used by ride-sharing companies to improve their overall service quality and enhance customer experience.


We employ Apache Spark for the analysis process due to its sophisticated capabilities that enable processing large datasets efficiently. The findings from this analysis will aid ride-sharing providers in making informed business decisions related to their marketing strategies or fleet management. Ultimately resulting in a better riding experience for customers utilizing bike sharing within city limits.

## Table Of Contents
- [Introduction](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark#introduction)
- [Apache Spark](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark#apache-spark)
- [Data Set](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark#data-set)
- [Data Analysis](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark#data-analysis)
- [Conclusion](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark#conclusion)

## Apache Spark

Apache Spark is a data processing engine that allows you to perform big data analytics with its distributed computing capabilities.

PySpark is the Python interface for Apache Spark, which enables you to construct scalable and efficient applications using Python.

## Data Set

The provided dataset includes details related to bike rides, including ride_id, the type of vehicle used for the ride (rideable_type), start and end times (started_at and ended_at), starting and ending station names and IDs (start_station_name, start_station_id, end_station_name, end_station_id), latitude/longitude coordinates of starting and ending locations (start_lat/start_lng; end_lat/end_lng) as well as member vs. casual user information.

    |-- ride_id
    |-- rideable_type
    |-- started_at
    |-- ended_at
    |-- start_station_name
    |-- start_station_id
    |-- end_station_name
    |-- end_station_id
    |-- start_lat
    |-- start_lng
    |-- end_lat
    |-- end_lng 
    |-- member_casual 
NB : For the purpose of this project, we only utilized and analyzed data from December. 

DATA SOURCE : https://www.capitalbikeshare.com/system-data

## Data Analysis 

The objective of this project is to analyze data and extract valuable insights regarding usage patterns, popular routes, and other trends. 

The insights obtained from the analysis can be used to improve the overall experience of the ride-sharing service and provide better recommendations to the customers.

The data used and analyzed in this project was limited to the month of December. 

Regarding the analysis, the popular routes were examined in terms of usage patterns through three main categories: rides by hour of day (I), rides by day of week (II), and rides by month (III). The first part investigated peak times for ridership, while the second part examined which days saw higher or lower levels of activity. 

NB : Please note that the notebook contains detailed code and visualizations for reference.
### Popular routes:

    popular_routes = df_clean.groupBy("start_station_name", "end_station_name") \
                    .agg(count("*").alias("num_rides")) \
                    .orderBy("num_rides", ascending=False) 



visualizing Results : 
![profile](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark/blob/main/images/routes.JPG)

### Usage Pattern : 
    
####  I - Rides by hour of day
    rides_by_hour = rides_by_hour.groupBy("hour") \
                    .agg(count("*").alias("num_rides"))

    rides_by_hour = rides_by_hour.orderBy('num_rides',ascending=False)

    rides_by_hour.show(24)

visualizing Results : 
![profile](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark/blob/main/images/hours.JPG)

#### II - Rides by day of week
    rides_by_dayofweek = df_clean.withColumn('dayofweek', date_format('started_at', 'E'))

    # group the data by day of week and count the number of rides
    rides_by_dayofweek = rides_by_dayofweek.groupBy('dayofweek').agg(count('*').alias('num_rides'))

    weekday_order = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']

    rides_by_dayofweek = rides_by_dayofweek.orderBy('num_rides' , ascending=False)

    rides_by_dayofweek.show()

visualizing Results : 
![profile](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark/blob/main/images/days.JPG)

#### III- Rides by months
 
    rides_by_month = df_clean.withColumn('month', month('started_at'))

    rides_by_month = rides_by_month.groupBy('month').agg(count('*').alias('num_rides'))

    rides_by_month = rides_by_month.orderBy('month')

    rides_by_month.show()

visualizing Results : 
![profile](https://github.com/aym0ane/Analyzing-Bike-Sharing-Data-using-Spark/blob/main/images/months.JPG)


## Conclusion

 In conclusion, bike-sharing has emerged as an increasingly popular mode of transportation in many cities and generated large volumes of data. By analyzing this data through various techniques, ride-sharing companies can gain valuable insights into user behavior and preferences such as usage patterns, popular routes, peak hours/days, demographics etc. These insights can be used to improve service quality and enhance customer experience by providing them with better services that meet their needs. As bike-sharing continues to grow as a sustainable alternative for transit systems worldwide, the utilization of data-driven insights will be vital for successful future development and expansion efforts.


