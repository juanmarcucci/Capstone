# Problem Statement
When looking to book short-term rental stays, such as through Airbnb, how do you know if you're getting a good deal? The area of interest might be totally unfamiliar and without context a good judgment call on affordability of the rental is uncertain. On top of this there are also seasonal patterns, changing travel preferences, and inflation which can all vary the price for the same location year after year. In order to help the consumer I am developing a website widget that can learn from historical and recent prices, analyze listings of interest, and return how over or under market price they are charging per night. This will ensure you have an edge when finding your next travel destination lodge and you feel comfortable that you can find the best deals!

# Data Acquisition
http://insideairbnb.com/get-the-data/ \
Inside Airbnb is a volunteer organization/website that collects publibly available data from Airbnnb, across 100s of cities, and performs their own cleaning to make it easily accesible. For this proof-of concept model and initial exploration of the data I downloaded their 06 June, 2022 data for Los Angeles. \
I am using their Detailed Listings data and neighbourhoods list. A data dictionary can be found in their website and I have also dowloaded it here, in the 'data' folder.

# EDA
The dataset contains 40,438 entries for different listings, and 75 different features for each. I started by analyzing the numerical values first with correlation to pick the best predictors of the 'price' variable. With 'bedrooms', 'accommodates', 'beds' showing the strongest correlation, albeit still relatively low. After cleaning up the data and creating a basic model I moved on to the categorical features and those which are technically numerical but needed parsing to be calcualted as continous. \
Following intuition I first pursued the location based variables but to no avail, 'latitude', 'longitude' showed weak correlation even when combined together. \
Even the neighbourhoods feature proved unfruitful, I believe the dimensionality was too big for the model, goven that there were 265 unique neighbourhoods. This feature could use another look from a different angle. \
Time data also proved a little tricky to work with, the datatset is not built for time analysis and trying to perform a basic age-of-account analysis proved unfruitful, maily due to the lack of review data. \
Host Location initially looked favorable, with some intial statistical results showing promise yet it did not significantly improve the metrics of the model. \
Bathrooms proved surprisingly robust in correlation and did have a positive effect on the metrics. \
Finally 'Room Type' rounded out this iteration of feature selection, showing a visible linear relationship with 'Price' and effectively adding to the metrics.

# Modeling
Most of the time spent on this project was spent cleaning and selecting the data so Linear Regression was the go-to model for comparison, with the r2 score standing in as a measure of the effectivness of each additional feature. Unfortunately the highest r2 score achieved was a 0.25 both for the trainining and testing data. Further anaylsis and different models are needed to make the most out of this data, but given that this was not the original intention of Airbnb it still showed surprising promise.


# Results and Recommendations
The best predictor features for our purposes were = 'bedrooms', 'accommodates', 'beds', 'bathrooms_text', 'room_type', 'price'. The most surprising aspect being that the location based variables proved unfrutiful, contradicting well-known real estate adages.

After extensive feature selection and engineering next steps would be trying different models and loading in more data. It seems that the features we have at the moment might not be the best for predicting prices of the listings. After that intergrating the model into a web browser widget would be the priority, so that the model could be tested against new data such as brand new listings.