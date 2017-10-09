---
title: "конвейеры aaaCreate прогнозирующих данных, с помощью фабрики данных Azure | Документы Microsoft"
description: "Описывает, как toocreate создание прогнозирующих конвейеров с помощью фабрики данных Azure и машинного обучения Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure

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

## <a name="introduction"></a>Введение

### <a name="azure-machine-learning"></a>Машинное обучение Azure
[Машинное обучение Azure](https://azure.microsoft.com/documentation/services/machine-learning/) позволяет toobuild, тестировать и развертывать прогнозирующие аналитические решения. Этот процесс можно обобщить до трех этапов.

1. **Создание обучающего эксперимента**. Выполните этот шаг с помощью hello Azure ML Studio. Hello ML studio является коллективную визуальную среду разработки использовать tootrain и проверки модели прогнозирования с помощью обучающих данных.
2. **Преобразовать прогнозной эксперимента tooa**. После обучения модели с существующие данные и будут готовы toouse его tooscore новых данных, подготовки и оптимизировать свой эксперимент оценки.
3. **Развертывание эксперимента в виде веб-службы**. Оценивающий эксперимент можно опубликовать в виде веб-службы Azure. Можно отправлять tooyour модели данных посредством этой конечной точки службы web и получения результатов прогнозов из модели hello.  

### <a name="azure-data-factory"></a>Фабрика данных Azure
Фабрика данных — это служба интеграции данных на основе облака, которая координирует и автоматизирует процессы hello **перемещения** и **преобразования** данных. Можно создать решений по интеграции данных с помощью фабрики данных Azure, можно получать данные из различных хранилищ данных, преобразования или процесс данных hello и публикации хранилищ данных toohello данных результата hello.

Служба фабрики данных позволяет вам toocreate конвейеры данных, перемещения и преобразования данных и запустите конвейеры hello по указанному расписанию (ежечасно, ежедневно, еженедельно, и т. д.). Также предоставляет широкие возможности визуализации toodisplay hello журнала обращений и преобразований, так и зависимости между конвейеры данных и отслеживать все конвейеры данных из найти решение проблем с tooeasily единое представление и установки предупреждений мониторинга.

В разделе [tooAzure введение фабрики данных](data-factory-introduction.md) и [построение первой конвейер](data-factory-build-your-first-pipeline.md) tooquickly статьи Приступая к работе с hello служба фабрики данных Azure.

### <a name="data-factory-and-machine-learning-together"></a>Фабрика данных и машинное обучение вместе
Azure позволяет фабрики данных, вы tooeasily создавать конвейеры, использующих опубликованной [машинного обучения Azure] [ azure-machine-learning] веб-службы для прогнозирования. С помощью hello **действие выполнения пакета** в конвейере фабрики данных Azure, можно вызвать прогнозы toomake машинного Обучения Azure веб-службы на hello данных в пакете. В разделе [вызова машинного Обучения Azure веб-службы с использованием hello действие выполнения пакета](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) подробные сведения см.

Со временем hello прогнозных моделей в экспериментах оценки машинного Обучения Azure hello должны toobe повторное обучение с помощью новых входных наборов данных. Можно повторить Обучение модели машинного Обучения Azure из конвейера фабрики данных, выполнив следующие шаги hello:

1. Опубликуйте эксперимента обучения hello (не прогнозной эксперимента) как веб-службы. На этом шаге hello Azure ML Studio сделать, как в случае tooexpose прогнозной эксперимент как веб-службы в предыдущем сценарии hello.
2. Используйте hello действие выполнения пакета машинного Обучения Azure tooinvoke hello веб-службы для hello эксперимента обучения. По сути можно использовать tooinvoke действие hello Azure ML Пакетное выполнение веб-службы обучения и оценки веб-службы.

После завершения переподготовки, обновите hello оценки веб-службы (прогнозной эксперимент, предоставляемых как веб-службы) с hello вновь обученной модели с помощью hello **действия ресурса обновления машинного Обучения Azure**. Дополнительные сведения см. в статье [Updating Azure Machine Learning models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс").

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Вызов веб-службы с помощью действия выполнения пакета
Перемещение данных tooorchestrate фабрики данных Azure и обработки и затем выполнить пакетное выполнение с помощью машинного обучения Azure. Ниже приведены шаги верхнего уровня hello.

1. Создайте связанную службу Машинного обучения Azure. Требуется hello следующие значения:

   1. **URI запроса** для hello API выполнения пакета. Hello URI запроса можно найти, щелкнув hello **ПАКЕТНОЕ выполнение** ссылку hello веб-странице службы.
   2. **Ключ API** hello опубликованных веб-службы машинного обучения Azure. Ключ API hello можно найти, щелкнув hello веб-службу, которая опубликована.
   3. Используйте hello **AzureMLBatchExecution** действия.

      ![Панель мониторинга машинного обучения](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Универсальный код ресурса (URI) пакета](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Сценарий: Экспериментов с помощью Web service ввода вывода, ссылающиеся toodata в хранилище больших двоичных объектов Azure
В этом сценарии hello Azure Machine Learning, веб-службы делает прогнозов с использованием данных из файла в хранилище больших двоичных объектов и сохраняет результаты прогноза hello в hello хранилища больших двоичных объектов. Hello следующий JSON определяет конвейера фабрики данных с AzureMLBatchExecution действия. Hello действие имеет набор данных hello **DecisionTreeInputBlob** в качестве входного и **DecisionTreeResultBlob** в качестве выходных данных hello. Hello **DecisionTreeInputBlob** передается в качестве входного toohello веб-службы с помощью hello **webServiceInput** свойства JSON. Hello **DecisionTreeResultBlob** передается в качестве выходных данных toohello веб-службы с помощью hello **webServiceOutputs** свойства JSON.  

> [!IMPORTANT]
> Если веб-служба hello принимает несколько входов, использовать hello **webServiceInputs** свойство вместо **webServiceInput**. . В разделе hello [веб-службы требуется несколько входов](#web-service-requires-multiple-inputs) раздела Пример использования свойства webServiceInputs hello.
>
> Наборы данных, на которые ссылается hello **webServiceInput**/**webServiceInputs** и **webServiceOutputs** свойства (в  **typeProperties**) также должно быть включено в действие hello **входов** и **выводит**.
>
> В эксперименте Машинного обучения Azure у входных и выходных портов и глобальных параметров есть имена по умолчанию (input1, input2), которые можно настроить. имя, используемое для webServiceInputs, webServiceOutputs и globalParameters параметры как Hello должен точно соответствовать имена hello в экспериментах hello. Полезные данные запроса образец hello можно просмотреть на странице справки выполнения пакета hello для hello ожидается сопоставлении tooverify конечная точка машинного Обучения Azure.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Только входные и выходные данные действия AzureMLBatchExecution hello могут передаваться как параметры toohello веб-службы. Например в hello выше фрагменте кода JSON DecisionTreeInputBlob является входной toohello AzureMLBatchExecution действия, которое передается в качестве входного toohello веб-службы через параметр webServiceInput.   
>
>

### <a name="example"></a>Пример
Этот пример использует хранилище Azure toohold оба hello входных и выходных данных.

Рекомендуется пройти hello [построение первой конвейер с фабрикой данных] [ adf-build-1st-pipeline] учебника перед переходом в этом примере. В этом примере, используйте артефактов фабрики данных Редактор фабрики данных toocreate hello (связанные службы, наборы данных, конвейера).   

1. Создайте **связанную службу** для **службы хранилища Azure**. Если hello входные и выходные файлы находятся в разных учетных записей хранения, то необходимо два связанных служб. Ниже приведен пример JSON:

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Создать hello **ввода** фабрики данных Azure **набора данных**. В отличие от некоторых других наборов данных фабрики данных, эти наборы должны содержать значения **folderPath** и **fileName**. Можно использовать секционирования toocause каждого tooprocess пакетного выполнения (каждый фрагмент данных) или создать уникальный входных данных и выходные файлы. Может потребоваться tooinclude некоторые hello tootransform восходящего действия введены в hello CSV-файл и поместить его в hello учетной записи хранилища для каждого среза. В этом случае не будет включена hello **внешних** и **externalData** параметры, отображаемые в hello следующий пример и вашей DecisionTreeInputBlob бы hello выходной набор данных из другого действия.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    Входные CSV-файл должен иметь hello строку заголовков столбцов. Если вы используете hello **действие копирования** toocreate или перемещения hello csv в хранилище больших двоичных объектов hello, необходимо задать значение свойства приемника hello **blobWriterAddHeader** слишком**true**. Например:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Если hello CSV-файле отсутствует строка заголовка hello, может появиться следующая ошибка hello: **ошибки в действии: ошибка при чтении строки. Непредвиденный токен: StartObject. Путь '', строка 1, позиция 1**.
3. Создать hello **вывода** фабрики данных Azure **набора данных**. В этом примере секционирования toocreate уникальный выходной путь для каждого выполнения среза. Без секционирования hello, действие hello перезапишет файл hello.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. Создание **связанная служба** типа: **AzureMLLinkedService**, предоставив ключ hello API и модели URL-адрес выполнения пакета.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. Наконец, создайте конвейер, содержащий действие **AzureMLBatchExecution** . Во время выполнения конвейера выполняет следующие шаги hello.

   1. Получает расположение hello hello входного файла из входных наборов данных.
   2. Вызывает выполнение пакета машинного обучения Azure hello API
   3. Копирует hello пакетного выполнения вывода toohello больших двоичных объектов в выходной набор данных.

      > [!NOTE]
      > У действия AzureMLBatchExecution может быть ноль или более входных наборов данных и один или несколько выходных наборов данных.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      Даты **начала** и **окончания** должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2014-10-14T16:32:41Z. Hello **окончания** времени является необязательным. Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов.**» конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство. Дополнительные сведения о свойствах JSON см. в [справочнике по скриптам JSON](https://msdn.microsoft.com/library/dn835050.aspx).

      > [!NOTE]
      > Входные данные для действия AzureMLBatchExecution hello указывать не обязательно.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Сценарий: Экспериментов с помощью toodata toorefer модулей чтения и записи в различных хранилищах
При создании экспериментах Azure ML другим распространенным сценарием является toouse модулей чтения и записи. модуль считывания Hello используется tooload данных в эксперимент она hello модуль записи данных toosave из эксперимента. Дополнительные сведения о модулях [чтения](https://msdn.microsoft.com/library/azure/dn905997.aspx) и [записи](https://msdn.microsoft.com/library/azure/dn905984.aspx) см. в соответствующих разделах в библиотеке MSDN.     

При использовании hello модулей чтения и записи, это хороший способ toouse параметр веб-службы для каждого свойства из этих модулей чтения и записи. Эти параметры web включить tooconfigure hello значения во время выполнения. Например, можно создать эксперимент с модулем чтения, который использует базу данных SQL Azure: XXX.database.windows.net. После развертывания веб-службу hello потребители hello tooenable hello web service toospecify требуется другой сервер SQL Azure, называется YYY.database.windows.net. Tooallow параметр Web service можно использовать этот toobe значение настройки.

> [!NOTE]
> Входные и выходные данные веб-службы отличаются от параметров веб-службы. В первом сценарии hello вы уже узнали, как входа и выхода можно указать для службы Azure ML Web. В этом сценарии передать параметры для веб-службы, которые соответствуют tooproperties модулей чтения и записи.
>
>

Рассмотрим сценарий использования параметров веб-службы. У вас есть развернутой веб-службы машинного обучения Azure, использующего модуль tooread модуль чтения данных из одного из источников данных hello поддерживается машинным обучением Azure (например: база данных SQL Azure). После выполнения пакетного hello hello записаны результаты с помощью модуля записи (база данных SQL Azure).  Нет web service входных и выходных данных определяются в экспериментах hello. В этом случае рекомендуется настраивать параметры соответствующих веб-службы для hello модулей чтения и записи. Эта конфигурация обеспечивает hello чтения и записи toobe модули настроены при помощи hello AzureMLBatchExecution действия. Укажите параметры веб-службы в hello **globalParameters** раздела действие hello JSON.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Можно также использовать [функции фабрики данных](data-factory-functions-variables.md) при передаче значения для hello параметры веб-службы, как показано в следующий пример hello:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Параметры веб-службы Hello чувствительны к регистру, поэтому убедитесь hello имена, указываемые в действии hello JSON соответствует hello из них, предоставляемые hello веб-службы.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>С помощью модуля tooread модуль чтения данных из нескольких файлов в BLOB-объектов Azure
Конвейеры больших данных с такими действиями, как Pig и Hive, могут формировать один или несколько выходных файлов без расширений. Например при указании внешнюю таблицу Hive hello данных для внешней таблицы Hive hello могут храниться в хранилище больших двоичных объектов с hello, следуя 000000_0 имя. Можно использовать модуль чтения hello в эксперименте tooread несколько файлов и использовать их для прогнозов.

При использовании модуля чтения hello в эксперимент машинного обучения Azure, можно указать в качестве ввода больших двоичных объектов Azure. файлы Hello в hello хранилище больших двоичных объектов может быть hello выходные файлы (пример: 000000_0), созданные с помощью сценарий Pig и Hive в HDInsight. Hello модуля чтения позволяет tooread файлы (с без расширения), настроив hello **toocontainer путь, каталог или большого двоичного объекта**. Hello **toocontainer путь** точки toohello контейнера и **каталога или большого двоичного объекта** указывает toofolder файлами hello, как показано в hello после изображения. Hello именно звездочка \*) **указывает, что все hello файлы в папку контейнера hello (то есть данных/aggregateddata/год = 2014-месяц-6 /\*)** считываются как часть эксперимента hello.

![Свойства большого двоичного объекта Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Пример
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Конвейер с действием AzureMLBatchExecution с параметрами веб-службы

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

В hello в приведенном выше примере JSON:

* Hello развернуты служба использует средство чтения и записи модуля tooread и записи данных из компьютер обучения Azure веб-tooan базы данных SQL Azure. Этот веб-служба предоставляет hello следующие четыре параметра: имя сервера, имя базы данных, имя учетной записи пользователя сервера и пароль учетной записи пользователя сервера базы данных.  
* Даты **начала** и **окончания** должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2014-10-14T16:32:41Z. Hello **окончания** времени является необязательным. Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов.**» конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство. Дополнительные сведения о свойствах JSON см. в [справочнике по скриптам JSON](https://msdn.microsoft.com/library/dn835050.aspx).

### <a name="other-scenarios"></a>Другие сценарии
#### <a name="web-service-requires-multiple-inputs"></a>Веб-службе требуется несколько входных данных
Если веб-служба hello принимает несколько входов, использовать hello **webServiceInputs** свойство вместо **webServiceInput**. Наборы данных, на которые ссылается hello **webServiceInputs** также должны быть включены в действие hello **входов**.

В эксперименте Машинного обучения Azure у входных и выходных портов и глобальных параметров есть имена по умолчанию (input1, input2), которые можно настроить. имя, используемое для webServiceInputs, webServiceOutputs и globalParameters параметры как Hello должен точно соответствовать имена hello в экспериментах hello. Полезные данные запроса образец hello можно просмотреть на странице справки выполнения пакета hello для hello ожидается сопоставлении tooverify конечная точка машинного Обучения Azure.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>Веб-служба не требует входных данных
Azure ML пакетного выполнения веб-службы может быть используется toorun все рабочие процессы, например R или сценариев Python, который не может потребоваться входные данные. Или эксперимента hello могут быть настроены с помощью модуля чтения, не предоставляет все GlobalParameters. В этом случае hello AzureMLBatchExecution действие будет настроена следующим образом:

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>Веб-служба не требует входных или выходных данных
Hello Azure ML пакетного выполнения веб-службы могут не иметь никаких выходных данных веб-службы настроены. В данном примере не настроены ни входные или выходные параметры, ни глобальные параметры. По-прежнему выхода, настроенного на само действие hello, но он не указан в качестве webServiceOutput.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Веб-служба использует чтения и записи и hello действие выполняется только в том случае, если другие действия успешно выполнены
Hello Azure ML веб-службы чтения и записи модули, может быть настроенный toorun независимо от любой GlobalParameters. Тем не менее вы можете tooembed службы вызовов в конвейера, который использует службу hello tooinvoke зависимости набора данных только в том случае, когда некоторые вышестоящего Обработка завершена. Вы можете запускать другие действия после завершения выполнения пакета hello этот подход. В этом случае можно выразить с помощью действия входов и выходов, без задания имени, такого как веб-службе входные и выходные данные зависимостей hello.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

Hello **общие выводы** являются:

* Если ваш конечная эксперимента использует webServiceInput: он представлен набор данных BLOB-объектов и входит в состав входные данные действия hello и свойство webServiceInput hello. В противном случае свойство webServiceInput hello опускается.
* Если ваш конечная эксперимента использует webServiceOutput(s): они представляются в наборах данных больших двоичных объектов и включены в выходных данных действия hello и в свойстве webServiceOutputs hello. Выводит действие Hello и webServiceOutputs, сопоставляются по имени hello каждого выхода в эксперименте hello. В противном случае свойство webServiceOutputs hello опускается.
* Если конечная точка эксперимента предоставляет globalParameter(s), они задаются в свойстве globalParameters действие hello в виде пар ключ/значение. В противном случае свойство globalParameters hello опускается. ключи Hello чувствительны к регистру. [Функции фабрики данных Azure](data-factory-functions-variables.md) могут использоваться в значениях hello.
* Дополнительные наборы данных могут быть включены в свойства входов и выходов действия hello, без, на которую ссылается действие typeProperties hello. Эти наборы данных определяют выполнение с помощью зависимости среза, но пропускаются hello AzureMLBatchExecution действия.


## <a name="updating-models-using-update-resource-activity"></a>Обновление моделей с помощью действия обновления ресурса
После завершения переподготовки, обновите hello оценки веб-службы (прогнозной эксперимент, предоставляемых как веб-службы) с hello вновь обученной модели с помощью hello **действия ресурса обновления машинного Обучения Azure**. Дополнительные сведения см. в статье [Updating Azure Machine Learning models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс").

### <a name="reader-and-writer-modules"></a>Модули чтения и записи
Распространенный сценарий использования параметры веб-службы является использование hello Azure SQL чтения и записи. модуль считывания Hello — используется tooload данных в эксперимент из служб управления данными вне студии машинного обучения Azure. модуль записи Hello — toosave данные из экспериментов в службах управления данными вне студии машинного обучения Azure.  

Сведения о модулях [чтения](https://msdn.microsoft.com/library/azure/dn905997.aspx) и [записи](https://msdn.microsoft.com/library/azure/dn905984.aspx) больших двоичных объектов Azure и SQL Azure см. в соответствующих разделах в библиотеке MSDN. пример Hello в предыдущем разделе hello использовать hello больших двоичных объектов Azure чтения и записи больших двоичных объектов Azure. В этом разделе рассматривается использование модуля чтения и модуля записи SQL Azure.

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы
**Вопрос.** Имеется несколько файлов, сформированных моими конвейерами больших данных. Можно использовать toowork hello AzureMLBatchExecution действия для всех файлов hello

**Ответ.** Да. В разделе hello **с помощью модуля tooread модуль чтения данных из нескольких файлов в большом двоичном объекте Azure** подробные сведения см.

## <a name="azure-ml-batch-scoring-activity"></a>Действие количественной оценки Azure ML
Если вы используете hello **AzureMLBatchScoring** toointegrate действия с машинного обучения Azure, рекомендуется использовать последнюю hello **AzureMLBatchExecution** действия.

Hello действия AzureMLBatchExecution впервые появился в hello августа 2015 г. выпуск пакета SDK для Azure и Azure PowerShell.

Если требуется использование действия AzureMLBatchScoring hello toocontinue продолжайте чтение в этом разделе.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Действие количественной оценки Azure ML с использованием хранилища Azure в качестве входных и (или) выходных данных

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Параметры веб-службы
Добавьте значения toospecify параметры веб-службы **typeProperties** toohello раздел **AzureMLBatchScoringActivty** раздела hello конвейера JSON, как показано в следующий пример hello:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Можно также использовать [функции фабрики данных](data-factory-functions-variables.md) при передаче значения для hello параметры веб-службы, как показано в следующий пример hello:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Параметры веб-службы Hello чувствительны к регистру, поэтому убедитесь hello имена, указываемые в действии hello JSON соответствует hello из них, предоставляемые hello веб-службы.
>
>

## <a name="see-also"></a>См. также
* [Запись блога Azure: «Приступая к работе с фабрикой данных Azure и Машинным обучением Azure»](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
