---
title: "хранилище таблиц Azure с поиском Azure aaaIndexing | Документы Microsoft"
description: "Узнайте, как tooindex данные, хранящиеся в хранилище таблиц Azure с поиском Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Индексирование хранилища таблиц Azure с помощью поиска Azure
В этой статье показано, как сохранить toouse tooindex данных поиска Azure в хранилище таблиц Azure.

## <a name="set-up-azure-table-storage-indexing"></a>Настройка индексирования хранилища таблиц Azure

Вы можете настроить индексатор хранилища таблиц Azure с помощью следующих ресурсов:

* [Портал Azure](https://ms.portal.azure.com)
* [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) Поиска Azure;
* [пакета SDK .NET для Поиска Azure](https://aka.ms/search-sdk);

Здесь продемонстрированы hello потока с помощью API-интерфейса REST hello. 

### <a name="step-1-create-a-datasource"></a>Шаг 1. Создание источника данных

Источник данных указывает, какие данные tooindex, hello учетными данными tooaccess hello и hello политики, позволяющие tooefficiently поиска Azure выявления изменений в данных hello.

Для индексирования таблицы, hello источник данных должен иметь hello следующие свойства:

- **имя** hello уникальное имя источника данных hello в службе поиска.
- Свойство **type** должно иметь значение `azuretable`.
- **учетные данные** параметр содержит строку подключения к учетной записи хранилища hello. В разделе hello [укажите учетные данные](#Credentials) подробные сведения см.
- **контейнер** hello задает имя таблицы и необязательный запрос.
    - Укажите имя таблицы hello с помощью hello `name` параметра.
    - При необходимости укажите запрос с помощью hello `query` параметра. 

> [!IMPORTANT] 
> По возможности для повышения производительности используйте фильтр на PartitionKey. После любого другого запроса выполняется сканирование всей таблицы, что приводит к снижению производительности для больших таблиц. В разделе hello [вопросы производительности](#Performance) раздела.


toocreate источника данных:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Дополнительные сведения о hello создать источник данных API см. в разделе [создать источник данных](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Учетные данные toospecify способами ####

Можно предоставить учетные данные hello hello таблицы в одном из следующих способов: 

- **Строка подключения учетной записи хранилища полный доступ**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` hello строку подключения можно получить из hello портал Azure, будет toohello **колонке учетной записи хранилища** > **параметры**   >  **Ключей** (для учетных записей хранилища классический) или **параметры** > **ключи доступа** (для ресурсов Azure Учетные записи хранения Manager).
- **Учетная запись хранения общую строку соединения подписи доступа**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` hello подписанный URL-адрес должен иметь hello перечислить разрешения на чтение и на контейнеры (таблицы, в данном случае) и объекты (таблицы строк).
-  **Подписанный URL-адрес таблицы**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` hello подписанный URL-адрес должен иметь разрешения запроса (чтение) на таблицу hello.

Дополнительные сведения о подписанных URL-адресах хранения см. в разделе [Использование подписанных URL-адресов](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> При использовании учетных данных подписи общего доступа, необходимо будет учетные данные источника данных hello tooupdate периодически с обновленной подписи tooprevent истечения срока их действия. При истечении срока действия учетных данных подписи общего доступа, индексатор hello выдает сообщение об ошибке, слишком «учетные данные, указанные в строке подключения hello недопустимые или истек срок действия.»  

### <a name="step-2-create-an-index"></a>Шаг 2. Создание индекса
Индекс Hello указывает hello поля в документе, а атрибуты hello и другие конструкции, этот процесс поиска hello фигуры.

toocreate индекса:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Дополнительные сведения о создании индексов см. в статье [Создание индекса](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Шаг 3. Создание индексатора
Индексатор, который подключается с индексом поиска целевого источника данных и предоставляет расписание обновления данных hello tooautomate. 

После создания индекса hello и источник данных вы будете готовы toocreate hello индексатора:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Этот индексатор выполняется каждые два часа. (интервал расписания hello задано слишком «PT2H».) toorun индексатор каждые 30 минут для интервала hello слишком «PT30M». Hello минимально поддерживаемые интервал — 5 минут. расписание Hello является необязательным. Если не указано, индексатор, который выполняется только один раз, при его создании. Однако индексатор можно запустить по запросу в любое время.   

Дополнительные сведения о hello Создание индексатора API в разделе [Создание индексатора](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Работа с различными именами полей
В некоторых случаях hello имена полей в существующий индекс, отличаются от приветствия имен свойств в таблице. Имена полей сопоставления toomap hello свойства с именами полей toohello hello таблицы можно использовать в индексе поиска. toolearn Подробнее о сопоставления полей в разделе [сопоставления полей индексатор поиска Azure мост hello различия между источников данных и поиска индексов](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Обработка ключей документа
В поиске Azure ключ документа hello однозначно определяет документа. Каждый индекс поиска должен содержать только одно поле ключа типа `Edm.String`. Hello ключевое поле является обязательным для каждого документа, который добавляется toohello индекса. (На самом деле ее hello требуется только поля.)

Так как строки таблицы имеют составной ключ, поиск Azure создает искусственное поле с именем `Key`, которое представляет собой объединение значений ключа секции и ключа строки. Например, если строка PartitionKey должен `PK1` и RowKey `RK1`, затем hello `Key` значение `PK1RK1`.

> [!NOTE]
> Hello `Key` значение может содержать символы, недопустимые в документе клавиши, такие как дефисы. Можно обработать недопустимые символы с помощью hello `base64Encode` [поле функции сопоставления](search-indexer-field-mappings.md#base64EncodeFunction). После этого следует помните tooalso кодировке Base64 кодировке при передаче ключей документов в API вызывает например Уточняющий запрос.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Добавочное индексирование и обнаружение удаления 
При настройке toorun индексатора таблицы по расписанию, она reindexes только новых или обновленных строк, как определено в строке `Timestamp` значение. У вас нет toospecify политику обнаружения изменений. Добавочное индексирование активируется автоматически.

tooindicate что некоторые документы должны быть удалены из индекса hello, можно использовать стратегию обратимого удаления. Вместо удаления строки, добавьте tooindicate свойства, которые удален и настроить политику обнаружения удаления, мягкие hello источника данных. Например, следующая политика hello рассматривает удалить строку, если строка hello имеет свойство `IsDeleted` со значением hello `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Рекомендации по производительности

По умолчанию поиск Azure использует следующие фильтр запроса hello: `Timestamp >= HighWaterMarkValue`. Так как таблицы Azure нет необходимости во вторичном индексе на hello `Timestamp` поля этого типа запросов требуется полное сканирование таблицы и поэтому медленно для больших таблиц.


Ниже приведены два возможных метода повышения производительности индексирования таблиц. Оба эти метода зависят от секционирования таблиц: 

- Если данные естественным образом можно разделить на несколько секций, создайте источник данных и соответствующий индексатор для каждой секции. Каждому индексатору теперь имеет tooprocess только определенной секции диапазона, что приводит к повышению производительности запросов. Если требуется toobe индексированных данных hello имеет несколько основных разделов, а еще лучше: каждого индексатора только просматривает секции. Например, toocreate источник данных для обработки диапазона секций с ключи из `000` слишком`100`, используйте запрос, подобный следующему: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Если данные секционируются по времени (например, создании раздела каждого дня или недели), рекомендуется следующий подход hello: 
    - Используйте запрос hello формате: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Отслеживать ход выполнения индексатора с помощью [получить API состояния индексатора](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)и периодически обновлять hello `<TimeStamp>` условие hello запроса на основе hello последней успешной-пиковой значения. 
    - При таком подходе Если вам требуется полное повторное индексирование, tootrigger должны tooreset hello источник данных запроса в дополнение tooresetting hello индексатора. 


## <a name="help-us-make-azure-search-better"></a>Помогите нам усовершенствовать службу поиска Azure
Если вам нужна какая-либо функция или у вас есть идеи, которые можно было бы реализовать, сообщите об этом на [сайте UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
