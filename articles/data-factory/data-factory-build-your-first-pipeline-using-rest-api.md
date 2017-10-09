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
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="25e71-103">Руководство. Создание первой фабрики данных Azure с помощью REST API фабрики данных</span><span class="sxs-lookup"><span data-stu-id="25e71-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25e71-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="25e71-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="25e71-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="25e71-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="25e71-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25e71-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="25e71-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25e71-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="25e71-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25e71-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="25e71-109">REST API</span><span class="sxs-lookup"><span data-stu-id="25e71-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="25e71-110">В этой статье используется API-Интерфейс REST фабрики данных toocreate первый фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="25e71-111">toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="25e71-112">конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="25e71-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="25e71-113">Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="25e71-114">Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="25e71-115">Данная статья не охватывает все hello REST API.</span><span class="sxs-lookup"><span data-stu-id="25e71-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="25e71-116">Полную документацию по командлетам фабрики данных см. в [справочнике по REST API фабрики данных](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="25e71-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="25e71-117">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="25e71-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="25e71-118">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="25e71-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="25e71-119">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="25e71-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="25e71-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="25e71-120">Prerequisites</span></span>
* <span data-ttu-id="25e71-121">Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="25e71-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="25e71-122">Установите на компьютер программу [curl](https://curl.haxx.se/dlwiz/) .</span><span class="sxs-lookup"><span data-stu-id="25e71-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="25e71-123">Используйте средство ПЕРЕЛИСТЫВАНИЕ hello с toocreate команды REST фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="25e71-124">Следуя инструкциям в [этой статье](../azure-resource-manager/resource-group-create-service-principal-portal.md) , выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="25e71-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="25e71-125">Создайте веб-приложение с именем **ADFGetStartedApp** в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25e71-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="25e71-126">Получите **идентификатор клиента** и **секретный ключ**.</span><span class="sxs-lookup"><span data-stu-id="25e71-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="25e71-127">Получите значение для **tenant_id**.</span><span class="sxs-lookup"><span data-stu-id="25e71-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="25e71-128">Назначить hello **ADFGetStartedApp** toohello приложения **участника фабрики данных** роли.</span><span class="sxs-lookup"><span data-stu-id="25e71-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="25e71-129">Установите [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25e71-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="25e71-130">Запустите **PowerShell** и выполнения hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="25e71-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="25e71-131">Не закрывайте Azure PowerShell до завершения этого учебника hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="25e71-132">Если закрыть и снова открыть понадобятся toorun hello команд.</span><span class="sxs-lookup"><span data-stu-id="25e71-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="25e71-133">Запустите **AzureRmAccount входа** и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="25e71-134">Запустите **Get AzureRmSubscription** tooview все hello подписок для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="25e71-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="25e71-135">Запустите **NameOfAzureSubscription Get AzureRmSubscription - SubscriptionName | Набор AzureRmContext** tooselect hello подписки на toowork с.</span><span class="sxs-lookup"><span data-stu-id="25e71-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="25e71-136">Замените **NameOfAzureSubscription** с именем hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="25e71-137">Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в hello PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="25e71-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="25e71-138">Некоторые шаги hello в этом учебнике предполагается использовать ADFTutorialResourceGroup с именем группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="25e71-139">Если вы используете другой группе ресурсов, в этом учебнике требуется имя hello toouse вместо ADFTutorialResourceGroup группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="25e71-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="25e71-140">Создание определений JSON</span><span class="sxs-lookup"><span data-stu-id="25e71-140">Create JSON definitions</span></span>
<span data-ttu-id="25e71-141">Создайте следующие файлы JSON в папке hello, где находится curl.exe.</span><span class="sxs-lookup"><span data-stu-id="25e71-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="25e71-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="25e71-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="25e71-143">Имя должно быть глобально уникальным, поэтому можно toomake ADFCopyTutorialDF tooprefix или суффикса его уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="25e71-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="25e71-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="25e71-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="25e71-145">Замените значения **accountname** и **accountkey** на имя вашей учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="25e71-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="25e71-146">toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="25e71-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="25e71-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="25e71-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="25e71-148">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="25e71-149">Свойство</span><span class="sxs-lookup"><span data-stu-id="25e71-149">Property</span></span> | <span data-ttu-id="25e71-150">Описание</span><span class="sxs-lookup"><span data-stu-id="25e71-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="25e71-151">ClusterSize (размер кластера)</span><span class="sxs-lookup"><span data-stu-id="25e71-151">ClusterSize</span></span> |<span data-ttu-id="25e71-152">Размер кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="25e71-153">TimeToLive (срок жизни)</span><span class="sxs-lookup"><span data-stu-id="25e71-153">TimeToLive</span></span> |<span data-ttu-id="25e71-154">Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="25e71-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="25e71-155">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="25e71-155">linkedServiceName</span></span> |<span data-ttu-id="25e71-156">Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные HDInsight</span><span class="sxs-lookup"><span data-stu-id="25e71-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="25e71-157">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="25e71-157">Note hello following points:</span></span>

* <span data-ttu-id="25e71-158">Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello выше JSON.</span><span class="sxs-lookup"><span data-stu-id="25e71-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="25e71-159">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="25e71-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="25e71-160">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="25e71-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="25e71-161">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="25e71-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="25e71-162">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="25e71-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="25e71-163">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="25e71-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="25e71-164">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="25e71-164">This behavior is by design.</span></span> <span data-ttu-id="25e71-165">С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз при обработке среза, если нет существующего кластера динамическая (**timeToLive**) и удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="25e71-166">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="25e71-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="25e71-167">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="25e71-168">имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp».</span><span class="sxs-lookup"><span data-stu-id="25e71-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="25e71-169">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="25e71-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="25e71-170">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="25e71-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="25e71-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="25e71-171">inputdataset.json</span></span>

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

<span data-ttu-id="25e71-172">Hello JSON определяет набор данных с именем **AzureBlobInput**, который представляет входные данные для действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="25e71-173">Кроме того, он указывает, hello входных данных находится в контейнере hello BLOB-объекта с именем **adfgetstarted** и hello папку с именем **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="25e71-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="25e71-174">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="25e71-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="25e71-175">Property</span></span> | <span data-ttu-id="25e71-176">Описание</span><span class="sxs-lookup"><span data-stu-id="25e71-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="25e71-177">type</span><span class="sxs-lookup"><span data-stu-id="25e71-177">type</span></span> |<span data-ttu-id="25e71-178">Hello свойство type имеет значение tooAzureBlob, так как данные находятся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="25e71-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="25e71-179">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="25e71-179">linkedServiceName</span></span> |<span data-ttu-id="25e71-180">ссылается toohello StorageLinkedService, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="25e71-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="25e71-181">fileName</span><span class="sxs-lookup"><span data-stu-id="25e71-181">fileName</span></span> |<span data-ttu-id="25e71-182">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="25e71-182">This property is optional.</span></span> <span data-ttu-id="25e71-183">Если это свойство не указан, извлекаются все файлы hello из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="25e71-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="25e71-184">В этом случае обрабатывается только input.log hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="25e71-185">type</span><span class="sxs-lookup"><span data-stu-id="25e71-185">type</span></span> |<span data-ttu-id="25e71-186">файлы журнала Hello находятся в текстовом формате, поэтому мы используем TextFormat.</span><span class="sxs-lookup"><span data-stu-id="25e71-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="25e71-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="25e71-187">columnDelimiter</span></span> |<span data-ttu-id="25e71-188">столбцы в файлах журнала hello разделяются запятой ()</span><span class="sxs-lookup"><span data-stu-id="25e71-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="25e71-189">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="25e71-189">frequency/interval</span></span> |<span data-ttu-id="25e71-190">tooMonth задать частоту и интервал равен 1, это означает, что входные срезы hello доступны ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="25e71-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="25e71-191">external</span><span class="sxs-lookup"><span data-stu-id="25e71-191">external</span></span> |<span data-ttu-id="25e71-192">Это свойство имеет значение tootrue, если входные данные hello не создается службой фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="25e71-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="25e71-193">outputdataset.json</span></span>

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

<span data-ttu-id="25e71-194">Hello JSON определяет набор данных с именем **AzureBlobOutput**, который представляет выходные данные для действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="25e71-195">Кроме того, он указывает, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfgetstarted** и hello папку с именем **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="25e71-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="25e71-196">Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе.</span><span class="sxs-lookup"><span data-stu-id="25e71-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="25e71-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="25e71-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="25e71-198">Замените свойство **storageaccountname** именем вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="25e71-199">Фрагмент кода hello JSON вы создаете конвейера, который состоит из одного действия, которое использует данные tooprocess Hive в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25e71-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="25e71-200">файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **StorageLinkedService**) и в **сценария**  папки в контейнере hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="25e71-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="25e71-201">Hello **определяет** раздел определяет параметры среды выполнения, которые передаются как значения конфигурации Hive скрипт hive toohello (например ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="25e71-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="25e71-202">Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="25e71-203">В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="25e71-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="25e71-204">В разделе «Конвейера JSON» в [конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md) подробные сведения о JSON свойства, используемые в предшествующих пример hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="25e71-205">Настройка глобальных переменных</span><span class="sxs-lookup"><span data-stu-id="25e71-205">Set global variables</span></span>
<span data-ttu-id="25e71-206">Выполните следующие команды после замены значения hello собственные hello в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25e71-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25e71-207">Инструкции по получению значений для параметров client_id, client_secret, tenant и subscription_id см. в разделе [Предварительные требования](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="25e71-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="25e71-208">Проверка подлинности с помощью AAD</span><span class="sxs-lookup"><span data-stu-id="25e71-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="25e71-209">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="25e71-209">Create data factory</span></span>
<span data-ttu-id="25e71-210">На этом шаге вы создадите фабрику данных Azure с именем **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="25e71-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="25e71-211">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="25e71-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="25e71-212">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="25e71-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="25e71-213">Например действие копирования toocopy данные из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight данных tootransform скрипт Hive.</span><span class="sxs-lookup"><span data-stu-id="25e71-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="25e71-214">Выполните следующие hello данных команды toocreate фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="25e71-215">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="25e71-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="25e71-216">Убедитесь, что hello имя фабрики данных hello, указанные здесь имя, указанное в hello hello совпадений (ADFCopyTutorialDF) **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="25e71-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="25e71-217">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="25e71-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="25e71-218">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-218">View hello results.</span></span> <span data-ttu-id="25e71-219">Если hello фабрика данных успешно создана, вы видите hello JSON для фабрики данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="25e71-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="25e71-220">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="25e71-220">Note hello following points:</span></span>

* <span data-ttu-id="25e71-221">Имя Hello hello фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="25e71-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="25e71-222">При возникновении ошибки hello в результатах: **имя фабрики данных «FirstDataFactoryREST» недоступен**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="25e71-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="25e71-223">Изменение имени hello (например, yournameFirstDataFactoryREST) в hello **datafactory.json** файла.</span><span class="sxs-lookup"><span data-stu-id="25e71-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="25e71-224">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="25e71-225">В первой команде hello Здравствуйте, где **$cmd** переменной присваивается значение, замените FirstDataFactoryREST hello новое имя и выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="25e71-226">Запуск hello следующие две команды tooinvoke hello API-интерфейса REST toocreate hello данных фабрики и печати hello результатов операции hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="25e71-227">экземпляры toocreate фабрики данных, необходимо toobe участника или администратор hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="25e71-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="25e71-228">Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и поэтому становятся публично видимых.</span><span class="sxs-lookup"><span data-stu-id="25e71-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="25e71-229">Если ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**», выполните одно из следующих hello и повторите попытку публикации:</span><span class="sxs-lookup"><span data-stu-id="25e71-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="25e71-230">В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика.</span><span class="sxs-lookup"><span data-stu-id="25e71-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="25e71-231">Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="25e71-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="25e71-232">Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="25e71-233">Это действие автоматически регистрирует поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="25e71-234">Перед созданием конвейера, необходимо toocreate несколько сущностей фабрики данных сначала.</span><span class="sxs-lookup"><span data-stu-id="25e71-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="25e71-235">Необходимо сначала создать связанные службы данных toolink хранилищ и вычисляет tooyour хранилище, определение входных данных и выводить данные toorepresent наборов данных в хранилищах данных связанного.</span><span class="sxs-lookup"><span data-stu-id="25e71-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="25e71-236">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="25e71-236">Create linked services</span></span>
<span data-ttu-id="25e71-237">На этом шаге связать учетную запись хранилища Azure и фабрикой данных кластера tooyour для Azure HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="25e71-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="25e71-238">содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="25e71-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="25e71-239">Hello связанной службы HDInsight — используется toorun скрипт Hive, указанное в действии hello конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="25e71-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="25e71-240">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="25e71-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="25e71-241">На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="25e71-242">С помощью данного учебника используйте hello Azure учетную запись хранения toostore ввода вывода данных и hello HQL файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="25e71-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="25e71-243">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="25e71-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="25e71-244">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="25e71-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="25e71-245">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-245">View hello results.</span></span> <span data-ttu-id="25e71-246">Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="25e71-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="25e71-247">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="25e71-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="25e71-248">На этом шаге связать фабрикой данных кластера tooyour для HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="25e71-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="25e71-249">кластер HDInsight Hello автоматически создается во время выполнения и удалена после завершения обработки и время простоя для hello указанного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="25e71-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="25e71-250">Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25e71-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="25e71-251">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="25e71-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="25e71-252">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="25e71-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="25e71-253">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="25e71-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="25e71-254">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-254">View hello results.</span></span> <span data-ttu-id="25e71-255">Если hello связаны была успешно создана служба см. в разделе hello JSON для службы hello связаны в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="25e71-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="25e71-256">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="25e71-256">Create datasets</span></span>
<span data-ttu-id="25e71-257">На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive.</span><span class="sxs-lookup"><span data-stu-id="25e71-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="25e71-258">Эти наборы данных ссылаются toohello **StorageLinkedService** вы создали ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="25e71-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="25e71-259">Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="25e71-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="25e71-260">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="25e71-260">Create input dataset</span></span>
<span data-ttu-id="25e71-261">На этом шаге создается hello входного набора данных toorepresent входных данных в хранилище больших двоичных объектов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="25e71-262">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="25e71-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="25e71-263">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="25e71-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="25e71-264">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-264">View hello results.</span></span> <span data-ttu-id="25e71-265">Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="25e71-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="25e71-266">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="25e71-266">Create output dataset</span></span>
<span data-ttu-id="25e71-267">На этом шаге создается hello выходной набор данных toorepresent выходные данные хранятся в hello хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="25e71-268">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="25e71-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="25e71-269">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="25e71-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="25e71-270">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-270">View hello results.</span></span> <span data-ttu-id="25e71-271">Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="25e71-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="25e71-272">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="25e71-272">Create pipeline</span></span>
<span data-ttu-id="25e71-273">На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="25e71-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="25e71-274">Входной фрагмент доступен ежемесячно (частота: месяц, интервал: 1), выходные данные срезов ежемесячно и toomonthly также установлено свойство планировщика hello для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="25e71-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="25e71-275">Параметры Hello для hello выходной набор данных и планировщик действие hello должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="25e71-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="25e71-276">В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="25e71-277">Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="25e71-278">Подтвердите, что вы видите hello **input.log** файла в hello **adfgetstarted/inputdata** папку, в хранилище больших двоичных объектов hello и выполнения hello, следующая команда toodeploy hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="25e71-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="25e71-279">С момента hello **запустить** и **окончания** время установлено в прошлом hello и **isPaused** работает toofalse набор, конвейер hello (действие в конвейере hello) сразу же после развертывания.</span><span class="sxs-lookup"><span data-stu-id="25e71-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="25e71-280">Назначить hello команды toovariable с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="25e71-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="25e71-281">Команда hello с помощью **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="25e71-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="25e71-282">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-282">View hello results.</span></span> <span data-ttu-id="25e71-283">Если набор данных hello успешно создана, вы видите hello JSON для набора данных hello в hello **результатов**; в противном случае отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="25e71-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="25e71-284">Поздравляем! Вы создали свой первый конвейер с помощью Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="25e71-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="25e71-285">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="25e71-285">Monitor pipeline</span></span>
<span data-ttu-id="25e71-286">На этом шаге используется фрагменты toomonitor REST API фабрики данных, получаемых hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="25e71-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

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
> <span data-ttu-id="25e71-287">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="25e71-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="25e71-288">Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.</span><span class="sxs-lookup"><span data-stu-id="25e71-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="25e71-289">Запустить hello Invoke-Command и hello следующему пока не увидите срез hello в **готовности** состояние или **сбой** состояния.</span><span class="sxs-lookup"><span data-stu-id="25e71-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="25e71-290">Когда hello среза находится в состоянии готовности, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="25e71-291">Создание кластера HDInsight по требованию Hello обычно занимает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="25e71-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![выходные данные](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="25e71-293">входной файл Hello, удаляется при успешно обработал hello среза.</span><span class="sxs-lookup"><span data-stu-id="25e71-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="25e71-294">Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.</span><span class="sxs-lookup"><span data-stu-id="25e71-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="25e71-295">Можно также использовать Azure портала toomonitor фрагментов и устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="25e71-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="25e71-296">Дополнительные сведения см. в разделе [Отслеживание конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="25e71-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="25e71-297">Сводка</span><span class="sxs-lookup"><span data-stu-id="25e71-297">Summary</span></span>
<span data-ttu-id="25e71-298">В этом учебнике вы создали данных tooprocess фабрики данных Azure, выполнив скрипт Hive в кластере HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="25e71-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="25e71-299">Вы использовали hello редактор фабрики данных в Azure портала toodo hello hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="25e71-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="25e71-300">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="25e71-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="25e71-301">создание двух **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="25e71-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="25e71-302">**Хранилище Azure** связанные toolink службы хранилища больших двоичных объектов Azure, содержащий фабрики данных toohello ввода вывода файлов.</span><span class="sxs-lookup"><span data-stu-id="25e71-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="25e71-303">**Azure HDInsight** связанная служба toolink по требованию фабрикой по требованию toohello кластера HDInsight Hadoop данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="25e71-304">Фабрика данных Azure создает HDInsight Hadoop кластера tooprocess just-in-time входных данных и создают выходных данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="25e71-305">Создать два **наборы данных**, которые описывают входных и выходных данных для действие Hive в HDInsight из конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="25e71-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="25e71-306">Создание **конвейера** с действием **HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="25e71-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25e71-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25e71-307">Next steps</span></span>
<span data-ttu-id="25e71-308">В этой статье описывается создание конвейера с помощью действия преобразования (действие HDInsight), которое по требованию выполняет сценарий Hive в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25e71-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="25e71-309">toosee toouse toocopy действие копирования данных из больших двоичных объектов Azure tooAzure SQL, в статье [учебника: копирование данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="25e71-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="25e71-310">См. также</span><span class="sxs-lookup"><span data-stu-id="25e71-310">See Also</span></span>
| <span data-ttu-id="25e71-311">Раздел</span><span class="sxs-lookup"><span data-stu-id="25e71-311">Topic</span></span> | <span data-ttu-id="25e71-312">Описание</span><span class="sxs-lookup"><span data-stu-id="25e71-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="25e71-313">Справочник по REST API фабрики данных</span><span class="sxs-lookup"><span data-stu-id="25e71-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="25e71-314">См. полную документацию по командлетам фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="25e71-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="25e71-315">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="25e71-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="25e71-316">Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="25e71-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="25e71-317">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="25e71-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="25e71-318">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="25e71-319">Планирование и выполнение</span><span class="sxs-lookup"><span data-stu-id="25e71-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="25e71-320">В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="25e71-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="25e71-321">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="25e71-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="25e71-322">В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="25e71-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
