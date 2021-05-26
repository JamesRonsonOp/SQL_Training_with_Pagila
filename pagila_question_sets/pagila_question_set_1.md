### This notebook is from [Harmony Ausiello's Github](https://github.com/hpausiello/SQL-pagila-queries)

Pagila Example Queries
====

#### To create the pagila database needed to run these sample queries open psql in the directory the pagila data files have been saved in and run these commands in this order:

#### \i pagila-schema.sql 
#### \i pagila-data.sql
#### \i pagila-insert-data.sql

---

1a. You need a list of all the actors’ first name and last name

```
SELECT first_name,
         last_name
FROM actor; 
```


1b. Display the first and last name of each actor in a single column in upper case letters. Name the column Actor Name

```
SELECT first_name ||' '|| last_name AS Actor_Name
FROM actor;
```


2a. You need to find the id, first name, and last name of an actor of whom you know only the first name of "Joe." What is one query would you use to obtain this information?

```
SELECT actor_id,
         first_name,
         last_name
FROM actor
WHERE first_name LIKE 'JOE';
```


2b. Find all actors whose last name contain the letters GEN. Make this case insensitive

##### gives all actors who has a G, E or N anywhere in their last name

```
SELECT *
FROM actor
WHERE last_name similar to '%[GEN]%';
```

##### gives all actors who have the letters "GEN" appear consecutively in their last name (case insensitive)

```
SELECT *
FROM actor
WHERE last_name ilike '%GEN%';
```


2c. Find all actors whose last names contain the letters LI. This time, order the rows by last name and first name, in that order. Make this case insensitive.

```
SELECT *
FROM actor
WHERE last_name ilike '%LI%'
ORDER BY  last_name, first_name;
```


2d. Using IN, display the country_id and country columns of the following countries: Afghanistan, Bangladesh, and China:

```
SELECT country_id,
         country
FROM country
WHERE country IN ('Afghanistan', 'Bangladesh', 'China');
```


3a. Add a middle_name column to the table actor. Specify the appropriate column type

```
ALTER TABLE actor ADD COLUMN middle_name VARCHAR(255);
```


3b. You realize that some of these actors have tremendously long last names. Change the data type of the middle_name column to something that can hold more than varchar.

```
ALTER TABLE actor ALTER COLUMN middle_name TYPE TEXT;
```

##### check data types of each column
```
SELECT column_name,
        data_type
FROM information_schema.columns
WHERE table_name = 'actor';
```


3c. Now write a query that would remove the middle_name column.

```
ALTER TABLE actor DROP COLUMN middle_name;
```


4a. List the last names of actors, as well as how many actors have that last name.

```
SELECT last_name,
         count(last_name)
FROM actor
GROUP BY  last_name;
```


4b. List last names of actors and the number of actors who have that last name, but only for names that are shared by at least two actors

```
SELECT last_name,
         count(last_name)
FROM actor
GROUP BY  last_name
HAVING count(last_name) > 1;
```


4c. Oh, no! The actor HARPO WILLIAMS was accidentally entered in the actor table as GROUCHO WILLIAMS. Write a query to fix the record.

```
UPDATE actor SET first_name = 'HARPO'
WHERE first_name = 'GROUCHO';
```

##### to check
```
SELECT first_name,
         last_name
FROM actor
WHERE first_name LIKE 'HARPO';
```


4d. Perhaps we were too hasty in changing GROUCHO to HARPO. It turns out that GROUCHO was the correct name after all! In a single query, if the first name of the actor is currently HARPO, change it to GROUCHO. Otherwise, change the first name to MUCHO GROUCHO, as that is exactly what the actor will be with the grievous error. BE CAREFUL NOT TO CHANGE THE FIRST NAME OF EVERY ACTOR TO MUCHO GROUCHO(Hint: update the record using a unique identifier.)

```
UPDATE actor SET first_name =
    CASE
    WHEN first_name = 'HARPO' THEN
    'GROUCHO'
    WHEN first_name = 'GROUCHO' THEN
    'MUCHO GROUCHO'
    ELSE first_name
    END
WHERE actor_id = 172;
```

##### to find unique identifier, actor_id
```
SELECT actor_id
FROM actor
WHERE first_name = 'HARPO'
        AND last_name = 'WILLIAMS';
```


5a. You’re answering each of these questions. Please include examples and answer them in plain english. 


#### What’s the difference between a left join and a right join. 

