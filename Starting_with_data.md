Question 1: Which host has the average most expensive price?

SQL Queries: 
SELECT host_name, SUM(CAST(REPLACE(REPLACE(price,'$', ''), ',', '') AS DECIMAL)) as total_price
FROM listings
GROUP BY host_name
ORDER BY total_price DESC
LIMIT 1

Answer:"Esme"	1037871.00

Question 2: What is The Commonest Room Type?

SQL Queries:SELECT room_type, COUNT(room_type)
FROM listings
GROUP by room_type
LIMIT 1


Answer:"Entire home/apt"	9695


Question 3: How Many Listings can be Instantly Booked?

SQL Queries:SELECT COUNT(instant_bookable)
FROM listings
WHERE instant_bookable = 'true'

Answer:2441

Question 4:Is there any correlation between price and number of bedrooms? 


SQL Queries:SELECT CORR(bedrooms, CAST(REPLACE(replace(price,'$', ''), ',', '') as DECIMAL)) as correlation
FROM listings

Answer:0.2049909777417887, Very low Positive correlation between Bedrooms and Price.

Question 5: What Percentage of the Host per superhost?

SQL Queries:SELECT (COUNT(CASEWHEN host_is_superhost= 'true' THEN 1 END) * 100 / COUNT(*)) as percentage_true
FROM listings


Answer: 38% of Host are superhost.
