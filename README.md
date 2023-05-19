


# Recipe Ratings

by Antara Sengupta (asengupt@ucsd.edu) and George Chong (gchong@ucsd.edu)

---

## Introduction

Main Question: What is the relationship between Indian and Italian cuisine and average rating of their respective recipes?

The dataset that we are working with in this project is the Recipe and Ratings set. We have two sets of data that we are dealing with, recipes and ratings. The recipe data has information regarding recipes and has columns regarding nutritional content, steps & time, contributor identification, along with tags and descriptions. The recipe dataset has 83,782 observations, or rows. The ratings data has information regarding reviews and ratings of the recipes from the recipe dataset. The ratings dataset has 731,927 observations, or rows. To start off our project, we merged these two datasets on their common shared column of recipe ID, and then proceeded with all other analysis on this merged data frame. All this data has been made available by scraping www.food.com, which contains the recipes and ratings. 

For this specific project, our main question is: What is the relationship between Indian and Italian cuisine and the average rating of their respective recipes? This question compares the average ratings of the two most popular and common cuisines that have recipes at www.food.com. We found that this would be relevant and important information for visitors of this website as it provides insight into which popular cuisine has better recipes, based on user reviews. The columns that we found relevant to our analysis and question are the recipe ID, tags and ratings columns. The recipe ID column has a string value of numbers that are unique to each recipe. The tags column has a list of strings that are associated with the specific recipe, which include things such as cuisine, number of steps, recipe time, and health information. The ratings column contains numerical data that represent each user’s rating of a certain recipe, and the possible values for ratings are 1-5. We used the recipe ID column to group the data frame and find the average rating for each recipe, which was information that we added as a new ‘Average Rating’ column. We used the original tags column to find out which recipes were Indian and Italian, which was also information added to our existing data frame as a new ‘Cuisine’ column. We then continued the rest of our analysis using the ‘Cuisine’ and ‘Average Rating’ columns to conduct our hypothesis testing and other forms of analysis to approach our main question. 

---

## Cleaning and EDA

### Data Cleaning 

The data we worked with were given to us in two separate datasets, recipe data and ratings data, as detailed in the previous section. We created a few functions to clean our data. To clean our ratings (interaction) data, we created the clean_interaction() function, which took in the data frame and changed all 0 ratings to NaN values, as the ratings are only meant to be between 1 and 5. Secondly, we changed all the type of all the values in the 'date' column to date time. To clean our recipe data, we created the function clean_recipe(), which renamed the 'id' column to 'recipe_id' for the sake of specificity and also to help us merge it with the interaction dataset in future steps - we also indexed the data frame by this column for the same reason. We also expanded the nutrition column to various different columns (one for each nutritional aspect), in order for us to do further analysis on different nutritional features and their relationships with other features, and also the distribution of them throughout the data. We also dropped the pre-existing nutrition column. We converted the type of values in 'submitted' column to date time. Lastly, we merged the two data frames with our function recipe_with_rating() which merged the two data frames on the recipe id column. We then grouped the data frame by recipe id and added an average rating column which holds the values of average rating for each recipe. 

```py
markdown_table = recipe.head().to_markdown(index=False)
print(markdown_table)
```



### Univariate Analysis

### Bivariate Analysis

### Interesting Aggregates 

---

## Assessment of Missingness

### NMAR Analysis

The rating column is NMAR because sometimes people do not want to leave a rating. This means that the data itself is the reason for missingness - the people who are leaving the rating column blank simply do so because they have no rating to give. Additional data that might be helpful is the reviews column and also information directly from the reviews section of www.food.com, because we looked through the website and sometimes the ratings that are missing are associated with reviews that are questions or remarks. Therefore, they are not actual reviews of someone who tried the recipe, meaning that they would not even be able to have a valid review. This can make the missingness in the ratings column MAR because the missingness can be dependent on the reviews column. The value in the review column can impact the missingness in the rating column, because if the review is a question and remark instead of a rating based review, then the corresponding value in the rating column may be missing. 

### Missingness Dependency 


---

## Hypothesis Testing

The main question that we wanted to approach with our hypothesis testing was: Are Italian Recipes rated higher than Indian Recipes? The method we chose for investigating was permutation testing, as we were dealing with figuring out whether two samples, in this case Indian recipes and Italian recipes, come from the same distribution. Our approach involved shuffling group labels under the null in attempts to reject the null hypothesis. 

We built a function has_tag() which takes in a dataframe and a tag, and returns a boolean series based upon whether each recipe has the desired tag. We used this as a mask to extract the desired rows of our dataframe, which in this case were the rows that had ‘Indian’ or ‘Italian’ in the tags column, and created a cuisine column that had three values: ‘Indian’, ‘Italian’, and ‘NaN’ (if it was neither). We dropped the null values in order to only deal with the relevant data, and then ran our permutation test by shuffling the cuisine labels and recalculating the total average rating for Indian and Italian recipes. 

The test statistic that we chose was the difference in group means, as our question attempts to explore if a certain cuisine is rated higher on average than another, and we believe that finding the difference in group means was the most appropriate statistic to calculate in this scenario. Our observed statistic showed that the average rating for Italian recipes were higher than Indian. The significance level we chose was alpha = 0.01. After running our permutation test 1500 times, we got a p-value of 0.0413, which is greater than our significance level, meaning that we failed to reject the null hypothesis. That means that in terms of our permutation test, we cannot determine whether Indian and Italian recipes are from different populations. 


---
