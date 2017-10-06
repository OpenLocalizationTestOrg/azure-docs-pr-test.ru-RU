---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Предварительная документация для функции hello синонимы (Предварительная версия), отображаемые в hello REST API поиска Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Synonyms в Поиске Azure (предварительная версия)

Синонимы в поисковых системах связать эквивалентные термины, которые неявно расширить область hello запроса, без необходимости предоставить термин hello tooactually пользователя hello. Например заданного hello термин «dog» и взаимосвязи синонимов «овчарка» и «малышку в продажу», документы, содержащие «dog», «овчарка» или «малышку в продажу» будет попадают в области hello hello запроса.

В Поиске Azure добавление синонимов выполняется во время обработки запроса. Вы можете добавить синоним maps tooa службы с операциями tooexisting без перебоев в работе. Можно добавить **synonymMaps** определение поля tooa свойства без необходимости toorebuild hello индекса. Дополнительные сведения см. в статье [Update Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index) (Обновление индекса (REST API службы Поиска Azure)).

## <a name="feature-availability"></a>Доступность функций

синонимы Hello компонент в настоящий момент в Предварительный просмотр и поддерживается в только hello последнюю версию api предварительной версии (api-version = 2016-09-01-Preview). Портал Azure такую поддержку пока не предоставляет. Поскольку при запросе hello указана версия hello API, он является возможные toocombine общедоступной (GA) и API предварительной версии в hello то же приложение. Тем не менее предварительные версии API не регулируются соглашением об уровне обслуживания, и их возможности могут измениться, поэтому мы не рекомендуем использовать их в рабочих приложениях.

## <a name="how-toouse-synonyms-in-azure-search"></a>Как поиск toouse синонимы в Azure

В поиске Azure поддержка синонимов основан на синоним maps определение и tooyour служба отправки. Эти карты представляют собой независимый ресурс (как индексы или источники данных) и могут использоваться любым полем, поддерживающим поиск, в любом индекс в службе поиска.

Карты синонимов и индексы обслуживаются независимо друг от друга. После определения схемы синонима и tooyour служба отправки функции hello синоним для поля можно включить, добавив новое свойство с именем **synonymMaps** в определение поля hello. Создание, обновление и удаление карты синоним всегда равно операции целого документа, это означает, что нельзя создать, обновить или удалять части карты синоним hello постепенно. Для обновления даже одной записи требуется перезагрузка.

Внедрение синонимов в приложение поиска состоит из двух этапов:

1.  Добавление службы поиска tooyour синоним карты через API-интерфейсы ниже hello.  

2.  Настройка соответствия синоним hello toouse для поиска полей в определение индекса hello.

### <a name="synonymmaps-resource-apis"></a>Интерфейсы API ресурсов SynonymMaps

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Добавить или обновить кату синонимов в службе можно с помощью запроса POST или PUT.

Синоним maps передаются службе toohello с помощью POST или PUT. Каждое правило должны быть разделены hello символ новой строки («\n»). Можно определить too5, 000 правил для каждой карты синонима в бесплатной службы и 10 000 правил во всех SKU. Каждое правило может находиться до too20 расширения.

В этой предварительной версии maps синоним должен быть в формате hello Apache Solr, который описывается ниже. Если существующий словарь синонима в другом формате и хотите toouse ее напрямую, сообщите нам об этом на [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

Можно создать новую карту синоним, с помощью HTTP POST, как следующий пример hello.

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

Кроме того можно использовать PUT и указать имя синонима hello на hello URI. Если карта синоним hello не существует, он будет создан.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Формат синонимов Apache Solr

Формат Solr Hello поддерживает синоним эквивалентны, явные сопоставления. Правила сопоставления придерживаться открытой toohello синоним спецификацию фильтра Solr Apache, описанные в этом документе: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Ниже приведен пример правила для эквивалентных синонимов.
```
              USA, United States, United States of America
```

С правилом hello выше, запрос поиска «США» будет расширяться слишком «США» или «Соединенные Штаты» или «США».

Явное сопоставление обозначается стрелкой "=>". При указании последовательность термин поискового запроса, который соответствует hello левой части «= >» будет заменена альтернативы hello hello правой стороны. Имея hello снизу, поисковые запросы «Вашингтон», «Штат Вашингтон.» или «WA» будет все переписать слишком «WA». Явное сопоставление только применяется в указанном направлении hello и не перезаписывает hello запроса «WA» слишком «Вашингтон», в данном случае.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Вывод карт синонимов в службе.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Получение карты синонимов в службе.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Удаление карты синонимов в службе.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Настройка соответствия синоним hello toouse для поиска полей в определение индекса hello.

Новое свойство поля **synonymMaps** может быть используется toospecify toouse карты синоним для поля с возможностью поиска. Синоним карты являются ресурсами уровня службы и позволяет ссылаться на любое поле в рамках службы hello индекса.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** могут быть указаны для поиска полей типа hello «Edm.String» или «Collection(Edm.String)».

> [!NOTE]
> В этой предварительной версии можно использовать только одну карту синонимов на поле. Если вы хотите toouse несколько карт синоним, сообщите нам на [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Влияние синонимов на другие функции поиска

функция синонимы Hello перезаписывает hello исходного запроса с синонимами с hello оператор OR. По этой причине попаданий выделение и профили оценки обрабатывают исходный термин hello и синонимы как эквивалентные.

Функция синоним применяется toosearch запросы и не применяется toofilters или аспекты. Аналогичным образом предложения основаны только на исходный термин hello; Синоним совпадения не отображаются в ответ hello.

Синоним расширения неприменимы условия поиска toowildcard; префикс, Нечеткий и регулярное выражение условия не преобразуются.

## <a name="tips-for-building-a-synonym-map"></a>Советы по созданию карты синонимов

- Краткая и хорошо спроектированная карта синонимов намного эффективнее, чем всеобъемлющий список возможных совпадений. Чрезмерно больших или сложных словари занять больше времени, tooparse и влияет на задержку hello запроса, если запрос hello разворачивается toomany синонимы. Вместо предположения, в котором могут использоваться термины, могут получать фактические условия hello через [поиска отчет об анализе трафика](search-traffic-analytics.md).

- В качестве упражнения проверки и предварительно включить и затем использовать этот отчет tooprecisely определить, какие условия будет преимущества соответствие синонима, а затем продолжить toouse его как проверки, что ваша карта синоним зарегистрировавшем лучшие показатели. В отчете hello предопределенные hello плитки «наиболее общие запросы поиска» и «запросов нулевой результат поиска» даст hello необходимые сведения.

- Можно создать несколько карт синонимов для приложения поиска (например, для разных языков, если приложение поддерживает многоязычную базу клиентов). В настоящее время поле может использовать только одну карту. Свойство synonymMaps поля можно обновить в любое время.

## <a name="next-steps"></a>Дальнейшие действия

- При наличии существующего индекса в среде разработки (нерабочей) Поэкспериментируйте с toosee небольшой словарь как hello Добавление синонимов изменяется hello поисковый интерфейс, включая влияние на профили оценки, попаданий выделение и предложения.

- [Включить аналитику трафика службы поиска](search-traffic-analytics.md) и hello использование стандартного отчета Power BI, какие термины toolearn hello большинство и какие другие возвращаемого документы. Используя эти знания, пересмотрите hello словарь tooinclude синонимы для производительности запросов, которые должны разрешения toodocuments в индексе.