##### When joining two tables, a left join takes the first (left) table and adds the matching records from the second (right) table.  Similarly, a right join is taking the right (second) table and adds the matching records from the first (left) table. Example:
```
SELECT *
FROM left_table l
LEFT JOIN right_table r
    ON l.column = r.column;
```

```
SELECT *
FROM left_table l
RIGHT JOIN right_table r
    ON l.column = r.column;
```


#### What about an inner join and an outer join? 

##### When joining two tables, an inner join creates a new table with only the matching records from both tables, while an outer join creates a new table with all the records from both tables. Example:
```
SELECT *
FROM left_table l
INNER JOIN right_table r
    ON l.column = r.column;
```

```
SELECT *
FROM left_table l 
FULL OUTER JOIN right_table r
    ON l.column = r.column;
```


#### When would you use rank? 

##### Rank would be used when looking for which row a new value starts in a column. The rank of a value shows which row it first appears in a column, so when there are repeat values, ranks will not be consecutive integers. Example:
```
SELECT column 
rank() over (ORDER BY column DESC) AS Rank
FROM table;
```


#### What about dense_rank? 

##### Dense rank would be used when looking for the consecutive order of values in a column. The dense rank of a value shows exactly where a value is with respect to the other values in the column.  So, even if there are repeat values, the dense ranks will be consecutive integers. Example:
```
SELECT column 
dense_rank() over (ORDER BY column DESC) AS Dense_Rank
FROM table;
```


#### When would you use a subquery in a select? 

##### A subquery is useful to filter data further than accessible in a single query, usually when pulling data from multiple tables.  The subquery filters the data that the outer select statement will query from. Example:
```
SELECT first_column
FROM table
WHERE second_column IN 
    (SELECT second_column
    FROM other_table
    WHERE third_column = 'some_value');
```


#### When would you use a right join?

##### A right join would be used when the entire second (right) table records are needed, but only the matching records from the first (left) table are needed. Example:
```
SELECT *
FROM left_table l
RIGHT JOIN right_table r
    ON l.column = r.column;
```


#### When would you use an inner join over an outer join?

##### Using an inner join instead of an outer join is applicable when only matching records from two tables are needed.  The inner join will give much less data than an outer join. Example:
```
SELECT *
FROM left_table l
INNER JOIN right_table r
    ON l.column = r.column;
```


#### What’s the difference between a left outer and a left join?

##### Nothing.  A left join can also be written as a left outer join. Example:
```
SELECT *
FROM left_table l
LEFT JOIN right_table r
    ON l.column = r.column;
```

```
SELECT *
FROM left_table l
LEFT OUTER JOIN right_table r
    ON l.column = r.column;
```


#### When would you use a group by?

##### When using an aggregate in your query (e.g. MIN, MAX, SUM, AVE, or COUNT), you can use GROUP BY to aggregate a column with respect to another column instead of simply aggregating only a single column. Example:
```
SELECT column_one,
         SUM(column_two)
FROM table_name
GROUP BY  column_one;
```


#### Describe how you would do data reformatting.

##### Use the FORMAT function to change how the data of a column is displayed. Example:
```
SELECT FORMAT(column_name,format) FROM table_name;
```


#### When would you use a with clause?

##### A WITH clause would be used to define a subquery (temporary table) that can be referred to in the same query.  It is used to simplify complicated queries. Example:
```
WITH subquery_alias AS 
    (some complicated SELECT query)
SELECT some_column 
FROM subquery_alias;
```


6a. Use a JOIN to display the first and last names, as well as the address, of each staff member. Use the tables staff and address:

```
SELECT s.first_name,
         s.last_name,
         a.address
FROM staff s
LEFT JOIN address a
    ON s.address_id = a.address_id;
```


6b. Use a JOIN to display the total amount rung up by each staff member in January of 2007. Use tables staff and payment.

```
SELECT p.staff_id,
         COUNT(p.amount)
FROM payment p
LEFT JOIN staff s
    ON p.staff_id = s.staff_id
GROUP BY  p.staff_id;
```


6c. List each film and the number of actors who are listed for that film. Use tables film_actor and film. Use inner join.

```
SELECT f.title,
         COUNT(fa.actor_id) AS number_of_actors
FROM film f
INNER JOIN film_actor fa
    ON f.film_id = fa.film_id
GROUP BY  f.title;
```

6d. How many copies of the film Hunchback Impossible exist in the inventory system?

```
SELECT f.title,
         count(i.inventory_id) AS number_of_copies
FROM film f
JOIN inventory i
    ON f.film_id = i.film_id
WHERE f.title = 'HUNCHBACK IMPOSSIBLE'
GROUP BY  f.title;
```

