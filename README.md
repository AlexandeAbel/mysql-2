# Домашнее задание к занятию «SQL. Часть 2»

# Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

    фамилия и имя сотрудника из этого магазина;
    город нахождения магазина;
    количество пользователей, закреплённых в этом магазине.
  
    SELECT 
    CONCAT (s2.first_name,' ',s2.last_name),
    c.city,
    COUNT(*)
    FROM store s
    JOIN customer c2 ON c2.store_id = s.store_id
    JOIN address a ON a.address_id = s.address_id
    JOIN staff s2 ON s2.staff_id = s.manager_staff_id 
    JOIN city c ON a.city_id = c.city_id
    GROUP BY c.city, s2.first_name, s2.last_name
    HAVING COUNT(*) > 300;

    #Output: Mike Hillyer	Lethbridge	326

# Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
  
    SELECT 
    COUNT(*)
    FROM film f
    WHERE f.length > (SELECT AVG(f2.length) FROM film f2);

    #Output: 489

# Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

    SELECT 
    COUNT(p.payment_id ) AS count_rents, 
    DATE_FORMAT(p.payment_date, '%Y-%m') AS mounth
    FROM payment p 
    GROUP BY DATE_FORMAT(p.payment_date, '%Y-%m')
    ORDER BY COUNT(p.payment_id )DESC
    LIMIT 1;

    #Output: 6709	2005-07
