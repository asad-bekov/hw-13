# Домашнее задание к занятию «SQL. Часть 1»
*Асадбеков Асадбек*

## Задание 1

**1. Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.**

```bash
SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a'
AND district NOT LIKE '% %';
```
![alt text](https://github.com/asad-bekov/hw-13/blob/main/img/1.png)

## Задание 2

**1. Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.**

```bash
SELECT *
FROM payment
WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-18'
AND amount > 10.00;
```
![alt text](https://github.com/asad-bekov/hw-13/blob/main/img/2.png)

## Задание 3

**1. Получите последние пять аренд фильмов.**

```bash
SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;
```
![alt text](https://github.com/asad-bekov/hw-13/blob/main/img/3.png)

## Задание 4

**1. Одним запросом получите активных покупателей, имена которых Kelly или Willie.**

Сформируйте вывод в результат таким образом:

- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,

- замените буквы 'll' в именах на 'pp'.

```bash
SELECT 
    REPLACE(LOWER(first_name), 'll', 'pp') AS first_name_fixed, 
    LOWER(last_name) AS last_name_fixed 
FROM customer 
WHERE active = 1 
AND LOWER(first_name) IN ('kelly', 'willie');
```
![alt text](https://github.com/asad-bekov/hw-13/blob/main/img/4.png)

## Задание 5*

**1. Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.**

```bash
SELECT 
    SUBSTRING_INDEX(email, '@', 1) AS email_prefix, 
    SUBSTRING_INDEX(email, '@', -1) AS email_domain 
FROM customer;
```
![alt text](https://github.com/asad-bekov/hw-13/blob/main/img/5.png)

## Задание 6*

**1. Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.**

```bash
SELECT 
    CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', 1), 1)), 
           LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', 1), 2))) AS email_prefix_fixed, 
    CONCAT(UPPER(LEFT(SUBSTRING_INDEX(email, '@', -1), 1)), 
           LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', -1), 2))) AS email_domain_fixed 
FROM customer;
```
![alt text](https://github.com/asad-bekov/hw-13/blob/main/img/6.png)

---