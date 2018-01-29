---
title: "Вызов программы MapReduce из фабрики данных Azure"
description: "Узнайте, как обрабатывать данные путем выполнения программ MapReduce в кластере Azure HDInsight из фабрики данных Azure."
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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 5961395f5ca4e9a6efb019a77dbdf5db5ff1ee38
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
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

> [!NOTE]
> Статья относится к версии 1 фабрики данных, которая является общедоступной версией. Если вы используете версию 2 службы фабрики данных, которая находится на этапе предварительной версии, ознакомьтесь с [преобразованием данных с использованием действий MapReduce в фабрике данных версии 2](../transform-data-using-hadoop-map-reduce.md).


Действие MapReduce HDInsight в [конвейере](data-factory-create-pipelines.md) фабрики данных выполняет программы MapReduce для [вашего собственного](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) кластера HDInsight или кластера HDInsight [по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) под управлением Windows или Linux. Данная статья основана на материалах статьи о [действиях преобразования данных](data-factory-data-transformation-activities.md) , в которой приведен общий обзор преобразования данных и список поддерживаемых действий преобразования.

> [!NOTE] 
> Если вы не знакомы с фабрикой данных Azure, ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md) и [Руководство. Создание первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md) перед ознакомлением с этой статьей.  

## <a name="introduction"></a>Введение
Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб. В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки. В этой статье описывается использование действия MapReduce в HDInsight.

Дополнительную информацию о выполнении сценариев Pig и Hive в кластере HDInsight на основе Windows или Linux из конвейера с помощью действий Pig и Hive в HDInsight см. в статьях [Действие Pig](data-factory-pig-activity.md) и [Действие Hive](data-factory-hive-activity.md). 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON для действия MapReduce в HDInsight
В определении JSON для действия HDInsight: 

1. В поле **тип** для **действия** задайте значение **HDInsight**.
2. Укажите имя класса для свойства **className** .
3. Укажите путь к JAR-файлу, включив в него имя файла для свойства **jarFilePath** .
4. Укажите связанную службу, которая обращается к хранилищу больших двоичных объектов Azure, содержащему JAR-файл для свойства **jarLinkedService** .   
5. Укажите необходимые аргументы для программы MapReduce в разделе **аргументы**. Во время выполнения вы увидите несколько дополнительных аргументов (например, mapreduce.job.tags) платформы MapReduce. Чтобы отличать свои аргументы от аргументов MapReduce, вы можете использовать параметр и значение в качестве аргументов, как показано в следующем примере (-s, --input, --output и т. д — параметры, за которыми сразу следуют их значения).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
С помощью действия MapReduce можно выполнить JAR-файл MapReduce в кластере HDInsight. В приведенном ниже образце определения конвейера JSON действие HDInsight настроено на запуск JAR-файла Mahout.

## <a name="sample-on-github"></a>Пример на GitHub
Вы можете скачать пример использования действия MapReduce в HDInsight на странице [примеров фабрики данных на сайте GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-the-word-count-program"></a>Выполнение программы подсчета слов
Конвейер в этом примере запускает в кластере Azure HDInsight программу подсчета слов MapReduce.   

### <a name="linked-services"></a>Связанные службы
Сначала необходимо создать связанную службу для связи службы хранилища Azure, используемой в кластере Azure HDInsight, с фабрикой данных Azure. При копировании и вставке следующего кода не забудьте заменить **имя** и **ключ учетной записи** именем и ключом хранилища Azure. 

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
Далее необходимо создать связанную службу для связи кластера Azure HDInsight с фабрикой данных Azure. При копировании и вставке следующего кода не забудьте заменить **имя кластера HDInsight** на имя вашего кластера HDInsight и изменить значения имени пользователя и пароля.   

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

### <a name="datasets"></a>Наборы данных
#### <a name="output-dataset"></a>Выходной набор данных
Конвейер в этом примере не принимает никаких входных данных. Следует указать выходной набор данных для действия MapReduce в HDInsight. Это просто фиктивный набор данных, необходимый для соблюдения расписания конвейера.  

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
Конвейер в этом примере имеет только одно действие с типом HDInsightMapReduce. Ниже приведены некоторые важные свойства в JSON. 

| Свойство | Заметки |
|:--- |:--- |
| Тип |Должен быть задан тип **HDInsightMapReduce**. |
| className |Имя класса: **wordcount** |
| jarFilePath |Путь к JAR-файлу, содержащему этот класс. Если вы копируете и вставляете приведенный код, не забудьте изменить имя кластера. |
| jarLinkedService |Служба, связанная со службой хранилища Azure, содержащая JAR-файл. Эта связанная служба ссылается на хранилище, связанное с кластером HDInsight. |
| arguments |Программа подсчета слов принимает два аргумента, входной и выходной. Входной файл — davinci.txt. |
| frequency и interval |Значения этих свойств соответствуют результирующему набору данных. |
| linkedServiceName |Указывает связанную службу HDInsight, созданную ранее. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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
Действие MapReduce можно использовать для запуска программ Spark в кластере HDInsight Spark. Дополнительные сведения см. в разделе [Вызов программ Spark из фабрики данных](data-factory-spark.md).  

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

