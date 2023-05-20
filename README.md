


# Recipe Ratings and Analysis

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

print(recipe.to_markdown())

```

|   recipe_id | name                                 |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                                                                                               |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fat (PDV) |   carbohydrates (PDV) |   avg rating |
|------------:|:-------------------------------------|----------:|-----------------:|:--------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|-------------:|
|      333281 | 1 brownies in the world    best ever |        40 |           985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |          138.4 |                10 |            50 |              3 |               3 |                    19 |                     6 |            4 |
|      453467 | 1 in canada chocolate chip cookies   |        45 |          1848091 | 2011-04-11 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |          595.1 |                46 |           211 |             22 |              13 |                    51 |                    26 |            5 |
|      306168 | 412 broccoli casserole               |        40 |            50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |            5 |
|      286009 | millionaire pound cake               |       120 |           461724 | 2008-02-12 00:00:00 | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |          878.3 |                63 |           326 |             13 |              20 |                   123 |                    39 |            5 |
|      475785 | 2000 meatloaf                        |        90 |          2202916 | 2012-03-06 00:00:00 | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             |        17 | ['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |          267   |                30 |            12 |             12 |              29 |                    48 |                     2 |            5 |



### Univariate Analysis

In the plot below, we are observing the distribution of average ratings across all recipes in our dataset. We can see a trend of increased amount of ratings for high rating values (ratings are on a scale of 1 to 5), and we can see the most common rating by far is 5, followed by 4, and decreasing after. 

<iframe src="assets/RatingDistribution.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis

In the plot below, we are observing the distribution of average rating of recipes based on cuisine - Indian or Italian. It is visible that the ratings of the two cuisine follow a similar pattern, where there is a trend of higher proportion of ratings for high rating values (ratings are on a scale of 1 to 5), and we can see the most common ratings for both cuisines lie close 5.  

<iframe src="assets/ratingByCuisine.html" width=800 height=600 frameBorder=0></iframe>


### Interesting Aggregates 

Pivot Table #1 

In the table below, we are observing the distribution of ratings for each cuisine depending on the caloric amount of each recipe. We have binned the calories column to observe the differences in rating between different ranges of caloric value. As our main question explores the relationship between Indian and Italian recipes and their average ratings, this aggregation is signficant as we are analyzing different factors and contributors to differences in ratings between the recipes of the two cuisines. Here we are observing if the relationship between amount of calories in a recipe and average ratings grouped by cuisine to see if caloric amount impacts rating values between our cuisines of focus. For Indian cuisine, we can see that recipes that are on really high or low end of the calorie spectrum tend to be rated slightly higher than those in the middle. We did not observe anything too significant in regards to patterns in the Italian cuisine row. 

```py

print(pivot1.to_markdown())

```

| cuisine   |   (-0.001, 146.5] |   (146.5, 248.9] |   (248.9, 370.6] |   (370.6, 563.3] |   (563.3, 45609.0] |
|:----------|------------------:|-----------------:|-----------------:|-----------------:|-------------------:|
| indian    |           4.64254 |          4.52866 |          4.59874 |           4.6155 |            4.70294 |
| italian   |           4.67562 |          4.6511  |          4.65472 |           4.65   |            4.65549 |


Pivot Table #2

In the table below, we are observing the distribution of ratings for each cuisine depending on number for ingredients for each recipe. We have binned the n_ingredients column to observe the differences in rating between different ranges of ingredient amount. As our main question explores the relationship between Indian and Italian recipes and their average ratings, this aggregation is signficant as we are analyzing different factors and contributors to differences in ratings between the recipes of the two cuisines. Here we are observing if the relationship between amount of ingredients in a recipe and average ratings grouped by cuisine to see if ingredient amount impacts rating values between our cuisines of focus. For Indian cuisine, we can see that there s a slight decrease in rating as number of ingredients increase, however, this is variable and not constantly decreasing, so we did not observe any significant trend or pattern. None was observed for Italian cuisine either. 


```py

print(pivot2.to_markdown())

