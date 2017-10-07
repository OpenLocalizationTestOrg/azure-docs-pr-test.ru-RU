---
title: "aaaHow toouse хранилища BLOB-объектов из Node.js | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Как toouse хранилища BLOB-объектов из Node.js
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Обзор
В этой статье показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов. образцы Hello записываются через Node.js API hello. Hello сценарии включают как tooupload, список, загрузка и удаление больших двоичных объектов.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Создание приложения Node.js
Инструкции о том, как toocreate приложении Node.js. в разделе [создать веб-приложение Node.js в службе приложений Azure], [построения и развертывания tooan приложений Node.js облачной службы Azure] — с помощью Windows PowerShell , или [построения и развертывания приложения tooAzure web Node.js, с помощью Web Matrix].

## <a name="configure-your-application-tooaccess-storage"></a>Настройка хранилища tooaccess приложения
toouse хранилища Azure необходимо hello пакет SDK хранилища Azure для Node.js, включающий набор библиотек удобства, взаимодействующих со службами REST hello хранилища.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета
1. Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix), toonavigate toohello папку, где создан примера приложение.
2. Тип **npm установить хранилища azure** в командном окне приветствия. Выходные данные команды hello — примерно toohello следующий пример кода.

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
3. Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана. В этой папке найти hello **хранилища azure** пакет, который содержит необходимые хранилища tooaccess библиотеки hello.

### <a name="import-hello-package"></a>Импорт пакета hello
С помощью блокнота или другого текстового редактора, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello предполагаемой toouse хранилища:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
Hello модуль Azure будет считывать переменные среды hello `AZURE_STORAGE_ACCOUNT` и `AZURE_STORAGE_ACCESS_KEY`, или `AZURE_STORAGE_CONNECTION_STRING`, сведения, необходимые учетной записи хранилища Azure tooyour tooconnect. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове **createBlobService**.

