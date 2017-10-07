---
title: "Операции с индексаторами (REST API службы поиска Azure: версия 2015-02-28-Preview) | Документация Майкрософт"
description: "Операции с индексаторами (API REST службы \"Поиск Azure\": версия 2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Операции с индексаторами (API REST службы "Поиск Azure": версия 2015-02-28-Preview)
> [!NOTE]
> В этой статье описывается индексаторы в hello [2015-02-28-Preview REST API](search-api-2015-02-28-preview.md). В этой версии API добавлены предварительные версии индексатора хранилища BLOB-объектов Azure с извлечением документов и индексатора хранилища таблиц Azure, а также другие улучшения. Hello API также поддерживает общедоступной (версии GA) индексаторы, включая индексаторы для базы данных SQL Azure, SQL Server на виртуальных машинах Azure и Azure Cosmos DB.
> 
> 

## <a name="overview"></a>Обзор
Поиск Azure можно интегрировать непосредственно с некоторыми общими источниками данных, удаление toowrite кода hello необходимость tooindex данных. tooset этого можно вызвать API поиска Azure toocreate hello и управление **индексаторы** и **источники данных**. 

**Индексатор** — это ресурс, соединяющий источники данных с целевыми индексами поиска. Индексатор, который используется в hello следующих способов: 

* Выполнение однократного копирования данных hello toopopulate индекса.
* Синхронизация индекса с изменениями в источнике данных hello по расписанию. Hello расписание является частью определения индексатора hello.
* Вызов по требованию tooupdate индекс по мере необходимости. 

