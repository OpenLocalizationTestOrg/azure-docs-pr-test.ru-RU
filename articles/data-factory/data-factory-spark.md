---
title: "Вызов программ Spark из фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как вызывать программы Spark из фабрики данных Azure с помощью действия MapReduce."
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
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="ea090-103">Вызов программ Spark из конвейеров фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="ea090-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ea090-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="ea090-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="ea090-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="ea090-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ea090-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="ea090-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ea090-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="ea090-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ea090-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="ea090-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ea090-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ea090-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ea090-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ea090-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ea090-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="ea090-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ea090-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ea090-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ea090-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="ea090-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="ea090-114">Введение</span><span class="sxs-lookup"><span data-stu-id="ea090-114">Introduction</span></span>
<span data-ttu-id="ea090-115">Действие Spark — это одно из [действий преобразования данных](data-factory-data-transformation-activities.md), которое поддерживает фабрика данных Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="ea090-116">Это действие запускает указанную программу Spark в кластере Apache Spark в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea090-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="ea090-117">Действие Spark не поддерживает кластеры HDInsight Spark, использующие Azure Data Lake Store в качестве основного хранилища.</span><span class="sxs-lookup"><span data-stu-id="ea090-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="ea090-118">Оно поддерживает только существующие (собственные) кластеры HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="ea090-119">Связанная служба HDInsight по запросу не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ea090-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="ea090-120">Пошаговое руководство по созданию конвейера с действием Spark</span><span class="sxs-lookup"><span data-stu-id="ea090-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="ea090-121">Ниже приведены стандартные действия, необходимые для создания конвейера фабрики данных с действием Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="ea090-122">Создадите фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-122">Create a data factory.</span></span>
2. <span data-ttu-id="ea090-123">Создайте связанную службу хранилища Azure для связи хранилища Azure, которые связано с кластером HDInsight Spark, с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="ea090-124">Создайте связанную службу Azure HDInsight, чтобы связать кластер Apache Spark в Azure HDInsight с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="ea090-125">Создайте набор данных, который ссылается на связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="ea090-126">Затем определите выходной набор данных для действия, даже если выходные данные не выдаются.</span><span class="sxs-lookup"><span data-stu-id="ea090-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="ea090-127">Создайте конвейер с действием Spark, который ссылается на связанную службу HDInsight, созданную на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="ea090-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="ea090-128">Конфигурация действия выполняется на основе набора данных, созданного на предыдущем шаге в качестве выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="ea090-129">На основе этого набора настраивается расписание (ежечасно, ежедневно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ea090-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ea090-130">Исходя из сказанного выше, вы должны определить выходной набор данных, даже если действие не выдает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ea090-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ea090-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea090-131">Prerequisites</span></span>
1. <span data-ttu-id="ea090-132">Создайте **учетную запись хранения Azure общего назначения**, следуя указаниям в [этом разделе](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ea090-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="ea090-133">Создайте **кластер Apache Spark в Azure HDInsight**, следуя инструкциям в [этом руководстве](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ea090-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="ea090-134">Свяжите учетную запись хранения Azure, созданную на шаге 1, с этим кластером.</span><span class="sxs-lookup"><span data-stu-id="ea090-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="ea090-135">Скачайте и просмотрите файл скрипта Python **test.py**, который расположен по адресу: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="ea090-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="ea090-136">Отправьте файл **test.py** в папку **pyFiles** контейнера **adfspark** в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="ea090-137">Создайте контейнер и папку, если их нет.</span><span class="sxs-lookup"><span data-stu-id="ea090-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="ea090-138">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="ea090-138">Create data factory</span></span>
<span data-ttu-id="ea090-139">Начнем с создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="ea090-140">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ea090-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ea090-141">Щелкните **Создать** в меню слева, выберите **Данные+аналитика** и щелкните **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="ea090-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="ea090-142">В колонке **Новая фабрика данных** введите в поле "Имя" **SProcDF**.</span><span class="sxs-lookup"><span data-stu-id="ea090-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ea090-143">Имя фабрики данных Azure должно быть **глобально уникальным**.</span><span class="sxs-lookup"><span data-stu-id="ea090-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="ea090-144">Если появится сообщение об ошибке **Имя GetStartedDF фабрики данных недоступно**,</span><span class="sxs-lookup"><span data-stu-id="ea090-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="ea090-145">измените это имя (например, на ваше_имя_SparkDFdate) и попробуйте создать ее снова.</span><span class="sxs-lookup"><span data-stu-id="ea090-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="ea090-146">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="ea090-147">Выберите **подписку Azure** , в рамках которой вы хотите создать фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="ea090-148">Выберите существующую **группу ресурсов** Azure или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="ea090-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="ea090-149">Кроме того, выберите **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="ea090-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="ea090-150">В колонке **Создание фабрики данных** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ea090-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ea090-151">Создавать экземпляры фабрики данных может пользователь с ролью [Участник фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) на уровне подписки или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea090-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="ea090-152">Созданная фабрика данных появится на **панели мониторинга** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="ea090-153">Ее содержимое отобразится на соответствующей странице.</span><span class="sxs-lookup"><span data-stu-id="ea090-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="ea090-154">Если страница фабрики данных не отображается, щелкните плитку вашей фабрики данных на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ea090-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Колонка "Фабрика данных"](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="ea090-156">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="ea090-156">Create linked services</span></span>
<span data-ttu-id="ea090-157">На этом шаге вы создадите две связанные службы: одну — для связи с фабрикой данных кластера Spark, а вторую — хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ea090-158">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="ea090-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="ea090-159">На этом шаге вы свяжете учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="ea090-160">Набор данных, который вы создадите на следующем шаге этого пошагового руководства, относится к этой связанной службе,</span><span class="sxs-lookup"><span data-stu-id="ea090-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="ea090-161">как и связанная служба HDInsight, которую вы определите на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="ea090-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="ea090-162">Щелкните **Создать и развернуть** в колонке **Фабрика данных** вашей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="ea090-163">Откроется редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="ea090-164">Щелкните **Новое хранилище данных** и выберите пункт **Служба хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="ea090-164">Click **New data store** and choose **Azure storage**.</span></span>

   !["Новое хранилище данных" — пункт меню "Служба хранилища Azure"](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="ea090-166">В редакторе отобразится **скрипт JSON** для создания связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Связанная служба хранения Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="ea090-168">Замените **имя учетной записи**  и **ключ учетной записи** значениями имени и ключа учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="ea090-169">Сведения о получении, просмотре, копировании и повторном создании ключей доступа к хранилищу см. в разделе [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ea090-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="ea090-170">Чтобы развернуть связанную службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="ea090-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="ea090-171">После развертывания связанной службы окно **Draft-1** должно исчезнуть, а в представлении в виде дерева слева отобразится служба **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ea090-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="ea090-172">Создание связанной службы HDInsight</span><span class="sxs-lookup"><span data-stu-id="ea090-172">Create HDInsight linked service</span></span>
<span data-ttu-id="ea090-173">На этом шаге вы создадите связанную службу Azure HDInsight, чтобы связать кластер HDInsight Spark с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="ea090-174">В этом примере кластер HDInsight используется для выполнения программы Spark, указанной в действии Spark конвейера.</span><span class="sxs-lookup"><span data-stu-id="ea090-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="ea090-175">Нажмите **... Еще** на панели инструментов, выберите **Новое вычисление**, а затем щелкните **Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ea090-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Создание связанной службы HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="ea090-177">Вставьте следующий фрагмент в окно **Draft-1** .</span><span class="sxs-lookup"><span data-stu-id="ea090-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="ea090-178">В редакторе JSON выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ea090-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="ea090-179">укажите **URI** для кластера HDInsight Spark;</span><span class="sxs-lookup"><span data-stu-id="ea090-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="ea090-180">Например, `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="ea090-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="ea090-181">укажите имя **пользователя**, имеющего доступ к кластеру Spark;</span><span class="sxs-lookup"><span data-stu-id="ea090-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="ea090-182">укажите **пароль** для пользователя;</span><span class="sxs-lookup"><span data-stu-id="ea090-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="ea090-183">укажите **связанную службу хранилища Azure**, которая связана с кластером HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ea090-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="ea090-184">(в этом примере это **AzureStorageLinkedService**).</span><span class="sxs-lookup"><span data-stu-id="ea090-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="ea090-185">Действие Spark не поддерживает кластеры HDInsight Spark, использующие Azure Data Lake Store в качестве основного хранилища.</span><span class="sxs-lookup"><span data-stu-id="ea090-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="ea090-186">Оно поддерживает только существующие (собственные) кластеры HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="ea090-187">Связанная служба HDInsight по запросу не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ea090-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="ea090-188">Подробные сведения о связанной службе HDInsight см. [в этом разделе](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ea090-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="ea090-189">Чтобы развернуть связанную службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="ea090-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="ea090-190">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="ea090-190">Create output dataset</span></span>
<span data-ttu-id="ea090-191">На основе этого набора настраивается расписание (ежечасно, ежедневно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ea090-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ea090-192">Исходя из сказанного выше, вы должны определить выходной набор данных для действия Spark в конвейере, даже если действие не создает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ea090-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="ea090-193">Указание входного набора данных для действия необязательно.</span><span class="sxs-lookup"><span data-stu-id="ea090-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="ea090-194">В **редакторе фабрики данных** нажмите кнопку **... Еще** на панели команд, щелкните **Новый набор данных** и выберите **Хранилище больших двоичных объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="ea090-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="ea090-195">Вставьте следующий фрагмент в окно Draft-1.</span><span class="sxs-lookup"><span data-stu-id="ea090-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="ea090-196">Этот фрагмент кода JSON определяет набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ea090-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="ea090-197">Кроме того, нужно указать, что результаты будут храниться в контейнере больших двоичных объектов **adfspark** и в папке **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="ea090-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="ea090-198">Как упоминалось ранее, это фиктивный набор данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="ea090-199">В этом примере программа Spark не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="ea090-200">В разделе **availability** указывается частота, с которой ежедневно будет создаваться выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="ea090-201">Чтобы развернуть набор данных, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="ea090-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="ea090-202">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="ea090-202">Create pipeline</span></span>
<span data-ttu-id="ea090-203">На этом шаге создается конвейер с действием **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ea090-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="ea090-204">В настоящее время расписание активируется с помощью выходного набора данных, поэтому его необходимо создать, даже если действие не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="ea090-205">Если действие не принимает никаких входных данных, входной набор данных можно не создавать.</span><span class="sxs-lookup"><span data-stu-id="ea090-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="ea090-206">Таким образом, в этом примере входной набор данных не указывается.</span><span class="sxs-lookup"><span data-stu-id="ea090-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="ea090-207">В **редакторе фабрики данных** щелкните **Еще** и выберите **Новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="ea090-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="ea090-208">Замените скрипт в окне Draft-1 следующим скриптом:</span><span class="sxs-lookup"><span data-stu-id="ea090-208">Replace the script in the Draft-1 window with the following script:</span></span>

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
    <span data-ttu-id="ea090-209">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="ea090-209">Note the following points:</span></span>
    - <span data-ttu-id="ea090-210">Свойству **type** присваивается значение **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ea090-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="ea090-211">Свойству **rootPath** присваивается значение **adfspark\\pyFiles**, где adfspark — контейнер больших двоичных объектов Azure, а pyFiles — папка с файлами в этом контейнере.</span><span class="sxs-lookup"><span data-stu-id="ea090-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="ea090-212">В этом примере хранилище BLOB-объектов Azure связано с кластером Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="ea090-213">Файл можно отправить в другое хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="ea090-214">Чтобы сделать это, создайте связанную службу хранилища Azure, которая свяжет эту учетную запись хранения с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="ea090-215">Затем укажите имя связанной службы в качестве значения свойства **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ea090-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="ea090-216">Сведения об этом свойстве и других свойствах, поддерживаемых действием Spark, см. в [этом разделе](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ea090-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="ea090-217">Свойству **entryFilePath** присваивается значение **test.py**, которое является файлом Python.</span><span class="sxs-lookup"><span data-stu-id="ea090-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="ea090-218">Свойству **getDebugInfo** присваивается значение **Always**. Так файлы журналов будут создаваться постоянно (успешные и неудачные события).</span><span class="sxs-lookup"><span data-stu-id="ea090-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="ea090-219">Если вы не устраняете неполадки, советуем не устанавливать для этого свойства значение `Always` в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ea090-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="ea090-220">В разделе **outputs** содержится один выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="ea090-221">Вы должны определить выходной набор данных, даже если программа Spark не выдает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ea090-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="ea090-222">На основе этого набора настраивается расписание конвейера (ежечасно, ежедневно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ea090-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="ea090-223">Сведения о свойствах, поддерживаемых действием Spark, см. в [этом разделе](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ea090-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="ea090-224">Чтобы развернуть конвейер, на панели команд нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="ea090-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="ea090-225">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="ea090-225">Monitor pipeline</span></span>
1. <span data-ttu-id="ea090-226">Щелкните **X**, чтобы закрыть колонки редактора фабрики данных и вернуться на домашнюю страницу фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="ea090-227">Щелкните **Мониторинг и управление** для запуска приложения мониторинга на другой вкладке.</span><span class="sxs-lookup"><span data-stu-id="ea090-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![Плитка "Мониторинг и управление"](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="ea090-229">Вверху укажите для фильтра **Время начала** дату **01.02.2017** и нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="ea090-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="ea090-230">Вы должны видеть только одно окно действия, так как между временем начала (01.02.2017) и окончания (02.02.2017) конвейера всего один день.</span><span class="sxs-lookup"><span data-stu-id="ea090-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="ea090-231">Убедитесь, что срез данных находится в состоянии **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ea090-231">Confirm that the data slice is in **ready** state.</span></span>

    ![Мониторинг конвейера](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="ea090-233">Выберите **окно действия** для просмотра подробной информации о выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="ea090-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="ea090-234">В случае ошибки в области справа будут отображаться детали.</span><span class="sxs-lookup"><span data-stu-id="ea090-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="ea090-235">Проверка результатов</span><span class="sxs-lookup"><span data-stu-id="ea090-235">Verify the results</span></span>

1. <span data-ttu-id="ea090-236">Запустите **записную книжку Jupyter** для кластера HDInsight Spark, перейдя по адресу: https://имя_кластера.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="ea090-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="ea090-237">Можно также сначала запустить панель мониторинга для кластера HDInsight Spark, а затем запустить **записную книжку Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="ea090-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="ea090-238">Щелкните **Создать** -> **PySpark**, чтобы создать новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="ea090-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Новая записная книжка Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="ea090-240">Выполните следующую команду, скопировав и вставив текст и нажав **SHIFT+ENTER** в конец второй инструкции.</span><span class="sxs-lookup"><span data-stu-id="ea090-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="ea090-241">Убедитесь, что вы видите данные из таблицы hvac:</span><span class="sxs-lookup"><span data-stu-id="ea090-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Результаты запроса Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="ea090-243">Подробные инструкции см. в разделе [Выполнение запроса Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql).</span><span class="sxs-lookup"><span data-stu-id="ea090-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="ea090-244">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="ea090-244">Troubleshooting</span></span>
<span data-ttu-id="ea090-245">Так как вы задали для **getDebugInfo** значение **Always**, вы увидите вложенную папку **log** в папке **pyFiles** в контейнере больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ea090-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="ea090-246">В файле журнала в папке log содержатся дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="ea090-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="ea090-247">Этот файл журнала особенно полезен в случае возникновения ошибки.</span><span class="sxs-lookup"><span data-stu-id="ea090-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="ea090-248">В рабочей среде вы можете настроить состояние ошибки **Failure**.</span><span class="sxs-lookup"><span data-stu-id="ea090-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="ea090-249">Для дальнейшего устранения неполадок выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ea090-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="ea090-250">Перейдите на страницу `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="ea090-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Приложение пользовательского интерфейса YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="ea090-252">Щелкните **Журналы** для одной из попыток выполнения.</span><span class="sxs-lookup"><span data-stu-id="ea090-252">Click **Logs** for one of the run attempts.</span></span>

    ![Страница приложения](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="ea090-254">Вы должны увидеть дополнительные сведения об ошибке на странице журнала.</span><span class="sxs-lookup"><span data-stu-id="ea090-254">You should see additional error information in the log page.</span></span>

    ![Описание ошибки в журнале](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="ea090-256">В следующих разделах приведены сведения о сущностях фабрики данных, необходимых для использования кластера Apache Spark и действия Spark в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="ea090-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="ea090-257">Свойства действия Spark</span><span class="sxs-lookup"><span data-stu-id="ea090-257">Spark activity properties</span></span>
<span data-ttu-id="ea090-258">Ниже приведен пример определения JSON конвейера с действием Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="ea090-259">В следующей таблице приведено описание свойств, используемых в определении JSON.</span><span class="sxs-lookup"><span data-stu-id="ea090-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="ea090-260">Свойство</span><span class="sxs-lookup"><span data-stu-id="ea090-260">Property</span></span> | <span data-ttu-id="ea090-261">Описание</span><span class="sxs-lookup"><span data-stu-id="ea090-261">Description</span></span> | <span data-ttu-id="ea090-262">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ea090-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ea090-263">name</span><span class="sxs-lookup"><span data-stu-id="ea090-263">name</span></span> | <span data-ttu-id="ea090-264">Имя действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="ea090-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="ea090-265">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-265">Yes</span></span> |
| <span data-ttu-id="ea090-266">description</span><span class="sxs-lookup"><span data-stu-id="ea090-266">description</span></span> | <span data-ttu-id="ea090-267">Описание действия.</span><span class="sxs-lookup"><span data-stu-id="ea090-267">Text describing what the activity does.</span></span> | <span data-ttu-id="ea090-268">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-268">No</span></span> |
| <span data-ttu-id="ea090-269">type</span><span class="sxs-lookup"><span data-stu-id="ea090-269">type</span></span> | <span data-ttu-id="ea090-270">Для этого свойства необходимо задать значение HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="ea090-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="ea090-271">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-271">Yes</span></span> |
| <span data-ttu-id="ea090-272">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="ea090-272">linkedServiceName</span></span> | <span data-ttu-id="ea090-273">Имя связанной службы HDInsight, в которой выполняется программа Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="ea090-274">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-274">Yes</span></span> |
| <span data-ttu-id="ea090-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="ea090-275">rootPath</span></span> | <span data-ttu-id="ea090-276">Контейнер BLOB-объектов Azure и папка, содержащая файл Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="ea090-277">В имени файла учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="ea090-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="ea090-278">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-278">Yes</span></span> |
| <span data-ttu-id="ea090-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="ea090-279">entryFilePath</span></span> | <span data-ttu-id="ea090-280">Относительный путь к корневой папке пакета и кода Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="ea090-281">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-281">Yes</span></span> |
| <span data-ttu-id="ea090-282">className</span><span class="sxs-lookup"><span data-stu-id="ea090-282">className</span></span> | <span data-ttu-id="ea090-283">Основной класс Java или Spark приложения.</span><span class="sxs-lookup"><span data-stu-id="ea090-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="ea090-284">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-284">No</span></span> |
| <span data-ttu-id="ea090-285">arguments</span><span class="sxs-lookup"><span data-stu-id="ea090-285">arguments</span></span> | <span data-ttu-id="ea090-286">Список аргументов командной строки для программы Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="ea090-287">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-287">No</span></span> |
| <span data-ttu-id="ea090-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="ea090-288">proxyUser</span></span> | <span data-ttu-id="ea090-289">Учетная запись пользователя для олицетворения, используемая для выполнения программы Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="ea090-290">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-290">No</span></span> |
| <span data-ttu-id="ea090-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="ea090-291">sparkConfig</span></span> | <span data-ttu-id="ea090-292">Укажите значения для свойств конфигурации Spark, перечисленных в разделе [Конфигурация Spark — свойства приложения](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="ea090-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="ea090-293">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-293">No</span></span> |
| <span data-ttu-id="ea090-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="ea090-294">getDebugInfo</span></span> | <span data-ttu-id="ea090-295">Указывает, когда файлы журнала Spark копируются в службу хранилища Azure, используемое кластером HDInsight или определенное sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ea090-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="ea090-296">Допустимые значения: None, Always или Failure.</span><span class="sxs-lookup"><span data-stu-id="ea090-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="ea090-297">Значение по умолчанию: None.</span><span class="sxs-lookup"><span data-stu-id="ea090-297">Default value: None.</span></span> | <span data-ttu-id="ea090-298">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-298">No</span></span> |
| <span data-ttu-id="ea090-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="ea090-299">sparkJobLinkedService</span></span> | <span data-ttu-id="ea090-300">Связанная служба службы хранилища Azure, в которой хранятся файл задания Spark, зависимости и журналы.</span><span class="sxs-lookup"><span data-stu-id="ea090-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="ea090-301">Если значение этого свойства не указано, используется хранилище, связанное с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea090-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="ea090-302">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="ea090-303">Структура папок</span><span class="sxs-lookup"><span data-stu-id="ea090-303">Folder structure</span></span>
<span data-ttu-id="ea090-304">Действие Spark не поддерживает встроенный сценарий, в отличие от действий Pig и Hive.</span><span class="sxs-lookup"><span data-stu-id="ea090-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="ea090-305">Задания Spark также обеспечивают большую гибкость, чем задания Pig и Hive.</span><span class="sxs-lookup"><span data-stu-id="ea090-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="ea090-306">Для заданий Spark можно указать несколько зависимостей, например пакеты JAR (размещаются в CLASSPATH Java), файлы Python (размещаются в PYTHONPATH) и другие файлы.</span><span class="sxs-lookup"><span data-stu-id="ea090-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="ea090-307">Создайте следующую структуру папок в хранилище BLOB-объектов Azure, на которое ссылается связанная служба HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea090-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="ea090-308">Затем передайте зависимые файлы в соответствующие вложенные папки в корневой папке, определенной значением **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="ea090-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="ea090-309">Например, передайте файлы Python во вложенную папку pyFiles, а JAR-файлы — во вложенную папку jars, расположенный в корневой папке.</span><span class="sxs-lookup"><span data-stu-id="ea090-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="ea090-310">Во время выполнения служба фабрики данных ожидает в хранилище BLOB-объектов Azure следующую структуру папок.</span><span class="sxs-lookup"><span data-stu-id="ea090-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="ea090-311">Путь</span><span class="sxs-lookup"><span data-stu-id="ea090-311">Path</span></span> | <span data-ttu-id="ea090-312">Описание</span><span class="sxs-lookup"><span data-stu-id="ea090-312">Description</span></span> | <span data-ttu-id="ea090-313">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ea090-313">Required</span></span> | <span data-ttu-id="ea090-314">Тип</span><span class="sxs-lookup"><span data-stu-id="ea090-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="ea090-315">.</span><span class="sxs-lookup"><span data-stu-id="ea090-315">.</span></span> | <span data-ttu-id="ea090-316">Путь к корневому каталогу задания Spark в хранилище связанной службы.</span><span class="sxs-lookup"><span data-stu-id="ea090-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="ea090-317">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-317">Yes</span></span> | <span data-ttu-id="ea090-318">Папка</span><span class="sxs-lookup"><span data-stu-id="ea090-318">Folder</span></span> |
| <span data-ttu-id="ea090-319">&lt;Определяется пользователем&gt;</span><span class="sxs-lookup"><span data-stu-id="ea090-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="ea090-320">Путь к файлу записи задания Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="ea090-321">Да</span><span class="sxs-lookup"><span data-stu-id="ea090-321">Yes</span></span> | <span data-ttu-id="ea090-322">Файл</span><span class="sxs-lookup"><span data-stu-id="ea090-322">File</span></span> |
| <span data-ttu-id="ea090-323">./jars</span><span class="sxs-lookup"><span data-stu-id="ea090-323">./jars</span></span> | <span data-ttu-id="ea090-324">Все файлы в этой папке передаются и помещаются в папку CLASSPATH Java для кластера.</span><span class="sxs-lookup"><span data-stu-id="ea090-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="ea090-325">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-325">No</span></span> | <span data-ttu-id="ea090-326">Папка</span><span class="sxs-lookup"><span data-stu-id="ea090-326">Folder</span></span> |
| <span data-ttu-id="ea090-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="ea090-327">./pyFiles</span></span> | <span data-ttu-id="ea090-328">Все файлы в этой папке передаются и помещаются в папку PYTHONPATH для кластера.</span><span class="sxs-lookup"><span data-stu-id="ea090-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="ea090-329">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-329">No</span></span> | <span data-ttu-id="ea090-330">Папка</span><span class="sxs-lookup"><span data-stu-id="ea090-330">Folder</span></span> |
| <span data-ttu-id="ea090-331">./files</span><span class="sxs-lookup"><span data-stu-id="ea090-331">./files</span></span> | <span data-ttu-id="ea090-332">Все файлы в этой папке передаются и помещаются в рабочий каталог исполнителя.</span><span class="sxs-lookup"><span data-stu-id="ea090-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="ea090-333">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-333">No</span></span> | <span data-ttu-id="ea090-334">Папка</span><span class="sxs-lookup"><span data-stu-id="ea090-334">Folder</span></span> |
| <span data-ttu-id="ea090-335">./archives</span><span class="sxs-lookup"><span data-stu-id="ea090-335">./archives</span></span> | <span data-ttu-id="ea090-336">Все файлы в этой папке не сжаты.</span><span class="sxs-lookup"><span data-stu-id="ea090-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="ea090-337">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-337">No</span></span> | <span data-ttu-id="ea090-338">Папка</span><span class="sxs-lookup"><span data-stu-id="ea090-338">Folder</span></span> |
| <span data-ttu-id="ea090-339">./logs</span><span class="sxs-lookup"><span data-stu-id="ea090-339">./logs</span></span> | <span data-ttu-id="ea090-340">Папка, в которой хранятся журналы из кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="ea090-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="ea090-341">Нет</span><span class="sxs-lookup"><span data-stu-id="ea090-341">No</span></span> | <span data-ttu-id="ea090-342">Папка</span><span class="sxs-lookup"><span data-stu-id="ea090-342">Folder</span></span> |

<span data-ttu-id="ea090-343">Ниже приведен пример хранилища, содержащего два файла заданий Spark в хранилище BLOB-объектов Azure, на которое ссылается связанная служба HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea090-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

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
