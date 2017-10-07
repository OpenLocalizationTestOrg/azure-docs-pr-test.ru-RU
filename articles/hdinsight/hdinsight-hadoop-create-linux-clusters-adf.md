---
title: "по запросу Hadoop кластеры, использующие фабрика данных — Azure HDInsight aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate Hadoop по требованию кластеров в HDInsight с помощью фабрики данных Azure."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Создание кластеров Hadoop в HDInsight по запросу с помощью фабрики данных Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Фабрика данных Azure](../data-factory/data-factory-introduction.md) — служба интеграции данных на основе облака, которая координирует и автоматизирует процессы hello перемещения и преобразования данных. Его можно создать tooprocess just-in-time кластера HDInsight Hadoop срез входных данных и удалить hello кластера после завершения обработки hello. Ниже приведены некоторые преимущества hello кластера Hadoop в HDInsight по требованию.

- Вы только оплаты для задания времени hello выполняется на hello кластера HDInsight Hadoop (а также краткое настраиваемое время простоя). Hello выставления счетов для кластеров HDInsight пропорциональной в минуту, ли вы используете их, или нет. При использовании по требованию связанной службы HDInsight в фабрике данных кластеров hello создаются по запросу. И кластеры hello автоматически удаляются по завершении задания hello. Таким образом вы платите только за hello задание, выполняющееся hello краткое время простоя (значение срока жизни) и времени.
- С помощью конвейера фабрики данных можно создать рабочий процесс. Например может иметь hello конвейера toocopy данные из локального SQL Server tooan хранилище больших двоичных объектов, обработка данных hello, запустив скрипт Hive и сценарий Pig в кластере HDInsight Hadoop по требованию. Затем скопируйте результат hello данных tooan хранилище данных SQL Azure для tooconsume приложений бизнес-Аналитики.
- Можно запланировать hello рабочего процесса toorun периодически (каждый час, день, неделю, месяц, и т. д.).

В фабрике данных Azure фабрика данных может содержать один или несколько конвейеров. Конвейер данных включает одно или несколько действий. Существует два типа действий: [действия перемещения данных](../data-factory/data-factory-data-movement-activities.md) и [действия преобразования данных](../data-factory/data-factory-data-transformation-activities.md). Используйте toomove действия (в настоящее время только действие копирования) перемещения данных из источника данных хранилища tooa целевое хранилище данных. Используются данные tootransform или процесс действия преобразования данных. Действие Hive в HDInsight является одним из действий hello преобразования, поддерживаемые фабрикой данных. В этом учебнике используется действие преобразования Hive hello.

Можно настроить toouse действие hive кластера HDInsight Hadoop или кластер Hadoop в HDInsight по требованию. В этом учебнике hello действие Hive в конвейере фабрики данных hello является настроенным toouse кластер HDInsight по требованию. Таким образом когда запускается действие hello tooprocess срез данных, происходит следующее:

1. Кластер HDInsight Hadoop автоматически создается для вас tooprocess just-in-time hello среза.  
2. Hello входные данные обрабатываются, выполнив сценарий HiveQL в кластере hello.
3. кластер HDInsight Hadoop Hello удаляется после завершения обработки hello и hello кластера используется в течение hello настроить количество времени (параметр timeToLive). Если для обработки с в это время простоя timeToLive hello следующий срез данных, hello одного кластера — используется tooprocess hello срез.  

В этом учебнике hello сценарий HiveQL, связанный с действием hive hello выполняет hello, следующие действия:

1. Создает внешнюю таблицу, которая ссылки hello необработанные веб-данных журнала, хранящиеся в службе хранилища больших двоичных объектов Azure.
2. Секции hello необработанные данные за год и месяц.
3. Сохраняет hello секционированными данными в хранилище больших двоичных объектов hello.

В этом учебнике hello сценарий HiveQL, связанный с действием hive hello создает внешнюю таблицу, которая ссылки hello необработанные web журнала данных, хранящихся в hello хранилища больших двоичных объектов. Вот hello образцов строк для каждого месяца во входном файле hello.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

