### /* QUESTION 1. HOw many films in inventory? */
SELECT COUNT(*)
FROM film;

### /* QUESTION 2. What does a sample output of the films tables look like? */

SELECT * FROM film
LIMIT 5;

### /* QUESTION 3. What films are longer than three hours? Order the output */
/* by title in reverse alphabetical order */

SELECT title, length
FROM film
WHERE length > 180
ORDER BY title DESC;

### /* QUESTION 4. What films are longer than three hours AND */
/* have a rental duration of a week ordered by rating? */

SELECT title, rental_duration, length
FROM film
WHERE length > 180 AND rental_duration = 7
ORDER BY rating;

### /* QUESTION 5. What are the max and min rental rates of the movies in inventory? */

SELECT MAX(rental_rate) AS max_rate, MIN(rental_rate) AS min_rate
FROM film;

### /* QUESTION 6. What is the average rental rate? */

SELECT ROUND(AVG(rental_rate), 2)
FROM film;

### /* QUESTION 7. Find the range of dates in the payment table. */

SELECT MIN(payment_date), MAX(payment_date)
FROM payment;

### /* QUESTION 8. What customers made a payment in May? Order by payment date. */

SELECT customer_id AS id, CONCAT(last_name, first_name) AS customer, 
payment_date
FROM customer c
INNER JOIN payment p
ON c.customer_id = p.customer_id
WHERE EXTRACT (MONTH FROM payment_date) = 5
ORDER BY payment_date;

### /* QUESTION 9. What is the average payment by customer? 
Display results by descending amount */

SELECT c.customer_id, CONCAT(last_name, first_name) AS customer_name, ROUND(AVG(amount), 2) AS avg_amount
FROM customer c
LEFT JOIN payment p
ON c.customer_id = p.customer_id
GROUP BY c.customer_id, customer_name
ORDER BY avg_amount DESC;

