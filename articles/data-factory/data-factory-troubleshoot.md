---
title: "проблемы aaaTroubleshoot фабрики данных Azure"
description: "Узнайте, как tootroubleshoot проблемы с помощью фабрики данных Azure."
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
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="38f4c-103">Устранение неполадок фабрики данных</span><span class="sxs-lookup"><span data-stu-id="38f4c-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="38f4c-104">В этой статье приводятся советы по устранению неполадок, возникающих при использовании фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="38f4c-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="38f4c-105">В этой статье не включает все возможные причины неполадок hello, при использовании службы hello, однако он охватывает некоторые проблемы и Общие советы по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="38f4c-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="38f4c-106">Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="38f4c-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="38f4c-107">Ошибка: hello подписки не зарегистрированного toouse пространством имен «Microsoft.DataFactory»</span><span class="sxs-lookup"><span data-stu-id="38f4c-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="38f4c-108">Если эта ошибка поставщика ресурсов hello фабрики данных Azure не был зарегистрирован на компьютере.</span><span class="sxs-lookup"><span data-stu-id="38f4c-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="38f4c-109">Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="38f4c-109">Do hello following:</span></span>

1. <span data-ttu-id="38f4c-110">Запустите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38f4c-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="38f4c-111">Войдите в систему tooyour учетная запись Azure с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="38f4c-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="38f4c-112">Выполните следующие команды tooregister hello фабрики данных Azure поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="38f4c-113">Проблема: ошибка авторизации при выполнении командлета фабрики данных</span><span class="sxs-lookup"><span data-stu-id="38f4c-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="38f4c-114">Возможно, не используются hello справа учетной записи Azure или подписок с hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38f4c-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="38f4c-115">Используйте следующие командлеты tooselect hello справа Azure toouse учетной записи и подписки с hello Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="38f4c-116">AzureRmAccount входа - используйте hello правой пользователя и пароль</span><span class="sxs-lookup"><span data-stu-id="38f4c-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="38f4c-117">Get-AzureRmSubscription - представление всех hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="38f4c-118">Выберите AzureRmSubscription &lt;имя подписки&gt; -выберите подходящую подписку hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="38f4c-119">Используйте hello один на портал Azure hello используется toocreate фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="38f4c-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="38f4c-120">Проблема: Не toolaunch экспресс-установки данных управления шлюза с портала Azure</span><span class="sxs-lookup"><span data-stu-id="38f4c-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="38f4c-121">Установка экспресс-выпуск Hello для hello шлюз управления данными требуется Internet Explorer или браузер, совместимый Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="38f4c-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="38f4c-122">При сбое установки Express hello toostart выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="38f4c-123">Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="38f4c-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="38f4c-124">При использовании Chrome go toohello [Chrome веб-хранилище](https://chrome.google.com/webstore/)поиска с ключевым словом «ClickOnce», выбрав один из модулей ClickOnce hello и установить его.</span><span class="sxs-lookup"><span data-stu-id="38f4c-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="38f4c-125">Здравствуйте же для Firefox (установка надстройки).</span><span class="sxs-lookup"><span data-stu-id="38f4c-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="38f4c-126">Нажмите кнопку Открыть меню на панели инструментов hello (три горизонтальные линии в правом верхнем углу hello), выберите дополнительные компоненты, поиска с ключевым словом «ClickOnce», выбрать один из модулей ClickOnce hello и установить его.</span><span class="sxs-lookup"><span data-stu-id="38f4c-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="38f4c-127">Используйте hello **ручной установки** ссылки, представленной на hello же колонке hello портала.</span><span class="sxs-lookup"><span data-stu-id="38f4c-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="38f4c-128">Используйте этот подход toodownload установочный файл и запустить его вручную.</span><span class="sxs-lookup"><span data-stu-id="38f4c-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="38f4c-129">После успешного завершения установки hello, появится диалоговое окно настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="38f4c-130">Копировать hello **ключ** из портала экран приветствия и используйте его в hello configuration manager toomanually зарегистрируйте шлюз hello службе hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="38f4c-131">Проблема: Не tooconnect tooon локальный SQL Server</span><span class="sxs-lookup"><span data-stu-id="38f4c-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="38f4c-132">Запустите **диспетчера конфигурации шлюза управления данными** на компьютере шлюза hello и использовать hello **Устранение неполадок** вкладке tooSQL подключения tootest hello Server с компьютера шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="38f4c-133">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="38f4c-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="38f4c-134">Проблема: срезы входных данных постоянно находятся в состоянии "Waiting"</span><span class="sxs-lookup"><span data-stu-id="38f4c-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="38f4c-135">Hello срезы могут находиться в **ожидания** состояния из-за причин toovarious.</span><span class="sxs-lookup"><span data-stu-id="38f4c-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="38f4c-136">Одной из распространенных причин hello является, hello **внешних** свойство не задано слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="38f4c-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="38f4c-137">Любой набор данных, производимых hello вне области фабрики данных Azure должны быть отмечены **внешних** свойство.</span><span class="sxs-lookup"><span data-stu-id="38f4c-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="38f4c-138">Это свойство указывает, что данные hello внешний и не резервная копия по любой конвейера в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="38f4c-139">срезы данных Hello, помечаются как **готовности** после hello данные недоступны в хранилище соответствующие hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="38f4c-140">См. следующий пример использования hello hello hello **внешних** свойство.</span><span class="sxs-lookup"><span data-stu-id="38f4c-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="38f4c-141">Дополнительно можно указать **externalData*** при задании внешнего tootrue.</span><span class="sxs-lookup"><span data-stu-id="38f4c-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="38f4c-142">Дополнительные сведения об этом свойстве см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="38f4c-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="38f4c-143">tooresolve Здравствуйте ошибки, добавьте hello **внешних** свойство и необязательный hello **externalData** статьи toohello JSON определение входной таблицы hello и заново создайте таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="38f4c-144">Проблема: сбой гибридной операции копирования</span><span class="sxs-lookup"><span data-stu-id="38f4c-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="38f4c-145">В разделе [Устранение неполадок шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) для хранения tootroubleshoot проблемы с копированием из локальных данных с помощью действия hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="38f4c-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="38f4c-146">Проблема: сбой подготовки HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="38f4c-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="38f4c-147">При использовании связанной службы типа HDInsightOnDemand, необходимо toospecify linkedServiceName, который указывает tooan хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="38f4c-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="38f4c-148">Служба фабрики данных использует это хранилище toostore журналы и вспомогательные файлы для кластера HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="38f4c-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="38f4c-149">Иногда подготовки кластера HDInsight по требованию завершается hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="38f4c-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="38f4c-150">Эта ошибка обычно указывает, что расположение hello hello учетной записи хранения указан в hello linkedServiceName не hello местоположении, где происходит Подготовка HDInsight hello центра обработки данных и те же данные.</span><span class="sxs-lookup"><span data-stu-id="38f4c-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="38f4c-151">Пример: Если фабрики данных является на Западе США и hello хранилища Azure находится в США, Восток, hello подготовки завершается с ошибкой по запросу на Западе США.</span><span class="sxs-lookup"><span data-stu-id="38f4c-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="38f4c-152">Есть еще одно свойство JSON, additionalLinkedServiceNames, где можно указать дополнительные учетные записи хранения в HDInsight по запросу.</span><span class="sxs-lookup"><span data-stu-id="38f4c-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="38f4c-153">Эти дополнительные связанные учетные записи хранения должно быть в hello местоположения кластера HDInsight hello, или она завершается ошибкой с hello же ошибка.</span><span class="sxs-lookup"><span data-stu-id="38f4c-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="38f4c-154">Проблема: сбой настраиваемого действия .NET</span><span class="sxs-lookup"><span data-stu-id="38f4c-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="38f4c-155">Подробные действия см. в разделе [Отладка конвейера с помощью настраиваемого действия](data-factory-use-custom-activities.md#troubleshoot-failures).</span><span class="sxs-lookup"><span data-stu-id="38f4c-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="38f4c-156">Использование Azure tootroubleshoot портала</span><span class="sxs-lookup"><span data-stu-id="38f4c-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="38f4c-157">Использование колонок на портале</span><span class="sxs-lookup"><span data-stu-id="38f4c-157">Using portal blades</span></span>
<span data-ttu-id="38f4c-158">Действия см. в статье [Мониторинг конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="38f4c-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="38f4c-159">Использование приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="38f4c-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="38f4c-160">Сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="38f4c-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="38f4c-161">Использовать tootroubleshoot Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="38f4c-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="38f4c-162">Использование Azure PowerShell tootroubleshoot ошибку</span><span class="sxs-lookup"><span data-stu-id="38f4c-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="38f4c-163">Сведения см. в разделе [Мониторинг конвейеров фабрики данных с помощью Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="38f4c-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