**Индексатора** полезно, если требуется регулярное обновление tooan индекса. Можно настроить встроенное расписание как часть определения индексатора или запустить его по запросу, используя операцию [Запуск индексатора](#RunIndexer). 

Объект **источника данных** указывает, какие данные должны toobe индексировать, учетные данные tooaccess hello данных и политики tooenable поиска Azure tooefficiently выявления изменений в данных hello (таких, как изменить или удаленные строки в таблицу базы данных). Он определяется как независимый ресурс, который могут использовать несколько индексаторов.

в настоящее время поддерживаются следующие источники данных Hello:

* **База данных SQL Azure** и **SQL Server на виртуальных машинах Azure**. Пошаговое руководство для целевых платформ см. в [этой статье](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Пошаговое руководство для целевых платформ см. в [этой статье](search-howto-index-documentdb.md). 
* **Хранилища больших двоичных объектов Azure**, в том числе следующие hello документов форматы: PDF, Microsoft Office (DOCX/DOC, XSLX и XLS, PPTX и PPT, MSG), HTML, XML, ZIP и текстовых файлов (включая JSON). Пошаговое руководство для целевых платформ см. в [этой статье](search-howto-indexing-azure-blob-storage.md).
* **Хранилище таблиц Azure.** Пошаговое руководство для целевых платформ см. в [этой статье](search-howto-indexing-azure-tables.md).

Мы рассматриваем, добавляя поддержку дополнительных источников данных в будущем hello. toohelp нам определить приоритеты этих решений, оставьте свой отзыв на hello [форуме отзывов по поиску Azure](http://feedback.azure.com/forums/263029-azure-search).

В разделе [ограничения служб](search-limits-quotas-capacity.md) для источника данных и tooindexer связанные ресурсы ограничивает максимальное.

## <a name="typical-usage-flow"></a>Типичные рабочий процесс
Можно создавать индексаторы и источники данных, а также управлять ими через простые HTTP-запросы (POST, GET, PUT, DELETE) к заданному ресурсу `data source` или `indexer`.

Настройка автоматического индексирования обычно состоит из четырех этапов.

1. Определите источник данных hello, содержащий hello данные, необходимые индексированных toobe. Имейте в виду, что поиск Azure могут не поддерживать все типы данных hello присутствуют в источнике данных. В разделе [поддерживаемые типы данных](https://msdn.microsoft.com/library/azure/dn798938.aspx) список hello.
2. Создайте индекс Поиска Azure, схема которого совместима с источником данных.
3. Создайте источник данных для Поиска Azure, как описано в разделе [Создание источника данных](#CreateDataSource).
4. Создайте индексатор Поиска Azure, как описано в разделе [Создание индексатора](#CreateIndexer).

Для каждой комбинации целевого индекса и источника данных необходимо запланировать создание одного индексатора. У вас есть несколько индексаторов, записывающих в hello же индекс и можно повторно использовать hello одного источника данных для нескольких индексаторов. Однако индексатор один источник данных может использовать только одновременно и может записывать только один индекс tooa. 

После создания индексатора можно получить его состояния выполнения, с помощью hello [Получение состояния индексатора](#GetIndexerStatus) операции. Можно также запустить индексатор в любое время (вместо или в дополнение toorunning он периодически по расписанию) с помощью hello [запуска индексатора](#RunIndexer) операции.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Создание источника данных
В поиске Azure источника данных используется с индексаторы, предоставляя сведения о соединении hello для нерегламентированных или запланированное обновление данных целевой индекс. Для создания источника данных в службе поиска Azure используется запрос HTTP POST.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Кроме того можно использовать PUT и указать имя источника данных hello на hello URI. Если hello источника данных не существует, он будет создан.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> Hello максимальное количество источников данных зависит от цен. Hello бесплатная служба позволяет создавать too3 источников данных. Стандартная служба позволяет использовать до 50 источников данных. Подробные сведения можно найти в разделе [Ограничения службы](search-limits-quotas-capacity.md) .
> 
> 

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Hello **Создание источника данных** можно составить запрос с помощью метода POST или PUT. При использовании POST необходимо указать имя источника данных в тексте запроса hello вместе с hello определение источника данных. С помощью метода PUT hello имя является частью URL-адрес hello. Если источник данных hello не существует, он создается. Если он уже существует, это новое определение обновленных toohello. 

Имя источника данных Hello должен состоять из строчных букв, начинаться с буквы или цифры, иметь нет символы косой черты или точек и быть не длиннее 128 символов. После имени источника данных hello начиная с буквы или цифры, hello остальная часть имени hello может включать любой буквы, числа и дефисы, при условии, что hello дефисы не являются последовательными. Подробные сведения приведены в статье [Правила именования (Поиск Azure)](https://msdn.microsoft.com/library/azure/dn857353.aspx) .

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`.

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов. 

* `Content-Type`: обязательный параметр. Установите это слишком`application/json`
* `api-key`: обязательный параметр. Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **Создание источника данных** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса). 

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на hello [портала Azure](https://portal.azure.com/). В разделе [Создание службы поиска на портале hello](search-create-service-portal.md) для справки о навигации по странице.

<a name="CreateDataSourceRequestSyntax"></a>
**Синтаксис текста запроса**

текст Hello hello запроса содержит определение источника данных, которая включает тип источника данных hello, данных hello tooread учетные данные, а также необязательные данные обнаружения изменений и обнаружения удаления данных, определить политики, используемые tooefficiently изменено или удаленные данные в источнике данных hello при использовании с регулярному расписанию индексатор. 

Hello синтаксис для структуризации полезных данных запроса hello выглядит следующим образом. Далее в этом разделе приведен пример запроса.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

Запрос содержит hello следующие свойства: 

* `name`: обязательный параметр. Имя источника данных hello Hello. Имя источника данных должно только содержать строчные буквы, цифры или дефисы, не может начинаться или заканчиваться тире и имеет ограниченный too128 символов.
* `description`: необязательное описание. 
* `type`: обязательный параметр. Должен быть одним из типов источников данных hello поддерживается:
  * `azuresql` — база данных SQL Azure или SQL Server на виртуальных машинах Azure.
  * `documentdb` — Azure Cosmos DB.
  * `azureblob` — хранилище BLOB-объектов Azure.
  * `azuretable` — хранилище таблиц Azure.
* `credentials`:
  * требуется Hello `connectionString` свойство указывает hello строку подключения для источника данных hello. Формат Hello hello строки подключения зависит от типа источника данных hello: 
    * Для Azure SQL это hello обычные строка подключения SQL Server. Если вы используете строку подключения hello Azure портала tooretrieve hello, используйте hello `ADO.NET connection string` параметр.
    * Для Azure Cosmos DB, строка подключения hello должны быть hello следующий формат: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Все значения hello являются обязательными. Их можно найти в hello [портал Azure](https://portal.azure.com/).  
    * Для больших двоичных объектов и хранилище таблиц это строка подключения учетной записи хранилища hello. Формат Hello описан [здесь](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). Необходимо указать протокол конечной точки HTTPS.  
* `container`, требуется: hello tooindex данных, с помощью hello указывает `name` и `query` свойства: 
  * `name`, обязательный.
    * Azure SQL: указывает hello таблицы или представления. Можно использовать имена с указанием через схему, такие как `[dbo].[mytable]`.
    * DocumentDB: Определяет коллекцию hello. 
    * Хранилище больших двоичных объектов Azure: Указывает контейнер хранилища hello.
    * Хранилище таблиц Azure: Указывает имя hello hello таблицы. 
  * `query`, необязательный.
    * DocumentDB: позволяет toospecify запрос, выполняющий сведение произвольного макета документа JSON в плоскую схему, поиск Azure можно индексировать.  
    * Хранилище больших двоичных объектов Azure: можно toospecify создается виртуальная папка, в контейнере больших двоичных объектов hello. Например, для пути больших двоичных объектов `mycontainer/documents/blob.pdf`, `documents` можно использовать в качестве виртуальной папке hello.
    * Хранилище таблиц Azure: позволяет toospecify запроса, что фильтры hello набор строк toobe импортированы.
    * Azure SQL: запрос не поддерживается. Если данная функция необходима, проголосуйте за [это предложение](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Необязательный Hello `dataChangeDetectionPolicy` и `dataDeletionDetectionPolicy` свойства описаны ниже.

<a name="DataChangeDetectionPolicies"></a>
**Политики обнаружения изменения данных**

Назначение данных Hello политику обнаружения изменения tooefficiently определения измененных элементов данных. Поддерживаемые политики зависят от типа источника данных hello. В следующих разделах описывается каждая из политик. 

***Политика обнаружения изменений верхнего предела*** 

Используйте эту политику, если источник данных содержит столбец или свойство, которое удовлетворяет hello следующие условия:

* Все вставки укажите значение для столбца hello. 
* Элемент tooan всех обновлений также изменить значение hello hello столбца. 
* Hello значение этого столбца увеличивается при каждом изменении.
* Запросы, использующие следующий фильтр предложение аналогичные toohello `WHERE [High Water Mark Column] > [Current High Water Mark Value]` могут выполняться эффективно.

Например, при использовании источников данных Azure SQL, индексируемого `rowversion` столбец является hello идеальным для использования с пиковой политике hello. 

Эту политику можно указать следующим образом.

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

При использовании Azure Cosmos DB источников данных, необходимо использовать hello `_ts` свойства, предоставляемые Azure Cosmos DB. 

При использовании источников данных больших двоичных объектов Azure, поиск Azure автоматически использует верхнего предела политику обнаружения изменения по меткам времени последнего изменения большого двоичного объекта; не требуется такой политики toospecify самостоятельно.   

***Встроенная политика определения изменений SQL***

Если база данных SQL поддерживает [отслеживание изменений](https://msdn.microsoft.com/library/bb933875.aspx), мы рекомендуем использовать встроенную политику отслеживания изменений SQL. Эта политика позволяет hello наиболее эффективному отслеживанию изменений и позволяет tooidentify удалены строки поиска Azure без необходимости toohave столбцом явную «обратимое удаление» в схеме.

Интегрированное отслеживание изменений поддерживается начиная с hello следующие версии базы данных SQL Server: 

* SQL Server 2008 R2, если вы используете SQL Server на виртуальных машинах Azure.
* База данных SQL Azure 12, если вы используете базу данных SQL Azure.  

При использовании встроенной политики отслеживания изменений SQL не указывайте отдельную политику обнаружения удаления данных, так как она уже поддерживает выявление удаленных строк. 

Эту политику можно использовать только с таблицами. С представлениями ее использовать невозможно. Необходимо tooenable отслеживание изменений для таблицы hello, которую вы используете, прежде чем использовать эту политику. Инструкции см. в разделе [Включение и отключение отслеживания изменений](https://msdn.microsoft.com/library/bb964713.aspx).    

При структурировании hello **Создание источника данных** запроса SQL встроенную политику отслеживания изменений может быть указан следующим образом:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Политики обнаружения удаления данных**

Hello политику обнаружения удалений данных предназначена tooefficiently определения удаленных элементов данных. В настоящее время поддерживается только hello политики — hello `Soft Delete` политика, которая позволяет идентификации удаленных элементов на основе значения hello `soft delete` столбца или свойства в источнике данных hello. Эту политику можно указать следующим образом.

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Поддерживаются только столбцы, имеющие строковые, целочисленные или логические значения. Здравствуйте, которое используется в качестве `softDeleteMarkerValue` должно быть строкой, даже если соответствующий столбец hello содержит целые или логические значения. Например, если hello значение, которое появляется в источнике данных равен 1, используйте `"1"` как hello `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Примеры текста запроса**

Если источник данных hello toouse с индексатором, который запускается по расписанию, в этом примере показано, как изменить toospecify и удаление политики обнаружения: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Если предполагается только источник данных hello toouse для разового копирования данных hello hello политики можно опустить:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Ответ**

Для успешного запроса: "201 — Создан ресурс". 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Обновление источника данных
Обновить существующий источник данных можно с помощью HTTP-запроса PUT. Необходимо указать имя hello tooupdate источника данных hello hello URI запроса:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`. Дополнительные сведения о других версиях см. в статье [Управление версиями службы поиска Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx).

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Запрос**

Hello синтаксис текста запроса является hello аналогичны [запрашивает создание источника данных](#CreateDataSourceRequestSyntax).

Некоторые свойства в существующем источнике данных нельзя обновить. Например нельзя изменить тип hello существующего источника данных.  

Если вы не хотите строка подключения toochange hello для существующего источника данных, можно указать литерал hello `<unchanged>` для строки подключения hello. Это полезно в ситуации, когда требуется tooupdate источника данных, но не иметь строку подключения toohello удобный доступ, так как это конфиденциальные данные.

**Ответ**

Для успешного запроса: код состояния "201 Создан ресурс", если источник данных был создан, и "204 Нет содержимого", если был обновлен существующий источник данных.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Список источников данных
Hello **список источников данных** возвращает список источников данных hello в службе поиска Azure. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Для успешного запроса: «200 — ОК».

Вот пример тела запроса:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Обратите внимание, что можно отфильтровать ответ hello вниз toojust hello свойства, которые вас интересуют. Например, если требуется только список имен источников данных, использовать hello OData `$select` параметра запроса:

    GET /datasources?api-version=205-02-28&$select=name

В этом случае ответ hello hello в приведенном выше примере будет выглядеть следующим образом: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Это удобно toosave пропускной способности, если имеется много источников данных в службе поиска.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Получение источника данных
Hello **получить источник данных** операция получает определение источника данных hello из поиска Azure.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

Hello ответ — аналогично tooexamples в [Создание источника данных приводятся примеры запросов](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Не устанавливайте hello `Accept` заголовок запроса слишком`application/json;odata.metadata=none` при вызове этой функции API, как это вызовет `@odata.type` toobe атрибут опущена hello ответа и вы не будет возможности toodifferentiate между изменение данных и данных обнаружения удаления политики применения различных типов. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Удаление источника данных
Hello **удалить источник данных** операция удаляет источник данных из службы поиска Azure.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Если какие-либо индексаторы ссылаются hello источника данных, который необходимо удалить, hello операции удаления все равно будет продолжена. Однако эти индексаторы перейдут в состояние ошибки при их следующем запуске.  
> 
> 

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "204 — Нет содержимого".

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Создание индексатора
Для создания индекса в службе поиска Azure используется запрос HTTP POST.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Кроме того можно использовать PUT и указать имя источника данных hello на hello URI. Если hello источника данных не существует, он будет создан.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> Максимальное количество допустимых индексаторов Hello зависит от ценового уровня. Hello бесплатная служба позволяет создавать копии too3 индексаторов. Стандартная служба позволяет использовать до 50 индексаторов. Подробные сведения можно найти в разделе [Ограничения службы](search-limits-quotas-capacity.md) .
> 
> 

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

<a name="CreateIndexerRequestSyntax"></a>
**Синтаксис текста запроса**

текст Hello hello запроса содержит определение индексатора, который указывает источник данных hello и hello целевой индекс для индексирования, а также необязательное расписание индексирования и параметры. 

Hello синтаксис для структуризации полезных данных запроса hello выглядит следующим образом. Далее в этом разделе приведен пример запроса.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Расписание индексатора**

Индексатор может дополнительно задавать расписание. Если расписание присутствует, индексатор hello будет запускаться периодически по этому расписанию. Расписание имеет hello следующие атрибуты:

* `interval`: обязательный параметр. Значение длительности, указывающее интервал или период между запусками индексатора. Разрешенная Hello наименьший интервал составляет 5 минут. самая длинная Hello — один день. Значение должно быть отформатировано как значение dayTimeDuration XSD (ограниченное подмножество значения [продолжительности ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). Hello схема выглядит следующим образом: `"P[nD][T[nH][nM]]"`. Примеры: `PT15M` для каждых 15 минут, `PT2H` для каждых 2 часов. 
* `startTime`: обязательный параметр. Дата и время UTC начала запуска индексатора hello. 

**Параметры индексатора**

При необходимости индексатор может указывать несколько параметров, которые влияют на его поведение. Все параметры hello являются необязательными.  

* `maxFailedItems`: hello число элементов, которые не toobe индексации по превышении которого запуск индексатора считается неудачным. Значение по умолчанию — 0. Информация об ошибочных элементах возвращается hello [Получение состояния индексатора](#GetIndexerStatus) операции. 
* `maxFailedItemsPerBatch`: hello число элементов, которые не toobe индексации в каждом пакете по превышении которого запуск индексатора считается неудачным. Значение по умолчанию — 0.
* `base64EncodeKeys`. Указывает, будут ли ключи документа в кодировке base-64. Поиск Azure накладывает ограничения на символы, которые может содержать ключ документа. Однако hello значений в источник данных может содержать недопустимые символы. Если необходимые tooindex значений, таких как ключи документов, этот флаг можно задать tootrue. Значение по умолчанию — `false`.
* `batchSize`: Указывает hello количество элементов, которые считываются из источника данных hello и индексированных как единый пакет в порядке tooimprove производительности. по умолчанию Hello зависит от типа источника данных hello: 1000 для Azure SQL и Azure Cosmos DB и 10 для хранилища больших двоичных объектов.

**Сопоставления полей**

Можно использовать сопоставления полей toomap имя поля в hello данных источника tooa другое имя поля в индексе назначения hello. Например, рассмотрим исходную таблицу с полем `_id`. Поиск Azure не разрешает имя поля, начиная со знака подчеркивания, поэтому необходимо переименовать поле hello. Это можно сделать с помощью hello `fieldMappings` свойство индексатора hello следующим образом: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Можно задать несколько сопоставлений полей. 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

В исходных и целевых именах полей не учитывается регистр.

<a name="FieldMappingFunctions"></a>
***Функции сопоставления полей***

Сопоставления полей также можно с помощью значения полей источника используется tootransform *сопоставление функций*.

В настоящее время поддерживается только одна такая функция: `jsonArrayToStringCollection`. Выполняет синтаксический анализ к полю, содержащему строки, отформатированной как массив JSON, в поле Collection(EDM.String)) в индексе назначения hello. В частности, эта функция предназначена для использования с индексатором SQL Azure, поскольку в SQL отсутствует собственные тип данных коллекции. Эта функция используется следующим образом. 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Например, если hello исходное поле содержит строку hello `["red", "white", "blue"]`, то hello целевое поле типа `Collection(Edm.String)` будет заполняться значениями hello трех `"red"`, `"white"` и `"blue"`.

Обратите внимание, что hello `targetFieldName` свойство является необязательным; Если опущены, hello `sourceFieldName` используется значение. 

<a name="CreateIndexerRequestExamples"></a>
**Примеры текста запроса**

Hello следующем примере создается индексатор, который копирует данные из таблицы hello ссылается hello `ordersds` toohello источника данных `orders` индекс по расписанию, который начинается 1 января 2015 г. UTC и запускается каждый час. Каждый вызов индексатора будет успешным, если не более 5 элементов не toobe индексации в каждом пакете, и не более 10 элементов не проиндексированы всего toobe. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Ответ**

Успешный запрос возвращает код состояния "201 — Создан ресурс".

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Обновление индексатора
Обновить существующий индексатор можно с помощью HTTP-запроса PUT. Необходимо указать имя индексатора tooupdate hello hello hello URI запроса:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hello `api-version` является обязательным. Текущая версия Hello `2015-02-28`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Запрос**

Hello синтаксис текста запроса является hello аналогичны [запрашивает создание индексатора](#CreateIndexerRequestSyntax).

**Ответ**

Для успешного запроса: возвращается код состояния "201 — Создан ресурс", если индексатор был создан, и "204 — Нет содержимого", если был обновлен существующий индексатор.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Список индексаторов
Hello **список индексаторов** операция возвращает список hello индексаторов в службе поиска Azure. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Hello `api-version` является обязательным. Hello предварительной версии — `2015-02-28-Preview`. Дополнительные сведения о других версиях см. в статье [Управление версиями службы поиска Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx).

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Для успешного запроса: «200 — ОК».

Вот пример тела запроса:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Обратите внимание, что можно отфильтровать ответ hello вниз toojust hello свойства, которые вас интересуют. Например, если требуется только список имен индексаторов, используйте hello OData `$select` параметра запроса:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

В этом случае ответ hello hello в приведенном выше примере будет выглядеть следующим образом: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Это удобно toosave пропускной способности, если у вас много индексаторов в службе поиска.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Получение индексатора
Hello **Get Indexer** операция получает hello определение индексатора из поиска Azure.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` является обязательным. Hello предварительной версии — `2015-02-28-Preview`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

Hello ответ — аналогично tooexamples в [запросы пример создания индексатора](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Удаление индексатора
Hello **удалить индексатор** операция удаляет индексатор из службы поиска Azure.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

При удалении индексатора hello индексатора выполняемые в в это время будет выполняться toocompletion, но не последующие выполнения планироваться. Toouse попыток несуществующий индексатор приведет к получению кода состояния HTTP 404 не найдено. 

Hello `api-version` является обязательным. Hello предварительной версии — `2015-02-28-Preview`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "204 — Нет содержимого".

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Запуск индексатора
В дополнение toorunning периодически по расписанию, индексатор, который также может вызываться по требованию с помощью hello **запуска индексатора** операции: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` является обязательным. Hello предварительной версии — `2015-02-28-Preview`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код «202 — Принято».

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Получение состояния индексатора
Hello **Получение состояния индексатора** операция получает hello текущее состояние и журнал выполнения индексатора: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Hello `api-version` является обязательным. Hello предварительной версии — `2015-02-28-Preview`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код «200 — ОК».

Hello текст ответа содержит сведения об общем состоянии работоспособности индексатора, hello при последнем вызове индексатора, а также hello журнал последних вызовов индексатора (при его наличии). 

Пример текста ответа выглядит следующим образом. 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Состояние индексатора**

Состояние индексатора может принимать одно из hello следующие значения:

* `running`Указывает, что этот hello индексатор работает нормально. Обратите внимание на то, что некоторые из выполнений индексатора hello может по-прежнему завершаться неудачно, поэтому рекомендуется toocheck hello `lastResult` также свойство. 
* `error`Указывает, что этот индексатор hello возникла ошибка, которую невозможно исправить без вмешательства человека. Например, истек срок действия учетных данных источника данных hello или hello схемы источника данных hello или целевой индекс hello изменилось в важных способом. 

**Результат выполнения индексатора**

Результат выполнения индексатора содержит сведения об одном выполнении индексатора. Hello последний результат представлен как hello `lastResult` свойство hello состояние индексатора. Другие Недавние результаты при их наличии возвращаются в виде hello `executionHistory` свойство hello состояние индексатора. 

Результат выполнения индексатора содержит hello следующие свойства: 

* `status`: hello состояние выполнения. Подробные сведения см. в разделе [Состояние выполнения индексатора](#IndexerExecutionStatus) ниже. 
* `errorMessage`: сообщение об ошибке при выполнении. 
* `startTime`: hello время запуска этого выполнения в формате UTC.
* `endTime`: hello время завершения этого выполнения в формате UTC. Это значение не задано, если выполнение hello все еще выполняется.
* `errors`: массив ошибок на уровне элементов, если таковые имеются. Каждая запись содержит ключ документа (свойство `key`) и сообщение об ошибке (свойство `errorMessage`). 
* `itemsProcessed`: hello количество элементов источника данных (например, строк таблицы), которые hello tooindex индексатора предпринята во время этого выполнения. 
* `itemsFailed`: hello число элементов, которые не удалось выполнить во время этого выполнения.  
* `initialTrackingState`: всегда `null` для первого выполнения индексатора hello, или если политика отслеживания изменений данных hello не включена на hello для используемого источника данных. Если такая политика включена, это значение в последующих выполнениях указывает hello первый (наименьшее) значение отслеживания изменений, обработанное в этом выполнении. 
* `finalTrackingState`: всегда `null` Если политика отслеживания изменений данных hello на hello для используемого источника данных не включен. В противном случае указывает hello последней (наивысшая) значение отслеживания изменений, успешно обработанное в этом выполнении. 

<a name="IndexerExecutionStatus"></a>
**Состояние выполнения индексатора**

Состояние выполнения индексатора регистрирует состояние одного выполнения индексатора hello. Может иметь следующие значения hello.

* `success`Указывает, что выполнение индексатора hello завершено успешно.
* `inProgress`Указывает ход выполнения индексатора hello. 
* `transientFailure` указывает на сбой выполнения индексатора. Подробности см. в свойстве `errorMessage`. Hello сбоя может или не требовать вмешательства человека toofix: например, устранение несовместимости схемы между источником данных hello и целевой индекс hello требует действий пользователя, а Временная недоступность источника данных нет. Вызовы индексатора будут продолжаться по расписанию, если оно установлено. 
* `persistentFailure`Указывает, что сбой индексатора, hello способом, который требует вмешательства человека. Запланированные выполнения индексатора останавливаются. После устранения проблемы hello, используйте API Сброс индексатора toorestart hello запланированных выполнений. 
* `reset`Указывает, что этот hello индексатор был сброшен путем вызова tooReset API индексатор (см. ниже). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Сброс индексатора
Hello **Сброс индексатора** операции сбрасывает состояние, связанное с индексатором hello отслеживания изменений hello. Это позволяет вам tootrigger с нуля повторная индексация (например, если была изменена схема источника данных) или toochange hello политику обнаружения изменений для источника данных, связанный с hello индексатора.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` является обязательным. Hello предварительной версии — `2015-02-28-Preview`. 

Hello `api-key` должен быть ключом администратора (как противоположность tooa ключа запроса). См. в разделе проверки подлинности toohello [API REST службы поиска](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn дополнительные ключи. [Создание службы поиска на портале hello](search-create-service-portal.md) объясняется, как использовать URL-адрес службы tooget hello и ключевые свойства в запросе hello.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код «204 — Нет содержимого».

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Сопоставление типов данных SQL и типов данных службы "Поиск Azure"
<table style="font-size:12">
<tr>
<td>Тип данных SQL</td>    
<td>Совместимые типы полей целевого индекса</td>
<td>Примечания</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>real, float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, money<br>decimal<br>numeric
</td>
<td>Edm.String</td>
<td>Поиск Azure не поддерживает преобразование десятичных типов в Edm.Double, так как это отрицательно скажется на точности.
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>В разделе [функции сопоставления полей](#FieldMappingFunctions) в этом документе, Дополнительные сведения о том, как tootransform строковый столбец в Collection(Edm.String)</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>geography</td>
<td>Edm.GeographyPoint</td>
<td>Поддерживаются только экземпляры географических объектов типа POINT с SRID 4326 (по умолчанию hello)</td>
</tr>
<tr>
<td>rowversion</td>
<td>Недоступно</td>
<td>Столбцы версии строк не могут храниться в индекс поиска hello, но они могут использоваться для отслеживания изменений</td>
</tr>
<tr>
<td>time, timespan<br>binary, varbinary, image,<br>xml, geometry, CLR types</td>
<td>Недоступно</td>
<td>Не поддерживается</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Сопоставление типов данных JSON и типов данных службы поиска Azure
<table style="font-size:12">
<tr>
<td>Тип данных JSON</td>    
<td>Совместимые типы полей целевого индекса</td>
<td>Примечания</td>
</tr>
<tr>
<td>bool</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Целые числа</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Числа с плавающей запятой</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Массивы примитивных типов, например ["a", "b", "c"]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Строки, которые выглядят как даты</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Объекты GeoJSON типа Point</td>
<td>Edm.GeographyPoint</td>
<td>Geojson являются объектами JSON в кодировке hello: {«type»: «Точка», «coordinates»: [long, lat]} </td>
</tr>
<tr>
<td>Другие объекты JSON</td>
<td>Недоступно</td>
<td>Не поддерживаются. В настоящее время служба "Поиск Azure" поддерживает только типы примитивов и коллекции строк.</td>
</tr>
</table>
