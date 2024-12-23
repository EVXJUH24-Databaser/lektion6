# Övningar vecka 2

## Övning 7 

users:
- id (PK)
- name
- email
- phone_number

goals:
- id (PK) -> index -> snabb sökning
- activity_id
- user_id
- threshold / minimum value / goal
- deadline_date

activities:
- id
- name (weight, run time, bench press)

fitness_values:
- activity_id
- value
- date
- user_id

## Övning 9 

recipes:
- id
- name
- recipe_category_id

ingredients:
- id
- name

recipe_ingredients:
- recipe_id
- ingredient_id
- ingredient_amount

recipe_categories:
- id
- name (frukost, lunch, middag m.m)

users:
- id
- name

recipe_comments:
- id
- user_id
- recipe_id
- content
- rating

favorite_recipes:
- user_id
- recipe_id

shopping_list:
- id
- title
- user_id
- recipe_id

shopping_list_items:
- shopping_list_id
- ingredient_id
- amount
