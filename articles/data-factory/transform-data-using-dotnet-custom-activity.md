---
title: "Использование настраиваемых действий в конвейере фабрики данных Azure"
description: "Узнайте, как создавать пользовательские действия и использовать их в конвейере фабрики данных Azure."
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: shengc
ms.openlocfilehash: 2674b431ba610bccb92f6b209970af1fab110f48
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Использование настраиваемых действий в конвейере фабрики данных Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Версия 1 — общедоступная](v1/data-factory-use-custom-activities.md)
> * [Версия 2 — предварительная](transform-data-using-dotnet-custom-activity.md)

Существует два типа действий, которые можно использовать в конвейере фабрики данных Azure.

- [Действия перемещения данных](copy-activity-overview.md) для перемещения данных между [поддерживаемыми исходными хранилищами данных и хранилищами данных-приемниками](copy-activity-overview.md#supported-data-stores-and-formats).
- [Действия преобразования данных](transform-data.md) для преобразования данных с помощью служб вычислений, например: в Azure HDInsight, пакетной службе Azure и Машинном обучении Azure. 

Чтобы переместить данные в хранилище данных, которое не поддерживает фабрика данных, и обратно, или чтобы преобразовать или обработать данные способом, который не поддерживается фабрикой данных Azure, создайте **пользовательское действие** с собственной логикой перемещения или преобразования данных и используйте это действие в конвейере. Настраиваемые действия запускают настраиваемую логику кода в пуле **пакетной службы Azure** виртуальных машин.

> [!NOTE]
> Эта статья относится к версии 2 фабрики данных, которая в настоящее время доступна в предварительной версии. Если вы используете службу фабрики данных версии 1 (общедоступная версия), перейдите к статье [Использование настраиваемых действий в конвейере фабрики данных Azure](v1/data-factory-use-custom-activities.md).
 

Если вы еще не знакомы с пакетной службой Azure, см. следующие статьи.

* [Основные сведения о пакетной службе Azure](../batch/batch-technical-overview.md) — общие сведения о пакетной службе Azure.
* Статья о командлете [New-AzureRmBatchAccount](/powershell/module/azurerm.batch/New-AzureRmBatchAccount?view=azurermps-4.3.1) со сведениями о создании учетной записи пакетной службы Azure или статья о [портале Azure](../batch/batch-account-create-portal.md) со сведениями о создании учетной записи пакетной службы Azure с помощью портала Azure. Подробные инструкции по использованию этого командлета см. в статье [Using PowerShell to manage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) (Использование PowerShell для управления учетной записью пакетной службы Azure).
* [New-AzureBatchPool](/powershell/module/azurerm.batch/New-AzureBatchPool?view=azurermps-4.3.1) со сведениями о создании пула пакетной службы Azure.

## <a name="azure-batch-linked-service"></a>Связанная пакетная служба Azure 
Ниже приведен фрагмент кода JSON, который определяет пример связанной пакетной службы Azure. Дополнительные сведения см. в статье [Вычислительные среды, поддерживаемые фабрикой данных Azure](compute-linked-services.md).

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "batchaccount",
            "accessKey": {
                "type": "SecureString",
                "value": "access key"
            },
            "batchUri": "https://batchaccount.region.batch.azure.com",
            "poolName": "poolname",
            "linkedServiceName": {
                "referenceName": "StorageLinkedService",
                "type": "LinkedServiceReference"
            }
        }
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

 Дополнительные сведения о связанной пакетной службе Azure см. в статье [Вычислительные среды, поддерживаемые фабрикой данных Azure](compute-linked-services.md). 

## <a name="custom-activity"></a>Настраиваемое действие

В следующем фрагменте кода JSON определяется конвейер с простым настраиваемым действием. Определение действия содержит ссылку на связанную пакетную службу Azure. 

