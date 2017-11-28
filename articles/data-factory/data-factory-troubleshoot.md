---
title: "Устранение неполадок фабрики данных Azure"
description: "Узнайте, как устранять неполадки при использовании фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="aa58c-103">Устранение неполадок фабрики данных</span><span class="sxs-lookup"><span data-stu-id="aa58c-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="aa58c-104">В этой статье приводятся советы по устранению неполадок, возникающих при использовании фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="aa58c-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="aa58c-105">В этой статье перечислены не все возможные проблемы использования службы, однако рассматриваются некоторые вопросы и приводятся общие рекомендации по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="aa58c-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="aa58c-106">Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="aa58c-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="aa58c-107">Ошибка "Подписка не зарегистрирована для использования пространства имен Microsoft.DataFactory"</span><span class="sxs-lookup"><span data-stu-id="aa58c-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="aa58c-108">Если эта ошибка возникает, поставщик ресурсов фабрики данных Azure не был зарегистрирован на компьютере.</span><span class="sxs-lookup"><span data-stu-id="aa58c-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="aa58c-109">Выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="aa58c-109">Do the following:</span></span>

1. <span data-ttu-id="aa58c-110">Запустите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa58c-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="aa58c-111">Войдите в свою учетную запись Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="aa58c-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="aa58c-112">Выполните следующую команду, чтобы зарегистрировать поставщик фабрики данных Azure:</span><span class="sxs-lookup"><span data-stu-id="aa58c-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="aa58c-113">Проблема: ошибка авторизации при выполнении командлета фабрики данных</span><span class="sxs-lookup"><span data-stu-id="aa58c-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="aa58c-114">Скорее всего, для Azure PowerShell используется неправильная учетная запись или подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="aa58c-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="aa58c-115">Чтобы выбрать правильную учетную запись и подписку Azure для Azure PowerShell, используйте такие командлеты:</span><span class="sxs-lookup"><span data-stu-id="aa58c-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="aa58c-116">Login-AzureRmAccount — ввод имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="aa58c-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="aa58c-117">Get-AzureRmSubscription — просмотр всех подписок в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="aa58c-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="aa58c-118">Select-AzureRmSubscription &lt;имя_подписки&gt; — выбор нужной подписки.</span><span class="sxs-lookup"><span data-stu-id="aa58c-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="aa58c-119">Используйте подписку, которая использовалась для создания фабрики данных на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="aa58c-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="aa58c-120">Проблема: не удается запустить экспресс-установку шлюза управления данными с портала Azure</span><span class="sxs-lookup"><span data-stu-id="aa58c-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="aa58c-121">Для экспресс-установки шлюза управления данными требуется Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="aa58c-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="aa58c-122">Если не удается запустить экспресс-установку, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="aa58c-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="aa58c-123">Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="aa58c-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="aa58c-124">Если вы используете браузер Chrome, перейдите в [интернет-магазин Chrome](https://chrome.google.com/webstore/), введите ClickOnce в строке поиска, а затем выберите и установите одно из расширений ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="aa58c-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="aa58c-125">То же самое (установку надстройки) сделайте и в случае с браузером Firefox.</span><span class="sxs-lookup"><span data-stu-id="aa58c-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="aa58c-126">Нажмите кнопку "Открыть меню" на панели инструментов (три горизонтальные линии в правом верхнем углу), нажмите кнопку "Надстройки", введите "ClickOnce" в строку поиска, выберите одно из расширений ClickOnce и установите его.</span><span class="sxs-lookup"><span data-stu-id="aa58c-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="aa58c-127">Щелкните ссылку **Установка вручную** в той же колонке на портале.</span><span class="sxs-lookup"><span data-stu-id="aa58c-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="aa58c-128">Этот подход используется для скачивания файла установки и его запуска вручную.</span><span class="sxs-lookup"><span data-stu-id="aa58c-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="aa58c-129">После успешного завершения установки откроется диалоговое окно настройки шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="aa58c-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="aa58c-130">Скопируйте **ключ** на экране портала и используйте его в диспетчере конфигурации, чтобы вручную зарегистрировать шлюз в службе.</span><span class="sxs-lookup"><span data-stu-id="aa58c-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="aa58c-131">Проблема: не удается подключиться к локальному серверу SQL Server</span><span class="sxs-lookup"><span data-stu-id="aa58c-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="aa58c-132">Запустите **диспетчер конфигурации шлюза управления данными** на компьютере шлюза и используйте вкладку **Устранение неполадок**, чтобы проверить подключение к SQL Server с компьютера шлюза.</span><span class="sxs-lookup"><span data-stu-id="aa58c-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="aa58c-133">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="aa58c-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="aa58c-134">Проблема: срезы входных данных постоянно находятся в состоянии "Waiting"</span><span class="sxs-lookup"><span data-stu-id="aa58c-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="aa58c-135">Срезы могут находиться в состоянии **ожидания** по разным причинам.</span><span class="sxs-lookup"><span data-stu-id="aa58c-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="aa58c-136">Одна из распространенных причин — для свойства **external** не задано значение **true**.</span><span class="sxs-lookup"><span data-stu-id="aa58c-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="aa58c-137">Все наборы данных, созданные вне фабрики данных Azure, должны быть помечены свойством **external** .</span><span class="sxs-lookup"><span data-stu-id="aa58c-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="aa58c-138">Это свойство указывает на то, что данные являются внешними и не поддерживаются какими-либо конвейерами в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="aa58c-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="aa58c-139">После того как данные станут доступны в соответствующем хранилище, срезы данных помечаются флагом **Ready** (готово).</span><span class="sxs-lookup"><span data-stu-id="aa58c-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="aa58c-140">Пример использования свойства **external** приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="aa58c-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="aa58c-141">При необходимости можно указать свойство **externalData***, если для свойства external задано значение true.</span><span class="sxs-lookup"><span data-stu-id="aa58c-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="aa58c-142">Дополнительные сведения об этом свойстве см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="aa58c-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="aa58c-143">Чтобы устранить эту ошибку, добавьте свойство **external** и дополнительный раздел **externalData** в определение JSON входной таблицы и повторно создайте эту таблицу.</span><span class="sxs-lookup"><span data-stu-id="aa58c-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="aa58c-144">Проблема: сбой гибридной операции копирования</span><span class="sxs-lookup"><span data-stu-id="aa58c-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="aa58c-145">Действия по устранению неполадок с копированием в локальное хранилище данных и из него с помощью шлюза управления данными см. в статье [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="aa58c-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="aa58c-146">Проблема: сбой подготовки HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="aa58c-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="aa58c-147">При использовании связанной службы типа HDInsightOnDemandLinkedService нужно задать имя linkedServiceName, указывающее на хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="aa58c-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="aa58c-148">Фабрика данных использует это хранилище для хранения журналов и вспомогательных файлов для кластера HDInsight по запросу.</span><span class="sxs-lookup"><span data-stu-id="aa58c-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="aa58c-149">Иногда подготовка кластера HDInsight по запросу завершается следующей ошибкой:</span><span class="sxs-lookup"><span data-stu-id="aa58c-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="aa58c-150">Обычно эта ошибка указывает на то, что расположение учетной записи хранения, указанной в linkedServiceName, не совпадает с расположением центра обработки данных, в котором происходит подготовка HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa58c-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="aa58c-151">Например, если ваша фабрика данных Azure находится на Западе США (West US), а хранилище Azure расположено на Востоке США (East US), то подготовка по запросу на Западе США выполнена не будет.</span><span class="sxs-lookup"><span data-stu-id="aa58c-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="aa58c-152">Есть еще одно свойство JSON, additionalLinkedServiceNames, где можно указать дополнительные учетные записи хранения в HDInsight по запросу.</span><span class="sxs-lookup"><span data-stu-id="aa58c-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="aa58c-153">Эти дополнительные связанные учетные записи хранения должны находиться в том же расположении, что и кластер HDInsight, иначе происходит сбой с той же ошибкой.</span><span class="sxs-lookup"><span data-stu-id="aa58c-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="aa58c-154">Проблема: сбой настраиваемого действия .NET</span><span class="sxs-lookup"><span data-stu-id="aa58c-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="aa58c-155">Подробные действия см. в разделе [Отладка конвейера с помощью настраиваемого действия](data-factory-use-custom-activities.md#troubleshoot-failures).</span><span class="sxs-lookup"><span data-stu-id="aa58c-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="aa58c-156">Устранение неполадок с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="aa58c-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="aa58c-157">Использование колонок на портале</span><span class="sxs-lookup"><span data-stu-id="aa58c-157">Using portal blades</span></span>
<span data-ttu-id="aa58c-158">Действия см. в статье [Мониторинг конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="aa58c-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="aa58c-159">Использование приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="aa58c-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="aa58c-160">Сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa58c-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="aa58c-161">Использование Azure PowerShell для устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="aa58c-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="aa58c-162">Использование Azure PowerShell для устранения ошибок</span><span class="sxs-lookup"><span data-stu-id="aa58c-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="aa58c-163">Сведения см. в разделе [Мониторинг конвейеров фабрики данных с помощью Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="aa58c-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
