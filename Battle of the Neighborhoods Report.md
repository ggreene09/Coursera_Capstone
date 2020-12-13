# Battle of the Neighborhoods - Report

## Introduction/Business Problem
In this project, our theoretical business is interested in opening a new high-end Italian restaurant in the city of Chicago, Illinois. Chicago is known worldwide for its food, and much of it is rooted in Italian cuisine, deep dish pizza being the primary example. However, Chicago is also incredibly diverse, with major Polish, Chinese, Arabic, Korean and other neighborhoods.

The biggest challenge is that the restaurant scene in Chicago is very saturated, especially so for an Italian venue. So we will be taking a look at Chicago's demographic data to determine the best location to open the business. In order to come to a conclusion, we need to determine which neighborhoods lack Italian food options, which areas are most similar to those where Italian restaurants thrive, and which of our remaining areas are the most affluent.

## Data
Information on current Chicago restaurants and their locations will be obtained from Foursquare's API. We will use this to obtain all listed venues in Chicago.

Luckily, the city of Chicago maintains a rather large amount of data that we'll need for this project. In order to determine which neighborhood to target, we need demographic information such as population and income. This can be obtained from Chicago's census data, pulled from [here](https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2/data).

This data contains the Per Capita Income for each neighborhood in Chicago, as well as the percentage of the population that is under the age of 18 and over the age of 64. We will consider this population range when making our determination.

Another piece of data we need is the total population for each neighborhood, since they vary greatly in actual size. This will be pull from the [Wikipedia page on Chicago Community Areas](https://en.wikipedia.org/wiki/Community_areas_in_Chicago).

## Methodology

I started by pulling the demographic data for Chicago. In order to pull data from Foursquare and match the restaurants to the neighborhoods, I added a column for the latitude and longitude for each column
After exploring the data, I could see that it required a small amount of cleaning. First, the neighborhood Montclare was misspelled as "Montclaire," while Washington Heights was missing the "s" at the end of its name.
There was also a "total" row at the bottom that showed demographic information for Chicago as a whole. This was removed from the data set.

I used Nominatim to retrieve the latitude and longitude for each of the neighborhoods. The coordinates where then fed into the Foursquare API in order to pull all venues in a radius of 1 kilometer.
By having the total venues in each neighborhood, I could then segment the neighbrohoods into different clusters to determine which ones were most similar to each other.

By using one hot encoding, I averaged out the numbers for each venue and used K-means clustering to segment the neighborhoods. The clustering result showed 3 distinct groups (clusters 0, 1 and 3)
along with 2 other clusters that were so different from the rest that they were classified into their own groups (clusters 2 and 4).

Cluster 2, consisting solely of Riverdale, is one of Chicago's poorest neighborhoods. With a per capita income of just over $8,000 per year, it was determined to be a bad fit for an upscale restaurant.
Likewise, cluster 4 was only made up of South Deering, which is a heavily industrial area that would not be a good fit either.

That said, 48 of the restaurants that Foursquare listed as "Italian" were in the cluster #1. Clusters 0 and 3 had only 2 restaurants apiece. With that in mind, it's clear that the neighborhoods in Cluster 1
are a good fit for an Italian restaurant. However, since we are opening an "upscale" Italian restaurant, community areas with a per capita income of under $40,000 per year will not be considered.

The next thing to look at was the current saturation of each neighborhood. We obviously don't want to open up yet another Italian restaurant if there are already several in the area. Since the sizes
of the neighborhoods are very different, we will consider the ratio of Italian restaurants to population. The population data was pulled from the Wikipedia page and merged into our dataset. Then, from our earlier
Foursquare report, I added the number of Italian restuarants per neighborhood and added the number in a new column.

We then needed to find out how many people would be in each neighborhood per Italian restaurant if one more (ours) were to open in the area. To get an even better idea of where we should open the restaurant,
I multiplied the population per Italian restaurant by the per capita income, and then reduced this by the percentage of the population that is out of our target age range (under 18 and older than 64). The results became clear.

## Results
After looking at market saturation, Lincoln Park emerged as the front runner. It was closely followed by the Near West Side, Lake View, and Forest Glen.

However, we then took into account the income for each area. With the Near North Side having far and away the richest of Chicago's citizens, it shot from seventh place to second. The rankings did not change much after accounting for the target age range. However, when this was considered, Forest Glen moved from sixth place to eighth due to 40.5 percent of its population being outside our target age.

In any way the results are read, it's clear that Lincoln Park would be the best neighborhood to open the restaurant.

## Discussion
Lincoln Park already has 2 established Italian Restaurants. However, its population being on the higher side of our dataset, saturation was not determined to be a problem. If
the restaurant is opened here, there will still be 22,570 people per Italian restaurant. Combined with the area's income (in our age range), this means that there is $1.267 billion in income per Italian restaurant.

The Near North Side is the second option. The market here is very saturated. If we open here, there would only be 14,815 people per restaurant. However, its wealth means there is more opportunity than less saturated neighborhoods.

Lake View looked like a clear choice when initially looking at the data. It easily has the highest population (over 100,000 compared to Lincoln Park's 67,000) in Cluster 1 with income above $40,000. However, there are already 4 Italian restaurants here
which meant there would be 20,957 people per restaurant. It will be the third choice.

If we did not make any distinction on the affluence of the neighborhood, Uptown would be the first choice. There are no restaurants here at all that are classified as Italian. However, with only $35,000 per year in per capita income, it was not determined to be a good fit.

## Conclusion
Based on the data, I recommend that any high-end Italian restaurant opens in Lincoln Park. The neighborhood has the second highest income per capita at $71,551. 88.5% of the population is either an adult or below 64 years old, and it has a decently high population 67,710.
Two Italian restaurants currently operate here, which signals that this cuisine can do well here. Notwithstanding the fact that the characteristics of Lincoln Park are similar to other areas where Italian restaurants thrive.