```json
{
    "name": "MyCustomActivityPipeline",
    "properties": {
      "description": "Custom activity sample",
      "activities": [{
        "type": "Custom",
        "name": "MyCustomActivity",
        "linkedServiceName": {
          "referenceName": "AzureBatchLinkedService",
          "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "command": "helloworld.exe",
          "folderPath": "customactv2/helloworld",
          "resourceLinkedService": {
            "referenceName": "StorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }]
    }
  }
```

В этом примере helloworld.exe является пользовательским приложением, которое хранится в папке customactv2/helloworld учетной записи хранения Azure, используемой в resourceLinkedService. Настраиваемое действие отправляет пользовательское приложение для выполнения в пакетной службе Azure. Вы можете заменить команду на любое предпочитаемое приложение, которое можно выполнить в целевой операционной системе узлов пула пакетной службы Azure. 

В следующей таблице описаны имена и описания свойств, относящихся к этому действию. 

| Свойство              | ОПИСАНИЕ                              | Обязательно |
| :-------------------- | :--------------------------------------- | :------- |
| name                  | Имя действия в конвейере.     | Yes      |
| description           | Описание действия.  | Нет        |
| Тип                  | Для пользовательского действия используется тип действия **Custom**. | Yes      |
| linkedServiceName     | Связанная служба пакетной службы Azure. Дополнительные сведения об этой связанной службе см. в статье [Вычислительные среды, поддерживаемые фабрикой данных Azure](compute-linked-services.md).  | Yes      |
| command               | Команда для выполнения пользовательского приложения. Если приложение уже находится в узле пула пакетной службы Azure, resourceLinkedService и folderPath могут быть пропущены. Например, можно указать команду `cmd /c dir`, которая изначально поддерживается узлом пула пакетной службы Windows. | Yes      |
| resourceLinkedService | Связанная служба хранилища Azure учетной записи хранения, в которой хранится пользовательское приложение. | Нет        |
| folderPath            | Путь к папке пользовательского приложения и всех его зависимостей. | Нет        |
| referenceObjects      | Массив имеющихся связанных служб и наборов данных. Указанные связанные службы и наборы данных передаются в пользовательское приложение в формате JSON. Пользовательский код может использовать ресурсы фабрики данных. | Нет        |
| extendedProperties    | Определенные пользователем свойства, которые могут быть переданы в пользовательское приложение в формате JSON. Пользовательский код может использовать дополнительные свойства. | Нет        |

## <a name="executing-commands"></a>Выполнение команд

Вы можете непосредственно выполнить команду, используя настраиваемое действие. В приведенном ниже примере мы выполняем команду "echo hello world" на целевых узлах пула пакетной службы Azure, которая выводит выходные данные в stdout. 

  ```json
  {
    "name": "MyCustomActivity",
    "properties": {
      "description": "Custom activity sample",
      "activities": [{
        "type": "Custom",
        "name": "MyCustomActivity",
        "linkedServiceName": {
          "referenceName": "AzureBatchLinkedService",
          "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "command": "cmd /c echo hello world"
        }
      }]
    }
  } 
  ```

## <a name="passing-objects-and-properties"></a>Передача объектов и свойств

В этом примере показано, как использовать свойства referenceObjects и extendedProperties для передачи объектов фабрики данных и определенных пользователем свойств в пользовательское приложение. 


```json
{
  "name": "MyCustomActivityPipeline",
  "properties": {
    "description": "Custom activity sample",
    "activities": [{
      "type": "Custom",
      "name": "MyCustomActivity",
      "linkedServiceName": {
        "referenceName": "AzureBatchLinkedService",
        "type": "LinkedServiceReference"
      },
      "typeProperties": {
        "command": "SampleApp.exe",
        "folderPath": "customactv2/SampleApp",
        "resourceLinkedService": {
          "referenceName": "StorageLinkedService",
          "type": "LinkedServiceReference"
        },
        "referenceObjects": {
          "linkedServices": [{
            "referenceName": "AzureBatchLinkedService",
            "type": "LinkedServiceReference"
          }]
        },
        "extendedProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "aSampleSecureString"
            },
            "PropertyBagPropertyName1": "PropertyBagValue1",
            "propertyBagPropertyName2": "PropertyBagValue2",
            "dateTime1": "2015-04-12T12:13:14Z"              
        }
      }
    }]
  }
}
```

