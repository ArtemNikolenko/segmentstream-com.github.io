---
layout: page
section: integrationsRU
title: "Vkontakte"
order: 1
---

В данном разделе вы узнаете:
* Как установить пиксель Vkontakte на ваш сайт.
* Как подключить ретаргетинг в Vkontakte.
* Как настроить передачу событий в Vkontakte.
* Как подключить динамический ретаргетинг Vkontakte

Vkontakte - социальная сеть с небольшим набором рекламных инструментов. Vkontakte умеет создавать аудитории на основе событий сайта и показывать объявления этой аудитории. В ноябре 2017 года Vkontakte добавил продуктовый динамический ремаркетинг. SegmentStream позволяет отправлять данные о поведении ваших пользователей в [Vkontakte](https://vk.com/dev/openapi_3?f=7.%2B%D0%A0%D0%B5%D1%82%D0%B0%D1%80%D0%B3%D0%B5%D1%82%D0%B8%D0%BD%D0%B3%2B%D0%B2%2BOpen%2BAPI).

### Навигация по странице
------
<ul class="page-navigation">
  <li><a href="#0">Введение</a></li>
  <li><a href="#1">ID пикселя ВКонтакте</a></li>
  <li><a href="#2">Мэппинг событий</a></li>
  <li><a href="#3">Мэппинг событий (устаревшая версия)</a></li>
  <li><a href="#4">ID прайс-листа по умолчанию для динамического ретаргетинга</a></li>
</ul>


### <a name="0"></a>Введение
------
С помощью SegmentStream можно полностью интегрировать Vkontakte с вашим сайтом.

>Vkontakte поддерживает 2 версии API, поэтому в интерфейсе SegmentStream есть настройки как для новой так и для старой версий.

Чтобы настроить интеграцию с Vkontakte:
1. Авторизуйтесь на сайте [segmentstream.com](https://admin.segmentstream.com/) и перейдите к панели управления интеграциями
2. Войдите на вкладку "Интеграции" и кликните по блоку с логотипом Vkontakte.
3. В открывшейся панели - настройте интеграцию.

![](/img/integrations.vkontakte.1.png)

Подробнее о настройках вы можете прочитать ниже.


### <a name="1"></a>ID пикселя ВКонтакте
------
Идентификатор Пикселя Vkontakte вы можете найти в разделе Vkontakte: Реклама > Таргетинг > Ретаргетинг > Пиксели.

![](/img/integrations.vkontakte.2.png)
![](/img/integrations.vkontakte.3.png)

Скопируйте идентификатор и вставьте его в поле "ID пикселя ВКонтакте" окна настроек интеграции.

### <a name="2"></a>Мэппинг событий
------
SegmentStream может передавать любые события в Vkontakte.
Чтобы настроить передачу событий, заполните 2 поля:
1. Слева - Название события, которое добавляется в массив `digitalData.events`, например: [Registered](/ru/events/registered)
2. Справа - Название события, которое вы хотите видеть в интерфейсе Vkontakte.

Вы можете добавить неограниченное количество событий.

[Справка Vkontakte по Событиям](https://vk.com/dev/openapi_3?f=7.%2B%D0%A0%D0%B5%D1%82%D0%B0%D1%80%D0%B3%D0%B5%D1%82%D0%B8%D0%BD%D0%B3%2B%D0%B2%2BOpen%2BAPI)

### <a name="3"></a>Мэппинг событий (устаревшая версия)
------
В устаревшей версии API под каждое событие в интерфейсе vkontakte нужно создать специальный трекер.
Чтобы настроить передачу событий в эти трекеры, заполните 2 поля:
1. Слева - Название событие, которое добавляется в массив `digitalData.events`, например: [Completed Transaction](/ru/events/completed-transaction)
2. Справа - URL трекера из интерфейса Vkontakte.

### <a name="4"></a>ID прайс-листа по умолчанию для динамического ретаргетинга
------
Для корректной работы модуля динамического ретаргетинга необходимы следующие события:
* [Viewed Page](/ru/events/viewed-page)
* [Viewed Product Detail](/ru/events/viewed-product-detail)
* [Viewed Product Listing](/ru/events/viewed-product-listing)
* [Searched Products](/ru/events/searched-products)
* [Added Product](/ru/events/added-product)
* [Added Product to Wishlist](/ru/events/added-product-to-wishlist)
* [Removed Product](/ru/events/removed-product)
* [Removed Product from Wishlist](/ru/events/removed-product-from-wishlist)
* [Started Order](/ru/events/started-order) (не обязательно)
* [Added Payment Info](/ru/events/added-payment-info) (не обязательно)
* [Completed Transaction](/ru/events/completed-transaction)

>Динамический ретаргетинг работает только с новой версией пикселя.

Для корректной работы системы необходимо указать идентификатор прайс-листа. Укажите 1, если цены на вашем сайте не меняются от региона к региону.

Если цены зависят от региона, сделайте дополнительную настройку во вкладке "Переменные событий":
 - В поле "имя переменной" напишите `priceListId`
 - Поле "Название события" оставьте пустым. Это значит, что для любого события будет использован нестандартный прайс-лист
 - В поле "Функция, которая заполняет значение переменной" напишите функцию, которая в зависимости от региона пользователя возвращает соответствующее значение прайс-листа.
 - Нажмите кнопку "Сохранить"

 ![](/img/integrations.vkontakte.4.png)