Pagila Example Queries
====

### These questions were sourced from here: 
[Course Hero](https://www.coursehero.com/file/77271391/Lab06-Abdullah-Shafqat-291276docx/) 

and here: 

[Chegg](https://www.chegg.com/homework-help/questions-and-answers/following-questions-help-practice-writing-sql-statements-questions-based-sakila-database-s-q30255475)

and here:

[Jooq](https://www.jooq.org/sakila)

---

1. Retrieve names of movies starting with P.

```

```
2. Which movies were released in year 2006

```

```
3. What password did the DBA assign to the user 'MIKE'?
```

```
4. Retrieve data of all actors whose names are not ending on T. 

```

```
5. List one or more languages in which any movie is available.

```

```
6. Find and display income(payments) generated during August 2005. Sort them in descending order.  

```

```
7.What category does the movie ADAPTATION HOLES belong to? 

```

```
8. Retrieve first and last name of actors who played in ALONE TRIP. 

```

```
9. list all of the actors names sorted by last name, then by first name without using the wildcard * for the fields. 

```

```
10. list all of the films that are category "Action" and include the record count with using the wildcard for the fields. 

```

```
11. list all of the films that are rated 'R' and include the record count without using the wildcard * for the fields. 

```

```
12. list all of the films that have the string "SIDE" in their name and include the record count without using the wildcard for the fields. 

```

```
13. Provide just the count of films under 90 minutes and include the record count and the film count without using the wildcard for the fields.  

```

```

14. Find the actor with the most films.  

```
SELECT first_name, last_name, COUNT(*) films
FROM actor AS a
JOIN film_actor AS fa USING (actor_id)
GROUP BY actor_id, first_name, last_name
ORDER BY films DESC
LIMIT 1;
```

15. Find the cumulative revenue for all store

```
SELECT payment_date, amount, SUM(amount) OVER (ORDER BY payment_date)
FROM (
    SELECT CAST(payment_date AS DATE) AS payment_date, SUM(amount) AS amount
    FROM payment
    GROUP BY CAST(payment_date AS DATE)
) p
ORDER BY payment_date;


 
```