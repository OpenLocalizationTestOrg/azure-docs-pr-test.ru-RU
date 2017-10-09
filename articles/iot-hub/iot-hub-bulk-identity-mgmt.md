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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="5e167-104">Управление удостоверениями устройств Центра Интернета вещей в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="5e167-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="5e167-105">Каждый центр IoT имеет toocreate ресурсы на устройство можно использовать в службе hello реестра удостоверений.</span><span class="sxs-lookup"><span data-stu-id="5e167-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="5e167-106">Hello удостоверение реестра можно также toocontrol toohello доступа устройств с выходом, конечные точки.</span><span class="sxs-lookup"><span data-stu-id="5e167-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="5e167-107">В этой статье описывается, как удостоверений устройств tooimport и экспорта в массовом tooand из реестра удостоверений.</span><span class="sxs-lookup"><span data-stu-id="5e167-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="5e167-108">Операции импорта и экспорта выполняются в контексте hello *заданий* , позволяющие tooexecute массовых операций службы от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="5e167-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="5e167-109">Hello **RegistryManager** класс включает hello **ExportDevicesAsync** и **ImportDevicesAsync** методы, использующие hello **задания** Платформа.</span><span class="sxs-lookup"><span data-stu-id="5e167-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="5e167-110">Эти методы позволяют tooexport импорта и синхронизировать hello весь реестр удостоверения IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5e167-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="5e167-111">Что такое задания?</span><span class="sxs-lookup"><span data-stu-id="5e167-111">What are jobs?</span></span>

<span data-ttu-id="5e167-112">Использовать удостоверение операциями с реестром hello **задания** системы при hello операции:</span><span class="sxs-lookup"><span data-stu-id="5e167-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="5e167-113">Выполнено потенциально длительное время выполнения сравнение toostandard во время выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="5e167-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="5e167-114">Возвращает большой объем данных toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="5e167-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="5e167-115">Вместо одного вызова API, ожидающих или блокирование hello результат операции hello, hello операции асинхронно создает **задания** концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="5e167-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="5e167-116">Операция Hello, затем немедленно возвращает **JobProperties** объекта.</span><span class="sxs-lookup"><span data-stu-id="5e167-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="5e167-117">Hello, следуя C# кода фрагменте кода показано, как toocreate задания экспорта:</span><span class="sxs-lookup"><span data-stu-id="5e167-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="5e167-118">toouse hello **RegistryManager** класса в коде C#, добавьте hello **Microsoft.Azure.Devices** tooyour пакета NuGet проекта.</span><span class="sxs-lookup"><span data-stu-id="5e167-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="5e167-119">Hello **RegistryManager** класс находится в hello **Microsoft.Azure.Devices** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="5e167-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="5e167-120">Можно использовать hello **RegistryManager** класса tooquery состояние hello hello **задания** hello возвращаются с помощью **JobProperties** метаданных.</span><span class="sxs-lookup"><span data-stu-id="5e167-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="5e167-121">Hello следующий фрагмент кода C# показано, как toopoll toosee каждые пять секунд, если hello задание завершено выполнение:</span><span class="sxs-lookup"><span data-stu-id="5e167-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="5e167-122">Экспорт устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-122">Export devices</span></span>

