# ETL_Project

Gideon Schultz, Martha Karran, Jenny Yi

OVERVIEW:
Extracting, cleaning, transforming, and unionizing Netflix and Hulu TV show data to see which shows are available on which streaming service(s).

EXTRACT:
We extracted the following datasets in csv. formats:
1.	A data set of 6,234 movies and TV shows available on Netflix as of 2019. The dataset is collected from Flixable, which is a third-party Netflix search engine. 
a.	https://www.kaggle.com/shivamb/netflix-shows
2.	A dataset of Hulu’s top 1,000 most popular TV shows up until 2017. 
a.	https://data.world/chasewillden/top-1-000-most-popular-hulu-shows

TRANSFORM:
Similar variables existed in both datasets, which made it easy to identify the variables we wanted to include in our final dataset. We chose to extract the following columns from each dataset: “Show_ID,” “Show_Name,” “Genre,” “TV_Rating,” “Description”

We reformatted the column names and used underscores instead of spaces to ensure consistency between the two datasets, being mindful of the order of the columns when we unionized the two datasets, which made it easier to upload into SQL later.

Transforming the Netflix CSV file:
1.	Choosing the columns we wanted and renaming them:
a.	The following columns were extracted from the original netflix dataset: show_id, title, listed_in, rating, description. 
b.	These columns were renamed “Show_ID,” “Show_Name,” “Genre,” “TV_Rating,” and “Description,” respectively. 
2.	Since this data set included both movies and TV shows, we filtered out all 4,265 movies 

Transforming the Hulu CSV file:
1.	Transforming columns 
a.	The following columns were extracted from the original Hulu dataset: show/id, show/name, show/genre, show/show_rollups/subscriber/highest_rating, show/description
b.	These columns were renamed “Show_ID,” “Show_Name,” “Genre,” “TV_Rating,” and “Description,” respectively. 
2.	We sorted the new dataset alphabetically by “Show_Name” to visualize any duplicates.
a.	To assess the duplicates further, we counted the number of instances of each show in the “Show_Name” column. 
b.	Using the drop_duplicates function in pandas, we dropped duplicates, keeping the last instance of each. 
c.	To confirm that duplicates were successfully removed, we counted the number of instances of each show again, looking for only one instance of each. 

Unionizing and adding data to the combined dataframe:
We unionized the two dataframes as opposed to merging because we had set up each dataframe to have exactly the same columns. Unionizing meant we would be place all the data from each on top of each other, as opposed to combining columns through merging. 

First, we created a new column that would capture whether each TV show was available on each streaming service (see below).
-	netflix/hulu_df_2["Available on Netflix/Hulu"] = "Yes"

However, once we unionized both datasets, we realized all the empty rows of each competitor column contained “NaN,” so we also replaced all the “NaN” with “No” so that each cell in the availability columns contained either “Yes” or “No.”

LOAD:
We decided to use a Relational Database because our merged CSV file is highly structured. Because we planned ahead and transformed this data, we can quickly conduct analysis for any future projects using this data as it would not need any further cleaning.


