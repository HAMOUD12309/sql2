# sql2
# :movie_camera: KSA THEATERS ANALYSIS
This repository is dedicated to the analysis of theater ratings within the Kingdom of Saudi Arabia. By examining ratings data collected from cinema-goers, this project aims to uncover insights into audience satisfaction, performance variations across regions, and overall trends in the cinema industry in KSA.

## 1. Get the Average Review Count for Each Genre

```sql
select 
    genre, 
    round(avg(review_count),1) as avg_review_count_by_genre
from theaters_ksa
group by genre;

```

<img width="486" alt="Screenshot 1446-08-12 at 9 27 13 PM" src="https://github.com/user-attachments/assets/8d33bf57-53cb-466e-9c2b-001bb676c382" />

## 2. Retrieve the Top 5 Theaters by Rating

```sql
select * from theaters_ksa;
select name , rating
from theaters_ksa
order by rating desc
limit 5;
```

<img width="486" alt="Screenshot 1446-08-12 at 9 34 30 PM" src="https://github.com/user-attachments/assets/5dc0fb79-e6f1-4bd9-a0e8-0bfe71398135" />

## 4. Count the Number of Theater per Genre

```sql
select genre,count(name) as count
from theaters_ksa
group by genre
order by count desc;
```

<img width="486" alt="Screenshot 1446-08-12 at 9 43 00 PM" src="https://github.com/user-attachments/assets/d00dece3-00aa-4bde-837f-dc964962f7da" />

## 5. Get the Average Rating for Each Genre

```sql
select 
    genre, 
    round(avg(rating),2) as avg_rating_by_genre
from theaters_ksa
group by genre;
```

<img width="486" alt="Screenshot 1446-08-12 at 9 46 50 PM" src="https://github.com/user-attachments/assets/7c54451d-8ced-4fa4-acd3-3a3c83d5b832" />

## 6. Get the Average Rating for * Theaters

```sql
select 
    round(avg(rating),2) as avg_rating
from theaters_ksa;
```

<img width="486" alt="Screenshot 1446-08-12 at 9 49 16 PM" src="https://github.com/user-attachments/assets/a75f45cf-0e39-493a-9cd8-d74a9bc42fc9" />

## 7. Total Theaters in Riyadh

```sql
select 
    count(location) as total_theaters_in_Riyadh
from theaters_ksa
where location like '%Riyadh%';
```

<img width="486" alt="Screenshot 1446-08-12 at 10 05 47 PM" src="https://github.com/user-attachments/assets/ad80fc00-2ec2-4f51-896d-41fda2ec1929" />


## 8. Average Rating in Riyadh

```sql
select 'Riyadh' as location, avg(rating) as avg_rating
from theaters_ksa
where location like '%Riyadh%';
```

<img width="486" alt="Screenshot 1446-08-12 at 10 11 45 PM" src="https://github.com/user-attachments/assets/66d19e0e-0a42-43bb-a2a0-767bd21aac2a" />


## 9. Theaters with Above Average Review Count

```sql
select 
    name, 
    review_count
from theaters_ksa
where review_count > (select avg(review_count) from theaters_ksa)
order by review_count desc;
```

<img width="486" alt="Screenshot 1446-08-12 at 10 18 24 PM" src="https://github.com/user-attachments/assets/2299c0bd-1604-4a4a-aa7c-173dcdf9e33d" />

## 10. Theaters with Below Average Review Count

```sql
select 
    name, 
    review_count
from theaters_ksa
where review_count < (select avg(review_count) from theaters_ksa)
order by review_count desc;

```
<img width="486" alt="Screenshot 1446-08-12 at 10 31 42 PM" src="https://github.com/user-attachments/assets/2d8c4bf9-99b4-4741-9c6e-1fa2ad19a857" />


## :gift: Bonus: A Simple MySQL Function for Theater Rating Categorization
**This function converts a numeric rating into labels like "Excellent" or "Poor" based on rating. It helps make the ratings more understandable.**
# Function:
```sql
delimiter $$

create function get_rating_category(rating_value decimal(3,2))
returns varchar(20)
deterministic
begin
  declare category varchar(20);

  if rating_value >= 4.5 then
    set category = 'Excellent';
  elseif rating_value >= 3.5 then
    set category = 'Good';
  elseif rating_value >= 2.5 then
    set category = 'Average';
  elseif rating_value >= 1.5 then
    set category = 'Below Average';
  else
    set category = 'Poor';
  end if;

  return category;
end$$

delimiter ;

```

# How to use:
**Once the function is created, you can use it in a query.** 

# Example:
```sql
select 
  name, 
  rating, 
  get_rating_category(rating) as rating_category
from theaters_ksa;
```

<img width="486" alt="Screenshot 1446-08-12 at 10 40 31 PM" src="https://github.com/user-attachments/assets/6633a0dd-ee3c-40ee-a7b8-6fc0135420e0" />

