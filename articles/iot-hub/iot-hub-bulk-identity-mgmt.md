---
title: "При экспорте aaaImport идентификаторы устройства Azure IoT Hub | Документы Microsoft"
description: "Как toouse hello Azure IoT службы SDK tooperform массовой операции с tooimport реестра удостоверений hello и экспортировать удостоверения устройства. Операции импорта позволяют toocreate, update и delete удостоверения устройства в пакетном режиме."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Управление удостоверениями устройств Центра Интернета вещей в пакетном режиме

Каждый центр IoT имеет toocreate ресурсы на устройство можно использовать в службе hello реестра удостоверений. Hello удостоверение реестра можно также toocontrol toohello доступа устройств с выходом, конечные точки. В этой статье описывается, как удостоверений устройств tooimport и экспорта в массовом tooand из реестра удостоверений.

Операции импорта и экспорта выполняются в контексте hello *заданий* , позволяющие tooexecute массовых операций службы от центра IoT.

Hello **RegistryManager** класс включает hello **ExportDevicesAsync** и **ImportDevicesAsync** методы, использующие hello **задания** Платформа. Эти методы позволяют tooexport импорта и синхронизировать hello весь реестр удостоверения IoT hub.

## <a name="what-are-jobs"></a>Что такое задания?

Использовать удостоверение операциями с реестром hello **задания** системы при hello операции:

* Выполнено потенциально длительное время выполнения сравнение toostandard во время выполнения операции.
* Возвращает большой объем данных toohello пользователя.

Вместо одного вызова API, ожидающих или блокирование hello результат операции hello, hello операции асинхронно создает **задания** концентратора IoT. Операция Hello, затем немедленно возвращает **JobProperties** объекта.

Hello, следуя C# кода фрагменте кода показано, как toocreate задания экспорта:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> toouse hello **RegistryManager** класса в коде C#, добавьте hello **Microsoft.Azure.Devices** tooyour пакета NuGet проекта. Hello **RegistryManager** класс находится в hello **Microsoft.Azure.Devices** пространства имен.

Можно использовать hello **RegistryManager** класса tooquery состояние hello hello **задания** hello возвращаются с помощью **JobProperties** метаданных.

Hello следующий фрагмент кода C# показано, как toopoll toosee каждые пять секунд, если hello задание завершено выполнение:

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a>Экспорт устройств

