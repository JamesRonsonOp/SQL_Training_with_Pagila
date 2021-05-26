Pagila Example Queries
====

### These questions were sourced from here: 

[pgdash](https://pgdash.io/blog/postgres-indexes.html)

TO SEE HOW THESE QUERIES WORK BEHIND THE SCENES DO THIS: 

```
EXPLAIN SELECT email
    FROM customer 
    WHERE active = 0;
        QUERY PLAN
```

---USE COVERING INDEXES---

1. Fetch the emails of all inactive customers.

```
SELECT email
FROM customer 
WHERE active = 0;
```
hint: customer table has an active column

2. Create an index on the active column and name it idx_cust1. Then repeat the query from question 1. 
```
CREATE INDEX idx_cust1 ON customer(active);

SELECT email
FROM customer
WHERE active = 0;
```
    explanation: the query in question 1 required a full sequential scan of the customer table which is more time consuming. Indexing helps to speed up the query by replacing a sequential scan with an "index scan." This means Postgres will can the index "idx_cust1," and then further lookup the table's heap to read the other column values (in this case, the email column) that the query needs. 
    
3. This time, fetch the emails of all inactive customers by creating a "covering index" by including the email column.
```
CREATE INDEX idx_cust2 
ON customer(active)
INCLUDE (email);

SELECT email FROM customer WHERE active = 0;
```

---USE PARTIAL INDEXES---
Partial Indexes only index a subset of the rows in a table. This keeps the indexes smaller in size and faster to scan through. 

4. Get the list of emails of customers located in California.  
```
SELECT c.email 
FROM customer c
JOIN address a
ON c.address_id = a.address_id
WHERE a.district = 'California';
```
QUERY Explain: involves scanning both the tables that are joined. 

---using regular indexing---
CREATE INDEX idx_address1 ON address(district);

```SELECT c.email FROM customer c
JOIN address a ON c.address_id = a.address_id
WHERE a.district = 'California';```

QUERY Explain: the scan of `address` has been replaced witha n index scan over idx_address1, and a scan of address's heap. Assuming this is a frequent query and needs to be optimized, we can use a partial index which only indexes those rows of address where the district is 'California':

---using partial indexing---
```CREATE INDEX idx_address2 ON address(address_id)
    WHERE district = 'California';
   
   SELECT c.email FROM customer c
   JOIN address a ON c.address_id = a.address_id
   WHERE a.district = 'California';

Query Explain: The query now reads only the index idx_address2 and does not touch the table address. 

---TO LEARN MORE ABOUT INDEX GO HERE: 

Multi-Value Indexes, Eliminating Duplicate Indexes, Superset Indexes, Unused Indexes Rebuilding indexes with less locking, enabling parallesl index creation, creating indexes in the background 

```
5. 
```

```