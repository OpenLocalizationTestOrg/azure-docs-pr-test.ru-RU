---
title: "aaaTransform данных, с помощью действия Hive - Azure | Документы Microsoft"
description: "Дополнительные сведения об использовании hello действие Hive в запросы Hive toorun фабрики данных Azure в кластере HDInsight на запросу или свой собственный."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Преобразование данных с помощью действия Hive в фабрике данных Azure 
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

Hello действие Hive в HDInsight в фабрике данных [конвейера](data-factory-create-pipelines.md) выполняет запросы Hive на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) кластера HDInsight под управлением Windows и Linux. Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.

> [!NOTE] 
> Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье. 

## <a name="syntax"></a>Синтаксис

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
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
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a>Сведения о синтаксисе
| Свойство | Описание | Обязательно |
| --- | --- | --- |
| name |Имя действия hello |Да |
| Описание |Текст, описывающий, какое действие hello используется для |Нет |
| type |HDInsightHive. |Да |
| inputs |Входные данные, используемые действием Hive hello |Нет |
| outputs |Выходные данные, полученные в результате действия Hive hello |Да |
| linkedServiceName (имя связанной службы) |Кластер HDInsight toohello ссылка зарегистрирован как связанной службы в фабрике данных |Да |
| script |Укажите встроенного скрипта Hive hello |Нет |
| script path |Хранилище hello Hive скрипт в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello. Можно использовать либо свойство script, либо свойство scriptPath, но не оба сразу. Имя файла Hello учитывается регистр. |Нет |
| defines |Укажите параметры как пары "ключ значение" для ссылки на куст скрипте hello «hiveconf» |Нет |

## <a name="example"></a>Пример
Давайте рассмотрим пример игры журналы аналитики, где требуется tooidentify hello времени, затраченного пользователями, игры, запускаемого по вашей компании. 

Hello следующий журнал приведен пример игры журнала, который является запятая (`,`) разделены и содержит следующие поля — ProfileID, SessionStart, длительность, SrcIPAddress и GameType hello.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Hello **скрипта Hive** tooprocess эти данные:

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

tooexecute этот куст сценария в конвейере фабрики данных, требуются следующие toodo hello

1. Создание tooregister связанной службы [собственные HDInsight вычислительный кластер](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или настроить [вычислительный кластер HDInsight по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Назовем эту связанную службу HDInsightLinkedService.
2. Создание [связанная служба](data-factory-azure-blob-connector.md) tooconfigure hello подключения tooAzure хранилища BLOB-данных размещение данных hello. Назовем эту связанную службу StorageLinkedService.
3. Создание [наборы данных](data-factory-create-datasets.md) и toohello входных данных, а затем hello выходных данных. Давайте hello вызовов входной набор данных «HiveSampleIn» и hello выходной набор данных «HiveSampleOut»
4. Запрос Hive hello Копировать как файл tooAzure хранилища больших двоичных объектов, настроенную на шаге #2. Если hello хранилища для размещения данных hello отличается от hello одно размещение этот файл запроса, создайте отдельный связанной службой хранилища Azure и tooit в действии hello. Используйте ** scriptPath ** hello путь toospecify toohive-файл запроса и **scriptLinkedService** toospecify hello хранилища Azure, содержащей файл скрипта hello. 
   
   > [!NOTE]
   > Можно также предоставить с помощью hello встроенного скрипта Hive hello в определении действия hello **сценарий** свойство. Не рекомендуется этот подход, а все специальные символы в скрипте hello в документе JSON hello необходимо экранировать toobe может причина отладки проблем. Hello рекомендуется toofollow шаг #4.
   > 
   > 
5. Создайте конвейер с hello HDInsightHive действия. Действие Hello процессов и преобразований данных hello.

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Развертывание конвейера hello. Дополнительные сведения см. в разделе [Создание конвейеров](data-factory-create-pipelines.md). 
7. Отслеживание с помощью мониторинга фабрики данных hello конвейера hello и административные представления. Подробные сведения см. в статье [Мониторинг конвейеров фабрики данных и управление ими](data-factory-monitor-manage-pipelines.md). 

## <a name="specifying-parameters-for-a-hive-script"></a>Настройка параметров для сценария Hive
В этом примере журналы игры ежедневно добавляются в хранилище BLOB-объектов Azure и хранятся в папках, разбитых по дате и времени. Требуется, чтобы скрипт Hive tooparameterize hello и передать входные папку hello динамически во время выполнения, а также выходом hello, разбитый на дату и время.

toouse параметризованные скрипт Hive, выполните следующие hello

* Задать параметры hello в **определяет**.

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* В hello скрипт Hive ссылаться с помощью параметра toohello **${hiveconf: ParameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>См. также
* [Действие Pig](data-factory-pig-activity.md)
* [Действие MapReduce](data-factory-map-reduce.md)
* [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
* [Вызов программ Spark](data-factory-spark.md)
* [Вызов сценариев R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