При выполнении действия referenceObjects и extendedProperties сохраняются в указанных ниже файлах. Эти файлы будут развернуты в той же папке выполнения SampleApp.exe. 

- activity.json

  Хранит свойство extendedProperties и свойства настраиваемых действий. 

- linkedServices.json

  Хранит массив связанных служб, определенных в свойстве referenceObjects. 

- datasets.json

  Хранит массив наборов данных, определенных в свойстве referenceObjects. 

В следующем примере кода показано, как SampleApp.exe может получить доступ к необходимой информации в JSON-файлах. 

```csharp
using Newtonsoft.Json;
using System;
using System.IO;

namespace SampleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            //From Extend Properties
            dynamic activity = JsonConvert.DeserializeObject(File.ReadAllText("activity.json"));
            Console.WriteLine(activity.typeProperties.extendedProperties.connectionString.value);

            // From LinkedServices
            dynamic linkedServices = JsonConvert.DeserializeObject(File.ReadAllText("linkedServices.json"));
            Console.WriteLine(linkedServices[0].properties.typeProperties.connectionString.value);
        }
    }
}
```

## <a name="retrieve-execution-outputs"></a>Извлечение выходных данных выполнения

  Чтобы запустить выполнение конвейера, выполните следующую команду PowerShell: 

  ```.powershell
  $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName
  ```
  Во время выполнения конвейера его текущие выходные данные можно проверить с помощью следующих команд: 

  ```.powershell
  while ($True) {
      $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

      if(!$result) {
          Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
      }
      elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
          Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
      }
      else {
          Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
          $result
          break
      }
      ($result | Format-List | Out-String)
      Start-Sleep -Seconds 15
  }

  Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
  $result.Output -join "`r`n"

  Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
  $result.Error -join "`r`n"
  ```

  Свойства **stdout** и **stderr** пользовательского приложения сохраняются в контейнер **adfjobs** в связанной службе хранилища Azure, определенной при создании связанной пакетной службы Azure с помощью GUID задания. Вы можете получить подробный путь из выходных данных выполнения действия, как показано в следующем фрагменте кода: 

  ```shell
  Pipeline ' MyCustomActivity' run finished. Result:

  ResourceGroupName : resourcegroupname
  DataFactoryName   : datafactoryname
  ActivityName      : MyCustomActivity
  PipelineRunId     : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  PipelineName      : MyCustomActivity
  Input             : {command}
  Output            : {exitcode, outputs, effectiveIntegrationRuntime}
  LinkedServiceName : 
  ActivityRunStart  : 10/5/2017 3:33:06 PM
  ActivityRunEnd    : 10/5/2017 3:33:28 PM
  DurationInMs      : 21203
  Status            : Succeeded
  Error             : {errorCode, message, failureType, target}

  Activity Output section:
  "exitcode": 0
  "outputs": [
    "https://shengcstorbatch.blob.core.windows.net/adfjobs/<GUID>/output/stdout.txt",
    "https://shengcstorbatch.blob.core.windows.net/adfjobs/<GUID>/output/stderr.txt"
  ]
  "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)"
  Activity Error section:
  "errorCode": ""
  "message": ""
  "failureType": ""
  "target": "MyCustomActivity"
  ```
