# best_in_show

For our project, we set out with a goal to be able to predict movies that have the greatest chance of winning Best Picture (also previously known as Outstanding Motion Picture, Outstanding Picture, Outstanding Production, and Best Motion Picture) at the Academy Awards. We were able to find a dataset which held all of the winners and nominees for all categories included at the Academy Awards. This set our first challenge of creating a data frame from this data and cleaning it. It was a very large data set, however got down to a much more manageable number once we cleaned and filtered for only the category of Best Picture (also all its previous aliases). 
<img width="1037" alt="Screenshot 2023-09-14 at 7 03 45 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/587f272f-c81c-48f9-a747-d412f6a1b2a4">

Once we had this portion completed we found an API key which we then used our data frame to compare the films we were able to find.  We filtered through and found which films within our csv data were able to be found in our API key by comparing on like variables.
<img width="1097" alt="Screenshot 2023-09-14 at 7 09 40 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/6aa8c50e-7f1f-4ec9-a2f3-0eb76158029a">

The data frame we created using our csv and our API required a lot of cleaning. It was important that we started by recognizing we needed to change many of our columns to int64. After this we also saw issues with some of our columns having multiple data pieces within one column, the most noted example being our genre column.<img width="972" alt="Screenshot 2023-09-14 at 7 14 44 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/d0c9ed96-4f2c-4ca8-a268-db03c02cd1d6">

This required us to utilize the split function and try to split on the comma of the genres. However, after this it was recognized that we actually needed to create many columns which contained all the genre names and one-hot-encoding and then having a "1" or "0" be the data to represent if the movie in question fell in that category or not respectively.
<img width="718" alt="Screenshot 2023-09-14 at 7 19 53 PM" src="https://github.com/joannasantana/best_in_show/assets/129118228/fc77e351-cb40-4944-8976-c2edd9d473be">

After cleaning all this information it was finally time for us to utilize our data and attempt to teach this model to predict the future "Best Picture" at the Academy Awards.  In order to do this we had to do the linear regression.  Unfortunately, the best we could seem to get was about 0.53 which was when we also used data collected on the Golden Globes to also help predict winners.  One of the difficulties we found at this point in the project was an 'nan' value being given in one of our columns, which we believed could be skewing the data.  
![Screenshot 2023-09-14 at 8 18 35 PM](https://github.com/joannasantana/best_in_show/assets/129118228/894c0415-a2f1-4c4b-91dd-3e00fdc166bc)


In order to get through this issue, we had to go back in and update our columns in order to ensure that did not show up and change our data.  As you can see in our updated columns there is no 'nan' present.