секции сценарий HiveQL Hello hello необработанные данные за год и месяц. Он создает три папки выходных данных, на основе предыдущих ввода hello. Каждая папка содержит файл с записями по каждому месяцу.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Список действий преобразования данных фабрики данных в операции сложения tooHive см [преобразования и анализа с помощью фабрики данных Azure](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Сейчас в фабрике данных Azure можно создать только кластер HDInsight версии 3.2.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать hello инструкции в этой статье, необходимо иметь hello следующих элементов:

* [Подписка Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Подготовка учетной записи хранения
Воспользуйтесь toothree учетных записей хранения в этом сценарии.

- Учетная запись хранения по умолчанию для кластера HDInsight hello
- Учетная запись хранения для hello входных данных
- Учетная запись хранения для hello выходных данных

Учебник toosimplify hello, использовать одну учетную запись tooserve hello трех целей хранения. Пример сценария Hello Azure PowerShell, представленные в этом разделе выполняет следующие задачи hello.

1. Войдите в tooAzure.
2. Создание группы ресурсов Azure.
3. Создание учетной записи хранения Azure.
4. Создать контейнер больших двоичных объектов в учетной записи хранения hello
5. Скопируйте следующие два контейнера больших двоичных объектов toohello файлы hello:

   * Файл входных данных: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * Сценарий HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Оба файла хранятся в общедоступном контейнере больших двоичных объектов.


**tooprepare hello хранилища и скопируйте hello файлы с помощью Azure PowerShell:**
> [!IMPORTANT]
> Укажите имена для группы ресурсов Azure hello и hello учетной записи хранилища Azure, будет создан скрипт hello.
> Запишите **имя группы ресурсов**, **имя учетной записи хранения**, и **ключ учетной записи хранения** выдаваемые hello скрипта. Они необходимы в следующем разделе hello.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Если вам нужна помощь с помощью скрипта PowerShell hello, см. раздел [hello использование Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md). Если вы хотите toouse Azure CLI вместо этого разделе hello [приложение](#appendix) раздел для hello сценария Azure CLI.

**tooexamine hello хранилища учетной записи и hello содержимое**

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **групп ресурсов** на левой панели hello.
3. Дважды щелкните имя группы ресурсов hello, созданный в скриптах PowerShell. Используйте фильтр hello, при наличии слишком много групп ресурсов в списке.
4. На hello **ресурсов** плитки, должен иметь один ресурс, если группа ресурсов hello предоставить другие проекты в списке. Этот ресурс является hello учетной записи хранилища с именем hello, указанного ранее. Щелкните имя учетной записи хранения hello.
5. Нажмите кнопку hello **большие двоичные объекты** плитки.
6. Нажмите кнопку hello **adfgetstarted** контейнера. Вы увидите две папки: **inputdata** и **script**.
7. Откройте папку hello и проверьте hello файлы в папках hello. Hello inputdata файлом hello input.log с входными данными и hello скрипт папка содержит файл скрипта HiveQL hello.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Создание фабрики данных с помощью шаблона Resource Manager
Hello учетной записи хранилища, hello входных данных и hello подготовить сценарий HiveQL будут готовы toocreate фабрикой данных Azure. Существует несколько способов создания фабрики данных. В этом учебнике создать фабрику данных путем развертывания шаблона Azure Resource Manager с помощью портала Azure hello. Вы также можете развернуть шаблон Resource Manager с помощью [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) или [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Описание других способов создания фабрики данных вы найдете в [руководстве по созданию фабрики данных](../data-factory/data-factory-build-your-first-pipeline.md).

1. Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure. Hello шаблона находится в https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. В разделе hello [фабрики данных сущности в шаблоне hello](#data-factory-entities-in-the-template) подробные сведения о сущности, определенные в шаблоне hello. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Выберите **использовать существующие** параметр для hello **группы ресурсов** параметр и выберите hello имя группы ресурсов hello, созданный на предыдущем шаге hello (с помощью сценария PowerShell).
3. Введите имя фабрики данных hello (**имя фабрики данных**). Оно должно быть глобально уникальным.
4. Введите hello **имя учетной записи хранения** и **ключ учетной записи хранения** записанные на предыдущем шаге hello.
5. Выберите **я принимаю условия toohello** говорилось выше, после тщательного изучения **условий**.
6. Выберите **toodashboard ПИН-код** параметр.
6. Щелкните **Purchase/Create** (Купить или Создать). Вы видите плитку на панель мониторинга называется hello **развертывание шаблона-развертывания**. Подождите, пока hello **группы ресурсов** открывает колонку для группы ресурсов. Можно также щелкнуть плитку hello под названием как вашей группы имя tooopen hello ресурсов группы колонки ресурсов.
6. Щелкните группу ресурсов hello tooopen плитки приветствия, если колонки группы ресурсов hello еще не открыт. Теперь будет отображаться один дополнительные ресурсы фабрики данных, кроме перечисленных toohello ресурс учетной записи хранения.
7. Щелкните имя hello фабрики данных (значение, указанное для hello **имя фабрики данных** параметр).
8. В колонке hello фабрики данных, нажмите кнопку hello **схема** плитки. Hello схеме показано одно действие с входного набора данных и выходной набор данных.

    ![Фабрика данных Azure: схема конвейера действий Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    имена Hello определены в шаблоне hello диспетчера ресурсов.
9. Дважды щелкните **AzureBlobOutput**.
10. На hello **последние обновления фрагменты**, вы увидите один срез. Если состояние hello **выполняется**, подождите, пока он изменяется слишком**готовности**. Обычно это занимает около **20 минут** toocreate кластера HDInsight.

### <a name="check-hello-data-factory-output"></a>Проверьте выходные данные для фабрики данных hello

1. Используйте hello же процедуру, описанную в hello последнего сеанса toocheck hello контейнеров hello adfgetstarted контейнера. Существует два новых контейнеров в дополнение к этому слишком**adfgetsarted**:

   * Контейнер с именем, hello шаблону: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Этот контейнер — контейнер по умолчанию hello для кластера HDInsight hello.
   * adfjobs: этот контейнер — контейнер hello для hello ADF. журналы заданий.

     Вывод фабрики Hello данных хранится в **afgetstarted** , которые были настроены в шаблоне hello диспетчера ресурсов.
2. Щелкните **adfgetstarted**.
3. Дважды щелкните **partitioneddata**. Вы видите **год = 2014** папку, так как все веб-журналы hello датированные 2014 года.

    ![Фабрика данных Azure: выходные данные конвейера действия Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Если детализация углублением список hello, будет отображаться три папки за январь, февраль и март. Для каждого месяца существует журнал.

    ![Фабрика данных Azure: выходные данные конвейера действия Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Фабрика сущностями данных в шаблоне hello
Вот, как выглядит hello верхнего уровня шаблона диспетчера ресурсов для фабрики данных.

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Определение фабрики данных
Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
с именем dataFactoryName Hello — имя hello hello фабрики данных, которые указываются при развертывании шаблона hello. Фабрика данных — в настоящее время поддерживается только в регионах hello Восток США, Запад США и Северной Европе.

### <a name="defining-entities-within-hello-data-factory"></a>Определение сущности в рамках фабрики данных hello
Hello следующие сущности фабрики данных определены в шаблоне hello JSON:

* [Связанная служба хранения Azure](#azure-storage-linked-service)
* [Связанная служба кластера HDInsight по запросу](#hdinsight-on-demand-linked-service)
* [Входной набор данных большого двоичного объекта Azure](#azure-blob-input-dataset)
* [Выходной набор данных большого двоичного объекта Azure](#azure-blob-output-dataset)
* [Конвейер данных с действием копирования](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure
Hello хранилища Azure связанные ссылки на службу фабрики данных toohello учетной записи хранилища Azure. В этом учебнике hello учетную запись хранения используется как учетная запись хранения HDInsight по умолчанию hello, входные данные и хранилищем вывода данных. Таким образом, вы определяете только одну связанную службу хранилища Azure. В определении службы hello связаны укажите имя hello и ключ учетной записи хранилища Azure. В разделе [связанная служба хранилища Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Hello **connectionString** использует hello storageAccountName и storageAccountKey параметров. Необходимо указать значения для этих параметров при развертывании шаблона hello.  

#### <a name="hdinsight-on-demand-linked-service"></a>Связанная служба кластера HDInsight по запросу
В hello HDInsight по требованию связанное определение службы, укажите значения для параметров конфигурации, используемых hello фабрики данных службы toocreate кластера HDInsight Hadoop во время выполнения. В разделе [связанные службы вычислений](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) статьи для получения сведений об toodefine свойства, используемые JSON связанной службы HDInsight по требованию.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Обратите внимание hello после точки.

* Hello фабрики данных создает **под управлением Linux** кластера HDInsight для вас.
* Hello кластера HDInsight Hadoop создается в hello же регионе, что учетная запись хранения hello.
* Обратите внимание hello *timeToLive* параметр. Фабрика данных Hello автоматически удаляет hello кластера после hello кластера простоя в течение 30 минут.
* Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз фрагмент должен обработать, если нет существующего кластера динамической toobe (**timeToLive**) и удаляется при завершении обработки hello.

Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).

> [!IMPORTANT]
> По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp». Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.

#### <a name="azure-blob-input-dataset"></a>Входной набор данных большого двоичного объекта Azure
В определении hello входного набора данных укажите имена hello контейнер больших двоичных объектов, папки и файла, содержащего входные данные hello. В разделе [свойства набора данных больших двоичных объектов Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

Обратите внимание, следующие параметры в определении JSON hello hello:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Выходной набор данных BLOB-объекта Azure
В определении набора данных для вывода hello укажите имена hello контейнер больших двоичных объектов и папке, содержащей hello выходных данных. В разделе [свойства набора данных больших двоичных объектов Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Hello folderPath указывает hello путь toohello папке, содержащей hello выходные данные:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Hello [доступности набора данных](../data-factory/data-factory-create-datasets.md#dataset-availability) задается следующим образом:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

В фабрике данных Azure, выходной набор данных доступности дисков hello конвейера. В этом примере hello срез создается ежемесячно hello последний день месяца (EndOfInterval). Дополнительные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Конвейер данных
Здесь вы определите конвейер для преобразования данных. Для этого нужно запустить скрипт Hive в кластере HDInsight Azure по требованию. В разделе [конвейера JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) описания toodefine элементы, используемые JSON конвейера в этом примере.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

конвейер Hello содержит одно действие, действие HDInsightHive. Так как даты начала и окончания находятся в пределах января 2016 г., обрабатываются данные только за один месяц (срез). Оба *запустить* и *окончания* hello действия имеют прошедшую дату, поэтому hello фабрики данных обрабатывает данные за месяц hello немедленно. Если конец hello дату в будущем, hello фабрики данных создает другой срез, когда наступает время hello. Дополнительные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Очистка hello учебника

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Удаление контейнеров больших двоичных объектов hello, созданное кластером HDInsight по требованию
С помощью по требованию связанной службы HDInsight кластер HDInsight создается каждый раз фрагмент должен toobe обработки, если нет существующего кластера динамическая (timeToLive); и hello кластер будет удален после завершения обработки hello. Для каждого кластера фабрики данных Azure создает контейнер больших двоичных объектов в хранилище больших двоичных объектов, используется в качестве учетной записи хранилища по умолчанию hello для кластера hello hello. Несмотря на то, что кластер HDInsight удален, контейнер хранилища больших двоичных объектов по умолчанию hello и учетной записи хранения связанных hello не удаляются. В этом весь замысел. По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Удалить hello **adfjobs** и **adfyourdatafactoryname linkedservicename-datetimestamp** папки. контейнер adfjobs Hello содержит журналы заданий из фабрики данных Azure.

### <a name="delete-hello-resource-group"></a>Удаление группы ресурсов hello
[Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md) — используется toodeploy управлять и отслеживать ваше решение как группу.  При удалении группы ресурсов удаляются все компоненты hello внутри группы hello.  

1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Нажмите кнопку **групп ресурсов** на левой панели hello.
3. Щелкните имя группы ресурсов hello, созданный в скриптах PowerShell. Используйте фильтр hello, при наличии слишком много групп ресурсов в списке. Группа ресурсов hello открывается новая колонка.
4. На hello **ресурсов** плитки, должен иметь учетную запись хранения по умолчанию hello и hello фабрики данных, если группа ресурсов hello предоставить другие проекты в списке.
5. Нажмите кнопку **удалить** на hello верхней части колонки hello. Таким образом Удаляет учетную запись хранения hello и hello данные, хранящиеся в учетной записи хранения hello.
6. Введите удаление tooconfirm имя группы ресурсов hello и нажмите кнопку **удалить**.

В случае, если вы не хотите учетной записи хранилища hello toodelete при удалении группы ресурсов hello, рассмотрите следующие архитектуры, разделяя hello бизнес-данных из учетной записи хранения по умолчанию hello hello. В этом случае одну группу ресурсов для учетной записи хранения hello hello бизнес-данными и hello другой группе ресурсов для учетной записи хранения по умолчанию hello для HDInsight связанные службы и hello фабрики данных. При удалении hello второй группы ресурсов, не мешая учетной записи хранилища данных предприятия hello. toodo так:

* Добавьте hello, следуя toohello группы ресурсов верхнего уровня, а также hello Microsoft.DataFactory/datafactories ресурсов в шаблон диспетчера ресурсов. При этом будет создана учетная запись хранения.

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Добавление новой связанной службы toohello точки учетной записи хранения:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Настройте службу ondemand связанных hello HDInsight с дополнительных dependsOn и additionalLinkedServiceNames.

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали как tooprocess кластера HDInsight toouse фабрики данных Azure toocreate по требованию задания Hive. Дополнительные tooread:

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Документация по HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Документация по фабрике данных](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Приложение

### <a name="azure-cli-script"></a>Скрипт Azure CLI
Вместо использования учебника hello toodo Azure PowerShell можно использовать Azure CLI. toouse Azure CLI, сначала следует установить Azure CLI согласно инструкциям hello:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Использовать хранилище hello tooprepare Azure CLI и скопируйте файлы hello

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

Имя контейнера Hello — *adfgetstarted*. Не изменяйте его. В противном случае необходимо tooupdate шаблона диспетчера ресурсов hello. Если вам нужна помощь с помощью этого сценария CLI, см. раздел [использование hello Azure CLI со службой хранилища Azure](../storage/common/storage-azure-cli.md).
