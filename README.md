# DVD-Rental-Database-Analysis-SQL-PowerBI

This project is focused on extracting meaningful insights from a DVD rental database using SQL query and visualizing the results with PowerBI. The DVD rental database represents the business processes of a DVD rental store, within a period of 4 months. The database utilized in this project is designed with a snowflake schema, requiring slightly more complex joins between tables to extract relevant information with SQL query.

To start, I designed and executed an SQL query to join multiple tables within the database and extract the necessary information. Once the data was extracted, I downloaded it as a CSV file and imported it into PowerBI to clean and organize the data using Power Query Editor. I have then created the necessary tables and built the relationship model so that the data can be manipulated. Finally, I have created interactive visualizations and dashboards that contain slicers to filter the visuals by month and film genres. This would allow users to analyze the data in a more intuitive and user-friendly way and gain valuable insights.

##  Data Visualization in PowerBI

### 1. Entity Relationship Diagram Model
![Entity Relationship Diagram](https://user-images.githubusercontent.com/127214128/235675767-cfdc60b5-040e-4733-a1bd-ce44e1f1ed3d.PNG)

### 2. Sales Overview Dashboard
![Sales Overview](https://user-images.githubusercontent.com/127214128/235675910-e2e61a66-0f15-4f57-91f7-3aa87dca98fc.PNG)

### 3. Films and Customers Dashboard
![Films and Customers](https://user-images.githubusercontent.com/127214128/235693618-2409493d-a4d4-4f29-b27b-699464f1ce3f.PNG)

##  Database and SQL query in PostgreSQL

### 1. Database Entity Relationship Diagram Model
![Entity Relationship Diagram of Database](https://user-images.githubusercontent.com/127214128/235706207-2526f55c-be39-4cdc-b9bd-b59d35f5632a.PNG)

### 2. SQL Query
```
SELECT

c.customer_id,
p.payment_id,
p.amount,
DATE(p.payment_date) AS payment_date,
concat(c.first_name, ' ', c.last_name) AS customer_name,
ci.city,
ci.city_id,
co.country_id,
co.country,

f.film_id,
f.title,
f.length,
f.rental_rate,
f.rental_duration,
f.rating AS mpaa_rating,

cat.category_id,
cat.name AS film_category

FROM payment p

INNER JOIN customer c 
ON p.customer_id = c.customer_id
INNER JOIN address a
ON a.address_id = c.address_id
INNER JOIN city ci
ON ci.city_id = a.city_id
INNER JOIN country co
ON co.country_id = ci.country_id

INNER JOIN rental re
ON re.customer_id = c.customer_id AND p.rental_id = re.rental_id
INNER JOIN inventory i
ON i.inventory_id = re.inventory_id
INNER JOIN film f
ON i.film_id = f.film_id
JOIN film_category fc
ON fc.film_id = f.film_id
INNER JOIN category cat
ON cat.category_id = fc.category_id

ORDER BY 
c.customer_id ASC
```
