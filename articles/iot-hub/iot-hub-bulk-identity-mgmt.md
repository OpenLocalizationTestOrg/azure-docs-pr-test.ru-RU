---
title: "Импорт и экспорт удостоверений устройств Центра Интернета вещей Azure | Документация Майкрософт"
description: "Сведения об использовании пакета SDK для служб Azure IoT для выполнения массовых операций с реестром удостоверений (импорт и экспорт удостоверений устройств). Операции импорта позволяют создавать, обновлять и удалять удостоверения устройств в пакетном режиме."
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
ms.openlocfilehash: d2a6660b93fee1e1fc24269eb7075e5243ce88ed
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/11/2018
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Управление удостоверениями устройств Центра Интернета вещей в пакетном режиме

В каждом Центре Интернета вещей есть реестр удостоверений, который можно использовать для создания в службе уникальных ресурсов устройства. Реестр удостоверений обеспечивает доступ к конечным точкам, обращенным к устройствам. В этой статье описывается массовый импорт удостоверений устройств в реестр удостоверений и массовый экспорт удостоверений из реестра.

Операции импорта и экспорта выполняются в контексте *заданий*, позволяющих выполнять операции массового обслуживания в Центре Интернета вещей.

Класс **RegistryManager** содержит методы **ExportDevicesAsync** и **ImportDevicesAsync**, которые используют платформу **заданий**. С помощью этих методов можно экспортировать, импортировать и синхронизировать весь реестр удостоверений Центра Интернета вещей.

В этой статье описано использование класса **RegistryManager** и системы **заданий** для выполнения массового импорта устройств в реестр удостоверений центра Интернета вещей и экспорта устройств из него. Вы можете использовать службу подготовки устройств для Центра Интернета вещей, чтобы настроить автоматическую подготовку JIT для одного или нескольких центров Интернета вещей без вмешательства оператора. Дополнительные сведения см. в [документации по подготовке службы][lnk-dps].

## <a name="what-are-jobs"></a>Что такое задания?

Операции реестра удостоверений используют систему **задания**, когда операция

* характеризуется длительным временем выполнения по сравнению со стандартными операциями среды выполнения или же
* возвращает пользователю большой объем данных.

Вместо одного вызова API, ожидающего или блокирующего результат операции, операция асинхронно создает **задание** для этого Центра Интернета вещей. и сразу же возвращает объект **JobProperties**.

В следующем фрагменте кода C# показано, как создать задание экспорта.

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> Чтобы использовать класс **RegistryManager** в коде C#, добавьте в проект пакет NuGet **Microsoft.Azure.Devices**. Класс **RegistryManager** находится в пространстве имен **Microsoft.Azure.Devices**.

Вы можете использовать класс **RegistryManager** для запросов состояния **задания** с помощью возвращенных метаданных **JobProperties**.

В следующем фрагменте кода C# показано, как каждые пять секунд выполнять опрос, чтобы увидеть, завершено ли выполнение задания.

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

