# Recipe Ratings

by Antara Sengupta (asengupt@ucsd.edu) and George Chong (gchong@ucsd.edu)

---

## Introduction

The dataset that we are working with in this project is the Recipe and Ratings set. We have two sets of data that we are dealing with, recipes and ratings. The recipe data has information regarding recipes and has columns regarding nutritional content, steps & time, contributor identification, along with tags and descriptions. The recipe dataset has 83,782 observations, or rows. The ratings data has information regarding reviews and ratings of the recipes from the recipe dataset. The ratings dataset has 731,927 observations, or rows. To start off our project, we merged these two datasets on their common shared column of recipe ID, and then proceeded with all other analysis on this merged dataframe. All this data has been made available by scraping www.food.com, which contains the recipes and ratings. 
	
	For this specific project, our main question is: Are Italian recipes on average rated higher than Indian recipes? This question compares the average ratings of the two most popular and common cuisines that have recipes at www.food.com. We found that this would be relevant and important information for visitors of this website as it provides insight into which popular cuisine has better recipes, based on user reviews. The columns that we found relevant to our analysis and question are the recipe ID, tags and ratings columns. The recipe ID column has a string value of numbers that are unique to each recipe. The tags column has a list of strings that are associated with the specific recipe, which include things such as cuisine, number of steps, recipe time, and health information. The ratings column contains numerical data that represent each user’s rating of a certain recipe, and the possible values for ratings are 1-5. We used the recipe ID column to group the data frame and find the average rating for each recipe, which was information that we added as a new ‘Average Rating’ column. We used the original tags column to find out which recipes were Indian and Italian, which was also information added to our existing data frame as a new ‘Cuisine’ column. We then continued the rest of our analysis using the ‘Cuisine’ and ‘Average Rating’ columns to conduct our hypothesis testing and other forms of analysis to approach our main question. 
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


---