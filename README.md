# Lyft Baywheels 2022 Exploratory Data Analysis 

## Project Overview
In this project, we analyzed Lyft Baywheels trip data from 2022 and suggested measures that could be taken to improve the experience of Baywheels users and increase customer satisfaction.

## Business Understanding
We approach this analysis from the point of view of the operators of the Baywheels rideshare program, Lyft. We want to understand the different types of Baywheels bike users, and how the company can better cater to the needs users as a group, and as a whole.

To achieve this, we aim to answer the following questions:
1. Do the needs of the customers differ by membership type? How do they differ and how can the company cater to these needs?
2. Do the needs of the customers differ by the type of bike they use? How do they differ and how can the company cater to these needs?
3. At which stations can Lyft focus more on rebalancing efforts to alleviate bike shortage for Baywheels users?

**What is rebalancing?** \
Rebalancing is an optimization problem that refers to meeting demand at certain stations by relocating them and temporarily increasing station capacity, and is a key challenge faced by operators providing such rideshare services [[1](https://people.orie.cornell.edu/shane/pubs/BSOvernight.pdf)].  

In the most common approach, trucks are used to move bikes to high-demand areas. This is particularly effective overnight, when both traffic and demand are low. During the day, vehicular traffic impairs these
efforts, and instead operators use trikes to transport a smaller number of bikes across stations, or corrals to artificially increase the capacity of stations.

The optimization of rebalancing is a complex problem that we will only briefly touch on in this analysis.

**Summary of Findings** \
Overall, our findings can be summarized thus:
1. Subscribers are more likely to use the bikes for short distances during peak hours on weekdays, they also tend to prefer classic bikes. Non-subscribers prefer to use electric bikes for convenience or leisure during offpeak hours and on weekends. When providing classic and electric bikes, the company should provide fast classic bikes and comfortable electric bikes in line with subscribers and non-subscribers' preferences.
2. Electric bikes are utilized for longer distances, accruing greater mileage in a shorter period of time and thus may be more prone to wear and tear. The company may wish to check on the condition of these bikes more often.
3. Page St at Masonic Ave and Leavenworth St at Broadway stations have the greatest deficit in bikes at the end of the day; more bikes can be allocated to these stations during rebalancing overnight. Howard St at Beale St and Post St at Kearny St stations have some of the highest mid-day deficits during evening rush hours; special effort can be taken during mid-day rebalancing to supply bikes to these stations at 5pm.


## Data Understanding
The dataset used contains records of individual rides made via a bike-sharing system covering the greater San Francisco Bay area in 2022. It provides details of each ride, such as a unique ride ID, start and end stations, start and end coordinates, bike type and membership type.

The data is made up of over 2.5 million rows of data. Of 2.5 million, 400,000 rows were missing the start, end, or both stations of trips, and 2000 rows were missing endpoint coordinates. By comparing station name and station ID, we were able to fill in only about 2700 missing station names. 

With the datetime python package, we were able to create columns for:
- Trip duration in minutes
- Month the trip started
- Day the trip started
  If the day is a weekday or a weekend
- Hour of the day the trip started

With the math python package, we were able to define the Haversine function in python. The Haversine distance can be defined as the angular distance between two locations on the Earth’s surface [[2](https://towardsdatascience.com/calculating-distance-between-two-geolocations-in-python-26ad3afe287b)]. Using this function and the start/endpoint coordinates, we were able to create a new calculated column for the total distance of each trip in kilometers.

The original data is available on [Lyft's System Data page](https://www.lyft.com/bikes/bay-wheels/system-data).

## Analysis
#### All Users


#### Subscribers vs. Non-Subscribers
Baywheels user can be split into subscribers and non-subscribers. Subscriber take up 58% of the ridership and non-subscribers are 43%.
![newplot (3)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/624d4f0a-8c05-47d1-ae7c-611f67efaac1)


For example, we can see in the below chart that subscribers use bikes more often on weekdays, while non-subscribers prefer trips on weekends. At the same time, subscribers tend to take shorter trips with smaller distances compared to non-subscribers. 
![newplot (4)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/afb0baf1-43ff-46d3-8e75-6fbf29ec22df)
![newplot (5)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/6d9c2a18-204a-4e1e-bd6f-49c59aa1b2c5)
![newplot (15)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/01357715-103a-4eb6-9165-bb9cae7b7c64)


Let's also see the breakdown of number of trips for every hour of a typical weekday. The number of bike trips by subscribers is extremely clustered around the peak hours of 8am and 5pm.
![newplot (7)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/79669de9-8692-46e5-b643-0ddbab1a2f28)
![newplot (8)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/4fae0727-294a-4707-911d-e70f22bf6dfc)

Constructing a profile of each type of user, we can say:
- A subscriber is more likely to take shorter rides during peak hours on a weekday. This rider profile fits people who may be working adults or college students, and are on a committed schedule.
- A non-subscriber is more likely to take longer rides during non-peak hours on a weekend. This rider profile fits people who may have a more flexible schedule or does not use Baywheels bikes regularly. They may be more spontaneous in using Baywheels bikes, or use them for leisure or enjoyment.


#### Electric Bikes vs. Classic Bikes
Baywheels users can also be split into electric bike users and classic bike users. 65% of rides use electric bikes, 35% use classic bikes
![newplot (9)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/e2bb7c00-3350-4a0e-b75d-79b11894adbf)

As we do not know the how many electric bikes and classic bikes that the operator has provided, it is difficult to determine if the this 65-35 ratio is reflecting the ratio of bikes provided by the operator or if it is reflecting the true preferences of the customers. As a baseline, there are 1.85 more rides that use an electric bike compared to a classic bike. 
At first glance, this ratio of electric bikes to classic bikes does not seem to change across the week. The ratio remains at approximately 1.8 with a slight peak on Friday, when it reaches 1.9 electric bikes to classic bikes.
![newplot (19)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/57f66fe5-c5ae-4d02-9578-5146e334ac4b)

However, when we take a closer look at the ratio based on membership type, we notice a significant difference. For subscribers, the ratio of electric bikes to classic bikes has a lower ratio of 1.63, while non-subscribers significantly prefer electric bikes. Non-subscribers are at a whopping 2.2 electric bike rides to every classic bike ride! Electric bikes can carry the user a great distance with little effort on the user's part, so it's possible that this convenience attracts casual nom-subscribers. On the other hand, a significant number of subscribers seem to prefer classic bikes more than electric bikes. 
![newplot (21)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/7dfac7c0-5311-41f4-918c-ffe78c62f5d3)

Also, we note that the median distance of an electric bike trip is longer than the median distance of a classic bike trip for all days.
![newplot (12)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/7bcf4756-808d-492d-962c-6fe4d9496534) 

#### Stations With High Demand of Bikes
The top 10 stations with the most outgoing traffic are also the stations with the most incoming traffic and likewise for the stations with the least traffic. The demand for bikes are the greatest at Howard St at Beale St, Salesforce Transit Center (Natoma St at 2nd St) and Post St at Kearny St on the weekdays at 5pm. Likewise the supply of bikes are greatest at these 3 stations at 8am.
![newplot (13)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/eb5b1636-835e-4ebf-b125-1c8fe1b7322d)
![newplot (14)](https://github.com/kuehbiko/01-Portfolio-Projects/assets/88494428/6211df6f-08fc-4e31-a5bc-4c0f3448d6b8)

Over the week, the demand for bikes are greatest at Page St at Masonic Ave and Leavenworth St at Broadway and the supply of bikes are greatest at North Point St at Polk St on the weekends.


## Conclusions
**Do the needs of the customers differ by membership type? How do they differ and how can the company cater to these needs?**

The preferences of members and casual users are significantly different. Trips by members are shorter and more frequent during the peak hours of weekdays, while casual customers prefer trips that are longer and during off-peak hours or weekends. We can infer that most members are working adults or college students with a fixed schedule and need for reliable transportation. Casual customers on the other hand are more likely to make a trip out of convenience or spontaneity. 

We recommend that targeted ad campaigns towards members and casual users differ in the kinds of promotions being offered. For example, members might be more likely to enjoy a discount on recurring monthly subscriptions while casual users might be more likely to enjoy one-time promotions. 

**Do the needs of the customers differ by the type of bike they use? How do they differ and how can the company cater to these needs?**

There is no significant preference by the overal customer base for the type of bike provided by the service, although we note that subscribers prefer classic bikes while non-subscribers prefer electric bikes. This is in line with subscribers apparently having a fixed schedule, either for work or for exercise, while non-subscribers prefer electric bikes that can travel great distance with little effort. However, as the overall preference for electric and classic bikes, we have no recommendation to provide more of either type of bike as a whole. Still, keeping the preferences of subscribers and non-subscribers in mind, we suggest that the company provide faster classic bikes for subscribers and more comfortable electric bikes for non-subscribers.

Electric bikes accrue a higher mileage than classic bikes across all days of the week. Due to heavily usage, electric bikes may be at a higher risk of wear and tear compared to classic bikes. Therefore we would recommend that maintenance for electric bikes occur more frequently than classic bikes.

**3. At which stations can Lyft focus more on rebalancing efforts to alleviate bike shortage for Baywheels users?**

In terms of rebalancing, the demand for bikes are greatest at Page St at Masonic Ave and Leavenworth St at Broadway. The company could take this into account during overnight rebalancing to provide more bikes to this station. Also, there is often a surplus of bikes at North Point St at Polk St. For efficient rebalancing, the company may consider funneling bikes from this station to stations with high daily demand.

**Next Steps** \
Given the true location of each station and the cost of transporting bikes, there is an opportunity to optimize the rebalancing process of bikes, both overnight and during the day. This will allow the company to efficiently allocate resources to the rebalancing of bikes at each station with greater precision of the exact hour and minute when demand is the greatest (at the moment, we only have an estimate).

We can further explore the preferences of members and casual users through binary classification techniques. This will allow us to identify the features that are most strongly associated with subscribers. This way, the company may be able to identify casual users with certain habits that have to potential to become members. The company may then be able to send such users targeted adviertisements to convince them.
