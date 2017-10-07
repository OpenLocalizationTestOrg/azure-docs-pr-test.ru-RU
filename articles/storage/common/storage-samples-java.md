---
title: "Примеры для хранилища aaaAzure с помощью Java | Документы Microsoft"
description: "Просмотрите, загрузите и запустите образцы кода и приложений для хранилища Azure. Обнаружение, Приступая к работе образцы для больших двоичных объектов, очередей, таблиц и файлов, с помощью клиентских библиотек хранилища hello Java."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a>Примеры для службы хранилища Azure с использованием Java

## <a name="java-sample-index"></a>Указатель по примерам для Java

Hello следующей таблице представлены общие сведения о наши примеры репозитория и hello сценарии, описанные в каждой выборке. Щелкните hello ссылки tooview hello соответствующие примеры кода в GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Конечная точка</th><th style="font-size:110%">Сценарий</th><th style="font-size:110%">Пример кода</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Большой двоичный объект</b></td>
<td>Добавление больших двоичных объектов</td> 
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Блочный BLOB-объект</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Шифрование на стороне клиента</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Приступая к работе с шифрованием на стороне клиента Azure в Java</a></td>
</tr> 
<tr> 
<td>Копирование BLOB-объекта</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Create Container (Создание контейнера)</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Delete BLOB (Удаление BLOB-объекта)</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Delete Container (Удаление контейнера)</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Метаданные, свойства и статистика больших двоичных объектов</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>ACL, метаданные и свойства контейнера</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Get Page Ranges (Получение диапазона страницы)</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Пример тестов страничного BLOB-объекта</a></td>
</tr> 
<tr> 
<td>Аренда большого двоичного объекта и контейнера</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Список больших двоичных объектов и контейнеров</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td>Страничный BLOB-объект</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Пример тестов SAS</a></td>
</tr>   
<tr> 
<td>Свойства службы</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr>           
<tr> 
<td>Создание моментального снимка большого двоичного объекта</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Приступая к работе со службой BLOB-объектов Azure на языке Java)</td>
</tr> 
<tr> 
<td rowspan="9"><b>File</b></td>
<td>Создание общих папок, каталогов и файлов</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr>
<tr> 
<td>Удаление общих папок, каталогов и файлов</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Метаданные и свойства каталога</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Скачивание файлов</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Метрики, метаданные и свойства файла</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Свойства службы файлов</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Список каталогов и файлов</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr>
<tr> 
<td>Список общих папок</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr>
<tr> 
<td>Статистика, метаданные и свойства общей папки</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Приступая к работе с файловой службой Azure на языке Java)</td> 
</tr>
<tr> 
<td rowspan="8"><b>Очередь</b></td>
<td>Добавление сообщения</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></td> 
</tr> 
<tr> 
<td>Шифрование на стороне клиента</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></td> 
</tr> 
<tr> 
<td>Создание очередей</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Удаление сообщения и очереди</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Просмотр сообщения</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</td> 
</tr> 
<tr> 
<td>ACL, метаданные и статистика очереди</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Свойства службы очередей</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Сообщение об обновлении</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a> (Приступая к работе со службой очередей Azure на языке Java)</td> 
</tr> 
<tr> 
<td rowspan="7"><b>Таблица</b></td>
<td>Создание таблицы</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Удаление сущности или таблицы</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Вставка, слияние или замена сущностей</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></td> 
</tr> 
<tr> 
<td>Query Entities (Сущности запроса)</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Запросы к таблицам</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Свойства и ACL таблицы</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a> (Приступая к работе со службой таблиц Azure на языке Java)</td> 
</tr> 
<tr> 
<td>Update Entity (Обновление сущности)</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Примеры для клиентской библиотеки хранилища Azure для Java</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Библиотека примеров кода Azure

Полный образец библиотеки tooview hello перейдите toohello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=storage) библиотеку, которая включает примеры для хранилища Azure, можно загрузить и запустить его локально. Hello кода образца библиотеки содержит пример кода в формате ZIP. Кроме того можно просмотреть и клонирование репозитория GitHub hello для каждого образца.

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a>Руководства по началу работы

Извлечение hello следующие руководства, если вам нужны дополнительные сведения о tooinstall и приступить к работе с hello клиентских библиотек хранилища Azure.

* [Getting Started with Azure Blob Service in Java](../blobs/storage-java-how-to-use-blob-storage.md) (Приступая к работе со службой BLOB-объектов Azure на языке Java)
* [Getting Started with Azure Queue Service in Java](../storage-java-how-to-use-queue-storage.md) (Приступая к работе со службой очередей Azure на языке Java)
* [Getting Started with Azure Table Service in Java](../../cosmos-db/table-storage-how-to-use-java.md) (Приступая к работе со службой таблиц Azure на языке Java)
* [Getting Started with Azure File Service in Java](../storage-java-how-to-use-file-storage.md) (Приступая к работе с файловой службой Azure на языке Java)

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о примерах для других языков см. здесь:

* .NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md) (Примеры для службы хранилища Azure с использованием .NET)
* Все остальные языки: [Azure Storage samples](../storage-samples.md) (Примеры для службы хранилища Azure)
