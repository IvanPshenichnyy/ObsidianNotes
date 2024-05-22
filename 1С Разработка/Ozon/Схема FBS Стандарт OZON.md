## Схема FBS Стандарт

1. Перед началом работы с отправлениями получите список необработанных отправлений: [/v3/posting/fbs/unfulfilled/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingUnfulfilledList).
    
    Если покупатель юридическое лицо, то в блоке `requirements` будет информация о необходимости передать страну-производителя для всех товаров в заказе, у которых она не указана. Получите список доступных для выбора стран: [/v2/posting/fbs/product/country/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_ListCountryProductFbsPostingV2). Затем передайте информацию о стране-производителе: [/v2/posting/fbs/product/country/set](https://docs.ozon.ru/api/seller/#operation/PostingAPI_SetCountryProductFbsPostingV2).
    
    Также можно получать список заказов (отправлений): [/v3/posting/fbs/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingListV3). Он позволяет получить все заказы, используя фильтры с различными статусами. Можно также получить данные аналитики, если поле `with` отправить со значением `analytics_data`.
    
    Отправления могут прийти в статусах `awaiting_packaging`, `awaiting_approve` или `awaiting_verification`.
    
2. Получите дополнительную информацию о заказах: [/v3/posting/fbs/get](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingV3).
    
    В блоке `requirements` указывается:
    
    - какие товары подлежат обязательной маркировке;
    - нужно ли передать номер грузовой таможенной декларации и регистрационный номер партии товара — эту информацию также можно получить с помощью методов [/v3/posting/fbs/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingListV3) и [/v3/posting/fbs/unfulfilled/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingUnfulfilledList).
    
    Дополнительную информацию вы также можете получить по штрихкоду: [/v2/posting/fbs/get-by-barcode](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingByBarcode).
    
3. Проверьте, что коды маркировки соответствуют требованиям системы «Честный ЗНАК» по составу и количеству символов: [/v4/fbs/posting/product/exemplar/validate](https://docs.ozon.ru/api/seller/#operation/PostingAPI_FbsPostingProductExemplarValidate).
    
    С помощью метода [/v5/fbs/posting/product/exemplar/set](https://docs.ozon.ru/api/seller/#operation/PostingAPI_FbsPostingProductExemplarSet) добавьте для каждого экземпляра маркировку, которую будете передавать в систему «Честный ЗНАК». При необходимости передайте номера таможенных деклараций и регистрационные номера партии товара или укажите, что их нет.
    
    [Подробнее о маркировке «Честный ЗНАК» в Базе знаний](https://seller-edu.ozon.ru/work-with-goods/trebovaniya-k-kartochkam-tovarov/product-information/obyazatelnaya-markirovka-tovarov)
    
    Получите статусы передачи маркировок:
    

- [/v4/fbs/posting/product/exemplar/status](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetProductExemplarStatus) — получить статус добавления экземпляров.
- [/v5/fbs/posting/product/exemplar/create-or-get](https://docs.ozon.ru/api/seller/#operation/PostingAPI_FbsPostingProductExemplarCreateOrGet) — получить данные созданных экземпляров.

4. Перед сборкой убедитесь, что отправление соответствует установленным в пункте приёма ограничениям. Получите ограничения пункта приёма по номеру отправления: [/v1/posting/fbs/restrictions](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetRestrictions).
    
5. До окончания времени на сборку подтвердите, что вы собрали заказ: [/v4/posting/fbs/ship](https://docs.ozon.ru/api/seller/#operation/PostingAPI_ShipFbsPostingV4). Вы не сможете собрать заказ, если:
    
    - заказ не в статусе `awaiting_packaging`;
    - вы не указали коды маркировки для товаров, подлежащих обязательной маркировке.
    
    При необходимости используйте этот метод, чтобы разделить заказ на несколько отправлений. Например, если в заказе несколько товаров и их необходимо упаковать в разные коробки, так как вместе они не отвечают требованиям к упаковке.
    
    После использования метода статус отправления изменится на `awaiting_deliver`.
    
    Вы можете использовать метод для частичной сборки: [/v4/posting/fbs/ship/package](https://docs.ozon.ru/api/seller/#operation/PostingAPI_ShipFbsPostingPackage).
    
6. Для каждого отправления распечатайте наклейку для идентификации в системе Ozon: [/v2/posting/fbs/package-label](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSPackageLabel).
    
7. Подтвердите отгрузку и запустите формирование транспортной накладной: [/v2/posting/fbs/act/create](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSActCreate). В ответе метода вы получите идентификатор задания на формирование транспортной накладной и штрихкода для отгрузки.
    
8. Получите список перевозок, по которым нужно распечатать штрихкод для отгрузки и транспортную накладную: [/v1/posting/carriage-available/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetCarriageAvailableList).
    
9. Проверьте, что отгрузка создана: [/v2/posting/fbs/act/check-status](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSActCheckStatus).
    
10. Получите штрихкод для отгрузки: [/v2/posting/fbs/act/get-barcode](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSGetBarcode).
    
11. Проверьте статус формирования накладной: [/v2/posting/fbs/digital/act/check-status](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSDigitalActCheckStatus). Когда статус документа перейдёт в `FORMED`, получите файлы:
    
    - Транспортная накладная: [/v2/posting/fbs/act/get-pdf](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSGetAct).
    - Лист отгрузки: [/v2/posting/fbs/digital/act/get-pdf](https://docs.ozon.ru/api/seller/#operation/PostingAPI_PostingFBSGetDigitalAct).

После этого можете отвезти отправления и документы в пункт приёма.

Если отправление передано в доставку, но не просканировано в сортировочном центре, вы можете открыть спор: [/v2/posting/fbs/arbitration](https://docs.ozon.ru/api/seller/#operation/PostingAPI_MoveFbsPostingToArbitration). Открытый спор переведёт отправление в статус `arbitration`.

Если спор по отправлению откроет покупатель, статус отправления изменится на `client_arbitration`.

Чтобы отследить изменение статуса, когда отправление найдено, используйте [/v3/posting/fbs/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetFbsPostingListV3) с нужными фильтрами.

Для передачи спорных заказов к отгрузке используйте [/v2/posting/fbs/awaiting-delivery](https://docs.ozon.ru/api/seller/#operation/PostingAPI_MoveFbsPostingToAwaitingDelivery). Статус отправления изменится на `awaiting_deliver`.

### Отменить доставку отправления

1. Используйте [/v2/posting/fbs/cancel-reason/list](https://docs.ozon.ru/api/seller/#operation/PostingAPI_GetPostingFbsCancelReasonList) на любом этапе работы с отправлением, чтобы получить список причин отмены отправления.
    
2. Передайте этот список и номер отправления: [/v2/posting/fbs/cancel](https://docs.ozon.ru/api/seller/#operation/PostingAPI_CancelFbsPosting).
    

Чтобы отменить часть товаров в отправлении, используйте [/v2/posting/fbs/product/cancel](https://docs.ozon.ru/api/seller/#operation/PostingAPI_CancelFbsPostingProduct).

Если отправление отменит покупатель, статус изменится на `cancelled`.