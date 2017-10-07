---
title: "aaaTransform данные, используя действие потоковой передачи Hadoop - Azure | Документы Microsoft"
description: "Дополнительные сведения об использовании hello действие потоковой передачи Hadoop данных tootransform фабрики данных Azure путем запуска программ потоковой передачи Hadoop на запросу или ваш собственный кластер HDInsight."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Преобразование данных с помощью действия потоковой передачи Hadoop в фабрике данных Azure
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

Можно использовать hello HDInsightStreamingActivity действия вызова задания потоковой передачи Hadoop из конвейера фабрики данных Azure. Hello следующем фрагменте JSON показан синтаксис hello использования hello HDInsightStreamingActivity в файле JSON конвейера. 

Hello действие потоковой передачи HDInsight в фабрике данных [конвейера](data-factory-create-pipelines.md) выполняет программ потоковой передачи Hadoop на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight под управлением Windows и Linux кластер. Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.

> [!NOTE] 
> Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье. 

## <a name="json-sample"></a>Образец JSON
кластер HDInsight Hello автоматически заполняется пример программы (wc.exe и cat.exe) и данные (davinci.txt). По умолчанию имя контейнера hello, используемой кластером HDInsight hello — hello имя самого кластера hello. Например если myhdicluster имя кластера, имя связанный контейнер больших двоичных объектов hello будет myhdicluster. 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

Обратите внимание hello после точки.

1. Набор hello **linkedServiceName** toohello имя hello связанной службы, которая указывает tooyour кластера HDInsight, на какие hello потоковой передачи mapreduce задание запускается.
2. Задайте тип hello hello действия слишком**HDInsightStreaming**.
3. Для hello **сопоставления** свойство, укажите имя исполняемого файла модуля сопоставления hello. В примере hello cat.exe является исполняемого файла модуля сопоставления hello.
4. Для hello **редуктора** свойство, укажите имя исполняемого файла редуктора hello. В примере hello wc.exe — исполняемого файла редуктора hello.
5. Для hello **ввода** свойство type, укажите hello входного файла (в том числе расположение hello) для сопоставления hello. В примере hello: «wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt»: adfsample — контейнер больших двоичных объектов hello, пример/data/Gutenberg — папка hello и davinci.txt — hello большого двоичного объекта.
6. Для hello **вывода** свойство type, укажите hello выходного файла (в том числе расположение hello) для hello редуктора. выходные данные задания потоковой передачи Hadoop hello Hello записывается toohello расположение, заданное для этого свойства.
7. В hello **filePaths** статьи, укажите пути hello для исполняемых файлов сопоставления и редуктора hello. В примере hello: «adfsample/example/apps/wc.exe» adfsample — hello контейнер больших двоичных объектов, example/apps — папка hello и wc.exe — hello исполняемый файл.
8. Для hello **fileLinkedService** свойство, укажите hello связанной службы, которая представляет hello хранилища Azure, содержащей hello файлы, указанные в разделе filePaths hello хранилища Azure.
9. Для hello **аргументы** свойство, задайте аргументы hello для потоковой передачи задания hello.
10. Hello **getDebugInfo** свойство — это необязательный элемент. Если он имеет значение tooFailure, hello журналы будут загружены только при сбое. Если он имеет значение tooAlways, журналы, загружаются всегда независимо от состояния выполнения hello.

> [!NOTE]
> Как показано в примере hello, можно указать выходной набор данных для hello действие потоковой передачи Hadoop для hello **выводит** свойство. Этот набор данных — просто пустой набор данных, необходимые toodrive hello конвейера расписание. Нет необходимости toospecify любого входного набора данных для действия "hello" для hello **входов** свойство.  
> 
> 

## <a name="example"></a>Пример
конвейер Hello в этом пошаговом руководстве hello Статистика потоковой передачи Map/Reduce программа будет запущена на кластере Azure HDInsight. 

### <a name="linked-services"></a>Связанные службы
#### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure
Сначала необходимо создать hello toolink связанной службы хранилища Azure, используемой фабрики данных Azure toohello кластера Azure HDInsight hello. Если вы скопируйте и вставьте следующий код hello, не забудьте tooreplace учетной записи имя и учетную запись с именем hello и ключ хранилища Azure. 

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
Создайте toolink связанной службы фабрики данных Azure toohello кластера Azure HDInsight. Если вы скопируйте и вставьте следующий код hello, замените имя кластера HDInsight hello имя кластера HDInsight и измените значения имени пользователя и пароля. 

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
конвейер Hello в этом примере не принимает входные данные. Необходимо указать выходной набор данных для hello действие потоковой передачи HDInsight. Этот набор данных — просто пустой набор данных, необходимые toodrive hello конвейера расписание. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Конвейер
конвейер Hello в этом примере имеется только одно действие, которое относится к типу: **HDInsightStreaming**. 

кластер HDInsight Hello автоматически заполняется пример программы (wc.exe и cat.exe) и данные (davinci.txt). По умолчанию имя контейнера hello, используемой кластером HDInsight hello — hello имя самого кластера hello. Например если myhdicluster имя кластера, имя связанный контейнер больших двоичных объектов hello будет myhdicluster.  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>См. также
* [Действие Hive](data-factory-hive-activity.md)
* [Действие Pig](data-factory-pig-activity.md)
* [Действие MapReduce](data-factory-map-reduce.md)
* [Вызов программ Spark](data-factory-spark.md)
* [Вызов сценариев R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

