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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="b025c-103">Руководство. Создание первой фабрики данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b025c-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b025c-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b025c-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="b025c-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b025c-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="b025c-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b025c-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="b025c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b025c-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="b025c-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b025c-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="b025c-109">REST API</span><span class="sxs-lookup"><span data-stu-id="b025c-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="b025c-110">В этой статье используется Azure PowerShell toocreate первый фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="b025c-111">toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="b025c-112">конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b025c-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="b025c-113">Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="b025c-114">Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="b025c-115">конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="b025c-116">Копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="b025c-117">Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b025c-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="b025c-118">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="b025c-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b025c-119">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="b025c-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="b025c-120">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b025c-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b025c-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b025c-121">Prerequisites</span></span>
* <span data-ttu-id="b025c-122">Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="b025c-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="b025c-123">Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи tooinstall последнюю версию Azure PowerShell на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b025c-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="b025c-124">(необязательно) Данная статья не охватывает все командлеты фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="b025c-125">Полную документацию по командлетам фабрики данных см. в [этом справочнике](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="b025c-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="b025c-126">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="b025c-126">Create data factory</span></span>
<span data-ttu-id="b025c-127">На этом шаге используется Azure PowerShell toocreate фабрикой данных Azure с именем **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="b025c-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="b025c-128">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="b025c-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b025c-129">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="b025c-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b025c-130">Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входные данные.</span><span class="sxs-lookup"><span data-stu-id="b025c-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="b025c-131">Давайте начнем с создания фабрики данных hello на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="b025c-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="b025c-132">Запустите Azure PowerShell и выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="b025c-133">Не закрывайте Azure PowerShell до завершения этого учебника hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="b025c-134">Если закрыть и снова открыть понадобятся toorun этих команд.</span><span class="sxs-lookup"><span data-stu-id="b025c-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="b025c-135">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="b025c-136">Запустите следующие команды tooview hello все hello подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b025c-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="b025c-137">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="b025c-138">Эта подписка должна hello равна hello, который используется в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="b025c-139">Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b025c-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="b025c-140">Некоторые шаги hello в этом учебнике предполагается использовать ADFTutorialResourceGroup с именем группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="b025c-141">Если вы используете другой группе ресурсов, необходимо toouse его вместо ADFTutorialResourceGroup в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b025c-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="b025c-142">Запустите hello **New AzureRmDataFactory** командлет, который создает фабрики данных с именем **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="b025c-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="b025c-143">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="b025c-143">Note hello following points:</span></span>

