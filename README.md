# TMDB Movie Analysis

<a id='intro'></a>
## Introduction

### Dataset Description 

This dataset is from Kaggle: 5000 Movie Dataset and contains information about 10,000 movies collected from The Movie Database (TMDb), including user ratings and revenue.
The primary goal of this project is to practice pandas, Numpy, and Matplotlib data analysis techniques.


### Questions for Analysis
1) Which genres are most popular from year to year? 
2) How did film budgets change from each decade? 
3) What kinds of properties are associated with movies that have high revenues?

<a id='conclusions'></a>
## Conclusions

### Summary

1) The top two most popular genres are Drama and Comedy.
2) Drama has been most popular generally from 1960 to 2015.
3) 1990s has the highest film budget on average while 1970s has the lowest.
4) There is an increase in budget from 1970s to 1990s.
5) There is a decrease in budget from 1990s to 2010s.
6) Vote Count, Budget, and Popularity has highest association with the movies that have high revenues.


### Limitations:
1) The dataset contains null and zero values in some features. These zero and null values hinders the analysis and have to be removed. so data cleaning is a necessary part before moving on to the dataset's investigation.
2) There were multiple genres in each movie, I split the genress so each genre is allocated to 1 row.
3) The revenue and budget were not denominated in currency, so it’s unsure whether they are in USD, or another currency.
