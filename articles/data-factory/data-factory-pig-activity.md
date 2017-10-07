---
title: "Использование Pig действия в фабрике данных Azure данных aaaTransform | Документы Microsoft"
description: "Дополнительные сведения об использовании hello действие Pig в скриптах Pig toorun фабрики данных Azure в кластере HDInsight на запросу или свой собственный."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Преобразование данных с помощью действия Pig в фабрике данных Azure
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Действие Hive](data-factory-hive-activity.md) 
> * [Действие Pig](data-factory-pig-activity.md)
> * [Действие MapReduce](data-factory-map-reduce.md)
> * [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Действие Spark](data-factory-spark.md)
> * [Действие выполнения пакета машинного обучения](data-factory-azure-ml-batch-execution-activity.md)
> * [Действие "Обновить ресурс" в службе машинного обучения](data-factory-azure-ml-update-resource-activity.md)
> * [Действие хранимой процедуры](data-factory-stored-proc-activity.md)
> * [Действие U-SQL в Data Lake Analytics](data-factory-usql-activity.md)
> * [Настраиваемое действие .NET](data-factory-use-custom-activities.md)

Hello действие Pig с HDInsight в фабрике данных [конвейера](data-factory-create-pipelines.md) выполняет запросы Pig на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) кластера HDInsight под управлением Windows и Linux. Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.

> [!NOTE] 
> Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье. 

## <a name="syntax"></a>Синтаксис

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a>Сведения о синтаксисе
| Свойство | Описание | Обязательно |
| --- | --- | --- |
| name |Имя действия hello |Да |
| Описание |Текст, описывающий, какое действие hello используется для |Нет |
| type |HDinsightPig |Да |
| inputs |Один или несколько входов занятая hello действие Pig |Нет |
| outputs |Один или несколько выходов созданные hello действие Pig |Да |
| linkedServiceName (имя связанной службы) |Кластер HDInsight toohello ссылка зарегистрирован как связанной службы в фабрике данных |Да |
| script |Укажите встроенного скрипта Pig hello |Нет |
| script path |Хранить сценарий Pig hello в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello. Можно использовать либо свойство script, либо свойство scriptPath, но не оба сразу. Имя файла Hello учитывается регистр. |Нет |
| defines |Укажите параметры как пары "ключ значение" для ссылки в пределах hello сценарий Pig |Нет |

## <a name="example"></a>Пример
Давайте рассмотрим пример игры журналы аналитики, место tooidentify hello времени, затраченного игроки, игры, запускаемого по вашей компании.

Следующий пример игры журнала Hello — это файл запятыми (,). Он содержит следующие поля — ProfileID, SessionStart, длительность, SrcIPAddress и GameType hello.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hello **сценарий Pig** tooprocess эти данные:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

tooexecute Pig для этого сценария в конвейере фабрики данных hello следующие шаги:

1. Создание tooregister связанной службы [собственные HDInsight вычислительный кластер](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или настроить [вычислительный кластер HDInsight по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Назовем эту связанную службу **HDInsightLinkedService**.
2. Создание [связанная служба](data-factory-azure-blob-connector.md) tooconfigure hello подключения tooAzure хранилища BLOB-данных размещение данных hello. Назовем эту связанную службу **StorageLinkedService**.
3. Создание [наборы данных](data-factory-create-datasets.md) и toohello входных данных, а затем hello выходных данных. Давайте назовем входного набора данных hello **PigSampleIn** и hello выходной набор данных **PigSampleOut**.
4. Скопируйте запрос Pig hello в файл hello хранилища больших двоичных объектов, настроенную на шаге #2. Если hello хранилища Azure, на котором размещена hello данных отличается от hello один, на котором размещается файл запрос hello, создайте отдельный связанной службой хранилища Azure. См. в связанных toohello службы в конфигурации действия hello. Используйте ** scriptPath ** файл сценария toopig путь hello toospecify и **scriptLinkedService**. 
   
   > [!NOTE]
   > Можно также предоставить с помощью hello hello встроенного скрипта Pig в определении действия hello **сценарий** свойство. Однако не рекомендуется этот подход, как все специальные символы в скрипте hello должен toobe escape-последовательность и может вызвать проблемы отладки. Hello рекомендуется toofollow шаг #4.
   > 
   > 
5. Создайте конвейер hello с hello HDInsightPig действия. Это действие обрабатывает входные данные hello путем выполнения сценария Pig в кластере HDInsight.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. Развертывание конвейера hello. Дополнительные сведения см. в разделе [Создание конвейеров](data-factory-create-pipelines.md). 
7. Отслеживание с помощью мониторинга фабрики данных hello конвейера hello и административные представления. Подробные сведения см. в статье [Мониторинг конвейеров фабрики данных и управление ими](data-factory-monitor-manage-pipelines.md).

## <a name="specifying-parameters-for-a-pig-script"></a>Указание параметров для сценария Pig
Рассмотрим следующий пример hello: игры журналы, полученный ежедневно в хранилище больших двоичных объектов Azure и сохраняются в папке секционированные по дате и времени. Сценарий Pig tooparameterize hello и передать входные папку hello динамически во время выполнения, а также выходом hello, разбитый на дату и время.

toouse параметризованные сценарий Pig, выполните hello следующие действия.

* Задать параметры hello в **определяет**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* В hello сценарий Pig, ссылаетесь toohello параметров с помощью "**$parameterName**" как показано в следующий пример hello:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>См. также
* [Действие Hive](data-factory-hive-activity.md)
* [Действие MapReduce](data-factory-map-reduce.md)
* [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
* [Вызов программ Spark](data-factory-spark.md)
* [Вызов сценариев R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

