# best_in_show
![Screenshot 2023-09-19 at 5 39 01 PM](https://github.com/joannasantana/best_in_show/assets/129118228/01b515f4-00e4-4767-b34e-0e77bd201e01)


For our project, we set out with a goal to be able to predict movies that have the greatest chance of winning Best Picture (also previously known as Outstanding Motion Picture, Outstanding Picture, Outstanding Production, and Best Motion Picture) at the Academy Awards. We were able to find a dataset which held all of the winners and nominees for all categories included at the Academy Awards. This set our first challenge of creating a data frame from this data and cleaning it. It was a very large data set, however got down to a much more manageable number once we cleaned and filtered for only the category of Best Picture (also all its previous aliases). 
<img width="1037" alt="Screenshot 2023-09-14 at 7 03 45 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/587f272f-c81c-48f9-a747-d412f6a1b2a4">

Once we had this portion completed we used an OMDB API call to get more information about each film and used these as the features in our machine learing model. We took the year and title of the Academy Awards recognized films and used this information to make the API call.
<img width="1097" alt="Screenshot 2023-09-14 at 7 09 40 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/6aa8c50e-7f1f-4ec9-a2f3-0eb76158029a">

The dataframe we created by merging csv and our API results required a lot of cleaning. It was important that we started by recognizing we needed to change many of our columns to an int64 data type. This required that we clean up the numeric data to remove any special characters ($ and ,). After this we also saw issues with some of our columns having multiple data pieces within one column, the most noted example being our genre column.<img width="972" alt="Screenshot 2023-09-14 at 7 14 44 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/d0c9ed96-4f2c-4ca8-a268-db03c02cd1d6">

This required us to utilize the str.split function to split on the comma of the genres. We then used one-hot-encoding to make a separate column for each genre and then having a "1" or "0" be the data to represent if the movie in question fell in that category or not, respectively.
<img width="718" alt="Screenshot 2023-09-14 at 7 19 53 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/fc77e351-cb40-4944-8976-c2edd9d473be">

One of the difficulties we found at this point in the project was an 'nan' value being given in one of our columns, which we needed to eliminate.  
![Screenshot 2023-09-14 at 8 18 35 PM](https://github.com/joannasantana/best_in_show/assets/129118228/894c0415-a2f1-4c4b-91dd-3e00fdc166bc)

Our first model attempt used logistic regression and included the following features: movie runtime, metascore based on critic reviews, IMDB’s Rating based on audience reviews, number of votes on IMDB, box office revenue, movie genre, movie rating, and the year of the oscars ceremony.

This initial model didn’t predict a winner at all, it predicted loser every time. As you can see the accuracy score is still pretty high, at 84%...but that’s just because 16% of our dataset were actually winners! The actual results are heavily imbalanced, as far more movies are nominated for an Oscar but only one wins each year. For this reason, when looking at accuracy we focused on getting the balanced accuracy score to improve, meaning that our model was not only correctly predicting losers, but correctly predicting winners. You can see that the balanced accuracy score we’re starting with is 0.5, so our model is essentially no better than a completely uninformed guess.


The following changes were attempted to improve our model:
- Model types: Logistic Regression + Random Forest
- Data added: Golden Globes results, Director, Producer, Country
- Data transformed: Standard Scaling on numeric columns (We saw a large improvement in the effectiveness of our model once we scaled our data!)
- Data removed: Box Office
- Data limited: Years of Ceremony (past 50 years only, 1944 - 2020 only)

Because of inflation, we thought maybe removing the box office column would make sense, as two box office return values decades apart aren’t very comparable.

We also tried limiting our dataset to just the past 50 years of data just because the movie business has changed so much since the 1920s. Whenever we included the golden globes results, the years were limited to 1944-2020 since those were the years that we had golden globes results for.

With all that said, in all our attempts we were not able to get our balanced accuracy score above 75%. 

<img width="983" alt="Screenshot 2023-09-17 at 8 23 41 AM" src="https://github.com/joannasantana/best_in_show/assets/129118228/30375661-ee44-4ff7-858e-88ecd364c556">

Our best model attempt ended up using logistic regression with standard scaling on our numeric columns. None of the data from our first attempt was removed but we added the golden globes results which limited the years of our data to 1944-2020.
We chose this model as our best attempt because it had the best balanced accuracy score of all our models, at 64%.

When analyzing the confusion matrix, we see that the model predicted winner 15% of the time, which is a nice improvement over the 0% in our first attempt. Considering that most years of the oscars have 5-10 nominees and only one winner…15% seems right.

In looking at the precision, the model is correct 81% of the time when it predicts loser, and 62% of the time when it predicts winner. Compared to the precision scores, recall scores go up for actual losers and down for actual winners which makes sense because of our imbalanced dataset.


After recreating our model, we were officially ready to start using it to try and predict the 2024 Oscar Winners!  We ran the model with films that are predicted to be nominated for best picture to see how they compare to one another using our model. 


<img width="1038" alt="Screenshot 2023-09-17 at 8 35 22 AM" src="https://github.com/joannasantana/best_in_show/assets/129118228/670a71fc-1b23-4ef6-9414-d30ef53d933b">

Unfortunately, our model said none of them would win.  We considered that this may be since we do not have the Golden Globes winners for 2024 yet this year, so we manipulated the data to say that each movie won the Golden Globe.  In that case our model will then predict that "Oppenheimer" will win 'Best Picture' at the Oscars in 2024. 

However, we are aware that our model is not foolproof.  Our idea was to test films viewed as "snubbed" in their year to see if our model would correctly determine that they did not win.  This was not the case.  "Singin' in the Rain" was famously snubbed from a 'Best Picture' nomination, however based on our model "Singin' in the Rain" would have won!  



<img width="478" alt="Screenshot 2023-09-17 at 8 39 12 AM" src="https://github.com/joannasantana/best_in_show/assets/129118228/bac05c9b-71b2-4edc-a064-079413aab21e">


In order to get a better visual of our data, we used Tableau to make some comparisons of different features we examined.  This gave us the opportunity to look at some variables independently such as how the rating of the movie affected the result.

![Screenshot 2023-09-19 at 5 28 32 PM](https://github.com/joannasantana/best_in_show/assets/129118228/5cdee040-94e3-4bbd-8ebd-2680fa68e5c8)

These kind of visualizations also made us curious about other variables and their effect on results, this led us to also looking at runtime which also appeared to have at least some sort of pattern in results, with variation on the preference for longer or shorter runtimes over the years.

![Screenshot 2023-09-19 at 5 30 37 PM](https://github.com/joannasantana/best_in_show/assets/129118228/b2b0e1e8-1a2e-4d8b-bfb6-48ca7c6e64ee)

So obviously, it still has many improvements to be made in order for it to give a more accurate prediction.  Based on the information we have used, we were rather happy with how our model performed!  Brainstorming and researching other models led us to the conclusion that one of our problems was most likely that we did not have sentiment scores.  Another model did utilize this important field and still were at 0.89 at best.  Specifically for this type of data, it seems that sentiment scores are an important predictor of which film will win.  So considering that our data does not have this key piece of data and still was able to have an effectiveness of 0.64, we were pleased and excited to utilize our model during the 2024 Academy Awards!

Sources:
Academy awards database: https://awardsdatabase.oscars.org/

Kaggle: https://www.kaggle.com/datasets/unanimad/the-oscar-award?select=the_oscar_award.csv,
https://www.kaggle.com/datasets/unanimad/golden-globe-awards

