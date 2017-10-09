---
title: "aaaIndexing хранилища больших двоичных объектов с поиском Azure"
description: "Узнайте, как tooindex BLOB-объектов Azure хранения и извлечения текста из документов с поиском Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Индексирование документов в хранилище BLOB-объектов Azure с помощью службы поиска Azure
В этой статье показано, как документы tooindex toouse поиска Azure (такие как PDF-файлов, документов Microsoft Office и некоторые другие распространенные форматы) в хранилище больших двоичных объектов Azure. Во-первых здесь также описаны hello основы установки и настройки индексатора большого двоичного объекта. Затем оно предлагает более глубокого исследования поведения и сценарии, скорее всего, tooencounter.

## <a name="supported-document-formats"></a>Поддерживаемые форматы документов
индексатор Hello больших двоичных объектов можно извлечь текст из hello следующие форматы документов:

* PDF;
* форматы Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (сообщения электронной почты Outlook);  
* HTML
* XML
* ZIP;
* EML
* RTF
* обычные текстовые файлы (см. также [индексирование обычного текста](#IndexingPlainText));
* JSON (см. [индексирование BLOB-объектов JSON](search-howto-index-json-blobs.md));
* CSV (сведения о предварительной версии функции см. в статье [Индексирование больших двоичных объектов CSV с помощью индексатора больших двоичных объектов службы поиска Azure](search-howto-index-csv-blobs.md)).

> [!IMPORTANT]
> Массивы CSV и JSON сейчас поддерживаются только в предварительной версии. Эти форматы — доступна только при использовании версии **2016-09-01-Preview** из hello предварительной версии 2.x API-интерфейса REST или версия для hello .NET SDK. Помните, что предварительные версии API предназначены для тестирования и ознакомления. Они не должны использоваться в рабочей среде.
>
>

## <a name="setting-up-blob-indexing"></a>Настройка индексирования больших двоичных объектов
Можно настроить индексатор хранилище BLOB-объектов Azure с помощью следующих инструментов:

* [Портал Azure](https://ms.portal.azure.com)
* [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) Поиска Azure;
* [пакета SDK .NET для Поиска Azure](https://aka.ms/search-sdk);

> [!NOTE]
> Некоторые функции (например, для сопоставления полей) еще не доступны на портале hello и иметь toobe использовать программно.
>
>

Здесь продемонстрированы hello потока с помощью API-интерфейса REST hello.

### <a name="step-1-create-a-data-source"></a>Шаг 1. Создание источника данных
Источник данных задает, какие данные tooindex, учетные данные, необходимые tooaccess hello данные и политики tooefficiently выявления изменений в данных hello (новых, измененных или удаленных строк). Источник данных можно использовать несколько индексаторов в hello же службы поиска.

Для индексирования большого двоичного объекта, hello источник данных должен иметь hello следующие необходимые свойства:

* **имя** hello уникальное имя источника данных hello в службе поиска.
* Свойство **type** должно иметь значение `azureblob`.
* **учетные данные** предоставляет hello строка подключения учетной записи хранилища как hello `credentials.connectionString` параметра. В разделе [как учетные данные toospecify](#Credentials) ниже сведения.
* Свойство **container** определяет контейнер в вашей учетной записи хранения. По умолчанию извлекаются все большие двоичные объекты в контейнере hello. Требуется только tooindex большие двоичные объекты из определенного виртуального каталога, можно указать этот каталог, используя необязательный hello **запроса** параметра.

toocreate источника данных:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Дополнительные сведения о hello создать источник данных API см [создать источник данных](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Как toospecify учетные данные ####

Вы можете указать учетные данные hello hello контейнера больших двоичных объектов в одном из следующих способов:

- **Строка подключения учетной записи хранения с полным доступом**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Hello строка подключения hello портал Azure можно получить, перейдя по колонке учетной записи хранилища toohello > Параметры > ключей (для учетных записей хранения классический) или параметры > доступ к ключам (для учетных записей хранилища Azure Resource Manager).
- **Подпись общего доступа учетной записи хранилища** строки подключения (SAS): `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS должен иметь hello перечислить разрешения на чтение и на контейнеры и объекты (BLOB-объектов в данном случае).
-  **Подписанный URL-адрес контейнера**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS должен иметь hello перечислить разрешения на чтение и на контейнер hello.

Дополнительные сведения о подписанных URL-адресах см. в статье [Использование подписанных URL-адресов (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Если вы используете учетные данные SAS, необходимо будет tooupdate hello учетные данные источника данных периодически с обновленной подписи tooprevent истечения срока их действия. При истечении срока действия учетных данных SAS, hello индексатора, будут завершаться сообщение об ошибке слишком`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Шаг 2. Создание индекса
Индекс Hello указывает hello поля в документе, атрибуты, и другие конструкции, интерфейс поиска hello фигуры.

Вот как toocreate индекса с возможностью поиска `content` поле текста hello toostore, извлеченных из BLOB-объектов:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Дополнительные сведения о создании индексов см. в статье [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index) (Создание индекса).

### <a name="step-3-create-an-indexer"></a>Шаг 3. Создание индексатора
Индексатор, который подключается с индексом поиска целевого источника данных, а также расписание обновления данных hello tooautomate.

После создания hello индекс и источник данных вы будете готовы toocreate hello индексатора:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Этот индексатор будет запускаться каждые два часа (интервал расписания задано слишком «PT2H»). toorun индексатор каждые 30 минут для интервала hello слишком «PT30M». Hello минимально поддерживаемые интервал составляет 5 минут. Hello расписания необязательно — Если не указано, индексатор, который выполняется только один раз, при его создании. Однако индексатор можно запустить по запросу в любое время.   

Дополнительные сведения о hello создания API индексатора, ознакомьтесь с [Создание индексатора](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Индексирование больших двоичных объектов с помощью службы поиска Azure

В зависимости от hello [конфигурации индексатора](#PartsOfBlobToIndex), индексатор hello больших двоичных объектов может индексировать только метаданных хранилища (полезен, если только осторожностью около hello метаданных и не нужен tooindex hello содержимого больших двоичных объектов), хранилищу и содержимому метаданные, или оба метаданные и текстовое содержимое. По умолчанию hello индексатор извлекает метаданные и содержимое.

> [!NOTE]
> По умолчанию большие двоичные объекты со структурированным содержимым, например JSON- или CSV-файлы, индексируются как один блок текста. Если tooindex JSON и CSV большие двоичные объекты в структурированный способ, см. [больших двоичных объектов JSON, индексирование](search-howto-index-json-blobs.md) и [CSV индексирование больших двоичных объектов](search-howto-index-csv-blobs.md) Предварительный просмотр компонентов.
>
> Составной или внедренный документ (например, ZIP-файл или документ Word с внедренным электронным сообщением Outlook, содержащим вложения) также индексируется как один документ.

* Hello текстовому содержимому документа hello извлекается в строковое поле с именем `content`.

> [!NOTE]
> Поиск Azure ограничивает количество текста, он извлекает в зависимости от ценового уровня hello: бесплатно уровня 32000 знаков, 64 000 для обычной и 4 миллионов для уровней Standard, Standard S2 и Standard S3. Предупреждение включается в ответ состояние индексатора hello усеченное документов.  

* Определяемые пользователем метаданные свойства на большой двоичный объект hello, если таковые имеются, извлекаются открытым текстом.
* Стандартная большого двоичного объекта метаданных свойства извлекаются в hello следующие поля:

  * **метаданные\_хранения\_имя** (Edm.String) — имя файла hello hello большого двоичного объекта. Например, при наличии blob /my-container/my-folder/subfolder/resume.pdf hello значением этого поля является `resume.pdf`.
  * **метаданные\_хранения\_путь** (Edm.String) - hello полный URI большого двоичного объекта hello, включая hello учетной записи хранилища. Например, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **метаданные\_хранения\_содержимого\_типа** (Edm.String) - тип содержимого как определяемый кода hello используется tooupload hello большого двоичного объекта. Например, `application/octet-stream`.
  * **метаданные\_хранения\_последний\_изменить** (Edm.DateTimeOffset) - последнего изменения отметок времени для hello большого двоичного объекта. Поиск Azure использует этот отметка времени изменить tooidentify больших двоичных объектов, tooavoid переиндексирования все, что после начального индексирования hello.
  * **metadata\_storage\_size** (Edm.Int64) — размер большого двоичного объекта в байтах.
  * **метаданные\_хранения\_содержимого\_md5** (Edm.String) - хэш MD5 содержимого большого двоичного объекта hello, если он доступен.
* Формат документа метаданных свойства определенного tooeach извлекаются в перечисленных полей hello [здесь](#ContentSpecificMetadata).

Не требуется toodefine поля для всех hello выше свойств в индексе поиска, — просто захват hello свойства, необходимые для приложения.

> [!NOTE]
> Часто hello имена полей в существующий индекс будет отличаться от имен полей hello, созданных во время извлечения документа. Можно использовать **поля сопоставления** имена свойств toomap hello, предоставляемые имена полей toohello поиска Azure в индекс поиска. Ниже вы увидите пример использования сопоставления полей.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Определение ключей документа и сопоставлений полей
В поиске Azure ключ документа hello однозначно определяет документа. Каждый индекс поиска должен содержать только одно поле ключа типа Edm.String. Hello ключевое поле является обязательным для каждого документа, который добавляется индекс toohello (это фактически hello единственное обязательное поле).  

Необходимо тщательно рассмотреть извлеченные поле, которое необходимо сопоставить toohello ключевого поля для выбранного индекса. Hello кандидаты:

* **метаданные\_хранения\_имя** — это может быть удобным кандидата, но Обратите внимание, что имена hello 1) может быть не уникальным, при наличии больших двоичных объектов с таким же именем в разных папках hello и (2) hello имя может содержать символы, недопустимы в документе клавиши, такие как дефисы. Можно обработать недопустимые символы с помощью hello `base64Encode` [поле функции сопоставления](search-indexer-field-mappings.md#base64EncodeFunction) — Если это сделать, помните tooencode ключи документов при их передачей в API вызывает например Уточняющий запрос. (Например, в .NET можно использовать hello [UrlTokenEncode метод](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) для этой цели).
* **метаданные\_хранения\_путь** — с использованием полного пути hello гарантирует уникальность, но определенно содержит путь hello `/` символы, которые [недопустимые в ключе документа](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Как показано выше, предусмотрена возможность hello кодирования ключей hello, с помощью hello `base64Encode` [функция](search-indexer-field-mappings.md#base64EncodeFunction).
* Если ни один из вариантов hello выше подходит, можно добавить большие двоичные объекты toohello пользовательские метаданные свойства. Этот параметр Однако требуется вашей tooadd процесс передачи больших двоичных объектов, большие двоичные объекты метаданных свойства tooall. Поскольку hello ключ является обязательным свойством, все большие двоичные объекты, у которых нет свойства даст сбой toobe проиндексированы.

> [!IMPORTANT]
> Если нет явного сопоставления для hello ключевого поля в индексе hello, поиск Azure автоматически использует `metadata_storage_path` как hello ключа и base-64 кодируется ключевых значений (hello второй вариант выше).
>
>

Например, выберем hello `metadata_storage_name` как ключ документа hello. Предположим также, что индекс имеет ключевое поле с именем `key` и поле `fileSize` для хранения hello размер документа. toowire всех компонентов в случае необходимости, указать следующие сопоставления полей при создании или обновлении индексатор hello:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring этот вместе, вот как можно добавить сопоставления полей и включить ключей для существующий индексатор кодировку base-64:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn Подробнее о сопоставления полей в разделе [в этой статье](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Управление индексированием больших двоичных объектов
Вы можете выбирать, какие большие двоичные объекты необходимо индексировать, а какие — пропустить.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Индексировать только hello большие двоичные объекты с определенных расширений файлов
Можно индексировать только hello большие двоичные объекты с расширениями имен файлов hello, указываются с помощью hello `indexedFileNameExtensions` параметр конфигурации индексатора. Hello значение является строкой, содержащей разделенные запятыми список расширений файлов (с точкой). Например tooindex только hello. PDF и. Большие двоичные объекты DOCX, выполните следующие действия:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>Исключение больших двоичных объектов с определенными расширениями файлов
Большие двоичные объекты с определенных расширений имен файлов можно исключить из индексирования с помощью hello `excludedFileNameExtensions` параметра конфигурации. Hello значение является строкой, содержащей разделенные запятыми список расширений файлов (с точкой). Например tooindex всех больших двоичных объектов за исключением тех, которые hello. PNG и. Расширения JPEG, выполните следующие действия:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Если присутствуют оба параметра `indexedFileNameExtensions` и `excludedFileNameExtensions`, то Azure сначала выполняет поиск по `indexedFileNameExtensions`, а затем по `excludedFileNameExtensions`. Это означает, что если hello одинаковое расширение присутствует в оба списка, он будет исключен из индексирования.

### <a name="dealing-with-unsupported-content-types"></a>Работа с неподдерживаемыми типами содержимого

По умолчанию hello BLOB-объект индексатора останавливается, как только обнаруживается большой двоичный объект с неподдерживаемым типом контента (например, изображения). Конечно, можно использовать hello `excludedFileNameExtensions` параметр tooskip определенных типов содержимого. Тем не менее может потребоваться большие двоичные объекты tooindex заранее не известен все hello возможных типов содержимого. toocontinue индексирования при обнаружении неподдерживаемый тип содержимого, задайте hello `failOnUnsupportedContentType` параметр конфигурации слишком`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Игнорирование ошибок анализа

Azure логики извлечения для поиска документов имеет свои недостатки и иногда не удастся tooparse документы поддерживаемого типа содержимого, такие как. DOCX или. PDF. Если нежелательно hello toointerrupt индексирования в таких случаях установите hello `maxFailedItems` и `maxFailedItemsPerBatch` значения разумного toosome параметров конфигурации. Например:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Управление индексируются, какие части hello больших двоичных объектов

Можно выбрать, какие части hello большие двоичные объекты индексируются посредством hello `dataToExtract` параметра конфигурации. Возможны следующие значения hello:

* `storageMetadata`-Указывает, что только hello [свойства стандартных большого двоичного объекта и определяемые пользователем метаданные](../storage/blobs/storage-properties-metadata.md) индексируются.
* `allMetadata`-Указывает, что метаданные хранилища и hello [определенных метаданных типа содержимого](#ContentSpecificMetadata) извлечь из большого двоичного объекта hello индексируются содержимого.
* `contentAndMetadata`-Указывает, что индексируются все метаданные и извлечь из большого двоичного объекта hello текстовое содержимое. Это значение по умолчанию hello.

Например tooindex только hello хранилища метаданных, используйте:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>С помощью toocontrol метаданные большого двоичного объекта как индексируются больших двоичных объектов

описанные выше параметры конфигурации Hello применяются tooall больших двоичных объектов. В некоторых случаях может потребоваться toocontrol *отдельные большие двоичные объекты* индексируются. Это можно сделать, добавив следующие hello BLOB-объектов метаданные свойства и значения:

| Имя свойства | Значение свойства | Пояснение |
| --- | --- | --- |
| AzureSearch_Skip |True |Указывает, что hello индексатора toocompletely пропустить hello больших двоичных объектов. Не извлекаются ни метаданные, ни содержимое. Это полезно в том случае, когда отдельного большого двоичного объекта постоянно завершается неудачей и прерывания процесса индексирования hello. |
| AzureSearch_SkipContent |True |Это эквивалент `"dataToExtract" : "allMetadata"` описанный [выше](#PartsOfBlobToIndex) tooa области отдельного большого двоичного объекта. |

## <a name="incremental-indexing-and-deletion-detection"></a>Добавочное индексирование и обнаружение удаления 
При настройке toorun индексатора больших двоичных объектов по расписанию, он повторно индексирует hello изменении больших двоичных объектов, как определено hello большого двоичного объекта только `LastModified` отметки времени.

> [!NOTE]
> Нет toospecify политику обнаружения изменений: Добавочное индексирование будет включен автоматически.

toosupport удаление документов, используйте подход «обратимое удаление». При удалении hello большие двоичные объекты сразу, соответствующие документы, не удаляется из индекса поиска hello. Вместо этого используйте hello следующие шаги:  

1. Добавить tooAzure tooindicate большого двоичного объекта toohello свойство пользовательских метаданных поиска логически удален
2. Настройте политику обнаружения удаления, мягкие на источнике данных hello
3. После обработки индексатора hello hello двоичный объект (отображается состояние индексатора hello API) большого двоичного объекта hello физически удалить

Например, следующая политика hello рассматривает toobe большого двоичного объекта, удалить, если он содержит свойство метаданных `IsDeleted` со значением hello `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Индексирование больших наборов данных

Индексирование больших двоичных объектов может занимать много времени. В случаях, когда имеют миллионы tooindex больших двоичных объектов можно ускорить индексацию путем секционирования данных и использования данных hello tooprocess несколько индексаторов в параллельном режиме. Вот как это можно сделать.

- Секционируйте данные в несколько контейнеров больших двоичных объектов или виртуальных папок.
- Настройте несколько источников данных службы поиска Azure, по одному на контейнер или папку. toopoint tooa большого двоичного объекта папки используйте hello `query` параметр:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Создайте соответствующий индексатор для каждого источника данных. Все hello индексаторы могут точки toohello же целевой индекс поиска.  

- Одна единица поиска в службе в определенный момент времени может запустить один индексатор. Создание нескольких индексаторов, как описано выше, полезно только при их фактическом параллельном выполнении. toorun несколько индексаторов в параллельном режиме, горизонтальное масштабирование службы поиска, создав на достаточное количество разделов и реплик. Например если служба поиска имеет 6 единиц поиска (например, 2 раздела x 3 реплики), затем 6 индексаторы могут выполняться одновременно, приведет к six-fold увеличение пропускной способности индексации hello. toolearn Дополнительные сведения о масштабировании и Планирование производительности, в разделе [масштабировать уровни ресурсов для запросов и индексирования рабочих нагрузок в поиске Azure](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Индексация документов и связанных данных

Вы можете слишком «сборка» документов из нескольких источников в индексе. Например может потребоваться toomerge текст из больших двоичных объектов с другими метаданными, хранящимися в Cosmos DB. Можно даже использовать hello принудительной индексирования API вместе с различными индексаторы слишком надстраивать поиск документов из нескольких частей. 

Для этого toowork всех индексаторов и других компонентов должны tooagree на ключ документа hello. Подробное пошаговое руководство см. в статье [Combine documents with other data in Azure Search](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html) (Объединение документов с другими данными в службе "Поиск Azure").

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Индексирование обычного текста 

Если все BLOB-объектов содержат в обычный текст hello кодировкой, может значительно повысить производительность индексирования с помощью **разбора режим текста**. разбора режим hello набора текста toouse `parsingMode` свойство конфигурации слишком`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

По умолчанию hello `UTF-8` предполагается кодировка. использовать другую кодировку, toospecify hello `encoding` свойство конфигурации: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Свойства метаданных определенного типа содержимого
Hello следующей таблице приведена сводка обработки для каждого формата документа и описание свойств метаданных hello, извлекаемые фильтрами поиска Azure.

| Формат документа или тип содержимого | Свойства метаданных определенного типа содержимого | Сведения об обработке |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Удаление разметки HTML и извлечение текста |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Извлечение текста, включая внедренные документы (кроме изображений) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Извлечение текста, включая внедренные документы |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Извлечение текста, включая внедренные документы |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Извлечение текста, включая внедренные документы |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Извлечение текста, включая внедренные документы |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Извлечение текста, включая внедренные документы |
| PPT (application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Извлечение текста, включая внедренные документы |
| MSG (application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Извлечение текста, включая вложения |
| ZIP (application/zip) |`metadata_content_type` |Извлеките текст из всех документов в архиве hello |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Удаление разметки XML и извлечение текста |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Извлечение текста<br/>Примечание: См. Если вам требуется tooextract документ на несколько полей из большого двоичного объекта JSON, [больших двоичных объектов JSON, индексирование](search-howto-index-json-blobs.md) подробные сведения |
| EML (message/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Извлечение текста, включая вложения |
| RTF (приложение или RTF) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Извлечение текста|
| Обычный текст (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Извлечение текста|


## <a name="help-us-make-azure-search-better"></a>Помогите нам усовершенствовать службу поиска Azure
Если вам нужна какая-либо функция или у вас есть идеи, которые можно было бы реализовать, сообщите об этом на [сайте UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
