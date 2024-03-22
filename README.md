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

```html
<iframe
  src="ratings_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
```

### Bivariate Analysis



### Interesting Aggregates



## Assessment of Missingness

### NMAR Analysis



### Missingness Dependency



## Hypothesis Testing



## Framing a Prediction Problem



## Baseline Model



## Final Model



## Fairness Analysis



