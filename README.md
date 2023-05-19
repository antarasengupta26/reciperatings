# Recipe Ratings

by Antara Sengupta (asengupt@ucsd.edu) and George Chong (gchong@ucsd.edu)

---

## Introduction

The dataset that we are working with in this project is the Recipe and Ratings set. We have two sets of data that we are dealing with, recipes and ratings. The recipe data has information regarding recipes and has columns regarding nutritional content, steps & time, contributor identification, along with tags and descriptions. The recipe dataset has 83,782 observations, or rows. The ratings data has information regarding reviews and ratings of the recipes from the recipe dataset. The ratings dataset has 731,927 observations, or rows. To start off our project, we merged these two datasets on their common shared column of recipe ID, and then proceeded with all other analysis on this merged dataframe. All this data has been made available by scraping www.food.com, which contains the recipes and ratings. For this specific project, our main question is: Are Italian recipes on average rated higher than Indian recipes? This question compares the average ratings of the two most popular and common cuisines that have recipes at www.food.com. We found that this would be relevant and important information for visitors of this website as it provides insight into which popular cuisine has better recipes, based on user reviews. The columns that we found relevant to our analysis and question are the recipe ID, tags and ratings columns. The recipe ID column has a string value of numbers that are unique to each recipe. The tags column has a list of strings that are associated with the specific recipe, which include things such as cuisine, number of steps, recipe time, and health information. The ratings column contains numerical data that represent each user’s rating of a certain recipe, and the possible values for ratings are 1-5. We used the recipe ID column to group the data frame and find the average rating for each recipe, which was information that we added as a new ‘Average Rating’ column. We used the original tags column to find out which recipes were Indian and Italian, which was also information added to our existing data frame as a new ‘Cuisine’ column. We then continued the rest of our analysis using the ‘Cuisine’ and ‘Average Rating’ columns to conduct our hypothesis testing and other forms of analysis to approach our main question. 

---

## Cleaning and EDA

<iframe src="assets/10-80-enrollment.html" width=800 height=600 frameBorder=0></iframe>

---

## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |

---

## Hypothesis Testing

The main question that we wanted to approach with our hypothesis testing was: Are Italian Recipes rated higher than Indian Recipes? The method we chose for investigating was permutation testing, as we were dealing with figuring out whether two samples, in this case Indian recipes and Italian recipes, come from the same distribution. Our approach involved shuffling group labels under the null in attempts to reject the null hypothesis. 

We built a function has_tag() which takes in a dataframe and a tag, and returns a boolean series based upon whether each recipe has the desired tag. We used this as a mask to extract the desired rows of our dataframe, which in this case were the rows that had ‘Indian’ or ‘Italian’ in the tags column, and created a cuisine column that had three values: ‘Indian’, ‘Italian’, and ‘NaN’ (if it was neither). We dropped the null values in order to only deal with the relevant data, and then ran our permutation test by shuffling the cuisine labels and recalculating the total average rating for Indian and Italian recipes. 

The test statistic that we chose was the difference in group means, as our question attempts to explore if a certain cuisine is rated higher on average than another, and we believe that finding the difference in group means was the most appropriate statistic to calculate in this scenario. Our observed statistic showed that the average rating for Italian recipes were higher than Indian. The significance level we chose was alpha = 0.05. After running our permutation test 500 times, we got a p-value of 0.056, which is greater than our significance level, meaning that we failed to reject the null hypothesis. That means that in terms of our permutation test, we cannot determine whether Indian and Italian recipes are from different populations. 


---