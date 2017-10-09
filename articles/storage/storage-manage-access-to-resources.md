---
title: "aaaEnable открытый доступ чтения для контейнеров и больших двоичных объектов в хранилище больших двоичных объектов Azure | Документы Microsoft"
description: "Узнайте, как toomake контейнеры и большие двоичные объекты доступны для анонимного доступа и как tooaccess их программно."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Управление toocontainers анонимный доступ для чтения и больших двоичных объектов
Можно включить анонимные, открытый доступ на чтение tooa контейнера и BLOB-объектов в хранилище больших двоичных объектов Azure. Таким образом, вы можете предоставить доступ только для чтения toothese ресурсы без предоставления ключа учетной записи и без необходимости подписанного URL-адреса (SAS).

Общий доступ на чтение лучше всего подходит для сценариев, место определенных tooalways большие двоичные объекты будут доступны для анонимного доступа на чтение. Для более точного контроля можно создать подписанный URL-адрес. Подписанные URL-адреса позволяют tooprovide ограниченный доступ при помощи различные разрешения для конкретного периода времени. Дополнительные сведения о создании подписанных URL-адресов см. в статье [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Предоставьте разрешения toocontainers анонимных пользователей и больших двоичных объектов
По умолчанию контейнер и все большие двоичные объекты в ней может обращаться только владелец учетной записи хранилища hello hello. toogive анонимным пользователям разрешения на чтение tooa контейнера и BLOB-объектов, можно задать hello контейнера разрешения tooallow общего доступа. Анонимные пользователи могут считывать большие двоичные объекты в контейнере общедоступный без проверки подлинности запроса hello.

Можно настроить контейнер hello следующие разрешения:

* **Отсутствует общий доступ на чтение:** hello контейнера и BLOB-объектов может осуществляться только владелец учетной записи хранилища hello. Это hello по умолчанию для всех новых контейнеров.
* **Открытый доступ для больших двоичных объектов только чтения:** большие двоичные объекты в контейнере hello может считываться анонимный запрос, но данные контейнера недоступны. Анонимные клиенты не могут перечислять hello большие двоичные объекты в контейнере hello.
* **Полный открытый доступ на чтение.** Все данные контейнера и больших двоичных объектов можно считать с помощью анонимного запроса. Клиенты могут перечислять большие двоичные объекты в контейнере hello с анонимный запрос, но не могут перечислять контейнеры в учетной записи хранилища hello.

Можно использовать следующие разрешения контейнера tooset hello.

* [Портал Azure](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Azure CLI 2.0](storage-azure-cli.md#create-and-manage-blobs)
* Программно с помощью одного из клиентских библиотек хранилища hello или hello REST API

### <a name="set-container-permissions-in-hello-azure-portal"></a>Задание разрешений для контейнера в hello портал Azure
разрешения контейнера tooset в hello [портал Azure](https://portal.azure.com), выполните следующие действия:

1. Откройте ваш **учетной записи хранилища** колонке hello портала. Учетной записи хранилища можно найти, выбрав **учетные записи хранения** в главном меню портала колонке hello.
1. В разделе **службы BLOB-ОБЪЕКТОВ** колонке hello меню, выберите **контейнеры**.
1. Щелкните правой кнопкой мыши строку hello контейнера или tooopen hello hello выберите кнопку с многоточием контейнера **контекстное меню**.
1. Выберите **доступ к политике** в контекстном меню hello.
1. Выберите **тип доступа** из hello раскрывающемся меню.

    ![Диалоговое окно «Изменение метаданных контейнера»](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Назначение разрешений контейнера с помощью .NET
tooset разрешения для контейнера с помощью C# и hello клиентской библиотеки хранилища для .NET, сначала получить hello контейнера существующие разрешения с вызывающему Привет **GetPermissions** метод. Затем набор hello **PublicAccess** свойство для hello **BlobContainerPermissions** объект, возвращаемый hello **GetPermissions** метод. Наконец, вызовите hello **SetPermissions** метод с hello обновлены разрешения.

Следующий пример Hello задает разрешения контейнера hello toofull общего доступа на чтение. toopublic tooset разрешения чтение для больших двоичных объектов, значение hello **PublicAccess** свойство слишком**BlobContainerPublicAccessType.Blob**. задать все разрешения для анонимных пользователей tooremove hello свойство слишком**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Анонимный доступ к контейнерам и большим двоичным объектам
Клиент, который обращается к контейнерам и большим двоичным объектам анонимно, может использовать конструкторы, не требующие учетных данных. Следующие примеры Hello Показать несколькими разными способами ресурсов службы BLOB-объектов tooreference анонимно.

### <a name="create-an-anonymous-client-object"></a>Создание анонимного клиентского объекта
Можно создать новый объект клиента службы для анонимного доступа, предоставляя hello конечной точки службы BLOB-объекта для учетной записи hello. Тем не менее необходимо также знать имя hello контейнера в этой учетной записи, которая доступна для анонимного доступа.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Анонимная ссылка на контейнер
Если у вас есть контейнер tooa hello URL-адрес, который доступна анонимно, можно использовать его tooreference hello контейнера непосредственно.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Анонимная ссылка на большой двоичный объект
При наличии hello URL-адрес tooa blob, которая доступна для анонимного доступа, можно создать ссылку hello больших двоичных объектов, непосредственно с помощью URL-адреса:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Доступные tooanonymous возможности для пользователей
Hello в следующей таблице показаны операции, которые могут быть вызваны анонимным пользователям при ACL контейнера имеет значение tooallow общего доступа.

| Операция REST | Разрешение на полный общий доступ для чтения | Разрешение на общий доступ для чтения только больших двоичных объектов |
| --- | --- | --- |
| Перечисление контейнеров |Только владелец |Только владелец |
| Create Container (Создание контейнера) |Только владелец |Только владелец |
| Get Container Properties (Получение свойств контейнера) |Все |Только владелец |
| Get Container Metadata (Получение метаданных контейнера) |Все |Только владелец |
| Set Container Metadata (Определение метаданных контейнера) |Только владелец |Только владелец |
| Get Container ACL (Получение списка управления доступом для контейнера) |Только владелец |Только владелец |
| Set Container ACL (Задание списка управления доступом для контейнера) |Только владелец |Только владелец |
| Delete Container (Удаление контейнера) |Только владелец |Только владелец |
| List Blobs (Отображение списка BLOB-объектов) |Все |Только владелец |
| Put BLOB (Вставка BLOB-объекта) |Только владелец |Только владелец |
| Get BLOB (Получение BLOB-объекта) |Все |Все |
| Get BLOB Properties (Получение свойств BLOB-объекта) |Все |Все |
| Set BLOB Properties (Задание свойств службы BLOB-объекта) |Только владелец |Только владелец |
| Get BLOB Metadata (Получение метаданных BLOB-объекта) |Все |Все |
| Set BLOB Metadata (Задание метаданных BLOB-объекта) |Только владелец |Только владелец |
| Put Block (Вставка блокировки) |Только владелец |Только владелец |
| Получение списка блоков (только зафиксированные блоки) |Все |Все |
| Получение списка блоков (только незафиксированные блоки или все блоки) |Только владелец |Только владелец |
| Put Block List (Вставка списка блокировки) |Только владелец |Только владелец |
| Delete BLOB (Удаление BLOB-объекта) |Только владелец |Только владелец |
| Копирование BLOB-объекта |Только владелец |Только владелец |
| Создание моментального снимка большого двоичного объекта |Только владелец |Только владелец |
| Lease Blob (Аренда BLOB-объекта) |Только владелец |Только владелец |
| Put Page (Вставка страницы) |Только владелец |Только владелец |
| Get Page Ranges (Получение диапазона страницы) |Все |Все |
| Добавление больших двоичных объектов |Только владелец |Только владелец |

## <a name="next-steps"></a>Дальнейшие действия

* [Проверка подлинности для служб хранилища Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md)
* [Делегирование доступа с помощью подписанного URL-адреса](https://msdn.microsoft.com/library/azure/ee395415.aspx)
