#Databases HW_12-05
## VADIM TSVETKOV

«Индексы»

**Задание 1.**

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

![img](https://github.com/vadimtsvetkov/Databases-HW_12-05/blob/main/1.jpg)

**Задание 2.**

Выполните explain analyze следующего запроса:
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id
перечислите узкие места;
оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.

Запустим оператор explain analyze для оригинальной версии кода запроса:

![img](https://github.com/vadimtsvetkov/Databases-HW_12-05/blob/main/explain_analize.jpg)

Результат:

![img](https://github.com/vadimtsvetkov/Databases-HW_12-05/blob/main/result.jpg)

Создание индекса idx_payment_date:

![img](https://github.com/vadimtsvetkov/Databases-HW_12-05/blob/main/index_payment.jpg)

Результаты запроса explain analyze, на которых видно, что индекс "idx_payment_date" используется:

![img](https://github.com/vadimtsvetkov/Databases-HW_12-05/blob/main/result_index.jpg)