<span data-ttu-id="5e167-123">Используйте hello **ExportDevicesAsync** метод tooexport hello полностью tooan реестра удостоверений концентратора IoT [хранилища Azure](../storage/index.md) контейнер больших двоичных объектов с помощью [подписи общего доступа](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="5e167-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="5e167-124">Этот метод позволяет toocreate надежного резервные копии вашего сведений об устройстве в контейнер больших двоичных объектов, которым вы управляете.</span><span class="sxs-lookup"><span data-stu-id="5e167-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="5e167-125">Hello **ExportDevicesAsync** метод требует два параметра:</span><span class="sxs-lookup"><span data-stu-id="5e167-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="5e167-126">*Строковый*, содержащий URI контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5e167-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="5e167-127">Этот URI должен содержать маркер SAS, который предоставляет доступ на запись toohello контейнера.</span><span class="sxs-lookup"><span data-stu-id="5e167-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="5e167-128">Задание Hello создает большой двоичный объект блока в эти данные устройства toostore hello сериализации контейнер экспорта.</span><span class="sxs-lookup"><span data-stu-id="5e167-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="5e167-129">маркер SAS Hello необходимо включить эти разрешения:</span><span class="sxs-lookup"><span data-stu-id="5e167-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="5e167-130">Объект *логическое* , указывающее, следует ли tooexclude ключей проверки подлинности из экспорта данных.</span><span class="sxs-lookup"><span data-stu-id="5e167-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="5e167-131">Если задано значение **false**, ключи аутентификации включены в выходные данные экспорта.</span><span class="sxs-lookup"><span data-stu-id="5e167-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="5e167-132">В противном случае экспортируются ключи со значением **null**.</span><span class="sxs-lookup"><span data-stu-id="5e167-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="5e167-133">Hello следующий фрагмент кода C# показано, как tooinitiate задание экспорта, содержащий ключи проверки подлинности устройства в hello экспортировать данные и затем запрашивают завершения:</span><span class="sxs-lookup"><span data-stu-id="5e167-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

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

<span data-ttu-id="5e167-134">Hello задания сохраняет выходные данные в контейнер больших двоичных объектов hello указано как блочного BLOB-объекта с именем hello **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="5e167-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="5e167-135">Hello выходных данных состоит из данных устройств сериализован в JSON, с одним устройством в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="5e167-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="5e167-136">Hello ниже приведен пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="5e167-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Если устройство имеет две данных, данные двойных hello также экспортируются вместе с данными hello устройства. Hello пример этого формата. <span data-ttu-id="5e167-139">Все данные из строки «twinETag» hello до завершения hello — двойных данные.</span><span class="sxs-lookup"><span data-stu-id="5e167-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

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

<span data-ttu-id="5e167-140">Если требуется получить доступ к toothis данных в коде, легко может десериализовать эти данные с помощью hello **ExportImportDevice** класса.</span><span class="sxs-lookup"><span data-stu-id="5e167-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="5e167-141">Hello следующий фрагмент кода C# показано, как tooread сведений об устройстве, который был ранее экспортирован tooa блочный BLOB-объект:</span><span class="sxs-lookup"><span data-stu-id="5e167-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

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
> <span data-ttu-id="5e167-142">Можно также использовать hello **GetDevicesAsync** метод hello **RegistryManager** toofetch класс список устройств.</span><span class="sxs-lookup"><span data-stu-id="5e167-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="5e167-143">Однако такой подход имеет жесткое ограничение в 1000 hello количество устройств объектов, возвращаемых.</span><span class="sxs-lookup"><span data-stu-id="5e167-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="5e167-144">вариант использования для hello ожидается Hello **GetDevicesAsync** метод предназначен для разработки сценариев tooaid отладки и не рекомендуется для рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="5e167-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="5e167-145">Импорт устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-145">Import devices</span></span>

<span data-ttu-id="5e167-146">Hello **ImportDevicesAsync** метод в hello **RegistryManager** класс позволяет tooperform массового импорта и синхронизации операций в реестре удостоверений концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="5e167-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="5e167-147">Как hello **ExportDevicesAsync** метод, hello **ImportDevicesAsync** метод использует hello **задания** framework.</span><span class="sxs-lookup"><span data-stu-id="5e167-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="5e167-148">Соблюдайте осторожность при использовании hello **ImportDevicesAsync** метода, так как в дополнение tooprovisioning новые устройства в реестре удостоверений, его можно также обновить и удалить существующие устройства.</span><span class="sxs-lookup"><span data-stu-id="5e167-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="5e167-149">Операцию импорта отменить нельзя.</span><span class="sxs-lookup"><span data-stu-id="5e167-149">An import operation cannot be undone.</span></span> <span data-ttu-id="5e167-150">Всегда выполнять резервное копирование существующих данных с помощью hello **ExportDevicesAsync** контейнер больших двоичных объектов метод tooanother перед внесением массового изменения реестра tooyour удостоверений.</span><span class="sxs-lookup"><span data-stu-id="5e167-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="5e167-151">Hello **ImportDevicesAsync** метод принимает два параметра:</span><span class="sxs-lookup"><span data-stu-id="5e167-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="5e167-152">Объект *строка* , содержащий URI [хранилища Azure](../storage/index.md) BLOB-объектов контейнера toouse как *ввода* toohello задания.</span><span class="sxs-lookup"><span data-stu-id="5e167-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="5e167-153">Этот URI должен содержать маркер SAS, который предоставляет доступ на чтение контейнера toohello.</span><span class="sxs-lookup"><span data-stu-id="5e167-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="5e167-154">Этот контейнер должен содержать большой двоичный объект с именем hello **devices.txt** , содержащий tooimport данные устройства hello сериализовать в реестре удостоверений.</span><span class="sxs-lookup"><span data-stu-id="5e167-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="5e167-155">Hello импорта данные должны содержать сведений об устройстве в hello формат JSON же, что hello **ExportImportDevice** задания использует при создании **devices.txt** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5e167-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="5e167-156">маркер SAS Hello необходимо включить эти разрешения:</span><span class="sxs-lookup"><span data-stu-id="5e167-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="5e167-157">Объект *строка* , содержащий URI [хранилища Azure](https://azure.microsoft.com/documentation/services/storage/) BLOB-объектов контейнера toouse как *вывода* из задания hello.</span><span class="sxs-lookup"><span data-stu-id="5e167-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="5e167-158">Hello задание создает большой двоичный объект блока в этот контейнер toostore сведений об ошибке из hello завершения импорта **задания**.</span><span class="sxs-lookup"><span data-stu-id="5e167-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="5e167-159">маркер SAS Hello необходимо включить эти разрешения:</span><span class="sxs-lookup"><span data-stu-id="5e167-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="5e167-160">Hello двух параметров может указывать toohello же контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5e167-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="5e167-161">отдельные параметры Hello просто позволяют лучше контролировать данные как контейнер hello выходных данных требуются дополнительные разрешения.</span><span class="sxs-lookup"><span data-stu-id="5e167-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="5e167-162">Hello, следуя C# кода фрагменте кода показано, как tooinitiate задания импорта:</span><span class="sxs-lookup"><span data-stu-id="5e167-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="5e167-163">Этот метод также может быть используется tooimport hello данные для устройства двойных hello.</span><span class="sxs-lookup"><span data-stu-id="5e167-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="5e167-164">Формат Hello hello входные данные hello же hello формате, показанном в hello **ExportDevicesAsync** раздела.</span><span class="sxs-lookup"><span data-stu-id="5e167-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="5e167-165">Таким образом можно повторно импортировать hello экспортированы данные.</span><span class="sxs-lookup"><span data-stu-id="5e167-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="5e167-166">Hello **$metadata** является необязательным.</span><span class="sxs-lookup"><span data-stu-id="5e167-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="5e167-167">Поведение при импорте</span><span class="sxs-lookup"><span data-stu-id="5e167-167">Import behavior</span></span>

<span data-ttu-id="5e167-168">Можно использовать hello **ImportDevicesAsync** hello следующий метод tooperform объема массовых операций в реестре удостоверений:</span><span class="sxs-lookup"><span data-stu-id="5e167-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="5e167-169">Массовая регистрация новых устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="5e167-170">Массовое удаление существующих устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="5e167-171">Массовое изменение состояния (включение или отключение устройств)</span><span class="sxs-lookup"><span data-stu-id="5e167-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="5e167-172">Массовое назначение новых ключей проверки подлинности устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="5e167-173">Массовое автоматическое повторное создание ключей проверки подлинности устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="5e167-174">Массовое обновление данных двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="5e167-174">Bulk update of twin data</span></span>

<span data-ttu-id="5e167-175">Можно выполнять любое сочетание hello предшествующих операций в одном **ImportDevicesAsync** вызова.</span><span class="sxs-lookup"><span data-stu-id="5e167-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="5e167-176">Например, можно зарегистрировать новые устройства и удалить или обновить существующие устройства на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="5e167-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="5e167-177">При использовании вместе с hello **ExportDevicesAsync** метод, все устройства полностью можно переносить из одного tooanother концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="5e167-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="5e167-178">Если файл импорта hello включает две метаданных, эти метаданные перезаписывает существующие метаданные двойных hello.</span><span class="sxs-lookup"><span data-stu-id="5e167-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="5e167-179">Если файл импорта hello не включает две метаданные, затем только hello `lastUpdateTime` обновления метаданных с помощью hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="5e167-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="5e167-180">Используйте hello необязательно **importMode** свойство в hello импорта сериализации данных для каждого устройства toocontrol hello импорта процессов на устройство.</span><span class="sxs-lookup"><span data-stu-id="5e167-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="5e167-181">Hello **importMode** свойство имеет hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="5e167-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="5e167-182">importMode</span><span class="sxs-lookup"><span data-stu-id="5e167-182">importMode</span></span> | <span data-ttu-id="5e167-183">Описание</span><span class="sxs-lookup"><span data-stu-id="5e167-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e167-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="5e167-184">**createOrUpdate**</span></span> |<span data-ttu-id="5e167-185">Если устройство не существует с hello указан **идентификатор**, будет заново зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="5e167-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="5e167-186">Если hello устройства уже существует, сведения о существующем перезаписывается hello, предоставленных входных данных без учета toohello **ETag** значение.</span><span class="sxs-lookup"><span data-stu-id="5e167-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="5e167-187">Hello пользователя можно дополнительно указать двойных данных вместе с данными hello устройства.</span><span class="sxs-lookup"><span data-stu-id="5e167-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="5e167-188">etag двойных Hello, если указано, обрабатываются независимо друг от друга из устройства hello etag.</span><span class="sxs-lookup"><span data-stu-id="5e167-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="5e167-189">Если существует несоответствие с существующие двойных hello etag, toohello файл журнала записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="5e167-190">**создание**</span><span class="sxs-lookup"><span data-stu-id="5e167-190">**create**</span></span> |<span data-ttu-id="5e167-191">Если устройство не существует с hello указан **идентификатор**, будет заново зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="5e167-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="5e167-192">Если устройство hello уже существует, файл журнала toohello записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="5e167-193">Hello пользователя можно дополнительно указать двойных данных вместе с данными hello устройства.</span><span class="sxs-lookup"><span data-stu-id="5e167-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="5e167-194">etag двойных Hello, если указано, обрабатываются независимо друг от друга из устройства hello etag.</span><span class="sxs-lookup"><span data-stu-id="5e167-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="5e167-195">Если существует несоответствие с существующие двойных hello etag, toohello файл журнала записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="5e167-196">**обновить**</span><span class="sxs-lookup"><span data-stu-id="5e167-196">**update**</span></span> |<span data-ttu-id="5e167-197">Если устройство уже существует с hello указан **идентификатор**, существующие данные будут перезаписаны моментальным hello, предоставленных входных данных без учета toohello **ETag** значение.</span><span class="sxs-lookup"><span data-stu-id="5e167-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="5e167-198">Если устройство hello не существует, файл журнала toohello записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="5e167-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="5e167-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="5e167-200">Если устройство уже существует с hello указан **идентификатор**, существующие данные будут перезаписаны моментальным hello, предоставленных входных данных только в том случае, если имеется **ETag** совпадают.</span><span class="sxs-lookup"><span data-stu-id="5e167-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="5e167-201">Если устройство hello не существует, файл журнала toohello записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="5e167-202">При наличии **ETag** несоответствие, ошибка записывается toohello файла журнала.</span><span class="sxs-lookup"><span data-stu-id="5e167-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="5e167-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="5e167-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="5e167-204">Если устройство не существует с hello указан **идентификатор**, будет заново зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="5e167-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="5e167-205">Если hello устройства уже существует, сведения о существующем перезаписывается hello, предоставленных входных данных только в том случае, если имеется **ETag** совпадают.</span><span class="sxs-lookup"><span data-stu-id="5e167-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="5e167-206">При наличии **ETag** несоответствие, ошибка записывается toohello файла журнала.</span><span class="sxs-lookup"><span data-stu-id="5e167-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="5e167-207">Hello пользователя можно дополнительно указать двойных данных вместе с данными hello устройства.</span><span class="sxs-lookup"><span data-stu-id="5e167-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="5e167-208">etag двойных Hello, если указано, обрабатываются независимо друг от друга из устройства hello etag.</span><span class="sxs-lookup"><span data-stu-id="5e167-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="5e167-209">Если существует несоответствие с существующие двойных hello etag, toohello файл журнала записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="5e167-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="5e167-210">**delete**</span></span> |<span data-ttu-id="5e167-211">Если устройство уже существует с hello указан **идентификатор**, она удаляется без учета toohello **ETag** значение.</span><span class="sxs-lookup"><span data-stu-id="5e167-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="5e167-212">Если устройство hello не существует, файл журнала toohello записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="5e167-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="5e167-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="5e167-214">Если устройство уже существует с hello указан **идентификатор**, удаляется только при наличии **ETag** совпадают.</span><span class="sxs-lookup"><span data-stu-id="5e167-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="5e167-215">Если устройство hello не существует, файл журнала toohello записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="5e167-216">Если имеется несоответствие ETag, toohello файл журнала записывается ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e167-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="5e167-217">Если данные сериализации hello не определен явно **importMode** флаг для устройства, то по умолчанию слишком**createOrUpdate** операции импорта hello.</span><span class="sxs-lookup"><span data-stu-id="5e167-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="5e167-218">Пример импорта устройств — массовая подготовка устройств</span><span class="sxs-lookup"><span data-stu-id="5e167-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="5e167-219">Hello следующий код C# показано, как toogenerate удостоверения устройства:</span><span class="sxs-lookup"><span data-stu-id="5e167-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="5e167-220">включают в себя ключи проверки подлинности;</span><span class="sxs-lookup"><span data-stu-id="5e167-220">Include authentication keys.</span></span>
* <span data-ttu-id="5e167-221">Записи, устройства сведения tooa блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="5e167-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="5e167-222">Импортируйте устройства hello в реестре удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="5e167-222">Import hello devices into hello identity registry.</span></span>

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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="5e167-223">Пример импорта устройств — массовое удаление</span><span class="sxs-lookup"><span data-stu-id="5e167-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="5e167-224">Hello следующем образце кода показано, как устройства toodelete hello, добавленные с помощью hello предыдущий пример кода:</span><span class="sxs-lookup"><span data-stu-id="5e167-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

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

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="5e167-225">Получение SAS URI контейнера hello</span><span class="sxs-lookup"><span data-stu-id="5e167-225">Get hello container SAS URI</span></span>

<span data-ttu-id="5e167-226">Hello следующем образце кода показано, как toogenerate [универсальный код Ресурса SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) чтения, записи и удаления разрешений для контейнера BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="5e167-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5e167-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e167-227">Next steps</span></span>

<span data-ttu-id="5e167-228">В этой статье вы узнали, как tooperform пакетных операций для реестра удостоверений hello в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="5e167-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="5e167-229">Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="5e167-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="5e167-230">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5e167-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="5e167-231">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5e167-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="5e167-232">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="5e167-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5e167-233">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5e167-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5e167-234">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="5e167-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