Если вы хотите использовать содержимое stdout.txt в последующих действиях, путь к файлу stdout.txt можно получить в значении выражения "@activity('MyCustomActivity').output.outputs[0]". 

  > [!IMPORTANT]
  > - Свойства activity.json, linkedServices.json и datasets.json хранятся в папке среды выполнения пакетной задачи. Для этого примера файлы activity.json, linkedServices.json и datasets.json хранятся по адресу https://adfv2storage.blob.core.windows.net/adfjobs/<GUID>/runtime/. При необходимости их следует очищать отдельно. 
  > - Для связанных служб, использующих локальную среду выполнения интеграции, конфиденциальная информация, например ключи или пароли, шифруется локальной средой выполнения интеграции. Это гарантирует, что учетные данные останутся в пределах частных сетевых сред, определенных клиентами. Некоторые поля с конфиденциальными данными, на которые таким образом ссылается пользовательский код приложения, могут отсутствовать. При необходимости в extendedProperties используйте SecureString, а не ссылку на связанную службу. 

## <a name="difference-between-custom-activity-in-azure-data-factory-v2-and-custom-dotnet-activity-in-azure-data-factory-v1"></a>Различия между настраиваемым действием в фабрике данных Azure версии 2 и (настраиваемым) действием DotNet в фабрике данных Azure версии 1 

  В фабрике данных Azure версии 1 вы создавали код (настраиваемого) действия DotNet в отдельном проекте библиотеки классов .Net, используя класс, который реализует метод Execute в интерфейсе IDotNetActivity. Связанные службы, наборы данных и расширенные свойства, входящие в полезные данные JSON для (настраиваемого) действия DotNet, передавались в метод выполнения в виде строго типизированных объектов. Подробнее это описано в статье [о (настраиваемых) действиях DotNet в фабрике данных версии 1](v1/data-factory-use-custom-activities.md). По этой причине пользовательский код нужно писать на .Net Framework 4.5.2 и выполнять на узлах пула пакетной службы Azure под управлением Windows. 

  В настраиваемых действиях фабрики данных Azure версии 2 не нужно реализовать интерфейс .Net. Теперь все команды, скрипты и пользовательский код можно компилировать и выполнять в виде исполняемого файла. Для этого следует указать свойство Command вместе со свойством folderPath. Настраиваемое действие передает указанный исполняемый файл и зависимости в каталог folderPath и выполняет нужную команду. 

  Связанные службы, наборы данных (определенные в объектах referenceObjects) и расширенные свойства, входящие в полезные данные JSON для настраиваемого действия, доступны для исполняемого файла в виде файлов JSON. Вы можете обратиться к нужным свойствам с помощью сериализатора JSON, как показано в предыдущем примере кода SampleApp.exe. 

  Изменения, внесенные в реализацию настраиваемых действий в фабрике данных Azure версии 2, позволяют реализовать логику кода на любом языке и выполнять этот код в любых операционных системах Windows и Linux, которые поддерживает пакетная служба Azure. 

  В следующей таблице описаны различия между настраиваемым действием в фабрике данных версии 2 и (настраиваемым) действием DotNet в фабрике данных версии 1. 


