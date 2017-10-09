---
title: "aaaBuild первый фабрики данных (PowerShell) | Документы Microsoft"
description: "В этом руководстве вы создадите образец конвейера фабрики данных Azure с помощью Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Руководство. Создание первой фабрики данных Azure с помощью Azure PowerShell
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-build-your-first-pipeline.md)
> * [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

В этой статье используется Azure PowerShell toocreate первый фабрики данных Azure. toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.

конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**. Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных. Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello. 

> [!NOTE]
> конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных. Копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Предварительные требования
* Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.
* Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи tooinstall последнюю версию Azure PowerShell на компьютере.
* (необязательно) Данная статья не охватывает все командлеты фабрики данных hello. Полную документацию по командлетам фабрики данных см. в [этом справочнике](/powershell/module/azurerm.datafactories).

## <a name="create-data-factory"></a>Создание фабрики данных
На этом шаге используется Azure PowerShell toocreate фабрикой данных Azure с именем **FirstDataFactoryPSH**. Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входные данные. Давайте начнем с создания фабрики данных hello на этом шаге.

1. Запустите Azure PowerShell и выполните следующую команду hello. Не закрывайте Azure PowerShell до завершения этого учебника hello. Если закрыть и снова открыть понадобятся toorun этих команд.
   * Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Запустите следующие команды tooview hello все hello подписки для этой учетной записи.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Следующая команда tooselect hello подписки на toowork с выполнения hello. Эта подписка должна hello равна hello, который используется в hello портал Azure.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду hello:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Некоторые шаги hello в этом учебнике предполагается использовать ADFTutorialResourceGroup с именем группы ресурсов hello. Если вы используете другой группе ресурсов, необходимо toouse его вместо ADFTutorialResourceGroup в этом учебнике.
3. Запустите hello **New AzureRmDataFactory** командлет, который создает фабрики данных с именем **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Обратите внимание hello после точки.

* Имя Hello hello фабрики данных Azure должно быть глобально уникальным. Если ошибка hello **имя фабрики данных «FirstDataFactoryPSH» недоступен**, измените имя hello (например, yournameFirstDataFactoryPSH). Используйте это имя вместо ADFTutorialFactoryPSH при выполнении шагов в этом руководстве. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.
* экземпляры toocreate фабрики данных, необходимо toobe участника или администратор hello подписки Azure
* Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.
* Если ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**», выполните одно из следующих hello и повторите попытку публикации:

  * В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика.

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure. Это действие автоматически регистрирует поставщик hello.

Перед созданием конвейера, необходимо toocreate несколько сущностей фабрики данных сначала. Необходимо сначала создать связанные службы данных toolink хранилищ и вычисляет tooyour данных хранения, определение входных данных и выходных данных ввода вывода toorepresent наборов данных в хранилищах данных связанного и затем создать конвейер hello с действие, которое использует эти наборы данных.

## <a name="create-linked-services"></a>Создание связанных служб
На этом шаге связать учетную запись хранилища Azure и фабрикой данных кластера tooyour для Azure HDInsight по требованию. содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце. Hello связанной службы HDInsight — используется toorun скрипт Hive, указанное в действии hello конвейера hello в этом образце. Определите, какие данные хранилища и вычислений служб используются в сценарий и связать эти фабрики служб toohello данных путем создания связанных служб.

### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure. Использовать hello Azure учетную запись хранения toostore ввода вывода данных и hello HQL файл скрипта.

1. Создайте JSON-файл с именем StorageLinkedService.json в папке C:\ADFGetStarted hello и hello после содержимого. Создайте папку hello ADFGetStarted, если он еще не существует.

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    Замените **имя учетной записи** с именем hello вашей учетной записи хранилища Azure и **ключ учетной записи** с ключом доступа hello hello учетной записи хранилища Azure. toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. В Azure PowerShell переключение toohello ADFGetStarted папки.
3. Можно использовать hello **New AzureRmDataFactoryLinkedService** командлете, создающем связанной службы. Этот командлет, а другие командлеты фабрики данных, используемый в этом учебнике требуется toopass значения для hello *ResourceGroupName* и *с именем DataFactoryName* параметров. Кроме того, можно использовать **Get AzureRmDataFactory** tooget **DataFactory** и передать hello объекта, не вводя *ResourceGroupName* и  *С именем DataFactoryName* при каждом выполнении командлета. Выполнения hello следующая команда tooassign hello выходные данные hello **Get AzureRmDataFactory** tooa командлет **$df** переменной.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Теперь запустите hello **New AzureRmDataFactoryLinkedService** командлете, создающем hello связаны **StorageLinkedService** службы.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Если еще не запущены hello **Get AzureRmDataFactory** командлета и назначенный hello выход toohello **$df** переменных, будет иметь значения toospecify для hello *ResourceGroupName*и *с именем DataFactoryName* параметры следующим образом.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Если вы закроете Azure PowerShell в середине hello учебника hello, у вас есть toorun hello **Get AzureRmDataFactory** командлета при следующей загрузке учебника hello toocomplete Azure PowerShell.

### <a name="create-azure-hdinsight-linked-service"></a>Создание связанной службы Azure HDInsight
На этом шаге связать фабрикой данных кластера tooyour для HDInsight по требованию. кластер HDInsight Hello автоматически создается во время выполнения и удалена после завершения обработки и время простоя для hello указанного интервала времени. Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight. Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).