Используйте метод **ExportDevicesAsync** для экспорта всего реестра удостоверений Центра Интернета вещей в контейнер больших двоичных объектов [службы хранилища Azure](../storage/index.yml) с помощью [подписанного URL-адреса](../storage/common/storage-security-guide.md#data-plane-security).

Этот метод позволяет создавать надежные резервные копии данных устройства в контейнере BLOB-объектов, которым вы управляете.

Для использования метода **ExportDevicesAsync** требуется два параметра.

* *Строковый*, содержащий URI контейнера больших двоичных объектов. Этот URI должен содержать маркер SAS, который предоставляет доступ на запись в контейнер. Задание создает в этом контейнере блочный BLOB-объект для хранения сериализованных данных экспорта устройств. Маркер SAS должен включать следующие разрешения.

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* *Логический*, указывающий, следует ли исключить из данных экспорта ключи проверки подлинности. Если задано значение **false**, ключи аутентификации включены в выходные данные экспорта. В противном случае экспортируются ключи со значением **null**.

В следующем фрагменте кода C# показано, как запустить задание экспорта, содержащее ключи проверки подлинности устройства в данных экспорта, а затем выполнить запрос данных о завершении:

```csharp
// Call an export job on the IoT Hub to retrieve all devices
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

Задание сохраняет выходные данные в указанном контейнере BLOB-объектов в виде блочного BLOB-объекта с именем **devices.txt**. Выходные данные состоят из сериализованных данных устройств JSON с одним устройством в строке.

В следующем примере показаны выходные данные.

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

При наличии данных двойника устройства они также будут экспортированы вместе с данными устройства. Этот формат приведен в примере ниже. Все данные, начиная со строки twinETag и до конца, являются данными двойника устройства.

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

Если вам нужен доступ к этим данным в коде, их можно легко десериализовать с помощью класса **ExportImportDevice** . В следующем фрагменте кода C# показано, как считать сведения об устройстве, которые ранее были экспортированы в блочный BLOB-объект.

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
> Для получения списка устройств можно использовать метод **GetDevicesAsync** класса **RegistryManager**. Однако такой подход имеет жесткое ограничение в 1000 возвращаемых объектов устройств. Метод **GetDevicesAsync** предназначен для использования в сценариях разработки для упрощения отладки. Он не рекомендуется для производственных рабочих нагрузок.

## <a name="import-devices"></a>Импорт устройств

Метод **ImportDevicesAsync** в классе **RegistryManager** позволяет выполнять операции массового импорта и синхронизации в реестре удостоверений Центра Интернета вещей. Как и метод **ExportDevicesAsync**, метод **ImportDevicesAsync** использует платформу **заданий**.

Использовать метод **ImportDevicesAsync** следует с осторожностью, так как наряду с подготовкой новых устройств в реестре удостоверений он также может обновлять и удалять существующие устройства.

> [!WARNING]
> Операцию импорта отменить нельзя. Прежде чем вносить массовые изменения в реестр удостоверений, всегда необходимо создавать резервную копию существующих данных в другом контейнере больших двоичных объектов с помощью метода **ExportDevicesAsync**.

Метод **ImportDevicesAsync** принимает два следующих параметра.

* *Строка*, содержащая URI контейнера больших двоичных объектов [службы хранилища Azure](../storage/index.yml), в качестве *входных данных* для задания. Этот URI должен содержать маркер SAS, который предоставляет доступ на чтение контейнера. Этот контейнер должен включать большой двоичный объект с именем **devices.txt**, содержащий сериализованные данные устройств для импорта в реестр удостоверений. Импортируемые данные должны включать в себя сведения об устройствах в том же формате JSON, который задание **ExportImportDevice** использует при создании большого двоичного объекта **devices.txt**. Маркер SAS должен включать следующие разрешения.

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* *Строка*, содержащая URI контейнера больших двоичных объектов [службы хранилища Azure](https://azure.microsoft.com/documentation/services/storage/), в качестве *выходных данных* задания. Задание создает в этом контейнере блочный BLOB-объект для хранения сведений об ошибках из завершенного **задания**импорта. Маркер SAS должен включать следующие разрешения.

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> Два параметра могут указывать на один и тот же контейнер BLOB-объектов. Отдельные параметры предоставляют больший уровень контроля над выходными данными, так как для выходного контейнера требуются дополнительные разрешения.

В следующем фрагменте кода C# показано, как инициировать задание импорта.

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Вы можете использовать этот метод, чтобы импортировать данные для двойника устройства. Для входных данных используется тот же формат, который был показан в разделе **ExportDevicesAsync**. Таким образом, экспортированные данные можно импортировать повторно. Параметр **$metadata** является необязательным.

## <a name="import-behavior"></a>Поведение при импорте

Метод **ImportDevicesAsync** можно использовать для выполнения следующих массовых операций в реестре удостоверений.

* Массовая регистрация новых устройств
* Массовое удаление существующих устройств
* Массовое изменение состояния (включение или отключение устройств)
* Массовое назначение новых ключей проверки подлинности устройств
* Массовое автоматическое повторное создание ключей проверки подлинности устройств
* Массовое обновление данных двойника устройства.

Один вызов метода **ImportDevicesAsync** позволяет выполнять любое сочетание приведенных выше операций. Например, можно регистрировать новые устройства и одновременно удалять или обновлять существующие. Если этот метод использовать вместе с методом **ExportDevicesAsync** , можно полностью перенести все устройства из одного центра IoT в другой.

Если файл импорта содержит метаданные двойника устройства, то эти метаданные заменяют метаданные двойника. Если файл импорта не содержит метаданных двойника устройства, то по текущему времени будут обновляться только метаданные `lastUpdateTime`.

Управление процессом импорта на уровне каждого устройства осуществляется с помощью необязательного свойства **importMode** в сериализованных данных импорта для каждого устройства. Свойство **importMode** имеет следующие параметры:

| importMode | ОПИСАНИЕ |
| --- | --- |
| **createOrUpdate** |Если устройство с указанным **идентификатором**не существует, оно регистрируется заново. <br/>Если устройство уже существует, имеющиеся данные заменяются предоставленными входными данными вне зависимости от значения **ETag** . <br> Вместе с данными устройства пользователь может дополнительно указать данные двойника устройства. Значение Etag двойника, если указано, обрабатывается отдельно от значения Etag устройства. При несоответствии между имеющимися значениями Etag двойника в файл журнала записывается ошибка. |
| **создание** |Если устройство с указанным **идентификатором**не существует, оно регистрируется заново. <br/>Если устройство уже существует, в файл журнала записывается ошибка. <br> Вместе с данными устройства пользователь может дополнительно указать данные двойника устройства. Значение Etag двойника, если указано, обрабатывается отдельно от значения Etag устройства. При несоответствии между имеющимися значениями Etag двойника в файл журнала записывается ошибка. |
| **обновить** |Если устройство с указанным **идентификатором** уже существует, имеющиеся данные заменяются предоставленными входными данными вне зависимости от значения **ETag**. <br/>Если устройство не существует, в файл журнала записывается ошибка. |
| **updateIfMatchETag** |Если устройство с указанным **идентификатором** уже существует, имеющиеся данные заменяются предоставленными входными данными только при совпадении **ETag**. <br/>Если устройство не существует, в файл журнала записывается ошибка. <br/>Если имеется несовпадение **ETag** , в файл журнала записывается ошибка. |
| **createOrUpdateIfMatchETag** |Если устройство с указанным **идентификатором**не существует, оно регистрируется заново. <br/>Если устройство уже существует, имеющиеся данные заменяются предоставленными входными данными только при совпадении **ETag** . <br/>Если имеется несовпадение **ETag** , в файл журнала записывается ошибка. <br> Вместе с данными устройства пользователь может дополнительно указать данные двойника устройства. Значение Etag двойника, если указано, обрабатывается отдельно от значения Etag устройства. При несоответствии между имеющимися значениями Etag двойника в файл журнала записывается ошибка. |
| **delete** |Если устройство с указанным **идентификатором** уже существует, оно удаляется вне зависимости от значения **ETag**. <br/>Если устройство не существует, в файл журнала записывается ошибка. |
| **deleteIfMatchETag** |Если устройство с указанным **идентификатором** уже существует, оно удаляется только при совпадении **ETag**. Если устройство не существует, в файл журнала записывается ошибка. <br/>Если имеется несовпадение ETag, в файл журнала записывается ошибка. |

> [!NOTE]
> Если данные сериализации явно не определяют флаг **importMode** для устройства, то по умолчанию используется **createOrUpdate** во время операции импорта.

## <a name="import-devices-example--bulk-device-provisioning"></a>Пример импорта устройств — массовая подготовка устройств

В следующем примере кода C# показано, как создать несколько удостоверений устройств, которые:

* включают в себя ключи проверки подлинности;
* записывают сведения об этом устройстве в блочный BLOB-объект;
* импортируют устройства в реестр удостоверений.

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
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

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
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

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
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

В следующем примере кода показано, как удалить устройства, добавленные с помощью предыдущего примера кода.

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
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

// Step 3: Call import using the same blob to delete all devices
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

## <a name="get-the-container-sas-uri"></a>Получение URI SAS контейнера

В следующем примере кода показано, как создать [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) с разрешениями на чтение, запись и удаление контейнера больших двоичных объектов.

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a>Дополнительная информация

В этой статье вы узнали, как выполнять массовые операции с реестром удостоверений в Центре Интернета вещей. Дополнительные сведения об управлении Центром Интернета вещей в Azure см. по следующим ссылкам:

* [Метрики Центра Интернета вещей][lnk-metrics]
* [Мониторинг операций][lnk-monitor]

Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]
* [Развертывание ИИ на пограничных устройствах с использованием Azure IoT Edge][lnk-iotedge]

Узнайте, как использовать службу подготовки устройств для Центра Интернета вещей, чтобы включить автоматическую подготовку JIT, из следующей статьи: 

* [Служба подготовки устройств для Центра Интернета вещей Azure][lnk-dps]


[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-dps]: https://azure.microsoft.com/documentation/services/iot-dps
