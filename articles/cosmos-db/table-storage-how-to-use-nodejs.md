---
title: "aaaHow toouse хранилище таблиц Azure из Node.js | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Как toouse хранилище таблиц Azure из Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Обзор
В этом разделе показано, как служба tooperform распространенные сценарии, с помощью hello таблиц Azure в приложение Node.js.

Примеры кода Hello в этом разделе предполагается, что у вас уже есть приложение Node.js. Сведения о том, как toocreate приложения Node.js в Azure, смотрите в любом из следующих разделов:

* [Создание веб-приложения Node.js в службе приложений Azure](../app-service-web/app-service-web-get-started-nodejs.md)
* [Построение и развертывание приложения tooAzure web Node.js, с помощью WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Построение и развертывание tooan приложений Node.js облачной службы Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (с помощью Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Настройка вашего приложения tooaccess хранилища Azure
toouse хранилища Azure необходимо hello пакет SDK хранилища Azure для Node.js, включающий набор библиотек удобства, взаимодействующих со службами REST hello хранилища.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>С помощью диспетчера пакетов узла (NPM) tooinstall hello пакета
1. Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix) и перейдите в папку toohello, где вы создали приложение.
2. Тип **npm установить хранилища azure** в командном окне приветствия. Выходные данные команды hello — примерно toohello следующий пример.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана. В этой папке можно найти hello **хранилища azure** пакет, который содержит библиотеки hello потребуется tooaccess хранилище.

### <a name="import-hello-package"></a>Импорт пакета hello
Добавьте следующий код toohello вверху hello hello **server.js** файл в приложении:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
модуль Hello azure будет считывать hello переменных среды AZURE\_ХРАНИЛИЩА\_учетной записи и AZURE\_ХРАНЕНИЯ\_доступа\_ключа или AZURE\_ХРАНЕНИЯ\_подключения \_Строка для tooyour tooconnect сведения, необходимые учетной записи хранилища Azure. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове **TableService**.

Пример настройки переменных среды hello в hello [портал Azure](https://portal.azure.com) на веб-сайт Azure в разделе [Node.js веб-приложения с использованием hello службы таблиц Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Создание таблицы
Hello следующий код создает **TableService** объекта и использует его toocreate новую таблицу. Добавьте следующее hello вверху hello **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Здравствуйте вызов слишком**createTableIfNotExists** создаст новую таблицу с указанным именем hello, если он еще не существует. Hello следующий пример создает новую таблицу с именем «mytable», если он еще не существует:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Hello `result.created` будет `true` Если создается новая таблица, и `false` Если hello таблица уже существует. Hello `response` будет содержать сведения о запросе hello.

### <a name="filters"></a>Фильтры
Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **TableService**. К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:

```nodejs
function handle (requestOptions, next)
```

После выполнения его предварительной обработки параметров запроса hello, метод hello должен toocall «Далее», передача обратный вызов с hello следующие подписи:

```nodejs
function (returnObject, finalCallback, next)
```

В этот обратный вызов, а после обработки returnObject hello (hello ответ от сервера toohello hello запроса), обратного вызова hello необходимы tooeither рядом вызова, если он существует toocontinue обработки других фильтров, или просто вызвав finalCallback в противном случае tooend hello вызов службы.

Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**. Hello следующий код создает **TableService** объект, который использует hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
tooadd сущности, сначала создайте объект, который определяет свойства сущности. Все сущности должны содержать **PartitionKey** и **RowKey**, которые являются уникальные идентификаторы для сущности hello.

* **PartitionKey** -определяет hello секции, хранящиеся в сущности hello
* **RowKey** — уникальным образом идентифицирует сущность hello в секции hello

**PartitionKey** и **RowKey** должны быть строковыми значениями. Дополнительные сведения см. в разделе [hello основные сведения о модели данных службы таблиц](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello ниже приведен пример определения сущности. Обратите внимание, что **dueDate** определяется как тип **Edm.DateTime**. Указание типа hello является необязательным, и типы будут будет выводиться, если не указана.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Для каждой записи есть поле **Timestamp** , значение которого задается Azure при вставке или обновлении сущности.
>
>

Можно также использовать hello **entityGenerator** toocreate сущностей. Hello следующий пример создает hello одной сущности задачи с помощью hello **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd таблицу tooyour сущности передать hello сущности объекта toohello **insertEntity** метод.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Если выполнена операция hello, `result` будет содержать hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) из hello вставить запись и `response` будет содержать сведения об операции hello.

Пример ответа:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> По умолчанию **insertEntity** не возвращает сущности hello вставлены в рамках hello `response` сведения. Если план для выполнения других операций в этой сущности, или если нужна toocache hello сведения, бывает полезно toohave, он возвращается как часть hello `result`. Это можно сделать следующим образом, включив **echoContent** :
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Обновление сущности
Существует несколько методов, доступных tooupdate существующей сущности.

* **replaceEntity** — обновляет имеющуюся сущность с ее заменой.
* **mergeEntity** -обновляет существующую сущность, объединив новых значений свойств в существующей сущности hello
* **insertOrReplaceEntity** — обновляет имеющуюся сущность с ее заменой. Если сущность не существует, будет вставлена новая сущность.
* **insertOrMergeEntity** -обновляет существующую сущность, объединяя новые значения свойств в существующую hello. Если сущность не существует, будет вставлена новая сущность.

Hello ниже приведен пример обновления сущности, используя **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> По умолчанию обновление сущности не проверяет toosee если обновляемые данные hello ранее был изменен другим процессом. toosupport одновременных обновлений:
>
> 1. Получение hello ETag обновляемый объект hello. Это значение возвращается как часть hello `response` для любой операции, связанные сущности и можно извлечь с помощью `response['.metadata'].etag`.
> 2. При выполнении операции обновления на сущность, добавьте новую сущность toohello ранее получить сведения о hello ETag. Например:
>
>       entity2['.metadata'].etag = currentEtag;
> 3. Выполните операцию обновления hello. Если сущность hello была изменена с момента получения hello значение ETag, такие как другой экземпляр приложения, `error` будет возвращаться о том, что не выполнено условие обновления hello, указанный в запросе hello.
>
>

С **replaceEntity** и **mergeEntity**, если hello сущности, которая обновляется не существует, то произойдет сбой операции обновления hello. Поэтому toostore сущности независимо от того, является ли он уже существует, используйте **insertOrReplaceEntity** или **insertOrMergeEntity**.

Hello `result` для успешного обновления операции будет содержать hello **Etag** hello обновить сущности.

## <a name="work-with-groups-of-entities"></a>Работа с группами сущностей
Иногда он делает toosubmit смысле несколько операций друг с другом в tooensure пакета atomic обработки сервером hello. tooaccomplish, использовать hello **TableBatch** класса toocreate пакета, а затем использовать hello **executeBatch** метод **TableService** tooperform hello пакетные операции.

 Следующий пример Hello демонстрируется отправка две сущности в пакете:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Для успешного пакетных операций `result` будет содержать сведения для каждой операции в пакете hello.

### <a name="work-with-batched-operations"></a>Работа с пакетными операциями
Операции добавлены tooa пакета можно проверить, просмотрев hello `operations` свойство. Можно также использовать следующие методы toowork с операциями hello:

* **clear** — удаляет все операции из пакета.
* **getOperations** -возвращает операции в пакете hello
* **hasOperations** -возвращает значение true, если пакет hello содержит операции
* **removeOperations** — удаляет операцию.
* **размер** -возвращает hello количество операций в пакете hello

## <a name="retrieve-an-entity-by-key"></a>Получение сущности по ключу
определенной сущности на основании hello tooreturn **PartitionKey** и **RowKey**, использовать hello **retrieveEntity** метод.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

После завершения этой операции `result` будет содержать сущность hello.

## <a name="query-a-set-of-entities"></a>Запрос набора сущностей
tooquery таблицы, используйте hello **TableQuery** toobuild выражение запроса, с помощью следующих предложений hello объекта:

* **Выберите** -toobe hello полей, возвращаемых запросом hello
* **где** — hello где предложения

  * **and** — условие `and` в предложении where.
  * **or** — условие `or` в предложении where.
* **Начало** -количество элементов toofetch hello

Hello следующий пример строится запрос, возвращающий hello top пяти элементов с PartitionKey «hometasks».

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Так как параметр **select** не используется, возвращаются все поля. tooperform hello запрос к таблице, используйте **queryEntities**. Hello следующий пример использует этот tooreturn запросы к сущностям из «mytable».

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

В случае успешного выполнения `result.entries` будет содержать массив объектов, соответствующих запросу hello. Если hello запроса было невозможно tooreturn все сущности `result.continuationToken` будет отличных*null* и может использоваться как hello третий параметр **queryEntities** tooretrieve дополнительных результатов. Начальный запрос hello, используйте *null* для третьего параметра hello.

### <a name="query-a-subset-of-entity-properties"></a>Запрос подмножества свойств сущности
Таблицы tooa запроса можно получить лишь несколько полей из сущности.
Этот позволяет снизить потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей. Используйте hello **выберите** возвращается предложения и передайте hello имена полей toobe hello. Например, hello следующий запрос возвращает только hello **описание** и **dueDate** поля.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Удаление сущности
Сущность можно удалить с помощью ее ключей раздела и строки. В этом примере hello **task1** объект содержит hello **RowKey** и **PartitionKey** значения toobe сущности hello удален. Затем hello объекта передается toohello **deleteEntity** метод.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Рассмотрите возможность использования теги eTag, при удалении элементов, tooensure, hello элемента еще не были изменены другим процессом. Сведения об использовании тегов ETag см. в разделе [Обновление сущности](#update-an-entity).
>
>

## <a name="delete-a-table"></a>Удаление таблицы
Привет, следующий код удаляет таблицу из учетной записи хранения.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Если неизвестно, существует ли таблица hello, используйте **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Использование маркеров продолжения
При выполнении запросов к таблицам для получения больших объемов результатов следует искать маркеры продолжения. Может существовать больших объемов данных, могут не узнать, если при наличии токен продолжения не создавайте toorecognize запроса.

результаты Hello объекта, возвращенного во время запроса наборов сущностей `continuationToken` свойства при наличии такой токен. Это затем можно использовать при выполнении запроса toocontinue toomove между сущностями hello секции и таблицы.

При выполнении запросов, параметр continuationToken может предоставляться между экземпляром объекта запроса hello и функция обратного вызова hello:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Если проверить hello `continuationToken` объект, свойства будут находиться такие как `nextPartitionKey`, `nextRowKey` и `targetLocation`, которую можно использовать tooiterate по результатам всех hello.

Также есть пример продолжения в пределах репозиторию hello Node.js хранилища Azure на GitHub. Поищите `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Работа с подписями общего доступа
Подписи общего доступа (SAS) являются tootables детального доступа tooprovide безопасным способом, без указания имени учетной записи хранения или ключи. SAS чаще используется tooprovide ограниченный доступ tooyour данных, например разрешение записи tooquery мобильного приложения.

Доверенного приложения, такие как облачная служба создает подписанный URL-адрес с помощью hello **generateSharedAccessSignature** из hello **TableService**и предоставляет его tooan приложения с частичным доверием или без доверия Например, мобильные приложения. Hello SAS создается с помощью политики, которая описывает hello начала и окончания в какой hello действует SAS, а также hello владельца SAS уровня toohello предоставленный доступ.

Hello следующий пример создает новую политику общего доступа, который позволит hello таблицы hello SAS владельца tooquery («r») и истечения срока действия 100 минут после hello время его создания.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Обратите внимание, что сведения об узле hello должен предоставляемых также, при необходимости при владельца SAS hello попытке tooaccess hello таблицы.

Здравствуйте клиентское приложение, а затем использует hello SAS с **TableServiceWithSAS** tooperform операций hello для таблицы. Следующий пример Hello подключается toohello таблицы и выполняет запрос.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Поскольку hello SAS был сформирован с использованием только доступ запроса, если были предпринята попытка tooinsert, обновления или удаления сущности, будет возвращена ошибка.

### <a name="access-control-lists"></a>Списки управления доступом
Также можно использовать политику доступа hello tooset список управления доступом (ACL) для SAS. Это полезно в том случае, если хотите tooallow таблицы hello tooaccess несколько клиентов, но добавлены политики различный уровень доступа для каждого клиента.

ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором. Следующий пример Hello определяет две политики: для «user1» и для «user2»:

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Следующий пример возвращает Hello hello текущего списка управления Доступом для hello **hometasks** таблицы, а затем добавляет hello новые политики с помощью **setTableAcl**. Такой подход допускает выполнение:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Один раз hello ACL было указано, можно создать на основе кода hello политики SAS. Привет, следующий пример создает новый SAS для «user2»:

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы.

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.
* [Пакет SDK службы хранилища Azure для Node](https://github.com/Azure/azure-storage-node) на веб-сайте GitHub.
* [Центр разработчиков Node.js.](/develop/nodejs/)
* [Создание и развертывание tooan приложений Node.js веб-сайте Azure](../app-service-web/app-service-web-get-started-nodejs.md)