1. Создайте JSON-файл с именем **HDInsightOnDemandLinkedService**.json в hello **C:\ADFGetStarted** папка с hello после содержимого.

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

   | Свойство | Описание |
   |:--- |:--- |
   | ClusterSize (размер кластера) |Указывает размер кластера HDInsight hello hello. |
   | TimeToLive (срок жизни) |Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением. |
   | linkedServiceName (имя связанной службы) |Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные HDInsight |

    Обратите внимание hello после точки.

   * Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello JSON. Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
   * Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**. См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
   * Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер**timeToLive**). Hello кластера автоматически удаляется при завершении обработки hello.

       По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp». Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.

     Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
2. Запустите hello **New AzureRmDataFactoryLinkedService** командлете, создающем hello связанной службы с именем HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Создание наборов данных
На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive. Эти наборы данных ссылаются toohello **StorageLinkedService** вы создали ранее в этом учебнике. Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.

### <a name="create-input-dataset"></a>Создание входного набора данных
1. Создайте JSON-файл с именем **InputTable.json** в hello **C:\ADFGetStarted** папка с hello после содержимого:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Hello JSON определяет набор данных с именем **AzureBlobInput**, который представляет входные данные для действия в конвейере hello. Кроме того, он указывает, hello входных данных находится в контейнере hello BLOB-объекта с именем **adfgetstarted** и hello папку с именем **inputdata**.

    Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

   | Свойство | Описание |
   |:--- |:--- |
   | type |Hello свойство type имеет значение tooAzureBlob, так как данные находятся в хранилище больших двоичных объектов. |
   | linkedServiceName (имя связанной службы) |ссылается toohello StorageLinkedService, созданного ранее. |
   | fileName |Это необязательное свойство. Если это свойство не указан, извлекаются все файлы hello из hello folderPath. В этом случае обрабатывается только input.log hello. |
   | type |файлы журнала Hello находятся в текстовом формате, поэтому мы используем TextFormat. |
   | columnDelimiter |столбцы в файлах журнала hello разделяются hello запятая (,). |
   | frequency и interval |tooMonth задать частоту и интервал равен 1, это означает, что входные срезы hello доступны ежемесячно. |
   | external |Это свойство имеет значение tootrue, если входные данные hello не создается службой фабрики данных hello. |
2. Выполните следующую команду в hello фабрики данных Azure PowerShell toocreate dataset hello.

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Создание выходного набора данных
Теперь создание выходных данных hello выходной набор данных toorepresent hello данные, хранящиеся в hello хранилища больших двоичных объектов Azure.

1. Создайте JSON-файл с именем **OutputTable.json** в hello **C:\ADFGetStarted** папка с hello после содержимого:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Hello JSON определяет набор данных с именем **AzureBlobOutput**, который представляет выходные данные для действия в конвейере hello. Кроме того, он указывает, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfgetstarted** и hello папку с именем **partitioneddata**. Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе.
2. Выполните следующую команду в hello фабрики данных Azure PowerShell toocreate dataset hello.

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Создание конвейера
На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** . Входной фрагмент доступен ежемесячно (частота: месяц, интервал: 1), выходные данные срезов ежемесячно и toomonthly также установлено свойство планировщика hello для действия "hello". Параметры Hello для hello выходной набор данных и планировщик действие hello должны совпадать. В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных. в конце hello в этом разделе объясняются Hello свойств, используемых в hello следующий JSON.

