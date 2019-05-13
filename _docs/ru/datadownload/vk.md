---
layout: page
section: datadownloadRU
title: "Vkontakte"
order: 1
---

>ВНИМАНИЕ! Для активации данного функционала необходимо включить и настроить интеграцию DDManager Streaming.

### Импорт данных из VK

Подключение данного источника данных позволяет раз в 24 часа импортировать информацию о расходах за последние 7 дней в Google BigQuery.

Данная интеграция доступна как для обычных рекламодателей, так и для рекламных агентств.

### Подключение и настройка

![](/img/vk.1.png)

Для того, чтобы включить этот источник данных, необходимо перейти в раздел "DATA IMPORTS → Automatic" (1), выбрать источник данных (2) и авторизоваться (3)

![](/img/vk.2.png)

Данная интеграция имеет одну обязательную настройку "Account ID" (1), ниже вы можете узнать где взять данный параметр.

>Рекламные агентства должны заполнить дополнительное поле "Client ID" (2), это id вашего клиента, данные которого необходимо выгружать. Ниже находится инструкция по получению данного параметра.

Чтобы сохранить и включить источник данных нажмите на "Save" (3).

Кнопка "Disconnect" (4) необходима для того, чтобы отозвать авторизационные данные. Настройки при этом сохраняются.

### Получение Account ID

Для того, чтобы узнать свой Account ID, необходимо авторизоваться в [vk.com](vk.com) под своим аккаунтом, который имеет доступ к необходимому рекламному кабинету.

Перейдите по ссылке [https://vk.com/ads?act=settings](https://vk.com/ads?act=settings) и скопируйте строку, которая указана на скриншоте ниже (1)

![](/img/vk.3.png)

### Получение Client ID

В рекламном кабинете [https://vk.com/ads?act=office](https://vk.com/ads?act=office) необходимо необходимо перейти в раздел "Центр клиентов" (1) и кликнуть нужному клиенту (2). В текущем URL будет находиться необходимое нам значение в параметре union_id. 

Пример: [https://vk.com/ads?act=office&union_id={client_id}](https://vk.com/ads?act=office&union_id={client_id})

![](/img/vk.4.png)

### Куда попадают данные о расходах на рекламу

Данные в BigQuery будут записаны в таблицу с именем **vkCosts_{CLIENT_ID}_ {DATE}**. И в **vkCosts_{ACCOUNT_ID}_ {DATE}** для обычных рекламодателей.

### Структура таблицы


Field name|Type|Mode
--- | --- | ---
cost | FLOAT | REQUIRED
clicks | INTEGER | NULLABLE
impressions | INTEGER | NULLABLE
utmTerm | STRING | NULLABLE
utmCampaign | STRING | NULLABLE
utmContent | STRING | NULLABLE
utmMedium | STRING | NULLABLE
utmSource | STRING | NULLABLE
currency | STRING | NULLABLE