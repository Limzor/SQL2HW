# Домашнее задание к занятию "`SQL. Часть 2`" - `Фёдоров Илья`
### Задание1
SELECT staff.last_name, staff.first_name, city.city, COUNT(customer.customer_id) AS customer_count
FROM staff
JOIN store ON staff.store_id = store.store_id
JOIN customer ON store.store_id = customer.store_id
JOIN address ON store.address_id = address.address_id
JOIN city ON address.city_id = city.city_id
GROUP BY staff.last_name, staff.first_name, city.city
HAVING COUNT(customer.customer_id) > 300;
![alt text](https://github.com/Limzor/SQL2HW/blob/main/Screenshot_1.png)
### Задание2
SELECT 
COUNT(*) AS "Количество фильмов"
FROM film 
WHERE length > (SELECT AVG(length) FROM film);
![alt text](https://github.com/Limzor/SQL2HW/blob/main/Screenshot_2.png)
### Задание3
SELECT 
    mp.payment_month AS "Месяц",
    mp.total_payment AS "Наибольшая сумма платежей",
    COUNT(r.rental_id) AS "Количество аренд"
FROM (
    SELECT 
        DATE_FORMAT(payment_date, '%Y-%m-01') AS payment_month,
        SUM(amount) AS total_payment
    FROM 
        payment
    GROUP BY 
        DATE_FORMAT(payment_date, '%Y-%m-01')
) AS mp
JOIN 
    rental r ON DATE_FORMAT(r.rental_date, '%Y-%m-01') = mp.payment_month
GROUP BY 
    mp.payment_month, mp.total_payment
ORDER BY 
    mp.total_payment DESC
LIMIT 1;
![alt text](https://github.com/Limzor/SQL2HW/blob/main/Screenshot_3.png)