1. Создайте JSON-файл с именем MyFirstPipelinePSH.json в папке C:\ADFGetStarted hello и hello после содержимого:

   > [!IMPORTANT]
   > Замените **storageaccountname** с именем hello вашей учетной записи хранилища в hello JSON.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    Фрагмент кода hello JSON вы создаете конвейера, который состоит из одного действия, которое использует куст tooprocess данных в кластере HDInsight.

    файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **StorageLinkedService**) и в **сценария**  папки в контейнере hello **adfgetstarted**.

    Hello **определяет** раздел представляет параметры среды выполнения используется toospecify hello, быть передана toohello скрипт hive в качестве значения конфигурации Hive (например ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

    Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.

    В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > В разделе «Конвейера JSON» в [конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md) подробные сведения о свойствах JSON, которые используются в примере hello.

2. Подтвердите, что вы видите hello **input.log** файла в hello **adfgetstarted/inputdata** папку, в хранилище больших двоичных объектов hello и выполнения hello, следующая команда toodeploy hello конвейера. С момента hello **запустить** и **окончания** время установлено в прошлом hello и **isPaused** работает toofalse набор, конвейер hello (действие в конвейере hello) сразу же после развертывания.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. Поздравляем! Вы создали свой первый конвейер с помощью Azure PowerShell!

## <a name="monitor-pipeline"></a>Отслеживание конвейера
На этом шаге используется Azure PowerShell toomonitor происходящем в фабрикой данных Azure.

1. Запустите **Get AzureRmDataFactory** и назначить hello вывода tooa **$df** переменной.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Запустите **Get AzureRmDataFactorySlice** tooget сведения о всех фрагментов hello **EmpSQLTable**, являющееся hello выходная таблица hello конвейера.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Обратите внимание, что этой hello StartDateTime здесь же указано время начала в формат JSON конвейера hello hello. Вот пример выходных данных hello.

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Запустите **Get AzureRmDataFactoryRun** сведения hello tooget действия выполняется для определенного среза.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Вот пример выходных данных hello. 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    Вы можно продолжать работать этот командлет, пока не увидите срез hello в **готовности** состояние или **сбой** состояния. Когда hello среза находится в состоянии готовности, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.  Создание кластера HDInsight по требованию занимает некоторое время.

    ![выходные данные](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут). Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.
>
> входной файл Hello, удаляется при успешно обработал hello среза. Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.
>
>

## <a name="summary"></a>Сводка
В этом учебнике вы создали данных tooprocess фабрики данных Azure, выполнив скрипт Hive в кластере HDInsight hadoop. Вы использовали hello редактор фабрики данных в Azure портала toodo hello hello, следующие шаги:

1. Создание **фабрики данных Azure**.
2. создание двух **связанных служб**.
   1. **Хранилище Azure** связанные toolink службы хранилища больших двоичных объектов Azure, содержащий фабрики данных toohello ввода вывода файлов.
   2. **Azure HDInsight** связанная служба toolink по требованию фабрикой по требованию toohello кластера HDInsight Hadoop данных. Фабрика данных Azure создает HDInsight Hadoop кластера tooprocess just-in-time входных данных и создают выходных данных.
3. Создать два **наборы данных**, которые описывают входных и выходных данных для действие Hive в HDInsight из конвейера hello.
4. Создание **конвейера** с действием **HDInsight Hive**.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье описывается создание конвейера с помощью действия преобразования (действие HDInsight), которое по требованию выполняет сценарий Hive в кластере Azure HDInsight. toosee toouse toocopy действие копирования данных из больших двоичных объектов Azure tooAzure SQL, в статье [учебника: копирование данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>См. также
| Раздел | Описание |
|:--- |:--- |
| [Справочник по командлетам фабрики данных](/powershell/module/azurerm.datafactories) |См. полную документацию по командлетам фабрики данных. |
| [Конвейеры](data-factory-create-pipelines.md) |Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса. |
| [Наборы данных](data-factory-create-datasets.md) |Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure. |
| [Планирование и выполнение](data-factory-scheduling-and-execution.md) |В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure. |
| [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md) |В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления. |