Пример настройки переменных среды hello в hello [портал Azure](https://portal.azure.com) Azure веб-приложение в разделе [Node.js веб-приложения с использованием hello службы таблиц Azure].

## <a name="create-a-container"></a>Создание контейнера
Hello **BlobService** объектов позволяет работать с контейнерами и BLOB-объектов. Hello следующий код создает **BlobService** объекта. Добавьте следующее hello вверху hello **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Вы можете анонимный доступ к большой двоичный объект с помощью **createBlobServiceAnonymous** и указать адрес узла hello. Например, воспользуйтесь `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

использовать новый контейнер toocreate **createContainerIfNotExists**. Hello следующий пример кода создает новый контейнер с именем «mycontainer»:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Если контейнер hello вновь создан, `result.created` имеет значение true. Если контейнер hello уже существует, `result.created` имеет значение false. `response`содержит сведения об операции hello, включая сведения hello ETag для контейнера hello.

### <a name="container-security"></a>Безопасность контейнера
По умолчанию все контейнеры частные, и доступ к ним не может быть анонимным. контейнер hello toomake public, его можно открыть анонимно, можно задать уровень доступа для контейнера hello слишком**большого двоичного объекта** или **контейнер**.

* **большой двоичный объект** -позволяет анонимный доступ для чтения tooblob содержимого и метаданных в контейнере, но не toocontainer метаданные, такие как перечисление всех больших двоичных объектов в контейнере
* **контейнер** -разрешает анонимный доступ для чтения tooblob содержимого и метаданных, а также метаданные контейнера

Hello следующий пример кода демонстрирует уровень доступа hello слишком**больших двоичных объектов**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Кроме того, можно изменить уровень доступа hello контейнера с помощью **setContainerAcl** toospecify уровень доступа hello. Hello следующий код уровня toocontainer hello изменения доступа пример:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Hello результат содержит сведения об операции hello, включая текущий hello **ETag** для контейнера hello.

### <a name="filters"></a>Фильтры
Можно применить необязательно фильтрации операций toooperations выполняется с использованием **BlobService**. К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:

```nodejs
function handle (requestOptions, next)
```

После выполнения его предварительной обработки параметров запроса hello, метод hello должен toocall «Далее», передача обратный вызов с hello следующие подписи:

```nodejs
function (returnObject, finalCallback, next)
```

В этот обратный вызов, а после обработки returnObject hello (hello ответ от сервера toohello hello запроса), обратного вызова hello необходимы tooeither рядом вызова, если он существует toocontinue обработки других фильтров, или просто вызвать службу hello tooend finalCallback вызов.

Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**. Hello следующий код создает **BlobService** объект, который использует hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Существует три типа больших двоичных объектов: блочные, страничные и добавочные. Блочные большие двоичные объекты позволяют toomore эффективной загрузки больших объемов данных. Добавочные BLOB-объекты оптимизированы для операций добавления. Страничные BLOB-объекты оптимизированы для операций чтения и записи. Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).

### <a name="block-blobs"></a>Blob-блоки
tooupload данных tooa блочного BLOB-объекта, используйте hello следующие:

* **createBlockBlobFromLocalFile** - создает новый большой двоичный объект и загружает содержимое файла hello
* **createBlockBlobFromStream** - создает новый большой двоичный объект и отправляет hello содержимое потока
* **createBlockBlobFromText** - создает новый большой двоичный объект и загружает содержимое строки hello
* **createWriteStreamToBlockBlob** -предоставляет большой двоичный объект блока записи потока tooa

Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **«myblob»**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Hello `result` возвращаемые этими методами содержится информация о hello операцию, например hello **ETag** hello большого двоичного объекта.

### <a name="append-blobs"></a>Добавочные BLOB-объекты
новый tooa данных tooupload append больших двоичных объектов, используйте hello ниже:

* **createAppendBlobFromLocalFile** - создает новый добавочный большой двоичный объект и загружает содержимое файла hello
* **createAppendBlobFromStream** - создает новый добавочный большой двоичный объект и отправляет hello содержимое потока
* **createAppendBlobFromText** - создает новый добавочный большой двоичный объект и загружает содержимое строки hello
* **createWriteStreamToNewAppendBlob** — создает новый добавочный большой двоичный объект, а затем предоставляет tooit toowrite потока

Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend в существующие tooan блок append большого двоичного объекта, используйте hello следующие:

* **appendFromLocalFile** -добавить содержимое hello tooan файл существующих append больших двоичных объектов
* **appendFromStream** -добавить содержимое hello tooan поток существующих append больших двоичных объектов
* **appendFromText** -добавить содержимое hello tooan строка существующих append больших двоичных объектов
* **appendBlockFromStream** -добавить содержимое hello tooan поток существующих append больших двоичных объектов
* **appendBlockFromText** -добавить содержимое hello tooan строка существующих append больших двоичных объектов

> [!NOTE]
> API-интерфейсы appendFromXXX будет выполнять некоторые вызовы ненужные server быстро tooavoid toofail проверки на стороне клиента. appendBlockFromXXX не будут делать этого.
>
>

Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Blob-страницы
tooupload данных tooa страничного большого двоичного объекта, используйте hello следующие:

* **createPageBlob** — создает новый страничный BLOB-объект заданной длины.
* **createPageBlobFromLocalFile** - создает новый большой двоичный объект страницы и загружает содержимое файла hello
* **createPageBlobFromStream** - создает новый большой двоичный объект страницы и передает hello содержимое потока
* **createWriteStreamToExistingPageBlob** -предоставляет записи потока tooan существующий страничный большой двоичный объект
* **createWriteStreamToNewPageBlob** — создает новый большой двоичный объект страницы, а затем предоставляет tooit toowrite потока

Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Страничные Вlob-объекты состоят из 512-байтовых "страниц". При отправке файлов с размером, не кратным 512, может возникать ошибка.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, используйте hello **listBlobsSegmented** метод. Если вы хотите tooreturn большие двоичные объекты с определенным префиксом, используйте **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Hello `result` содержит `entries` коллекции, который является массивом объектов, которые описывают каждый BLOB-объект. Здравствуйте, если все большие двоичные объекты, не может быть возвращен, `result` также предоставляет `continuationToken`, который может использоваться в качестве hello второй параметр tooretrieve дополнительных записей.

## <a name="download-blobs"></a>Скачивание больших двоичных объектов
toodownload данные из большого двоичного объекта используйте hello ниже:

* **getBlobToLocalFile** -записывает содержимое toofile hello больших двоичных объектов
* **getBlobToStream** -записывает поток tooa содержимое большого двоичного объекта hello
* **getBlobToText** -записывает содержимое большого двоичного объекта hello tooa строку
* **createReadStream** -предоставляет tooread поток из большого двоичного объекта hello

Hello следующем примере кода показано использование **getBlobToStream** toodownload содержимое hello hello **«myblob»** больших двоичных объектов и их сохранения toohello **output.txt** файла с помощью поток:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Hello `result` содержит сведения о больших двоичных объектов hello, включая **ETag** сведения.

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
Наконец, вызовите toodelete большой двоичный объект **deleteBlob**. Здравствуйте, следующий пример кода удаляет hello BLOB-объекта с именем **«myblob»**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Одновременный доступ
blob tooa toosupport одновременный доступ из нескольких клиентов или несколько экземпляров процесса, можно использовать **ETags** или **аренды**.

* **ETag** -предоставляет toodetect способом, который hello большого двоичного объекта или контейнера был изменен другим процессом
* **Аренда** — предоставляет способ tooobtain монопольный, обновляемым, запись или удаление больших двоичных объектов tooa доступ в течение заданного времени

### <a name="etag"></a>ETag
Используйте теги eTag, если требуется tooallow клиентов или экземпляров toowrite toohello блочного большого двоичного объекта или страницы больших двоичных объектов одновременно. Hello ETag можно toodetermine, если hello контейнера или большого двоичного объекта был изменен с момента его изначально чтения или она создана, позволяющий tooavoid перезапись изменений, зафиксированных другим клиентом или процессом.

Можно задать условия ETag с помощью hello необязательно `options.accessConditions` параметра. Hello следующий пример кода только передает hello **test.txt** содержится файл, если hello BLOB-объект уже существует и имеет значение ETag hello `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Если вы используете теги eTag, hello общим шаблоном является:

1. Получите hello ETag результате hello create, список или операции get.
2. Выполнить действие, проверка, hello значение ETag не был изменен.

Если было изменено значение hello, это указывает, что другой клиент или экземпляр изменены hello большого двоичного объекта или контейнера со времени получения hello значение ETag.

### <a name="lease"></a>Lease
Можно приобрести новую аренду с помощью hello **acquireLease** метод, указывая hello большого двоичного объекта или контейнера, на котором необходимо tooobtain аренду на. Например, следующий код hello аренды на **«myblob»**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

В последующих операциях в **«myblob»** необходимо предоставить hello `options.leaseId` параметра. Идентификатор возвращается в виде аренды Hello `result.id` из **acquireLease**.

> [!NOTE]
> По умолчанию срок действия аренды адреса hello бесконечна. Можно указать длительность бессрочной (от 15 до 60 секунд), предоставляя hello `options.leaseDuration` параметра.
>
>

использовать tooremove аренду, **releaseLease**. toobreak аренды, но никто другой не получил новую аренду до истечения hello исходного срока хранения, используя **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Работа с подписями общего доступа
Подписи коллективного доступа (SAS) являются tooblobs безопасным способом tooprovide детального доступа и контейнеров без указания имени учетной записи хранения или ключи. Подписи коллективного доступа чаще используется tooprovide ограниченный доступ tooyour данных, например разрешение мобильное приложение tooaccess больших двоичных объектов.

> [!NOTE]
> Хотя также можно разрешить анонимный доступ tooblobs, подписей общего доступа позволяют более контролируемых tooprovide доступ, как необходимо создать hello SAS.
>
>

Доверенного приложения, такие как облачная служба создает подписанных URL-адресов с помощью hello **generateSharedAccessSignature** из hello **BlobService**и предоставляет его tooan ненадежных или приложения с частичным доверием, например мобильного приложения. Подписи создаются с помощью политики, которая описывает hello начала общего доступа и конечные даты, во время которого hello допустимы подписанных URL-адресов, а также hello доступ уровня предоставленный владельца toohello подписи общего доступа.

Hello следующий пример кода приводит к возникновению ошибки политику общего доступа, позволяющий подписи владельца hello общего доступа tooperform операции считывания в hello **«myblob»** больших двоичных объектов и истечения срока действия 100 минут после hello время ее создания.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Обратите внимание, что сведения об узле hello должен предоставляемых также, при необходимости при владельца подписи общего доступа hello попытке tooaccess hello контейнера.

Hello клиентское приложение затем использует подписанных URL-адресов с **BlobServiceWithSAS** tooperform операций, выполняемых hello большого двоичного объекта. Hello следующие получает сведения **«myblob»**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Поскольку hello общий URL-адреса были созданы с доступом только для чтения, если предпринята toomodify hello больших двоичных объектов, будет возвращена ошибка.

### <a name="access-control-lists"></a>Доступ к спискам управления
Можно также использовать политики управления доступом (ACL) список tooset hello доступа для SAS. Это полезно в том случае, если хотите tooallow несколько клиентов tooaccess контейнера, но добавлены политики различный уровень доступа для каждого клиента.

ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором. Следующий пример кода Hello определяет две политики: для «user1» и для «user2»:

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Следующий пример возвращает кода Hello hello текущего списка управления Доступом для **mycontainer**, а затем добавляет hello новые политики с помощью **setBlobAcl**. Такой подход допускает выполнение:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Один раз hello задан список управления Доступом, можно создать на основе кода hello политики подписанных URL-адресов. Следующий пример кода Hello создает новые подписи общего доступа для «user2»:

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы.

* [Справочник по пакету SDK службы хранилища Azure для API Node][Azure Storage SDK for Node API Reference]
* [Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]
* Репозиторий [пакета SDK хранилища Azure для Node][Azure Storage SDK for Node] на веб-сайте GitHub.
* [Центр разработчиков Node.js.](https://azure.microsoft.com/develop/nodejs/)
* [Перенесите данные с помощью командной строки программу AzCopy hello](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[создать веб-приложение Node.js в службе приложений Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js веб-приложения с использованием hello службы таблиц Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[построения и развертывания приложения tooAzure web Node.js, с помощью Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[построения и развертывания tooan приложений Node.js облачной службы Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
