#### Оформление возврата с сайта VeryNeat

##### Задача
Получить _payment_id_ - Идентификатор платежа в ЮKassa. С сайта VeryNeat.

##### Обозначения
_payment_id_ - Идентификатор платежа в ЮKassa.
_orderId_ - Номер заказа сайта.
_access_token_ - Токен доступа. 
_error_massage_ - Сообщение об ошибке.

##### Способ получения payment_id 
Для оформления возврата с сайта нам нужен _payment_id_, его требуется указывать при создании возврата.

Для этого из 1С отправляем HTTP запрос на veryneat.ru, в ответ получаем _payment_id_.

**Запрос:** 
```http 
GET /api/v1/payment/{orderId} HTTP/1.1
Host: veryneat.ru
Authorization: _access_token_
```

**ИЛИ** 

```http
GET /api/v1/payment?orderId=593 HTTP/1.1
Host: veryneat.ru
Authorization: _access_token_
```

**Ответ:**
>[!success]  200 Успешно
> ```json
{
  "payment_id": "2e0cd9a7-000f-5000-8000-1b65d5965562"
}
> ```
> 

> [!bug]  Код ответа <> 200. Ответ при ошибке.
> ```json
{
  "error": "error_massage"
}
> ```
> 




