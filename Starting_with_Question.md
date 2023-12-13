Answer the following questions and provide the SQL queries used to find the answer.

Question 1: How many total listings are there in the Capetown AirBnB data? Would you say there are inactive listings in the data? If yes, What percentage of total listing is active or inactive?


# Total listings in Capetown AirBnB
SQL Queries: SELECT SUM(host_total_listings_count)
FROM listings

Answer:! 201844 Listings are in the Capetown AirBnB Data.
SQL Queries: SELECT *
FROM listing
WHERE has_availability = 'false'      
--269 listings are not active considering that they are not available.
If yes,
SQL Queries: SELECT (COUNT(CASE WHEN has_availability = 'true' THEN 1 end) * 100 / COUNT(*)) as percentage_true
FROM listings
--97% of the listings are active while 3% are inactive.


Question 2: How many distinct hosts are present in the CapeTown AirBnB listing? How many listings does each of this distinct hosts have? Which host have the most listings

# Distinct hosts present in the CapeTown AirBnB listing 
SQL Queries: SELECT COUNT (distinct host_id)
FROM listings
Answer: 5980 Distinct host are present in the CapeTown AirBnB listings.

# listings each of the distinct hosts.  
SQL Queries: SELECT host_id, COUNT(host_id) AS number_of_listing
FROM listings
GROUP BY host_id
ORDER BY number_of_listing DESC

Answer:
**"host_id"**	    **"number_of_listing"**
57218252	          115


Question 3: On Availability, What is the total number of listings available for more than 90 days a year? How many listings have availability for less than 30 days a year? What percentage of listings are available for instant booking?

SQL Queries: COUNT (distinct host_id)
FROM listings
WHERE CASE (availability_365 as integer) > 90

Answer: 4350 is the total number of listings available for more than 90 days a year.

# Listings with availability for less than 30 days a year 
SQL Queries: SELECT COUNT (distinct host_id)
FROM listings
WHERE CASE (availability_365 as integer) < 30

Answer:1198 Listings has availability for less than 30 days a year.
# percentage of listings that are available for instant booking.

SQL Queries: SELECT (COUNT(CASE WHEN instant_bookable = 'true' THEN 1 END) * 100 / COUNT(*)) AS percentage_true
FROM listings

Answer: 24 Percentage of listings are available for instant booking.


Question 4: What are the different types of properties available and their counts? Which property type has the highest average price? Write a query to show the correlation between review and pricing.

 # percentage of listings are available for instant booking.
SQL Queries: SELECT (COUNT(CASE WHEN instant_bookable = 'true' THEN 1 END) * 100 / COUNT(*)) AS percentage_true
FROM listings

Answer: "property_type"	      "COUNT"
"Private room in hostel"	      10
"Room in hotel"	                21
"Private room in bungalow"	    4
"Private room in townhouse"     2
"Private room"	                2
"Entire townhouse"	            165
"Entire vacation home"	        66
"Private room in serviced apartment"	12
"Hut"	1
"Entire guesthouse"	263
"Private room in guest suite"	35
"Entire home"	2315
"Entire cabin"	17
"Room in aparthotel"	6
"Casa particular"	2
"Entire villa"	457
"Private room in loft"	5
"Private room in condo"	1
"Earthen home"	4
"Entire serviced apartment"	253
"Private room in nature lodge"	7
"Treehouse"	1
"Entire bungalow"	48
"Castle"	1
"Shipping container"	9
"Entire cottage"	247
"Private room in farm stay"	1
"Tower"	3
"Room in hostel"	12
"Entire rental unit"	4214
"Floor"	1
"Entire loft"	148
"Entire condo"	715
"Dome"	1
"Private room in home"	28
"Room in heritage hotel"	1
"Private room in treehouse"	1
"Private room in guesthouse"	159
"Tiny home"	26
"Private room in bed and breakfast"	35
"Camper/RV"	1
"Entire place"	22
"Entire chalet"	10
"Farm stay"	23
"Private room in chalet"	1
"Room in boutique hotel"	46
"Private room in rental unit"	24
"Room in serviced apartment"	13
"Entire guest suite"	682
"Private room in vacation home"	1
"Private room in cottage"	1
"Room in bed and breakfast"	30
"Private room in villa"	10

# The property type that has the highest average price
SQL Queries: SELECT property_type, SUM(CASE(REPLACE(REPLACE(price,'$', ''), ',', '') AS DECIMAL)) AS total_price
FROM listings
GROUP BY property_type
ORDER BY total_price DESC
LIMIT 1

Answer: 
"property_type"	  "total_price"
"Entire home"    	10862254.00

# Query show the correlation between review and pricing.
SQL Queries: SELEC CORR(review_score_rating, CASE(REPLACE(REPLACE(price,'$', ''), ',', '') AS DECIMAL)) AS correlation
FROM listings

Answer: "correlation"
0.03138939778597713


Question 5: How do individual listings or hosts perform compared to the average or top-performing ones in terms of ratings, pricing, and booking frequency?

SQL Queries:SELECT round(AVG(review_score_rating),2) AS average_rating
FROM listings;

# Ratings for individual listings compared to the average
SELECT id, review_score_rating,
    CASE
        WHEN review_score_rating > (SELECT round(AVG(review_score_rating),2) FROM listings) THEN 'Above Average'
        WHEN review_score_rating < (SELECT round(AVG(review_score_rating),2) FROM listings) THEN 'Below Average'
        ELSE 'Average'
    END AS rating_comparison
FROM listings.

# Pricing for individual listings compared to the average
SQL Queries: SELECT id, price,
    CASE
        WHEN cast(replace(replace(price,'$', ''), ',', '') as decimal) > (SELECT avg(cast(replace(replace(price,'$', ''), ',', '') as decimal)) from listings) THEN 'Above Average'
        WHEN cast(replace(replace(price,'$', ''), ',', '') as decimal) < (SELECT avg(cast(replace(replace(price,'$', ''), ',', '') as decimal)) FROM listings) THEN 'Below Average'
        ELSE 'Average'
    END AS price_comparison
FROM listings;




Answer:


