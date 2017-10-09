---
title: "aaaHow toouse Fiddler tooevaluate и тестирования интерфейсы REST API поиска Azure | Документы Microsoft"
description: "Использование Fiddler для доступности службы поиска Azure tooverifying подход написания кода и ознакомление hello API-интерфейсов REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>С помощью Fiddler tooevaluate и тестирования интерфейсы REST API поиска Azure
> [!div class="op_single_selector"]
>
> * [Обзор](search-query-overview.md)
> * [Обозреватель поиска](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

В этой статье объясняется, как toouse Fiddler, доступной в качестве [бесплатно загрузить с Telerik](http://www.telerik.com/fiddler), tooissue HTTP запросы tooand просмотреть ответы с помощью hello REST API поиска Azure без необходимости toowrite любой код. Поиск Azure — это полностью управляемая облачная служба поиска в Microsoft Azure с простым программным управлением через API-интерфейсы REST и .NET. Hello описаны на API-интерфейс REST службы поиска Azure [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

Привет, выполнив действия будет создать индекс, отправлять документы, индекс hello запросов и запроса hello системы сведения о службах.

Эти шаги toocomplete, вам потребуется службы поиска Azure и `api-key`. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) инструкции о том, как tooget работы.

## <a name="create-an-index"></a>Создание индекса
1. Запустите Fiddler. На hello **файл** меню выберите Отключить **запись трафика** toohide лишние HTTP действий, которые являются несвязанными toohello текущей задачи.
2. На hello **Composer** вкладке будет сформулировать запрос, который выглядит как следующий снимок экрана приветствия.

      ![][1]
3. Выберите **PUT**.
4. Введите URL-адрес, на который указывает URL-адрес службы hello, атрибуты запроса и hello api-version. Несколько tookeep указателей помните:

   * Используйте HTTPS в качестве префикса hello.
   * Атрибут запроса: "/indexes/hotels". Это заставляет toocreate поиска индекс с именем «гостиницы».
   * Версия API вводится строчными буквами, в виде "?api-version=2016-09-01". Версии API имеют важное значение, так как обновления Поиска Azure разворачиваются на регулярной основе. В редких случаях обновление службы может вызвать критические изменения toohello API. Поэтому службе поиска Azure требуется версия API каждого запроса, чтобы вы могли полностью контролировать используемый запрос.

     Hello полный URL-адрес должен выглядеть примерно toohello следующий пример.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Укажите заголовок запроса hello, заменив значения, которые являются допустимыми для службы узла hello и ключ api.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. В текст запроса вставьте hello поля, составляющие определение индекса hello.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. Нажмите **Execute (Выполнить)**.

Через несколько секунд появится ответ HTTP 201 в список сеансов hello, возвращающее hello индекс был создан успешно.

Если вы получаете HTTP 504, убедитесь, что hello URL-адрес указывает протокол HTTPS. Если вы видите HTTP 400 или 404, tooverify тело запроса hello Проверьте наличие были без ошибок копирования и вставки. HTTP 403 обычно указывает на проблему с hello ключ api (недопустимый ключ или синтаксис неполадки как указывается hello api ключ).

## <a name="load-documents"></a>Загрузка документов
На hello **Composer** , документы toopost запрос будет выглядеть вкладка hello следующее. текст Hello hello запроса содержит данные поиска hello отелях 4.

   ![][2]

1. Выберите **POST**.
2. Введите URL-адрес, начинающийся с HTTPS, далее URL-адрес вашей службы, а затем "/indexes/<'indexname'>/docs/index?api-version=2016-09-01". Hello полный URL-адрес должен выглядеть примерно toohello следующий пример.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. Заголовок запроса должен быть hello же как и раньше. Помните, заменить узла hello и ключ api со значениями, которые являются допустимыми для службы.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hello текст запроса содержит четыре документы toobe добавлены toohello гостиницы индекса.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. Нажмите **Execute (Выполнить)**.

Через несколько секунд появится ответ HTTP 200 в список сеансов hello. Это указывает на приветствия документы успешно создан. Если вы получаете 207, по крайней мере один документ сбой tooupload. Если код 404, имеется синтаксическая ошибка в hello заголовок или текст запроса hello.

## <a name="query-hello-index"></a>Индекс hello запросов
После загрузки индекса и документов можно формировать запросы к ним.  На hello **Composer** вкладке **получить** команду, которая запрашивает службы будет выглядеть аналогично toohello следующий снимок экрана.

   ![][3]

1. Выберите **GET**.
2. Введите URL, начинающийся с HTTPS, далее URL вашей службы, далее "/indexes/<'indexname'>/docs?", далее параметры запроса. В качестве примера используйте hello URL-адреса, заменив имя узла образец hello допустимый для службы.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Этот запрос выполняет поиск по hello термин «motel» и извлекает аспект категории для оценки.
3. Заголовок запроса должен быть hello же как и раньше. Помните, заменить узла hello и ключ api со значениями, которые являются допустимыми для службы.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

код ответа Hello должен 200 и hello ответа вывод должен выглядеть примерно toohello следующий снимок экрана.

   ![][4]

Hello следующий пример взят из hello [операцию поиска индекса (API поиска Azure)](http://msdn.microsoft.com/library/dn798927.aspx) на сайте MSDN. Многие примеры запросов hello в этом разделе содержат пробелы, которые не разрешены в Fiddler. Замените каждый пространства с символ «+» перед вставкой в hello строку запроса перед выполнением запроса hello в Fiddler.

**До замены пробелов:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**После замены пробелов символом +:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>Система hello запроса
Можно также запросить hello системы tooget счетчики и хранения использование документов. На hello **Composer** , ваш запрос будет выглядеть примерно следующее toohello, а hello ответе возвращается число для hello число документов и используемого пространства.

 ![][5]

1. Выберите **GET**.
2. Введите URL, включающий URL-адрес вашей службы, а затем "/indexes/hotels/stats?api-version=2016-09-01":

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Укажите заголовок запроса hello, заменив значения, которые являются допустимыми для службы узла hello и ключ api.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Текст запроса hello оставьте пустым.
5. Нажмите **Execute (Выполнить)**. Вы увидите код состояния HTTP 200 в список сеансов hello. Выберите запись hello учтена для вашей команды.
6. Нажмите кнопку hello **инспекторы** щелкните hello **заголовки** вкладку и hello, а затем выберите формат JSON. Вы увидите hello документа число и размер для хранения (в КБ).

## <a name="next-steps"></a>Дальнейшие действия
В разделе [управление службой поиска в Azure](search-manage.md) toomanaging подход без кода и использования службы поиска Azure.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
