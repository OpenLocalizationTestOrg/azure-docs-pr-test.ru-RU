---
title: "aaaBuild первый фабрики данных (Visual Studio) | Документы Microsoft"
description: "В этом руководстве вы создадите образец конвейера фабрики данных Azure с помощью Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="381e7-103">Руководство: создание фабрики данных с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381e7-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="381e7-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="381e7-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="381e7-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="381e7-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="381e7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381e7-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="381e7-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="381e7-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="381e7-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="381e7-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="381e7-109">REST API</span><span class="sxs-lookup"><span data-stu-id="381e7-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="381e7-110">В этом учебнике показано как toocreate фабрикой данных Azure с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="381e7-110">This tutorial shows you how toocreate an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="381e7-111">Создание проекта Visual Studio, с помощью шаблона проекта hello фабрики данных, определить фабрики данных сущности (связанные службы, наборы данных и конвейера) в формате JSON и затем опубликовать или развернуть облако toohello этих сущностей.</span><span class="sxs-lookup"><span data-stu-id="381e7-111">You create a Visual Studio project using hello Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities toohello cloud.</span></span> 

<span data-ttu-id="381e7-112">конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="381e7-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="381e7-113">Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="381e7-114">Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="381e7-115">Копирование данных с помощью фабрики данных Azure в этом руководстве не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="381e7-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="381e7-116">Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="381e7-117">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="381e7-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="381e7-118">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="381e7-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="381e7-119">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="381e7-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="381e7-120">Пошаговое руководство: создание и публикация сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="381e7-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="381e7-121">Ниже приведены hello действий, выполняемых в рамках этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="381e7-121">Here are hello steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="381e7-122">Создать две связанные службы — **AzureStorageLinkedService1** и **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="381e7-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="381e7-123">В этом учебнике входных и выходных данных для действия hive hello в hello же хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="381e7-123">In this tutorial, both input and output data for hello hive activity are in hello same Azure Blob Storage.</span></span> <span data-ttu-id="381e7-124">Использования по требованию HDInsight кластера tooprocess существующих входных данных tooproduce вывода данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-124">You use an on-demand HDInsight cluster tooprocess existing input data tooproduce output data.</span></span> <span data-ttu-id="381e7-125">кластер HDInsight по требованию Hello автоматически создается фабрикой данных Azure во время выполнения при готовности toobe обработки hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-125">hello on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when hello input data is ready toobe processed.</span></span> <span data-ttu-id="381e7-126">Необходимо toolink данные хранятся или вычисляет tooyour фабрики данных, чтобы служба фабрики данных hello могли подключаться toothem во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="381e7-126">You need toolink your data stores or computes tooyour data factory so that hello Data Factory service can connect toothem at runtime.</span></span> <span data-ttu-id="381e7-127">Таким образом свяжите фабрики данных toohello вашей учетной записи хранилища Azure, используя hello AzureStorageLinkedService1 и связать с кластером HDInsight по требованию с помощью hello HDInsightOnDemandLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="381e7-127">Therefore, you link your Azure Storage Account toohello data factory by using hello AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using hello HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="381e7-128">При публикации, указывается имя hello для hello данных фабрики toobe создана или существующую фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-128">When publishing, you specify hello name for hello data factory toobe created or an existing data factory.</span></span>  
2. <span data-ttu-id="381e7-129">Два набора данных: **InputDataset** и **OutputDataset**, которые представляют Привет ввода вывода данных, хранящиеся в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent hello input/output data that is stored in hello Azure blob storage.</span></span> 
   
    <span data-ttu-id="381e7-130">Эти определения набора данных см. в toohello связанной службой хранилища Azure, созданный на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-130">These dataset definitions refer toohello Azure Storage linked service you created in hello previous step.</span></span> <span data-ttu-id="381e7-131">Для hello InputDataset укажите контейнер больших двоичных объектов hello (adfgetstarted) и hello папку (inptutdata), содержащий большой двоичный объект с hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-131">For hello InputDataset, you specify hello blob container (adfgetstarted) and hello folder (inptutdata) that contains a blob with hello input data.</span></span> <span data-ttu-id="381e7-132">Для hello OutputDataset укажите контейнер больших двоичных объектов hello (adfgetstarted) и папки hello (partitioneddata), содержащий hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-132">For hello OutputDataset, you specify hello blob container (adfgetstarted) and hello folder (partitioneddata) that holds hello output data.</span></span> <span data-ttu-id="381e7-133">Нужно указать и другие свойства, такие как структура, доступность данных и политика.</span><span class="sxs-lookup"><span data-stu-id="381e7-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="381e7-134">Создать конвейер с именем **MyFirstPipeline**.</span><span class="sxs-lookup"><span data-stu-id="381e7-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="381e7-135">В этом пошаговом руководстве конвейер hello содержит только одно действие: **действие Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="381e7-135">In this walkthrough, hello pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="381e7-136">Эти действия преобразования входных данных tooproduce выходные данные с помощью скрипта hive в кластере HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="381e7-136">This activity transform input data tooproduce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="381e7-137">toolearn Дополнительные сведения о действие hive в разделе [действие Hive](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="381e7-137">toolearn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="381e7-138">Создать фабрику данных с именем **DataFactoryUsingVS**.</span><span class="sxs-lookup"><span data-stu-id="381e7-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="381e7-139">Развертывание фабрики данных hello и все сущности фабрики данных (связанные службы, таблицы и hello конвейера).</span><span class="sxs-lookup"><span data-stu-id="381e7-139">Deploy hello data factory and all Data Factory entities (linked services, tables, and hello pipeline).</span></span>
