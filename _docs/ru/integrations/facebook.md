---
layout: page
section: integrationsRU
title: "Facebook"
order: 1
---

В данном разделе вы узнаете:
* Как установить пиксель Facebook на ваш сайт.
* Как подключить динамический ретаргетинг в Facebook.
* Как настроить передачу кастомных событий в Facebook.

Facebook - социальная сеть с большим набором рекламных инструментов. Facebook показывает объявления в ленте новостей своих пользователей включая динамический ретаргетинг. SegmentStream позволяет отправлять данные о поведении ваших пользователей в [Facebook Pixel](https://developers.facebook.com/docs/facebook-pixel/api-reference#events).

### Навигация по странице
------
<ul class="page-navigation">
  <li><a href="#0">Введение</a></li>
  <li><a href="#1">Необходимые события</a></li>
  <li><a href="#2">Идентификатор Facebook Pixel</a></li>
  <li><a href="#2_1">Используется фид с группами товаров</a></li>
  <li><a href="#2_2">Передавать стоимость товаров в параметр value событий</a></li>
  <li><a href="#3">Пользовательские события</a></li>
  <li><a href="#4">Проверка корректности настройки интеграции</a></li>
</ul>

### <a name="0"></a>Введение
------
С помощью SegmentStream можно полностью интегрировать Facebook с вашим сайтом: стандартные и уникальные события

[Справка Facebook по интеграции с сайтом](hhttps://developers.facebook.com/docs/facebook-pixel/api-reference)

Чтобы настроить интеграцию с Facebook:
1. Авторизуйтесь на сайте [segmentstream.com](https://admin.segmentstream.com/) и перейдите к панели управления интеграциями
2. Войдите на вкладку "Интеграции" и кликните по блоку с логотипом Facebook.
3. В открывшейся панели - настройте интеграцию.
![](/img/integrations.facebook.1.png)

Подробнее о настройках вы можете прочитать ниже.

### <a name="1"></a>Необходимые события
------
Для корректной работы интеграции вашего сайта с Facebook - необходимо настроить передачу 3-х событий в массив `digitalData.events`. Список событий приведен ниже:

**Обязательные события**
* [Viewed Page](/ru/events/viewed-page)
* [Viewed Product Detail](/ru/events/viewed-product-detail)
* [Completed Transaction](/ru/events/completed-transaction)

### <a name="2"></a>Идентификатор Facebook Pixel
------
Идентификатор Пикселя Facebook вы можете найти в разделе facebook: Управление Рекламой > Все инструменты > Пиксели.

![](/img/integrations.facebook.2.png)

Скопируйте идентификатор и вставьте его в поле "Идентификатор Facebook Pixel" окна настроек интеграции.

### <a name="2_1"></a>Используется фид с группами товаров
------
Facebook получает информацию о товарах, размещенных на сайте через XML-фид. С определенной периодичностью робот Facebook скачивает фид с вашего сервера. Такой фид содержит информацию о всех товарах, представленных на сайте.

[Подробнее о формате фида](https://support.google.com/merchants/answer/7052112)

Для корректной работы интеграции, Facebook также должен получать информацию о взаимодействии пользователей с товарами на сайте - просмотры, добавления в корзину, покупки и т.д. Система должна правильно сопоставить то, что она видит в поступающих событиях с XML-фидом.

[Подробнее о группировке товара](https://support.google.com/merchants/answer/6324507)

 -Если вы используете группировку товаров с помощью параметра xml-фида `item_group_id` - обязательно активируйте данную настройку.
  >В данном случае id товара из Вашего XML-фида должен совпадать с `product.skuCode`. Обязательно передавайте `product.skuCode` и `product.id` в каждом объекте `product`.

 -Если вы НЕ используете группировку товаров с помощью параметра xml-фида `item_group_id` - Не активируйте данную настройку.
  >В данном случае id товара из Вашего XML-фида должен совпадать с `product.id` объекта `digitalData`

### <a name="2_2"></a>Передавать стоимость товаров в параметр value событий
------
По-умолчанию вместе с событием `Viewed Product Detail` SegmentStream не передает цену товара в параметре `value`. В документации Facebook написано, что value - это ценность события, но не стоимость товара.
Если же вы хотите передавать стоимость товара в переменную `value` - включите данную настройку. Валюта из переменной `product.currency` также автоматически начнет передаваться.


### <a name="3"></a>Пользовательские события
------
SegmentStream наравне со стандартными событиями может передавать и кастомные события в Facebook.
Чтобы настроить передачу кастомных событий заполните 2 поля:
1. Слева - Название событие, которое добавляется в массив `digitalData.events`, например: [Registered](/ru/events/registered)
2. Справа - Название события, которое вы хотите видеть в интерфейсе Facebook.

> Название события в Facebook вы можете выбирать на свое усмотрение, однако мы рекомендуем придерживаться правил наименования самого Facebook. Facebook использует CamelCase формат.

Вы можете добавить неограниченное количество кастомных событий

### <a name="4"></a>Проверка корректности настройки интеграции
------
После настройки интеграции в интерфейсе SegmentStream, но ДО ПУБЛИКАЦИИ - перейдите на сайт в режиме test_mode, [пройдитесь по воронке конверсии и проверьте, нет ли ошибок](/ru/for-analyst/integrations#2).
Если ошибок нет - опубликуйте текущую версию.