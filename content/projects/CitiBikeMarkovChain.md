---
title: "Predicting Citi Bike Availability Using Markov Chains"
date: 2022-12-15T23:15:00+07:00
slug: Markov-Chain
category: projects
summary:
description:
cover:
  image: "covers/citibike.jpg"
  alt:
  caption:
  relative: true
showtoc: true
draft: false
author: ["Ruize Hou", "Zooey Zhang", "Micheal Ahedor", "Jack Guo"]
---

# Predict Citi Bike Availability Using Markov Chains

In this project, we used the stochastic model Markov Chains to predict the availability for Citi Bike of stations Broadway & W 25 St, Central Park S & 6 Ave, and Broadway & E 21 St in New York City.

### Method 1
#### Preprocessing 
In order to ensure adequate data, we first chose the three stations with the most bikes being ridden away as the object of our analysis, which are Broadway & W 25 St, Central Park S & 6 Ave, and Broadway & E 21 St. We defined daytime as 7am to 3pm and nighttime as 3pm to 11pm, keeping only the data from these two time periods and splitting them into two groups. In addition, we stripped out the weekend data, leaving only the weekday data (21 days in total).

#### Transition Matrix

We adopt the 10 minutes discrete time block, implying 48 time blocks for each daytime and nighttime data. Based on each time block, for example, the time block from 07:00 to 07:10, calculate its net flow by subtracting the bicycle flow in from the bicycle flow out. (Where flow in is the number of bikes that have an end time in this time period and flow out is the number of bikes that have a start time in this time period). Then put all the net flows into a list and compute the probability of each net flow. Build 2d net flow metrics for all time periods. For instance, if there are 19 docks at the station, a 20x20  matrix is generated with row and columns representing the number of cars from 0 to 19. Then fill the probability of net flow in, say the probability of -2 (net flow out) is 0.25, then the probability of the number of bicycles available at the station swift from 19 to 17, 18 to 16, and so on, are 0.25. Then, sum up this row and divide each element in the row by this sum to ensure that the probability transition always adds up to 1.  We get 6 transition matrices in total.
#### New method:
We attempted to use a new approach to estimate the transition matrix. We tried to model the transition probability matrix for each time interval, and then do matrix multiplication to all of these matrices to get the transition probabilities from each start of the morning/evening to end of the morning/evening. However, this method does not work well because our data set is not large enough to support such small segmentation of time.

#### Stationary distribution & Analysis
![image1](/images/CitiBike/SD_CP_M.png)
![image1](/images/CitiBike/SD_CP_E.png)
![image1](/images/CitiBike/SD_BW_M.png)
![image1](/images/CitiBike/SD_BW_E.png)
![image1](/images/CitiBike/SD_BE_M.png)
![image1](/images/CitiBike/SD_BE_E.png)

The stationary distribution tells us that in the morning, for all of the three stations, they all have very high availabilities around 15 to 17.5, which is reasonable because the Citibike staff will restock the bikes at morning. In addition, for these popular stations where the flow in exceeds flow out in the morning as people who work nearby and many tourists ride their bikes in. 

In the evening, in contrast to the morning, there are fewer bikes available at stations as the bike flow out exceeds flow in as people who work nearby and tourists ride their bikes out.

So we can say that all three stations tend to have many bikes at noon, and very few bikes in the evening.
