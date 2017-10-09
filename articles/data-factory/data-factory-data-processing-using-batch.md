---
title: "aaaProcess крупномасштабных наборы данных, с помощью фабрики данных и пакет | Документы Microsoft"
description: "Описывает, как конвейер tooprocess огромное количество данных в фабрике данных Azure с помощью возможности параллельной обработки пакетной службы Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="cd5d2-103">Обработка больших наборов данных с помощью фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="cd5d2-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="cd5d2-104">В этой статье описывается архитектура простого решения, которое автоматически и по расписанию перемещает и обрабатывает большие наборы данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="cd5d2-105">Он также предоставляет решение hello tooimplement Пошаговое руководство с начала до конца, с помощью фабрики данных Azure и пакета Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="cd5d2-106">Эта статья длиннее обычной статьи, так как в ней содержится пошаговое руководство для всего примера решения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="cd5d2-107">Если новый tooBatch и фабрики данных можно узнать об этих службах и о том, как они работают вместе.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="cd5d2-108">Если вы знаете, какое-либо службы hello и проектирование/архитектуры решения, вам может сосредоточиться только на hello [архитектура](#architecture-of-sample-solution) статье hello и если вы разрабатываете прототип или решения, вы также можете tootry out Пошаговые инструкции в hello [Пошаговое руководство](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="cd5d2-109">Мы приветствуем ваши комментарии об этой статье и использовании ее содержимого.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="cd5d2-110">Во-первых давайте взглянем на как фабрику данных и пакет служб может помочь с обработкой больших наборов данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="cd5d2-111">Сведения о пакетной службе Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-111">Why Azure Batch?</span></span>
<span data-ttu-id="cd5d2-112">Пакет Azure позволяет приложениям крупномасштабных параллельных и высокопроизводительных вычислительных систем (HPC) toorun эффективно работает в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="cd5d2-113">Она является службой платформы, которая планирует toorun работы с большим объемом вычислений в управляемой коллекции виртуальных машин и может автоматически масштабирование вычислительных потребностей hello toomeet ресурсы заданий.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="cd5d2-114">С hello пакетная служба можно определить tooexecute Azure вычислительные ресурсы приложения в параллельном режиме, а в масштабе.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="cd5d2-115">Можно запустить по требованию или по расписанию заданий и нет необходимости toomanually создания, настройки и управления кластера HPC, отдельных виртуальных машин, виртуальных сетей или сложных заданий и инфраструктуре планирования задач.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="cd5d2-116">См. следующие статьи, если вы не знакомы с пакетной службы Azure, он помогает обеспечивать понимание архитектуры и внедрению hello hello решения, описанные в этой статье hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="cd5d2-117">Основные сведения о пакетной службе Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="cd5d2-118">Обзор функций пакетной службы</span><span class="sxs-lookup"><span data-stu-id="cd5d2-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="cd5d2-119">(необязательно) toolearn Дополнительные сведения о пакетной службы Azure, в разделе hello [план обучения для пакетной службы Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="cd5d2-120">Сведения о фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="cd5d2-121">Фабрика данных — службы интеграции облачных данных, которая координирует и автоматизирует процессы hello перемещения и преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="cd5d2-122">С помощью hello служба фабрики данных, можно создать управляемые данные конвейеры, перемещения данных из локальных и облачных данных сохраняет tooa централизованное хранилище данных (например: хранилища больших двоичных объектов) и процесс или преобразования данных с помощью служб, таких как Azure HDInsight и Azure Машинное обучение.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="cd5d2-123">Можно также планировать toorun конвейеры данных в мониторе и запланированных способом (ежечасно, ежедневно, еженедельно, т. д.) и управлять ими в tooidentify Обзор проблемы и предпринять действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="cd5d2-124">См. следующие статьи, если вы не знакомы с фабрикой данных Azure, он помогает обеспечивать понимание архитектуры и внедрению hello hello решения, описанные в этой статье hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="cd5d2-125">Общие сведения о службе фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="cd5d2-126">Построение конвейера данных</span><span class="sxs-lookup"><span data-stu-id="cd5d2-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="cd5d2-127">(необязательно) toolearn Дополнительные сведения о фабрики данных Azure, в разделе hello [план обучения для фабрики данных Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="cd5d2-128">Совместное использование фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="cd5d2-128">Data Factory and Batch together</span></span>
<span data-ttu-id="cd5d2-129">Фабрика данных включает встроенные действия, такие как действие копирования toocopy или перемещения данных из источника данных хранить tooa целевое хранилище данных и данные tooprocess действие Hive, с использованием кластеров Hadoop (HDInsight) в Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="cd5d2-130">Список поддерживаемых действий преобразования см. в [этой статье](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="cd5d2-131">Также позволяет вам toocreate пользовательских действий .NET toomove или процесс данных с помощью собственной логики и выполните эти действия для кластера Azure HDInsight или пула виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="cd5d2-132">При использовании пакета Azure можно настроить hello пула tooauto масштабирование (Добавление или удаление виртуальных машин на основе рабочей нагрузки hello) на основе формулы, указываемые.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="cd5d2-133">Архитектура примера решения</span><span class="sxs-lookup"><span data-stu-id="cd5d2-133">Architecture of sample solution</span></span>
<span data-ttu-id="cd5d2-134">Несмотря на то, что архитектура hello, описанных в этой статье предназначен для простого решения, это применимо toocomplex сценариев, таких как рисков или моделирование финансовых служб, обработка изображений и подготовки к просмотру и генома анализа.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="cd5d2-135">Hello диаграмме 1) как фабрика данных управляет перемещение данных и обработки и (2) как пакетной службы Azure обрабатывает hello данных параллельных способом.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="cd5d2-136">Загрузка и Здравствуй, мир схемы для простоты обращения (11 x 17 дюймов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="cd5d2-137">или А3): [Управление данными и высокопроизводительными вычислениями с помощью пакетной службы и фабрики данных Azure](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="cd5d2-138">[![Схема обработки данных большого объема](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="cd5d2-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="cd5d2-139">Hello ниже приведены основные этапы процесса hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="cd5d2-140">Hello решение включает в себя код и объяснения toobuild hello решения начала до конца.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="cd5d2-141">**Настройка пула вычислительных узлов (виртуальные машины) для пакетной службы Azure**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="cd5d2-142">Можно указать hello числом узлов и размер каждого узла.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="cd5d2-143">**Создание экземпляра фабрики данных Azure** , для которого настраиваются сущности, представляющие хранилище BLOB-объектов, службу вычислений пакетной службы Azure, входные и выходные данные, а также рабочий процесс и конвейер с действиями, позволяющими перемещать и преобразовывать данные.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="cd5d2-144">**Создание настраиваемого действия .NET в конвейере данных фабрики hello**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="cd5d2-145">Действие Hello-пользовательского кода, выполняемого на hello пула.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="cd5d2-146">**Сохранение больших объемов входных данных в виде больших двоичных объектов в службе хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="cd5d2-147">Данные при этом разделяются на логические срезы (обычно по времени).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="cd5d2-148">**Фабрика данных копирует данные, которые обрабатываются параллельно** toohello вторичное расположение.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="cd5d2-149">**Фабрики данных выполняется с помощью пула hello, выделенной с помощью пакета пользовательское действие hello**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="cd5d2-150">Действия в фабрике данных могут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="cd5d2-151">В каждом действии обрабатывается один срез данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="cd5d2-152">Hello результаты хранятся в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="cd5d2-153">**Фабрика данных перемещает hello окончательные результаты tooa третье расположение**, либо для распространения приложения, либо для дальнейшей обработки другими средствами.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="cd5d2-154">Реализация примера решения</span><span class="sxs-lookup"><span data-stu-id="cd5d2-154">Implementation of sample solution</span></span>
<span data-ttu-id="cd5d2-155">Образец Hello решения намеренно простые и является tooshow вы как toouse фабрику данных и пакета вместе tooprocess наборов данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="cd5d2-156">решение Hello просто подсчитывает hello число вхождений условие поиска («Microsoft») во входных файлах, организованных во временных рядах.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="cd5d2-157">Он выводит файлы toooutput число hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="cd5d2-158">**Время**: Если вы знакомы с основами Azure, фабрике данных и пакет и иметь завершенного hello предварительные требования, перечисленные ниже, по нашим оценкам, это решение принимает toocomplete 1 – 2 часов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cd5d2-159">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd5d2-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="cd5d2-160">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-160">Azure subscription</span></span>
<span data-ttu-id="cd5d2-161">Если у вас нет подписки Azure, то всего за несколько минут можно создать бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cd5d2-162">Узнайте больше о [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="cd5d2-163">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-163">Azure storage account</span></span>
<span data-ttu-id="cd5d2-164">Использовать учетную запись хранилища Azure для хранения данных hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="cd5d2-165">Если у вас нет учетной записи хранения Azure, ознакомьтесь с разделом [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="cd5d2-166">Образец Hello решения используется хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="cd5d2-167">Учетная запись пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-167">Azure Batch account</span></span>
<span data-ttu-id="cd5d2-168">Создать учетную запись пакетной службы Azure с помощью hello [портал Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="cd5d2-169">Ознакомьтесь со статьей [Создание учетной записи пакетной службы Azure и управление ею](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="cd5d2-170">Обратите внимание, hello пакетной службы Azure имя и ключ учетной записи учетную запись.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="cd5d2-171">Можно также использовать [New AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) toocreate командлет учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="cd5d2-172">Подробные инструкции по использованию этого командлета см. в статье [Приступая к работе с командлетами PowerShell пакетной службы Azure](../batch/batch-powershell-cmdlets-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="cd5d2-173">Образец Hello решения использует данные tooprocess пакетной службы Azure (косвенно с помощью конвейера фабрики данных Azure) в виде параллельных в пуле вычислительных узлов (управляемой коллекции виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="cd5d2-174">Пул виртуальных машин пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="cd5d2-175">Создайте **пул пакетной службы Azure** с как минимум 2 вычислительными узлами.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="cd5d2-176">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **Обзор** в hello в левом меню и нажмите кнопку **учетные записи пакетного**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="cd5d2-177">Выберите ваш hello tooopen учетной записи пакетной службы Azure **пакетной учетной записи** колонку.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="cd5d2-178">Щелкните элемент **Пулы** .</span><span class="sxs-lookup"><span data-stu-id="cd5d2-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="cd5d2-179">В hello **пулы** колонке нажмите кнопку Добавить на панель инструментов hello tooadd пул.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="cd5d2-180">Введите идентификатор пула hello (**идентификатор пула**).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="cd5d2-181">Примечание hello **идентификатор пула hello**; необходимо при создании решения hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="cd5d2-182">Укажите **Windows Server 2012 R2** для приветствия семейство операционных систем.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="cd5d2-183">Выберите **Ценовая категория для узлов**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="cd5d2-184">Введите **2** как значение для hello **выделенной целевой** параметр.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="cd5d2-185">Введите **2** как значение для hello **Max задач на каждом узле** параметр.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="cd5d2-186">Нажмите кнопку **ОК** toocreate hello пула.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="cd5d2-187">обозреватель хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-187">Azure Storage Explorer</span></span>
<span data-ttu-id="cd5d2-188">[Azure Storage Explorer 6 (инструмент)](https://azurestorageexplorer.codeplex.com/) или [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (от ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="cd5d2-189">Используйте эти средства для проверки и изменения данных hello в проектах хранилища Azure, включая hello журналы приложений, размещенных в облаке.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="cd5d2-190">Создайте контейнер **mycontainer** с закрытым доступом (без анонимного доступа).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="cd5d2-191">Если вы используете **CloudXplorer**, создавать папки и подпапки с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="cd5d2-192">`Inputfolder`и `outputfolder` — это папки верхнего уровня в `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="cd5d2-193">Hello `inputfolder` содержит подпапки с метки даты и времени (гггг-мм-дд-ЧЧ).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="cd5d2-194">Если вы используете **обозреватель хранилищ Azure**, в следующем шаге hello необходимы tooupload файлы с именами: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` и т. д.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="cd5d2-195">Этот шаг автоматически создаются папки hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="cd5d2-196">Создайте текстовый файл **файла file.txt** на компьютере с содержимым, которое содержит ключевое слово hello **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="cd5d2-197">Например, test custom activity Microsoft test custom activity Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="cd5d2-198">Отправьте файл toohello hello, после ввода папок в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="cd5d2-199">Если вы используете **обозреватель хранилищ Azure**, отправьте файл hello **файла file.txt** слишком**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="cd5d2-200">Нажмите кнопку **копирования** на toocreate инструментов hello копию hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="cd5d2-201">В hello **копирования BLOB-объекта** диалоговое окно, изменение hello **имя BLOB-объекта назначения** слишком`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="cd5d2-202">Повторите этот шаг toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` и т. д.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="cd5d2-203">Это действие автоматически создает папки hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="cd5d2-204">Создайте другой контейнер с именем: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="cd5d2-205">Необходимо отправить контейнер toothis hello пользовательское действие ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="cd5d2-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd5d2-206">Visual Studio</span></span>
<span data-ttu-id="cd5d2-207">Установите Microsoft Visual Studio 2012 или более поздней версии toocreate hello пользовательского пакета действие toobe используется в hello решения фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="cd5d2-208">Пошаговые инструкции по toocreate hello решения</span><span class="sxs-lookup"><span data-stu-id="cd5d2-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="cd5d2-209">Создание пользовательского действия, содержащего логику обработки данных hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="cd5d2-210">Создайте фабрикой данных Azure, который использует пользовательское действие hello:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="cd5d2-211">Создание настраиваемого действия hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-211">Create hello custom activity</span></span>
<span data-ttu-id="cd5d2-212">Фабрика данных пользовательское действие Hello — основа hello в этом образце решения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="cd5d2-213">Образец Hello решения использует пакетной службы Azure toorun hello пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="cd5d2-214">В разделе [использовать настраиваемые действия в конвейере фабрики данных Azure](data-factory-use-custom-activities.md) для hello основные сведения toodevelop настраиваемые действия и использовать их в фабрике данных Azure конвейеров.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="cd5d2-215">toocreate .NET пользовательского действия, которое можно использовать в конвейере фабрики данных Azure необходимо toocreate **библиотеки классов .NET** проекта с классом, который реализует **IDotNetActivity** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="cd5d2-216">У этого интерфейса только один метод — **Execute**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="cd5d2-217">Вот hello сигнатура метода hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="cd5d2-218">метод Hello имеет несколько ключевых компонентов, необходимо toounderstand.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="cd5d2-219">метод Hello принимает четыре параметра:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="cd5d2-220">**linkedServices** —</span><span class="sxs-lookup"><span data-stu-id="cd5d2-220">**linkedServices**.</span></span> <span data-ttu-id="cd5d2-221">Перечислимый список связанных служб, связывающих источники данных ввода вывода (например: хранилища больших двоичных объектов) toohello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="cd5d2-222">В этом примере присутствует только одна связанная служба (служба хранилища Azure), которая используется для входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="cd5d2-223">**наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-223">**datasets**.</span></span> <span data-ttu-id="cd5d2-224">это перечисляемый список наборов данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="cd5d2-225">Можно использовать этот параметр tooget hello расположения и схем, определенных путем наборов входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="cd5d2-226">**activity** —</span><span class="sxs-lookup"><span data-stu-id="cd5d2-226">**activity**.</span></span> <span data-ttu-id="cd5d2-227">Этот параметр представляет hello текущей вычислений сущности - в этом случае пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="cd5d2-228">**logger** —</span><span class="sxs-lookup"><span data-stu-id="cd5d2-228">**logger**.</span></span> <span data-ttu-id="cd5d2-229">Hello средства ведения журнала позволяет создавать комментарии отладки поверхности, как «User» журнала для hello hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="cd5d2-230">метод Hello возвращает словарь, который может быть настраиваемых действий используется toochain друг с другом в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="cd5d2-231">Эта функция еще не реализован, чтобы возвращаемые пустой словарь из метода hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="cd5d2-232">Процедура: Создание настраиваемого действия hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="cd5d2-233">Создайте проект библиотеки классов .NET в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="cd5d2-234">Запустите **Visual Studio 2012,** /**Visual Studio 2013 или Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="cd5d2-235">Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="cd5d2-236">Разверните раздел **Шаблоны** и выберите **Visual C#\#**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="cd5d2-237">В этом пошаговом руководстве используется C\#, но можно использовать любой .NET языка toodevelop hello пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="cd5d2-238">Выберите **библиотеки классов** hello списке типов проекта на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="cd5d2-239">Введите **MyDotNetActivity** для hello **имя**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="cd5d2-240">Выберите **C:\\ADF** для hello **расположение**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="cd5d2-241">Создайте папку hello **ADF** , если он не существует.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="cd5d2-242">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="cd5d2-243">Нажмите кнопку **средства**, слишком точки**диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="cd5d2-244">В hello **консоль диспетчера пакетов**, выполните следующие команды tooimport hello **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="cd5d2-245">Импорт hello **хранилища Azure** пакета NuGet в проекте toohello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="cd5d2-246">Этот пакет необходимо так, как использовать API-Интерфейс хранилища больших двоичных объектов hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="cd5d2-247">Добавьте следующее hello **с помощью** директивы toohello исходный файл в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="cd5d2-248">Изменение имени hello объекта hello **имен** слишком**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="cd5d2-249">Изменение имени hello класса hello слишком**MyDotNetActivity** и производными hello **IDotNetActivity** интерфейс, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="cd5d2-250">Реализуйте (Добавить) hello **Execute** метод hello **IDotNetActivity** интерфейс toohello **MyDotNetActivity** hello класса и скопируйте следующий образец кода toohello метода.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="cd5d2-251">В разделе hello [выполнить метод](#execute-method) чтобы пояснения для hello логику, используемую в этом методе.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. <span data-ttu-id="cd5d2-252">Добавьте следующий вспомогательный класс toohello методы hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="cd5d2-253">Эти методы вызываются hello **Execute** метод.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="cd5d2-254">Здравствуйте, самое главное, **Calculate** метод изолирует hello код, выполняющий перебор элементов каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    <span data-ttu-id="cd5d2-255">Hello **GetFolderPath** метод возвращает папку toohello hello, hello tooand точки набора данных hello **GetFileName** метод возвращает имя hello hello большого двоичного объекта или файла, который hello указывает набор данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="cd5d2-256">Hello **Calculate** метод вычисляет hello число экземпляров ключевое слово **Microsoft** во входных файлах hello (большие двоичные объекты в папке hello).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="cd5d2-257">условие поиска Hello («Microsoft») жестко закодирована в коде hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="cd5d2-258">Скомпилируйте проект hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-258">Compile hello project.</span></span> <span data-ttu-id="cd5d2-259">Нажмите кнопку **построения** из hello меню и выберите пункт **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="cd5d2-260">Запустите **Проводник**и перейдите в слишком**bin\\отладки** или **bin\\выпуска** папку, в зависимости от типа hello сборки.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="cd5d2-261">Создать ZIP-файл **MyDotNetActivity.zip** , содержащий все двоичные файлы hello в hello  **\\bin\\отладки** папки.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="cd5d2-262">Вы можете tooinclude hello MyDotNetActivity. **pdb** так, чтобы получить дополнительные сведения, такие как номер строки в исходном коде hello, вызвавшего проблему hello, когда происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="cd5d2-263">Отправка **MyDotNetActivity.zip** как контейнер больших двоичных объектов blob toohello: `customactivitycontainer` в hello Azure хранилище больших двоичных объектов, hello **StorageLinkedService** связанная служба в hello  **ADFTutorialDataFactory** использует.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="cd5d2-264">Создание контейнера больших двоичных объектов hello `customactivitycontainer` , если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="cd5d2-265">Метод Execute</span><span class="sxs-lookup"><span data-stu-id="cd5d2-265">Execute method</span></span>
<span data-ttu-id="cd5d2-266">Этот раздел содержит дополнительные сведения и заметки о hello код в метод Execute hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="cd5d2-267">члены Hello для прохода по коллекции входных hello находятся в hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) пространства имен.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="cd5d2-268">Прохода по коллекции hello больших двоичных объектов, необходимо использовать hello **BlobContinuationToken** класса.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="cd5d2-269">По сути, необходимо использовать оператор do-во время цикла с маркером hello в качестве механизма hello для выхода из цикла hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="cd5d2-270">Дополнительные сведения см. в разделе [как toouse хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="cd5d2-271">Базовый цикл выглядит так:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="cd5d2-272">См. в документации hello для hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) метод подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="cd5d2-273">Hello для работы по hello набор больших двоичных объектов логически переходит в hello делать код-цикла while.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="cd5d2-274">В hello **Execute** метод, выполните hello-а цикл передает hello список больших двоичных объектов с именем метода tooa **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="cd5d2-275">метод Hello возвращает строковую переменную с именем **вывода** итерацию все большие двоичные объекты hello в сегменте hello, hello результат.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="cd5d2-276">Он возвращает hello число вхождений hello условие поиска (**Microsoft**) в большом двоичном объекте hello передан toohello **Calculate** метод.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="cd5d2-277">Здравствуйте, один раз **Calculate** метод проделал рабочих hello, оно должно быть написано tooa новый большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="cd5d2-278">Поэтому для каждого набора больших двоичных объектов, обработанных новый большой двоичный объект может иметь с результатами hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="cd5d2-279">новый большой двоичный объект toowrite tooa, первый поиска hello выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="cd5d2-280">Привет код также вызывает вспомогательный метод: **GetFolderPath** путь к папке hello tooretrieve (имя контейнера хранилища hello).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="cd5d2-281">Hello **GetFolderPath** приведения hello объекта DataSet tooan AzureBlobDataSet, который имеет свойство с именем FolderPath.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="cd5d2-282">hello вызовы кода Hello **GetFileName** метод tooretrieve hello имя файла (blob).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="cd5d2-283">Код Hello-аналогичные toohello выше путь к папке hello tooget кода.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="cd5d2-284">Имя файла hello Hello записывается, создав объект URI.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="cd5d2-285">конструктор URI Hello использует hello **BlobEndpoint** имя контейнера hello tooreturn свойства.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="cd5d2-286">путь и имя папки Hello добавляются tooconstruct hello вывода URI большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="cd5d2-287">будет записана Hello имя файла hello и теперь можно написать hello выходной строки из hello **Calculate** новый большой двоичный объект метод tooa:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="cd5d2-288">Создание фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-288">Create hello data factory</span></span>
<span data-ttu-id="cd5d2-289">В hello [создать пользовательское действие hello](#create-the-custom-activity) вы создали настраиваемых действий и hello загруженный ZIP-файл с двоичные файлы и hello PDB файла tooan контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="cd5d2-290">В этом разделе создайте Azure **фабрики данных** с **конвейера** , использующий hello **пользовательское действие**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="cd5d2-291">Здравствуйте входного набора данных для пользовательское действие hello представляет hello большие двоичные объекты (файлы) в папке входной hello (`mycontainer\\inputfolder`) в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="cd5d2-292">Hello выходной набор данных для hello действие представляет hello выходных данных BLOB-объектов в выходной папке hello (`mycontainer\\outputfolder`) в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="cd5d2-293">Удалите один или несколько файлов в папках входной hello:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="cd5d2-294">Например удалите один файл (file.txt) с hello, следуя содержимое в каждую из папки hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="cd5d2-295">Каждая папка входных данных соответствует tooa среза в фабрике данных Azure, даже если папка hello имеет 2 или более файлов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="cd5d2-296">При обработке каждого среза конвейером hello пользовательское действие hello выполняет итерацию всех больших двоичных объектов hello в hello папка входных данных для этого среза.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="cd5d2-297">Вы увидите, что пять выходных файлов с hello же содержимого.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-297">You see five output files with hello same content.</span></span> <span data-ttu-id="cd5d2-298">Например выходной файл hello не может обрабатывать файл hello в папке hello 2015-11-16-00 имеет hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="cd5d2-299">Если удалить несколько файлов (file.txt, file2.txt, file3.txt) с hello же toohello входной папки содержимого см. в разделе hello после содержимого в выходной файл для hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="cd5d2-300">Каждая папка (2015-11-16-00, т. д.) соответствует tooa среза в этом образце, даже если папка hello имеет несколько входных файлов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="cd5d2-301">Hello выходной файл имеет три строк, по одной на каждый входной файл (blob) в папке hello, связанные с hello среза (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="cd5d2-302">Такая задача создается для каждого запуска действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-302">A task is created for each activity run.</span></span> <span data-ttu-id="cd5d2-303">В этом примере имеется только одно действие в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="cd5d2-304">Если срез обрабатывается конвейером hello, пользовательское действие hello работает на срез hello tooprocess пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="cd5d2-305">Так как имеется 5 срезов (каждому срезу может соответствовать несколько больших двоичных объектов или файлов), в пакетной службе Azure создано 5 задач.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="cd5d2-306">Это фактически hello настраиваемое действие, которое выполняется при запуске задачи в пакете.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="cd5d2-307">Привет, пошаговое руководство содержит дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="cd5d2-308">Шаг 1: Создание фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="cd5d2-309">После входа в toohello [портал Azure](https://portal.azure.com/), hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="cd5d2-310">Нажмите кнопку **NEW** hello левом меню.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="cd5d2-311">Нажмите кнопку **данные + аналитика** в hello **New** колонку.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="cd5d2-312">Нажмите кнопку **фабрики данных** на hello **анализа данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="cd5d2-313">В hello **новую фабрику данных** колонке введите **CustomActivityFactory** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="cd5d2-314">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="cd5d2-315">При получении ошибки hello: **имя фабрики данных «CustomActivityFactory» недоступен**, измените имя hello hello фабрики данных (например, **yournameCustomActivityFactory**) и попробуйте создать еще раз.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="cd5d2-316">Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="cd5d2-317">Убедитесь, что вы используете hello правильные подписки и региона, место hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="cd5d2-318">Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="cd5d2-319">Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="cd5d2-320">После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="cd5d2-321">Шаг 2. Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="cd5d2-321">Step 2: Create linked services</span></span>
<span data-ttu-id="cd5d2-322">Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="cd5d2-323">На этом шаге связать ваш **хранилища Azure** учетной записи и **пакетной службы Azure** фабрики данных tooyour учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="cd5d2-324">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="cd5d2-325">Щелкните hello **автор и развернуть** плитки приветствия **ФАБРИКИ данных** колонке **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="cd5d2-326">Вы увидите hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="cd5d2-327">Нажмите кнопку **новое хранилище данных** hello панели команд и выберите **хранилища Azure.**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="cd5d2-328">Вы увидите hello скрипта JSON для создания хранилища Azure связанная служба в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="cd5d2-329">Замените **имя учетной записи** с именем hello вашей учетной записи хранилища Azure и **ключ учетной записи** с ключом доступа hello hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="cd5d2-330">toolearn tooget хранилищем доступом ключа, см. в разделе [ключи доступа Просмотр, копирование и повторное создание хранилища](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="cd5d2-331">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="cd5d2-332">Создание связанной пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="cd5d2-333">На этом шаге создания связанной службы для вашего **пакетной службы Azure** учетной записи, используемые toorun hello фабрики данных пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="cd5d2-334">Нажмите кнопку **новые вычислительные** hello панели команд и выберите **пакетной службы Azure.**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="cd5d2-335">Вы увидите hello скрипта JSON для создания пакета Azure связанная служба в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="cd5d2-336">В hello скрипта JSON:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="cd5d2-337">Замените **имя учетной записи** с именем hello учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="cd5d2-338">Замените **ключ доступа** с ключом доступа hello hello учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="cd5d2-339">Введите идентификатор hello пула hello hello **poolName** свойства**.**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="cd5d2-340">Для этого свойства можно задать имя пула или идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="cd5d2-341">Введите раздел hello URI для hello **batchUri** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="cd5d2-342">Hello **URL-адрес** из hello **колонке учетной записи пакетной службы Azure** в hello следующий формат: \<accountname\>.\< область\>. batch.azure.com. Для hello **batchUri** свойство в hello JSON необходимо слишком**удалить «accountname».**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="cd5d2-343">с URL-адреса hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-343">from hello URL.</span></span> <span data-ttu-id="cd5d2-344">Пример: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="cd5d2-345">Для hello **poolName** свойства, можно также указать идентификатор hello пула hello вместо имени hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="cd5d2-346">Hello служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="cd5d2-347">Пул пакетной службы Azure можно использовать только в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="cd5d2-348">Укажите **StorageLinkedService** для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="cd5d2-349">Эта связанная служба, созданный на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="cd5d2-350">Это хранилище используется в качестве промежуточной области для файлов и журналов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="cd5d2-351">Нажмите кнопку **развернуть** на панели toodeploy hello связаны службы hello команд.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="cd5d2-352">Шаг 3. Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="cd5d2-352">Step 3: Create datasets</span></span>
<span data-ttu-id="cd5d2-353">На этом шаге создания наборов данных toorepresent входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="cd5d2-354">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="cd5d2-354">Create input dataset</span></span>
1. <span data-ttu-id="cd5d2-355">В hello **редактор** hello фабрики данных, щелкните **новый набор данных** кнопки на панели инструментов hello и щелкните **хранилища больших двоичных объектов Azure** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="cd5d2-356">Замените hello JSON в правой области hello hello, следующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    <span data-ttu-id="cd5d2-357">Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2015-11-16T00:00:00Z и временем окончания 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="cd5d2-358">Это данные, запланированных tooproduce **каждый час**, поэтому 5 срезов ввода вывода (между **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="cd5d2-359">Hello **частоты** и **интервал** для hello входного набора данных задается слишком**час** и **1**, что означает, что hello ввода фрагмент доступен Каждый час.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="cd5d2-360">Ниже приведены временем начала hello для каждого сегмента, представленными в **SliceStart** системной переменной в hello выше фрагменте кода JSON.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="cd5d2-361">**Срез**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-361">**Slice**</span></span> | <span data-ttu-id="cd5d2-362">**Время начала**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="cd5d2-363">1</span><span class="sxs-lookup"><span data-stu-id="cd5d2-363">1</span></span>         | <span data-ttu-id="cd5d2-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="cd5d2-365">2</span><span class="sxs-lookup"><span data-stu-id="cd5d2-365">2</span></span>         | <span data-ttu-id="cd5d2-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="cd5d2-367">3</span><span class="sxs-lookup"><span data-stu-id="cd5d2-367">3</span></span>         | <span data-ttu-id="cd5d2-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="cd5d2-369">4.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-369">4</span></span>         | <span data-ttu-id="cd5d2-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="cd5d2-371">5</span><span class="sxs-lookup"><span data-stu-id="cd5d2-371">5</span></span>         | <span data-ttu-id="cd5d2-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="cd5d2-373">Hello **folderPath** вычисляется с помощью hello года, месяца, дня и часа часть время начала среза hello (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="cd5d2-374">Таким образом Вот как папка входных данных — сопоставленных tooa срез.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="cd5d2-375">**Срез**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-375">**Slice**</span></span> | <span data-ttu-id="cd5d2-376">**Время начала**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-376">**Start time**</span></span>          | <span data-ttu-id="cd5d2-377">**Входная папка**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="cd5d2-378">1</span><span class="sxs-lookup"><span data-stu-id="cd5d2-378">1</span></span>         | <span data-ttu-id="cd5d2-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="cd5d2-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="cd5d2-381">2</span><span class="sxs-lookup"><span data-stu-id="cd5d2-381">2</span></span>         | <span data-ttu-id="cd5d2-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="cd5d2-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="cd5d2-384">3</span><span class="sxs-lookup"><span data-stu-id="cd5d2-384">3</span></span>         | <span data-ttu-id="cd5d2-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="cd5d2-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="cd5d2-387">4.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-387">4</span></span>         | <span data-ttu-id="cd5d2-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="cd5d2-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="cd5d2-390">5</span><span class="sxs-lookup"><span data-stu-id="cd5d2-390">5</span></span>         | <span data-ttu-id="cd5d2-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="cd5d2-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="cd5d2-393">Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **InputDataset** таблицы.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="cd5d2-394">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="cd5d2-394">Create output dataset</span></span>
<span data-ttu-id="cd5d2-395">На этом шаге создается другой набор данных типа AzureBlob toorepresent hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="cd5d2-396">В hello **редактор** hello фабрики данных, щелкните **новый набор данных** кнопки на панели инструментов hello и щелкните **хранилища больших двоичных объектов Azure** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="cd5d2-397">Замените hello JSON в правой области hello hello, следующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    <span data-ttu-id="cd5d2-398">Для каждого входного среза данных создается выходной большой двоичный объект или файл.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="cd5d2-399">Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="cd5d2-400">Все hello выходные файлы создаются в одной папке выходных данных: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="cd5d2-401">**Срез**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-401">**Slice**</span></span> | <span data-ttu-id="cd5d2-402">**Время начала**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-402">**Start time**</span></span>          | <span data-ttu-id="cd5d2-403">**Выходной файл**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="cd5d2-404">1</span><span class="sxs-lookup"><span data-stu-id="cd5d2-404">1</span></span>         | <span data-ttu-id="cd5d2-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="cd5d2-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="cd5d2-407">2</span><span class="sxs-lookup"><span data-stu-id="cd5d2-407">2</span></span>         | <span data-ttu-id="cd5d2-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="cd5d2-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="cd5d2-410">3</span><span class="sxs-lookup"><span data-stu-id="cd5d2-410">3</span></span>         | <span data-ttu-id="cd5d2-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="cd5d2-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="cd5d2-413">4.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-413">4</span></span>         | <span data-ttu-id="cd5d2-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="cd5d2-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="cd5d2-416">5</span><span class="sxs-lookup"><span data-stu-id="cd5d2-416">5</span></span>         | <span data-ttu-id="cd5d2-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="cd5d2-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="cd5d2-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="cd5d2-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="cd5d2-419">Помните, что все hello файлы в папке ввода (например: 2015-11-16-00) являются частью фрагмента с временем начала hello: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="cd5d2-420">При обработке этого среза пользовательское действие hello просматривает каждый файл и создает строку в выходной файл hello с hello число вхождений условие поиска («Microsoft»).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="cd5d2-421">Если имеется три файла в папке hello 2015-11-16-00, существует три строки в выходной файл для hello: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="cd5d2-422">Нажмите кнопку **развернуть** hello toocreate инструментов и развернуть hello **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="cd5d2-423">Шаг 4: Создание и запуск конвейера hello с помощью настраиваемых действий</span><span class="sxs-lookup"><span data-stu-id="cd5d2-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="cd5d2-424">На этом шаге создания конвейера от одного действия, пользовательское действие hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd5d2-425">Если вы еще не загрузили hello **файла file.txt** tooinput папки в контейнер больших двоичных объектов hello, сделать это перед созданием конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="cd5d2-426">Hello **isPaused** свойству toofalse hello конвейера JSON, поэтому конвейера hello немедленно выполняется как hello **запустить** дата находится в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="cd5d2-427">В hello редактор фабрики данных, нажмите кнопку **новый конвейер** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="cd5d2-428">Если команда hello не отображается, нажмите кнопку **... (Многоточие)**  toosee его.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="cd5d2-429">Замените hello JSON в правой области hello hello следующий скрипт JSON:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="cd5d2-430">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-430">Note hello following points:</span></span>

   * <span data-ttu-id="cd5d2-431">Имеется только одно действие в конвейере hello и типа: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="cd5d2-432">**AssemblyName** задано имя toohello hello DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="cd5d2-433">**EntryPoint** задано слишком**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="cd5d2-434">По сути, это фрагмент кода \<пространство_имен\>.\<имя_класса\>.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="cd5d2-435">**PackageLinkedService** задано слишком**StorageLinkedService** , который указывает хранилище больших двоичных объектов toohello, содержащий ZIP-файл пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="cd5d2-436">При использовании различных учетных записей хранилища Azure для файлов ввода вывода и ZIP-файл пользовательское действие hello, у вас есть toocreate другого хранилища Azure связанной службы.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="cd5d2-437">В этой статье предполагается, что вы используете hello учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="cd5d2-438">**PackageFile** задано слишком**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="cd5d2-439">Он имеет формат hello: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="cd5d2-440">пользовательское действие Hello принимает **InputDataset** в качестве входного и **OutputDataset** в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="cd5d2-441">Hello **linkedServiceName** свойство пользовательское действие hello указывает toohello **AzureBatchLinkedService**, который сообщает фабрики данных Azure, пользовательское действие hello должен toorun на пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="cd5d2-442">Hello **параллелизма** параметр важен.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="cd5d2-443">При использовании значения по умолчанию hello, равное 1, даже если у вас есть 2 или вычислительные узлы в пуле пакетной службы Azure hello, срезы hello обрабатываются одна за другой.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="cd5d2-444">Таким образом вы не пользуетесь преимуществами возможности параллельной обработки hello пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="cd5d2-445">Если задать **параллелизма** tooa чем выше значение, например 2, это означает, что срезы (соответствует tootwo задач в пакетной службы Azure) могут одновременно обрабатываться в hello же время, в этом случае обе виртуальные машины hello в hello пула используются пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="cd5d2-446">Таким образом свойства hello параллелизма соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="cd5d2-447">По умолчанию на виртуальной машине в любой момент времени будет выполняться только одна задача (один срез).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="cd5d2-448">Hello причина том, что по умолчанию hello **максимально задачи на виртуальную Машину** задано too1 для пула пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="cd5d2-449">В рамках предварительных требований, созданный пул с этой too2 набор свойств, двумя фрагменты фабрики данных может выполняться на виртуальной Машине в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="cd5d2-450">**isPaused** свойству toofalse по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="cd5d2-451">конвейер Hello немедленно выполняется в этом примере, поскольку запуска среза hello в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="cd5d2-452">Можно задать это свойство tootrue toopause hello конвейера и задайте для него toorestart toofalse назад.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="cd5d2-453">Hello **запустить** время и **окончания** значения времени приведены пять часов друг от друга и фрагменты создаются каждый час, поэтому пять фрагменты, созданные с помощью конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="cd5d2-454">Нажмите кнопку **развернуть** на панели toodeploy hello конвейера hello команд.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="cd5d2-455">Шаг 5: Тестирование hello конвейера</span><span class="sxs-lookup"><span data-stu-id="cd5d2-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="cd5d2-456">На этом шаге теста hello конвейера путем перемещения файлов в папки входной hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="cd5d2-457">Начнем с конвейером тестирования hello с одного файла в одну папку ввода.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="cd5d2-458">В колонке фабрики данных hello в hello портала Azure щелкните **схема**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="cd5d2-459">В представлении диаграммы hello, дважды щелкните набор входных данных: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="cd5d2-460">Вы увидите hello **InputDataset** колонка с все пять срезы готова.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="cd5d2-461">Обратите внимание hello **время НАЧАЛА СРЕЗА** и **время окончания СРЕЗА** для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="cd5d2-462">В hello **представление диаграммы**, нажмите кнопку **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="cd5d2-463">Вы увидите, hello пять срезы выходных данных находятся в состоянии готовности hello, если они уже были созданы.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="cd5d2-464">Используйте Azure портала tooview hello **задачи** связанные с hello **фрагменты** и увидеть, какие виртуальной Машины выполнялось каждый фрагмент.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="cd5d2-465">Дополнительные сведения см. в разделе [Интеграция фабрики данных и пакетной службы](#data-factory-and-batch-integration).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="cd5d2-466">Вы увидите выходные файлы hello в hello `outputfolder` из `mycontainer` в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="cd5d2-467">Должно появиться пять выходных файлов, по одному на каждый входной срез.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="cd5d2-468">Каждый из hello выходной файл должен иметь содержимого аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="cd5d2-469">Hello следующей схеме показано сопоставление tootasks в пакете Azure фрагменты hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="cd5d2-470">В этом примере срез запускался всего один раз.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="cd5d2-471">Теперь давайте попробуем использовать несколько файлов в папке.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="cd5d2-472">Создание файлов: **file2.txt**, **file3.txt**, **file4.txt**, и **file5.txt** с hello же содержимого, как и file.txt в папке hello: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="cd5d2-473">В выходной папке hello **удаление** hello выходной файл: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="cd5d2-474">Теперь в hello **OutputDataset** колонка, щелкните правой кнопкой мыши срез hello с **время НАЧАЛА СРЕЗА** значение слишком**11/16/2015 01:00:00 AM**и нажмите кнопку **запуска**toorerun или повторно-process hello среза.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="cd5d2-475">Теперь hello фрагмент содержит пять файлов вместо одного файла.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="cd5d2-476">После запуска среза hello и она находится в состоянии **готовности**, проверьте содержимое hello в hello выходной файл для этого среза (**2015-11-16-01.txt**) в hello `outputfolder` из `mycontainer` в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="cd5d2-477">Строку для каждого файла фрагмента hello следует.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="cd5d2-478">Если не был удален hello выходной файл 2015-11-16-01.txt перед попыткой с пять входных файлов, можно увидеть, одну строку от предыдущего фрагмента hello запуска и пять строк из текущего среза hello запуска.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="cd5d2-479">По умолчанию hello содержимого — присоединенных toooutput файл, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="cd5d2-480">Интеграция фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="cd5d2-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="cd5d2-481">Служба фабрики данных Hello создает задание в пакетной службы Azure с именем hello: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Фабрика данных Azure — задания пакетной службы](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="cd5d2-483">Задачи в задании hello создается для каждого фрагмента запуска действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="cd5d2-484">При наличии 10 готов toobe фрагменты обработки, 10 задачи создаются в задании hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="cd5d2-485">Может иметь более одного фрагмента выполняется параллельно, если имеется несколько вычислительных узлов в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="cd5d2-486">Если максимальное число задач hello в вычислений слишком набор узлов > 1, может быть больше, чем один срез, работающих на hello же вычислений.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="cd5d2-487">В этом примере имеется пять срезов, что соответствует пяти задачам в пакетной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="cd5d2-488">С hello **параллелизма** значение слишком**5** в hello конвейера JSON в фабрике данных Azure и **максимально задачи на виртуальную Машину** значение слишком**2** в пакете Azure пул с **2** ВМ, hello задачи выполняется быстро (проверьте время начала и окончания для задач).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="cd5d2-489">Используйте hello портала tooview hello пакетного задания и его задачи, связанные с hello **фрагменты** и увидеть, какие виртуальной Машины выполнялось каждый фрагмент.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="cd5d2-491">Отладка hello конвейера</span><span class="sxs-lookup"><span data-stu-id="cd5d2-491">Debug hello pipeline</span></span>
<span data-ttu-id="cd5d2-492">Отладка состоит из нескольких базовых методов:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="cd5d2-493">Если входной срез hello не задано слишком**готовности**, убедитесь, что папка входных данных структуры hello указано правильно и file.txt существует в папках входной hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="cd5d2-494">В hello **Execute** метод настраиваемого действия, используйте hello **IActivityLogger** toolog сведения об объекте, которая позволяет выполнять устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="cd5d2-495">Hello в журнал сообщения отображаются в hello пользователя\_0. файла журнала.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="cd5d2-496">В hello **OutputDataset** колонка, щелкните hello срез toosee hello **СРЕЗ данных** колонку для этого среза.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="cd5d2-497">Для этого среза будет указано значение **Запуски операции** .</span><span class="sxs-lookup"><span data-stu-id="cd5d2-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="cd5d2-498">Должна появиться при выполнении среза hello одного действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="cd5d2-499">Если щелкнуть **запуска** hello панели команд, вы можете запустить другое действие запуска для hello того же фрагмента.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="cd5d2-500">При нажатии кнопки при выполнении действия hello, вы видите hello **сведения о выполнении действия** колонка со списком файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="cd5d2-501">Вы видите сообщения в журнале в hello **пользователя\_журнала 0.** файла.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="cd5d2-502">При возникновении ошибки, так как число повторных попыток hello задано too3 hello конвейера или действия JSON см запуске три действия.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="cd5d2-503">При нажатии кнопки при выполнении действия hello, вы видите что tootroubleshoot hello ошибки можно просмотреть файлы журнала hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="cd5d2-504">В списке hello файлов журнала щелкните hello **0.log пользователя**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="cd5d2-505">В правой панели hello являются hello результатов с помощью hello **IActivityLogger.Write** метод.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="cd5d2-506">Проверьте файл system-0.log на наличие любых системных сообщений об ошибках или исключений.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="cd5d2-507">Включить hello **PDB** файлов в ZIP-файле hello таким образом, что сведения об ошибке hello сведения например **стека вызовов** при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="cd5d2-508">Все файлы в ZIP-файле hello hello, пользовательское действие hello должен быть в hello **верхнего уровня** с без вложенных папок.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="cd5d2-509">Убедитесь, что hello **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) и **packageLinkedService** (следует точка toohello Azure хранилище больших двоичных объектов, содержащий hello ZIP-файл) значения toocorrect.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="cd5d2-510">Исправления ошибок и хотите hello срез tooreprocess щелкните правой кнопкой мыши срез hello в hello **OutputDataset** колонку и нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="cd5d2-511">В хранилище BLOB-объектов Azure появится **контейнер** с именем `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="cd5d2-512">Этот контейнер не удаляется автоматически, но ее можно безопасно удалить после завершения тестирования решения hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="cd5d2-513">Аналогичным образом hello решения фабрики данных создает пакет Azure **задания** с именем: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="cd5d2-514">После выполнения тестов hello решение при необходимости можно удалить это задание.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="cd5d2-515">пользовательское действие Hello не использует hello **app.config** файл из пакета.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="cd5d2-516">Таким образом Если код считывает все строки подключения из файла конфигурации hello, он не работает во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="cd5d2-517">Здравствуйте, рекомендуется при использовании пакета Azure, toohold все секреты в **Azure KeyVault**, используйте keyvault hello tooprotect участника службы на основе сертификатов и распространять hello пула tooAzure сертификат.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="cd5d2-518">Здравствуйте настраиваемых действий .NET, то можно получить доступ к секретные данные из hello KeyVault во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="cd5d2-519">Это решение универсальные и масштабируется tooany тип секретного кода, а не только строку подключения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="cd5d2-520">Отсутствует простой обходной путь (но не рекомендуется): можно создать **связанная служба Azure SQL** параметры строки соединения, создать набор данных, использует hello связанной службы и цепочки hello dataset в виде пустой входного набора данных toohello настраиваемых действий .NET.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="cd5d2-521">После этого можно доступа hello связаны строки подключения службы в коде пользовательское действие hello и он должен корректно работать во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="cd5d2-522">Расширение образца hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-522">Extend hello sample</span></span>
<span data-ttu-id="cd5d2-523">Можно расширить этот пример toolearn Дополнительные сведения о функции фабрики данных Azure и пакета Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="cd5d2-524">Например срезы tooprocess в другой диапазон дат, hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="cd5d2-525">Добавьте следующие вложенные папки в hello hello `inputfolder`: 2015-11-16-05 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 и поместите входные файлы в этих папках.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="cd5d2-526">Изменить hello время окончания для конвейера hello из `2015-11-16T05:00:00Z` слишком`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="cd5d2-527">В hello **представление диаграммы**, дважды щелкните hello **InputDataset**и убедитесь, что готовы входные срезы hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="cd5d2-528">Дважды щелкните **OuptutDataset** toosee состояние hello срезы выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="cd5d2-529">Если они находятся в состоянии готовности, проверьте папку вывода hello hello выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="cd5d2-530">Увеличение или уменьшение hello **параллелизма** параметр toounderstand о том, как она влияет на производительность hello решения, особенно hello обработки, которое происходит в пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="cd5d2-531">(См. шаг 4: Создание и запуск конвейера hello для получения дополнительных сведений об hello **параллелизма** параметр.)</span><span class="sxs-lookup"><span data-stu-id="cd5d2-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="cd5d2-532">Создайте пул с большим или меньшим значением для параметра **Maximum tasks per VM** (Максимальное число задач на виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="cd5d2-533">toouse hello новый созданный пул, hello обновления связанной пакетной службы Azure в решении hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="cd5d2-534">(См. шаг 4: Создание и запуск конвейера hello для получения дополнительных сведений об hello **максимально задачи на виртуальную Машину** параметр.)</span><span class="sxs-lookup"><span data-stu-id="cd5d2-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="cd5d2-535">Создайте пул пакетной службы Azure с использованием функции **автомасштабирования** .</span><span class="sxs-lookup"><span data-stu-id="cd5d2-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="cd5d2-536">Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure — hello динамическую настройку вычислительной мощности, используемую приложением.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="cd5d2-537">Образец формулы Hello позволяет достичь следующих поведение hello: при создании пула hello, он начинается с 1 виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="cd5d2-538">Метрика $PendingTasks определяет hello число задач в запущена + active (в очереди) состояние.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="cd5d2-539">Hello формула находит hello среднее число ожидающих задач в hello последние 180 секунд и соответствующим образом задает параметром TargetDedicated.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="cd5d2-540">Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="cd5d2-541">Таким образом как отправлены новые задачи, пул автоматически увеличивается и как задачи завершаются, виртуальные машины становятся свободного один за другим и автоматическое масштабирование hello уменьшается этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="cd5d2-542">startingNumberOfVMs и maxNumberofVMs могут быть скорректированное tooyour потребностей.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="cd5d2-543">Формула автоматического масштабирования:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="cd5d2-544">Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d2-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="cd5d2-545">Если пул hello используется по умолчанию hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello пакетная служба может занять 15-30 минут tooprepare hello виртуальной Машины перед запуском пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="cd5d2-546">Если пул hello использует разные autoScaleEvaluationInterval, hello пакетная служба может получить autoScaleEvaluationInterval + 10 минут.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="cd5d2-547">В решении образец hello hello **Execute** метод вызывает hello **Calculate** метода, который обрабатывает входные данные срез tooproduce срез данных выходные данные.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="cd5d2-548">Можно написать собственный метод tooprocess входные данные и замените вызов метода Calculate hello в методе Execute hello tooyour вызова метода.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="cd5d2-549">Дальнейшие действия: использовать данные hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="cd5d2-550">После обработки данных их можно использовать в интерактивных инструментах, например в **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="cd5d2-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="cd5d2-551">Ниже приведены ссылки toohelp понять Power BI и как toouse его в Azure:</span><span class="sxs-lookup"><span data-stu-id="cd5d2-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="cd5d2-552">Изучение набора данных в Power BI</span><span class="sxs-lookup"><span data-stu-id="cd5d2-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="cd5d2-553">Приступая к работе с Power BI Desktop hello</span><span class="sxs-lookup"><span data-stu-id="cd5d2-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="cd5d2-554">Обновление данных в Power BI</span><span class="sxs-lookup"><span data-stu-id="cd5d2-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="cd5d2-555">Общая информация об Azure и Power BI</span><span class="sxs-lookup"><span data-stu-id="cd5d2-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="cd5d2-556">Ссылки</span><span class="sxs-lookup"><span data-stu-id="cd5d2-556">References</span></span>
* [<span data-ttu-id="cd5d2-557">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="cd5d2-558">Введение tooAzure служба фабрики данных</span><span class="sxs-lookup"><span data-stu-id="cd5d2-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="cd5d2-559">Начало работы с фабрикой данных Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="cd5d2-560">Использование настраиваемых действий в конвейере фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="cd5d2-561">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="cd5d2-562">Основные сведения о пакетной службе Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="cd5d2-563">Обзор функций пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="cd5d2-564">Создание и управление учетной записью пакетной службы Azure в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cd5d2-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="cd5d2-565">Начало работы с библиотекой Пакетной службы Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="cd5d2-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
