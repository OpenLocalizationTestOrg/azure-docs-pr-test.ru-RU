---
title: "aaaSet и получения объектов, свойств и метаданных в хранилище Azure | Документы Microsoft"
description: "Хранение пользовательских метаданных для объектов в службе хранилища Azure, а также задание и получение свойств системы."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a>Задание и получение свойств и метаданных

Объектов в хранилище Azure поддержка системные свойства и определяемые пользователем метаданные, кроме toohello данных, содержащихся в них. В этой статье описывается управление системные свойства и определяемые пользователем метаданные с hello [клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Свойства системы.** Свойства системы есть у каждого ресурса хранилища. Некоторые из них можно считать или задать, некоторые — только считать. На деле hello некоторые системные свойства соответствуют toocertain стандартные заголовки HTTP. Клиентская библиотека хранилища Azure Hello обслуживает их.

* **Определяемые пользователем метаданные**: определяемые пользователем метаданные — это метаданные, указанные для определенного ресурса в форме hello пары "имя значение". Можно использовать дополнительные значения метаданных toostore ресурсом хранилища. Значения этих дополнительных метаданных только по своему усмотрению и не влияют на поведение hello ресурсов.

Получение значений свойств и метаданных ресурса хранилища выполняется в два этапа. Прежде чем можно будет прочитать эти значения, необходимо явно запросить их по вызывающему Привет **FetchAttributes** метод.

> [!IMPORTANT]
> Значения свойств и метаданных для ресурса хранилища не заполняются только при вызове одного из hello **FetchAttributes** методы.
>
> Если любая из пар имен и значений содержит знаки не из набора ASCII, возвратится ошибка с кодом `400 Bad Request`. Пары имя/значение метаданных являются допустимыми заголовками HTTP и поэтому должен соответствовать tooall ограничений, относящихся к заголовкам HTTP. Для имен и значений, содержащих знаки не из набора ASCII, мы рекомендуем использовать кодировку URL или кодировку Base64.
>

## <a name="setting-and-retrieving-properties"></a>Установка и получение свойств
значения свойств tooretrieve, вызов hello **FetchAttributes** метод на большой двоичный объект или контейнер toopopulate hello свойств, затем считывать значения hello.

tooset свойств объекта, укажите значение свойства hello, а затем вызвать hello **SetProperties** метод.

Hello следующий пример кода создает контейнер, а затем записывает некоторые из его окна консоли tooa значения свойства.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>Установка и получение метаданных
Метаданные можно указать как одну или несколько пар "имя-значение" для BLOB-ресурса или ресурса контейнера. метаданные tooset добавьте пары "имя значение" toohello **метаданные** коллекции hello ресурса, затем вызовите hello **SetMetadata** метод toosave hello значения toohello службы.

> [!NOTE]
> Имя Hello метаданных должны соответствовать toohello соглашения об именовании идентификаторов C#.
>
>

Hello следующий пример кода задает метаданные для контейнера. Одно значение задается с помощью коллекции hello **добавить** метод. Hello других значение задается с помощью синтаксиса неявный ключ значение. Можно использовать любой из способов.

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

метаданные tooretrieve, вызов hello **FetchAttributes** метод toopopulate вашей большого двоичного объекта или контейнера hello **метаданных** коллекции, затем считывать значения hello, как показано в приведенном ниже примере hello.

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
* [Справочные материалы клиентской библиотеки хранилища Azure для .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Клиентская библиотека хранилища Azure для пакетов NuGet .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