5. <span data-ttu-id="381e7-140">После публикации, использовании Azure портала колонок и мониторинг & приложение для управления конвейера toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-140">After you publish, you use Azure portal blades and Monitoring & Management App toomonitor hello pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="381e7-141">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="381e7-141">Prerequisites</span></span>
1. <span data-ttu-id="381e7-142">Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="381e7-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span> <span data-ttu-id="381e7-143">Можно также выбрать hello **Обзор и необходимые компоненты** вариант в раскрывающемся списке hello во статья toohello top tooswitch hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-143">You can also select hello **Overview and prerequisites** option in hello drop-down list at hello top tooswitch toohello article.</span></span> <span data-ttu-id="381e7-144">После выполнения необходимых компонентов hello переключиться назад toothis статьи, выбрав **Visual Studio** вариант в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-144">After you complete hello prerequisites, switch back toothis article by selecting **Visual Studio** option in hello drop-down list.</span></span>
2. <span data-ttu-id="381e7-145">экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.</span><span class="sxs-lookup"><span data-stu-id="381e7-145">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>  
3. <span data-ttu-id="381e7-146">Необходимо иметь следующие hello, установленной на компьютере.</span><span class="sxs-lookup"><span data-stu-id="381e7-146">You must have hello following installed on your computer:</span></span>
   * <span data-ttu-id="381e7-147">Visual Studio 2013 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="381e7-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="381e7-148">Загрузите пакет SDK Azure для Visual Studio 2013 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="381e7-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="381e7-149">Перейдите в слишком[странице загрузки Azure](https://azure.microsoft.com/downloads/) и нажмите кнопку **VS 2013** или **VS 2015** в hello **.NET** раздела.</span><span class="sxs-lookup"><span data-stu-id="381e7-149">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="381e7-150">Загрузите hello последнюю фабрики данных Azure, подключаемый модуль для Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) или [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="381e7-150">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="381e7-151">Можно также обновить hello подключаемого модуля, выполнив следующие шаги hello: hello меню **средства** -> **расширения и обновления** -> **Online**  ->  **Коллекции visual Studio** -> **средства фабрики данных Microsoft Azure для Visual Studio** -> **обновление**.</span><span class="sxs-lookup"><span data-stu-id="381e7-151">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="381e7-152">Теперь воспользуемся Visual Studio toocreate фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-152">Now, let's use Visual Studio toocreate an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="381e7-153">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381e7-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="381e7-154">Запустите **Visual Studio 2013** или **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="381e7-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="381e7-155">Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="381e7-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="381e7-156">Вы увидите hello **новый проект** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="381e7-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="381e7-157">В hello **новый проект** диалоговое окно, выберите hello **DataFactory** шаблона и нажмите кнопку **пустой проект фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="381e7-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![Диалоговое окно "Новый проект"](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="381e7-159">Введите **имя** для проекта hello **расположение**и имя для hello **решения**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="381e7-159">Enter a **name** for hello project, **location**, and a name for hello **solution**, and click **OK**.</span></span>

    ![Обозреватель решений](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="381e7-161">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="381e7-161">Create linked services</span></span>
<span data-ttu-id="381e7-162">На этом шаге вы создадите две связанные службы — **службу хранилища Azure** и **связанную службу кластера HDInsight по запросу**.</span><span class="sxs-lookup"><span data-stu-id="381e7-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="381e7-163">Hello хранилища Azure связанные ссылки на службу фабрики данных toohello учетной записи хранилища Azure, предоставляя сведения о соединении hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-163">hello Azure Storage linked service links your Azure Storage account toohello data factory by providing hello connection information.</span></span> <span data-ttu-id="381e7-164">Служба фабрики данных использует строку подключения hello из toohello tooconnect параметр hello связанной службы хранилища Azure во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="381e7-164">Data Factory service uses hello connection string from hello linked service setting tooconnect toohello Azure storage at runtime.</span></span> <span data-ttu-id="381e7-165">Это хранилище содержит входные и выходные данные для конвейера hello и hello hive файл скрипта, используемый действием hive hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-165">This storage holds input and output data for hello pipeline, and hello hive script file used by hello hive activity.</span></span> 

<span data-ttu-id="381e7-166">С по требованию связанной службы HDInsight hello кластера HDInsight создается автоматически во время выполнения при готовности tooprocessed hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-166">With on-demand HDInsight linked service, hello HDInsight cluster is automatically created at runtime when hello input data is ready tooprocessed.</span></span> <span data-ttu-id="381e7-167">Hello кластера удаляется после завершения обработки и время простоя для hello указанного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="381e7-167">hello cluster is deleted after it is done processing and idle for hello specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="381e7-168">Создать фабрику данных, указав его имя и параметры во время hello публикации решения фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-168">You create a data factory by specifying its name and settings at hello time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="381e7-169">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="381e7-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="381e7-170">Щелкните правой кнопкой мыши **связанные службы** в обозревателе решений hello точки слишком**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="381e7-170">Right-click **Linked Services** in hello solution explorer, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="381e7-171">В hello **Добавление нового элемента** выберите **связанной службы хранилища Azure** hello списка и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-171">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span>
    <span data-ttu-id="381e7-172">![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="381e7-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="381e7-173">Замените `<accountname>` и `<accountkey>` hello имя вашей учетной записи хранилища Azure и ее ключа.</span><span class="sxs-lookup"><span data-stu-id="381e7-173">Replace `<accountname>` and `<accountkey>` with hello name of your Azure storage account and its key.</span></span> <span data-ttu-id="381e7-174">toolearn как доступ tooget хранилища ключей см. в разделе hello сведения о доступом tooview, копирования и повторное создание хранилища ключей в [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="381e7-174">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="381e7-175">![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="381e7-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="381e7-176">Сохранить hello **AzureStorageLinkedService1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="381e7-176">Save hello **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="381e7-177">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="381e7-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="381e7-178">В hello **обозревателе решений**, щелкните правой кнопкой мыши **связанные службы**, слишком точки**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="381e7-178">In hello **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="381e7-179">Выберите **Связанная служба HDInsight по запросу**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="381e7-180">Замените hello **JSON** с hello, следуя JSON:</span><span class="sxs-lookup"><span data-stu-id="381e7-180">Replace hello **JSON** with hello following JSON:</span></span>

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="381e7-181">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-181">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="381e7-182">Свойство</span><span class="sxs-lookup"><span data-stu-id="381e7-182">Property</span></span> | <span data-ttu-id="381e7-183">Описание</span><span class="sxs-lookup"><span data-stu-id="381e7-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="381e7-184">ClusterSize (размер кластера)</span><span class="sxs-lookup"><span data-stu-id="381e7-184">ClusterSize</span></span> | <span data-ttu-id="381e7-185">Задает размер hello hello кластера HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="381e7-185">Specifies hello size of hello HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="381e7-186">TimeToLive (срок жизни)</span><span class="sxs-lookup"><span data-stu-id="381e7-186">TimeToLive</span></span> | <span data-ttu-id="381e7-187">Задает время простоя, "hello" для кластера HDInsight hello, перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="381e7-187">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="381e7-188">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="381e7-188">linkedServiceName</span></span> | <span data-ttu-id="381e7-189">Указывает учетную запись хранилища hello, используемые toostore hello журналы, созданные в кластере HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="381e7-189">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="381e7-190">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="381e7-190">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="381e7-191">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="381e7-191">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="381e7-192">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="381e7-192">This behavior is by design.</span></span> <span data-ttu-id="381e7-193">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер (timeToLive)).</span><span class="sxs-lookup"><span data-stu-id="381e7-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="381e7-194">Hello кластера автоматически удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-194">hello cluster is automatically deleted when hello processing is done.</span></span>
    > 
    > <span data-ttu-id="381e7-195">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="381e7-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="381e7-196">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-196">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="381e7-197">имена этих контейнеров Hello соответствуют шаблону: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="381e7-197">hello names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="381e7-198">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="381e7-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="381e7-199">Дополнительные сведения о свойствах JSON см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="381e7-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="381e7-200">Сохранить hello **HDInsightOnDemandLinkedService1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="381e7-200">Save hello **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="381e7-201">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="381e7-201">Create datasets</span></span>
<span data-ttu-id="381e7-202">На этом шаге создания наборов данных toorepresent hello входных и выходных данных для обработки Hive.</span><span class="sxs-lookup"><span data-stu-id="381e7-202">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="381e7-203">Эти наборы данных ссылаются toohello **AzureStorageLinkedService1** вы создали ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="381e7-203">These datasets refer toohello **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="381e7-204">Здравствуйте tooan точек связанной службы учетной записи хранилища Azure и указать наборы данных контейнера, папки, имя файла в хранилище hello, который содержит входные данные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="381e7-204">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="381e7-205">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="381e7-205">Create input dataset</span></span>
1. <span data-ttu-id="381e7-206">В hello **обозревателе решений**, щелкните правой кнопкой мыши **таблиц**, слишком точки**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="381e7-206">In hello **Solution Explorer**, right-click **Tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="381e7-207">Выберите **больших двоичных объектов Azure** из списка hello изменение hello имени файла hello слишком**InputDataSet.json**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-207">Select **Azure Blob** from hello list, change hello name of hello file too**InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="381e7-208">Замените hello **JSON** в редакторе hello и hello, следующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="381e7-208">Replace hello **JSON** in hello editor with hello following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="381e7-209">Этот фрагмент JSON определяет набор данных с именем **AzureBlobInput** , представляющий входные данные для действия hive hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for hello hive activity in hello pipeline.</span></span> <span data-ttu-id="381e7-210">Укажите, hello входных данных находится в контейнере hello BLOB-объекта с именем `adfgetstarted` и hello папку с именем `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="381e7-210">You specify that hello input data is located in hello blob container called `adfgetstarted` and hello folder called `inputdata`.</span></span>

    <span data-ttu-id="381e7-211">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-211">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="381e7-212">Свойство</span><span class="sxs-lookup"><span data-stu-id="381e7-212">Property</span></span> | <span data-ttu-id="381e7-213">Описание</span><span class="sxs-lookup"><span data-stu-id="381e7-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="381e7-214">type</span><span class="sxs-lookup"><span data-stu-id="381e7-214">type</span></span> |<span data-ttu-id="381e7-215">Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-215">hello type property is set too**AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="381e7-216">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="381e7-216">linkedServiceName</span></span> | <span data-ttu-id="381e7-217">Ссылается toohello AzureStorageLinkedService1, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="381e7-217">Refers toohello AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="381e7-218">fileName</span><span class="sxs-lookup"><span data-stu-id="381e7-218">fileName</span></span> |<span data-ttu-id="381e7-219">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="381e7-219">This property is optional.</span></span> <span data-ttu-id="381e7-220">Если это свойство не указан, извлекаются все файлы hello из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="381e7-220">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="381e7-221">В этом случае обрабатывается только input.log hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-221">In this case, only hello input.log is processed.</span></span>
    <span data-ttu-id="381e7-222">type</span><span class="sxs-lookup"><span data-stu-id="381e7-222">type</span></span> | <span data-ttu-id="381e7-223">файлы журнала Hello находятся в текстовом формате, поэтому мы используем TextFormat.</span><span class="sxs-lookup"><span data-stu-id="381e7-223">hello log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="381e7-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="381e7-224">columnDelimiter</span></span> | <span data-ttu-id="381e7-225">столбцы в файлах журнала hello разделяются запятой hello (`,`)</span><span class="sxs-lookup"><span data-stu-id="381e7-225">columns in hello log files are delimited by hello comma character (`,`)</span></span>
    <span data-ttu-id="381e7-226">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="381e7-226">frequency/interval</span></span> | <span data-ttu-id="381e7-227">tooMonth задать частоту и интервал равен 1, это означает, что входные срезы hello доступны ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="381e7-227">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span>
    <span data-ttu-id="381e7-228">external</span><span class="sxs-lookup"><span data-stu-id="381e7-228">external</span></span> | <span data-ttu-id="381e7-229">Это свойство имеет значение tootrue, если конвейером hello не создается hello входные данные для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="381e7-229">This property is set tootrue if hello input data for hello activity is not generated by hello pipeline.</span></span> <span data-ttu-id="381e7-230">Это свойство указывается только для входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="381e7-231">Для hello входного набора данных из первого действия hello всегда установите его tootrue.</span><span class="sxs-lookup"><span data-stu-id="381e7-231">For hello input dataset of hello first activity, always set it tootrue.</span></span>
4. <span data-ttu-id="381e7-232">Сохранить hello **InputDataset.json** файла.</span><span class="sxs-lookup"><span data-stu-id="381e7-232">Save hello **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="381e7-233">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="381e7-233">Create output dataset</span></span>
<span data-ttu-id="381e7-234">Теперь создание hello выходной набор данных toorepresent выходные данные хранятся в hello хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-234">Now, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="381e7-235">В hello **обозревателе решений**, щелкните правой кнопкой мыши **таблиц**, слишком точки**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="381e7-235">In hello **Solution Explorer**, right-click **tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="381e7-236">Выберите **больших двоичных объектов Azure** из списка hello изменение hello имени файла hello слишком**OutputDataset.json**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-236">Select **Azure Blob** from hello list, change hello name of hello file too**OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="381e7-237">Замените hello **JSON** в редакторе hello и hello, следуя JSON:</span><span class="sxs-lookup"><span data-stu-id="381e7-237">Replace hello **JSON** in hello editor with hello following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="381e7-238">фрагмент кода Hello JSON определяет набор данных с именем **AzureBlobOutput** , представляет выходные данные, полученные в результате действия hive hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-238">hello JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by hello hive activity in hello pipeline.</span></span> <span data-ttu-id="381e7-239">Укажите, что hello вывода данных, полученных при действие hive hello размещается в контейнер больших двоичных объектов hello вызывается `adfgetstarted` и hello папку с именем `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="381e7-239">You specify that hello output data is produced by hello hive activity is placed in hello blob container called `adfgetstarted` and hello folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="381e7-240">Hello **доступности** раздела указывает, что hello выходной набор данных создается на ежемесячной основе.</span><span class="sxs-lookup"><span data-stu-id="381e7-240">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="381e7-241">Hello выходного набора данных дисков hello расписания hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="381e7-241">hello output dataset drives hello schedule of hello pipeline.</span></span> <span data-ttu-id="381e7-242">конвейер Hello выполняется раз в месяц между временем его начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="381e7-242">hello pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="381e7-243">В разделе **Создание входного набора данных hello** раздел для описания этих свойств.</span><span class="sxs-lookup"><span data-stu-id="381e7-243">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="381e7-244">Не задано внешних свойств hello в выходной набор данных как hello набора данных создается путем hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="381e7-244">You do not set hello external property on an output dataset as hello dataset is produced by hello pipeline.</span></span>
4. <span data-ttu-id="381e7-245">Сохранить hello **OutputDataset.json** файла.</span><span class="sxs-lookup"><span data-stu-id="381e7-245">Save hello **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="381e7-246">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="381e7-246">Create pipeline</span></span>
<span data-ttu-id="381e7-247">Вы создали hello связанной службой хранилища Azure и входные и выходные наборы данных к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="381e7-247">You have created hello Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="381e7-248">Теперь вы можете создать конвейер с помощью действия **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="381e7-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="381e7-249">Hello **ввода** для куста hello действия установлено слишком**AzureBlobInput** и **вывода** задано слишком**AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="381e7-249">hello **input** for hello hive activity is set too**AzureBlobInput** and **output** is set too**AzureBlobOutput**.</span></span> <span data-ttu-id="381e7-250">Срез входной набор данных доступен ежемесячно (частота: месяц, интервал: 1), и hello вывода срезов ежемесячно слишком.</span><span class="sxs-lookup"><span data-stu-id="381e7-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and hello output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="381e7-251">В hello **обозревателе решений**, щелкните правой кнопкой мыши **конвейеры**, слишком точки**добавить**и нажмите кнопку **новый элемент.**</span><span class="sxs-lookup"><span data-stu-id="381e7-251">In hello **Solution Explorer**, right-click **Pipelines**, point too**Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="381e7-252">Выберите **конвейера преобразования Hive** hello списка и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-252">Select **Hive Transformation Pipeline** from hello list, and click **Add**.</span></span>
3. <span data-ttu-id="381e7-253">Замените hello **JSON** с hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="381e7-253">Replace hello **JSON** with hello following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="381e7-254">Замените `<storageaccountname>` с именем hello вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="381e7-254">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="381e7-255">Замените `<storageaccountname>` с именем hello вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="381e7-255">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

    <span data-ttu-id="381e7-256">фрагмент кода Hello JSON определяет конвейера, который состоит из одного действия (действие Hive).</span><span class="sxs-lookup"><span data-stu-id="381e7-256">hello JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="381e7-257">Это действие выполняет сценарий Hive tooprocess входные данные на по требованию tooproduce кластера HDInsight выходных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-257">This activity runs a Hive script tooprocess input data on an on-demand HDInsight cluster tooproduce output data.</span></span> <span data-ttu-id="381e7-258">В разделе действий hello hello конвейера JSON, вы видите только одно действие в массиве hello типом слишком**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="381e7-258">In hello activities section of hello pipeline JSON, you see only one activity in hello array with type set too**HDInsightHive**.</span></span> 

    <span data-ttu-id="381e7-259">В hello свойства типа, определенного tooHDInsight действие Hive можно указать, какие связанной службой хранилища Azure имеет файлу скрипта hive hello, файла сценария toohello путь hello и параметры файла сценария toohello.</span><span class="sxs-lookup"><span data-stu-id="381e7-259">In hello type properties that are specific tooHDInsight Hive activity, you specify what Azure Storage linked service has hello hive script file, hello path toohello script file, and parameters toohello script file.</span></span> 

    <span data-ttu-id="381e7-260">файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (как указано в hello scriptLinkedService), а в hello `script` папки в контейнере hello `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="381e7-260">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService), and in hello `script` folder in hello container `adfgetstarted`.</span></span>

    <span data-ttu-id="381e7-261">Hello `defines` раздел представляет параметры среды выполнения используется toospecify hello, переданных toohello скрипт hive в качестве значения конфигурации Hive (например `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span><span class="sxs-lookup"><span data-stu-id="381e7-261">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="381e7-262">Hello **запустить** и **окончания** свойства конвейера hello указывает hello активного периода конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-262">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span> <span data-ttu-id="381e7-263">Вы настроили toobe hello набора данных, полученных ежемесячно, таким образом, только в том случае, когда срезов конвейером hello (поскольку hello месяц — то же, даты начала и окончания).</span><span class="sxs-lookup"><span data-stu-id="381e7-263">You configured hello dataset toobe produced monthly, therefore, only once slice is produced by hello pipeline (because hello month is same in start and end dates).</span></span>

    <span data-ttu-id="381e7-264">В действии hello JSON, указать, что hello скрипт Hive будет выполняться на hello вычислений, определяемое hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="381e7-264">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="381e7-265">Сохранить hello **HiveActivity1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="381e7-265">Save hello **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="381e7-266">Добавление файлов partitionweblogs.hql и input.log в качестве зависимости</span><span class="sxs-lookup"><span data-stu-id="381e7-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="381e7-267">Щелкните правой кнопкой мыши **зависимости** в hello **обозревателе решений** окна, точки слишком**добавить**и нажмите кнопку **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="381e7-267">Right-click **Dependencies** in hello **Solution Explorer** window, point too**Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="381e7-268">Перейдите toohello **C:\ADFGettingStarted** и выберите **partitionweblogs.hql**, **input.log** файлы и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-268">Navigate toohello **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="381e7-269">Вы создали эти файлы как часть необходимые компоненты из hello [Обзор учебника](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-269">You created these two files as part of prerequisites from hello [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="381e7-270">При публикации решения hello в следующем шаге hello hello **partitionweblogs.hql** файл является отправленного toohello **сценарий** папки в hello `adfgetstarted` контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="381e7-270">When you publish hello solution in hello next step, hello **partitionweblogs.hql** file is uploaded toohello **script** folder in hello `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="381e7-271">Публикация и развертывание сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="381e7-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="381e7-272">На этом шаге вы опубликовать hello фабрики данных сущности (связанные службы, наборы данных и конвейера) в ваш проект toohello служба фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-272">In this step, you publish hello Data Factory entities (linked services, datasets, and pipeline) in your project toohello Azure Data Factory service.</span></span> <span data-ttu-id="381e7-273">В процесс публикации hello укажите имя hello для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-273">In hello process of publishing, you specify hello name for your data factory.</span></span> 

1. <span data-ttu-id="381e7-274">Щелкните правой кнопкой мыши проект в обозревателе решений hello и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="381e7-274">Right-click project in hello Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="381e7-275">Если вы видите **входа в учетную запись Майкрософт tooyour** диалоговое окно, введите свои учетные данные для hello учетной записи, имеющей подписку Azure и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="381e7-275">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="381e7-276">Вы должны увидеть следующие диалоговое окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="381e7-276">You should see hello following dialog box:</span></span>

   ![Диалоговое окно "Опубликовать"](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="381e7-278">В hello **фабрики данных Настройка** страницы, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="381e7-278">In hello **Configure data factory** page, do hello following steps:</span></span>

    ![Публикация. Новые параметры фабрики данных](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="381e7-280">Выберите **Создать новую фабрику данных** .</span><span class="sxs-lookup"><span data-stu-id="381e7-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="381e7-281">Введите уникальный **имя** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-281">Enter a unique **name** for hello data factory.</span></span> <span data-ttu-id="381e7-282">Например: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="381e7-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="381e7-283">Hello имя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="381e7-283">hello name must be globally unique.</span></span>
   3. <span data-ttu-id="381e7-284">Выберите подходящую подписку hello hello **подписки** поля.</span><span class="sxs-lookup"><span data-stu-id="381e7-284">Select hello right subscription for hello **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="381e7-285">Если вы не видите любую подписку, убедитесь, что вы вошли в учетную запись, которая является администратором или соадминистратором подписки hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>
   4. <span data-ttu-id="381e7-286">Выберите hello **группы ресурсов** для hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="381e7-286">Select hello **resource group** for hello data factory toobe created.</span></span>
   5. <span data-ttu-id="381e7-287">Выберите hello **область** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-287">Select hello **region** for hello data factory.</span></span>
   6. <span data-ttu-id="381e7-288">Нажмите кнопку **Далее** tooswitch toohello **публиковать элементы** страницы.</span><span class="sxs-lookup"><span data-stu-id="381e7-288">Click **Next** tooswitch toohello **Publish Items** page.</span></span> <span data-ttu-id="381e7-289">(Нажмите клавишу **ВКЛАДКЕ** toomove из hello имя поля tooif hello **Далее** кнопка отключена.)</span><span class="sxs-lookup"><span data-stu-id="381e7-289">(Press **TAB** toomove out of hello Name field tooif hello **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="381e7-290">Если ошибка hello **имя фабрики данных «DataFactoryUsingVS» недоступен** при публикации, измените имя hello (например, yournameDataFactoryUsingVS).</span><span class="sxs-lookup"><span data-stu-id="381e7-290">If you receive hello error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change hello name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="381e7-291">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="381e7-292">В hello **публиковать элементы** убедитесь, что все hello фабрик данных сущностей установлены и нажмите кнопку **Далее** tooswitch toohello **Сводка** страницы.</span><span class="sxs-lookup"><span data-stu-id="381e7-292">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>

    ![Страница Publish items (Публикация элементов)](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="381e7-294">Просмотрите hello сводки и нажмите кнопку **Далее** toostart hello развертывания процесса и представление hello **состояние развертывания**.</span><span class="sxs-lookup"><span data-stu-id="381e7-294">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>

    ![Страница "Сводка"](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="381e7-296">В hello **состояние развертывания** страницы, вы увидите hello состояние процесса развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-296">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="381e7-297">После завершения развертывания hello, нажмите кнопку "Готово".</span><span class="sxs-lookup"><span data-stu-id="381e7-297">Click Finish after hello deployment is done.</span></span>

<span data-ttu-id="381e7-298">Toonote важные моменты:</span><span class="sxs-lookup"><span data-stu-id="381e7-298">Important points toonote:</span></span>

- <span data-ttu-id="381e7-299">Если ошибка hello: **этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory**, выполните одно из следующих hello и повторите попытку публикации:</span><span class="sxs-lookup"><span data-stu-id="381e7-299">If you receive hello error: **This subscription is not registered toouse namespace Microsoft.DataFactory**, do one of hello following and try publishing again:</span></span>
    - <span data-ttu-id="381e7-300">В Azure PowerShell запустите hello, следующая команда tooregister hello фабрики данных поставщика.</span><span class="sxs-lookup"><span data-stu-id="381e7-300">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="381e7-301">Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-301">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="381e7-302">Имя входа с помощью hello подписку Azure в toohello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-302">Login using hello Azure subscription in toohello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="381e7-303">Это действие автоматически регистрирует поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-303">This action automatically registers hello provider for you.</span></span>
- <span data-ttu-id="381e7-304">Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.</span><span class="sxs-lookup"><span data-stu-id="381e7-304">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
- <span data-ttu-id="381e7-305">экземпляры toocreate фабрики данных, необходимые toobe администратором или соадминистратором подписки Azure hello</span><span class="sxs-lookup"><span data-stu-id="381e7-305">toocreate Data Factory instances, you need toobe an admin or co-admin of hello Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="381e7-306">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="381e7-306">Monitor pipeline</span></span>
<span data-ttu-id="381e7-307">На этом шаге отслеживать использование представления схемы фабрики данных hello конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-307">In this step, you monitor hello pipeline using Diagram View of hello data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="381e7-308">Мониторинг конвейера с использованием представления схемы</span><span class="sxs-lookup"><span data-stu-id="381e7-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="381e7-309">Войдите в toohello [портал Azure](https://portal.azure.com/), hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="381e7-309">Log in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>
   1. <span data-ttu-id="381e7-310">Щелкните **Другие службы** и выберите **Фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="381e7-310">Click **More services** and click **Data factories**.</span></span>
       
        ![Обзор фабрик данных](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="381e7-312">Выберите hello имя фабрики данных (например: **DataFactoryUsingVS09152016**) из списка hello фабрик данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-312">Select hello name of your data factory (for example: **DataFactoryUsingVS09152016**) from hello list of data factories.</span></span>
   
       ![Выбор фабрики данных](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="381e7-314">На домашней странице приветствия для фабрики данных, нажмите кнопку **схема**.</span><span class="sxs-lookup"><span data-stu-id="381e7-314">In hello home page for your data factory, click **Diagram**.</span></span>

    ![Плитка "Схема"](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="381e7-316">В hello представление диаграммы отображаются общие сведения о конвейерах hello и наборы данных, используемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="381e7-316">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Представление схемы](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="381e7-318">tooview все действия в конвейере hello, щелкните правой кнопкой мыши конвейера в hello схемы и нажмите кнопку Открыть конвейера.</span><span class="sxs-lookup"><span data-stu-id="381e7-318">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Откройте меню конвейера](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="381e7-320">Убедитесь, что это действие HDInsightHive hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-320">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Откройте представление конвейера](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="381e7-322">toonavigate резервное toohello предыдущего представления, нажмите кнопку **фабрики данных** в меню навигации hello верхней hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-322">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
6. <span data-ttu-id="381e7-323">В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="381e7-323">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="381e7-324">Убедитесь, что срез hello в **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="381e7-324">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="381e7-325">Он может занять несколько минут для tooshow срез hello в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="381e7-325">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="381e7-326">Если не происходят через некоторое время, убедитесь, что hello входного файла (input.log) в нужных контейнерах hello (`adfgetstarted`) и папки (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="381e7-326">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="381e7-327">И убедитесь, что hello **внешних** на входной набор данных hello задано слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="381e7-327">And, make sure that hello **external** property on hello input dataset is set too**true**.</span></span> 

   ![Срез входных данных в состоянии "Готово"](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="381e7-329">Нажмите кнопку **X** tooclose **AzureBlobInput** колонку.</span><span class="sxs-lookup"><span data-stu-id="381e7-329">Click **X** tooclose **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="381e7-330">В hello **представление диаграммы**, дважды щелкните набор данных hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="381e7-330">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="381e7-331">Вы увидите, что hello срез, который обрабатывается в данный момент.</span><span class="sxs-lookup"><span data-stu-id="381e7-331">You see that hello slice that is currently being processed.</span></span>

   ![Выборка](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="381e7-333">После завершения обработки отображается срез hello в **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="381e7-333">When processing is done, you see hello slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="381e7-334">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="381e7-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="381e7-335">Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.</span><span class="sxs-lookup"><span data-stu-id="381e7-335">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>  
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="381e7-337">Если срез hello находится в **готовности** состоянии, проверьте hello `partitioneddata` папки в hello `adfgetstarted` контейнера в хранилище BLOB-объектов для hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-337">When hello slice is in **Ready** state, check hello `partitioneddata` folder in hello `adfgetstarted` container in your blob storage for hello output data.</span></span>  

    ![выходные данные](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="381e7-339">Нажмите кнопку hello срез toosee сведения о нем на **срез данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="381e7-339">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

    ![Сведения о срезе данных](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="381e7-341">Щелкните действие в hello **действие выполняется список** toosee сведения о действиях (Hive действие выполнения в нашем сценарии) **сведения о выполнении действия** окна.</span><span class="sxs-lookup"><span data-stu-id="381e7-341">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![СВЕДЕНИЯ О ВЫПОЛНЕННОМ ДЕЙСТВИИ](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="381e7-343">Из файлов журнала hello вы увидите выполненного запроса Hive hello и сведения о состоянии.</span><span class="sxs-lookup"><span data-stu-id="381e7-343">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="381e7-344">Эти журналы полезны при устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="381e7-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="381e7-345">В разделе [отслеживать наборы данных и конвейера](data-factory-monitor-manage-pipelines.md) инструкции как toouse hello Azure портала toomonitor hello конвейера и наборы данных вы создали в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="381e7-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="381e7-346">Мониторинг конвейера с использованием приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="381e7-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="381e7-347">Вы можете использовать монитор и управлять конвейеры toomonitor приложения.</span><span class="sxs-lookup"><span data-stu-id="381e7-347">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="381e7-348">Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="381e7-349">Щелкните плитку Monitor & Manage (Мониторинг и управление).</span><span class="sxs-lookup"><span data-stu-id="381e7-349">Click Monitor & Manage tile.</span></span>

    ![Плитка Monitor & Manage (Мониторинг и управление)](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="381e7-351">Вы должны увидеть приложение по мониторингу и управлению.</span><span class="sxs-lookup"><span data-stu-id="381e7-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="381e7-352">Изменение hello **время начала** и **время окончания** toomatch начала (04-01-2016 12:00 AM) время и окончания (04-02-2016 12:00 AM) конвейера и щелкните **применить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-352">Change hello **Start time** and **End time** toomatch start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![Приложение по мониторингу и управлению](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="381e7-354">toosee сведения об окне активности, выберите его в hello **список действий Windows** toosee сведения о ней.</span><span class="sxs-lookup"><span data-stu-id="381e7-354">toosee details about an activity window, select it in hello **Activity Windows list** toosee details about it.</span></span>
    <span data-ttu-id="381e7-355">![Сведения об окне действия](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="381e7-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="381e7-356">входной файл Hello, удаляется при успешно обработал hello среза.</span><span class="sxs-lookup"><span data-stu-id="381e7-356">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="381e7-357">Таким образом, если toorerun hello кольца или hello учебник, отправить hello входного файла (input.log) toohello `inputdata` папки hello `adfgetstarted` контейнера.</span><span class="sxs-lookup"><span data-stu-id="381e7-357">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello `inputdata` folder of hello `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="381e7-358">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="381e7-358">Additional notes</span></span>
- <span data-ttu-id="381e7-359">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="381e7-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="381e7-360">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="381e7-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="381e7-361">Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входные данные.</span><span class="sxs-lookup"><span data-stu-id="381e7-361">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="381e7-362">В разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех hello источники и приемники, поддерживаемые действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="381e7-363">В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) список hello вычислительных служб, поддерживаемые фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-363">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="381e7-364">Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений.</span><span class="sxs-lookup"><span data-stu-id="381e7-364">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="381e7-365">В разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех hello источники и приемники, поддерживаемые действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="381e7-366">В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) список hello вычислительных служб, поддерживаемые фабрикой данных и [действия преобразования](data-factory-data-transformation-activities.md) , можно запустить на них.</span><span class="sxs-lookup"><span data-stu-id="381e7-366">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="381e7-367">В разделе [перемещения данных из / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойств, используемых в hello связанная определение службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-367">See [Move data from/tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in hello Azure Storage linked service definition.</span></span>
- <span data-ttu-id="381e7-368">Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="381e7-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="381e7-369">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="381e7-370">Hello фабрики данных создает **под управлением Linux** кластера HDInsight для вас с hello, предшествующий JSON.</span><span class="sxs-lookup"><span data-stu-id="381e7-370">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello preceding JSON.</span></span> <span data-ttu-id="381e7-371">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="381e7-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="381e7-372">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="381e7-372">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="381e7-373">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="381e7-373">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="381e7-374">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="381e7-374">This behavior is by design.</span></span> <span data-ttu-id="381e7-375">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер (timeToLive)).</span><span class="sxs-lookup"><span data-stu-id="381e7-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="381e7-376">Hello кластера автоматически удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-376">hello cluster is automatically deleted when hello processing is done.</span></span>
    
    <span data-ttu-id="381e7-377">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="381e7-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="381e7-378">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-378">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="381e7-379">имена этих контейнеров Hello соответствуют шаблону: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="381e7-379">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="381e7-380">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="381e7-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="381e7-381">В настоящее время выходной набор данных — того, какие диски hello расписания, поэтому вам необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-381">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="381e7-382">Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-382">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 
- <span data-ttu-id="381e7-383">Копирование данных с помощью фабрики данных Azure в этом руководстве не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="381e7-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="381e7-384">Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-384">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-tooview-data-factories"></a><span data-ttu-id="381e7-385">Использовать обозреватель серверов tooview данных фабрики</span><span class="sxs-lookup"><span data-stu-id="381e7-385">Use Server Explorer tooview data factories</span></span>
1. <span data-ttu-id="381e7-386">В **Visual Studio**, нажмите кнопку **представление** hello меню и нажмите кнопку **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="381e7-386">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="381e7-387">Разверните в окне обозревателя серверов hello **Azure** и разверните **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="381e7-387">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="381e7-388">Если вы видите **входа tooVisual Studio**, введите hello **учетной записи** связанный с подпиской Azure и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-388">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="381e7-389">Введите **пароль** и нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="381e7-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="381e7-390">Visual Studio предпринимает tooget сведения о всех фабрик данных Azure в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="381e7-390">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="381e7-391">Состояние данной операции в hello hello **список задач фабрики данных** окна.</span><span class="sxs-lookup"><span data-stu-id="381e7-391">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Обозреватель серверов](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="381e7-393">Щелкните правой кнопкой мыши фабрику данных и выберите **tooNew экспорта фабрики данных проекта** toocreate проект Visual Studio основан на существующей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-393">You can right-click a data factory, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Экспорт фабрики данных](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="381e7-395">Обновление средств фабрик данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381e7-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="381e7-396">средства tooupdate фабрики данных Azure для Visual Studio hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="381e7-396">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="381e7-397">Нажмите кнопку **средства** hello меню и выберите пункт **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="381e7-397">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="381e7-398">Выберите **обновления** в hello левой панели, а затем выберите **коллекции Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="381e7-398">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="381e7-399">Выберите **Azure Data Factory tools for Visual Studio** (Средства фабрики данных Azure для Visual Studio) и нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="381e7-400">Если эта запись отсутствует, уже hello последнюю версию средств hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-400">If you do not see this entry, you already have hello latest version of hello tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="381e7-401">Использование файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="381e7-401">Use configuration files</span></span>
<span data-ttu-id="381e7-402">Файлы конфигурации в свойствах tooconfigure Visual Studio можно использовать для связанной службы, таблицы и конвейеры по-разному для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="381e7-402">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="381e7-403">Рассмотрим следующие определения JSON для связанной службой хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-403">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="381e7-404">toospecify **connectionString** с различными значениями для accountname и accountkey в зависимости от среды (разработки или тестирования и рабочего) toowhich hello развертывании сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-404">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="381e7-405">Это можно сделать с помощью отдельного файла конфигурации для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="381e7-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="381e7-406">Добавление файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="381e7-406">Add a configuration file</span></span>
<span data-ttu-id="381e7-407">Добавьте файл конфигурации для каждой среды, выполнив следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-407">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="381e7-408">Щелкните правой кнопкой мыши hello фабрики данных проекта в решении Visual Studio, выберите пункт слишком**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="381e7-408">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="381e7-409">Выберите **Config** выберите из списка установленных шаблонов слева hello hello **файла конфигурации**, введите **имя** для hello конфигурации файла и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="381e7-409">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Добавление файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="381e7-411">Добавление параметров конфигурации и их значений в кодировке hello:</span><span class="sxs-lookup"><span data-stu-id="381e7-411">Add configuration parameters and their values in hello following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="381e7-412">В этом примере настраивается свойство connectionString связанной службы хранилища Azure и связанной службы Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="381e7-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="381e7-413">Обратите внимание, что hello синтаксис для указания имени [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="381e7-413">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="381e7-414">Если JSON имеет свойство, которое содержит массив значений, как показано на hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="381e7-414">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="381e7-415">Настройте свойства, как показано в hello следующий файл конфигурации (Используйте индексацию с нуля).</span><span class="sxs-lookup"><span data-stu-id="381e7-415">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="381e7-416">Имена свойств c пробелами</span><span class="sxs-lookup"><span data-stu-id="381e7-416">Property names with spaces</span></span>
<span data-ttu-id="381e7-417">Если имя свойства содержит пробелы, используйте квадратные скобки, как показано в hello в следующем примере (имя сервера базы данных):</span><span class="sxs-lookup"><span data-stu-id="381e7-417">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="381e7-418">Развертывание решения с помощью конфигурации</span><span class="sxs-lookup"><span data-stu-id="381e7-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="381e7-419">При публикации сущностей фабрики данных Azure в Visual STUDIO, можно указать hello конфигурации требуется toouse для этой операции публикации.</span><span class="sxs-lookup"><span data-stu-id="381e7-419">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="381e7-420">toopublish сущности в проекте фабрики данных Azure, с помощью файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="381e7-420">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="381e7-421">Щелкните правой кнопкой мыши проект в фабрике данных и нажмите кнопку **публикации** toosee hello **публиковать элементы** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="381e7-421">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="381e7-422">Выберите существующую фабрику данных или указать значения для создания фабрики данных hello **фабрики данных Настройка** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="381e7-422">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="381e7-423">На hello **публиковать элементы** страницы: отображается список раскрывающегося списка с конфигурации для hello **выбора конфигурации развертывания** поля.</span><span class="sxs-lookup"><span data-stu-id="381e7-423">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Выбор файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="381e7-425">Выберите hello **файла конфигурации** , необходимо будет toouse и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="381e7-425">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="381e7-426">Убедитесь, что это имя hello файла JSON в hello **Сводка** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="381e7-426">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="381e7-427">Нажмите кнопку **Готово** после завершения операции развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-427">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="381e7-428">При развертывании, hello значения из файла конфигурации hello: используется tooset значения свойств в файлах JSON hello, прежде чем сущностей hello развернутой tooAzure служба фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-428">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="381e7-429">Использование хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="381e7-429">Use Azure Key Vault</span></span>
<span data-ttu-id="381e7-430">Это не рекомендуется и часто безопасности политики toocommit конфиденциальных данных, таких как репозиторий кода toohello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="381e7-430">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="381e7-431">В разделе [ADF Secure публикации](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) на GitHub toolearn о хранение конфиденциальных сведений в хранилище ключей Azure и его использования при публикации сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="381e7-432">Hello Secure публикации расширения для Visual Studio позволяет toobe hello секретные данные, хранящиеся в хранилище ключей и только ссылки на toothem указываются в связанных служб или конфигураций развертывания.</span><span class="sxs-lookup"><span data-stu-id="381e7-432">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="381e7-433">Эти ссылки разрешаются во время публикации tooAzure сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-433">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="381e7-434">Эти файлы затем могут быть зафиксированы toosource репозитория без предоставления никакую конфиденциальную информацию.</span><span class="sxs-lookup"><span data-stu-id="381e7-434">These files can then be committed toosource repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="381e7-435">Сводка</span><span class="sxs-lookup"><span data-stu-id="381e7-435">Summary</span></span>
<span data-ttu-id="381e7-436">В этом учебнике вы создали данных tooprocess фабрики данных Azure, выполнив скрипт Hive в кластере HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="381e7-436">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="381e7-437">Вы использовали hello редактор фабрики данных в Azure портала toodo hello hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="381e7-437">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="381e7-438">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="381e7-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="381e7-439">создание двух **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="381e7-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="381e7-440">**Хранилище Azure** связанные toolink службы хранилища больших двоичных объектов Azure, содержащий фабрики данных toohello ввода вывода файлов.</span><span class="sxs-lookup"><span data-stu-id="381e7-440">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="381e7-441">**Azure HDInsight** связанная служба toolink по требованию фабрикой по требованию toohello кластера HDInsight Hadoop данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-441">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="381e7-442">Фабрика данных Azure создает HDInsight Hadoop кластера tooprocess just-in-time входных данных и создают выходных данных.</span><span class="sxs-lookup"><span data-stu-id="381e7-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="381e7-443">Создать два **наборы данных**, которые описывают входных и выходных данных для действие Hive в HDInsight из конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="381e7-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="381e7-444">Создание **конвейера** с действием **HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="381e7-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="381e7-445">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="381e7-445">Next Steps</span></span>
<span data-ttu-id="381e7-446">В этой статье вы создали конвейер с действием преобразования (действие HDInsight), которое выполняет сценарий Hive в кластере HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="381e7-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="381e7-447">toosee toouse toocopy действие копирования данных из больших двоичных объектов Azure tooAzure SQL, в статье [учебника: копирование данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-447">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="381e7-448">Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="381e7-448">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="381e7-449">Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="381e7-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="381e7-450">См. также</span><span class="sxs-lookup"><span data-stu-id="381e7-450">See Also</span></span>
| <span data-ttu-id="381e7-451">Раздел</span><span class="sxs-lookup"><span data-stu-id="381e7-451">Topic</span></span> | <span data-ttu-id="381e7-452">Описание</span><span class="sxs-lookup"><span data-stu-id="381e7-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="381e7-453">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="381e7-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="381e7-454">Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct управляемые данными рабочие процессы сценария или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="381e7-454">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="381e7-455">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="381e7-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="381e7-456">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="381e7-457">Действия по преобразованию данных</span><span class="sxs-lookup"><span data-stu-id="381e7-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="381e7-458">В этой статье рассматриваются действия по преобразованию данных (например, преобразование HDInsight Hive, используемое в этом руководстве), поддерживаемые фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="381e7-459">Планирование и исполнение с использованием фабрики данных</span><span class="sxs-lookup"><span data-stu-id="381e7-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="381e7-460">В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="381e7-460">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="381e7-461">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="381e7-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="381e7-462">В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="381e7-462">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
