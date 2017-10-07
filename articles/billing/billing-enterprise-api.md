---
title: "Выставление счетов Enterprise API-интерфейсы aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello API отчетов, которые программным образом включить корпоративных клиентов toopull потребления данных Azure."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Обзор API- интерфейсов отчетов для корпоративных клиентов
Hello Reporting API позволяют корпоративных клиентов tooprogrammatically запросу подписка Azure и выставления счетов в средства анализа предпочтительным. 

## <a name="enabling-data-access-toohello-api"></a>Включение toohello API-Интерфейс
* **Создать или получить ключ hello API** - журнал toohello корпоративного портала и выполните hello учебника в разделе справки - API для сбора. Hello первый раздел находится в этой справочной статье объясняется, как toogenerate или получить ключ hello API для hello указанном регистрации.
* **Передача ключей в hello API** -hello API-ключ должен toobe, переданный для каждого вызова для проверки подлинности и авторизации. Hello следующие свойства должны заголовки toohello HTTP toobe

|Ключ заголовка запроса | Значение|
|-|-|
|Авторизация| Укажите значение hello в следующем формате: **bearer {API_KEY}** <br/> Пример: bearer eyr....09|

## <a name="consumption-apis"></a>Интерфейсы API потребления
Доступен конечной точки Swagger [здесь](https://consumption.azure.com/swagger/ui/index) hello интерфейсов API, описанных ниже которого следует включить легко интроспекции hello API и hello возможность toogenerate клиентских SDK с помощью [AutoRest](https://github.com/Azure/AutoRest) или [ Swagger CodeGen](http://swagger.io/swagger-codegen/). С 1 мая 2014 г. данные доступны через этот API. 

* **Сводка и баланс** - hello [баланс и Сводка API](billing-enterprise-api-balance-summary.md) предлагает ежемесячные сводку сведений о сальдо, новый покупок, плата за Azure Marketplace, корректировки и избыточные расходы.

* **Сведения об использовании** - hello [API сведений об использовании](billing-enterprise-api-usage-detail.md) предлагает ежедневного декомпозиция обрабатываемом количеств и оценка расходов по регистрации. результат Hello также содержатся сведения о экземпляров, показателей и отделах. можно запрашивать Hello API периода выставления счетов или указанными датами начала и окончания. 

* **Издержки магазина Marketplace** - hello [API платы магазина Marketplace](billing-enterprise-api-marketplace-storecharge.md) возвращает декомпозиции расходов на основе использования marketplace hello за день для указанной hello период выставления счетов или даты начала и окончания (сборов за один раз, не включены) .

* **Прайс-лист** - hello [цена лист API](billing-enterprise-api-pricesheet.md) предоставляет hello применимые скорость для каждого индикатора для регистрации и выставления счетов за период hello. 

## <a name="helper-apis"></a>Интерфейсы API вспомогательного приложения
 **Список периодов выставления счетов** - hello [выставления счетов за периоды API](billing-enterprise-api-billing-periods.md) возвращает список периодов, которые имеют данные потребления для регистрации, указанной в обратном хронологическом порядке hello выставления счетов. Для каждого периода содержит свойство, указывающее toohello API маршрута для hello четырех наборов данных - BalanceSummary, UsageDetails, о расходах в Marketplace и прайс-листа.


## <a name="api-response-codes"></a>Коды ответов API  
|Код состояния отклика|Сообщение|Описание|
|-|-|-|
|200| ОК|Без ошибок|
|401| Не авторизовано| Ключ API не найден, недопустимый формат, срок действия истек и т. д.|
|404| Рекомендации недоступны| Не найдена конечная точка отчетов|
|400| Ошибка запроса| Недопустимые параметры — диапазоны дат, числа EA и т. д.|
|500| Ошибка сервера| Непредвиденная ошибка при обработке запроса| 









