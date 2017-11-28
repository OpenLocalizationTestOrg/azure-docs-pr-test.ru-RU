---
title: "aaaUse настраиваемых действий в конвейере фабрики данных Azure"
description: "Узнайте, как toocreate настраиваемые действия и использовать их из конвейера фабрики данных Azure."
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
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="5a265-103">Использование настраиваемых действий в конвейере фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="5a265-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5a265-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="5a265-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5a265-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="5a265-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5a265-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="5a265-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5a265-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="5a265-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5a265-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="5a265-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5a265-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="5a265-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5a265-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="5a265-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5a265-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="5a265-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5a265-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5a265-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5a265-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="5a265-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5a265-114">Существует два типа действий, которые можно использовать в конвейере фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="5a265-115">[Действия перемещения данных](data-factory-data-movement-activities.md) toomove данных между [поддерживается хранилищ данных источника и приемника](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="5a265-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="5a265-116">[Действия преобразования данных](data-factory-data-transformation-activities.md) tootransform данных с помощью службы Azure HDInsight, пакетной службы Azure и машинного обучения Azure вычислений.</span><span class="sxs-lookup"><span data-stu-id="5a265-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="5a265-117">toomove данные из хранилища данных, который не поддерживает фабрики данных, создайте **пользовательское действие** собственные перемещение логики и использование hello действием данных в конвейере.</span><span class="sxs-lookup"><span data-stu-id="5a265-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="5a265-118">Аналогичным образом tootransform и обработки данных в виде, не поддерживается службой фабрики данных, создать пользовательское действие с свою собственную логику для преобразования данных и использования hello действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="5a265-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="5a265-119">Можно настроить toorun настраиваемого действия на **пакетной службы Azure** пула виртуальных машин или на основе Windows **Azure HDInsight** кластера.</span><span class="sxs-lookup"><span data-stu-id="5a265-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="5a265-120">При использовании пакетной службы Azure можно использовать только имеющийся пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="5a265-121">А при использовании HDInsight можно применить имеющийся кластер HDInsight или кластер, который автоматически создается для вас по запросу в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="5a265-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="5a265-122">Hello следующее пошаговое руководство содержит пошаговые инструкции по созданию настраиваемого действия .NET и использованию пользовательское действие hello в конвейере.</span><span class="sxs-lookup"><span data-stu-id="5a265-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="5a265-123">пошаговом руководстве Hello **пакетной службы Azure** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="5a265-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="5a265-124">toouse Azure HDInsight вместо связанной службы, создания связанной службы типа **HDInsight** (собственный кластер HDInsight) или **HDInsightOnDemand** (фабрики данных создает кластер HDInsight по запросу).</span><span class="sxs-lookup"><span data-stu-id="5a265-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="5a265-125">Затем настройте toouse пользовательское действие hello связанной службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="5a265-126">В разделе [HDInsight Azure используйте связанные службы](#use-hdinsight-compute-service) разделе подробные сведения о работе Azure HDInsight toorun hello пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="5a265-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="5a265-127">пользовательские действия .NET Hello выполняются только на кластеры HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="5a265-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5a265-128">Обойти это ограничение — toouse hello кода toorun пользовательские действия уменьшить карты Java в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5a265-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5a265-129">Другой вариант — toouse пула виртуальных машин toorun настраиваемые действия вместо использования кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="5a265-130">Это не возможные toouse шлюз управления данными из источников данных в локальной tooaccess настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="5a265-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="5a265-131">В настоящее время [шлюз управления данными](data-factory-data-management-gateway.md) поддерживает только действие копирования hello и действие хранимой процедуры в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="5a265-132">Пошаговое руководство по созданию настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="5a265-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="5a265-133">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a265-133">Prerequisites</span></span>
* <span data-ttu-id="5a265-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="5a265-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="5a265-135">Скачайте и установите пакет [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="5a265-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="5a265-136">Предварительные требования для пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5a265-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="5a265-137">В пошаговом руководстве hello выполнения настраиваемых действий .NET с помощью пакетной службы Azure как вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5a265-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="5a265-138">**Пакет Azure** — это платформа службы для выполнения крупномасштабных параллельных и высокопроизводительных вычислительных (систем HPC) приложения эффективно работает в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="5a265-139">Пакет Azure планирует интенсивных вычислительных рабочих toorun управляемого **коллекции виртуальных машин**, и может автоматически масштабирование вычислительных потребностей hello toomeet ресурсы заданий.</span><span class="sxs-lookup"><span data-stu-id="5a265-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="5a265-140">В разделе [основы пакетной службы Azure] [ batch-technical-overview] статье подробный обзор hello пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="5a265-141">В учебнике hello создайте учетную запись пакетной службы Azure с помощью пула виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a265-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="5a265-142">Ниже приведены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-142">Here are hello steps:</span></span>

1. <span data-ttu-id="5a265-143">Создание **учетной записи пакетной службы** с помощью hello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a265-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="5a265-144">Инструкции см. в статье [Создание учетной записи пакетной службы Azure на портале Azure][batch-create-account].</span><span class="sxs-lookup"><span data-stu-id="5a265-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="5a265-145">Запишите имя учетной записи пакетной службы Azure hello, ключ учетной записи, URI и имя пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="5a265-146">При необходимости toocreate связанной пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="5a265-147">На домашней странице приветствия для учетной записи пакетной службы Azure, вы видите **URL-адрес** в hello следующий формат: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5a265-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="5a265-148">В этом примере **myaccount** — имя учетной записи пакетной службы Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="5a265-149">URI, используемого в определении службы hello связаны — hello URL-адрес без имени hello hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5a265-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="5a265-150">Например, `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5a265-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="5a265-151">Нажмите кнопку **ключей** hello левого меню, а также копировать hello **первичный ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="5a265-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="5a265-152">toouse существующий пул, нажмите кнопку **пулы** в меню "hello" и запишите hello **идентификатор** hello пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="5a265-153">Если у вас нет существующего пула, переместите toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="5a265-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="5a265-154">Создайте **пул пакетной службы Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a265-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="5a265-155">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Обзор** в hello в левом меню и нажмите кнопку **учетные записи пакетного**.</span><span class="sxs-lookup"><span data-stu-id="5a265-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="5a265-156">Выберите ваш hello tooopen учетной записи пакетной службы Azure **пакетной учетной записи** колонку.</span><span class="sxs-lookup"><span data-stu-id="5a265-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="5a265-157">Щелкните элемент **Пулы** .</span><span class="sxs-lookup"><span data-stu-id="5a265-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="5a265-158">В hello **пулы** колонке нажмите кнопку Добавить на панель инструментов hello tooadd пул.</span><span class="sxs-lookup"><span data-stu-id="5a265-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="5a265-159">Введите идентификатор пула hello (идентификатор пула).</span><span class="sxs-lookup"><span data-stu-id="5a265-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="5a265-160">Примечание hello **идентификатор пула hello**; необходимо при создании решения hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="5a265-161">Укажите **Windows Server 2012 R2** для приветствия семейство операционных систем.</span><span class="sxs-lookup"><span data-stu-id="5a265-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="5a265-162">Выберите **Ценовая категория для узлов**.</span><span class="sxs-lookup"><span data-stu-id="5a265-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="5a265-163">Введите **2** как значение для hello **выделенной целевой** параметр.</span><span class="sxs-lookup"><span data-stu-id="5a265-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="5a265-164">Введите **2** как значение для hello **Max задач на каждом узле** параметр.</span><span class="sxs-lookup"><span data-stu-id="5a265-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="5a265-165">Нажмите кнопку **ОК** toocreate hello пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="5a265-166">Запишите hello **идентификатор** hello пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="5a265-167">Пошаговые действия</span><span class="sxs-lookup"><span data-stu-id="5a265-167">High-level steps</span></span>
<span data-ttu-id="5a265-168">Ниже приведены два hello высокоуровневые действия, выполняемых в рамках этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="5a265-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="5a265-169">Создайте пользовательское действие, содержащее простую логику преобразования и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="5a265-170">Создайте фабрику данных Azure с конвейером, который использует пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="5a265-171">Создать настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="5a265-171">Create a custom activity</span></span>
<span data-ttu-id="5a265-172">Создание toocreate .NET пользовательское действие, **библиотеки классов .NET** проекта с классом, который реализует **IDotNetActivity** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5a265-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="5a265-173">У этого интерфейса есть только один метод [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , и его сигнатура такова.</span><span class="sxs-lookup"><span data-stu-id="5a265-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="5a265-174">метод Hello принимает четыре параметра:</span><span class="sxs-lookup"><span data-stu-id="5a265-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="5a265-175">**linkedServices** —</span><span class="sxs-lookup"><span data-stu-id="5a265-175">**linkedServices**.</span></span> <span data-ttu-id="5a265-176">Это свойство является Перечислимый список служб хранилища данных связанной ссылается наборы данных ввода вывода для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="5a265-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="5a265-177">**наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="5a265-177">**datasets**.</span></span> <span data-ttu-id="5a265-178">Это свойство является Перечислимый список наборов данных ввода вывода для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="5a265-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="5a265-179">Можно использовать этот параметр tooget hello расположения и схем, определенных путем наборов входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="5a265-180">**activity** —</span><span class="sxs-lookup"><span data-stu-id="5a265-180">**activity**.</span></span> <span data-ttu-id="5a265-181">Это свойство представляет текущее действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-181">This property represents hello current activity.</span></span> <span data-ttu-id="5a265-182">Его можно использовать tooaccess расширенные свойства, связанные с пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="5a265-183">Дополнительные сведения см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).</span><span class="sxs-lookup"><span data-stu-id="5a265-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="5a265-184">**logger** —</span><span class="sxs-lookup"><span data-stu-id="5a265-184">**logger**.</span></span> <span data-ttu-id="5a265-185">Этот объект позволяет писать комментарии отладки этой рабочей области в hello входа пользователя для hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="5a265-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="5a265-186">метод Hello возвращает словарь, который может быть настраиваемых действий используется toochain друг с другом в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="5a265-187">Эта функция еще не реализован, чтобы возвращаемые пустой словарь из метода hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="5a265-188">Описание процедуры</span><span class="sxs-lookup"><span data-stu-id="5a265-188">Procedure</span></span>
1. <span data-ttu-id="5a265-189">Создайте проект **библиотеки классов .NET** .</span><span class="sxs-lookup"><span data-stu-id="5a265-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="5a265-190">Запустите <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> или <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="5a265-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="5a265-191">Нажмите кнопку <b>файл</b>, слишком точки<b>New</b>и нажмите кнопку <b>проекта</b>.</span><span class="sxs-lookup"><span data-stu-id="5a265-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="5a265-192">Разверните раздел <b>Шаблоны</b> и выберите <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="5a265-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="5a265-193">В этом пошаговом руководстве вы используете C#, но можно использовать любой .NET языка toodevelop hello пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="5a265-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="5a265-194">Выберите <b>библиотеки классов</b> hello списке типов проекта на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="5a265-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="5a265-195">В VS 2017 выберите <b>Библиотека классов (.NET Framework)</b> .</span><span class="sxs-lookup"><span data-stu-id="5a265-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="5a265-196">Введите <b>MyDotNetActivity</b> для hello <b>имя</b>.</span><span class="sxs-lookup"><span data-stu-id="5a265-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="5a265-197">Выберите <b>C:\ADFGetStarted</b> для hello <b>расположение</b>.</span><span class="sxs-lookup"><span data-stu-id="5a265-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="5a265-198">Нажмите кнопку <b>ОК</b> toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="5a265-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="5a265-199">
2.Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="5a265-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="5a265-200">3.</span><span class="sxs-lookup"><span data-stu-id="5a265-200">3.</span></span> <span data-ttu-id="5a265-201">В hello консоль диспетчера пакетов, выполните следующие команды tooimport hello **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="5a265-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="5a265-202">Импорт hello **хранилища Azure** пакета NuGet в проекте toohello.</span><span class="sxs-lookup"><span data-stu-id="5a265-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="5a265-203">Запуск службы фабрики данных требуется версия hello 4.3 WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="5a265-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="5a265-204">При добавлении tooa ссылка более позднюю версию сборки хранилища Azure в проект пользовательского действия, появится сообщение об ошибке при выполнении действия hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="5a265-205">Ошибка tooresolve hello, в разделе [изоляции домена приложения](#appdomain-isolation) раздела.</span><span class="sxs-lookup"><span data-stu-id="5a265-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="5a265-206">Добавьте следующее hello **с помощью** инструкций toohello исходного файла в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-206">Add hello following **using** statements toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="5a265-207">Изменение имени hello объекта hello **имен** слишком**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="5a265-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="5a265-208">Изменить имя hello класса hello слишком**MyDotNetActivity** и производными hello **IDotNetActivity** интерфейс, как показано в hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="5a265-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="5a265-209">Реализуйте (Добавить) hello **Execute** метод hello **IDotNetActivity** интерфейс toohello **MyDotNetActivity** hello класса и скопируйте следующий образец кода toohello метода.</span><span class="sxs-lookup"><span data-stu-id="5a265-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="5a265-210">Hello следующий пример считает hello число вхождений hello условие поиска («Microsoft») в каждый BLOB-объект, связанный с срез данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
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
    
        // toolog information, use hello logger object
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

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="5a265-211">Добавьте следующие вспомогательные методы hello:</span><span class="sxs-lookup"><span data-stu-id="5a265-211">Add hello following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
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
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="5a265-212">Hello GetFolderPath метод возвращает hello путь toohello папки, hello набор данных указывает tooand hello GetFileName метод возвращает hello имя hello большого двоичного объекта или файла, hello указывает набор данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="5a265-213">Если вы havefolderPath определяет использование переменных, например {Year}, {Month} возвращает {Day} и т.д., метод hello hello строку как есть и без их замены на значений времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="5a265-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="5a265-214">Дополнительные сведения о доступе к SliceStart, SliceEnd и т. д. см. в разделе [Доступ к расширенным свойствам](#access-extended-properties).</span><span class="sxs-lookup"><span data-stu-id="5a265-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="5a265-215">метод Calculate Hello вычисляет hello число экземпляров ключевое слово Microsoft во входных файлах hello (большие двоичные объекты в папке hello).</span><span class="sxs-lookup"><span data-stu-id="5a265-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="5a265-216">условие поиска Hello («Microsoft») жестко закодирована в коде hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="5a265-217">Скомпилируйте проект hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-217">Compile hello project.</span></span> <span data-ttu-id="5a265-218">Нажмите кнопку **построения** из hello меню и выберите пункт **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="5a265-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5a265-219">Набор 4.5.2 версии .NET Framework в качестве hello целевой платформы для проекта: щелкните правой кнопкой мыши проект hello и нажмите кнопку **свойства** tooset hello требуемой версии .NET framework.</span><span class="sxs-lookup"><span data-stu-id="5a265-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="5a265-220">Фабрика данных не поддерживает настраиваемые действия, скомпилированные для более поздних версий, чем .NET Framework 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="5a265-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="5a265-221">Запустите **Проводник**и перейдите в слишком**bin\debug** или **bin\release** папку, в зависимости от типа hello сборки.</span><span class="sxs-lookup"><span data-stu-id="5a265-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="5a265-222">Создать ZIP-файл **MyDotNetActivity.zip** , содержащий все двоичные файлы hello в hello <project folder>папку \bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="5a265-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="5a265-223">Включить hello **MyDotNetActivity.pdb** так, чтобы получить дополнительные сведения, такие как номер строки в исходном коде hello, вызвавшего проблему hello, если произошел сбой.</span><span class="sxs-lookup"><span data-stu-id="5a265-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="5a265-224">Все файлы в ZIP-файле hello hello, пользовательское действие hello должен быть в hello **верхнего уровня** с нет вложенных папок.</span><span class="sxs-lookup"><span data-stu-id="5a265-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![Двоичные выходные файлы](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="5a265-226">Создайте контейнер больших двоичных объектов **customactivitycontainer**, если он еще не создан.</span><span class="sxs-lookup"><span data-stu-id="5a265-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="5a265-227">Загрузите MyDotNetActivity.zip как customactivitycontainer toohello большого двоичного объекта в **общего назначения** хранилище больших двоичных объектов (хранилище больших двоичных объектов не горячей/стильной), который ссылается AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="5a265-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="5a265-228">Если добавить этот проект tooa .NET действия решение в Visual Studio, которое содержит проект фабрики данных и добавьте проект действия too.NET ссылку из проекта приложения hello фабрики данных, не обязательно tooperform hello последних двух этапов создания вручную Hello ZIP-файл и передать его в хранилище toohello общего назначения больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5a265-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="5a265-229">При публикации сущностей фабрики данных, с помощью Visual Studio следующие действия в процессе публикации hello происходит автоматически.</span><span class="sxs-lookup"><span data-stu-id="5a265-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="5a265-230">Дополнительные сведения см. в разделе [Проект фабрики данных в Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="5a265-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="5a265-231">Создание конвейера с настраиваемым действием</span><span class="sxs-lookup"><span data-stu-id="5a265-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="5a265-232">После создания пользовательского действия и отправить hello ZIP-файл с контейнер больших двоичных объектов tooa двоичные файлы в **общего назначения** учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="5a265-233">В этом разделе создается фабрикой данных Azure с конвейером, который использует пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="5a265-234">Hello входного набора данных для пользовательского действия hello представляет большие двоичные объекты (файлы) в папке customactivityinput hello adftutorial контейнера в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="5a265-235">Hello выходной набор данных для действия "hello" представляет выходные данные больших двоичных объектов в папке customactivityoutput hello adftutorial контейнера в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="5a265-236">Создание **файла file.txt** файл с hello следующие содержимого и передать его слишком**customactivityinput** папки hello **adftutorial** контейнера.</span><span class="sxs-lookup"><span data-stu-id="5a265-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="5a265-237">Создание контейнера adftutorial hello, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="5a265-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="5a265-238">Папка входных данных Hello соответствует tooa среза в фабрике данных Azure, даже если папка hello имеет два или более файлов.</span><span class="sxs-lookup"><span data-stu-id="5a265-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="5a265-239">При обработке каждого среза конвейером hello пользовательское действие hello выполняет итерацию всех больших двоичных объектов hello в hello папка входных данных для этого среза.</span><span class="sxs-lookup"><span data-stu-id="5a265-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="5a265-240">Вы увидите, что один выходной файл в папке adftutorial\customactivityoutput hello с одной или нескольких строк (то же, как количество больших двоичных объектов в папке входной hello):</span><span class="sxs-lookup"><span data-stu-id="5a265-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="5a265-241">Ниже приведены шаги hello, выполняемых в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5a265-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="5a265-242">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="5a265-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="5a265-243">Создание **связанные службы** для hello пула виртуальных машин, на какие hello настраиваемое действие выполняется, а hello хранилища Azure, содержащий hello большие двоичные объекты ввода вывода.</span><span class="sxs-lookup"><span data-stu-id="5a265-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="5a265-244">Создать входной и выходной **наборы данных** , представляющие вход и выход пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="5a265-245">Создание **конвейера** , использующий настраиваемое действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="5a265-246">Создать hello **файла file.txt** и отправьте его tooa контейнер больших двоичных объектов, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="5a265-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="5a265-247">См. инструкции в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="5a265-248">Шаг 1: Создание фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="5a265-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="5a265-249">После входа в систему toohello портал Azure, hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5a265-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="5a265-250">Нажмите кнопку **NEW** hello левом меню.</span><span class="sxs-lookup"><span data-stu-id="5a265-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="5a265-251">Нажмите кнопку **данные + аналитика** в hello **New** колонку.</span><span class="sxs-lookup"><span data-stu-id="5a265-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="5a265-252">Нажмите кнопку **фабрики данных** на hello **анализа данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="5a265-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Меню создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="5a265-254">В hello **новую фабрику данных** колонке введите **CustomActivityFactory** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="5a265-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="5a265-255">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="5a265-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="5a265-256">При получении ошибки hello: **имя фабрики данных «CustomActivityFactory» недоступен**, измените имя hello hello фабрики данных (например, **yournameCustomActivityFactory**) и попробуйте создать еще раз.</span><span class="sxs-lookup"><span data-stu-id="5a265-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Колонка создания фабрики данных Azure](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="5a265-258">Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a265-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="5a265-259">Убедитесь, что вы используете правильный hello **подписки** и **область** место hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="5a265-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="5a265-260">Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="5a265-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="5a265-261">Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="5a265-262">После успешного создания фабрики данных hello, вы видите колонке hello фабрики данных, в котором отображается содержимое фабрики данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Колонка "Фабрика данных"](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="5a265-264">Шаг 2. Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="5a265-264">Step 2: Create linked services</span></span>
<span data-ttu-id="5a265-265">Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений.</span><span class="sxs-lookup"><span data-stu-id="5a265-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="5a265-266">На этом шаге связать учетную запись хранилища Azure и фабрики данных tooyour учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="5a265-267">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="5a265-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="5a265-268">Щелкните hello **автор и развернуть** плитки приветствия **ФАБРИКИ данных** колонке **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="5a265-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="5a265-269">Вы увидите hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="5a265-270">Нажмите кнопку **новое хранилище данных** hello панели команд и выберите **хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a265-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="5a265-271">Вы увидите hello скрипта JSON для создания хранилища Azure связанная служба в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    !["Новое хранилище данных" — "Служба хранилища Azure"](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="5a265-273">Замените `<accountname>` с именем вашей учетной записи хранилища Azure и `<accountkey>` с ключом доступа hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="5a265-274">toolearn tooget хранилищем доступом ключа, см. в разделе [ключи доступа Просмотр, копирование и повторное создание хранилища](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5a265-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Связанная служба хранилища Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="5a265-276">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="5a265-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="5a265-277">Создание связанной пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5a265-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="5a265-278">В hello редактор фабрики данных, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новые вычислительные**, а затем выберите **пакетной службы Azure** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="5a265-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    !["Новое вычисление" — "Пакет Azure"](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="5a265-280">Внести следующие изменения скрипта JSON toohello hello:</span><span class="sxs-lookup"><span data-stu-id="5a265-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="5a265-281">Укажите имя учетной записи пакетной службы Azure для hello **accountName** свойство.</span><span class="sxs-lookup"><span data-stu-id="5a265-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="5a265-282">Hello **URL-адрес** из hello **колонке учетной записи пакетной службы Azure** в hello следующий формат: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5a265-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="5a265-283">Для hello **batchUri** свойство в hello JSON, вы должны tooremove `accountname.` из URL-адрес и используйте hello hello `accountname` для hello `accountName` свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="5a265-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="5a265-284">Укажите ключ учетной записи пакетной службы Azure hello для hello **accessKey** свойство.</span><span class="sxs-lookup"><span data-stu-id="5a265-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="5a265-285">Укажите имя hello hello пула, созданного в рамках предварительных требований для hello **poolName** свойство.</span><span class="sxs-lookup"><span data-stu-id="5a265-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="5a265-286">Можно также указать идентификатор hello пула hello вместо имени hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="5a265-287">Укажите URI пакета Azure для hello **batchUri** свойство.</span><span class="sxs-lookup"><span data-stu-id="5a265-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="5a265-288">Пример: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5a265-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="5a265-289">Укажите hello **AzureStorageLinkedService** для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="5a265-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

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

       <span data-ttu-id="5a265-290">Для hello **poolName** свойства, можно также указать идентификатор hello пула hello вместо имени hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="5a265-291">Hello служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="5a265-292">Пул пакетной службы Azure можно использовать только в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="5a265-293">Шаг 3. Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="5a265-293">Step 3: Create datasets</span></span>
<span data-ttu-id="5a265-294">На этом шаге создания наборов данных toorepresent входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="5a265-295">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="5a265-295">Create input dataset</span></span>
1. <span data-ttu-id="5a265-296">В hello **редактор** hello фабрики данных, щелкните **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**, а затем выберите **хранилища больших двоичных объектов Azure** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="5a265-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="5a265-297">Замените hello JSON в правой области hello hello, следующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="5a265-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

   <span data-ttu-id="5a265-298">Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2016-11-16T00:00:00Z и временем окончания 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="5a265-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="5a265-299">Запланированные tooproduce данных — час, поэтому существуют пять фрагменты ввода вывода (между **00**: -> 00:00 **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="5a265-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="5a265-300">Hello **частоты** и **интервал** для hello входного набора данных задается слишком**час** и **1**, что означает, что hello ввода фрагмент доступен Каждый час.</span><span class="sxs-lookup"><span data-stu-id="5a265-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="5a265-301">В этом примере это hello же файла (файла file.txt) в hello intputfolder.</span><span class="sxs-lookup"><span data-stu-id="5a265-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="5a265-302">Ниже приведены hello временем начала для каждого среза, представленного SliceStart системной переменной в hello выше фрагменте кода JSON.</span><span class="sxs-lookup"><span data-stu-id="5a265-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="5a265-303">Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="5a265-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="5a265-304">Подтвердите, что вы видите hello **таблица СОЗДАНА успешно** сообщение hello заголовке hello редактора.</span><span class="sxs-lookup"><span data-stu-id="5a265-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="5a265-305">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="5a265-305">Create an output dataset</span></span>
1. <span data-ttu-id="5a265-306">В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные** на панели команд hello, нажмите кнопку **новый набор данных**, а затем выберите **хранилища больших двоичных объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a265-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="5a265-307">Замените скрипт JSON hello в правой области hello hello следующий скрипт JSON:</span><span class="sxs-lookup"><span data-stu-id="5a265-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

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

     <span data-ttu-id="5a265-308">Расположение выходных данных — **adftutorial/customactivityoutput/** и имя выходного файла гггг мм дд HH.txt, где гггг мм дд чч — hello года, месяца, даты и часа hello среза, созданных.</span><span class="sxs-lookup"><span data-stu-id="5a265-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="5a265-309">Подробную информацию см. в [справочнике разработчика фабрики данных Azure][adf-developer-reference].</span><span class="sxs-lookup"><span data-stu-id="5a265-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="5a265-310">Для каждого входного среза данных создается выходной большой двоичный объект или файл.</span><span class="sxs-lookup"><span data-stu-id="5a265-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="5a265-311">Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="5a265-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="5a265-312">Все hello выходные файлы создаются в одной папке выходных данных: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="5a265-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="5a265-313">Срез</span><span class="sxs-lookup"><span data-stu-id="5a265-313">Slice</span></span> | <span data-ttu-id="5a265-314">Время начала</span><span class="sxs-lookup"><span data-stu-id="5a265-314">Start time</span></span> | <span data-ttu-id="5a265-315">Выходной файл</span><span class="sxs-lookup"><span data-stu-id="5a265-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="5a265-316">1</span><span class="sxs-lookup"><span data-stu-id="5a265-316">1</span></span> |<span data-ttu-id="5a265-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="5a265-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="5a265-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="5a265-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="5a265-319">2</span><span class="sxs-lookup"><span data-stu-id="5a265-319">2</span></span> |<span data-ttu-id="5a265-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="5a265-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="5a265-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="5a265-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="5a265-322">3</span><span class="sxs-lookup"><span data-stu-id="5a265-322">3</span></span> |<span data-ttu-id="5a265-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="5a265-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="5a265-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="5a265-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="5a265-325">4</span><span class="sxs-lookup"><span data-stu-id="5a265-325">4</span></span> |<span data-ttu-id="5a265-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="5a265-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="5a265-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="5a265-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="5a265-328">5</span><span class="sxs-lookup"><span data-stu-id="5a265-328">5</span></span> |<span data-ttu-id="5a265-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="5a265-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="5a265-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="5a265-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="5a265-331">Помните, что все файлы hello в папке ввода являются частью фрагмента с временем начала hello, упомянутых выше.</span><span class="sxs-lookup"><span data-stu-id="5a265-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="5a265-332">При обработке этого среза пользовательское действие hello просматривает каждый файл и создает строку в выходной файл hello с hello число вхождений условие поиска («Microsoft»).</span><span class="sxs-lookup"><span data-stu-id="5a265-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="5a265-333">Имеется три файла в hello inputfolder, есть три строки в hello выходной файл для каждого среза почасовой: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, и т. д.</span><span class="sxs-lookup"><span data-stu-id="5a265-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="5a265-334">toodeploy hello **OutputDataset**, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="5a265-335">Создание и выполнение конвейера, который использует пользовательское действие hello</span><span class="sxs-lookup"><span data-stu-id="5a265-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="5a265-336">В hello редактор фабрики данных, нажмите кнопку **... Дополнительные**, а затем выберите **новый конвейер** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="5a265-337">Замените hello JSON в правой области hello hello следующий скрипт JSON:</span><span class="sxs-lookup"><span data-stu-id="5a265-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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

    <span data-ttu-id="5a265-338">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="5a265-338">Note hello following points:</span></span>

   * <span data-ttu-id="5a265-339">**Параллелизм** задано слишком**2** , чтобы два фрагменты обрабатываются параллельно, 2 виртуальные машины в пуле пакетной службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="5a265-340">Имеется одно действие в разделе действий hello и имеет тип: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5a265-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="5a265-341">**AssemblyName** задано имя toohello hello DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="5a265-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="5a265-342">**EntryPoint** задано слишком**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5a265-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="5a265-343">**PackageLinkedService** задано слишком**AzureStorageLinkedService** , который указывает хранилище больших двоичных объектов toohello, содержащий ZIP-файл пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="5a265-344">При использовании различных учетных записей хранилища Azure для ввода вывода файлов и hello ZIP-файл пользовательских действий, можно создать другой связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="5a265-345">В этой статье предполагается, что вы используете hello учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="5a265-346">**PackageFile** задано слишком**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="5a265-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="5a265-347">Он имеет формат hello: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="5a265-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="5a265-348">пользовательское действие Hello принимает **InputDataset** в качестве входного и **OutputDataset** в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="5a265-349">Свойство linkedServiceName Hello пользовательское действие hello указывает toohello **AzureBatchLinkedService**, который сообщает фабрики данных Azure, пользовательское действие hello должен toorun на виртуальных машинах Azure пакета.</span><span class="sxs-lookup"><span data-stu-id="5a265-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="5a265-350">**isPaused** задано слишком**false** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5a265-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="5a265-351">конвейер Hello немедленно выполняется в этом примере, поскольку запуска среза hello в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="5a265-352">Можно задать это свойство tootrue toopause hello конвейера и задайте для него toorestart toofalse назад.</span><span class="sxs-lookup"><span data-stu-id="5a265-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="5a265-353">Hello **запустить** время и **окончания** время **пять** часы друг от друга и фрагменты создаются каждый час, поэтому пять фрагменты, созданные с помощью конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="5a265-354">toodeploy hello конвейера, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="5a265-355">Монитор hello конвейера</span><span class="sxs-lookup"><span data-stu-id="5a265-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="5a265-356">В колонке фабрики данных hello в hello портала Azure щелкните **схема**.</span><span class="sxs-lookup"><span data-stu-id="5a265-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Плитка "Схема"](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="5a265-358">В hello представление диаграммы щелкните hello OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="5a265-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Представление схемы](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="5a265-360">Вы увидите, что hello пять срезы выходных данных находятся в состоянии готовности hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="5a265-361">Если они не находятся в состоянии готовности hello, они еще не были созданы еще.</span><span class="sxs-lookup"><span data-stu-id="5a265-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Выходные срезы](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="5a265-363">Убедитесь, что hello выходные файлы создаются в хранилище больших двоичных объектов hello в hello **adftutorial** контейнера.</span><span class="sxs-lookup"><span data-stu-id="5a265-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![выходные данные настраиваемого действия][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="5a265-365">При открытии hello выходной файл, вы увидите hello выходной аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5a265-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="5a265-366">Используйте hello [портал Azure] [ azure-preview-portal] или toomonitor командлеты Azure PowerShell вашей фабрики данных, конвейеры и наборов данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="5a265-367">Можно видеть сообщения от hello **ActivityLogger** в коде hello пользовательское действие hello в журналах hello (в частности пользователя 0.log), которые можно загрузить с портала hello или с помощью командлетов.</span><span class="sxs-lookup"><span data-stu-id="5a265-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![скачивание журналов из настраиваемого действия][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="5a265-369">Подробные указания по мониторингу наборов данных и конвейеров см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5a265-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="5a265-370">Проект фабрики данных в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a265-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="5a265-371">Можно создать и опубликовать сущности фабрики данных, используя Visual Studio вместо портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="5a265-372">Подробные сведения о создании и публикации сущностей фабрики данных с помощью Visual Studio, в разделе [построение первой конвейер с помощью Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) и [копирования данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="5a265-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="5a265-373">Здравствуйте, следующие дополнительные шаги при создании фабрики данных проекта в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5a265-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="5a265-374">Добавьте hello фабрики данных проекта toohello Visual Studio решение, содержащее проект пользовательского действия hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="5a265-375">Добавьте проект действия .NET toohello ссылку из проекта hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="5a265-376">Щелкните правой кнопкой мыши проект фабрики данных, укажите слишком**добавить**и нажмите кнопку **ссылка**.</span><span class="sxs-lookup"><span data-stu-id="5a265-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="5a265-377">В hello **добавить ссылку** диалоговое окно, выберите hello **MyDotNetActivity** проекта, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5a265-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="5a265-378">Построение и публикация решения hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5a265-379">При публикации сущностей фабрики данных, в ZIP-файл автоматически создается и — контейнер больших двоичных объектов отправленного toohello: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="5a265-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="5a265-380">Если контейнер больших двоичных объектов hello не существует, она будет создана автоматически слишком.</span><span class="sxs-lookup"><span data-stu-id="5a265-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="5a265-381">Интеграция фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="5a265-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="5a265-382">Служба фабрики данных Hello создает задание в пакетной службы Azure с именем hello: **adf poolname: задание xxx**.</span><span class="sxs-lookup"><span data-stu-id="5a265-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="5a265-383">Нажмите кнопку **заданий** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-383">Click **Jobs** from hello left menu.</span></span> 

![Фабрика данных Azure — задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="5a265-385">Такое задание создается для каждого запуска действия среза.</span><span class="sxs-lookup"><span data-stu-id="5a265-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="5a265-386">Если есть пять готов toobe фрагменты обработки, пять задачи создаются в рамках этого задания.</span><span class="sxs-lookup"><span data-stu-id="5a265-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="5a265-387">Если существует несколько вычислительных узлов в hello пула, два или более фрагментов могут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="5a265-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="5a265-388">Если вычислений hello максимальное число задач в набор узлов слишком > 1, вы также можете более одного фрагмента, работающих на hello же вычислений.</span><span class="sxs-lookup"><span data-stu-id="5a265-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="5a265-390">Привет, следующая схема иллюстрирует hello связь между задачами фабрики данных Azure и пакета.</span><span class="sxs-lookup"><span data-stu-id="5a265-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Фабрика данных и пакетная служба](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="5a265-392">Устранение ошибок</span><span class="sxs-lookup"><span data-stu-id="5a265-392">Troubleshoot failures</span></span>
<span data-ttu-id="5a265-393">Устранение неполадок состоит из нескольких базовых методов:</span><span class="sxs-lookup"><span data-stu-id="5a265-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="5a265-394">Если появится следующая ошибка hello, возможно, используется активная/стильной хранилища больших двоичных объектов вместо хранения общего назначения BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="5a265-395">Отправка файла tooa hello zip **общего назначения учетной записи хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a265-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="5a265-396">Если следующая ошибка hello, убедитесь, что hello имя класса hello в имя соответствует hello hello CS файла, указанное для hello **EntryPoint** свойство hello конвейера JSON.</span><span class="sxs-lookup"><span data-stu-id="5a265-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="5a265-397">В пошаговом руководстве hello, является именем класса hello: MyDotNetActivity и hello точки входа в hello JSON: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="5a265-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="5a265-398">При совпадении имен hello, убедитесь, что все двоичные файлы hello в hello **корневую папку** hello ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="5a265-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="5a265-399">То есть при открытии hello ZIP-файл, вы увидите все файлы hello в корневой папке hello, а не все вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="5a265-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="5a265-400">Если входной срез hello не задано слишком**готовности**, подтвердите правильность структуры hello папка входных данных и **файла file.txt** существует в папках входной hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="5a265-401">В hello **Execute** метод настраиваемого действия, используйте hello **IActivityLogger** toolog сведения об объекте, которая позволяет выполнять устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="5a265-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="5a265-402">Hello в журнал сообщения отображаются в файлах журнала пользователя hello (один или несколько файлов с именем: 0.log пользователя, пользователь 1.log, 2.log пользователя, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="5a265-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="5a265-403">В hello **OutputDataset** колонка, щелкните hello срез toosee hello **СРЕЗ данных** колонку для этого среза.</span><span class="sxs-lookup"><span data-stu-id="5a265-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="5a265-404">Для этого среза будет указано значение **Запуски операции** .</span><span class="sxs-lookup"><span data-stu-id="5a265-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="5a265-405">Должна появиться при выполнении среза hello одного действия.</span><span class="sxs-lookup"><span data-stu-id="5a265-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="5a265-406">Если нажать кнопку запуска на панели команд hello, можно запустить другое действие запуска для hello того же фрагмента.</span><span class="sxs-lookup"><span data-stu-id="5a265-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="5a265-407">При нажатии кнопки при выполнении действия hello, вы видите hello **сведения о выполнении действия** колонка со списком файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="5a265-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="5a265-408">Вы увидите сообщение регистрируется в файле user_0.log hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="5a265-409">При возникновении ошибки, так как число повторных попыток hello задано too3 hello конвейера или действия JSON см запуске три действия.</span><span class="sxs-lookup"><span data-stu-id="5a265-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="5a265-410">При нажатии кнопки при выполнении действия hello, вы видите что tootroubleshoot hello ошибки можно просмотреть файлы журнала hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="5a265-411">В списке hello файлов журнала щелкните hello **0.log пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5a265-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="5a265-412">В правой панели hello являются hello результатов с помощью hello **IActivityLogger.Write** метод.</span><span class="sxs-lookup"><span data-stu-id="5a265-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="5a265-413">Если вы не видите всех сообщений, проверьте наличие дополнительных файлов журнала user_1.log, user_2.log и т. д. В противном случае — код hello возможно произошел сбой после последнего hello в журнал сообщения.</span><span class="sxs-lookup"><span data-stu-id="5a265-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="5a265-414">Кроме того, проверьте файл **system-0.log** на наличие любых системных сообщений об ошибках или исключений.</span><span class="sxs-lookup"><span data-stu-id="5a265-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="5a265-415">Включить hello **PDB** файлов в ZIP-файле hello таким образом, что сведения об ошибке hello сведения например **стека вызовов** при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="5a265-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="5a265-416">Все файлы в ZIP-файле hello hello, пользовательское действие hello должен быть в hello **верхнего уровня** с нет вложенных папок.</span><span class="sxs-lookup"><span data-stu-id="5a265-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="5a265-417">Убедитесь, что hello **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) и **packageLinkedService** (должен указывать toohello **общего назначения**хранилище больших двоичных объектов, содержащий hello ZIP-файл) значения toocorrect.</span><span class="sxs-lookup"><span data-stu-id="5a265-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="5a265-418">Исправления ошибок и хотите hello срез tooreprocess щелкните правой кнопкой мыши срез hello в hello **OutputDataset** колонку и нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="5a265-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="5a265-419">Если появится следующая ошибка hello, вы используете пакет hello хранилища Azure версии > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5a265-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="5a265-420">Запуск службы фабрики данных требуется версия hello 4.3 WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="5a265-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="5a265-421">В разделе [изоляции домена приложения](#appdomain-isolation) статьи для обхода, если необходимо использовать hello более позднюю версию сборки хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5a265-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="5a265-422">При использовании версии hello 4.3.0 пакета хранилища Azure удалите hello существующей ссылки tooAzure хранилища пакета версии > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5a265-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="5a265-423">Выполните следующую команду из консоли диспетчера пакетов NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="5a265-424">Построение проекта hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-424">Build hello project.</span></span> <span data-ttu-id="5a265-425">Удалите Azure.Storage сборки версии > 4.3.0 из папки bin\Debug hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="5a265-426">Создайте ZIP-файл с двоичные файлы и PDB-файл hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="5a265-427">Замените старый ZIP-файл hello в контейнер больших двоичных объектов hello (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="5a265-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="5a265-428">Запустите hello срезы, сбой (щелкните правой кнопкой мыши срез и нажмите кнопку Выполнить).</span><span class="sxs-lookup"><span data-stu-id="5a265-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="5a265-429">пользовательское действие Hello не использует hello **app.config** файл из пакета.</span><span class="sxs-lookup"><span data-stu-id="5a265-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="5a265-430">Таким образом Если код считывает все строки подключения из файла конфигурации hello, он не работает во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5a265-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="5a265-431">Здравствуйте, рекомендуется при использовании пакета Azure, toohold все секреты в **Azure KeyVault**, использовать службы на основе сертификата субъекта tooprotect hello **keyvault**и распространить сертификат hello tooAzure пула.</span><span class="sxs-lookup"><span data-stu-id="5a265-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="5a265-432">Здравствуйте настраиваемых действий .NET, то можно получить доступ к секретные данные из hello KeyVault во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5a265-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="5a265-433">Это решение является универсальным решением и масштабируется tooany тип секретного кода, а не только строку подключения.</span><span class="sxs-lookup"><span data-stu-id="5a265-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="5a265-434">Отсутствует простой обходной путь (но не рекомендуется): можно создать **связанная служба Azure SQL** параметры строки соединения, создать набор данных, использует hello связанной службы и цепочки hello dataset в виде пустой входного набора данных toohello настраиваемых действий .NET.</span><span class="sxs-lookup"><span data-stu-id="5a265-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="5a265-435">После этого можно доступа hello связаны строки подключения службы в коде пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="5a265-436">Обновление пользовательского действия</span><span class="sxs-lookup"><span data-stu-id="5a265-436">Update custom activity</span></span>
<span data-ttu-id="5a265-437">При обновлении кода hello для пользовательское действие hello, сборки, а также отправить hello ZIP-файл, содержащий новое хранилище больших двоичных объектов toohello двоичных файлов.</span><span class="sxs-lookup"><span data-stu-id="5a265-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="5a265-438">Изоляция домена приложения</span><span class="sxs-lookup"><span data-stu-id="5a265-438">Appdomain isolation</span></span>
<span data-ttu-id="5a265-439">. В разделе [Cross образец AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) , которое показывает, как toocreate пользовательского действия, которое не является ограниченное tooassembly версии, используемые запуска фабрики данных hello (пример: WindowsAzure.Storage версии 4.3.0, Newtonsoft.Json v6.0.x, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="5a265-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="5a265-440">Доступ к расширенным свойствам</span><span class="sxs-lookup"><span data-stu-id="5a265-440">Access extended properties</span></span>
<span data-ttu-id="5a265-441">Расширенные свойства можно объявить в действие hello JSON, как показано в следующих образец hello:</span><span class="sxs-lookup"><span data-stu-id="5a265-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

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


<span data-ttu-id="5a265-442">В примере hello имеется два расширенные свойства: **SliceStart** и **с именем DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="5a265-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="5a265-443">Hello SliceStart основано на hello SliceStart системной переменной.</span><span class="sxs-lookup"><span data-stu-id="5a265-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="5a265-444">Список поддерживаемых системных переменных см. [в этом разделе](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5a265-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="5a265-445">Hello с именем DataFactoryName значение жестко tooCustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="5a265-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="5a265-446">tooaccess эти расширенные свойства в hello **Execute** метод toohello аналогичные кода используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="5a265-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="5a265-447">Автомасштабирование пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5a265-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="5a265-448">Можно также создать пул пакетной службы Azure с использованием функции **автомасштабирования** .</span><span class="sxs-lookup"><span data-stu-id="5a265-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="5a265-449">Например можно создать пул пакет azure с 0 выделенных виртуальных машин и формулу автомасштабирования на основе количества hello ожидающих задач.</span><span class="sxs-lookup"><span data-stu-id="5a265-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="5a265-450">Образец формулы Hello позволяет достичь следующих поведение hello: при создании пула hello, он начинается с 1 виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5a265-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="5a265-451">Метрика $PendingTasks определяет hello число задач в запущена + active (в очереди) состояние.</span><span class="sxs-lookup"><span data-stu-id="5a265-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="5a265-452">Hello формула находит hello среднее число ожидающих задач в hello последние 180 секунд и соответствующим образом задает параметром TargetDedicated.</span><span class="sxs-lookup"><span data-stu-id="5a265-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="5a265-453">Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a265-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="5a265-454">Таким образом как отправлены новые задачи, пул автоматически увеличивается и как задачи завершаются, виртуальные машины становятся свободного один за другим и автоматическое масштабирование hello уменьшается этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a265-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="5a265-455">startingNumberOfVMs и maxNumberofVMs могут быть скорректированное tooyour потребностей.</span><span class="sxs-lookup"><span data-stu-id="5a265-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="5a265-456">Формула автоматического масштабирования:</span><span class="sxs-lookup"><span data-stu-id="5a265-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="5a265-457">Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="5a265-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="5a265-458">Если пул hello используется по умолчанию hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello пакетная служба может занять 15-30 минут tooprepare hello виртуальной Машины перед запуском пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="5a265-459">Если пул hello использует разные autoScaleEvaluationInterval, hello пакетная служба может получить autoScaleEvaluationInterval + 10 минут.</span><span class="sxs-lookup"><span data-stu-id="5a265-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="5a265-460">Использование службы вычислений HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a265-460">Use HDInsight compute service</span></span>
<span data-ttu-id="5a265-461">В пошаговом руководстве hello использовать пользовательское действие hello toorun пакетной службы Azure compute.</span><span class="sxs-lookup"><span data-stu-id="5a265-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="5a265-462">Также можно использовать собственный кластер HDInsight под управлением Windows или использовать фабрику данных создайте по требованию кластера HDInsight под управлением Windows, и запуска в кластере HDInsight hello пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="5a265-463">Здесь перечислены hello высокоуровневые действия для использования кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a265-464">пользовательские действия .NET Hello выполняются только на кластеры HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="5a265-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5a265-465">Обойти это ограничение — toouse hello кода toorun пользовательские действия уменьшить карты Java в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5a265-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5a265-466">Другой вариант — toouse пула виртуальных машин toorun настраиваемые действия вместо использования кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="5a265-467">Создайте связанную службу Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="5a265-468">Использование HDInsight связанная служба вместо **AzureBatchLinkedService** в hello конвейера JSON.</span><span class="sxs-lookup"><span data-stu-id="5a265-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="5a265-469">Если требуется, чтобы tootest его с помощью hello пошагового руководства, изменение **запустить** и **окончания** времени для конвейера hello, благодаря чему можно протестировать hello сценарий с hello службы Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="5a265-470">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a265-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="5a265-471">Hello служба фабрики данных Azure поддерживает создание кластера по требованию и использовать его tooprocess ввода tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="5a265-472">Также можно использовать собственный кластер tooperform hello таким же.</span><span class="sxs-lookup"><span data-stu-id="5a265-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="5a265-473">Когда вы используете кластер HDInsight по запросу, для каждого среза создается отдельный кластер.</span><span class="sxs-lookup"><span data-stu-id="5a265-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="5a265-474">В то время как при использовании кластера HDInsight hello кластер готов tooprocess немедленно hello среза.</span><span class="sxs-lookup"><span data-stu-id="5a265-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="5a265-475">Таким образом при использовании кластера по запросу, может отсутствовать hello выходных данных сразу, как при использовании собственных кластера.</span><span class="sxs-lookup"><span data-stu-id="5a265-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5a265-476">Во время выполнения экземпляра действия .NET работает только на один рабочий узел в кластере HDInsight hello; он не может быть масштабированный toorun на нескольких узлах.</span><span class="sxs-lookup"><span data-stu-id="5a265-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="5a265-477">Несколько экземпляров действия .NET могут выполняться параллельно на разных узлах кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="5a265-478">toouse кластер HDInsight по требованию</span><span class="sxs-lookup"><span data-stu-id="5a265-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="5a265-479">В hello **портал Azure**, нажмите кнопку **автор и развернуть** на домашней странице hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="5a265-480">В hello редактор фабрики данных, нажмите кнопку **новые вычислительные** из hello командной строке и выберите **кластер HDInsight по требованию** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="5a265-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="5a265-481">Внести следующие изменения скрипта JSON toohello hello:</span><span class="sxs-lookup"><span data-stu-id="5a265-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="5a265-482">Для hello **значение clusterSize** свойство, укажите размер кластера HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="5a265-483">Для hello **timeToLive** свойство, укажите, как долго hello клиента может простаивать перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="5a265-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="5a265-484">Для hello **версии** свойство, укажите требуется toouse версии HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="5a265-485">Если исключить это свойство используется последняя версия hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="5a265-486">Для hello **linkedServiceName**, укажите **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5a265-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

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
    > <span data-ttu-id="5a265-487">пользовательские действия .NET Hello выполняются только на кластеры HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="5a265-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="5a265-488">Обойти это ограничение — toouse hello кода toorun пользовательские действия уменьшить карты Java в кластере HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5a265-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5a265-489">Другой вариант — toouse пула виртуальных машин toorun настраиваемые действия вместо использования кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="5a265-490">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="5a265-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="5a265-491">toouse кластеру HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5a265-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="5a265-492">В hello **портал Azure**, нажмите кнопку **автор и развернуть** на домашней странице hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="5a265-493">В hello **редактор фабрики данных**, нажмите кнопку **новые вычислительные** из hello командной строке и выберите **кластера HDInsight** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="5a265-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="5a265-494">Внести следующие изменения скрипта JSON toohello hello:</span><span class="sxs-lookup"><span data-stu-id="5a265-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="5a265-495">Для hello **clusterUri** свойство, введите URL-адрес hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a265-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="5a265-496">Например, https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="5a265-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="5a265-497">Для hello **UserName** свойство, введите имя пользователя hello, обладающего кластера HDInsight toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="5a265-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="5a265-498">Для hello **пароль** свойство, введите пароль hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="5a265-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="5a265-499">Для hello **LinkedServiceName** свойство, введите **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5a265-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="5a265-500">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="5a265-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="5a265-501">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="5a265-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="5a265-502">В hello **конвейера JSON**, используйте HDInsight (по запросу или собственные) связанной службы:</span><span class="sxs-lookup"><span data-stu-id="5a265-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

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

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="5a265-503">Создание пользовательского действия с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="5a265-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="5a265-504">В пошаговом руководстве hello в этой статье создать фабрику данных с конвейером, который использует пользовательское действие hello с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5a265-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="5a265-505">Привет, следующий код показывает, как toocreate hello фабрики данных, используя пакет SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="5a265-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="5a265-506">Можно найти дополнительные сведения об использовании пакета SDK tooprogrammatically Конвейеры создаются в hello [создать конвейер с действием копирования с помощью интерфейса API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="5a265-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

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

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
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

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="5a265-507">Отладка настраиваемого действия в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a265-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="5a265-508">Hello [фабрики данных Azure - локальной среде](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) пример на GitHub включает средство, которое позволяет вам toodebug пользовательские действия .NET в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a265-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="5a265-509">Примеры настраиваемых действий на портале GitHub</span><span class="sxs-lookup"><span data-stu-id="5a265-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="5a265-510">Образец</span><span class="sxs-lookup"><span data-stu-id="5a265-510">Sample</span></span> | <span data-ttu-id="5a265-511">Результат настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="5a265-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="5a265-512">[Загрузчик данных HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)</span><span class="sxs-lookup"><span data-stu-id="5a265-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="5a265-513">Загружает данные из конечной точки HTTP tooAzure хранилища больших двоичных объектов с помощью пользовательского действия C# в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="5a265-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="5a265-514">Пример анализа мнений с помощью Twitter</span><span class="sxs-lookup"><span data-stu-id="5a265-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="5a265-515">Вызов модели машинного обучения Azure и выполнение анализа мнений, оценки, прогнозирования и т. д.</span><span class="sxs-lookup"><span data-stu-id="5a265-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="5a265-516">[Запуск скрипта R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)</span><span class="sxs-lookup"><span data-stu-id="5a265-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="5a265-517">Вызов сценария R путем запуска RScript.exe в кластере HDInsight, где уже установлен R.</span><span class="sxs-lookup"><span data-stu-id="5a265-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="5a265-518">Действие перекрестного домена приложения .NET</span><span class="sxs-lookup"><span data-stu-id="5a265-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="5a265-519">Использует разные версии сборки из тех, которые используются с запуска hello фабрики данных</span><span class="sxs-lookup"><span data-stu-id="5a265-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="5a265-520">Повторная обработка модели в службах Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5a265-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="5a265-521">Повторная обработка модели в службах Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5a265-521">Reprocesses a model in Azure Analysis Services.</span></span> |

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
