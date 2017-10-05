---
title: "Использование настраиваемых действий в конвейере фабрики данных Azure"
description: "Узнайте, как создавать пользовательские действия и использовать их в конвейере фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="179e2-103">Использование настраиваемых действий в конвейере фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="179e2-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="179e2-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="179e2-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="179e2-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="179e2-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="179e2-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="179e2-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="179e2-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="179e2-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="179e2-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="179e2-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="179e2-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="179e2-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="179e2-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="179e2-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="179e2-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="179e2-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="179e2-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="179e2-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="179e2-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="179e2-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="179e2-114">Существует два типа действий, которые можно использовать в конвейере фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="179e2-115">[Действия перемещения данных](data-factory-data-movement-activities.md) для перемещения данных между [поддерживаемыми исходными хранилищами данных и хранилищами данных-приемниками](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="179e2-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="179e2-116">[Действия преобразования данных](data-factory-data-transformation-activities.md) для преобразования данных с помощью служб вычислений, например: в Azure HDInsight, пакетной службе Azure и Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="179e2-117">Чтобы переместить данные из хранилища данных, которое не поддерживает фабрика данных Azure, или в такое хранилище, можно создать **пользовательское действие** с собственной логикой перемещения данных и использовать это действие в конвейере.</span><span class="sxs-lookup"><span data-stu-id="179e2-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="179e2-118">Аналогично, чтобы преобразовать или обработать данные способом, который не поддерживается фабрикой данных Azure, создайте пользовательское действие с собственной логикой преобразования данных и используйте это действие в конвейере.</span><span class="sxs-lookup"><span data-stu-id="179e2-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="179e2-119">Вы можете настроить запуск пользовательского действия в пуле виртуальных машин **пакетной службы Azure** или в кластере **Azure HDInsight** на базе Windows.</span><span class="sxs-lookup"><span data-stu-id="179e2-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="179e2-120">При использовании пакетной службы Azure можно использовать только имеющийся пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="179e2-121">А при использовании HDInsight можно применить имеющийся кластер HDInsight или кластер, который автоматически создается для вас по запросу в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="179e2-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="179e2-122">В следующем руководстве содержатся пошаговые инструкции по созданию пользовательского действия .NET и его использованию в конвейере.</span><span class="sxs-lookup"><span data-stu-id="179e2-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="179e2-123">В этом пошаговом руководстве используется связанная **пакетная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="179e2-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="179e2-124">Чтобы вместо нее использовалась связанная служба Azure HDInsight, создайте связанную службу типа **HDInsight** (ваш кластер HDInsight) или **HDInsightOnDemand** (фабрика данных создает кластер HDInsight по запросу).</span><span class="sxs-lookup"><span data-stu-id="179e2-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="179e2-125">Затем настройте пользовательское действие для использования связанной службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="179e2-126">Дополнительные сведения об использовании Azure HDInsight для выполнения пользовательского действия приведены в разделе [Использование связанных служб Azure HDInsight](#use-hdinsight-compute-service) .</span><span class="sxs-lookup"><span data-stu-id="179e2-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="179e2-127">Пользовательские действия .NET выполняются только в кластерах HDInsight на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="179e2-127">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="179e2-128">Чтобы обойти это ограничение, используйте действие Map Reduce для запуска пользовательского кода Java в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="179e2-128">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="179e2-129">Другой вариант — использовать для выполнения пользовательских действий пул виртуальных машин пакетной службы Azure, а не кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-129">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="179e2-130">Невозможно использовать шлюз управления данными из пользовательского действия для доступа к локальным источникам данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-130">It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources.</span></span> <span data-ttu-id="179e2-131">В настоящее время [шлюз управления данными](data-factory-data-management-gateway.md) поддерживает действие копирования и действие хранимой процедуры только в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="179e2-132">Пошаговое руководство по созданию настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="179e2-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="179e2-133">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="179e2-133">Prerequisites</span></span>
* <span data-ttu-id="179e2-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="179e2-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="179e2-135">Скачайте и установите пакет [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="179e2-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="179e2-136">Предварительные требования для пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="179e2-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="179e2-137">В этом руководстве вы запустите свои настраиваемые действия .NET с помощью пакетной службы Azure как вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="179e2-137">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="179e2-138">**Пакетная служба Azure** — это служба платформы, которая позволяет эффективно работать с приложениями для крупномасштабных параллельных и высокопроизводительных вычислений (HPC) в облаке.</span><span class="sxs-lookup"><span data-stu-id="179e2-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="179e2-139">Пакетная служба Azure планирует запуск ресурсоемких вычислительных задач в управляемой **коллекции виртуальных машин** и автоматически масштабирует вычислительные ресурсы, учитывая требования заданий.</span><span class="sxs-lookup"><span data-stu-id="179e2-139">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="179e2-140">Подробные сведения о пакетной службе Azure см. в [этой статье][batch-technical-overview].</span><span class="sxs-lookup"><span data-stu-id="179e2-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="179e2-141">Для этого руководства создайте учетную запись пакетной службы Azure с пулом виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="179e2-141">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="179e2-142">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="179e2-142">Here are the steps:</span></span>

1. <span data-ttu-id="179e2-143">Создание **учетной записи пакетной службы Azure** на [портале Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="179e2-143">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="179e2-144">Инструкции см. в статье [Создание учетной записи пакетной службы Azure на портале Azure][batch-create-account].</span><span class="sxs-lookup"><span data-stu-id="179e2-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="179e2-145">Запишите ключ и имя учетной записи пакетной службы Azure, а также URI и имя пула.</span><span class="sxs-lookup"><span data-stu-id="179e2-145">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="179e2-146">Они понадобятся при создании связанной службы пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-146">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="179e2-147">На домашней странице учетной записи пакетной службы Azure отображается **URL-адрес** в следующем формате: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="179e2-147">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="179e2-148">В этом примере **myaccount** — это имя учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-148">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="179e2-149">URI, используемый в определении связанной службы — это URL-адрес без имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="179e2-149">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="179e2-150">Например, `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="179e2-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="179e2-151">В меню слева щелкните **Ключи** и скопируйте значение параметра **Первичный ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="179e2-151">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="179e2-152">Чтобы использовать имеющийся пул, щелкните **Пулы** в меню и запишите **идентификатор** пула.</span><span class="sxs-lookup"><span data-stu-id="179e2-152">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="179e2-153">Если у вас нет пула, перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="179e2-153">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="179e2-154">Создайте **пул пакетной службы Azure**.</span><span class="sxs-lookup"><span data-stu-id="179e2-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="179e2-155">На [портале Azure](https://portal.azure.com) щелкните **Обзор** в меню слева и выберите **Уч. записи пакетной службы**.</span><span class="sxs-lookup"><span data-stu-id="179e2-155">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="179e2-156">Выберите свою учетную запись пакетной службы Azure, чтобы открыть колонку **Учетная запись пакетной службы** .</span><span class="sxs-lookup"><span data-stu-id="179e2-156">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="179e2-157">Щелкните элемент **Пулы** .</span><span class="sxs-lookup"><span data-stu-id="179e2-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="179e2-158">В колонке **Пулы** нажмите кнопку "Добавить" на панели инструментов, чтобы добавить пул.</span><span class="sxs-lookup"><span data-stu-id="179e2-158">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="179e2-159">Введите идентификатор для пула (идентификатор пула).</span><span class="sxs-lookup"><span data-stu-id="179e2-159">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="179e2-160">Сохраните **идентификатор пула**. Он понадобится при создании решения фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-160">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="179e2-161">В качестве параметра семейства операционных систем укажите **Windows Server 2012 R2** .</span><span class="sxs-lookup"><span data-stu-id="179e2-161">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="179e2-162">Выберите **Ценовая категория для узлов**.</span><span class="sxs-lookup"><span data-stu-id="179e2-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="179e2-163">Для параметра **Выделенный целевой объект** укажите значение **2**.</span><span class="sxs-lookup"><span data-stu-id="179e2-163">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="179e2-164">Для параметра **Максимальное число заданий на узел** укажите значение **2**.</span><span class="sxs-lookup"><span data-stu-id="179e2-164">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="179e2-165">Нажмите кнопку **ОК** , чтобы создать пул.</span><span class="sxs-lookup"><span data-stu-id="179e2-165">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="179e2-166">Запишите **идентификатор** пула.</span><span class="sxs-lookup"><span data-stu-id="179e2-166">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="179e2-167">Пошаговые действия</span><span class="sxs-lookup"><span data-stu-id="179e2-167">High-level steps</span></span>
<span data-ttu-id="179e2-168">Ниже приведены два высокоуровневых шага, выполняемые в рамках этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="179e2-168">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="179e2-169">Создайте пользовательское действие, содержащее простую логику преобразования и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="179e2-170">Создайте фабрику данных Azure с конвейером, использующим пользовательское действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-170">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="179e2-171">Создать настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-171">Create a custom activity</span></span>
<span data-ttu-id="179e2-172">Чтобы создать настраиваемое действие .NET, создайте проект **библиотеки классов .NET** с классом, который реализует интерфейс **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="179e2-172">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="179e2-173">У этого интерфейса есть только один метод [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , и его сигнатура такова.</span><span class="sxs-lookup"><span data-stu-id="179e2-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="179e2-174">Метод принимает четыре параметра:</span><span class="sxs-lookup"><span data-stu-id="179e2-174">The method takes four parameters:</span></span>

- <span data-ttu-id="179e2-175">**linkedServices** —</span><span class="sxs-lookup"><span data-stu-id="179e2-175">**linkedServices**.</span></span> <span data-ttu-id="179e2-176">Это свойство является перечисляемым списком связанных служб хранилища данных, на которые ссылаются входные и выходные наборы данных для действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="179e2-177">**наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="179e2-177">**datasets**.</span></span> <span data-ttu-id="179e2-178">Это свойство является перечисляемым списком входных и выходных наборов данных для действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-178">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="179e2-179">Этот параметр можно использовать для получения расположений и схем, которые определяются входными и выходными наборами данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-179">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="179e2-180">**activity** —</span><span class="sxs-lookup"><span data-stu-id="179e2-180">**activity**.</span></span> <span data-ttu-id="179e2-181">Это свойство представляет текущее действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-181">This property represents the current activity.</span></span> <span data-ttu-id="179e2-182">Его можно использовать для доступа к расширенным свойствам, связанным с пользовательским действием.</span><span class="sxs-lookup"><span data-stu-id="179e2-182">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="179e2-183">Дополнительные сведения см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).</span><span class="sxs-lookup"><span data-stu-id="179e2-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="179e2-184">**logger** —</span><span class="sxs-lookup"><span data-stu-id="179e2-184">**logger**.</span></span> <span data-ttu-id="179e2-185">Этот объект позволяет записывать комментарии отладки, которые отображаются в виде пользовательского журнала для конвейера.</span><span class="sxs-lookup"><span data-stu-id="179e2-185">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="179e2-186">Этот метод возвращает словарь, который можно будет использовать для создания цепочки из настраиваемых действий в будущем.</span><span class="sxs-lookup"><span data-stu-id="179e2-186">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="179e2-187">Эта функция еще не реализована, поэтому из метода просто возвращается пустой словарь.</span><span class="sxs-lookup"><span data-stu-id="179e2-187">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="179e2-188">Описание процедуры</span><span class="sxs-lookup"><span data-stu-id="179e2-188">Procedure</span></span>
1. <span data-ttu-id="179e2-189">Создайте проект **библиотеки классов .NET** .</span><span class="sxs-lookup"><span data-stu-id="179e2-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="179e2-190">Запустите <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> или <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="179e2-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="179e2-191">Щелкните <b>Файл</b>, наведите указатель мыши на пункт <b>Создать</b> и щелкните <b>Проект</b>.</span><span class="sxs-lookup"><span data-stu-id="179e2-191">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="179e2-192">Разверните раздел <b>Шаблоны</b> и выберите <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="179e2-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="179e2-193">В этом руководстве используется язык C#, но для создания настраиваемого действия вы можете использовать любой язык .NET.;</span><span class="sxs-lookup"><span data-stu-id="179e2-193">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="179e2-194">Выберите тип <b>Библиотека классов</b> из списка типов проектов справа.</span><span class="sxs-lookup"><span data-stu-id="179e2-194">Select <b>Class Library</b> from the list of project types on the right.</span></span> <span data-ttu-id="179e2-195">В VS 2017 выберите <b>Библиотека классов (.NET Framework)</b> .</span><span class="sxs-lookup"><span data-stu-id="179e2-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="179e2-196">В поле <b>Имя</b> введите <b>MyDotNetActivity</b>.</span><span class="sxs-lookup"><span data-stu-id="179e2-196">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="179e2-197">В качестве <b>расположения</b> укажите <b>C:\ADFGetStarted</b>.</span><span class="sxs-lookup"><span data-stu-id="179e2-197">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="179e2-198">Нажмите кнопку <b>ОК</b> , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="179e2-198">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="179e2-199">
2. Щелкните **Инструменты**, наведите указатель мыши на пункт **Диспетчер пакетов NuGet** и щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="179e2-199">
2. Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="179e2-200">3.</span><span class="sxs-lookup"><span data-stu-id="179e2-200">3.</span></span> <span data-ttu-id="179e2-201">В консоли диспетчера пакетов выполните следующую команду, чтобы импортировать пакет **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="179e2-201">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="179e2-202">Импортируйте пакет NuGet для **службы хранилища Azure** в проект.</span><span class="sxs-lookup"><span data-stu-id="179e2-202">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="179e2-203">Средство запуска службы фабрики данных требует пакет WindowsAzure.Storage версии 4.3.</span><span class="sxs-lookup"><span data-stu-id="179e2-203">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="179e2-204">Если добавить ссылку в проекте настраиваемого действия в сборку службы хранилища Azure более поздней версии, при выполнении действия возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="179e2-204">If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes.</span></span> <span data-ttu-id="179e2-205">Чтобы устранить ее, см. раздел [Изоляция домена приложения](#appdomain-isolation).</span><span class="sxs-lookup"><span data-stu-id="179e2-205">To resolve the error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="179e2-206">Добавьте следующие инструкции с **using** в исходный файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="179e2-206">Add the following **using** statements to the source file in the project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="179e2-207">Измените имя **пространства имен** на **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="179e2-207">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="179e2-208">Измените имя класса на **MyDotNetActivity** и извлеките класс из интерфейса **IDotNetActivity**, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="179e2-208">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="179e2-209">Реализуйте (добавьте) метод **Execute** интерфейса **IDotNetActivity** для класса **MyDotNetActivity** и скопируйте следующий пример кода в этот метод.</span><span class="sxs-lookup"><span data-stu-id="179e2-209">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="179e2-210">Следующий пример подсчитывает количество вхождений поисковой фразы ("Microsoft") в каждый большой двоичный объект, связанный со срезом данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-210">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="179e2-211">Добавьте следующие вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="179e2-211">Add the following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="179e2-212">Метод GetFolderPath возвращает путь к папке, на которую указывает набор данных, а метод GetFileName — имя большого двоичного объекта или файла, на который указывает набор данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-212">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="179e2-213">Если параметр havefolderPath определяется с помощью переменных, таких как {Year}, {Month} {Day} и т. д, то метод возвращает строку как есть, не заменяя эти переменные соответствующими значениями на момент запуска.</span><span class="sxs-lookup"><span data-stu-id="179e2-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="179e2-214">Дополнительные сведения о доступе к SliceStart, SliceEnd и т. д. см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).</span><span class="sxs-lookup"><span data-stu-id="179e2-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="179e2-215">Метод Calculate вычисляет количество экземпляров ключевого слова Microsoft во входных файлах (в больших двоичных объектах в папке).</span><span class="sxs-lookup"><span data-stu-id="179e2-215">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="179e2-216">Условие поиска (Microsoft) жестко задано в коде.</span><span class="sxs-lookup"><span data-stu-id="179e2-216">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="179e2-217">Скомпилируйте проект.</span><span class="sxs-lookup"><span data-stu-id="179e2-217">Compile the project.</span></span> <span data-ttu-id="179e2-218">В меню щелкните **Построить** и **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="179e2-218">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="179e2-219">Задайте версию 4.5.2 платформы .NET Framework в качестве целевой для своего проекта: щелкните правой кнопкой мыши проект и выберите **Свойства**, чтобы задать целевую платформу.</span><span class="sxs-lookup"><span data-stu-id="179e2-219">Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework.</span></span> <span data-ttu-id="179e2-220">Фабрика данных не поддерживает настраиваемые действия, скомпилированные для более поздних версий, чем .NET Framework 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="179e2-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="179e2-221">Запустите **проводник Windows** и перейдите к папке **bin\debug** или **bin\release** в зависимости от типа сборки.</span><span class="sxs-lookup"><span data-stu-id="179e2-221">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="179e2-222">Создайте ZIP-файл **MyDotNetActivity.zip**, который содержит все двоичные файлы из папки <project folder>\bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="179e2-222">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="179e2-223">Добавьте файл **MyDotNetActivity.pdb**, чтобы в случае сбоя получить дополнительные сведения, например номер строки в исходном коде, вызвавшем ошибку.</span><span class="sxs-lookup"><span data-stu-id="179e2-223">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="179e2-224">Все файлы в ZIP-файле для настраиваемого действия должны размещаться на **верхнем уровне** без вложенных папок.</span><span class="sxs-lookup"><span data-stu-id="179e2-224">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>

    ![Двоичные выходные файлы](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="179e2-226">Создайте контейнер больших двоичных объектов **customactivitycontainer**, если он еще не создан.</span><span class="sxs-lookup"><span data-stu-id="179e2-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="179e2-227">Отправьте файл MyDotNetActivity.zip в виде BLOB-объекта в контейнер customactivitycontainer в хранилище BLOB-объектов Azure **общего назначения** (не в "горячее" или "холодное" хранилище BLOB-объектов), на которое ссылается служба AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="179e2-227">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="179e2-228">Если добавить этот проект действия .NET в решение в Visual Studio, содержащее проект фабрики данных, и добавить ссылку в проект действия .NET из проекта приложения фабрики данных, то не обязательно выполнять два последних шага по созданию ZIP-файла и его добавлению в хранилище BLOB-объектов Azure общего назначения.</span><span class="sxs-lookup"><span data-stu-id="179e2-228">If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage.</span></span> <span data-ttu-id="179e2-229">При публикации сущностей фабрики данных с помощью Visual Studio эти шаги выполняются автоматически в процессе публикации.</span><span class="sxs-lookup"><span data-stu-id="179e2-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process.</span></span> <span data-ttu-id="179e2-230">Дополнительные сведения см. в разделе [Проект фабрики данных в Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="179e2-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="179e2-231">Создание конвейера с настраиваемым действием</span><span class="sxs-lookup"><span data-stu-id="179e2-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="179e2-232">Вы создали пользовательское действие и отправили ZIP-файл с двоичными файлами в контейнер больших двоичных объектов в учетной записи хранения Azure **общего назначения**.</span><span class="sxs-lookup"><span data-stu-id="179e2-232">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="179e2-233">В этом разделе вы создадите фабрику данных Azure с конвейером, использующим пользовательское действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-233">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="179e2-234">Входной набор данных для пользовательского действия представляет собой большие двоичные объекты (файлы) в папке customactivityinput контейнера adftutorial в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="179e2-234">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="179e2-235">Выходной набор данных для пользовательского действия представляет собой выходные большие двоичные объекты в папке customactivityoutput контейнера adftutorial в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="179e2-235">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="179e2-236">Создайте файл **file.txt** со следующим содержимым, а затем отправьте его в папку **customactivityinput** контейнера **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="179e2-236">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="179e2-237">Если контейнер adftutorial еще не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="179e2-237">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="179e2-238">Входная папка соответствует одному срезу в фабрике данных Azure, даже если она содержит два файла или более.</span><span class="sxs-lookup"><span data-stu-id="179e2-238">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="179e2-239">При обработке каждого среза конвейером пользовательское действие выполняет итерацию всех больших двоичных объектов во входной папке для этого среза.</span><span class="sxs-lookup"><span data-stu-id="179e2-239">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="179e2-240">В папке adftutorial\customactivityoutput отображается один выходной файл с одной или несколькими строками (соответствует количеству больших двоичных объектов во входной папке):</span><span class="sxs-lookup"><span data-stu-id="179e2-240">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="179e2-241">Ниже приведены шаги, подробно описанные далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="179e2-241">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="179e2-242">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="179e2-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="179e2-243">Создание **связанных служб** для пула виртуальных машин пакетной службы Azure, в котором выполняется пользовательское действие, а также экземпляр службы хранилища Azure, содержащей входные и выходные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="179e2-243">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="179e2-244">Создание входных и выходных **наборов данных**, которые представляют собой входные и выходные данные пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-244">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="179e2-245">Создание **конвейера**, который использует пользовательское действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-245">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="179e2-246">Создайте файл **file.txt** и передайте его в контейнер больших двоичных объектов, если еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="179e2-246">Create the **file.txt** and upload it to a blob container if you haven't already done so.</span></span> <span data-ttu-id="179e2-247">Инструкции см. в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="179e2-247">See instructions in the preceding section.</span></span>   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="179e2-248">Шаг 1. Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="179e2-248">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="179e2-249">Войдите на портал Azure и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="179e2-249">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="179e2-250">В меню слева нажмите кнопку **Создать** .</span><span class="sxs-lookup"><span data-stu-id="179e2-250">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="179e2-251">В колонке **Создание** щелкните **Данные и аналитика**.</span><span class="sxs-lookup"><span data-stu-id="179e2-251">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="179e2-252">Щелкните **Фабрика данных** в колонке **Аналитика данных**.</span><span class="sxs-lookup"><span data-stu-id="179e2-252">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![Меню создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="179e2-254">В колонке **Создание фабрики данных** в поле "Имя" введите **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="179e2-254">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="179e2-255">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="179e2-255">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="179e2-256">Если возникнет ошибка **Имя фабрики данных CustomActivityFactory недоступно**, измените имя этой фабрики данных (например, на **ваше_имяCustomActivityFactory**) и попробуйте создать ее снова.</span><span class="sxs-lookup"><span data-stu-id="179e2-256">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Колонка создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="179e2-258">Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="179e2-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="179e2-259">Убедитесь, что используется именно те **подписка** и **регион**, в которых необходимо создать фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-259">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="179e2-260">В колонке **Создание фабрики данных** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="179e2-260">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="179e2-261">Созданная фабрика данных появится на **панели мониторинга** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-261">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="179e2-262">После создания фабрики данных ее содержимое отобразится в соответствующей колонке.</span><span class="sxs-lookup"><span data-stu-id="179e2-262">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![Колонка "Фабрика данных"](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="179e2-264">Шаг 2. Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="179e2-264">Step 2: Create linked services</span></span>
<span data-ttu-id="179e2-265">Связанные службы связывают хранилища данных или службы вычислений с фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-265">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="179e2-266">На этом этапе учетная запись службы хранилища Azure и учетная запись пакетной службы Azure будут связаны с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-266">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="179e2-267">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="179e2-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="179e2-268">В колонке **Фабрика данных** для **CustomActivityFactory** щелкните элемент **Создание и развертывание**.</span><span class="sxs-lookup"><span data-stu-id="179e2-268">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="179e2-269">Отобразится редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-269">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="179e2-270">На панели команд щелкните **Создание хранилища данных** и выберите **Служба хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="179e2-270">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="179e2-271">В редакторе отобразится сценарий JSON для создания связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-271">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    !["Новое хранилище данных" — "Служба хранилища Azure"](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="179e2-273">Замените `<accountname>` именем своей учетной записи хранения Azure, а `<accountkey>` — ключом доступа к ней.</span><span class="sxs-lookup"><span data-stu-id="179e2-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="179e2-274">Сведения о получении ключа доступа к хранилищу см. в разделах о [просмотре, копировании и повторном создании ключей доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="179e2-274">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Связанная служба хранилища Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="179e2-276">Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="179e2-276">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="179e2-277">Создание связанной пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="179e2-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="179e2-278">В редакторе фабрики данных нажмите кнопку **... Еще** на панели команд, щелкните **Новое вычисление** и выберите в меню пункт **Пакет Azure**.</span><span class="sxs-lookup"><span data-stu-id="179e2-278">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    !["Новое вычисление" — "Пакет Azure"](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="179e2-280">Внесите следующие изменения в сценарий JSON:</span><span class="sxs-lookup"><span data-stu-id="179e2-280">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="179e2-281">В свойстве **accountName** укажите имя учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-281">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="179e2-282">**URL-адрес** из **колонки учетной записи пакетной службы Azure** имеет следующий формат: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="179e2-282">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="179e2-283">В свойстве **batchUri** в JSON требуется удалить заполнитель `accountname.` в URL-адресе и использовать значение `accountname` для свойства JSON `accountName`.</span><span class="sxs-lookup"><span data-stu-id="179e2-283">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="179e2-284">В свойстве **accessKey** укажите ключ учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-284">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="179e2-285">В свойстве **poolName** укажите имя пула, созданного при выполнении предварительных требований.</span><span class="sxs-lookup"><span data-stu-id="179e2-285">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="179e2-286">Вместо имени пула также можно указать идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="179e2-286">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="179e2-287">В свойстве **batchUri** укажите универсальный код ресурса (URI) пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-287">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="179e2-288">Пример: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="179e2-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="179e2-289">Для свойства **AzureStorageLinkedService** for the **linkedServiceName** укажите имя учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-289">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="179e2-290">Для свойства **poolName** можно также указать идентификатор пула вместо его имени.</span><span class="sxs-lookup"><span data-stu-id="179e2-290">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="179e2-291">Служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-291">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="179e2-292">Пул пакетной службы Azure можно использовать только в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="179e2-293">Шаг 3. Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="179e2-293">Step 3: Create datasets</span></span>
<span data-ttu-id="179e2-294">На этом шаге вы создадите наборы данных, которые представляют входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="179e2-294">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="179e2-295">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="179e2-295">Create input dataset</span></span>
1. <span data-ttu-id="179e2-296">В **редакторе** фабрики данных щелкните **... Еще** на панели команд, щелкните **Новый набор данных** и выберите в раскрывающемся меню пункт **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="179e2-296">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="179e2-297">Замените код JSON в правой области на следующий фрагмент кода JSON:</span><span class="sxs-lookup"><span data-stu-id="179e2-297">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="179e2-298">Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2016-11-16T00:00:00Z и временем окончания 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="179e2-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="179e2-299">Данные будут создаваться почасово, поэтому мы получим пять входных и выходных срезов (от **00**:00:00 до **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="179e2-299">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="179e2-300">Для параметров **frequency** и **interval** входного набора данных установлены значения **Hour** и **1**. Это означает, что входной срез данных будет создаваться каждый час.</span><span class="sxs-lookup"><span data-stu-id="179e2-300">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="179e2-301">В этом примере используется тот же файл (file.txt) в папке intputfolder.</span><span class="sxs-lookup"><span data-stu-id="179e2-301">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="179e2-302">Это значения времени начала для каждого среза, представленные системной переменной SliceStart в приведенном выше фрагменте кода JSON.</span><span class="sxs-lookup"><span data-stu-id="179e2-302">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="179e2-303">На панели инструментов щелкните **Развернуть**, чтобы создать и развернуть **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="179e2-303">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="179e2-304">Убедитесь, что на панели заголовка редактора отображается сообщение **ТАБЛИЦА УСПЕШНО СОЗДАНА** .</span><span class="sxs-lookup"><span data-stu-id="179e2-304">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="179e2-305">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="179e2-305">Create an output dataset</span></span>
1. <span data-ttu-id="179e2-306">В **редакторе фабрики данных** нажмите кнопку **... Еще** на панели команд, щелкните **Новый набор данных** и выберите пункт **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="179e2-306">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="179e2-307">Замените сценарий JSON в правой области на следующий:</span><span class="sxs-lookup"><span data-stu-id="179e2-307">Replace the JSON script in the right pane with the following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="179e2-308">Выходное расположение — **adftutorial/customactivityoutput/**, а имя выходного файла — ГГГГ-ММ-ДД-ЧЧ.txt (где ГГГГ, ММ, ДД и ЧЧ — год, месяц, день и час создания среза).</span><span class="sxs-lookup"><span data-stu-id="179e2-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="179e2-309">Подробную информацию см. в [справочнике разработчика фабрики данных Azure][adf-developer-reference].</span><span class="sxs-lookup"><span data-stu-id="179e2-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="179e2-310">Для каждого входного среза данных создается выходной большой двоичный объект или файл.</span><span class="sxs-lookup"><span data-stu-id="179e2-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="179e2-311">Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="179e2-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="179e2-312">Все выходные файлы создаются в одной выходной папке: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="179e2-312">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="179e2-313">Срез</span><span class="sxs-lookup"><span data-stu-id="179e2-313">Slice</span></span> | <span data-ttu-id="179e2-314">Время начала</span><span class="sxs-lookup"><span data-stu-id="179e2-314">Start time</span></span> | <span data-ttu-id="179e2-315">Выходной файл</span><span class="sxs-lookup"><span data-stu-id="179e2-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="179e2-316">1</span><span class="sxs-lookup"><span data-stu-id="179e2-316">1</span></span> |<span data-ttu-id="179e2-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="179e2-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="179e2-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="179e2-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="179e2-319">2</span><span class="sxs-lookup"><span data-stu-id="179e2-319">2</span></span> |<span data-ttu-id="179e2-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="179e2-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="179e2-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="179e2-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="179e2-322">3</span><span class="sxs-lookup"><span data-stu-id="179e2-322">3</span></span> |<span data-ttu-id="179e2-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="179e2-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="179e2-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="179e2-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="179e2-325">4</span><span class="sxs-lookup"><span data-stu-id="179e2-325">4</span></span> |<span data-ttu-id="179e2-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="179e2-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="179e2-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="179e2-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="179e2-328">5</span><span class="sxs-lookup"><span data-stu-id="179e2-328">5</span></span> |<span data-ttu-id="179e2-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="179e2-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="179e2-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="179e2-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="179e2-331">Помните, что все файлы во входной папке являются частью среза со значениями времени начала, указанными выше.</span><span class="sxs-lookup"><span data-stu-id="179e2-331">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="179e2-332">Во время обработки этого среза пользовательское действие сканирует каждый файл и создает строку в выходном файле с количеством вхождений условия поиска (Microsoft).</span><span class="sxs-lookup"><span data-stu-id="179e2-332">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="179e2-333">Если в папке inputfolder находятся три файла, в выходном файле будут содержаться три строки для каждого почасового среза: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt и т. д.</span><span class="sxs-lookup"><span data-stu-id="179e2-333">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="179e2-334">На панели команд нажмите кнопку **Развернуть**, чтобы развернуть **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="179e2-334">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="179e2-335">Создание и запуск конвейера, который использует настраиваемое действие</span><span class="sxs-lookup"><span data-stu-id="179e2-335">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="179e2-336">В редакторе фабрики данных нажмите кнопку **... Еще**, а затем нажмите на панели команд кнопку **Новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="179e2-336">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="179e2-337">Замените сценарий JSON в правой области приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="179e2-337">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="179e2-338">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="179e2-338">Note the following points:</span></span>

   * <span data-ttu-id="179e2-339">Для свойства **Concurrency** установлено значение **2**, чтобы два среза параллельно обрабатывались двумя виртуальными машинами в пуле пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-339">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="179e2-340">в разделе действий содержится одно действие типа **DotNetActivity**;</span><span class="sxs-lookup"><span data-stu-id="179e2-340">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="179e2-341">В **AssemblyName** задано имя библиотеки DLL **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="179e2-341">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="179e2-342">В **EntryPoint** — **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="179e2-342">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="179e2-343">Для параметра **PackageLinkedService** задано значение **AzureStorageLinkedService**, которое указывает на хранилище BLOB-объектов, содержащее ZIP-файл настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-343">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="179e2-344">Если для входных и выходных файлов и ZIP-файла настраиваемого действия используются разные учетные записи службы хранилища Azure, необходимо создать другую связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-344">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="179e2-345">В этой статье предполагается использование одной и той же учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-345">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="179e2-346">Для **PackageFile** установлено значение **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="179e2-346">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="179e2-347">Используется формат <контейнер_для_zip-файла>/<имя_zip-файла.zip>.</span><span class="sxs-lookup"><span data-stu-id="179e2-347">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="179e2-348">Настраиваемое действие принимает **InputDataset** в качестве входных данных и **OutputDataset** — в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-348">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="179e2-349">Свойство linkedServiceNam настраиваемого действия указывает на свойство **AzureBatchLinkedService**, которое сообщает фабрике данных Azure, что необходимо запустить настраиваемое действие на виртуальных машинах пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-349">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="179e2-350">Для свойства **isPaused** по умолчанию установлено значение **false**.</span><span class="sxs-lookup"><span data-stu-id="179e2-350">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="179e2-351">В этом примере конвейер запускается незамедлительно, потому что срезы приходятся на прошлое.</span><span class="sxs-lookup"><span data-stu-id="179e2-351">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="179e2-352">Для этого свойства можно задать значение true, чтобы приостановить работу конвейера. Чтобы перезапустить его, нужно снова установить значение false.</span><span class="sxs-lookup"><span data-stu-id="179e2-352">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="179e2-353">Разница между временем **начала** и временем **окончания** составляет **пять** часов, а срезы создаются каждый час. Таким образом конвейер создает пять срезов.</span><span class="sxs-lookup"><span data-stu-id="179e2-353">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="179e2-354">Чтобы развернуть конвейер, на панели команд нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="179e2-354">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="179e2-355">Мониторинг конвейера</span><span class="sxs-lookup"><span data-stu-id="179e2-355">Monitor the pipeline</span></span>
1. <span data-ttu-id="179e2-356">На портале Azure в колонке "Фабрика данных" щелкните **Схема**.</span><span class="sxs-lookup"><span data-stu-id="179e2-356">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![Плитка "Схема"](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="179e2-358">Теперь в представлении схемы щелкните OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="179e2-358">In the Diagram View, now click the OutputDataset.</span></span>

    ![Представление схемы](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="179e2-360">Вы увидите пять выходных срезов данных в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="179e2-360">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="179e2-361">Если они не в состоянии готовности, они еще не созданы.</span><span class="sxs-lookup"><span data-stu-id="179e2-361">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![Выходные срезы](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="179e2-363">Убедитесь, что выходные файлы создаются в хранилище больших двоичных объектов в контейнере **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="179e2-363">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![выходные данные настраиваемого действия][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="179e2-365">Если вы откроете выходной файл, вы увидите выходные данные, похожие на следующие:</span><span class="sxs-lookup"><span data-stu-id="179e2-365">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="179e2-366">Используйте [портал Azure][azure-preview-portal] или командлеты Azure PowerShell для отслеживания состояния фабрики данных, конвейеров и наборов данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-366">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="179e2-367">Вы можете просматривать сообщения **ActivityLogger** о настраиваемом действии в журналах (а именно — user-0.log), которые можно скачать на портале или с помощью командлетов.</span><span class="sxs-lookup"><span data-stu-id="179e2-367">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![скачивание журналов из настраиваемого действия][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="179e2-369">Подробные указания по мониторингу наборов данных и конвейеров см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="179e2-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="179e2-370">Проект фабрики данных в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="179e2-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="179e2-371">Можно создать и опубликовать сущности фабрики данных, используя Visual Studio вместо портала Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="179e2-372">Подробные сведения о создании и публикации сущностей фабрики данных с помощью Visual Studio см. в статьях [Создание первого конвейера с помощью Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) и [Копирование данных из большого двоичного объекта Azure в SQL Azure](data-factory-copy-activity-tutorial-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="179e2-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="179e2-373">При создании проекта фабрики данных в Visual Studio выполните следующие дополнительные шаги:</span><span class="sxs-lookup"><span data-stu-id="179e2-373">Do the following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="179e2-374">Добавьте проект фабрики данных в решение Visual Studio, содержащее проект настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-374">Add the Data Factory project to the Visual Studio solution that contains the custom activity project.</span></span> 
2. <span data-ttu-id="179e2-375">Добавьте ссылку на проект действия .NET из проекта фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-375">Add a reference to the .NET activity project from the Data Factory project.</span></span> <span data-ttu-id="179e2-376">Щелкните проект фабрики данных правой кнопкой мыши, наведите курсор на команду **Добавить** и щелкните **Ссылка**.</span><span class="sxs-lookup"><span data-stu-id="179e2-376">Right-click Data Factory project, point to **Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="179e2-377">В диалоговом окне **Добавление ссылки** выберите проект **MyDotNetActivity** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="179e2-377">In the **Add Reference** dialog box, select the **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="179e2-378">Выполните сборку и опубликуйте решение.</span><span class="sxs-lookup"><span data-stu-id="179e2-378">Build and publish the solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="179e2-379">При публикации сущностей фабрики данных автоматически создается ZIP-файл, который затем передается в контейнер BLOB-объектов customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="179e2-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded to the blob container: customactivitycontainer.</span></span> <span data-ttu-id="179e2-380">Если контейнер BLOB-объектов не существует, то он также создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="179e2-380">If the blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="179e2-381">Интеграция фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="179e2-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="179e2-382">Служба фабрики данных создает в пакетной службе Azure задание с именем **adf-poolname:job-xxx**.</span><span class="sxs-lookup"><span data-stu-id="179e2-382">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="179e2-383">В меню слева щелкните **Задания**.</span><span class="sxs-lookup"><span data-stu-id="179e2-383">Click **Jobs** from the left menu.</span></span> 

![Фабрика данных Azure — задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="179e2-385">Такое задание создается для каждого запуска действия среза.</span><span class="sxs-lookup"><span data-stu-id="179e2-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="179e2-386">При наличии пяти срезов, готовых к обработке, в рамках этого задания создаются пять задач.</span><span class="sxs-lookup"><span data-stu-id="179e2-386">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="179e2-387">Если в пуле пакетной службы есть несколько вычислительных узлов, два или больше среза могут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="179e2-387">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="179e2-388">Если для максимального количества задач на вычислительный узел установлено значение > 1, также можно выполнять сразу несколько срезов в одной среде выполнения приложений.</span><span class="sxs-lookup"><span data-stu-id="179e2-388">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="179e2-390">На следующей схеме показана связь между задачами фабрики данных и пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-390">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![Фабрика данных и пакетная служба](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="179e2-392">Устранение ошибок</span><span class="sxs-lookup"><span data-stu-id="179e2-392">Troubleshoot failures</span></span>
<span data-ttu-id="179e2-393">Устранение неполадок состоит из нескольких базовых методов:</span><span class="sxs-lookup"><span data-stu-id="179e2-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="179e2-394">Если отображается следующая ошибка, возможно, используется "горячее" или "холодное" хранилище BLOB-объектов вместо хранилища BLOB-объектов Azure общего назначения.</span><span class="sxs-lookup"><span data-stu-id="179e2-394">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="179e2-395">Отправьте ZIP-файл в **учетную запись хранения Azure общего назначения**.</span><span class="sxs-lookup"><span data-stu-id="179e2-395">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="179e2-396">Если отображается следующая ошибка, убедитесь, что имя класса в CS-файле соответствует имени, указанному для свойства **EntryPoint** в конвейере JSON.</span><span class="sxs-lookup"><span data-stu-id="179e2-396">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="179e2-397">В пошаговом руководстве имя класса — MyDotNetActivity, а для свойства EntryPoint в конвейере JSON указано значение MyDotNetActivityNS.**MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="179e2-397">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="179e2-398">Если имена соответствуют, убедитесь, что все двоичные файлы размещены в **корневой папке** ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="179e2-398">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="179e2-399">Это означает, что при открытии ZIP-файла все файлы должны находиться в корневой папке, а не во вложенных.</span><span class="sxs-lookup"><span data-stu-id="179e2-399">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="179e2-400">Если для входного среза данных не установлено значение **Готов**, убедитесь, что структура входной папки правильная и что в ней существует файл **file.txt**.</span><span class="sxs-lookup"><span data-stu-id="179e2-400">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="179e2-401">В методе **Execute** настраиваемого действия используйте объект **IActivityLogger**, чтобы записывать в журнал сведения, которые помогут устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="179e2-401">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="179e2-402">Сообщения, записываемые в журналы, появятся в файлах журнала пользователя (один или несколько файлов с именами user-0.log, user-1.log, user-2.log и т. д.).</span><span class="sxs-lookup"><span data-stu-id="179e2-402">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="179e2-403">В колонке **OutputDataset** щелкните срез, чтобы открыть для него колонку **Срез данных**.</span><span class="sxs-lookup"><span data-stu-id="179e2-403">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="179e2-404">Для этого среза будет указано значение **Запуски операции** .</span><span class="sxs-lookup"><span data-stu-id="179e2-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="179e2-405">Должно выполняться лишь одно действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-405">You should see one activity run for the slice.</span></span> <span data-ttu-id="179e2-406">Если в командной строке нажать кнопку «Запуск», можно запустить другое действие для этого среза.</span><span class="sxs-lookup"><span data-stu-id="179e2-406">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="179e2-407">Если щелкнуть выполняемое действие, появится колонка **Подробности о выполнении операции** со списком файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="179e2-407">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="179e2-408">Записанные в журнал сообщения можно увидеть в файле user_0.log.</span><span class="sxs-lookup"><span data-stu-id="179e2-408">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="179e2-409">Если возникнет ошибка, действие будет выполнено три раза, так как для количества повторных попыток в JSON-файле конвейера или действия задано значение 3.</span><span class="sxs-lookup"><span data-stu-id="179e2-409">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="179e2-410">Если щелкнуть выполняемое действие, отобразятся файлы журнала, которые можно использовать для устранения ошибки.</span><span class="sxs-lookup"><span data-stu-id="179e2-410">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="179e2-411">В списке файлов журнала щелкните **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="179e2-411">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="179e2-412">На панели справа отображаются результаты использования метода **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="179e2-412">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="179e2-413">Если вы не видите всех сообщений, проверьте наличие дополнительных файлов журнала user_1.log, user_2.log и т. д. Если нет, сбой в коде, возможно, произошел уже после последнего сообщения, записанного в журнал.</span><span class="sxs-lookup"><span data-stu-id="179e2-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="179e2-414">Кроме того, проверьте файл **system-0.log** на наличие любых системных сообщений об ошибках или исключений.</span><span class="sxs-lookup"><span data-stu-id="179e2-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="179e2-415">Добавьте **PDB-файл** в ZIP-файл, чтобы в случае возникновения ошибки сведения об ошибке содержали, например, информацию о **стеке вызовов**.</span><span class="sxs-lookup"><span data-stu-id="179e2-415">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="179e2-416">Все файлы в ZIP-файле для настраиваемого действия должны размещаться на **верхнем уровне** без вложенных папок.</span><span class="sxs-lookup"><span data-stu-id="179e2-416">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="179e2-417">Убедитесь, что для параметров **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) и **packageLinkedService** (должен указывать на хранилище BLOB-объектов Azure **общего назначения**, содержащее ZIP-файл) установлены правильные значения.</span><span class="sxs-lookup"><span data-stu-id="179e2-417">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="179e2-418">Если ошибки устранены и необходимо повторно обработать срез, в колонке **OutputDataset** щелкните срез правой кнопкой мыши и выберите пункт **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="179e2-418">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="179e2-419">Если возникла указанная ниже ошибка, это значит, что вы используете пакет службы хранилища Azure более поздней версии, чем 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="179e2-419">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="179e2-420">Средство запуска службы фабрики данных требует пакет WindowsAzure.Storage версии 4.3.</span><span class="sxs-lookup"><span data-stu-id="179e2-420">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="179e2-421">Сведения о том, что делать, если вам нужно использовать более позднюю версию сборки службы хранилища Azure, см. в разделе [Изоляции домена приложения](#appdomain-isolation).</span><span class="sxs-lookup"><span data-stu-id="179e2-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="179e2-422">Если вы можете использовать пакет службы хранилища Azure версии 4.3.0, удалите существующую ссылку на пакет Azure.Storage более поздней версии, чем 4.3.0,</span><span class="sxs-lookup"><span data-stu-id="179e2-422">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="179e2-423">и выполните следующую команду в консоли диспетчера пакетов Nuget.</span><span class="sxs-lookup"><span data-stu-id="179e2-423">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="179e2-424">Создайте проект.</span><span class="sxs-lookup"><span data-stu-id="179e2-424">Build the project.</span></span> <span data-ttu-id="179e2-425">Удалите сборку WindowsAzure.Storage более поздней версии, чем 4.3.0, из папки bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="179e2-425">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="179e2-426">Создайте ZIP-файл с двоичными файлами и PDB-файлом.</span><span class="sxs-lookup"><span data-stu-id="179e2-426">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="179e2-427">Замените старый ZIP-файл в контейнере больших двоичных объектов (customactivitycontainer) созданным.</span><span class="sxs-lookup"><span data-stu-id="179e2-427">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="179e2-428">Повторно запустите срезы, в которых произошли сбои (щелкните срез правой кнопкой мыши и выберите пункт "Выполнить").</span><span class="sxs-lookup"><span data-stu-id="179e2-428">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="179e2-429">Настраиваемое действие не использует файл **app.config** из пакета.</span><span class="sxs-lookup"><span data-stu-id="179e2-429">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="179e2-430">Поэтому, если код считывает какие-либо строки подключения из файла конфигурации, это не сработает во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="179e2-430">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="179e2-431">При использовании пакетной службы Azure рекомендуется хранить все секреты в **хранилище ключей Azure**. Кроме того, следует использовать субъект-службу на основе сертификата для защиты **хранилища ключей** и переместить сертификат в пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-431">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="179e2-432">В этом случае пользовательское действие .NET в среде выполнения сможет использовать секреты из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="179e2-432">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="179e2-433">Это общее решение, которое можно использовать для любого типа секретов, а не только строк подключения.</span><span class="sxs-lookup"><span data-stu-id="179e2-433">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="179e2-434">Существует и более простое (но не самое лучшее) решение: можно создать **связанную службу SQL Azure** с параметрами строки подключения, набор данных, использующий связанную службу, и привязать его как фиктивный набор входных данных к настраиваемому действию .NET.</span><span class="sxs-lookup"><span data-stu-id="179e2-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="179e2-435">После этого вы сможете получить доступ к строке подключения связанной службы из кода пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-435">You can then access the linked service's connection string in the custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="179e2-436">Обновление пользовательского действия</span><span class="sxs-lookup"><span data-stu-id="179e2-436">Update custom activity</span></span>
<span data-ttu-id="179e2-437">Если вы обновляете код для настраиваемого действия, создайте его и отправьте ZIP-файл, содержащий новые двоичные файлы, в службу хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="179e2-437">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="179e2-438">Изоляция домена приложения</span><span class="sxs-lookup"><span data-stu-id="179e2-438">Appdomain isolation</span></span>
<span data-ttu-id="179e2-439">В разделе с [примером перекрестного домена приложения](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) показано, как создать пользовательское действие, которое не ограничено версиями сборок, используемых средством запуска фабрики данных Azure (например, WindowsAzure.Storage версии 4.3.0, Newtonsoft.Json версии 6.0.x и т. д.).</span><span class="sxs-lookup"><span data-stu-id="179e2-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="179e2-440">Доступ к расширенным свойствам</span><span class="sxs-lookup"><span data-stu-id="179e2-440">Access extended properties</span></span>
<span data-ttu-id="179e2-441">Вы можете объявить расширенные свойства в действии JSON, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="179e2-441">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="179e2-442">В примере есть два расширенных свойства: **SliceStart** и **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="179e2-442">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="179e2-443">Значение свойства SliceStart основано на системной переменной SliceStart.</span><span class="sxs-lookup"><span data-stu-id="179e2-443">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="179e2-444">Список поддерживаемых системных переменных см. [в этом разделе](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="179e2-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="179e2-445">Значение свойства DataFactoryName жестко задано как CustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="179e2-445">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="179e2-446">Для доступа к этим расширенным свойствам в методе **Execute** используйте код, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="179e2-446">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="179e2-447">Автомасштабирование пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="179e2-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="179e2-448">Можно также создать пул пакетной службы Azure с использованием функции **автомасштабирования** .</span><span class="sxs-lookup"><span data-stu-id="179e2-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="179e2-449">Например, можно создать пул пакетной службы Azure с нулем выделенных виртуальных машин и формулой автоматического масштабирования на основе числа ожидающих задач.</span><span class="sxs-lookup"><span data-stu-id="179e2-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="179e2-450">Приведенный здесь пример формулы обеспечивает следующее поведение: при создании пула он изначально содержит одну виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="179e2-450">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="179e2-451">Метрика $PendingTasks определяет количество задач в состоянии выполнения и активном состоянии (в очереди).</span><span class="sxs-lookup"><span data-stu-id="179e2-451">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="179e2-452">Формула находит среднее число ожидающих выполнения задач за последние 180 секунд и соответствующим образом задает значение TargetDedicated.</span><span class="sxs-lookup"><span data-stu-id="179e2-452">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="179e2-453">Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="179e2-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="179e2-454">Таким образом, по мере поступления новых задач пул автоматически увеличивается, а по мере их завершения виртуальные машины высвобождаются по одной, и функция автоматического масштабирования уменьшает пул.</span><span class="sxs-lookup"><span data-stu-id="179e2-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="179e2-455">Значения startingNumberOfVMs и maxNumberofVMs можно настроить в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="179e2-455">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="179e2-456">Формула автоматического масштабирования:</span><span class="sxs-lookup"><span data-stu-id="179e2-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="179e2-457">Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="179e2-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="179e2-458">Если в пуле используется [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)(значение по умолчанию), пакетной службе может потребоваться 15–30 минут на подготовку виртуальной машины перед выполнением настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="179e2-458">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="179e2-459">Если пул использует другое значение autoScaleEvaluationInterval, пакетная служба может затрачивать autoScaleEvaluationInterval плюс 10 минут.</span><span class="sxs-lookup"><span data-stu-id="179e2-459">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="179e2-460">Использование службы вычислений HDInsight</span><span class="sxs-lookup"><span data-stu-id="179e2-460">Use HDInsight compute service</span></span>
<span data-ttu-id="179e2-461">В пошаговом руководстве для запуска пользовательского действия был использован вычислительный ресурс пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-461">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="179e2-462">Также можно использовать собственный кластер HDInsight на базе Windows или создать такой кластер по требованию с помощью фабрики данных и запустить пользовательское действие на кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="179e2-463">Ниже приведены основные шаги для использования кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-463">Here are the high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="179e2-464">Пользовательские действия .NET выполняются только в кластерах HDInsight на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="179e2-464">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="179e2-465">Чтобы обойти это ограничение, используйте действие Map Reduce для запуска пользовательского кода Java в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="179e2-465">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="179e2-466">Другой вариант — использовать для выполнения пользовательских действий пул виртуальных машин пакетной службы Azure, а не кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-466">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="179e2-467">Создайте связанную службу Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="179e2-468">Используйте связанную службу HDInsight вместо **AzureBatchLinkedService** в конвейере JSON.</span><span class="sxs-lookup"><span data-stu-id="179e2-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="179e2-469">Чтобы протестировать сценарий с использованием службы Azure HDInsight в руководстве, измените время **начала** и **окончания** для конвейера.</span><span class="sxs-lookup"><span data-stu-id="179e2-469">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="179e2-470">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="179e2-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="179e2-471">Служба фабрики данных Azure поддерживает создание кластера по запросу и использует его для обработки входных данных, чтобы создать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="179e2-471">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="179e2-472">Вы также можете использовать для этого собственный кластер.</span><span class="sxs-lookup"><span data-stu-id="179e2-472">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="179e2-473">Когда вы используете кластер HDInsight по запросу, для каждого среза создается отдельный кластер.</span><span class="sxs-lookup"><span data-stu-id="179e2-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="179e2-474">Если вы используете собственный кластер HDInsight, он сразу сможет обработать срез.</span><span class="sxs-lookup"><span data-stu-id="179e2-474">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="179e2-475">Поэтому при использовании кластера по запросу выходные данные могут выводится не так быстро, как при использовании собственного кластера.</span><span class="sxs-lookup"><span data-stu-id="179e2-475">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="179e2-476">Во время выполнения экземпляр действия .NET выполняется только на одном рабочем узле в кластере HDInsight; его невозможно расширить для выполнения на нескольких узлах.</span><span class="sxs-lookup"><span data-stu-id="179e2-476">At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes.</span></span> <span data-ttu-id="179e2-477">Несколько экземпляров действия .NET действия могут выполняться параллельно на разных узлах кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-477">Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.</span></span>
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="179e2-478">Использование кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="179e2-478">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="179e2-479">На **портале Azure**щелкните **Создать и развернуть** .</span><span class="sxs-lookup"><span data-stu-id="179e2-479">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="179e2-480">В редакторе фабрики данных щелкните **Новое вычисление** на панели команд и выберите в меню **On-demand HDInsight cluster** (Кластер HDInsight по запросу).</span><span class="sxs-lookup"><span data-stu-id="179e2-480">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="179e2-481">Внесите следующие изменения в сценарий JSON:</span><span class="sxs-lookup"><span data-stu-id="179e2-481">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="179e2-482">В свойстве **clusterSize** укажите размер кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-482">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="179e2-483">В свойстве **timeToLive** укажите, как долго может простаивать клиент, прежде чем он будет удален.</span><span class="sxs-lookup"><span data-stu-id="179e2-483">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="179e2-484">В свойстве **version** укажите версию HDInsight, которую хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="179e2-484">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="179e2-485">Если исключить это свойство, будет использоваться последняя версия.</span><span class="sxs-lookup"><span data-stu-id="179e2-485">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="179e2-486">В свойстве **LinkedServiceName** укажите **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="179e2-486">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="179e2-487">Пользовательские действия .NET выполняются только в кластерах HDInsight на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="179e2-487">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="179e2-488">Чтобы обойти это ограничение, используйте действие Map Reduce для запуска пользовательского кода Java в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="179e2-488">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="179e2-489">Другой вариант — использовать для выполнения пользовательских действий пул виртуальных машин пакетной службы Azure, а не кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-489">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="179e2-490">Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="179e2-490">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="179e2-491">Использование собственного кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="179e2-491">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="179e2-492">На **портале Azure**щелкните **Создать и развернуть** .</span><span class="sxs-lookup"><span data-stu-id="179e2-492">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="179e2-493">В **редакторе фабрики данных** щелкните **Новое вычисление** на панели команд и выберите в меню **Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="179e2-493">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="179e2-494">Внесите следующие изменения в сценарий JSON:</span><span class="sxs-lookup"><span data-stu-id="179e2-494">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="179e2-495">В свойстве **clusterUri** укажите URL-адрес кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-495">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="179e2-496">Например, https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="179e2-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="179e2-497">В свойстве **UserName** введите имя пользователя, у которого есть доступ к кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179e2-497">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="179e2-498">В свойстве **Password** укажите пароль этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="179e2-498">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="179e2-499">В свойстве **LinkedServiceName** укажите **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="179e2-499">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="179e2-500">Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="179e2-500">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="179e2-501">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="179e2-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="179e2-502">В **конвейере JSON**используйте связанную службу HDInsight (по запросу или собственную):</span><span class="sxs-lookup"><span data-stu-id="179e2-502">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="179e2-503">Создание пользовательского действия с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="179e2-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="179e2-504">В этой статье содержится пошаговое руководство, в котором с помощью портала Azure создается фабрика данных с конвейером, использующим настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="179e2-504">In the walkthrough in this article, you create a data factory with a pipeline that uses the custom activity by using the Azure portal.</span></span> <span data-ttu-id="179e2-505">В приведенном ниже коде показано, как создать фабрику данных с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="179e2-505">The following code shows you how to create the data factory by using .NET SDK instead.</span></span> <span data-ttu-id="179e2-506">Дополнительные сведения об использовании пакета SDK для программного создания конвейеров см. в статье [Руководство. Создание конвейера с действием копирования с помощью API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="179e2-506">You can find more details about using SDK to programmatically create pipelines in the [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="179e2-507">Отладка настраиваемого действия в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="179e2-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="179e2-508">Пример [локальной среды фабрики данных Azure](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) на портале GitHub включает в себя инструмент, который позволяет выполнять отладку настраиваемых действий .NET в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="179e2-508">The [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you to debug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="179e2-509">Примеры настраиваемых действий на портале GitHub</span><span class="sxs-lookup"><span data-stu-id="179e2-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="179e2-510">Образец</span><span class="sxs-lookup"><span data-stu-id="179e2-510">Sample</span></span> | <span data-ttu-id="179e2-511">Результат настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="179e2-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="179e2-512">[Загрузчик данных HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)</span><span class="sxs-lookup"><span data-stu-id="179e2-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="179e2-513">Загрузка данных из конечной точки HTTP в хранилище BLOB-объектов с помощью настраиваемого действия C# в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="179e2-513">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="179e2-514">Пример анализа мнений с помощью Twitter</span><span class="sxs-lookup"><span data-stu-id="179e2-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="179e2-515">Вызов модели машинного обучения Azure и выполнение анализа мнений, оценки, прогнозирования и т. д.</span><span class="sxs-lookup"><span data-stu-id="179e2-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="179e2-516">[Запуск скрипта R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)</span><span class="sxs-lookup"><span data-stu-id="179e2-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="179e2-517">Вызов сценария R путем запуска RScript.exe в кластере HDInsight, где уже установлен R.</span><span class="sxs-lookup"><span data-stu-id="179e2-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="179e2-518">Действие перекрестного домена приложения .NET</span><span class="sxs-lookup"><span data-stu-id="179e2-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="179e2-519">Использование разных версий сборок, которые используются средством запуска фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="179e2-519">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="179e2-520">Повторная обработка модели в службах Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="179e2-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="179e2-521">Повторная обработка модели в службах Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="179e2-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
