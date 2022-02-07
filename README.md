# Nigeria is battling a food price inflation, I try to look at what the data says
## Analysis of the dataset shows that much of Nigeria's food producing states are battling violent activities. Is this the cause of the food inflation seen in different parts of the country, especially the southern part of the country where the prices are higher?
<hr>
An analysis of food price index in Nigeria that looks at insecurity as a cause for food inflation

Nigeria has been facing consistent food inflation over the last few years as it fights insecurity in form of insurgency, gang activities and uptick in general social crimes. The purpose of this project is to find out what the data reveals about the impact of this insecurity on the current food price hike.

## Datasets

For this analysis, I depended on the data from Nigeria's National Bureau of Statistics, which collects and publishes food price index every year. This has been consistent for more than 5 yyears but for this story, I used the food price index data from 2017, which is [this file](https://github.com/kfalayi/Food_price_Nigeria/blob/main/Nigfoodprices.xlsx)

Also, I used [another dataset](https://github.com/kfalayi/Food_price_Nigeria/blob/main/original_datalocation.xlsx) from the same agency which shows the average prices of the same food commodities listed in the previous dataset but this time, it shows the price in each state for December 2021 month. December was the most current price index available.

The prices in the datasets are in Naira and I decided to stick to that. $1 equalis ₦416.2. For each item in the dataset, for anyone who is wondering about the unit of measurement, they are explained on pages 4 to 14 of [this NBS report](file:///Users/owner/Downloads/SELECTED%20FOOD%20DECEMBER%202021%20REPORT.pdf).

A needed another data that gives an insight on the security issues of Nigeria, the best I could find is Council on Foreign Affairs which collates data on different forms of violent activities in the country and I used its security [tracker data](https://github.com/kfalayi/Food_price_Nigeria/blob/main/attacks.xlsx), which covers the last 10 years.
<hr>

# Data Analysis
Analyis is done using Python with Pandas and Plotnine.
The most important tool to import initially are pandas and all the plotnine's syntactic tools.

** import pandas as pd
pd.set_option('display.max_columns', None)
from plotnine import *

I first import my initial dataset, which does not allow me to do the needed analysis because the dates appear as column titles.

First of all, I got rid of the long decimal numbers by rounding the figures to 1 decimal place. Then I saved a copy of the file so I don't have to work out of my orgininal data file.

I read in the copy which is [this file](https://github.com/kfalayi/Food_price_Nigeria/blob/main/Myfood.xlsx).

The dataframe is wide and this would make any plotting impossible, so I had to melt it down for easy visualization in plotnine.

By melting it down, I am able to bring the dataframe to three columns  - date, price and items.

Nothing can be done with the date until it becomes a proper date, so what do I need to do? Convert to datetime. But there is a stumbling block - the damned 'underscore' needs to go away. I converted it to hyphens instead, which is recognized by datetime conversion.

Once I converted the date column to datetime, it is now possible to look at the price changes over time. But wait, does it make sense to look at all the food items? 
Maybe a subset would make more sense? So yeah, I decided to limit the dataframe to just 6 food items.
By visualizing the prices with plotnine, I am able to see how the prices have moved over the last 5 years.

But this is not enough to tell my story.

Just to see what the price movement would be like for another set of food, I did a similar visualization on another 6 sets of food commodities and it shows a similar pattern of increase in varying degress.

Then, I read in the the dataset that contains average price of items per states/location (Dec 2021 price).

The purpose of bringing in the dataset at this point is to find out the price difference in the states.
Again, I had to limit the dataframe to the first 6 food commodities I chose to focus on.

I transposed the columns so that the food rows become the food columns and I saved this in a fresh [file](https://github.com/kfalayi/Food_price_Nigeria/blob/main/MyFood_location.csv).

Then I melted down the dataframe because it is still wide and also added a column to show which zone of the country each state falls in.

I wanted to see the price according to state for each of the 6 items and filtered it by each commodity then visualized the top 10 price location.

Now is the time to bring in the security tracker data.

I imported the file and saved a [copy](https://github.com/kfalayi/Food_price_Nigeria/blob/main/attack_trimmed.csv).

I joined this to a [file](https://github.com/kfalayi/Food_price_Nigeria/blob/main/Nigeria_states_coords.xlsx) containing the geometry of each state to make it possible to visualize in map.

Again, I did some datetime conversion, then I saved the new dataframe into a [csv file](https://github.com/kfalayi/Food_price_Nigeria/blob/main/death_toll.csv).

I grouped the dataframe by the states with numbers of deaths and it was this I visualized in a heat map on the [web story](https://kfalayi.github.io/food-price-Nigeria.html).