6e. Using the tables payment and customer and the JOIN command, list the total paid by each customer. List the customers alphabetically by last name:

```
SELECT c.last_name,
         COUNT(p.amount) AS amount
FROM customer c
LEFT JOIN payment p
    ON c.customer_id = p.customer_id
GROUP BY  c.last_name
ORDER BY  c.last_name ASC;
```


7a. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, films starting with the letters K and Q have also soared in popularity. display the titles of movies starting with the letters K and Q whose language is English.

```
SELECT title
FROM film
WHERE language_id = 1
        AND title LIKE 'K%'
        OR title LIKE 'Q%';
```


7b. Use subqueries to display all actors who appear in the film Alone Trip.

```SELECT s.last_name,
         s.first_name
FROM 
    (SELECT a.first_name,
         a.last_name,
         f.title
    FROM actor a
    JOIN film_actor fa
        ON a.actor_id = fa.actor_id
    JOIN film f
        ON f.film_id = fa.film_id
    WHERE title = 'ALONE TRIP' ) s
GROUP BY s.first_name, s.last_name
ORDER BY  s.last_name ASC;
```


7c. You want to run an email marketing campaign in Canada, for which you will need the names and email addresses of all Canadian customers. Use joins to retrieve this information.

```
SELECT c.last_name,
         c.first_name,
         c.email
FROM customer c
JOIN address a
    ON c.address_id = a.address_id
JOIN city ci
    ON a.city_id = ci.city_id
JOIN country co
    ON ci.country_id = co.country_id
WHERE country = 'Canada'
ORDER BY  last_name ASC;
```


7d. Sales have been lagging among young families, and you wish to target all family movies for a promotion. Identify all movies categorized as a family film. Now we mentioned family film, but there is no family film category. There’s a category that resembles that. In the real world nothing will be exact.

```
SELECT title
FROM film f
JOIN film_category fc
    ON f.film_id = fc.film_id
JOIN category c
    ON fc.category_id = c.category_id
WHERE c.category_id = 8;
```


7e. Display the most frequently rented movies in descending order.

```SELECT f.title,
         COUNT(r.inventory_id) AS rental_count
FROM film f
JOIN inventory i
    ON f.film_id = i.film_id
JOIN rental r
    ON i.inventory_id = r.inventory_id
GROUP BY  f.title
ORDER BY  rental_count DESC;
```


7f. Write a query to display how much business, in dollars, each store brought in.

```
SELECT str.store_id,
         SUM(p.amount) AS total_sales
FROM store str
JOIN staff stf
    ON str.store_id = stf.store_id
JOIN payment p
    ON stf.staff_id = p.staff_id
GROUP BY  str.store_id;
```


7g. Write a query to display for each store its store ID, city, and country.

```SELECT s.store_id,
         ci.city,
         co.country
FROM store s
JOIN address a
    ON s.address_id = a.address_id
JOIN city ci
    ON a.city_id = ci.city_id
JOIN country co
    ON ci.country_id = co.country_id;
```

7h. List the top five genres in gross revenue in descending order. 

```
SELECT c.name,
         SUM(p.amount) AS gross_revenue
FROM category c
JOIN film_category fc
    ON c.category_id = fc.category_id
JOIN inventory i
    ON fc.film_id = i.film_id
JOIN rental r
    ON i.inventory_id = r.inventory_id
JOIN payment p
    ON r.rental_id = p.rental_id
GROUP BY  c.name
ORDER BY  gross_revenue DESC limit 5;
```

8a. In your new role as an executive, you would like to have an easy way of viewing the Top five genres by gross revenue. Use the solution from the problem above to create a view. 

```
CREATE OR REPLACE VIEW top_five_grossing_genres AS
SELECT c.name,
         SUM(p.amount) AS gross_revenue
FROM category c
JOIN film_category fc
    ON c.category_id = fc.category_id
JOIN inventory i
    ON fc.film_id = i.film_id
JOIN rental r
    ON i.inventory_id = r.inventory_id
JOIN payment p
    ON r.rental_id = p.rental_id
GROUP BY  c.name
ORDER BY  gross_revenue DESC limit 5;
```


8b. How would you display the view that you created in 8a?

```
SELECT *
FROM top_five_grossing_genres;
```


8c. You find that you no longer need the view top_five_genres. Write a query to delete it.

```
DROP VIEW top_five_grossing_genres;
```

