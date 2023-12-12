This Queries was used to show the description of table.


SELECT 
   table_name, 
   column_name, 
   data_type 
FROM 
   information_schema.columns
WHERE 
   table_name = 'listings';



   This Queries was used to delect rows with missing values.

DELETE FROM listings
where id is null 
or name is null
or host_id is null
or host_name is null
or host_since is null
or host_location is null
or host_response_time is null
or host_response_rate is null
or host_acceptance_rate is null
or host_is_superhost is null
or host_listings_count is null
or host_total_listings_count is null
or host_verifications is null
or host_has_profile_pic is null
or neighbourhood is null
or property_type is null
or room_type is null
or accomodates is null
or bathrooms_text is null
or bedrooms is null
or beds is null
or amenities is null
or price is null
or minimum_nights is null
or maximum_nights is null
or has_availability is null
or availability_30 is null
or availability_60 is null
or availability_90 is null
or availability_365 is null
or number_of_reviews is null
or first_review is null
or last_review is null
or review_score_rating is null
or review_scores_accuracy is null
or review_scores_cleanliness is null
or review_scores_checkin is null
or review_scores_communication is null
or review_scores_location is null
or review_scores_value is null
or instant_bookable is null
