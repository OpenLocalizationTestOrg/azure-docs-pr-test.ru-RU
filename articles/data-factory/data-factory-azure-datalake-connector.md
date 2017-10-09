---
title: "aaaCopy tooand данных из хранилища Озера данных Azure | Документы Microsoft"
description: "Узнайте, как toocopy tooand данных из хранилища Озера данных с помощью фабрики данных Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Tooand копирования данных из хранилища Озера данных с помощью фабрики данных
В этой статье объясняется, как toouse действие копирования в tooand данных toomove фабрики данных Azure из хранилища Озера данных Azure. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статью Обзор перемещение данных в действии копирования.

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Можно скопировать данные **из хранилища Озера данных Azure** toohello следующие хранилищ данных:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Можно скопировать данные из hello, следуя хранилищ данных **tooAzure хранилища Озера данных**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Прежде чем создавать конвейер с действием копирования, создайте учетную запись Data Lake Store. Дополнительные сведения см. в статье [Начало работы с хранилищем озера данных Azure с помощью портала Azure](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Поддерживаемые типы аутентификации
Соединитель Hello хранилища Озера данных поддерживает следующие типы проверки подлинности:
* Проверка подлинности субъекта-службы
* Проверка подлинности учетных данных пользователя (OAuth) 

Мы рекомендуем использовать проверку подлинности субъекта-службы, особенно для копирования данных по расписанию. При проверке подлинности учетных данных пользователя может истечь срок действия маркера. Сведения о конфигурации, в разделе hello [связанные свойства службы](#linked-service-properties) раздела.

## <a name="get-started"></a>Начало работы
Можно создать конвейер с действием копирования, которое перемещает данные из Azure Data Lake Store или обратно с помощью различных инструментов и интерфейсов API.

Hello простым способом toocreate toocopy данных конвейера — toouse hello **мастер копирования**. Учебник по созданию конвейера с помощью мастера копирования hello см. в разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md).

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров. 
2. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных. Например при копировании данных из tooan хранилища BLOB-объектов Azure хранилища Озера данных Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour хранилища Озера данных Azure. Свойства связанной службы, определенные tooAzure хранилища Озера данных, в разделе [связанные свойства службы](#linked-service-properties) раздела. 
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных. И создать другой набор данных toospecify hello папки и путь к файлу в хранилище Озера данных hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello. Свойства набора данных, определенных tooAzure хранилища Озера данных, в разделе [свойства набора данных](#dataset-properties) раздела.
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. В примере hello приведенные выше используются BlobSource в исходной и AzureDataLakeStoreSink в приемник для действия копирования hello. Аналогично при копировании из хранилища Озера данных Azure tooAzure хранилища BLOB-объектов используется AzureDataLakeStoreSource и BlobSink в действии копирования hello. Свойства действия копирования, определенные tooAzure хранилища Озера данных, в разделе [скопировать свойства действия](#copy-activity-properties) раздела. Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.  

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища Озера данных Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-data-lake-store) этой статьи.

Hello в следующих разделах приведены сведения о JSON свойства, используемые toodefine хранилища Озера конкретных tooData сущностей фабрики данных.

## <a name="linked-service-properties"></a>Свойства связанной службы
Связанная служба связывает фабрику данных tooa хранилища данных. Создание связанной службы типа **AzureDataLakeStore** toolink фабрики данных tooyour данные хранилища Озера данных. Hello в следующей таблице описываются JSON элементы конкретного хранилища Озера tooData связанные службы. Вы можете выбирать между проверкой подлинности субъекта-службы и учетных данных пользователя.

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **type** | свойство типа Hello должно быть задано слишком**AzureDataLakeStore**. | Да |
| **dataLakeStoreUri** | Сведения о hello хранилища Озера данных Azure. Эти сведения принимает одно из следующих форматов hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` или `adl://[accountname].azuredatalakestore.net/`. | Да |
| **subscriptionId** | Принадлежит hello toowhich идентификатор подписки Azure хранилища Озера данных. | Необходимо для приемника |
| **resourceGroupName** | Принадлежит ресурс Azure группы имя toowhich hello хранилища Озера данных. | Необходимо для приемника |

### <a name="service-principal-authentication-recommended"></a>Проверка подлинности на основе субъекта-службы (рекомендуется)
toouse основной проверки подлинности службы, регистрация сущности приложения в Azure Active Directory (Azure AD) и предоставьте его hello доступа к хранилищу Озера tooData. Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Запишите следующие значения, которые вы используете hello toodefine hello связанной службы:
* Идентификатор приложения
* Ключ приложения 
* Tenant ID

> [!IMPORTANT]
> При использовании конвейеры данных tooauthor приветствия мастера копирования убедитесь, что предоставляются hello участника-службы по крайней мере **чтения** роль в системе контроля доступа (Управление удостоверениями и доступом) для учетной записи хранилища Озера данных hello. Кроме того, по крайней мере предоставить субъекту-службе hello **чтения + Execute** разрешение корневого хранилища Озера данных tooyour («/») и его дочерних элементов. В противном случае может появиться сообщение hello «hello, предоставленные учетные данные являются недопустимыми».<br/><br/>
После создания или обновления участника службы в Azure AD, занимает несколько минут для эффекта tootake изменения hello. Проверьте hello субъекта-службы и конфигурации списка управления Доступом управления доступа хранилища Озера данных. Если по-прежнему отображается приветственное сообщение «hello, предоставленные учетные данные являются недопустимыми», подождите и повторите попытку.

Используйте основной проверки подлинности службы, указав hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **servicePrincipalId** | Укажите идентификатор клиента приложения hello. | Да |
| **servicePrincipalKey** | Укажите ключ приложения hello. | Да |
| **tenant** | Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение. Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure. | Да |

**Пример. Проверка подлинности на основе субъекта-службы**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Использование проверки подлинности на основе учетных данных пользователя
Кроме того можно использовать toocopy проверки подлинности учетных данных пользователя из или хранилища Озера tooData, указав hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **authorization** | Нажмите кнопку hello **авторизовать** в hello редактор фабрики данных и ввести учетные данные, назначает hello автоматически авторизации URL-адрес toothis свойство. | Да |
| **sessionId** | Идентификатор сеанса OAuth из сеанса авторизации OAuth hello. Каждый идентификатор сеанса является уникальным и используется только один раз. Этот параметр автоматически создается при использовании hello редактор фабрики данных. | Да |

**Пример. Использование проверки подлинности на основе учетных данных пользователя**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Срок действия маркера
Здравствуйте, код авторизации, создать с помощью hello **авторизовать** кнопку срок действия истекает через некоторое время. следующие сообщения Hello означает, что истек срок действия токена проверки подлинности, hello:

"Произошла ошибка при операции с учетными данными: invalid_grant — AADSTS70002. Ошибка при проверке учетных данных. AADSTS70008: hello предоставляется право доступа просрочен или отозван. Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Метка времени: 2015-12-15 21-09-31Z".

Hello следующей таблице показаны hello сроков различных типов учетных записей пользователей.


| Тип пользователя | Срок действия |
|:--- |:--- |
| Учетные записи пользователей, которые *не* управляются с помощью Azure Active Directory (например, @hotmail.com или @live.com). |12 часов |
| Учетные записи пользователей, которые управляются с помощью Azure Active Directory |запустить через 14 дней после последнего фрагмента hello <br/><br/>90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней. |

Если изменить пароль, прежде чем срок действия токена hello, hello срок действия токена истекает немедленно. Вы увидите сообщение hello, приведенные выше в этом разделе.

Повторно авторизовать hello учетной записи с помощью hello **авторизовать** кнопки, когда tooredeploy hello истечения срока действия маркера hello связанной службы. Также можно создать значения для hello **sessionId** и **авторизации** свойств программным путем с помощью hello следующий код:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Дополнительные сведения о классах hello фабрики данных, используемые в коде hello см hello [класса AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [класса AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), и [ Класс AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) разделы. Добавить tooversion ссылки `2.9.10826.1824` из `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` для hello `WindowsFormsWebAuthenticationDialog` класс, используемый в коде hello.

## <a name="dataset-properties"></a>Свойства набора данных
toospecify toorepresent набора данных, входные данные в хранилище Озера данных, задайте hello **тип** свойства набора данных hello слишком**AzureDataLakeStore**. Набор hello **linkedServiceName** свойство toohello имя набора данных hello hello хранилища Озера данных связанной службы. Полный список разделов JSON и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы набора данных в JSON, такие как **structure**, **availability** и **policy**, одинаковы для всех типов наборов данных (таких как базы данных SQL, Blob-объекты Azure и таблицы Azure). Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет сведения, такие как расположение и формат данных hello в хранилище данных hello. 

Hello **typeProperties** раздел для набора данных типа **AzureDataLakeStore** содержит hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **folderPath** |Контейнер toohello путь к папке, в хранилище Озера данных. |Да |
| **fileName** |Имя файла hello в хранилище Озера данных Azure. Hello **fileName** свойство является необязательным, без учета регистра. <br/><br/>При указании **fileName**, действие hello (включая копирования) работает на конкретный файл hello.<br/><br/>Когда **fileName** не указан, копия включает все файлы в **folderPath** во входном наборе данных hello.<br/><br/>Когда **fileName** не указано для выходной набор данных и **preserveHierarchy** не указан в приемник действие hello hello созданный файл имеет имя в формате hello данных. _Идентификатор GUID_.txt ". Например: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Нет |
| **partitionedBy** |Hello **partitionedBy** свойство является необязательным. Можно использовать toospecify динамического путь и имя файла для временных рядов данных. Например, путь к папке (**folderPath**) каждый час может быть другим. Дополнительные сведения и примеры см. в разделе [hello свойство partitionedBy](#using-partitionedby-property). |Нет |
| **format** | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, и  **ParquetFormat**. Набор hello **тип** свойства в разделе **формат** tooone из следующих значений. Дополнительные сведения см. в разделе hello [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формат JSON](data-factory-supported-file-and-compression-formats.md#json-format), [формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формат ORC](data-factory-supported-file-and-compression-formats.md#orc-format), и [Parquet формат ](data-factory-supported-file-and-compression-formats.md#parquet-format) подразделы hello [сжатие файлов и форматы, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md) статьи. <br><br> Файлы toocopy» как-является» между файловых хранилищ (двоичный копия), пропустите hello `format` раздела оба определения набора входных и выходных данных. |Нет |
| **compression** | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

### <a name="hello-partitionedby-property"></a>Свойство partitionedBy Hello
Можно указать динамический **folderPath** и **fileName** свойства для данных временных рядов с hello **partitionedBy** свойств функции фабрики данных и система переменные. Дополнительные сведения см. в разделе hello [фабрики данных Azure - функции и системные переменные](data-factory-functions-variables.md) статьи.


В следующий пример, hello `{Slice}` заменяется hello значение системной переменной фабрики данных hello `SliceStart` в указанный формат hello (`yyyyMMddHH`). Имя Hello `SliceStart` ссылается toohello время начала среза hello. Hello `folderPath` свойство отличается для каждого среза, как `wikidatagateway/wikisampledataout/2014100103` или `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

В следующий пример, hello год, месяц, день и время hello `SliceStart` извлекаются в отдельные переменные, используемые hello `folderPath` и `fileName` свойства:
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Дополнительные сведения о наборах данных временных рядов, планирования и срезов, в разделе hello [наборов данных в фабрике данных Azure](data-factory-create-datasets.md) и [фабрики данных планированием и выполнением](data-factory-scheduling-and-execution.md) статей. 


## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

Здравствуйте, свойств, доступных в hello **typeProperties** раздел действия зависят от типа каждого действия. Для операции копирования они зависят от типов источников и приемников hello.

**AzureDataLakeStoreSource** поддерживает следующие свойства в hello hello **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| **recursive** |Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello или только пользователей из указанной папки hello. |True (значение по умолчанию), False |Нет |


**AzureDataLakeStoreSink** поддерживает следующие свойства в hello hello **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| **copyBehavior** |Задает способ копирования hello. |<b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello. Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.<br/><br/><b>FlattenHierarchy</b>: все файлы из исходной папки hello создаются в первый уровень hello hello целевую папку. автоматически созданные имена создаваемых файлов целевой Hello.<br/><br/><b>MergeFiles</b>: объединяет все файлы из папки tooone hello исходного файла. Если hello имя файла или большого двоичного объекта указан, hello объединенный файл называется hello указанное имя. В противном случае имя файла hello создается автоматически. |Нет |

### <a name="recursive-and-copybehavior-examples"></a>Примеры recursive и copyBehavior
Этот раздел описывает поведение функции hello операции копирования для различных сочетаний значений рекурсивные и copyBehavior hello.

| recursive | copyBehavior | Результаты выполнения операции |
| --- | --- | --- |
| Да |preserveHierarchy |Для исходной папки Folder1 с hello следующие структуры: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создается с таким же структуру как исходной hello hello<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5 |
| Да |flattenHierarchy |Для исходной папки Folder1 с hello следующие структуры: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>целевой Hello папка1 создана следующая структура hello: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5" |
| Да |mergeFiles |Для исходной папки Folder1 с hello следующие структуры: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>целевой Hello папка1 создана следующая структура hello: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем. |
| нет |preserveHierarchy |Для исходной папки Folder1 с hello следующие структуры: <br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создается с следующая структура hello<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/><br/><br/>Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку. |
| нет |flattenHierarchy |Для исходной папки Folder1 с hello следующие структуры:<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создается с следующая структура hello<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"<br/>&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"<br/><br/><br/>Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку. |
| нет |mergeFiles |Для исходной папки Folder1 с hello следующие структуры:<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Файл2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5<br/><br/>Hello целевую папку Folder1 создается с следующая структура hello<br/><br/>Папка1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем. Автоматически созданное имя для "Файл1"<br/><br/>Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку. |

## <a name="supported-file-and-compression-formats"></a>Поддерживаемые форматы файлов и сжатия
Дополнительные сведения см. в разделе hello [сжатие файлов и форматы в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md) статьи.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Примеры JSON для копирования данных tooand из хранилища Озера данных
Следующие примеры Hello предоставьте пример JSON определения. Можно использовать эти образец определения toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Здравствуйте примерах показано, как toocopy tooand данных из хранилища хранилища Озера данных и больших двоичных объектов Azure. Тем не менее, данные можно скопировать _непосредственно_ из любого tooany источников hello приемников hello поддерживается. Дополнительные сведения см. в разделе hello раздел «поддерживаемые хранилищ данных и форматы» в hello [перемещения данных с помощью действия копирования](data-factory-data-movement-activities.md) статьи.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Пример: Копирование данных из хранилища больших двоичных объектов tooAzure хранилища Озера данных
пример кода Hello в этом разделе показано:

* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Связанная служба типа [AzureDataLakeStore](#linked-service-properties).
* Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureDataLakeStore](#dataset-properties).
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, который использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [AzureDataLakeStoreSink](#copy-activity-properties).

Hello примерах показано, как временных рядов данных из хранилища больших двоичных объектов будет скопирован хранилища Озера tooData каждый час. 

**Связанная служба хранения Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Связанная служба Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Сведения о конфигурации, в разделе hello [связанные свойства службы](#linked-service-properties) раздела.
>

**Входной набор данных большого двоичного объекта Azure**

В следующем примере hello, данных берется из нового большого двоичного объекта каждый час (`"frequency": "Hour", "interval": 1`). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует hello год, месяц и день часть времени начала hello. Имя файла Hello использует часть hello время начала часа hello. Hello `"external": true` параметр уведомляет службу hello фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Выходной набор данных Azure Data Lake Store:**

следующие хранилища Озера tooData данных копии пример Hello. Новые данные копируются хранилища Озера tooData каждый час.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Действие копирования в конвейере с BLOB-объектом в качестве источника и Data Lake Store в качестве приемника**

В следующем примере hello, hello конвейера содержит операции копирования, настроенный toouse hello наборы входных и выходных данных. Действие копирования Hello — запланированных toorun каждый час. В определении JSON конвейера hello, hello `source` тип установлен слишком`BlobSource`и hello `sink` тип установлен слишком`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Пример: Копирование данных из хранилища Озера данных Azure tooan BLOB-объектов Azure
пример кода Hello в этом разделе показано:

* Связанная служба типа [AzureDataLakeStore](#linked-service-properties).
* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Входной [набор данных](data-factory-create-datasets.md) типа [AzureDataLakeStore](#dataset-properties).
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, который использует [AzureDataLakeStoreSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Каждый час кода Hello копируется из tooan хранилища Озера данных Azure BLOB-объекта данных временных рядов. 

**Связанная служба Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Сведения о конфигурации, в разделе hello [связанные свойства службы](#linked-service-properties) раздела.
>

**Связанная служба хранения Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Входной набор данных Azure Data Lake**

В этом примере параметр `"external"` слишком`true` информирует hello служба фабрики данных, таблица hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
**Выходной набор данных большого двоичного объекта Azure**

В следующем примере hello, данные записываются новый большой двоичный объект tooa каждый час (`"frequency": "Hour", "interval": 1`). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует hello год, месяц, день и часы часть времени начала hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Действие копирования в конвейере с Azure Data Lake Store в качестве источника и BLOB-объектом в качестве приемника:**

В следующем примере hello, hello конвейера содержит операции копирования, настроенный toouse hello наборы входных и выходных данных. Действие копирования Hello — запланированных toorun каждый час. В определении JSON конвейера hello, hello `source` тип установлен слишком`AzureDataLakeStoreSource`и hello `sink` тип установлен слишком`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

В определении действия копирования hello также можно сопоставить столбцы из hello исходного набора данных toocolumns в наборе данных приемник hello. Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Производительность и настройка
toolearn о hello факторы, влияющие на производительность действие копирования и как toooptimize, разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md) статьи.
