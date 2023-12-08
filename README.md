# Gamer-Group-I310D-Project
A data science group project by the "Gamer Group" (Alexander Ibrahim, Keegan Fleigner, & Shasa Kolur) for our I310D course at UT Austin. The goal of the project was to find a dataset and preforms some operations to accept or reject a hypothesis, test an ML model or some other data science work. Gamer Group choose a dataset of Chicago Taxis and looked at change in travel time over the day (bivarble) as well as overlap between start and stop locations (kmeans clustering). 

Goal:
Our goal was to test the hypothesis that travel time is longest during the 9:00am rush hour due to people all going to work around that time as well as around 5:00pm, when many people are going home. For the k-means clustering, our goal was to find common pickup and dropoff locations.

Outside Resources/Citations:
For this project we used multiple outside resources. We used: 

Buitinck, L., Louppe, G., Blondel, M., Pedregosa, F., Mueller, A., Grisel, O., Niculae, V., Prettenhofer, P., Gramfort, A., Grobler, J., Layton, R., Vanderplas, J., Joly, A., Holt, B., & Varoquaux, G. (2013,   September 1). API design for Machine Learning Software: Experiences from the scikit-learn project. arXiv.org. https://arxiv.org/abs/1309.0238

Codebasics. (2019, February 9). Machine Learning Tutorial Python - 13: K-Means Clustering Algorithm [Video]. https://www.youtube.com/watch?v=EItlUEPCIzM

Hunter, J. D. (2007). Matplotlib: A 2D graphics environment. Computing in Science & Engineering, 9(3), 90–95. https://doi.org/10.1109/MCSE.2007.55

Skytower, N. (2011, October). How can I get a value that’s inside parentheses in a string in Python? [duplicate]. stack overflow. https://stackoverflow.com/questions/8040795/how-can-i-get-a-value-thats-inside-parentheses-in-a-string-in-python

The pandas development team. pandas-dev/pandas: Pandas [Computer software]. https://github.com/pandas-dev/pandas

Dataset Extraction and Transformation:
Our Dataset was found at: https://data.cityofchicago.org/Transportation/Taxi-Trips/wrvz-psew. From this dataset, we used pandas to take 5 columns: “trip_start_timestamp” (ex.“2023-10-06T09:00:00.000”), “trip_seconds” (ex.“2061”), “trip_miles” (ex.“18.52”), “pickup_centroid_location” (ex. “POINT (-87.6327464887, 41.8809944707)”), and "“dropoff_centroid_location” (ex. “POINT (-87.6327464887, 41.8809944707)”). “trip_start_timestamp” was transformed 5 columns using multiple split commands (Year, Month, Day, Hour, and Minute) which were all saved as integers. “pickup_centroid_location” & "dropoff_centroid_location" were transformed into 2 columns each: pickup_longitude, pickup_latitude, dropoff_longitude, and dropoff_latitude. This was done by isolating the text in the parenthesis and then spliting the numbers. They were saved as floats. This lead to a final dataframe with the 11 columns: "trip_seconds", "trip_miles", "trip_start_day", "trip_start_month", "trip_start_year", "trip_start_hour", "trip_start_minute", "pickup_longitude", "pickup_latitude", "dropoff_longitude", "dropoff_latitude". This was the data that was used for analysis.

Methodology for Travel Time Over the Day:
We began with our bivariable analysis of travel time over the day. We started by creating a new subset "travel_time_df" with the columns "trip_seconds", "trip_miles", and "trip_start_time" so that any transformations we did of data would not affect the main data table. The "trip_start_time" column was created by changing minutes into a function of an hour (ex. 15 min = 0.25 hours) so that time of day could accurately be represented on an axis. Following this, the columns "trip_seconds" & "trip_miles" was used to create a rate of seconds/miles to represent the amount of seconds it takes to cross a mile and used this to make a new columns called "seconds_per_mile". We used this subset for all of our bivariable analysis. Before created a graph, we used a boxplot to check for outliers in the ""seconds_per_mile" column. We found their were high outliers so we used the 1.5IQR+3rd quadrants to set a limit on the why axis of our graph so that the graph doesn't display any outliers. We then created a scatterplot of ("trip_start_time", "seconds_per_mile") entitled "Trip Start Time vs Amount of Seconds it Takes to Travel a Mile".

Results for Travel Time Over the Day:
We concluded there is evidence of an increase of travel time during the morning rush to work however, the rest of the day had a somewhat consistent spread of travel time with the except of the late night (past 20:00) and early morning (before 5:00).

Methodolgy for Grouping of Pickup and Dropoff Locations:
Next, we did our k-mean clustering of pickup and dropoff locations. First we checked for duplicates in the dataset and found that pickup locations (pair of the longitude and latitude values) had only three unique points while dropoff had only 51 unique points. This can be considered a flaw in our data that hinders our ability to draw meaningful conlusions. However, we continued on to make our k-means cluster. We started this by creating a Sum of Square Error graph for both pickup and dropoff and decided that to use three clusters for both (this is using the data with duplicates). We then scaled our data points to be on a scale of 0 to 1 (these where added to the data table under the columns "scaled_longitude" and "scaled_latitude") and then used these points to determine and assign cluster groups; the cluster group numbers were added to the table under the column named "cluster" (this is done using MinMaxScaler and the sklearn library; this is done to the dataset with duplicates). The dataframe was then split into three seperate data frames based on the cluster group that each point was assigned to. We then graphed the non-scaled values (longitude, latitude) of each data frame with each data frame being a different color (this was done using the data with duplicates). This was done to both pickup and dropoff producing two seperate scatterplots.

Results for Grouping of Pickup and Dropoff Locations:
For conclusions, it was difficult to draw any from the pickup location due to the severe overlap of datapoints. All we can really so is that all pickups happen in one of those three pickup locations. As for dropoff, the clusters are fairly intermingled, with no tight groups. This tells us that there is no one location were you can expect a large amount of drop off to be in very close proximity to. It is worth noting however, that our graph is unable of showing were overlapping points are and to what degree they are overlapping, this, means our graph my be deceptive and lead to wrong conclusions - this is a limitation of our results.

Conclusion:
Overall, we determined that our hypothesis that there is an increase in travel time during morning commute is true but our hypothesis that the same happens in evening commute is false. We also found that our dataset does not lend itself to 2d modeling k-mean clusters as a result of a large number of duplicate data points. We were unable to make inferences from the pickup data due to having only three unique points and could only make the limited inference about drop off data that there are no regions with a high number of dropoffs with very close proximity.






