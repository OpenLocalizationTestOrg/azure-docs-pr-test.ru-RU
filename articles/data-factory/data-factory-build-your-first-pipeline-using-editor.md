---
title: "aaaBuild первый фабрики данных (портал Azure) | Документы Microsoft"
description: "В этом учебнике создается пример конвейера фабрики данных Azure, используя редактор фабрики данных в hello портал Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="df5b8-103">Руководство. Создание первой фабрики данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="df5b8-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df5b8-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df5b8-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="df5b8-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="df5b8-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="df5b8-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df5b8-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="df5b8-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df5b8-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="df5b8-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="df5b8-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="df5b8-109">REST API</span><span class="sxs-lookup"><span data-stu-id="df5b8-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="df5b8-110">В этой статье вы узнаете, как toouse [портал Azure](https://portal.azure.com/) toocreate первый фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="df5b8-111">toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="df5b8-112">конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="df5b8-113">Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="df5b8-114">Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="df5b8-115">конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="df5b8-116">Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5b8-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="df5b8-117">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="df5b8-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="df5b8-118">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="df5b8-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="df5b8-119">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="df5b8-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df5b8-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df5b8-120">Prerequisites</span></span>
1. <span data-ttu-id="df5b8-121">Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="df5b8-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="df5b8-122">Данная статья содержит общие сведения о hello служба фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="df5b8-123">Рекомендуется изучить [tooAzure введение фабрики данных](data-factory-introduction.md) статье подробный обзор службы hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="df5b8-124">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="df5b8-124">Create data factory</span></span>
<span data-ttu-id="df5b8-125">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="df5b8-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="df5b8-126">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="df5b8-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="df5b8-127">Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="df5b8-128">Давайте начнем с создания фабрики данных hello на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="df5b8-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="df5b8-129">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="df5b8-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="df5b8-130">Нажмите кнопку **NEW** hello левого меню **данные + аналитика**и нажмите кнопку **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Колонка "Создание"](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="df5b8-132">В hello **новую фабрику данных** колонке введите **GetStartedDF** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="df5b8-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Создать колонку "Фабрика данных"](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="df5b8-134">Имя фабрики данных Azure hello Hello должно быть **глобальный уникальный**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="df5b8-135">Если ошибка hello: **имя фабрики данных «GetStartedDF» недоступен**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="df5b8-136">Измените имя hello фабрики данных hello (например, yournameGetStartedDF) и повторите попытку создания.</span><span class="sxs-lookup"><span data-stu-id="df5b8-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="df5b8-137">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="df5b8-138">Имя фабрики данных hello Hello может быть зарегистрирован как **DNS** имя в будущем hello и поэтому становятся общедоступен.</span><span class="sxs-lookup"><span data-stu-id="df5b8-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="df5b8-139">Выберите hello **подписки Azure** место hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="df5b8-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="df5b8-140">Выберите имеющуюся **группу ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="df5b8-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="df5b8-141">Hello учебник, создать группу ресурсов с именем: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="df5b8-142">Выберите hello **расположение** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="df5b8-143">В раскрывающемся списке hello отображаются только регионов, поддерживаемых hello служба фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="df5b8-144">Выберите **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="df5b8-145">Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="df5b8-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="df5b8-146">экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.</span><span class="sxs-lookup"><span data-stu-id="df5b8-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="df5b8-147">На панели мониторинга hello см следующие hello плитку с состоянием: развертывание фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Статус создания фабрики данных](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="df5b8-149">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="df5b8-149">Congratulations!</span></span> <span data-ttu-id="df5b8-150">Вы успешно создали свою первую фабрику данных!</span><span class="sxs-lookup"><span data-stu-id="df5b8-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="df5b8-151">После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Колонка "Фабрика данных"](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="df5b8-153">Перед созданием конвейера в фабрике данных hello, необходимо toocreate несколько сущностей фабрики данных сначала.</span><span class="sxs-lookup"><span data-stu-id="df5b8-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="df5b8-154">Необходимо сначала создать связанные службы данных toolink хранилищ и вычисляет tooyour данных хранения, определение входных данных и выходных данных ввода вывода toorepresent наборов данных в хранилищах данных связанного и затем создать конвейер hello с действие, которое использует эти наборы данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="df5b8-155">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="df5b8-155">Create linked services</span></span>
<span data-ttu-id="df5b8-156">На этом шаге связать учетную запись хранилища Azure и фабрикой данных кластера tooyour для Azure HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="df5b8-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="df5b8-157">содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="df5b8-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="df5b8-158">Hello связанной службы HDInsight — используется toorun скрипт Hive, указанное в действии hello конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="df5b8-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="df5b8-159">Определить, что [хранилище данных](data-factory-data-movement-activities.md)/[службы вычислений](data-factory-compute-linked-services.md) используются в сценарий и связать эти фабрики служб toohello данных путем создания связанных служб.</span><span class="sxs-lookup"><span data-stu-id="df5b8-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="df5b8-160">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="df5b8-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="df5b8-161">На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="df5b8-162">В этом учебнике используется hello Azure учетную запись хранения toostore ввода вывода данных и hello HQL файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="df5b8-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="df5b8-163">Нажмите кнопку **автор и развернуть** на hello **ФАБРИКИ данных** колонке **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="df5b8-164">Вы увидите hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-164">You should see hello Data Factory Editor.</span></span>

   ![Плитка "Создание и развертывание"](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="df5b8-166">Щелкните **Новое хранилище данных** и выберите пункт **Служба хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-166">Click **New data store** and choose **Azure storage**.</span></span>

   !["Новое хранилище данных" — пункт меню "Служба хранилища Azure"](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="df5b8-168">Вы увидите hello скрипта JSON для создания хранилища Azure связанная служба в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="df5b8-170">Замените **имя учетной записи** с именем hello вашей учетной записи хранилища Azure и **ключ учетной записи** с ключом доступа hello hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="df5b8-171">toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="df5b8-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="df5b8-172">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="df5b8-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Кнопка «Развернуть»](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="df5b8-174">Здравствуйте, после hello связанная служба успешно развернут, **Draft 1** окна должна исчезнуть, и вы увидите **AzureStorageLinkedService** в древовидном представлении hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Связанная служба хранилища в меню](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="df5b8-176">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="df5b8-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="df5b8-177">На этом шаге связать фабрикой данных кластера tooyour для HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="df5b8-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="df5b8-178">кластер HDInsight Hello автоматически создается во время выполнения и удалена после завершения обработки и время простоя для hello указанного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="df5b8-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="df5b8-179">В hello **редактор фабрики данных**, нажмите кнопку **... Еще**, щелкните **Новое вычисление** и выберите **On-demand HDInsight cluster** (Кластер HDInsight по требованию).</span><span class="sxs-lookup"><span data-stu-id="df5b8-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Новая служба вычислений](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="df5b8-181">Скопируйте и вставьте следующий фрагмент кода toohello hello **Draft 1** окна.</span><span class="sxs-lookup"><span data-stu-id="df5b8-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="df5b8-182">фрагмент кода Hello JSON описаны свойства hello hello используется toocreate HDInsight кластера по требованию.</span><span class="sxs-lookup"><span data-stu-id="df5b8-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="df5b8-183">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="df5b8-184">Свойство</span><span class="sxs-lookup"><span data-stu-id="df5b8-184">Property</span></span> | <span data-ttu-id="df5b8-185">Описание</span><span class="sxs-lookup"><span data-stu-id="df5b8-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="df5b8-186">ClusterSize (размер кластера)</span><span class="sxs-lookup"><span data-stu-id="df5b8-186">ClusterSize</span></span> |<span data-ttu-id="df5b8-187">Указывает размер кластера HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="df5b8-188">TimeToLive (срок жизни)</span><span class="sxs-lookup"><span data-stu-id="df5b8-188">TimeToLive</span></span> | <span data-ttu-id="df5b8-189">Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="df5b8-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="df5b8-190">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="df5b8-190">linkedServiceName</span></span> | <span data-ttu-id="df5b8-191">Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df5b8-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="df5b8-192">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="df5b8-192">Note hello following points:</span></span>

   * <span data-ttu-id="df5b8-193">Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello JSON.</span><span class="sxs-lookup"><span data-stu-id="df5b8-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="df5b8-194">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="df5b8-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="df5b8-195">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="df5b8-196">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="df5b8-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="df5b8-197">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="df5b8-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="df5b8-198">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="df5b8-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="df5b8-199">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="df5b8-199">This behavior is by design.</span></span> <span data-ttu-id="df5b8-200">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="df5b8-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="df5b8-201">Hello кластера автоматически удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="df5b8-202">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="df5b8-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="df5b8-203">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="df5b8-204">имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp».</span><span class="sxs-lookup"><span data-stu-id="df5b8-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="df5b8-205">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="df5b8-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="df5b8-206">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="df5b8-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="df5b8-207">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="df5b8-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Развертывание связанной службы HDInsight по запросу](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="df5b8-209">Подтвердите, что вы видите оба **AzureStorageLinkedService** и **HDInsightOnDemandLinkedService** в древовидном представлении hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Иерархическое представление со связанными службами](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="df5b8-211">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="df5b8-211">Create datasets</span></span>
<span data-ttu-id="df5b8-212">На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive.</span><span class="sxs-lookup"><span data-stu-id="df5b8-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="df5b8-213">Эти наборы данных ссылаются toohello **AzureStorageLinkedService** вы создали ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="df5b8-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="df5b8-214">Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="df5b8-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="df5b8-215">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="df5b8-215">Create input dataset</span></span>
1. <span data-ttu-id="df5b8-216">В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**и выберите **хранилища больших двоичных объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Новый набор данных](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="df5b8-218">Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="df5b8-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="df5b8-219">В фрагменте кода JSON hello, создается набор данных с именем **AzureBlobInput** , представляющий входные данные для действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="df5b8-220">Кроме того, укажите, hello входных данных находится в контейнере hello BLOB-объекта с именем **adfgetstarted** и hello папку с именем **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="df5b8-221">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="df5b8-222">Свойство</span><span class="sxs-lookup"><span data-stu-id="df5b8-222">Property</span></span> | <span data-ttu-id="df5b8-223">Описание</span><span class="sxs-lookup"><span data-stu-id="df5b8-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="df5b8-224">type</span><span class="sxs-lookup"><span data-stu-id="df5b8-224">type</span></span> |<span data-ttu-id="df5b8-225">Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="df5b8-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="df5b8-226">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="df5b8-226">linkedServiceName</span></span> |<span data-ttu-id="df5b8-227">Указывает toohello **AzureStorageLinkedService** было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="df5b8-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="df5b8-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="df5b8-228">folderPath</span></span> | <span data-ttu-id="df5b8-229">Указывает hello blob **контейнера** и hello **папки** , содержащий входного BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="df5b8-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="df5b8-230">fileName</span><span class="sxs-lookup"><span data-stu-id="df5b8-230">fileName</span></span> |<span data-ttu-id="df5b8-231">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="df5b8-231">This property is optional.</span></span> <span data-ttu-id="df5b8-232">Если это свойство не указан, извлекаются все файлы hello из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="df5b8-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="df5b8-233">В этом учебнике только hello **input.log** обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="df5b8-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="df5b8-234">type</span><span class="sxs-lookup"><span data-stu-id="df5b8-234">type</span></span> |<span data-ttu-id="df5b8-235">файлы журнала Hello находятся в текстовом формате, поэтому мы используем **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="df5b8-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="df5b8-236">columnDelimiter</span></span> |<span data-ttu-id="df5b8-237">столбцы в файлах журнала hello разделяются **запятая (`,`)**</span><span class="sxs-lookup"><span data-stu-id="df5b8-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="df5b8-238">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="df5b8-238">frequency/interval</span></span> |<span data-ttu-id="df5b8-239">частота слишком значение**месяц** и интервал — **1**, это означает, что hello ввода фрагменты доступны ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="df5b8-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="df5b8-240">external</span><span class="sxs-lookup"><span data-stu-id="df5b8-240">external</span></span> | <span data-ttu-id="df5b8-241">Это свойство задано слишком**true** Если hello входных данных в этом конвейере не создается.</span><span class="sxs-lookup"><span data-stu-id="df5b8-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="df5b8-242">В этом учебнике файл input.log hello не создан в этом конвейере, задается свойство tootrue hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="df5b8-243">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="df5b8-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="df5b8-244">Нажмите кнопку **развернуть** на панели набора данных только что созданный hello toodeploy hello команд.</span><span class="sxs-lookup"><span data-stu-id="df5b8-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="df5b8-245">Вы увидите hello набора данных в древовидном представлении hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="df5b8-246">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="df5b8-246">Create output dataset</span></span>
<span data-ttu-id="df5b8-247">Теперь создание выходных данных hello выходной набор данных toorepresent hello данные, хранящиеся в hello хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="df5b8-248">В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**и выберите **хранилища больших двоичных объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="df5b8-249">Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="df5b8-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="df5b8-250">В фрагменте кода JSON hello, создается набор данных с именем **AzureBlobOutput**и указав hello структуры данных hello, произведенное hello скрипт Hive.</span><span class="sxs-lookup"><span data-stu-id="df5b8-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="df5b8-251">Кроме того, укажите, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfgetstarted** и hello папку с именем **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="df5b8-252">Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе.</span><span class="sxs-lookup"><span data-stu-id="df5b8-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="df5b8-253">В разделе **Создание входного набора данных hello** раздел для описания этих свойств.</span><span class="sxs-lookup"><span data-stu-id="df5b8-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="df5b8-254">Не задано внешних свойств hello в выходной набор данных как hello набора данных создается службой фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="df5b8-255">Нажмите кнопку **развернуть** на панели набора данных только что созданный hello toodeploy hello команд.</span><span class="sxs-lookup"><span data-stu-id="df5b8-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="df5b8-256">Убедитесь, что этот набор данных hello создан успешно.</span><span class="sxs-lookup"><span data-stu-id="df5b8-256">Verify that hello dataset is created successfully.</span></span>

    ![Иерархическое представление со связанными службами](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="df5b8-258">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="df5b8-258">Create pipeline</span></span>
<span data-ttu-id="df5b8-259">На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="df5b8-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="df5b8-260">Входной фрагмент доступен ежемесячно (частота: месяц, интервал: 1), выходные данные срезов ежемесячно и toomonthly также установлено свойство планировщика hello для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="df5b8-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="df5b8-261">Параметры Hello для hello выходной набор данных и планировщик действие hello должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="df5b8-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="df5b8-262">В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="df5b8-263">Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="df5b8-264">в конце hello в этом разделе объясняются Hello свойств, используемых в hello следующий JSON.</span><span class="sxs-lookup"><span data-stu-id="df5b8-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="df5b8-265">В hello **редактор фабрики данных**, щелкните **кнопку с многоточием (...) Дополнительные команды** и нажмите кнопку **новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Кнопка "Создать конвейер"](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="df5b8-267">Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="df5b8-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="df5b8-268">Замените **storageaccountname** с именем hello вашей учетной записи хранилища в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="df5b8-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    <span data-ttu-id="df5b8-269">Фрагмент кода hello JSON вы создаете конвейера, который состоит из одного действия, которое использует куст tooprocess данных в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df5b8-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="df5b8-270">файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **AzureStorageLinkedService**) и в  **сценарий** папки в контейнере hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="df5b8-271">Hello **определяет** раздел представляет параметры среды выполнения используется toospecify hello, переданных toohello скрипт hive в качестве значения конфигурации Hive (например ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="df5b8-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="df5b8-272">Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="df5b8-273">В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="df5b8-274">В разделе «Конвейера JSON» в [конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md) подробные сведения о свойствах JSON, используемый в примере hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="df5b8-275">Подтверждение hello следующее:</span><span class="sxs-lookup"><span data-stu-id="df5b8-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="df5b8-276">**Input.log** файл существует в hello **inputdata** папки hello **adfgetstarted** контейнера в хранилище больших двоичных объектов hello</span><span class="sxs-lookup"><span data-stu-id="df5b8-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="df5b8-277">**partitionweblogs.hql** файл существует в hello **сценарий** папки hello **adfgetstarted** контейнера в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="df5b8-278">Необходимое условие завершения hello шагов в hello [Обзор учебника](data-factory-build-your-first-pipeline.md) Если вы не видите эти файлы.</span><span class="sxs-lookup"><span data-stu-id="df5b8-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="df5b8-279">Убедитесь, что Вы заменили **storageaccountname** с именем hello вашей учетной записи хранилища в hello конвейера JSON.</span><span class="sxs-lookup"><span data-stu-id="df5b8-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="df5b8-280">Нажмите кнопку **развернуть** на панели toodeploy hello конвейера hello команд.</span><span class="sxs-lookup"><span data-stu-id="df5b8-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="df5b8-281">С момента hello **запустить** и **окончания** время установлено в прошлом hello и **isPaused** работает toofalse набор, конвейер hello (действие в конвейере hello) сразу же после развертывания.</span><span class="sxs-lookup"><span data-stu-id="df5b8-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="df5b8-282">Подтвердите, что вы видите hello конвейера в представлении дерева hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Иерархическое представление с конвейером](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="df5b8-284">Поздравляем! Вы создали свой первый конвейер!</span><span class="sxs-lookup"><span data-stu-id="df5b8-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="df5b8-285">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="df5b8-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="df5b8-286">Мониторинг конвейера с использованием представления схемы</span><span class="sxs-lookup"><span data-stu-id="df5b8-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="df5b8-287">Нажмите кнопку **X** tooclose редактор фабрики данных колонках toonavigate резервное колонке toohello фабрики данных и нажмите кнопку **схема**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Плитка "Схема"](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="df5b8-289">В hello представление диаграммы отображаются общие сведения о конвейерах hello и наборы данных, используемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="df5b8-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Представление схемы](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="df5b8-291">tooview все действия в конвейере hello, щелкните правой кнопкой мыши конвейера в hello схемы и нажмите кнопку Открыть конвейера.</span><span class="sxs-lookup"><span data-stu-id="df5b8-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Откройте меню конвейера](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="df5b8-293">Убедитесь, что это действие HDInsightHive hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Откройте представление конвейера](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="df5b8-295">toonavigate резервное toohello предыдущего представления, нажмите кнопку **фабрики данных** в меню навигации hello верхней hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="df5b8-296">В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="df5b8-297">Убедитесь, что срез hello в **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="df5b8-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="df5b8-298">Он может занять несколько минут для tooshow срез hello в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="df5b8-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="df5b8-299">Если не происходят через некоторое время, убедитесь, что hello входного файла (input.log) помещаются в нужных контейнерах hello (adfgetstarted) и папки (inputdata).</span><span class="sxs-lookup"><span data-stu-id="df5b8-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Срез входных данных в состоянии "Готово"](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="df5b8-301">Нажмите кнопку **X** tooclose **AzureBlobInput** колонку.</span><span class="sxs-lookup"><span data-stu-id="df5b8-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="df5b8-302">В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="df5b8-303">Вы увидите, что hello срез, который обрабатывается в данный момент.</span><span class="sxs-lookup"><span data-stu-id="df5b8-303">You see that hello slice that is currently being processed.</span></span>

   ![Выборка](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="df5b8-305">После завершения обработки отображается срез hello в **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="df5b8-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Выборка](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="df5b8-307">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="df5b8-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="df5b8-308">Таким образом, ожидать конвейера hello занять слишком **около 30 минут** tooprocess hello среза.</span><span class="sxs-lookup"><span data-stu-id="df5b8-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="df5b8-309">Если срез hello находится в **готовности** состоянии, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![выходные данные](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="df5b8-311">Нажмите кнопку hello срез toosee сведения о нем на **срез данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="df5b8-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Сведения о срезе данных](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="df5b8-313">Щелкните действие в hello **действие выполняется список** toosee сведения о действиях (Hive действие выполнения в нашем сценарии) **сведения о выполнении действия** окна.</span><span class="sxs-lookup"><span data-stu-id="df5b8-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="df5b8-315">Из файлов журнала hello вы увидите выполненного запроса Hive hello и сведения о состоянии.</span><span class="sxs-lookup"><span data-stu-id="df5b8-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="df5b8-316">Эти журналы полезны при устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="df5b8-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="df5b8-317">Дополнительные сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="df5b8-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df5b8-318">входной файл Hello, удаляется при успешно обработал hello среза.</span><span class="sxs-lookup"><span data-stu-id="df5b8-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="df5b8-319">Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.</span><span class="sxs-lookup"><span data-stu-id="df5b8-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="df5b8-320">Мониторинг конвейера с использованием приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="df5b8-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="df5b8-321">Вы можете использовать монитор и управлять конвейеры toomonitor приложения.</span><span class="sxs-lookup"><span data-stu-id="df5b8-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="df5b8-322">Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="df5b8-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="df5b8-323">Нажмите кнопку **отслеживать состо & Управление** плитки на домашней странице приветствия для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Плитка Monitor & Manage (Мониторинг и управление)](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="df5b8-325">Вы должны увидеть **приложение по мониторингу и управлению**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="df5b8-326">Изменение hello **время начала** и **время окончания** toomatch запуск и завершение работы конвейера и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![Приложение по мониторингу и управлению](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="df5b8-328">Выберите окно действия в hello **действия Windows** списка toosee сведения о ней.</span><span class="sxs-lookup"><span data-stu-id="df5b8-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Сведения об окне действия](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="df5b8-330">Сводка</span><span class="sxs-lookup"><span data-stu-id="df5b8-330">Summary</span></span>
<span data-ttu-id="df5b8-331">В этом учебнике вы создали данных tooprocess фабрики данных Azure, выполнив скрипт Hive в кластере HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="df5b8-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="df5b8-332">Вы использовали hello редактор фабрики данных в Azure портала toodo hello hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="df5b8-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="df5b8-333">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="df5b8-334">создание двух **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="df5b8-335">**Хранилище Azure** связанные toolink службы хранилища больших двоичных объектов Azure, содержащий фабрики данных toohello ввода вывода файлов.</span><span class="sxs-lookup"><span data-stu-id="df5b8-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="df5b8-336">**Azure HDInsight** связанная служба toolink по требованию фабрикой по требованию toohello кластера HDInsight Hadoop данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="df5b8-337">Фабрика данных Azure создает HDInsight Hadoop кластера tooprocess just-in-time входных данных и создают выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df5b8-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="df5b8-338">Создать два **наборы данных**, которые описывают входных и выходных данных для действие Hive в HDInsight из конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="df5b8-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="df5b8-339">Создание **конвейера** с действием **HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="df5b8-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df5b8-340">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df5b8-340">Next Steps</span></span>
<span data-ttu-id="df5b8-341">В этой статье вы создали конвейер с действием преобразования (действие HDInsight), которое выполняет сценарий Hive в кластере HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="df5b8-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="df5b8-342">toosee toouse toocopy действие копирования данных из больших двоичных объектов Azure tooAzure SQL, в статье [учебника: копирование данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="df5b8-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="df5b8-343">См. также</span><span class="sxs-lookup"><span data-stu-id="df5b8-343">See Also</span></span>
| <span data-ttu-id="df5b8-344">Раздел</span><span class="sxs-lookup"><span data-stu-id="df5b8-344">Topic</span></span> | <span data-ttu-id="df5b8-345">Описание</span><span class="sxs-lookup"><span data-stu-id="df5b8-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="df5b8-346">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="df5b8-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="df5b8-347">Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="df5b8-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="df5b8-348">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="df5b8-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="df5b8-349">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="df5b8-350">Планирование и исполнение с использованием фабрики данных</span><span class="sxs-lookup"><span data-stu-id="df5b8-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="df5b8-351">В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="df5b8-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="df5b8-352">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="df5b8-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="df5b8-353">В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="df5b8-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
