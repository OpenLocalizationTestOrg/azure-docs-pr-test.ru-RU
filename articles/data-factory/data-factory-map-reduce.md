---
title: "aaaInvoke программу MapReduce из фабрики данных Azure"
description: "Узнайте, как кластер tooprocess данных путем запуска на Azure HDInsight программ MapReduce из фабрики данных Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Вызов программы MapReduce из фабрики данных
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

Действие MapReduce в HDInsight в фабрике данных Hello [конвейера](data-factory-create-pipelines.md) выполняет программ MapReduce, на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) кластера HDInsight под управлением Windows и Linux. Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.

> [!NOTE] 
> Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье.  

## <a name="introduction"></a>Введение
Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб. В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки. В этой статье описывает использование hello действие MapReduce в HDInsight.

Дополнительную информацию о выполнении сценариев Pig и Hive в кластере HDInsight на основе Windows или Linux из конвейера с помощью действий Pig и Hive в HDInsight см. в статьях [Действие Pig](data-factory-pig-activity.md) и [Действие Hive](data-factory-hive-activity.md). 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON для действия MapReduce в HDInsight
В hello определение JSON для hello действие HDInsight: 

1. Набор hello **тип** из hello **действия** слишком**HDInsight**.
2. Укажите имя hello hello класса для **className** свойство.
3. Укажите hello путь toohello JAR-файл с именем файла hello для **jarFilePath** свойство.
4. Укажите hello связаны службы, которая ссылается toohello хранилища больших двоичных объектов, содержащий hello JAR-файл для **jarLinkedService** свойство.   
5. Укажите необходимые аргументы для программы MapReduce hello в hello **аргументы** раздела. Во время выполнения, появится несколько дополнительных аргументов (например: mapreduce.job.tags) на основе инфраструктуры MapReduce hello. toodifferentiate аргументов с аргументами MapReduce hello, рассмотрите использование параметра и значение в качестве аргументов, как показано в следующий пример hello (- s,--входных данных, — т. д., выходные данные будут сразу следуют значениями параметров).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
Действие MapReduce в HDInsight toorun hello можно использовать любой файл jar MapReduce в кластере HDInsight. Следующий пример определения JSON конвейера, hello действие HDInsight — hello настроены toorun Mahout JAR-файл.

## <a name="sample-on-github"></a>Пример на GitHub
Вы можете загрузить пример использования hello действие MapReduce в HDInsight из: [фабрики образцы данных на сайте GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Запуск программы Статистика hello
конвейер Hello в этом примере запускается hello Статистика Map/Reduce программы в кластере Azure HDInsight.   

### <a name="linked-services"></a>Связанные службы
Сначала необходимо создать hello toolink связанной службы хранилища Azure, используемой фабрики данных Azure toohello кластера Azure HDInsight hello. Если вы скопируйте и вставьте следующий код hello, не забудьте tooreplace **имя учетной записи** и **ключ учетной записи** с именем hello и ключ хранилища Azure. 

#### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Связанная служба Azure HDInsight
Создайте toolink связанной службы фабрики данных Azure toohello кластера Azure HDInsight. Если вы скопируйте и вставьте следующий код hello, замените **имя кластера HDInsight** с именем hello кластер HDInsight и изменение значения имени пользователя и пароля.   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>НАБОРЫ ДАННЫХ
#### <a name="output-dataset"></a>Выходной набор данных
конвейер Hello в этом примере не принимает входные данные. Необходимо указать выходной набор данных для hello действие MapReduce в HDInsight. Этот набор данных — просто пустой набор данных, необходимые toodrive hello конвейера расписание.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Конвейер
конвейер Hello в этом примере имеется только одно действие, которое относится к типу: HDInsightMapReduce. Ниже приведены некоторые важные свойства hello в hello JSON. 

| Свойство | Примечания |
|:--- |:--- |
| type |Hello тип должен быть установлен слишком**HDInsightMapReduce**. |
| className |Имя класса hello: **wordcount** |
| jarFilePath |Путь toohello jar-файл содержит класс hello. Если вы скопируйте и вставьте следующий код hello, не забывайте toochange hello имя кластера hello. |
| jarLinkedService |Связанная служба, которая содержит hello jar-файл хранилища Azure. Эта связанная служба ссылается toohello хранилища, связанного с кластером HDInsight hello. |
| arguments |Программа Hello wordcount принимает два аргумента, входным и выходным. Hello входной файл является файлом davinci.txt hello. |
| frequency и interval |значения этих свойств Hello соответствует hello выходной набор данных. |
| linkedServiceName (имя связанной службы) |ссылается toohello связанной службы HDInsight, был создан ранее. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Запуск программ Spark
Можно использовать программы Spark toorun действие MapReduce в кластере HDInsight Spark. Дополнительные сведения см. в разделе [Вызов программ Spark из фабрики данных](data-factory-spark.md).  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>См. также
* [Действие Hive](data-factory-hive-activity.md)
* [Действие Pig](data-factory-pig-activity.md)
* [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
* [Вызов программ Spark](data-factory-spark.md)
* [Вызов сценариев R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

