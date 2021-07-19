1. 

/* Retreive all actors with last names beginning with the letters A thru F. Order by Name alphabetically. */

SELECT * FROM actor
WHERE last_name SIMILAR TO '[A-F]%'
ORDER BY last_name;

/* This uses the SIMILAR TO statement along with the range bracket methodology */

Left off at
SECTION 11.5

