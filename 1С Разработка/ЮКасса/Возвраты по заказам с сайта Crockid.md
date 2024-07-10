#### Оформление возврата с сайта Crockid
##### Задача
Получить Идентификатор платежа в ЮKassa. С сайта Crockid.

##### Обозначения 
_payment_id_ - Идентификатор платежа в ЮKassa.
_orders_id_ - Номер заказа сайта.

##### Способ получения payment_id

Для оформления возврата с сайта нам нужен _payment_id_, его требуется указывать при создании возврата.

Для этого из 1с обращается на прямую в БД сайта 

Пример: 
```SQL
SELECT 
payment_id
FROM crockid_prod.orders
WHERE crockid_prod.orders.id = orders_id
```

