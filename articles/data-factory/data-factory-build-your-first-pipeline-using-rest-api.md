---
title: "aaaBuild первый фабрики данных (REST) | Документы Microsoft"
description: "В этом руководстве вы создадите образец конвейера фабрики данных Azure с помощью REST API фабрики данных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Руководство. Создание первой фабрики данных Azure с помощью REST API фабрики данных
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-build-your-first-pipeline.md)
> * [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


В этой статье используется API-Интерфейс REST фабрики данных toocreate первый фабрики данных Azure. toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.

конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**. Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных. Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello.

> [!NOTE]
> Данная статья не охватывает все hello REST API. Полную документацию по командлетам фабрики данных см. в [справочнике по REST API фабрики данных](/rest/api/datafactory/).
> 
> Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Предварительные требования
* Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.
* Установите на компьютер программу [curl](https://curl.haxx.se/dlwiz/) . Используйте средство ПЕРЕЛИСТЫВАНИЕ hello с toocreate команды REST фабрики данных.
* Следуя инструкциям в [этой статье](../azure-resource-manager/resource-group-create-service-principal-portal.md) , выполните следующее:
  1. Создайте веб-приложение с именем **ADFGetStartedApp** в Azure Active Directory.
  2. Получите **идентификатор клиента** и **секретный ключ**.
  3. Получите значение для **tenant_id**.
  4. Назначить hello **ADFGetStartedApp** toohello приложения **участника фабрики данных** роли.
* Установите [Azure PowerShell](/powershell/azure/overview).
* Запустите **PowerShell** и выполнения hello следующую команду. Не закрывайте Azure PowerShell до завершения этого учебника hello. Если закрыть и снова открыть понадобятся toorun hello команд.
  1. Запустите **AzureRmAccount входа** и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.
  2. Запустите **Get AzureRmSubscription** tooview все hello подписок для этой учетной записи.
  3. Запустите **NameOfAzureSubscription Get AzureRmSubscription - SubscriptionName | Набор AzureRmContext** tooselect hello подписки на toowork с. Замените **NameOfAzureSubscription** с именем hello подписки Azure.
* Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Некоторые шаги hello в этом учебнике предполагается использовать ADFTutorialResourceGroup с именем группы ресурсов hello. Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.

## <a name="create-json-definitions"></a>Создание определений JSON
Создайте следующие файлы JSON в папке hello, где находится curl.exe.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Имя должно быть глобально уникальным, поэтому можно toomake ADFCopyTutorialDF tooprefix или суффикса его уникальное имя.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Замените значения **accountname** и **accountkey** на имя вашей учетной записи хранения Azure и ее ключ. toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.

| Свойство | Описание |
|:--- |:--- |
| ClusterSize (размер кластера) |Размер кластера HDInsight hello. |
| TimeToLive (срок жизни) |Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением. |
| linkedServiceName (имя связанной службы) |Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные HDInsight |

Обратите внимание hello после точки.

* Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello выше JSON. Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
* Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**. См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
* Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз при обработке среза, если нет существующего кластера динамическая (**timeToLive**) и удаляется при завершении обработки hello.

    По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp». Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.

Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
| columnDelimiter |столбцы в файлах журнала hello разделяются запятой () |
| frequency и interval |tooMonth задать частоту и интервал равен 1, это означает, что входные срезы hello доступны ежемесячно. |
| external |Это свойство имеет значение tootrue, если входные данные hello не создается службой фабрики данных hello. |

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Замените свойство **storageaccountname** именем вашей учетной записи хранения Azure.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

Фрагмент кода hello JSON вы создаете конвейера, который состоит из одного действия, которое использует данные tooprocess Hive в кластере HDInsight.

файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **StorageLinkedService**) и в **сценария**  папки в контейнере hello **adfgetstarted**.

Hello **определяет** раздел определяет параметры среды выполнения, которые передаются как значения конфигурации Hive скрипт hive toohello (например ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.

В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.

> [!NOTE]
> В разделе «Конвейера JSON» в [конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md) подробные сведения о JSON свойства, используемые в предшествующих пример hello.
>
>

## <a name="set-global-variables"></a>Настройка глобальных переменных
Выполните следующие команды после замены значения hello собственные hello в Azure PowerShell.

> [!IMPORTANT]
> Инструкции по получению значений для параметров client_id, client_secret, tenant и subscription_id см. в разделе [Предварительные требования](#prerequisites).
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Проверка подлинности с помощью AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Создание фабрики данных
На этом шаге вы создадите фабрику данных Azure с именем **FirstDataFactoryREST**. Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Например действие копирования toocopy данные из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight данных tootransform скрипт Hive. Выполните следующие hello данных команды toocreate фабрики hello.

1. Назначить hello команды toovariable с именем **cmd**.

    Убедитесь, что hello имя фабрики данных hello, указанные здесь имя, указанное в hello hello совпадений (ADFCopyTutorialDF) **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если hello фабрика данных успешно создана, вы видите hello JSON для фабрики данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell
    Write-Host $results
    ```

Обратите внимание hello после точки.

* Имя Hello hello фабрики данных Azure должно быть глобально уникальным. При возникновении ошибки hello в результатах: **имя фабрики данных «FirstDataFactoryREST» недоступен**, hello следующие действия:
  1. Изменение имени hello (например, yournameFirstDataFactoryREST) в hello **datafactory.json** файла. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.
  2. В первой команде hello Здравствуйте, где **$cmd** переменной присваивается значение, замените FirstDataFactoryREST hello новое имя и выполните команду hello.
  3. Запуск hello следующие две команды tooinvoke hello API-интерфейса REST toocreate hello данных фабрики и печати hello результатов операции hello.
* экземпляры toocreate фабрики данных, необходимо toobe участника или администратор hello подписки Azure
* Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и поэтому становятся публично видимых.
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

Перед созданием конвейера, необходимо toocreate несколько сущностей фабрики данных сначала. Необходимо сначала создать связанные службы данных toolink хранилищ и вычисляет tooyour хранилище, определение входных данных и выводить данные toorepresent наборов данных в хранилищах данных связанного.

## <a name="create-linked-services"></a>Создание связанных служб
На этом шаге связать учетную запись хранилища Azure и фабрикой данных кластера tooyour для Azure HDInsight по требованию. содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце. Hello связанной службы HDInsight — используется toorun скрипт Hive, указанное в действии hello конвейера hello в этом образце.

### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure
На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure. С помощью данного учебника используйте hello Azure учетную запись хранения toostore ввода вывода данных и hello HQL файл скрипта.

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Создание связанной службы Azure HDInsight
На этом шаге связать фабрикой данных кластера tooyour для HDInsight по требованию. кластер HDInsight Hello автоматически создается во время выполнения и удалена после завершения обработки и время простоя для hello указанного интервала времени. Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight. Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Создание наборов данных
На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive. Эти наборы данных ссылаются toohello **StorageLinkedService** вы создали ранее в этом учебнике. Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.

### <a name="create-input-dataset"></a>Создание входного набора данных
На этом шаге создается hello входного набора данных toorepresent входных данных в хранилище больших двоичных объектов Azure hello.

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Создание выходного набора данных
На этом шаге создается hello выходной набор данных toorepresent выходные данные хранятся в hello хранилища больших двоичных объектов Azure.

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>Создание конвейера
На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** . Входной фрагмент доступен ежемесячно (частота: месяц, интервал: 1), выходные данные срезов ежемесячно и toomonthly также установлено свойство планировщика hello для действия "hello". Параметры Hello для hello выходной набор данных и планировщик действие hello должны совпадать. В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.

Подтвердите, что вы видите hello **input.log** файла в hello **adfgetstarted/inputdata** папку, в хранилище больших двоичных объектов hello и выполнения hello, следующая команда toodeploy hello конвейера. С момента hello **запустить** и **окончания** время установлено в прошлом hello и **isPaused** работает toofalse набор, конвейер hello (действие в конвейере hello) сразу же после развертывания.

1. Назначить hello команды toovariable с именем **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Команда hello с помощью **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Просмотр результатов hello. Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.

    ```PowerShell
    Write-Host $results
    ```
4. Поздравляем! Вы создали свой первый конвейер с помощью Azure PowerShell!

## <a name="monitor-pipeline"></a>Отслеживание конвейера
На этом шаге используется фрагменты toomonitor REST API фабрики данных, получаемых hello конвейера.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут). Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.
>
>

Запустить hello Invoke-Command и hello следующему пока не увидите срез hello в **готовности** состояние или **сбой** состояния. Когда hello среза находится в состоянии готовности, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.  Создание кластера HDInsight по требованию Hello обычно занимает некоторое время.

![выходные данные](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> входной файл Hello, удаляется при успешно обработал hello среза. Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.
>
>

Можно также использовать Azure портала toomonitor фрагментов и устранение неполадок. Дополнительные сведения см. в разделе [Отслеживание конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).

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
| [Справочник по REST API фабрики данных](/rest/api/datafactory/) |См. полную документацию по командлетам фабрики данных. |
| [Конвейеры](data-factory-create-pipelines.md) |Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса. |
| [Наборы данных](data-factory-create-datasets.md) |Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure. |
| [Планирование и выполнение](data-factory-scheduling-and-execution.md) |В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure. |
| [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md) |В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления. |
