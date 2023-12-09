Answer the following questions and provide the SQL queries used to find the answer.

Question 1: How many total listings are there in the Capetown AirBnB data? Would you say there are inactive listings in the data? If yes, What percentage of total listing is active or inactive?

SQL Queries:

Answer:




Question 2: How many distinct hosts are present in the CapeTown AirBnB listing? How many listings does each of this distinct hosts have? Which host have the most listings

SQL Queries:
#How many distinct hosts are present in the CapeTown AirBnB listing? 
select count (distinct host_id)
from listings

Answer:
5980

SQL Queries:
--How many listings does each of this distinct hosts have? 
select host_id, count(host_id) as number_of_listing
from listings
group by host_id
order by number_of_listing desc

Answer:

SQL Queries
--How many listings does each of this distinct hosts have? 
select host_id, count(host_id) as number_of_listing
from listings
group by host_id
order by number_of_listing desc

Answer:
**"host_id"**	    **"number_of_listing"**
57218252	          115




Question 3: On Availability, What is the total number of listings available for more than 90 days a year? How many listings have availability for less than 30 days a year? What percentage of listings are available for instant booking?

SQL Queries: --On Availability, What is the total number of listings available for more than 90 days a year?
select count(distinct host_id)
from listings
where cast(availability_365 as integer) > 90

Answer: 4350

SQL Queries: --How many listings have availability for less than 30 days a year? 
select count(distinct host_id)
from listings
where cast(availability_365 as integer) < 30

Answer:1198

SQL Queries: --What percentage of listings are available for instant booking?
select (count(case when instant_bookable = 'true' then 1 end) * 100 / count(*)) as percentage_true
from listings

Answer: 24




Question 4: What are the different types of properties available and their counts? Which property type has the highest average price? Write a query to show the correlation between review and pricing.

SQL Queries: --What percentage of listings are available for instant booking?
select (count(case when instant_bookable = 'true' then 1 end) * 100 / count(*)) as percentage_true
from listings

Answer:"property_type"	      "count"
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

SQL Queries:
--Which property type has the highest average price? 
select property_type, sum(cast(replace(replace(price,'$', ''), ',', '') as decimal)) as total_price
from listings
group by property_type
order by total_price desc
limit 1

Answer: 
"property_type"	  "total_price"
"Entire home"    	10862254.00

SQL Queries: --Write a query to show the correlation between review and pricing.
select corr(review_score_rating, cast(replace(replace(price,'$', ''), ',', '') as decimal)) as correlation
from listings

Answer: 
"correlation"
0.03138939778597713




Question 5: How do individual listings or hosts perform compared to the average or top-performing ones in terms of ratings, pricing, and booking frequency?

SQL Queries:

Answer:
