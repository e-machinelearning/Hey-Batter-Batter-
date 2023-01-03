# Hey Batter Batter!
## Capstone 2 Project Final Report
 
 When approached with this project, it was personally an incredible honor to take part and accept it. It may be a surprise, but I myself played baseball for about 12 years! And just as I was no stranger to baseball, baseball is no stranger to the world of statistics and machine learning. 
 
 Any one of you who enjoy movies might already know this, but back in 2011 was released a movie called Moneyball and in the movie describes some of the first usages of modern math and analysis to be used in the old sport of baseball. So when John Doe approached us with the idea of predicting the win percentages of KBO teams so he can safely buy a team, it was an obvious answer of yes we can do it! 
 
### Problem Statement
 John Doe came to us a couple months ago expressing his desire to get into the baseball scene. Before committing thought, he wanted to make sure he had a little advantage over the other teams by knowing who had the best chances of winning based on their stats and predicted stats for next year. He understood that a good baseball team needs a good pitching squad so he grabbed a hold of some pitching stats for the past 40 years of each team and presented us with the task of predicting each team's win percentage for the 2022 season based on these stats.
 
### Approach
 Our approach to this problem was fairly simple. John Doe gave us a pretty neat and organized dataset and our problem dealt with prediction so it was pretty easy to understand we were going to use linear regression. However, the caveat being that we had over 40 years of information so we had to make a time series model!
 
 A couple other minor problems that involved the long span of time was that teams had changed over the years, specifically team names and even some teams dropped from the league throughout the years for various reasons. We had to make sure we were analyzing the teams that were involved with the 2021-2022 seasons and make sure their past names were updated to their present names which involved some internet browsing. 
 
 Another issue was making sure we had all the stats and information we needed. For example, starting in 2020 there was a few addition to the type of stats being recorded such as "balks" or "intentional walks" which were never recorded pre-2000's. So we dropped those and then from there it was mainly analyzing and building the model. 
 
 An important note is that averages are very important in analyzing baseball statistics. Not just one player or one team's average, but we want to be using other players and other team's averages to predict specific players and specific teams. This might sound counterintuitive but everything REGRESSES TOWARDS THE MEAN. One of the many important theorem's in statistics is Stein's Theorem is based on this idea. In a nutshell it basically says that no matter what everything will regress towards the mean because everything is based on partly SKILL and partly LUCK. A player who is having an amazing batting season is probably a really good batter, but they're also probably lucky and they're more than likely not going to stay at that level forever and regress towards the means. Vice versa can be said with a player having a horrible season as well! 
 
 So we paid a lot of attention to the averages. If a team was performing better than the average then that was a good sign but it could also mean that they most likely would return back to the general average of other teams. And we had to make sure if distributions could at least be explained if they were off or if we had to drop some columns or impute some rows.
 
#### Before: 
 
 <img src="https://user-images.githubusercontent.com/99514228/210296726-6ed81b07-5839-4a22-8b0c-8589cf707e07.png" width="600">
 
We ended up only dropping the original rows missing the data pre-2000s but this still didn't explain why our data was not uniform or had quirks in it. Apparently one of the other things that changed over the past 40 years in the KBO is the amount of games played. They have increased multiple times over the years in different increments and so when you increase the amount of games, it also can increase the amount of stats in other columns such as "innings pitched" or "batters faced" since when you play more games you will play more innings and pitch against more batters in one season compared the last. So while our distributions were slightly off, we had an explainable reason as to why they were so. 

#### After: 
 <img src="https://user-images.githubusercontent.com/99514228/210296760-6982c67c-cfed-485c-8b47-71ff4be9bc0d.png" width="600">
 
 From there it was all just building the model. We went with Ridge Regression to help deal with some overfitting but most importantly it would help deal with some multicolinearity we had in our data. Win percentage is based on many factors so it is obvious that multicolinearity would be a big deal in our dataset since many of the stats are correlatted with each other as shown below.  
 
 <img src="https://user-images.githubusercontent.com/99514228/210343701-cc4e2e08-fc92-493d-b3c0-3112c964f2dd.png" width="600">
 
 We built a function that would take in our dataset, the type of model we were using, and the predictor variables we would be using as well. The function would loop through all the years of the dataset and essentially make sure we were only using previous years as the training set and fit the model in order to predict the current year which was the testing set. The function would then return all the predictions for the "Next W/L" ratio which in this case was the year of 2022. After training our model and refining/evaluation We finally got our results!
 
### Results and Findings
 Once we plugged in our model, we find out that our model had predicted the top teams to win would be: 
 
 1. Kiwoom Heroes, 0.5333
 2. LG Twins, 0.5251
 3. KT Wiz, 0.5238
 4. Doosan Bears, 0.5143
 5. SSG Landers, 0.4959
 6. NC Dinos, 0.4937
 7. Samsung Lions, 0.4917
 8. Kia Tigers, 0.4727
 9. Hanwha Eagles, 0.4632
 10. Lotte Giants, 0.4380
 
 So based on this data we would recommend John Doe to look at the top 3 teams which are the Kiwoom Heroes, LG Twins, KT Wiz as potentially winning teams. The reason for this is our model still has some close percentages between the teams so it still could be a close competition. 
 
 Another thing to note is our model was based only on pitching data, and while it produced decent results, it would be much better to include other pieces of data such as batting, fielding, injury report data to make for a much better model. This data is probably more useful in analyzing pitchers for the future and instead of predicting win percentage, John Doe should try predicting important pitching stats such as ERA to look for promising pitchers to add to the roster. The model is created to easily account and adjust for this to predict any other stats they may want to find in the future! So while we do present John Doe with these results, we also advise him to do research of his own and maybe combine our model with other models of batting and fielding data if he can get his hands on them! Good Luck!
 
 
 Model Metrics: 
  Model Features: Easily adjustable for client for other usages, Can add more data if needed
  
  Model Parameters: Dataframe, Model, Predictor Values
  
  Model Hyperparameters: Ridge Regression (alpha=1)
  
  Model Performance Metrics: MSE and RMSE
  

