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