Используйте hello **ExportDevicesAsync** метод tooexport hello полностью tooan реестра удостоверений концентратора IoT [хранилища Azure](../storage/index.md) контейнер больших двоичных объектов с помощью [подписи общего доступа](../storage/common/storage-security-guide.md#data-plane-security).

Этот метод позволяет toocreate надежного резервные копии вашего сведений об устройстве в контейнер больших двоичных объектов, которым вы управляете.

Hello **ExportDevicesAsync** метод требует два параметра:

* *Строковый*, содержащий URI контейнера больших двоичных объектов. Этот URI должен содержать маркер SAS, который предоставляет доступ на запись toohello контейнера. Задание Hello создает большой двоичный объект блока в эти данные устройства toostore hello сериализации контейнер экспорта. маркер SAS Hello необходимо включить эти разрешения:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* Объект *логическое* , указывающее, следует ли tooexclude ключей проверки подлинности из экспорта данных. Если задано значение **false**, ключи аутентификации включены в выходные данные экспорта. В противном случае экспортируются ключи со значением **null**.

Hello следующий фрагмент кода C# показано, как tooinitiate задание экспорта, содержащий ключи проверки подлинности устройства в hello экспортировать данные и затем запрашивают завершения:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

Hello задания сохраняет выходные данные в контейнер больших двоичных объектов hello указано как блочного BLOB-объекта с именем hello **devices.txt**. Hello выходных данных состоит из данных устройств сериализован в JSON, с одним устройством в каждой строке.

Hello ниже приведен пример выходных данных hello.

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Если устройство имеет две данных, данные двойных hello также экспортируются вместе с данными hello устройства. Hello пример этого формата. Все данные из строки «twinETag» hello до завершения hello — двойных данные.

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

Если требуется получить доступ к toothis данных в коде, легко может десериализовать эти данные с помощью hello **ExportImportDevice** класса. Hello следующий фрагмент кода C# показано, как tooread сведений об устройстве, который был ранее экспортирован tooa блочный BLOB-объект:

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> Можно также использовать hello **GetDevicesAsync** метод hello **RegistryManager** toofetch класс список устройств. Однако такой подход имеет жесткое ограничение в 1000 hello количество устройств объектов, возвращаемых. вариант использования для hello ожидается Hello **GetDevicesAsync** метод предназначен для разработки сценариев tooaid отладки и не рекомендуется для рабочих нагрузок.

## <a name="import-devices"></a>Импорт устройств

Hello **ImportDevicesAsync** метод в hello **RegistryManager** класс позволяет tooperform массового импорта и синхронизации операций в реестре удостоверений концентратора IoT. Как hello **ExportDevicesAsync** метод, hello **ImportDevicesAsync** метод использует hello **задания** framework.

Соблюдайте осторожность при использовании hello **ImportDevicesAsync** метода, так как в дополнение tooprovisioning новые устройства в реестре удостоверений, его можно также обновить и удалить существующие устройства.

> [!WARNING]
> Операцию импорта отменить нельзя. Всегда выполнять резервное копирование существующих данных с помощью hello **ExportDevicesAsync** контейнер больших двоичных объектов метод tooanother перед внесением массового изменения реестра tooyour удостоверений.

Hello **ImportDevicesAsync** метод принимает два параметра:

* Объект *строка* , содержащий URI [хранилища Azure](../storage/index.md) BLOB-объектов контейнера toouse как *ввода* toohello задания. Этот URI должен содержать маркер SAS, который предоставляет доступ на чтение контейнера toohello. Этот контейнер должен содержать большой двоичный объект с именем hello **devices.txt** , содержащий tooimport данные устройства hello сериализовать в реестре удостоверений. Hello импорта данные должны содержать сведений об устройстве в hello формат JSON же, что hello **ExportImportDevice** задания использует при создании **devices.txt** больших двоичных объектов. маркер SAS Hello необходимо включить эти разрешения:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* Объект *строка* , содержащий URI [хранилища Azure](https://azure.microsoft.com/documentation/services/storage/) BLOB-объектов контейнера toouse как *вывода* из задания hello. Hello задание создает большой двоичный объект блока в этот контейнер toostore сведений об ошибке из hello завершения импорта **задания**. маркер SAS Hello необходимо включить эти разрешения:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> Hello двух параметров может указывать toohello же контейнер больших двоичных объектов. отдельные параметры Hello просто позволяют лучше контролировать данные как контейнер hello выходных данных требуются дополнительные разрешения.

Hello, следуя C# кода фрагменте кода показано, как tooinitiate задания импорта:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Этот метод также может быть используется tooimport hello данные для устройства двойных hello. Формат Hello hello входные данные hello же hello формате, показанном в hello **ExportDevicesAsync** раздела. Таким образом можно повторно импортировать hello экспортированы данные. Hello **$metadata** является необязательным.

## <a name="import-behavior"></a>Поведение при импорте

Можно использовать hello **ImportDevicesAsync** hello следующий метод tooperform объема массовых операций в реестре удостоверений:

* Массовая регистрация новых устройств
* Массовое удаление существующих устройств
* Массовое изменение состояния (включение или отключение устройств)
* Массовое назначение новых ключей проверки подлинности устройств
* Массовое автоматическое повторное создание ключей проверки подлинности устройств
* Массовое обновление данных двойника устройства.

Можно выполнять любое сочетание hello предшествующих операций в одном **ImportDevicesAsync** вызова. Например, можно зарегистрировать новые устройства и удалить или обновить существующие устройства на hello то же время. При использовании вместе с hello **ExportDevicesAsync** метод, все устройства полностью можно переносить из одного tooanother концентратора IoT.

Если файл импорта hello включает две метаданных, эти метаданные перезаписывает существующие метаданные двойных hello. Если файл импорта hello не включает две метаданные, затем только hello `lastUpdateTime` обновления метаданных с помощью hello текущее время.

Используйте hello необязательно **importMode** свойство в hello импорта сериализации данных для каждого устройства toocontrol hello импорта процессов на устройство. Hello **importMode** свойство имеет hello следующие параметры:

| importMode | Описание |
| --- | --- |
| **createOrUpdate** |Если устройство не существует с hello указан **идентификатор**, будет заново зарегистрирован. <br/>Если hello устройства уже существует, сведения о существующем перезаписывается hello, предоставленных входных данных без учета toohello **ETag** значение. <br> Hello пользователя можно дополнительно указать двойных данных вместе с данными hello устройства. etag двойных Hello, если указано, обрабатываются независимо друг от друга из устройства hello etag. Если существует несоответствие с существующие двойных hello etag, toohello файл журнала записывается ошибка. |
| **создание** |Если устройство не существует с hello указан **идентификатор**, будет заново зарегистрирован. <br/>Если устройство hello уже существует, файл журнала toohello записывается ошибка. <br> Hello пользователя можно дополнительно указать двойных данных вместе с данными hello устройства. etag двойных Hello, если указано, обрабатываются независимо друг от друга из устройства hello etag. Если существует несоответствие с существующие двойных hello etag, toohello файл журнала записывается ошибка. |
| **обновить** |Если устройство уже существует с hello указан **идентификатор**, существующие данные будут перезаписаны моментальным hello, предоставленных входных данных без учета toohello **ETag** значение. <br/>Если устройство hello не существует, файл журнала toohello записывается ошибка. |
| **updateIfMatchETag** |Если устройство уже существует с hello указан **идентификатор**, существующие данные будут перезаписаны моментальным hello, предоставленных входных данных только в том случае, если имеется **ETag** совпадают. <br/>Если устройство hello не существует, файл журнала toohello записывается ошибка. <br/>При наличии **ETag** несоответствие, ошибка записывается toohello файла журнала. |
| **createOrUpdateIfMatchETag** |Если устройство не существует с hello указан **идентификатор**, будет заново зарегистрирован. <br/>Если hello устройства уже существует, сведения о существующем перезаписывается hello, предоставленных входных данных только в том случае, если имеется **ETag** совпадают. <br/>При наличии **ETag** несоответствие, ошибка записывается toohello файла журнала. <br> Hello пользователя можно дополнительно указать двойных данных вместе с данными hello устройства. etag двойных Hello, если указано, обрабатываются независимо друг от друга из устройства hello etag. Если существует несоответствие с существующие двойных hello etag, toohello файл журнала записывается ошибка. |
| **delete** |Если устройство уже существует с hello указан **идентификатор**, она удаляется без учета toohello **ETag** значение. <br/>Если устройство hello не существует, файл журнала toohello записывается ошибка. |
| **deleteIfMatchETag** |Если устройство уже существует с hello указан **идентификатор**, удаляется только при наличии **ETag** совпадают. Если устройство hello не существует, файл журнала toohello записывается ошибка. <br/>Если имеется несоответствие ETag, toohello файл журнала записывается ошибка. |

> [!NOTE]
> Если данные сериализации hello не определен явно **importMode** флаг для устройства, то по умолчанию слишком**createOrUpdate** операции импорта hello.

## <a name="import-devices-example--bulk-device-provisioning"></a>Пример импорта устройств — массовая подготовка устройств

Hello следующий код C# показано, как toogenerate удостоверения устройства:

* включают в себя ключи проверки подлинности;
* Записи, устройства сведения tooa блочного большого двоичного объекта.
* Импортируйте устройства hello в реестре удостоверений hello.

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a>Пример импорта устройств — массовое удаление

Hello следующем образце кода показано, как устройства toodelete hello, добавленные с помощью hello предыдущий пример кода:

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a>Получение SAS URI контейнера hello

Hello следующем образце кода показано, как toogenerate [универсальный код Ресурса SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) чтения, записи и удаления разрешений для контейнера BLOB-объектов:

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a>Дальнейшие действия

В этой статье вы узнали, как tooperform пакетных операций для реестра удостоверений hello в центр IoT. Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.

* [Метрики Центра Интернета вещей][lnk-metrics]
* [Мониторинг операций][lnk-monitor]

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]
* [Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
