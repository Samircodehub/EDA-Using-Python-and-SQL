
# Maven movie data analysis SQL Code

#### /* Email Campaigns for customers whose Store id is 2 */

* SELECT first_name, last_name,email, store_id
* FROM customer
* WHERE store_id = 2;

#### /* Number of film ids with rental rate of 0.99$ */
* SELECT COUNT(*)  FROM film
* WHERE rental_rate = 0.99;

#### /* we want to see rental rate and how many movies are in each rental rate categories */
* SELECT rental_rate, COUNT(*) AS total_number_of_movies
* FROM film
* GROUP BY rental_rate;

#### /* Which rating do we have the most films in? */
* SELECT rating,COUNT(*) AS Number of Ratings
* FROM film
* GROUP BY rating ;

#### /* Please provide films with higest numbers of rental */ 

* SELECT i.film_id, f.title, COUNT(i.film_id) AS total_number_of_rental_times
* FROM rental r
* JOIN inventory i ON r.inventory_id = i.inventory_id
* JOIN film f ON f.film_id = i.film_id
* GROUP BY i.film_id
* ORDER BY 3 DESC;


#### /* We want to mail the customers about the upcoming promotion so please provide first name ,last name, address,customer id*/
* SELECT c.customer_id, c.first_name, c.last_name, a.address
* FROM customer c
* JOIN address a ON a.address_id = c.address_id;

#### /* List of films by Film Name, Category, Language*/
* SELECT f.title AS 'Film Name',c.name AS' Film Type' ,l.name AS ' Film Language'
* FROM film f
* JOIN film_category fc ON fc.film_id = f.film_id
* JOIN category c ON fc.category_id = c.category_id
* JOIN language l ON l.language_id = f.language_id;

#### /* Revenue per Movie */

* SELECT i.film_id, f.title, COUNT(i.film_id) AS total_number_of_rental_times, f.rental_rate, COUNT(i.film_id)*f.rental_rate AS revenue_per_movie
* FROM  inventory i 
* JOIN film f ON f.film_id = i.film_id
* GROUP BY i.film_id
* ORDER BY 5 DESC;

#### /* We will need count of active customers for each of your store, separately please.*/
* SELECT  store_id, COUNT(customer_id) AS 'active customers'
* FROM customer
* WHERE active = 1
* group by store_id

#### /*We will need separate count inventory items separately at each of your two store*/

* SELECT  store_id, COUNT(inventory_id) AS 'inventorty items'
* FROM inventory
* group by store_id;

#### /*PROVIDE THE COUNT OF UNIQUE CATEGORIES*/

* SELECT 
* COUNT(DISTINCT name) AS 'UNIQUE CATEGORIES'
* FROM Category 


#### /* We would like to understand the replacement cost of your film.please provide the replacement cost for  the film that is least expensive to replace, the most expensive to replace and the  avg. of all film you carry.*/

* SELECT
* MIN(replacement_cost) AS 'Least expensive',
* MAX(replacement_cost) AS 'Most expensive',
* AVG(replacement_cost)AS 'Average replacement cost required'
* FROM film


#### /* Film id having highest replacement cost */

* SELECT film_id, replacement_cost
* FROM film
* order by replacement_cost DESC

#### /* Film id having highest replacement cost */

* SELECT film_id, replacement_cost
* FROM film
* order by 2 DESC

#### /* We are interested in having you put payment monitoring system  and maximum payment processing restrictions in place you order to minimize the future risk of fraud by your staff. please provide maximum and average payment you process*/

* SELECT 
* MAX(amount) AS 'Maximum payment',
* AVG(amount) AS 'Average payment'
* FROM payment


#### /* We would like to better understand what your customer base look like. Please provide a lIst of all customer identification values, with count of rental they have made all time, with your highest volume of customer at top of the list. */

* SELECT distinct
* customer_id, COUNT(rental_id) AS ' RENTAL MADE ALL TIME'
* FROM rental
* group by customer_id
* order by 2 desc


#### /* My partner and I would like to get to know your board of advisor and current investor.Could you please provide advisor and investor names in one table? And for investor, it would be good to include which company they work with.*/

* SELECT
* 'investor' AS type,
* first_name,
* company_name
* FROM investor


#### /* My partner and I want to come by each of stores in person and meet the managers. Please send over the managers name at each store, with full address of each property ( street address,city, district and contry please) */
* SELECT 
* staff.first_name AS 'Manager first name',
* staff.last_name AS 'Manager last name',
* address.address,
* address.district,
* city.city,
* country.country
* FROM store
* LEFT JOIN staff ON store.manager_staff_id = staff.staff_id
* LEFT JOIN address ON store.address_id = address.address_id
* LEFT JOIN city ON address.city_id = city.city_id
* LEFT JOIN country ON city.country_id = country.country_id

#### /* I would like to get better understanding of all of the inventory theat would come along with the bussiness. Please pull the list of each inventory item you have stocked , including store id number, inventory id ,name of film,film rating, its rental rate and replacement cost. */
* SELECT 
* inventory.inventory_id AS 'inventory item',
* inventory.store_id AS 'store id',
* film.title,
* film.rating,
* film.rental_rate,
* film.replacement_cost
* FROM inventory
* LEFT JOIN film ON inventory.film_id = film.film_id


#### /* Please provide list of all customers name, whivh store they go to, wethere or not currenty they active, and their full address(street address, city, contry)*/

* SELECT DISTINCT
* customer. first_name,customer.last_name,customer.store_id,customer.active,
* address.address,
* address.district,
* city.city
* from payment  
* JOIN customer ON customer.customer_id =payment.customer_id
* JOIN address ON address.address_id =customer.address_id
* JOIN city ON city.city_id = address.city_id
* group by 1

#### /* Please provide total number of film for each rental rate*/

* SELECT rental_rate, COUNT(*) AS total_number_of_movies
* FROM film
* GROUP BY 1;