* <span data-ttu-id="b025c-144">Имя Hello hello фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="b025c-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="b025c-145">Если ошибка hello **имя фабрики данных «FirstDataFactoryPSH» недоступен**, измените имя hello (например, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="b025c-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="b025c-146">Используйте это имя вместо ADFTutorialFactoryPSH при выполнении шагов в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b025c-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="b025c-147">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="b025c-148">экземпляры toocreate фабрики данных, необходимо toobe участника или администратор hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="b025c-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="b025c-149">Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.</span><span class="sxs-lookup"><span data-stu-id="b025c-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="b025c-150">Если ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**», выполните одно из следующих hello и повторите попытку публикации:</span><span class="sxs-lookup"><span data-stu-id="b025c-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="b025c-151">В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика.</span><span class="sxs-lookup"><span data-stu-id="b025c-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="b025c-152">Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="b025c-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="b025c-153">Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="b025c-154">Это действие автоматически регистрирует поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="b025c-155">Перед созданием конвейера, необходимо toocreate несколько сущностей фабрики данных сначала.</span><span class="sxs-lookup"><span data-stu-id="b025c-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="b025c-156">Необходимо сначала создать связанные службы данных toolink хранилищ и вычисляет tooyour данных хранения, определение входных данных и выходных данных ввода вывода toorepresent наборов данных в хранилищах данных связанного и затем создать конвейер hello с действие, которое использует эти наборы данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="b025c-157">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="b025c-157">Create linked services</span></span>
<span data-ttu-id="b025c-158">На этом шаге связать учетную запись хранилища Azure и фабрикой данных кластера tooyour для Azure HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="b025c-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="b025c-159">содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="b025c-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="b025c-160">Hello связанной службы HDInsight — используется toorun скрипт Hive, указанное в действии hello конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="b025c-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="b025c-161">Определите, какие данные хранилища и вычислений служб используются в сценарий и связать эти фабрики служб toohello данных путем создания связанных служб.</span><span class="sxs-lookup"><span data-stu-id="b025c-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="b025c-162">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="b025c-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="b025c-163">На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="b025c-164">Использовать hello Azure учетную запись хранения toostore ввода вывода данных и hello HQL файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="b025c-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="b025c-165">Создайте JSON-файл с именем StorageLinkedService.json в папке C:\ADFGetStarted hello и hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="b025c-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="b025c-166">Создайте папку hello ADFGetStarted, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="b025c-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="b025c-167">Замените **имя учетной записи** с именем hello вашей учетной записи хранилища Azure и **ключ учетной записи** с ключом доступа hello hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="b025c-168">toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b025c-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="b025c-169">В Azure PowerShell переключение toohello ADFGetStarted папки.</span><span class="sxs-lookup"><span data-stu-id="b025c-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="b025c-170">Можно использовать hello **New AzureRmDataFactoryLinkedService** командлете, создающем связанной службы.</span><span class="sxs-lookup"><span data-stu-id="b025c-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="b025c-171">Этот командлет, а другие командлеты фабрики данных, используемый в этом учебнике требуется toopass значения для hello *ResourceGroupName* и *с именем DataFactoryName* параметров.</span><span class="sxs-lookup"><span data-stu-id="b025c-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="b025c-172">Кроме того, можно использовать **Get AzureRmDataFactory** tooget **DataFactory** и передать hello объекта, не вводя *ResourceGroupName* и  *С именем DataFactoryName* при каждом выполнении командлета.</span><span class="sxs-lookup"><span data-stu-id="b025c-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="b025c-173">Выполнения hello следующая команда tooassign hello выходные данные hello **Get AzureRmDataFactory** tooa командлет **$df** переменной.</span><span class="sxs-lookup"><span data-stu-id="b025c-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="b025c-174">Теперь запустите hello **New AzureRmDataFactoryLinkedService** командлете, создающем hello связаны **StorageLinkedService** службы.</span><span class="sxs-lookup"><span data-stu-id="b025c-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="b025c-175">Если еще не запущены hello **Get AzureRmDataFactory** командлета и назначенный hello выход toohello **$df** переменных, будет иметь значения toospecify для hello *ResourceGroupName*и *с именем DataFactoryName* параметры следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b025c-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="b025c-176">Если вы закроете Azure PowerShell в середине hello учебника hello, у вас есть toorun hello **Get AzureRmDataFactory** командлета при следующей загрузке учебника hello toocomplete Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b025c-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="b025c-177">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b025c-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="b025c-178">На этом шаге связать фабрикой данных кластера tooyour для HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="b025c-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="b025c-179">кластер HDInsight Hello автоматически создается во время выполнения и удалена после завершения обработки и время простоя для hello указанного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="b025c-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="b025c-180">Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b025c-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b025c-181">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="b025c-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="b025c-182">Создайте JSON-файл с именем **HDInsightOnDemandLinkedService**.json в hello **C:\ADFGetStarted** папка с hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="b025c-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
    <span data-ttu-id="b025c-183">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="b025c-184">Свойство</span><span class="sxs-lookup"><span data-stu-id="b025c-184">Property</span></span> | <span data-ttu-id="b025c-185">Описание</span><span class="sxs-lookup"><span data-stu-id="b025c-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b025c-186">ClusterSize (размер кластера)</span><span class="sxs-lookup"><span data-stu-id="b025c-186">ClusterSize</span></span> |<span data-ttu-id="b025c-187">Указывает размер кластера HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="b025c-188">TimeToLive (срок жизни)</span><span class="sxs-lookup"><span data-stu-id="b025c-188">TimeToLive</span></span> |<span data-ttu-id="b025c-189">Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="b025c-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="b025c-190">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="b025c-190">linkedServiceName</span></span> |<span data-ttu-id="b025c-191">Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные HDInsight</span><span class="sxs-lookup"><span data-stu-id="b025c-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="b025c-192">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="b025c-192">Note hello following points:</span></span>

   * <span data-ttu-id="b025c-193">Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello JSON.</span><span class="sxs-lookup"><span data-stu-id="b025c-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="b025c-194">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b025c-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="b025c-195">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b025c-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b025c-196">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b025c-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="b025c-197">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="b025c-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="b025c-198">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="b025c-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="b025c-199">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="b025c-199">This behavior is by design.</span></span> <span data-ttu-id="b025c-200">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="b025c-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="b025c-201">Hello кластера автоматически удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="b025c-202">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="b025c-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="b025c-203">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="b025c-204">имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp».</span><span class="sxs-lookup"><span data-stu-id="b025c-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="b025c-205">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b025c-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="b025c-206">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b025c-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="b025c-207">Запустите hello **New AzureRmDataFactoryLinkedService** командлете, создающем hello связанной службы с именем HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="b025c-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="b025c-208">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="b025c-208">Create datasets</span></span>
