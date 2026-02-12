Создание пользователя в БД
```sql
CREATE USER service WITH PASSWORD '';
```

Выдача прав на схему public
```sql
GRANT USAGE ON SCHEMA public TO service;
GRANT CREATE ON SCHEMA public TO service;
```

Выдача прав на таблицы в схеме public
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO service;
```

Запрос кол-ва сосисок
```sql
SELECT o.date_created as date, SUM(op.quantity) as amount
FROM orders AS o
JOIN order_product AS op ON o.id = op.order_id
WHERE o.status = 'shipped' AND o.date_created > NOW() - INTERVAL '7 DAY'
GROUP BY o.date_created
ORDER BY date;

Time: 53,996 ms
```
Без индексов время запроса - `53,996 ms`
С использованием индексов время запроса - `22,999 ms`
