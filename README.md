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

The recipes were merged on `recipe_id`, and I used the rating's average. Before the merge, I replaced 0s in the rating with NaN values, as they were identified as missing values and would affect the mean values (lower them).

## Data Cleaning and Exploratory Data Analysis
