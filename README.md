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


| name                                 |     id |   minutes |   contributor_id | submitted   |   n_steps | description                                                                                                                                                                                                                                                                                                                                                                       |   n_ingredients |   recipe_id |   rating |   calories |   fat |   sugar |   sodium |   protein |   sat_fat |   carbohydrates | preparation_time   | n_ingredients_cat   |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|------------:|---------:|-----------:|------:|--------:|---------:|----------:|----------:|----------------:|:-------------------|:--------------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  |        10 | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              |               9 |      333281 |        4 |      138.4 |    10 |      50 |        3 |         3 |        19 |               6 | Medium             | (0, 10]             |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  |        12 | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            |              11 |      453467 |        5 |      595.1 |    46 |     211 |       22 |        13 |        51 |              26 | Medium             | (10, 20]            |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |               9 |      306168 |        5 |      194.8 |    20 |       6 |       32 |        22 |        36 |               3 | Medium             | (0, 10]             |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  |         7 | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                |               7 |      286009 |        5 |      878.3 |    63 |     326 |       13 |        20 |       123 |              39 | Long               | (0, 10]             |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  |        17 | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         |              13 |      475785 |        5 |      267   |    30 |      12 |       12 |        29 |        48 |               2 | Long               | (10, 20]            |


### Univariate Analysis



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



