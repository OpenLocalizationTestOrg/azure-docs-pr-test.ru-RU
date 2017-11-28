---
title: "Создание первой фабрики данных (REST) | Документация Майкрософт"
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
ms.openlocfilehash: b0c237667f1f55298df20ab0f525202aa1b42e0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="2c42d-103">Руководство. Создание первой фабрики данных Azure с помощью REST API фабрики данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c42d-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2c42d-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="2c42d-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2c42d-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="2c42d-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2c42d-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="2c42d-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c42d-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="2c42d-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c42d-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="2c42d-109">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="2c42d-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="2c42d-110">Из этой статьи вы узнаете, как создать первую фабрику данных Azure с помощью REST API фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-110">In this article, you use Data Factory REST API to create your first Azure data factory.</span></span> <span data-ttu-id="2c42d-111">Чтобы выполнить приведенные здесь инструкции с помощью других средств или пакетов SDK, выберите в раскрывающемся списке один из доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="2c42d-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="2c42d-112">В этом руководстве конвейеру доступно одно действие — **действие Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="2c42d-113">Это действие запускает сценарий Hive в кластере HDInsight Azure, который преобразует входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="2c42d-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="2c42d-114">Конвейер запускается раз в месяц по расписанию. Время начала и окончания запуска также указаны.</span><span class="sxs-lookup"><span data-stu-id="2c42d-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="2c42d-115">В этой статье рассматриваются не все REST API.</span><span class="sxs-lookup"><span data-stu-id="2c42d-115">This article does not cover all the REST API.</span></span> <span data-ttu-id="2c42d-116">Полную документацию по командлетам фабрики данных см. в [справочнике по REST API фабрики данных](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="2c42d-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="2c42d-117">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="2c42d-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="2c42d-118">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="2c42d-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="2c42d-119">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="2c42d-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2c42d-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2c42d-120">Prerequisites</span></span>
* <span data-ttu-id="2c42d-121">Прочтите [обзорную статью](data-factory-build-your-first-pipeline.md) и выполните **предварительные требования** .</span><span class="sxs-lookup"><span data-stu-id="2c42d-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="2c42d-122">Установите на компьютер программу [curl](https://curl.haxx.se/dlwiz/) .</span><span class="sxs-lookup"><span data-stu-id="2c42d-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="2c42d-123">Она будет использоваться с командами REST для создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-123">You use the CURL tool with REST commands to create a data factory.</span></span>
* <span data-ttu-id="2c42d-124">Следуя инструкциям в [этой статье](../azure-resource-manager/resource-group-create-service-principal-portal.md) , выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="2c42d-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="2c42d-125">Создайте веб-приложение с именем **ADFGetStartedApp** в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c42d-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="2c42d-126">Получите **идентификатор клиента** и **секретный ключ**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="2c42d-127">Получите значение для **tenant_id**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="2c42d-128">Назначьте приложение **ADFGetStartedApp** роли **участника фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-128">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="2c42d-129">Установите [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2c42d-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2c42d-130">Откройте **PowerShell** и выполните приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="2c42d-130">Launch **PowerShell** and run the following command.</span></span> <span data-ttu-id="2c42d-131">Не закрывайте Azure PowerShell, пока выполняются описанные в учебнике инструкции.</span><span class="sxs-lookup"><span data-stu-id="2c42d-131">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="2c42d-132">Если закрыть и снова открыть это окно, то придется вновь выполнять эти команды.</span><span class="sxs-lookup"><span data-stu-id="2c42d-132">If you close and reopen, you need to run the commands again.</span></span>
  1. <span data-ttu-id="2c42d-133">Выполните командлет **Login-AzureRmAccount** и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-133">Run **Login-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span></span>
  2. <span data-ttu-id="2c42d-134">Выполните командлет **Get-AzureRmSubscription** , чтобы просмотреть все подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2c42d-134">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span></span>
  3. <span data-ttu-id="2c42d-135">Выполните команду **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext**, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="2c42d-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span></span> <span data-ttu-id="2c42d-136">Замените **NameOfAzureSubscription** именем своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-136">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>
* <span data-ttu-id="2c42d-137">Создайте группу ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2c42d-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="2c42d-138">Некоторые действия, описанные в этом учебнике, предполагают, что вы используете группу ресурсов с именем ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="2c42d-138">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="2c42d-139">Если вы используете другую группу ресурсов, укажите ее имя вместо ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="2c42d-139">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="2c42d-140">Создание определений JSON</span><span class="sxs-lookup"><span data-stu-id="2c42d-140">Create JSON definitions</span></span>
<span data-ttu-id="2c42d-141">В папке, где находится файл curl.exe, создайте следующие JSON-файлы.</span><span class="sxs-lookup"><span data-stu-id="2c42d-141">Create following JSON files in the folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="2c42d-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="2c42d-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2c42d-143">Имя должно быть глобально уникальным, поэтому может потребоваться добавить к ADFCopyTutorialDF префикс или суффикс.</span><span class="sxs-lookup"><span data-stu-id="2c42d-143">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="2c42d-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="2c42d-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2c42d-145">Замените значения **accountname** и **accountkey** на имя вашей учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="2c42d-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="2c42d-146">Сведения о получении, просмотре, копировании и повторном создании ключей доступа к хранилищу см. в разделе [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2c42d-146">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="2c42d-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="2c42d-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="2c42d-148">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="2c42d-148">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="2c42d-149">Свойство</span><span class="sxs-lookup"><span data-stu-id="2c42d-149">Property</span></span> | <span data-ttu-id="2c42d-150">Описание</span><span class="sxs-lookup"><span data-stu-id="2c42d-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2c42d-151">ClusterSize (размер кластера)</span><span class="sxs-lookup"><span data-stu-id="2c42d-151">ClusterSize</span></span> |<span data-ttu-id="2c42d-152">Размер кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-152">Size of the HDInsight cluster.</span></span> |
| <span data-ttu-id="2c42d-153">TimeToLive (срок жизни)</span><span class="sxs-lookup"><span data-stu-id="2c42d-153">TimeToLive</span></span> |<span data-ttu-id="2c42d-154">Указывает, сколько времени может простаивать кластер HDInsight, прежде чем он будет удален.</span><span class="sxs-lookup"><span data-stu-id="2c42d-154">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="2c42d-155">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="2c42d-155">linkedServiceName</span></span> |<span data-ttu-id="2c42d-156">Указывает имя учетной записи хранения, в которой будут храниться журналы, создаваемые HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-156">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

<span data-ttu-id="2c42d-157">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-157">Note the following points:</span></span>

* <span data-ttu-id="2c42d-158">С помощью приведенного выше JSON-файла фабрика данных создает кластер HDInsight **под управлением Linux**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-158">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="2c42d-159">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="2c42d-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="2c42d-160">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="2c42d-161">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="2c42d-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="2c42d-162">Кластер HDInsight создает **контейнер по умолчанию** в хранилище BLOB-объектов, указанном в коде JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="2c42d-162">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="2c42d-163">При удалении кластера HDInsight этот контейнер не удаляется.</span><span class="sxs-lookup"><span data-stu-id="2c42d-163">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="2c42d-164">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="2c42d-164">This behavior is by design.</span></span> <span data-ttu-id="2c42d-165">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается всякий раз, когда обрабатывается срез данных (если не используется динамический кластер**timeToLive**), после чего кластер удаляется.</span><span class="sxs-lookup"><span data-stu-id="2c42d-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

    <span data-ttu-id="2c42d-166">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="2c42d-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="2c42d-167">Если эти контейнеры не используются для устранения неполадок с заданиями, удалите их — это позволит сократить расходы на хранение.</span><span class="sxs-lookup"><span data-stu-id="2c42d-167">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="2c42d-168">Имена контейнеров указаны в формате adf**имя_фабрики_данных**-**имя_связанной_службы**-метка_даты_и_времени.</span><span class="sxs-lookup"><span data-stu-id="2c42d-168">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="2c42d-169">Для удаления контейнеров в хранилище BLOB-объектов Azure используйте такие инструменты, как [Microsoft Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="2c42d-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="2c42d-170">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="2c42d-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="2c42d-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="2c42d-171">inputdataset.json</span></span>

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

<span data-ttu-id="2c42d-172">Приведенный выше JSON-файл определяет набор данных с именем **AzureBlobInput**, представляющий входные данные для действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="2c42d-172">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="2c42d-173">Кроме того, файл указывает, что входные данные размещаются в контейнере больших двоичных объектов **adfgetstarted** и в папке **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-173">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

<span data-ttu-id="2c42d-174">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="2c42d-174">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="2c42d-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="2c42d-175">Property</span></span> | <span data-ttu-id="2c42d-176">Описание</span><span class="sxs-lookup"><span data-stu-id="2c42d-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2c42d-177">type</span><span class="sxs-lookup"><span data-stu-id="2c42d-177">type</span></span> |<span data-ttu-id="2c42d-178">Для свойства типа задано значение AzureBlob, так как данные хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-178">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="2c42d-179">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="2c42d-179">linkedServiceName</span></span> |<span data-ttu-id="2c42d-180">Ссылается на созданную ранее службу StorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="2c42d-180">refers to the StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="2c42d-181">fileName</span><span class="sxs-lookup"><span data-stu-id="2c42d-181">fileName</span></span> |<span data-ttu-id="2c42d-182">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="2c42d-182">This property is optional.</span></span> <span data-ttu-id="2c42d-183">Если это свойство не указано, выбираются все файлы из папки folderPath.</span><span class="sxs-lookup"><span data-stu-id="2c42d-183">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="2c42d-184">В этом случае обрабатывается только файл input.log.</span><span class="sxs-lookup"><span data-stu-id="2c42d-184">In this case, only the input.log is processed.</span></span> |
| <span data-ttu-id="2c42d-185">type</span><span class="sxs-lookup"><span data-stu-id="2c42d-185">type</span></span> |<span data-ttu-id="2c42d-186">Файлы журнала представлены в текстовом формате, поэтому мы используем значение TextFormat.</span><span class="sxs-lookup"><span data-stu-id="2c42d-186">The log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="2c42d-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="2c42d-187">columnDelimiter</span></span> |<span data-ttu-id="2c42d-188">Столбцы в файлах журнала разделяются запятыми (,).</span><span class="sxs-lookup"><span data-stu-id="2c42d-188">columns in the log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="2c42d-189">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="2c42d-189">frequency/interval</span></span> |<span data-ttu-id="2c42d-190">Для свойства frequency задано значение Month, а для свойства interval — значение 1. Это означает, что срезы входных данных доступны ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="2c42d-190">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
| <span data-ttu-id="2c42d-191">external</span><span class="sxs-lookup"><span data-stu-id="2c42d-191">external</span></span> |<span data-ttu-id="2c42d-192">Это свойство имеет значение true, если входные данные не создаются службой фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-192">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="2c42d-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="2c42d-193">outputdataset.json</span></span>

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

<span data-ttu-id="2c42d-194">JSON-файл определяет набор данных с именем **AzureBlobOutput**, представляющий выходные данные для действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="2c42d-194">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="2c42d-195">Кроме того, файл указывает, что результаты хранятся в контейнере больших двоичных объектов **adfgetstarted** и в папке **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-195">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="2c42d-196">В разделе **availability** указывается частота, с которой будет создаваться выходной набор данных (ежемесячно).</span><span class="sxs-lookup"><span data-stu-id="2c42d-196">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="2c42d-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="2c42d-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2c42d-198">Замените свойство **storageaccountname** именем вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="2c42d-199">Этот фрагмент JSON-файла создает конвейер из одного действия, использующего Hive для обработки данных в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-199">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span></span>

<span data-ttu-id="2c42d-200">Файл **partitionweblogs.hql** скрипта Hive хранится в учетной записи хранения Azure (указывается с помощью свойства scriptLinkedService с именем **StorageLinkedService**) в папке **script** в контейнере **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-200">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

<span data-ttu-id="2c42d-201">Раздел **defines** указывает параметров среды выполнения, которые будут переданы в сценарий Hive в качестве значений конфигурации Hive (например, ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="2c42d-201">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="2c42d-202">Активный период конвейера задается с помощью свойств **start** и **end**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-202">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

<span data-ttu-id="2c42d-203">В действии JSON укажите, что скрипт Hive будет выполняться в среде вычислений, указанной в свойстве **linkedServiceName**, — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-203">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="2c42d-204">Сведения о свойствах JSON, используемых в предыдущем примере, см. в разделе "Конвейер JSON" статьи [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2c42d-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="2c42d-205">Настройка глобальных переменных</span><span class="sxs-lookup"><span data-stu-id="2c42d-205">Set global variables</span></span>
<span data-ttu-id="2c42d-206">Выполните следующие команды в Azure PowerShell, подставив собственные значения.</span><span class="sxs-lookup"><span data-stu-id="2c42d-206">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c42d-207">Инструкции по получению значений для параметров client_id, client_secret, tenant и subscription_id см. в разделе [Предварительные требования](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2c42d-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="2c42d-208">Проверка подлинности с помощью AAD</span><span class="sxs-lookup"><span data-stu-id="2c42d-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="2c42d-209">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-209">Create data factory</span></span>
<span data-ttu-id="2c42d-210">На этом шаге вы создадите фабрику данных Azure с именем **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="2c42d-211">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="2c42d-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="2c42d-212">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="2c42d-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="2c42d-213">Это может быть, например, действие копирования данных из исходного хранилища в целевое или действие HDInsight Hive для выполнения скрипта Hive, преобразующего данные.</span><span class="sxs-lookup"><span data-stu-id="2c42d-213">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform data.</span></span> <span data-ttu-id="2c42d-214">Чтобы создать фабрику данных, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2c42d-214">Run the following commands to create the data factory:</span></span>

1. <span data-ttu-id="2c42d-215">Назначьте команду переменной с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-215">Assign the command to variable named **cmd**.</span></span>

    <span data-ttu-id="2c42d-216">Указываемое здесь имя фабрики данных (ADFCopyTutorialDF) должно соответствовать имени, указанному в **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-216">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="2c42d-217">Выполните команду с использованием командлета **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-217">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="2c42d-218">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-218">View the results.</span></span> <span data-ttu-id="2c42d-219">После успешного создания фабрики данных в **результатах** появится JSON-файл. В противном случае отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2c42d-219">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="2c42d-220">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-220">Note the following points:</span></span>

* <span data-ttu-id="2c42d-221">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="2c42d-221">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="2c42d-222">Если в результатах отобразится сообщение об ошибке **Имя FirstDataFactoryREST фабрики данных недоступно**, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2c42d-222">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span></span>
  1. <span data-ttu-id="2c42d-223">Измените имя (например, на ваше_имя_FirstDataFactoryREST) в файле **datafactory.json** .</span><span class="sxs-lookup"><span data-stu-id="2c42d-223">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span></span> <span data-ttu-id="2c42d-224">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="2c42d-225">В первой команде, где переменной **$cmd** присваивается значение, замените FirstDataFactoryREST на новое имя и выполните команду.</span><span class="sxs-lookup"><span data-stu-id="2c42d-225">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span></span>
  3. <span data-ttu-id="2c42d-226">Выполните следующие две команды, чтобы вызвать REST API для создания фабрики данных и вывода результатов операции.</span><span class="sxs-lookup"><span data-stu-id="2c42d-226">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span>
* <span data-ttu-id="2c42d-227">Чтобы создать экземпляры фабрики данных, вы должны быть администратором или участником подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-227">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="2c42d-228">В будущем имя фабрики данных может быть зарегистрировано в качестве DNS-имени и, следовательно, стать отображаемым.</span><span class="sxs-lookup"><span data-stu-id="2c42d-228">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="2c42d-229">Если появится сообщение об ошибке**Подписка не зарегистрирована для использования пространства имен Microsoft.DataFactory**, выполните одно из следующих действий и повторите попытку публикации.</span><span class="sxs-lookup"><span data-stu-id="2c42d-229">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="2c42d-230">Чтобы зарегистрировать поставщик фабрики данных Azure, выполните следующую команду в Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2c42d-230">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="2c42d-231">Чтобы убедиться, что поставщик фабрики данных зарегистрирован, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2c42d-231">You can run the following command to confirm that the Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="2c42d-232">Войдите на [портал Azure](https://portal.azure.com) с использованием подписки Azure и откройте колонку фабрики данных или создайте на портале фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-232">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="2c42d-233">Поставщик будет зарегистрирован автоматически.</span><span class="sxs-lookup"><span data-stu-id="2c42d-233">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="2c42d-234">Прежде чем создавать конвейер, необходимо создать несколько сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-234">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="2c42d-235">Сначала создайте связанные службы, чтобы связать хранилища данных и вычисления со своим хранилищем данных, и определите входные и выходные наборы данных, которые будут представлять данные в связанных хранилищах.</span><span class="sxs-lookup"><span data-stu-id="2c42d-235">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="2c42d-236">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="2c42d-236">Create linked services</span></span>
<span data-ttu-id="2c42d-237">На этом шаге вы свяжете учетную запись службы хранилища Azure и используемый по запросу кластер Azure HDInsight с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="2c42d-238">В этом примере учетная запись хранения Azure содержит входные и выходные данные для конвейера.</span><span class="sxs-lookup"><span data-stu-id="2c42d-238">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="2c42d-239">Для выполнения скрипта Hive, указанного в действии конвейера, в этом примере используется связанная служба HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-239">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="2c42d-240">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="2c42d-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="2c42d-241">На этом шаге вы свяжете учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-241">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="2c42d-242">В целях данного руководства используйте одну и ту же учетную запись хранения Azure для хранения входных и выходных данных и файла скрипта HQL.</span><span class="sxs-lookup"><span data-stu-id="2c42d-242">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="2c42d-243">Назначьте команду переменной с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-243">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="2c42d-244">Выполните команду с использованием командлета **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-244">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="2c42d-245">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-245">View the results.</span></span> <span data-ttu-id="2c42d-246">После успешного создания связанной службы в **результатах** появится JSON-файл. В противном случае отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2c42d-246">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="2c42d-247">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c42d-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="2c42d-248">На этом шаге вы свяжете используемый по запросу кластер HDInsight с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-248">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="2c42d-249">Кластер HDInsight автоматически создается в среде выполнения и удаляется после завершения обработки и простоя в течение указанного времени.</span><span class="sxs-lookup"><span data-stu-id="2c42d-249">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="2c42d-250">Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="2c42d-251">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="2c42d-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="2c42d-252">Назначьте команду переменной с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-252">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="2c42d-253">Выполните команду с использованием командлета **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-253">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="2c42d-254">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-254">View the results.</span></span> <span data-ttu-id="2c42d-255">После успешного создания связанной службы в **результатах** появится JSON-файл. В противном случае отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2c42d-255">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="2c42d-256">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-256">Create datasets</span></span>
<span data-ttu-id="2c42d-257">На этом шаге вы создадите наборы данных, которые представляют входные и выходные данные для обработки Hive.</span><span class="sxs-lookup"><span data-stu-id="2c42d-257">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="2c42d-258">Эти наборы данных ссылаются на службу **StorageLinkedService** , созданную ранее в ходе работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="2c42d-258">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="2c42d-259">Точки связанной службы указывают на учетную запись хранения Azure, а наборы данных указывают контейнер, папку и имя файла в хранилище, в котором содержатся входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2c42d-259">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="2c42d-260">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-260">Create input dataset</span></span>
<span data-ttu-id="2c42d-261">Теперь создайте входной набор данных, представляющий входные данные, которые хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-261">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="2c42d-262">Назначьте команду переменной с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-262">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="2c42d-263">Выполните команду с использованием командлета **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-263">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="2c42d-264">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-264">View the results.</span></span> <span data-ttu-id="2c42d-265">После успешного создания набора данных в **результатах** появится JSON-файл. В противном случае отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2c42d-265">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="2c42d-266">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-266">Create output dataset</span></span>
<span data-ttu-id="2c42d-267">Теперь создайте выходной набор данных, представляющий выходные данные, которые хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-267">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="2c42d-268">Назначьте команду переменной с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-268">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="2c42d-269">Выполните команду с использованием командлета **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-269">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="2c42d-270">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-270">View the results.</span></span> <span data-ttu-id="2c42d-271">После успешного создания набора данных в **результатах** появится JSON-файл. В противном случае отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2c42d-271">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="2c42d-272">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="2c42d-272">Create pipeline</span></span>
<span data-ttu-id="2c42d-273">На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="2c42d-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="2c42d-274">Срез входных данных создается ежемесячно (frequency: Month, interval: 1), срез выходных данных создается ежемесячно, свойство scheduler для действия также указывается ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="2c42d-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="2c42d-275">Параметры выходного набора данных (outputs) и планировщика действия (scheduler) должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="2c42d-275">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="2c42d-276">В настоящее время расписание активируется с помощью выходного набора данных, поэтому его необходимо создать, даже если действие не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-276">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="2c42d-277">Если действие не принимает никаких входных данных, входной набор данных можно не создавать.</span><span class="sxs-lookup"><span data-stu-id="2c42d-277">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

<span data-ttu-id="2c42d-278">Убедитесь, что файл **input.log** отображается в папке **adfgetstarted/inputdata** в хранилище BLOB-объектов Azure, и выполните следующую команду, чтобы развернуть конвейер.</span><span class="sxs-lookup"><span data-stu-id="2c42d-278">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="2c42d-279">Так как время в свойствах **start** и **end** задано в прошлом, а для свойства **isPaused** задано значение false, конвейер (действие в конвейере) запускается сразу после развертывания.</span><span class="sxs-lookup"><span data-stu-id="2c42d-279">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="2c42d-280">Назначьте команду переменной с именем **cmd**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-280">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="2c42d-281">Выполните команду с использованием командлета **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-281">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="2c42d-282">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="2c42d-282">View the results.</span></span> <span data-ttu-id="2c42d-283">После успешного создания набора данных в **результатах** появится JSON-файл. В противном случае отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="2c42d-283">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="2c42d-284">Поздравляем! Вы создали свой первый конвейер с помощью Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="2c42d-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="2c42d-285">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="2c42d-285">Monitor pipeline</span></span>
<span data-ttu-id="2c42d-286">На этом шаге используется REST API фабрики данных, чтобы отслеживать срезы, созданные конвейером.</span><span class="sxs-lookup"><span data-stu-id="2c42d-286">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

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
> <span data-ttu-id="2c42d-287">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="2c42d-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="2c42d-288">Таким образом, конвейер обработает срез **примерно через 30 минут** .</span><span class="sxs-lookup"><span data-stu-id="2c42d-288">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
>

<span data-ttu-id="2c42d-289">Запускайте командлет Invoke-Command, пока не увидите срез в состоянии **Готово** или **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-289">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="2c42d-290">Когда срез перейдет в состояние "Готово", проверьте выходные данные в папке **partitioneddata** контейнера **adfgetstarted** в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2c42d-290">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="2c42d-291">Создание кластера HDInsight по требованию занимает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="2c42d-291">The creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![выходные данные](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="2c42d-293">В случае успешной обработки среза входной файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="2c42d-293">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="2c42d-294">Если вы хотите повторно обработать срез или еще раз выполнить инструкции из руководства, передайте входной файл (input.log) в папку inputdata в контейнере adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="2c42d-294">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

<span data-ttu-id="2c42d-295">Для отслеживания срезов и устранения возникших проблем можно использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-295">You can also use Azure portal to monitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="2c42d-296">Дополнительные сведения см. в разделе [Отслеживание конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="2c42d-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="2c42d-297">Сводка</span><span class="sxs-lookup"><span data-stu-id="2c42d-297">Summary</span></span>
<span data-ttu-id="2c42d-298">Следуя инструкциям из этого руководства, вы создали фабрику данных Azure для обработки данных путем выполнения сценария Hive в кластере Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-298">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="2c42d-299">Вы использовали редактор фабрики данных на портале Azure для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="2c42d-299">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="2c42d-300">создание **фабрики данных Azure**;</span><span class="sxs-lookup"><span data-stu-id="2c42d-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="2c42d-301">создание двух **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="2c42d-302">**Служба хранилища Azure** — связанная служба для связывания хранилища BLOB-объектов Azure, которое содержит входные и выходные файлы, с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-302">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="2c42d-303">**Azure HDInsight** — связанная служба по запросу для связывания кластера HDInsight Hadoop с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-303">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="2c42d-304">Фабрика данных Azure своевременно создает кластер HDInsight Hadoop для обработки входных данных и генерирования выходных данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="2c42d-305">Создание двух **наборов данных**, которые описывают входные и выходные данные для действия HDInsight Hive в конвейере.</span><span class="sxs-lookup"><span data-stu-id="2c42d-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="2c42d-306">Создание **конвейера** с действием **HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="2c42d-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c42d-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c42d-307">Next steps</span></span>
<span data-ttu-id="2c42d-308">В этой статье описывается создание конвейера с помощью действия преобразования (действие HDInsight), которое по требованию выполняет сценарий Hive в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c42d-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="2c42d-309">Сведения о том, как копировать данные из хранилища BLOB-объектов Azure в SQL Azure с помощью действия копирования, см. в статье [Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2c42d-309">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c42d-310">См. также</span><span class="sxs-lookup"><span data-stu-id="2c42d-310">See Also</span></span>
| <span data-ttu-id="2c42d-311">Раздел</span><span class="sxs-lookup"><span data-stu-id="2c42d-311">Topic</span></span> | <span data-ttu-id="2c42d-312">Описание</span><span class="sxs-lookup"><span data-stu-id="2c42d-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="2c42d-313">Справочник по REST API фабрики данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="2c42d-314">См. полную документацию по командлетам фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="2c42d-315">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="2c42d-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="2c42d-316">Эта статья поможет вам понять сущность конвейеров и действий в фабрике данных Azure, а также научиться с их помощью создавать комплексные рабочие процессы, управляемые данными, для конкретных бизнес-сценариев.</span><span class="sxs-lookup"><span data-stu-id="2c42d-316">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="2c42d-317">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="2c42d-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="2c42d-318">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42d-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="2c42d-319">Планирование и выполнение</span><span class="sxs-lookup"><span data-stu-id="2c42d-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="2c42d-320">Здесь объясняются аспекты планирования и исполнения в модели приложений фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2c42d-320">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="2c42d-321">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="2c42d-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="2c42d-322">В этой статье описывается мониторинг и отладка конвейеров, а также управление ими с помощью приложения мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="2c42d-322">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