```

| cuisine   |   (0.999, 6.0] |   (6.0, 8.0] |   (8.0, 10.0] |   (10.0, 12.0] |   (12.0, 37.0] |
|:----------|---------------:|-------------:|--------------:|---------------:|---------------:|
| indian    |        4.65803 |      4.68053 |       4.59473 |        4.61984 |        4.58681 |
| italian   |        4.68381 |      4.65686 |       4.63912 |        4.65186 |        4.6548  |


---

## Assessment of Missingness

### NMAR Analysis

The rating column is NMAR because sometimes people do not want to leave a rating. This means that the data itself is the reason for missingness - the people who are leaving the rating column blank simply do so because they have no rating to give. Additional data that might be helpful is the reviews column and also information directly from the reviews section of www.food.com, because we looked through the website and sometimes the ratings that are missing are associated with reviews that are questions or remarks. Therefore, they are not actual reviews of someone who tried the recipe, meaning that they would not even be able to have a valid review. This can make the missingness in the ratings column MAR because the missingness can be dependent on the reviews column. The value in the review column can impact the missingness in the rating column, because if the review is a question and remark instead of a rating based review, then the corresponding value in the rating column may be missing. 

### Missingness Dependency 

<iframe src="assets/ks_ingredients.html" width=800 height=600 frameBorder=0></iframe>


<iframe src="assets/diff_mean_ingredients.html" width=800 height=600 frameBorder=0></iframe>


---

## Hypothesis Testing

### Permutation Test Key Info:

Main Question: What is the relationship between Indian and Italian cuisine and average rating of their respective recipes? *Specifically for this permutation test, we used a more specific question: Are Italian Recipes on average rated higher than Indian Recipes?

Null Hypothesis: In the population,ratings of Italian recipes and indian recipes have the same distribution, and the observed differences in our samples are due to random chance.

Alternative hypotheses: In the population, italian recipes have higher ratings than indian recipes, on average. The observed difference in our samples cannot be explained by random chance alone.

Choice of test statistic: Difference in group means

Choice of significance level: alpha = 0.01 

Resulting p-value: 0.0413



### Process Details & Findings 

The main question that we explored throughout our project was: What is the relationship between Indian and Italian cuisine and average rating of their respective recipes? 

However, when it came to conducting our permutation test, we wanted to be very specific, so we went with an even more precise question: Are Italian Recipes on average rated higher than Indian Recipes? We chose to do this as we believd that while our main question was very important in all of exploratory analysis we did, we wanted to study a specific instance that was encompassed within our main question. While our main question studies the relationship between the recipes of two popular cuisinses and their ratings, our hypothesis test is based upon our observed statistic, which is that Italian recipes are rated higher than Indian recipes. We wanted to explore this phenomenon further, which is why we based our hypothesis test off of a specific instance in the relationship between the average ratings of Indian and Italian cuisine. 

The method we chose for investigating was permutation testing, as we were dealing with figuring out whether two samples, in this case Indian recipes and Italian recipes, come from the same distribution. Our approach involved shuffling group labels under the null in attempts to reject the null hypothesis. 

We built a function has_tag() which takes in a dataframe and a tag, and returns a boolean series based upon whether each recipe has the desired tag. We used this as a mask to extract the desired rows of our dataframe, which in this case were the rows that had ‘Indian’ or ‘Italian’ in the tags column, and created a cuisine column that had three values: ‘Indian’, ‘Italian’, and ‘NaN’ (if it was neither). We dropped the null values in order to only deal with the relevant data, and then ran our permutation test by shuffling the cuisine labels and recalculating the total average rating for Indian and Italian recipes. 

The test statistic that we chose was the difference in group means, as our question attempts to explore if a certain cuisine is rated higher on average than another, and we believe that finding the difference in group means was the most appropriate statistic to calculate in this scenario. Our observed statistic showed that the average rating for Italian recipes were higher than Indian. The significance level we chose was alpha = 0.01. We opted for a signficance level of 0.01 rather 0.05 because we wanted to reduce the likelihood of false positives, which occur with more frequency the larger the signficance level is. After running our permutation test 1500 times, we got a p-value of 0.0413, which is greater than our significance level, meaning that we failed to reject the null hypothesis. That means that in terms of and based on our permutation test, we cannot determine whether Indian and Italian recipes are from different populations. 


<iframe src="assets/permutationplot.html" width=800 height=600 frameBorder=0></iframe>


---
