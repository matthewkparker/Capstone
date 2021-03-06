# NETFLIX recommender system
- Have you ever had those days where you are scrolling through netflix, and a bunch of content that you have already watched is recommended to you? the goal of this project is to make those recommendations optional.
## libraries used:
- For this project, I utilized several Python libraries, including Pandas, Numpy, SQLAlchemy, and SKlearn. In the Assets folder, there will be a .txt file of all the programs that I used to complete this project and their versions.
## Data:
- The data for this project was provided by Kaggle.com, and is a exact copy of the data provided in the famous Netflix prize data. The review data comes in at around two and a half gigabytes, with over one hundred million individual reviews. For each review, the data, movie, and user_id are provided. There are over four hundred and fifty thousand unique users, and over seventeen thousand movies. There is also another data frame provided, which contains movie titles, the movie id from the user review data frames, and the date of the movie release. The data can be found at https://www.kaggle.com/netflix-inc/netflix-prize-data. For this project, I used the movie_titles.csv, and the combined_data.txt 1-4.
## Process:
### Preprocessing:
-The data as provided was unable to be processed, due to improper format, so the proper steps had to be taken in order to format it so that the proper methods could be applied to the data.
- Because the data is so large, and there are many users who do not have many reviews, this notebook also drops users that have less than a certain number of reviews, as well as dropping movies that do not have over a certain number of reviews.
- In addition to properly formatting the data, this notebook also removed individual 'bias' from their reviews, as well as the bias each movie may have. Subtracting the mean of all the reviews from a single users from each of their rating. The same process is then repeated, except the mean of all the reviews of a single movie are then subtracted from all reviews of that particular movie. This notebook also uploads the resultant dataframe into a postgreSQL server, which is being hosted on a AWS EC2 instance.
-NOTE: Because of the size of the data, this notebook may take a long time to run. For my personal computer, with eight gigabytes of RAM, it takes 4 minutes to run through the whole notebook, and 2 minutes to upload the resulting data frame to a postgreSQL server.
### EDA:
- The plot below shows how many times each rating score show up in the user review data
![alt text](https://github.com/matthewkparker/Capstone/blob/master/Images/Ratings.png)
- The plot below shows the distribution of number of reviews per person, capped at 500
![alt text](https://github.com/matthewkparker/Capstone/blob/master/Images/num_of_user_reviews.png)
- The plot below shows the distribution of the number of reviews per movie, capped at 20,000
![alt text](https://github.com/matthewkparker/Capstone/blob/master/Images/num_of_movie_reviews.png)
- This final plot shows the distribution of the number of reviews over time
![alt text](https://github.com/matthewkparker/Capstone/blob/master/Images/time.png)
### Cosine Similarity:
- This is where the actual 'recommending' happens. The first step involves pulling all of the data that was preprocessed from the postgreSQL server. From there, a cosine similarity matrix is created for a single specified user against all other users. What this means is that for an individual user, their reviews are transformed into a vector, compares that users vector to all of the other users vectors, and calculated the cosine of the angle between the two. the result is a scale from 0 to 1, where a 1 indicated that two users have the exact same reviews, and a 0 indicating that they have no review data in common
- after seeing which users are the most similar to the user that is being queried, a function then pulls all of the reviews of the similar users, see's which ones have a high review score, and then returns the movies that similar users rated highly.
## Moving Forward:
- Moving forward, it would be interesting to pull the movie descriptions for the provided movies, and then running cosine similarity on the movie descriptions in order to see how similar individual movies are from one another. This would be useful for recommending movies to users who have not rated movies, which this recommender system requires. I also would like to see how users respond to the recommendations that my system provides. One metric I would use to evaluate my success would be the average click position of recommendations, which means in layman's terms are using picking the most recommended movie, or the second most ect. Another metric I would use to evaluate my recommender system would be the review scores of the movies that my system recommends.
