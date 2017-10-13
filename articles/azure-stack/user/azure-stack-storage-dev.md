---
title: "Начало работы со средствами разработки стек хранилища Azure"
description: "Рекомендации, как приступить к работе со средствами разработки стек хранилища Azure"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a>Начало работы со средствами разработки стек хранилища Azure

*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*


Стека Microsoft Azure предоставляет набор служб хранилища, включая хранилище больших двоичных объектов Azure, таблиц и очередей.

Краткое руководство о том, как приступить к использованию средств разработки стек хранилища Azure в этой статье. Более подробные сведения и примеры кода можно найти в хранилище Azure руководства.

Существуют известные различия между хранилища Azure и стек хранилища Azure, включая определенные требования для каждой платформы. Например существуют определенные клиентские библиотеки и требования суффикс конкретной конечной точки для стека Azure. Дополнительные сведения см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).

## <a name="azure-client-libraries"></a>Клиентские библиотеки Azure
Поддерживаемая версия интерфейса API REST для стека хранилища Azure — 2015-04-05. Он не имеет полного контроля четности с последней версией API REST хранилища Azure. Поэтому для клиентских библиотек хранилища, необходимо иметь в виду версию, совместимую с REST API 2015-04-05.


|Клиентская библиотека|Стек Azure поддерживаемая версия|Ссылка|Спецификация конечной точки|
|---------|---------|---------|---------|
|.NET     |6.2.0|Пакет NuGet:<br>[https://www.NuGet.org/Packages/WindowsAzure.Storage/6.2.0](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br>Выпуск GitHub:<br>[https://github.com/Azure/Azure-Storage-NET/releases/Tag/v6.2.1](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|файл app.config|
|Java|4.1.0|Пакет maven:<br>[http://mvnrepository.com/Artifact/COM.Microsoft.Azure/Azure-Storage/4.1.0](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br>Выпуск GitHub:<br> [https://github.com/Azure/Azure-Storage-Java/releases/Tag/v4.1.0](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|Настройка строки подключения|
|Node.js     |1.1.0|Ссылка на NPM:<br>[https://www.npmjs.com/Package/Azure-Storage](https://www.npmjs.com/package/azure-storage)<br>(запуска:`npm install azure-storage@1.1.0)`<br><br>Выпуск Github:<br>[https://github.com/Azure/Azure-Storage-node/releases/Tag/1.1.0](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|Объявление экземпляра службы||C++|2.4.0|Пакет NuGet:<br>[https://www.NuGet.org/Packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>Выпуск GitHub:<br>[https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|Настройка строки подключения|
|C++|2.4.0|Пакет NuGet:<br>[https://www.NuGet.org/Packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>Выпуск GitHub:<br>[https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|Настройка строки подключения|
|PHP|0.15.0|Выпуск GitHub:<br>[https://github.com/Azure/Azure-Storage-PHP/releases/Tag/V0.15.0](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br>Установка через редактор (Подробности см. ниже)|Настройка строки подключения|
|Python     |0.30.0|Пакет PIP-адрес:<br> [https://pypi.Python.org/pypi/Azure-Storage/0.30.0](https://pypi.python.org/pypi/azure-storage/0.30.0)<br>(Запуска:`pip install -v azure-storage==0.30.0)`<br><br>Выпуск GitHub:<br> [https://github.com/Azure/Azure-Storage-Python/releases/Tag/V0.30.0](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|Объявление экземпляра службы|
|Ruby|0.12.1<br>Предварительный просмотр|Пакет RubyGems:<br> [https://rubygems.org/gems/Azure-Storage/Versions/0.12.1.Preview](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br>Выпуск GitHub:<br> [https://github.com/Azure/Azure-Storage-Ruby/releases/Tag/V0.12.1](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|Настройка строки подключения|

> [!NOTE]
> Сведения о PHP<br><br>
>Установка через редактор:
>1. Создайте файл с именем `composer.json` в корне проекта со следующим кодом:<br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. Загрузить [composer.phar](http://getcomposer.org/composer.phar) в корневой папке проекта.
>3. Выполните команду `php composer.phar install`.
>


## <a name="endpoint-declaration"></a>Конечная точка объявления
Конечную точку Azure стек состоит из двух частей: имя области и домена Azure стека.
В комплекте разработки Azure стека, конечная точка по умолчанию — **local.azurestack.external**.
Если вы не знаете о конечной точке, обратитесь к администратору облака.

## <a name="examples"></a>Примеры


### <a name="net"></a>.NET

Стек Azure суффикс конечной точки необходимо указать в файле app.config:

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a>Java

Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a>Node.js

Стек Azure суффикс конечной точки необходимо указать в объявлении экземпляра:

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a>C++

Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a>PHP

Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a>Python

Стек Azure суффикс конечной точки необходимо указать в объявлении экземпляра:

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a>Ruby

Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a>Хранилище BLOB-объектов

Стек Azure применяются следующие учебники хранилища больших двоичных объектов Azure. Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.

* [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Использование хранилища BLOB-объектов из Java](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [Способы использования хранилища больших двоичных объектов из Node.js]... /.. / storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Использование хранилища BLOB-объектов из C++](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Использование хранилища BLOB-объектов из PHP](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [Использование хранилища больших двоичных объектов Azure с Python](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [Использование хранилища BLOB-объектов из Ruby](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a>Хранилище очередей

В следующих учебниках хранилища очередей Azure относятся к Azure стека. Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.

* [Приступая к работе с хранилищем очередей Azure с помощью .NET](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Использование хранилища очередей из Java](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [Использование хранилища очередей из Node.js](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [Использование хранилища очередей из C++](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [Использование хранилища очередей из PHP](../../storage/queues/storage-php-how-to-use-queues.md)
* [Использование хранилища очередей из Python](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [Использование хранилища очередей из Ruby](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a>Хранилище таблиц

В следующих учебниках хранилища таблиц Azure относятся к Azure стека. Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.

* [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Использование табличного хранилища из Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Использование хранилища Azure таблицы из Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Как использовать хранилище таблиц из C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Использование табличного хранилища из PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Как использовать хранилище таблиц в Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Использование табличного хранилища из Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Введение в службу хранилища Microsoft Azure](../../storage/common/storage-introduction.md)