<span data-ttu-id="b025c-209">На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive.</span><span class="sxs-lookup"><span data-stu-id="b025c-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="b025c-210">Эти наборы данных ссылаются toohello **StorageLinkedService** вы создали ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b025c-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="b025c-211">Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="b025c-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="b025c-212">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="b025c-212">Create input dataset</span></span>
1. <span data-ttu-id="b025c-213">Создайте JSON-файл с именем **InputTable.json** в hello **C:\ADFGetStarted** папка с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="b025c-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="b025c-214">Hello JSON определяет набор данных с именем **AzureBlobInput**, который представляет входные данные для действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="b025c-215">Кроме того, он указывает, hello входных данных находится в контейнере hello BLOB-объекта с именем **adfgetstarted** и hello папку с именем **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="b025c-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="b025c-216">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="b025c-217">Свойство</span><span class="sxs-lookup"><span data-stu-id="b025c-217">Property</span></span> | <span data-ttu-id="b025c-218">Описание</span><span class="sxs-lookup"><span data-stu-id="b025c-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b025c-219">type</span><span class="sxs-lookup"><span data-stu-id="b025c-219">type</span></span> |<span data-ttu-id="b025c-220">Hello свойство type имеет значение tooAzureBlob, так как данные находятся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b025c-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="b025c-221">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="b025c-221">linkedServiceName</span></span> |<span data-ttu-id="b025c-222">ссылается toohello StorageLinkedService, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="b025c-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="b025c-223">fileName</span><span class="sxs-lookup"><span data-stu-id="b025c-223">fileName</span></span> |<span data-ttu-id="b025c-224">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="b025c-224">This property is optional.</span></span> <span data-ttu-id="b025c-225">Если это свойство не указан, извлекаются все файлы hello из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="b025c-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="b025c-226">В этом случае обрабатывается только input.log hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="b025c-227">type</span><span class="sxs-lookup"><span data-stu-id="b025c-227">type</span></span> |<span data-ttu-id="b025c-228">файлы журнала Hello находятся в текстовом формате, поэтому мы используем TextFormat.</span><span class="sxs-lookup"><span data-stu-id="b025c-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="b025c-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="b025c-229">columnDelimiter</span></span> |<span data-ttu-id="b025c-230">столбцы в файлах журнала hello разделяются hello запятая (,).</span><span class="sxs-lookup"><span data-stu-id="b025c-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="b025c-231">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="b025c-231">frequency/interval</span></span> |<span data-ttu-id="b025c-232">tooMonth задать частоту и интервал равен 1, это означает, что входные срезы hello доступны ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="b025c-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="b025c-233">external</span><span class="sxs-lookup"><span data-stu-id="b025c-233">external</span></span> |<span data-ttu-id="b025c-234">Это свойство имеет значение tootrue, если входные данные hello не создается службой фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="b025c-235">Выполните следующую команду в hello фабрики данных Azure PowerShell toocreate dataset hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="b025c-236">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="b025c-236">Create output dataset</span></span>
<span data-ttu-id="b025c-237">Теперь создание выходных данных hello выходной набор данных toorepresent hello данные, хранящиеся в hello хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="b025c-238">Создайте JSON-файл с именем **OutputTable.json** в hello **C:\ADFGetStarted** папка с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="b025c-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="b025c-239">Hello JSON определяет набор данных с именем **AzureBlobOutput**, который представляет выходные данные для действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="b025c-240">Кроме того, он указывает, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfgetstarted** и hello папку с именем **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="b025c-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="b025c-241">Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе.</span><span class="sxs-lookup"><span data-stu-id="b025c-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="b025c-242">Выполните следующую команду в hello фабрики данных Azure PowerShell toocreate dataset hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="b025c-243">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="b025c-243">Create pipeline</span></span>
<span data-ttu-id="b025c-244">На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="b025c-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="b025c-245">Входной фрагмент доступен ежемесячно (частота: месяц, интервал: 1), выходные данные срезов ежемесячно и toomonthly также установлено свойство планировщика hello для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="b025c-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="b025c-246">Параметры Hello для hello выходной набор данных и планировщик действие hello должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="b025c-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="b025c-247">В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="b025c-248">Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="b025c-249">в конце hello в этом разделе объясняются Hello свойств, используемых в hello следующий JSON.</span><span class="sxs-lookup"><span data-stu-id="b025c-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="b025c-250">Создайте JSON-файл с именем MyFirstPipelinePSH.json в папке C:\ADFGetStarted hello и hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="b025c-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b025c-251">Замените **storageaccountname** с именем hello вашей учетной записи хранилища в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="b025c-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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
    <span data-ttu-id="b025c-252">Фрагмент кода hello JSON вы создаете конвейера, который состоит из одного действия, которое использует куст tooprocess данных в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b025c-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="b025c-253">файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **StorageLinkedService**) и в **сценария**  папки в контейнере hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="b025c-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="b025c-254">Hello **определяет** раздел представляет параметры среды выполнения используется toospecify hello, быть передана toohello скрипт hive в качестве значения конфигурации Hive (например ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="b025c-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="b025c-255">Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="b025c-256">В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b025c-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b025c-257">В разделе «Конвейера JSON» в [конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md) подробные сведения о свойствах JSON, которые используются в примере hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="b025c-258">Подтвердите, что вы видите hello **input.log** файла в hello **adfgetstarted/inputdata** папку, в хранилище больших двоичных объектов hello и выполнения hello, следующая команда toodeploy hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="b025c-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="b025c-259">С момента hello **запустить** и **окончания** время установлено в прошлом hello и **isPaused** работает toofalse набор, конвейер hello (действие в конвейере hello) сразу же после развертывания.</span><span class="sxs-lookup"><span data-stu-id="b025c-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="b025c-260">Поздравляем! Вы создали свой первый конвейер с помощью Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="b025c-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="b025c-261">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="b025c-261">Monitor pipeline</span></span>