|Различия      |Настраиваемое действие в ADF версии 2      |Настраиваемое действие DotNet в ADF версии 1      |
| ---- | ---- | ---- |
|Способ определения настраиваемой логики      |Путем запуска любого исполняемого файла (использование существующего или реализация своего исполняемого файла)      |Путем реализации библиотеки DLL для .NET      |
|Среда выполнения настраиваемой логики      |Windows или Linux      |Windows (.NET Framework 4.5.2)      |
|Выполнение скриптов      |Поддерживает выполнение скриптов напрямую (например, cmd /c echo hello world на виртуальной машине Windows)      |Требуется реализация в библиотеке DLL для .NET      |
|Обязательный набор данных      |Необязательно      |Является обязательным для создания цепочки действий и передачи данных      |
|Передача данных из действия в настраиваемую логику      |С помощью ReferenceObjects (LinkedServices и Datasets) и ExtendedProperties (пользовательские свойства)      |С помощью ExtendedProperties (пользовательские свойства), входных и выходных наборов данных      |
|Извлечение данных в настраиваемой логике      |Анализ файлов activity.json, linkedServices.json и datasets.json, которые хранятся в одной папке с исполняемым файлом.      |С помощью пакета SDK для .NET (.NET Framework 4.5.2).      |
|Ведение журналов      |Запись непосредственно в STDOUT      |Реализация средства ведения журнала в DLL для .NET      |


  Если у вас есть код .Net, написанный для (настраиваемого) действия DotNet версии 1, вы можете использовать его в настраиваемом действии версии 2. Для этого следует внести некоторые правки в соответствии со следующими рекомендациями:  

   - Преобразуйте проект из библиотеки классов .Net в консольное приложение. 
   - Перенесите приложение в метод Main; метод Execute из интерфейса IDotNetActivity больше не используется. 
   - Примените сериализатор JSON ко всем связанным службам, наборам данных и действиям, которые ранее существовали в виде строго типизированных объектов, и передайте значения нужных свойств в главный код логики вашего приложения. В качестве примера воспользуйтесь представленным выше кодом SampleApp.exe. 
   - Объект средства ведения журнала теперь не поддерживается, а выходные данные исполняемого файла можно вывести в консоль и сохранить в файле stdout.txt. 
   - Пакет NuGet Microsoft.Azure.Management.DataFactories больше не требуется. 
   - Скомпилируйте код, передайте исполняемый файл и зависимости в хранилище Azure и укажите путь к ним в свойстве folderPath. 

Полный пример того, как повторно создать пример комплексной библиотеки DLL и конвейера, описанных в документе [Use custom activities in an Azure Data Factory pipeline](https://docs.microsoft.com/azure/data-factory/v1/data-factory-use-custom-activities) (Использование настраиваемых действий в конвейере фабрики данных Azure) для фабрики данных версии 1, в формате настраиваемого действия фабрики данных версии 2 см. в [примере настраиваемого действия фабрики данных версии 2](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFv2CustomActivitySample). 

## <a name="auto-scaling-of-azure-batch"></a>Автомасштабирование пакетной службы Azure
Можно также создать пул пакетной службы Azure с использованием функции **автомасштабирования** . Например, можно создать пул пакетной службы Azure с нулем выделенных виртуальных машин и формулой автоматического масштабирования на основе числа ожидающих задач. 

Приведенный здесь пример формулы обеспечивает следующее поведение: при создании пула он изначально содержит одну виртуальную машину. Метрика $PendingTasks определяет количество задач в состоянии выполнения и активном состоянии (в очереди).  Формула находит среднее число ожидающих выполнения задач за последние 180 секунд и соответствующим образом задает значение TargetDedicated. Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин. Таким образом, по мере поступления новых задач пул автоматически увеличивается, а по мере их завершения виртуальные машины высвобождаются по одной, и функция автоматического масштабирования уменьшает пул. Значения startingNumberOfVMs и maxNumberofVMs можно настроить в соответствии со своими потребностями.

Формула автоматического масштабирования:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).

Если в пуле используется [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)(значение по умолчанию), пакетной службе может потребоваться 15–30 минут на подготовку виртуальной машины перед выполнением настраиваемого действия.  Если пул использует другое значение autoScaleEvaluationInterval, пакетная служба может затрачивать autoScaleEvaluationInterval плюс 10 минут.


## <a name="next-steps"></a>Дополнительная информация
Ознакомьтесь со следующими ссылками, в которых описаны способы преобразования данных другими способами: 

* [Действие U-SQL](transform-data-using-data-lake-analytics.md)
* [Действие Hive](transform-data-using-hadoop-hive.md)
* [Действие Pig](transform-data-using-hadoop-pig.md)
* [Действие MapReduce](transform-data-using-hadoop-map-reduce.md)
* [Действие потоковой передачи Hadoop](transform-data-using-hadoop-streaming.md)
* [Действие Spark](transform-data-using-spark.md)
* [Создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure](transform-data-using-machine-learning.md)
* [Действие хранимой процедуры](transform-data-using-stored-procedure.md)
