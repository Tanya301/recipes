# Recipes Research Project
by Tatiana Samokhvalova

_This project was created as an assignment for UCSD's DSC 80 class in Winter 2024._

## Introduction

In this project, I dive into an extensive dataset comprising detailed information on a wide variety of recipes and user interactions with these recipes. This dataset contains a variety of factors such as preparation time, nutritional values, step-by-step instructions, user reviews, and other. My investigation centeres around the relationship between the recipes' different features and their preparation times.

The 2 datasets I merged were `interactions` and `recipes`. The interactions dataset contains the user' reviews of different recipes and has 731927 rows. The recipes dataset contains information about different recipes and consists of 83782 rows. Here are the columns of both datasets:

### interactions
- `user_id`: id of the user who submitted a review.
- `recipe_id`: recipes's id (was used to merge the two datasets).
- `date`: the date on which the review was submitted.
- `rating`: the rating that was given to a recipe.
- `review`: text review of a recipe.

### recipes
- `id`: recipe's id.
- `minutes`: how long a recipe takes to make (recipe's preparation time).
- `contributor_id`: the id of the person who submitted the recipe.
- `submitted`: the date when the recipe was submitted.
- `tags`: different tags associated with a recipe.
- `steps`: the recipe's steps.
- `nutrition`: recipe's nutritional values.
- `n_steps`: the number of steps in the recipe.
- `description`: the recipe's text description.
- `ingredients`: the ingredients required for the recipe.
- `n_ingredients`: the number of ingredients.

As my goal was to predict recipes prepaation time, the relevant columns here would be `minutes`, `n_steps`, `n_ingredients`, and possibly description and some nutritional values.

## Data Cleaning and Exploratory Data Analysis

### Data cleaning

First, as mentioned earlier, I replaced 0s in the `rating` column (before merging). I have come to that decision after seeing several positive reviews, or just questions and comments where the rating was 0. Hence, the value is not actually 0 and is in fact a missing value.

The recipes were merged on `recipe_id`, and I used the rating's average. Before the merge, I replaced 0s in the rating with NaN values, as they were identified as missing values and would affect the mean values (lower them). Furthermore, after merging I rounded the ratings to the nearest 0.5 so the variable would be categorical ordinal rather than continuous.

Then, I separated the column `nutrition` into 7 columns (`calories`, `fat`, `sugar`, `sodium`, `protein`, `sat_fat`, `carbohydrates`) for further analysis.

As a last step in this section, I dropped the following columns: `nutrition` (as it was transformed and the column itself became redundant), `steps`, `ingredients`, and `tags` (as I was not intending to use those columns for my analysis).
* The columns `steps` and `indredients` are a free-form description of what a recipe is, and would not be useful for the model I planned on building.
* As for the column `tags`, I did not consider it to be useful for the overall analysis, and as my model's goal was predicting how long a meal would take to cook, it seemed unreasonable to use tags for it (as they appear on the recipe after it has been added to the website and are most likely the last thing to be added to a recipe).

This is what my dataframe looked after cleaning (only some columns are shown for easier reading):

|     id |   minutes | description                                                                                                                                                                                                                                                                                                                                                                       |   n_steps |   n_ingredients |   calories |
|-------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|----------------:|-----------:|
| 333281 |        40 | these are the most; chocolatey, moist...                                                                                                              |        10 |               9 |      138.4 |
| 453467 |        45 | this is the recipe that we use at my...                                                                                                                                         |        12 |              11 |      595.1 |
| 306168 |        40 | since there are already 411 recipes... |         6 |               9 |      194.8 |
| 286009 |       120 | why a millionaire pound cake? ...                                                                                                                                                                |         7 |               7 |      878.3 |
| 475785 |        90 | ready, set, cook! special ...                                                                                                                                                                         |        17 |              13 |      267   |

### Univariate Analysis

I performed a univariate analysis on the `rating` column (that contained recipes' average ratings), and found that the ratings in the dataframe are heavily skewed. This means that the feature would be useless for analysis or making of the prediction model.

<iframe
  src="ratings_plot.html"
  width="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

I examined the relationship between the recipe's number of ingredients and its calories. I found it interesting that at first, as expected, the amount of calories rises with the number of ingridients. However, for larger quantities of ingridients the amount of calories becomes lower on average.

<iframe
  src="ingr-calories-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates

|   Short |   Medium |     Long |   Very long |
|--------:|---------:|---------:|------------:|
| 329.896 |  413.557 |  493.387 |     567.763 |
| 420.423 |  486.817 |  609.569 |     682.428 |
| 563.026 |  666.303 |  735.745 |    2472.27  |
| nan     |  670.275 | 2180.86  |     559     |

This is a pivot table containing number of ingredients againt preparation times, with mean calories as values. However, first I will put n_ingredients into bins, as number of ingredients goes all the way up to 35. The table suggests calorie count rises with more ingredients but varies by preparation time; 'Very long' prep often has fewer calories, but that could also be attributed to sample size.

## Assessment of Missingness

In the dataset, 3 columns showed missing data: `name` (MCAR), `description` (MAR), and `rating` (NMAR).

### NMAR Analysis

The `rating` column's missing mechanism is most likely NMAR, as people subjectively chose not to rate a recipe for different reasons: for example, when they want to ask a question or make a general comment without giving a recipe a grade. Some data that could be used as a confirmation here would be for example semantically analyzing people's reviews.

### Missingness Dependency

I have noticed that descriptions tend to be missing when recipes are simpler. So, `description`'s missingness could be MAR-dependent on the column `n-ingredients`. I performed a permutation test and confirmed the dependency.

|   n_ingredients_cat |
|--------------------:|
|                  58 |
|                  12 |
|                   0 |
|                   0 |

## Hypothesis Testing

The question explored: **Is there a strong correlation between the recipe's number of steps and its number of ingredients?**

Null hypothesis: There is no relationship between n_steps and n_ingredients in the recipes.

Alternative hypothesis: There is a relationship between the number of calories and the amount of protein in the recipes.

Test stat: correlation between `n_steps` and `n_ingredients`.

After performing the test, with p-value < 0.05, I rejected the null hypothesis in facor of the alternative: there most likely is a correlation between a recipe's number of steps and its number of ingredients.

## Framing a Prediction Problem

My prediction problem is to predict what preparation time category a recipe falls into ('Short', 'Medium', 'Long', 'Very long'). This is a multiclass classification problem. The features considered included mainly `n_steps`, `n_ingredients` or `n_ingredients_cat`, with the addition of `calories` and `description`s' containing certain keywords (such as 'quick'). The response variable is `preparation_time` (a categorical variable created from `minutes`). The metric used to validate the model is accuracy.

The features described are reasonable to have at the time of prediction, as I want to predict how long the recipe would take when it's already created, while such features as `tags` as most likely to be created after people have already cooked the recipes, hence the preparation time is already known.

## Baseline Model



## Final Model



## Fairness Analysis

As the model is still performing poorly, I consider it pointless to perform fairness analysis as of this moment. However, in the next steps of my project, I will consider seeing how fair the model predicts preparation times for recipes from different decades, and how fair it performs on recipes with different nurtitional values.