<span data-ttu-id="b025c-262">На этом шаге используется Azure PowerShell toomonitor происходящем в фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="b025c-263">Запустите **Get AzureRmDataFactory** и назначить hello вывода tooa **$df** переменной.</span><span class="sxs-lookup"><span data-stu-id="b025c-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="b025c-264">Запустите **Get AzureRmDataFactorySlice** tooget сведения о всех фрагментов hello **EmpSQLTable**, являющееся hello выходная таблица hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="b025c-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="b025c-265">Обратите внимание, что этой hello StartDateTime здесь же указано время начала в формат JSON конвейера hello hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="b025c-266">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-266">Here is hello sample output:</span></span>

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
3. <span data-ttu-id="b025c-267">Запустите **Get AzureRmDataFactoryRun** сведения hello tooget действия выполняется для определенного среза.</span><span class="sxs-lookup"><span data-stu-id="b025c-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="b025c-268">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-268">Here is hello sample output:</span></span> 

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
    <span data-ttu-id="b025c-269">Вы можно продолжать работать этот командлет, пока не увидите срез hello в **готовности** состояние или **сбой** состояния.</span><span class="sxs-lookup"><span data-stu-id="b025c-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="b025c-270">Когда hello среза находится в состоянии готовности, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="b025c-271">Создание кластера HDInsight по требованию занимает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="b025c-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![выходные данные](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="b025c-273">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="b025c-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="b025c-274">Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.</span><span class="sxs-lookup"><span data-stu-id="b025c-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="b025c-275">входной файл Hello, удаляется при успешно обработал hello среза.</span><span class="sxs-lookup"><span data-stu-id="b025c-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="b025c-276">Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.</span><span class="sxs-lookup"><span data-stu-id="b025c-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="b025c-277">Сводка</span><span class="sxs-lookup"><span data-stu-id="b025c-277">Summary</span></span>
<span data-ttu-id="b025c-278">В этом учебнике вы создали данных tooprocess фабрики данных Azure, выполнив скрипт Hive в кластере HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="b025c-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="b025c-279">Вы использовали hello редактор фабрики данных в Azure портала toodo hello hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b025c-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="b025c-280">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="b025c-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="b025c-281">создание двух **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="b025c-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="b025c-282">**Хранилище Azure** связанные toolink службы хранилища больших двоичных объектов Azure, содержащий фабрики данных toohello ввода вывода файлов.</span><span class="sxs-lookup"><span data-stu-id="b025c-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="b025c-283">**Azure HDInsight** связанная служба toolink по требованию фабрикой по требованию toohello кластера HDInsight Hadoop данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="b025c-284">Фабрика данных Azure создает HDInsight Hadoop кластера tooprocess just-in-time входных данных и создают выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="b025c-285">Создать два **наборы данных**, которые описывают входных и выходных данных для действие Hive в HDInsight из конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="b025c-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="b025c-286">Создание **конвейера** с действием **HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="b025c-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b025c-287">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b025c-287">Next steps</span></span>
<span data-ttu-id="b025c-288">В этой статье описывается создание конвейера с помощью действия преобразования (действие HDInsight), которое по требованию выполняет сценарий Hive в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b025c-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="b025c-289">toosee toouse toocopy действие копирования данных из больших двоичных объектов Azure tooAzure SQL, в статье [учебника: копирование данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b025c-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b025c-290">См. также</span><span class="sxs-lookup"><span data-stu-id="b025c-290">See Also</span></span>
| <span data-ttu-id="b025c-291">Раздел</span><span class="sxs-lookup"><span data-stu-id="b025c-291">Topic</span></span> | <span data-ttu-id="b025c-292">Описание</span><span class="sxs-lookup"><span data-stu-id="b025c-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="b025c-293">Справочник по командлетам фабрики данных</span><span class="sxs-lookup"><span data-stu-id="b025c-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="b025c-294">См. полную документацию по командлетам фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b025c-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="b025c-295">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="b025c-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="b025c-296">Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="b025c-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="b025c-297">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="b025c-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="b025c-298">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="b025c-299">Планирование и выполнение</span><span class="sxs-lookup"><span data-stu-id="b025c-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="b025c-300">В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b025c-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="b025c-301">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="b025c-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="b025c-302">В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="b025c-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
