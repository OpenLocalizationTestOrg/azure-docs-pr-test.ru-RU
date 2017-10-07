---
title: "aaaInvoke Spark программы из фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как программы Spark tooinvoke из фабрики данных Azure с помощью hello действия MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="4c270-103">Вызов программ Spark из конвейеров фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="4c270-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4c270-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="4c270-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="4c270-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="4c270-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4c270-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="4c270-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4c270-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="4c270-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4c270-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="4c270-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4c270-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="4c270-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4c270-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="4c270-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4c270-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="4c270-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4c270-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4c270-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4c270-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="4c270-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="4c270-114">Введение</span><span class="sxs-lookup"><span data-stu-id="4c270-114">Introduction</span></span>
<span data-ttu-id="4c270-115">Действие Spark является одним из hello [действия преобразования данных](data-factory-data-transformation-activities.md) поддерживаемые фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="4c270-116">Это действие выполняет указанное hello программы Spark в кластере Apache Spark в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c270-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="4c270-117">Действие Spark не поддерживает кластеры HDInsight Spark, использующие Azure Data Lake Store в качестве основного хранилища.</span><span class="sxs-lookup"><span data-stu-id="4c270-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="4c270-118">Оно поддерживает только существующие (собственные) кластеры HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="4c270-119">Связанная служба HDInsight по запросу не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4c270-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="4c270-120">Пошаговое руководство по созданию конвейера с действием Spark</span><span class="sxs-lookup"><span data-stu-id="4c270-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="4c270-121">Ниже приведены типичные шаги hello toocreate конвейера фабрики данных с действием Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="4c270-122">Создадите фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-122">Create a data factory.</span></span>
2. <span data-ttu-id="4c270-123">Создайте toolink службы хранилища Azure связанной службе хранилища Azure, связанный с вашей фабрике данных toohello кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="4c270-124">Создайте toolink Azure HDInsight связанной службы кластера Apache Spark в фабрике данных Azure HDInsight toohello.</span><span class="sxs-lookup"><span data-stu-id="4c270-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="4c270-125">Создание набора данных, который ссылается toohello связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="4c270-126">Затем определите выходной набор данных для действия, даже если выходные данные не выдаются.</span><span class="sxs-lookup"><span data-stu-id="4c270-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="4c270-127">Создайте конвейер Spark действием, которое ссылается toohello связанной службы HDInsight в #2.</span><span class="sxs-lookup"><span data-stu-id="4c270-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="4c270-128">Действие Hello настроено hello набор данных, созданный на предыдущем шаге hello как выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="4c270-129">Hello выходной набор данных является то, какие диски hello расписания (каждый час, день, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4c270-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="4c270-130">Таким образом необходимо указать hello выходной набор данных, несмотря на то, что действие hello действительно не создает выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4c270-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4c270-131">Prerequisites</span></span>
1. <span data-ttu-id="4c270-132">Создание **общего назначения учетной записи хранилища Azure** , следуя указаниям hello Пошаговое руководство: [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4c270-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="4c270-133">Создание **кластера Apache Spark в Azure HDInsight** , следуя указаниям hello учебника: [кластера создать Apache Spark в Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4c270-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="4c270-134">Свяжите учетную запись хранилища Azure hello, созданный на шаге #1 с кластером.</span><span class="sxs-lookup"><span data-stu-id="4c270-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="4c270-135">Загрузить и просмотреть файл сценария python hello **test.py** , расположенный: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="4c270-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="4c270-136">Отправка **test.py** toohello **pyFiles** папки в hello **adfspark** контейнера в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="4c270-137">Создайте контейнер hello и hello папки, если они не существуют.</span><span class="sxs-lookup"><span data-stu-id="4c270-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="4c270-138">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="4c270-138">Create data factory</span></span>
<span data-ttu-id="4c270-139">Давайте начнем с создания фабрики данных hello на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="4c270-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="4c270-140">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4c270-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4c270-141">Нажмите кнопку **NEW** hello левого меню **данные + аналитика**и нажмите кнопку **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="4c270-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="4c270-142">В hello **новую фабрику данных** колонке введите **SparkDF** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="4c270-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4c270-143">Имя фабрики данных Azure hello Hello должно быть **глобальный уникальный**.</span><span class="sxs-lookup"><span data-stu-id="4c270-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="4c270-144">При возникновении ошибки hello: **имя фабрики данных «SparkDF» недоступен**.</span><span class="sxs-lookup"><span data-stu-id="4c270-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="4c270-145">Изменение имени hello hello фабрики данных (например, yournameSparkDFdate и попробуйте еще раз.</span><span class="sxs-lookup"><span data-stu-id="4c270-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="4c270-146">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="4c270-147">Выберите hello **подписки Azure** место hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="4c270-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="4c270-148">Выберите существующую **группу ресурсов** Azure или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="4c270-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="4c270-149">Выберите **toodashboard ПИН-код** параметр.</span><span class="sxs-lookup"><span data-stu-id="4c270-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="4c270-150">Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="4c270-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4c270-151">экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.</span><span class="sxs-lookup"><span data-stu-id="4c270-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="4c270-152">Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4c270-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="4c270-153">После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="4c270-154">Если вы не видите страницу фабрики данных hello, щелкните плитку hello для фабрики данных на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Колонка "Фабрика данных"](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="4c270-156">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="4c270-156">Create linked services</span></span>
<span data-ttu-id="4c270-157">На этом шаге создания двух связанных служб, один toolink фабрики данных tooyour кластер Spark и hello других toolink фабрики данных tooyour хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4c270-158">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="4c270-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="4c270-159">На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="4c270-160">Набор данных, создаваемые вами в шаге далее в этом пошаговом руководстве относится toothis связанной службы.</span><span class="sxs-lookup"><span data-stu-id="4c270-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="4c270-161">Hello связанной службы HDInsight, определяется в следующем шаге hello слишком ссылается toothis связанной службы.</span><span class="sxs-lookup"><span data-stu-id="4c270-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="4c270-162">Нажмите кнопку **автор и развернуть** на hello **фабрики данных** колонку для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="4c270-163">Вы увидите hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="4c270-164">Щелкните **Новое хранилище данных** и выберите пункт **Служба хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="4c270-164">Click **New data store** and choose **Azure storage**.</span></span>

   !["Новое хранилище данных" — пункт меню "Служба хранилища Azure"](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="4c270-166">Вы увидите hello **скрипта JSON** для создания хранилища Azure связанная служба в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="4c270-168">Замените **имя учетной записи** и **ключ учетной записи** с hello имя и ключ доступа учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="4c270-169">toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4c270-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="4c270-170">toodeploy Здравствуйте связанной службы, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="4c270-171">Здравствуйте, после hello связанная служба успешно развернут, **Draft 1** окна должна исчезнуть, и вы увидите **AzureStorageLinkedService** в древовидном представлении hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="4c270-172">Создание связанной службы HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c270-172">Create HDInsight linked service</span></span>
<span data-ttu-id="4c270-173">На этом шаге создается toolink Azure HDInsight связанной службы фабрики данных toohello кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="4c270-174">кластер HDInsight Hello — используется toorun hello Spark программу, указанную в действие hello Spark конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="4c270-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="4c270-175">Нажмите **... Дополнительные** на панели инструментов hello, нажмите кнопку **новые вычислительные**, а затем нажмите кнопку **кластера HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4c270-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Создание связанной службы HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="4c270-177">Скопируйте и вставьте следующий фрагмент кода toohello hello **Draft 1** окна.</span><span class="sxs-lookup"><span data-stu-id="4c270-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="4c270-178">В редакторе JSON hello hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="4c270-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="4c270-179">Укажите hello **URI** hello HDInsight Spark кластера.</span><span class="sxs-lookup"><span data-stu-id="4c270-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="4c270-180">Например, `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="4c270-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="4c270-181">Укажите имя hello hello **пользователя** у кого есть кластера Spark toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="4c270-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="4c270-182">Укажите hello **пароль** для пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c270-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="4c270-183">Укажите hello **связанная служба хранилища Azure** связанное с hello кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="4c270-184">(в этом примере это **AzureStorageLinkedService**).</span><span class="sxs-lookup"><span data-stu-id="4c270-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="4c270-185">Действие Spark не поддерживает кластеры HDInsight Spark, использующие Azure Data Lake Store в качестве основного хранилища.</span><span class="sxs-lookup"><span data-stu-id="4c270-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="4c270-186">Оно поддерживает только существующие (собственные) кластеры HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="4c270-187">Связанная служба HDInsight по запросу не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4c270-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="4c270-188">В разделе [связанной службы HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) для получения сведений об hello HDInsight связанной службы.</span><span class="sxs-lookup"><span data-stu-id="4c270-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="4c270-189">toodeploy Здравствуйте связанной службы, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="4c270-190">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="4c270-190">Create output dataset</span></span>
<span data-ttu-id="4c270-191">Hello выходной набор данных является то, какие диски hello расписания (каждый час, день, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4c270-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="4c270-192">Таким образом необходимо указать выходной набор данных для действия spark hello в конвейере hello, несмотря на то, что действие hello действительно не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="4c270-193">Входной набор данных для действия "hello" указывать не обязательно.</span><span class="sxs-lookup"><span data-stu-id="4c270-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="4c270-194">В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**и выберите **хранилища больших двоичных объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="4c270-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="4c270-195">Скопируйте и вставьте hello, следуя окно фрагмента toohello Draft-1.</span><span class="sxs-lookup"><span data-stu-id="4c270-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="4c270-196">фрагмент кода Hello JSON определяет набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="4c270-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="4c270-197">Кроме того, укажите, что hello результаты сохраняются в контейнер больших двоичных объектов hello вызывается **adfspark** и hello папку с именем **pyFiles и вывода**.</span><span class="sxs-lookup"><span data-stu-id="4c270-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="4c270-198">Как упоминалось ранее, это фиктивный набор данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="4c270-199">Программа Hello Spark в этом примере не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="4c270-200">Hello **доступности** раздела указывает, что hello выходной набор данных создается ежедневно.</span><span class="sxs-lookup"><span data-stu-id="4c270-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="4c270-201">toodeploy Здравствуйте набора данных, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="4c270-202">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="4c270-202">Create pipeline</span></span>
<span data-ttu-id="4c270-203">На этом шаге создается конвейер с действием **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="4c270-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="4c270-204">В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="4c270-205">Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="4c270-206">Таким образом, в этом примере входной набор данных не указывается.</span><span class="sxs-lookup"><span data-stu-id="4c270-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="4c270-207">В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на hello панели команд и нажмите кнопку **новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="4c270-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="4c270-208">Замените сценарий hello в окне приветствия Draft 1 hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="4c270-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="4c270-209">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="4c270-209">Note hello following points:</span></span>
    - <span data-ttu-id="4c270-210">Hello **тип** задано слишком**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="4c270-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="4c270-211">Hello **rootPath** задано слишком**adfspark\\pyFiles** где adfspark — контейнер больших двоичных объектов Azure hello и pyFiles — нормально папки в этом контейнере.</span><span class="sxs-lookup"><span data-stu-id="4c270-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="4c270-212">В этом примере hello хранилища больших двоичных объектов — hello, связанная с кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="4c270-213">Вы можете отправить файл tooa hello другое хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="4c270-214">Если сделать это, создайте toolink службы хранилища Azure связаны этой фабрики данных toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4c270-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="4c270-215">Укажите имя hello hello связаны службы как значение для hello **sparkJobLinkedService** свойство.</span><span class="sxs-lookup"><span data-stu-id="4c270-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="4c270-216">В разделе [свойства действия Spark](#spark-activity-properties) подробные сведения об этом и других свойствах, поддерживаемых hello Spark действия.</span><span class="sxs-lookup"><span data-stu-id="4c270-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="4c270-217">Hello **entryFilePath** задано toohello **test.py**, который является файлом python hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="4c270-218">Hello **getDebugInfo** задано слишком**всегда**, что означает, файлы журнала hello всегда создается (успех или сбой).</span><span class="sxs-lookup"><span data-stu-id="4c270-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="4c270-219">Мы рекомендуем не задавать это свойство слишком`Always` в рабочей среде, если нужно устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="4c270-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="4c270-220">Hello **выводит** раздел содержит один выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="4c270-221">Необходимо указать выходной набор данных, даже если программа spark hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="4c270-222">Hello выходного набора данных дисков hello расписания для конвейера hello (каждый час, день, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4c270-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="4c270-223">Дополнительные сведения о свойствах hello, поддерживаемых Spark действия в разделе [Поместите здесь свойства действия](#spark-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="4c270-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="4c270-224">toodeploy hello конвейера, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="4c270-225">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="4c270-225">Monitor pipeline</span></span>
1. <span data-ttu-id="4c270-226">Нажмите кнопку **X** колонок редактор фабрики данных tooclose и toonavigate обратно toohello фабрики данных домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="4c270-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="4c270-227">Нажмите кнопку **монитор и управление** toolaunch hello мониторинг приложения на другой вкладке.</span><span class="sxs-lookup"><span data-stu-id="4c270-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Плитка "Мониторинг и управление"](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="4c270-229">Изменение hello **время начала** фильтрации вверху hello слишком**2/1/2017 г.**и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="4c270-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="4c270-230">Вы увидите только одно окно действия, как время (2017 г-02-02) hello конвейера только по одному дню между hello начала (2017 г-02-01) и окончания.</span><span class="sxs-lookup"><span data-stu-id="4c270-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="4c270-231">Убедитесь, что срез данных hello в **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="4c270-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Монитор hello конвейера](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="4c270-233">Выберите hello **окно действия** toosee сведения о выполнении действия hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="4c270-234">В случае ошибки будут отображаться сведения о нем в правой области hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="4c270-235">Проверьте результаты hello</span><span class="sxs-lookup"><span data-stu-id="4c270-235">Verify hello results</span></span>

1. <span data-ttu-id="4c270-236">Запустите **записную книжку Jupyter** для кластера HDInsight Spark, перейдя по адресу: https://имя_кластера.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="4c270-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="4c270-237">Можно также сначала запустить панель мониторинга для кластера HDInsight Spark, а затем запустить **записную книжку Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="4c270-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="4c270-238">Нажмите кнопку **New** -> **PySpark** toostart новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="4c270-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Новая записная книжка Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="4c270-240">Выполнения hello следующую команду, копирование и вставка текста hello и нажав клавишу **SHIFT + ВВОД** конце hello hello второй инструкции.</span><span class="sxs-lookup"><span data-stu-id="4c270-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="4c270-241">Подтвердите, что вы видите hello данные из таблицы кондиционирования hello:</span><span class="sxs-lookup"><span data-stu-id="4c270-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Результаты запроса Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="4c270-243">Подробные инструкции см. в разделе [Выполнение запроса Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql).</span><span class="sxs-lookup"><span data-stu-id="4c270-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="4c270-244">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="4c270-244">Troubleshooting</span></span>
<span data-ttu-id="4c270-245">Так как вы **getDebugInfo** слишком**всегда**, вы видите **журнала** подпапку hello **pyFiles** папки в контейнере больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="4c270-246">Дополнительные сведения предоставлены Hello файл журнала в папке журналов hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="4c270-247">Этот файл журнала особенно полезен в случае возникновения ошибки.</span><span class="sxs-lookup"><span data-stu-id="4c270-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="4c270-248">В рабочей среде может потребоваться tooset он слишком**сбоя**.</span><span class="sxs-lookup"><span data-stu-id="4c270-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="4c270-249">По устранению неполадок, hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="4c270-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="4c270-250">Перейдите в слишком`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="4c270-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Приложение пользовательского интерфейса YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="4c270-252">Нажмите кнопку **журналы** для одного из hello выполнения попытки.</span><span class="sxs-lookup"><span data-stu-id="4c270-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Страница приложения](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="4c270-254">Вы увидите Дополнительные сведения об ошибке на странице журнала hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-254">You should see additional error information in hello log page.</span></span>

    ![Описание ошибки в журнале](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="4c270-256">Hello в следующих разделах приводятся сведения о кластере Apache Spark toouse сущностей фабрики данных и Spark действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="4c270-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="4c270-257">Свойства действия Spark</span><span class="sxs-lookup"><span data-stu-id="4c270-257">Spark activity properties</span></span>
<span data-ttu-id="4c270-258">Вот определение JSON образец hello конвейер с действиями Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="4c270-259">Hello следующей таблице описаны свойства JSON hello, используемые в определении JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="4c270-260">Свойство</span><span class="sxs-lookup"><span data-stu-id="4c270-260">Property</span></span> | <span data-ttu-id="4c270-261">Описание</span><span class="sxs-lookup"><span data-stu-id="4c270-261">Description</span></span> | <span data-ttu-id="4c270-262">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4c270-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4c270-263">name</span><span class="sxs-lookup"><span data-stu-id="4c270-263">name</span></span> | <span data-ttu-id="4c270-264">Имя действия hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="4c270-265">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-265">Yes</span></span> |
| <span data-ttu-id="4c270-266">Описание</span><span class="sxs-lookup"><span data-stu-id="4c270-266">description</span></span> | <span data-ttu-id="4c270-267">Текст, описывающий, какие действия hello выполняет.</span><span class="sxs-lookup"><span data-stu-id="4c270-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="4c270-268">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-268">No</span></span> |
| <span data-ttu-id="4c270-269">type</span><span class="sxs-lookup"><span data-stu-id="4c270-269">type</span></span> | <span data-ttu-id="4c270-270">Это свойство должно быть задано tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="4c270-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="4c270-271">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-271">Yes</span></span> |
| <span data-ttu-id="4c270-272">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="4c270-272">linkedServiceName</span></span> | <span data-ttu-id="4c270-273">Имя hello HDInsight связанной службы, на какие hello Spark запускается программа.</span><span class="sxs-lookup"><span data-stu-id="4c270-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="4c270-274">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-274">Yes</span></span> |
| <span data-ttu-id="4c270-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="4c270-275">rootPath</span></span> | <span data-ttu-id="4c270-276">контейнер больших двоичных объектов Azure Hello и папку, содержащую файл Spark hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="4c270-277">Имя файла Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="4c270-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="4c270-278">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-278">Yes</span></span> |
| <span data-ttu-id="4c270-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="4c270-279">entryFilePath</span></span> | <span data-ttu-id="4c270-280">Относительный путь toohello корневую папку hello пакет кода Spark.</span><span class="sxs-lookup"><span data-stu-id="4c270-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="4c270-281">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-281">Yes</span></span> |
| <span data-ttu-id="4c270-282">className</span><span class="sxs-lookup"><span data-stu-id="4c270-282">className</span></span> | <span data-ttu-id="4c270-283">Основной класс Java или Spark приложения.</span><span class="sxs-lookup"><span data-stu-id="4c270-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="4c270-284">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-284">No</span></span> |
| <span data-ttu-id="4c270-285">arguments</span><span class="sxs-lookup"><span data-stu-id="4c270-285">arguments</span></span> | <span data-ttu-id="4c270-286">Список аргументов командной строки toohello Spark программы.</span><span class="sxs-lookup"><span data-stu-id="4c270-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="4c270-287">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-287">No</span></span> |
| <span data-ttu-id="4c270-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="4c270-288">proxyUser</span></span> | <span data-ttu-id="4c270-289">Hello учетной записи пользователя tooimpersonate tooexecute hello Spark программы</span><span class="sxs-lookup"><span data-stu-id="4c270-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="4c270-290">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-290">No</span></span> |
| <span data-ttu-id="4c270-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="4c270-291">sparkConfig</span></span> | <span data-ttu-id="4c270-292">Указать значения для свойств конфигурации Spark, перечисленных в разделе hello: [конфигурация Spark - свойства приложения](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="4c270-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="4c270-293">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-293">No</span></span> |
| <span data-ttu-id="4c270-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="4c270-294">getDebugInfo</span></span> | <span data-ttu-id="4c270-295">Указывает при файлов журнала Spark hello скопированный toohello хранилища Azure в кластере HDInsight (или) заданные sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="4c270-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="4c270-296">Допустимые значения: None, Always или Failure.</span><span class="sxs-lookup"><span data-stu-id="4c270-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="4c270-297">Значение по умолчанию: None.</span><span class="sxs-lookup"><span data-stu-id="4c270-297">Default value: None.</span></span> | <span data-ttu-id="4c270-298">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-298">No</span></span> |
| <span data-ttu-id="4c270-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="4c270-299">sparkJobLinkedService</span></span> | <span data-ttu-id="4c270-300">Hello связанной службой хранилища Azure, содержащий файл задания Spark hello, зависимости и журналы.</span><span class="sxs-lookup"><span data-stu-id="4c270-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="4c270-301">Если значение этого свойства не указано, используется хранилище hello, связанное с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c270-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="4c270-302">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="4c270-303">Структура папок</span><span class="sxs-lookup"><span data-stu-id="4c270-303">Folder structure</span></span>
<span data-ttu-id="4c270-304">Hello Spark действия не поддерживает сценарий Pig в строки и выполните действия Hive.</span><span class="sxs-lookup"><span data-stu-id="4c270-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="4c270-305">Задания Spark также обеспечивают большую гибкость, чем задания Pig и Hive.</span><span class="sxs-lookup"><span data-stu-id="4c270-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="4c270-306">Для задания Spark, можно указать несколько зависимостей например jar пакетов (размещено в hello java CLASSPATH), файлы python (размещен в hello PYTHONPATH) и другие файлы.</span><span class="sxs-lookup"><span data-stu-id="4c270-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="4c270-307">Создайте hello следующая структура папок в hello ссылается hello связанной службы HDInsight хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="4c270-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="4c270-308">Затем добавьте зависимые файлы toohello соответствующие вложенные папки в корневой папке hello, представленного **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="4c270-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="4c270-309">Например отправка python файлы toohello pyFiles папки и файлы jar toohello вложенной JAR-файлов hello корневую папку.</span><span class="sxs-lookup"><span data-stu-id="4c270-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="4c270-310">Во время выполнения служба фабрики данных ожидает hello следующая структура папок в hello хранилища больших двоичных объектов Azure:</span><span class="sxs-lookup"><span data-stu-id="4c270-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="4c270-311">Путь</span><span class="sxs-lookup"><span data-stu-id="4c270-311">Path</span></span> | <span data-ttu-id="4c270-312">Описание</span><span class="sxs-lookup"><span data-stu-id="4c270-312">Description</span></span> | <span data-ttu-id="4c270-313">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4c270-313">Required</span></span> | <span data-ttu-id="4c270-314">Тип</span><span class="sxs-lookup"><span data-stu-id="4c270-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="4c270-315">.</span><span class="sxs-lookup"><span data-stu-id="4c270-315">.</span></span> | <span data-ttu-id="4c270-316">путь к корневому каталогу Hello задания Spark hello в hello связанной службой хранилища</span><span class="sxs-lookup"><span data-stu-id="4c270-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="4c270-317">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-317">Yes</span></span> | <span data-ttu-id="4c270-318">Папка</span><span class="sxs-lookup"><span data-stu-id="4c270-318">Folder</span></span> |
| <span data-ttu-id="4c270-319">&lt;Определяется пользователем&gt;</span><span class="sxs-lookup"><span data-stu-id="4c270-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="4c270-320">Hello путем, указывающим toohello запись файла задания Spark hello</span><span class="sxs-lookup"><span data-stu-id="4c270-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="4c270-321">Да</span><span class="sxs-lookup"><span data-stu-id="4c270-321">Yes</span></span> | <span data-ttu-id="4c270-322">Файл</span><span class="sxs-lookup"><span data-stu-id="4c270-322">File</span></span> |
| <span data-ttu-id="4c270-323">./jars</span><span class="sxs-lookup"><span data-stu-id="4c270-323">./jars</span></span> | <span data-ttu-id="4c270-324">Загружаются все файлы в этой папке и разместить на hello java classpath hello кластера</span><span class="sxs-lookup"><span data-stu-id="4c270-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="4c270-325">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-325">No</span></span> | <span data-ttu-id="4c270-326">Папка</span><span class="sxs-lookup"><span data-stu-id="4c270-326">Folder</span></span> |
| <span data-ttu-id="4c270-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="4c270-327">./pyFiles</span></span> | <span data-ttu-id="4c270-328">Загружаются все файлы в этой папке и на hello PYTHONPATH hello кластера</span><span class="sxs-lookup"><span data-stu-id="4c270-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="4c270-329">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-329">No</span></span> | <span data-ttu-id="4c270-330">Папка</span><span class="sxs-lookup"><span data-stu-id="4c270-330">Folder</span></span> |
| <span data-ttu-id="4c270-331">./files</span><span class="sxs-lookup"><span data-stu-id="4c270-331">./files</span></span> | <span data-ttu-id="4c270-332">Все файлы в этой папке передаются и помещаются в рабочий каталог исполнителя.</span><span class="sxs-lookup"><span data-stu-id="4c270-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="4c270-333">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-333">No</span></span> | <span data-ttu-id="4c270-334">Папка</span><span class="sxs-lookup"><span data-stu-id="4c270-334">Folder</span></span> |
| <span data-ttu-id="4c270-335">./archives</span><span class="sxs-lookup"><span data-stu-id="4c270-335">./archives</span></span> | <span data-ttu-id="4c270-336">Все файлы в этой папке не сжаты.</span><span class="sxs-lookup"><span data-stu-id="4c270-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="4c270-337">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-337">No</span></span> | <span data-ttu-id="4c270-338">Папка</span><span class="sxs-lookup"><span data-stu-id="4c270-338">Folder</span></span> |
| <span data-ttu-id="4c270-339">./logs</span><span class="sxs-lookup"><span data-stu-id="4c270-339">./logs</span></span> | <span data-ttu-id="4c270-340">Папка Hello, где хранятся журналы из кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="4c270-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="4c270-341">Нет</span><span class="sxs-lookup"><span data-stu-id="4c270-341">No</span></span> | <span data-ttu-id="4c270-342">Папка</span><span class="sxs-lookup"><span data-stu-id="4c270-342">Folder</span></span> |

<span data-ttu-id="4c270-343">Ниже приведен пример для хранения данных, содержащую два файла задания Spark в hello ссылается hello связанной службы HDInsight хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4c270-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
