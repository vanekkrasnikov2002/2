
## Тема 2. Базовые SELECT ЗАПРОСЫ

## Выборка данных с `SELECT`

`SELECT` - это основная команда SQL для выборки данных из таблицы. Пример:

```sql
SELECT *
FROM products;
```

Этот запрос выбирает все строки из таблицы "products".

```sql
SELECT product_id, product_name, unit_price
FROM products;
```



## Выборка и простая арифметика в SQL



```sql
SELECT product_id, product_name, unit_price * units_in_stock AS total_price
FROM products;
```



## Использование `DISTINCT` в запросах

`DISTINCT` используется для выбора уникальных значений из столбца:

```sql
SELECT DISTINCT title
FROM employees;
```



```sql
SELECT DISTINCT country, title
FROM employees;
```


## Использование `COUNT` в запросах

`COUNT` используется для подсчета строк в выборке:

```sql
SELECT COUNT(*)
FROM employees;
```



```sql
SELECT COUNT(DISTINCT country)
FROM employees;
```



## Использование `WHERE` в запросах

`WHERE` используется для фильтрации результатов:

```sql
SELECT company_name, contact_name, phone, country
FROM customers
WHERE country = 'USA';
```



```sql
SELECT *
FROM products
WHERE unit_price > 20;
```


```sql
SELECT COUNT(*)
FROM products
WHERE unit_price < 20;
```


```sql
SELECT *
FROM products
WHERE discontinued = 1;
```



## `AND` и `OR`

Можно комбинировать условия с помощью операторов `AND` и `OR`:

```sql
SELECT *
FROM products
WHERE unit_price > 25 AND units_in_stock > 40;
```


```sql
SELECT *
FROM customers
WHERE city = 'Berlin' OR city = 'London' OR city = 'San Francisco';
```

Этот запрос вернет клиентов из городов Берлин, Лондон или Сан-Франциско.

## `BETWEEN`

`BETWEEN` используется для выбора значений в заданном диапазоне:

```sql
SELECT *
FROM orders
WHERE freight BETWEEN 20 AND 40;
```


## `IN`, `NOT IN`

`IN` и `NOT IN` используются для выбора значений из списка:

```sql
SELECT *
FROM customers
WHERE country IN ('Mexico', 'Germany', 'USA', 'Canada');
```

Этот запрос вернет клиентов из Мексики, Германии, США или Канады.

```sql
SELECT *
FROM products
WHERE categoryid NOT IN (1, 3, 5, 7);
```


## Сортировка с `ORDER BY`

`ORDER BY` используется для сортировки результатов:

```sql
SELECT DISTINCT country
FROM customers
ORDER BY country;
```


```sql
SELECT DISTINCT country, city
FROM customers
ORDER BY country DESC, city ASC;
```


## Вычисление минимума, максимума и среднего: `MIN`, `MAX`, `AVG`

Можно вычислять минимум, максимум и среднее значение столбца:

```sql
SELECT MIN(order_date)
FROM orders
WHERE ship_city = 'London';
```

```sql
SELECT MAX(order_date)
FROM orders
WHERE ship_city = 'London';
```


```sql
SELECT AVG(unit_price)
FROM products
WHERE discontinued <> 1;
```


## `LIKE` в запросах для поиска строк

`LIKE` используется для поиска строк по шаблону:

```sql
SELECT last_name, first_name
FROM employees
WHERE first_name LIKE '%n';
```


```sql
SELECT last_name, first_name
FROM employees
WHERE last_name LIKE 'B%';
```


```sql
SELECT last_name, first_name
FROM employees
WHERE last_name LIKE 'Buch%';
```


```sql
SELECT last_name, first_name
FROM employees
WHERE last_name LIKE '_uch%';
```


## `LIMIT`

`LIMIT` используется для ограничения количества возвращаемых строк:

```sql
SELECT product_name, unit_price
FROM products
WHERE discontinued <> 1
ORDER BY unit_price DESC
LIMIT 10;
```


## Проверка на NULL: `IS NULL`, `IS NOT NULL`

`IS NULL` и `IS NOT NULL` используются для проверки наличия или отсутствия значений NULL:

```sql
SELECT ship_city, ship_region, ship_country
FROM orders
WHERE ship_region IS NULL;
```


```sql
SELECT ship_city, ship_region, ship_country
FROM orders
WHERE ship_region IS NOT NULL;
```


## Группировка `GROUP BY`

`GROUP BY` используется для группировки результатов:

```sql
SELECT ship_country, COUNT(*)
FROM orders
WHERE freight > 50
GROUP BY ship_country
ORDER BY COUNT(*) DESC;
```


```sql
SELECT category_id, SUM(UnitsInStock)
FROM products
GROUP BY category_id
ORDER BY SUM(units_in_stock) DESC
LIMIT 5;
```


## Постфильтрация с `HAVING`

`HAVING` используется для фильтрации результатов после группировки:

```sql
SELECT category_id, SUM(unit_price * units_in_stock) AS total_value
FROM products
WHERE discontinued <> 1
GROUP BY category_id
HAVING total_value > 5000
ORDER BY total_value DESC;
```


## Объединение, пересечение, разница в SQL - `UNION`, `INTERSECT`, `EXCEPT`

`UNION`, `INTERSECT` и `EXCEPT` используются для объединения, пересечения и разницы результатов соответственно:

```sql

SELECT country
FROM customers
UNION
SELECT country
FROM employees;

SELECT country
FROM customers
UNION ALL
SELECT country
FROM employees;

SELECT DISTINCT country
FROM customers
UNION
SELECT DISTINCT country
FROM employees;

SELECT country 
FROM customers
INTERSECT
SELECT country
FROM suppliers;

SELECT country 
FROM customers
EXCEPT
SELECT country
FROM suppliers;

SELECT country 
FROM customers
EXCEPT ALL
SELECT country
FROM suppliers;
```
